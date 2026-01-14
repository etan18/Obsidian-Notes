### todo
- sequential combine of catBoost + K29
	- Try: no split (train both on same data), with split
	- https://chatgpt.com/c/69531e49-388c-8329-ad7f-be828e9b167e
- [X] go back to phi caching w default hyperparams
	- Sanity check: theta-caching and phi-caching on the same dataset produce same results
- clean up script
	- don't save joblib --- save only for final model
	- [X] log -1 error tensorboard
		- why use tensorboard at all?

---
## data addition dilemma

**baselines:**
fit a model to all data (across all hospitals)
- model: https://catboost.ai/ 
- add a feature that tells you what hospital the patient is from
	- run one with and one without the feature included
	- theoretically, the tree could split by hospital feature at the first node, then subtrees would be per-hospital classifiers. or, would at least group together similar hospitals.
- look at accuracy, auc, and r^2

one-to-one train test per-hospital


**11/7**
propose a method
- pool all data, run this thing, you'll do no worse than the one-to-one baseline

outstanding questions
- hosp 73 diagnostic: why acc so much higher than the baseline but R^2 so bad?
- from baselines: why are we not lower bounded by one-to-one? 
- look at feature splits

Baseline
- run a kernel method --- LR on top of mapped features (https://scikit-learn.org/stable/modules/generated/sklearn.kernel_approximation.RBFSampler.html)


**11/14**
- whole hospital similarity scores
- look at feature splits
- Idea: Section 6 of https://arxiv.org/pdf/2506.11848

**11/20**
Model ([[defensive forecasting]])
- Pass features through feature map ($\Phi$) , then concatenate one-hot hosp_id features
	- Algorithm 4 in paper 
	- Essentially two kernels, one for the features, one for the hospital IDs (to check if they belong to the same hospital)
- Idea: minimize 13 loss functions (1 per hospital, then overall), such that we can treat each hospital as outcome indistinguishable
	- Do anti-correlation search on the kernel (provided by Juanky)

**12/5**
- K29 algorithm: base runs, hyper-parameter sweep
- Initial runs on 1000 or so data points.

**12/12**
- Potential function can be rewritten w/ caching (current is incorrect)
S = self_term + sum_{i=1}^t <RFF(x), RFF(x_i) (y_i-p_i)>  +  <RFF(x), RFF(x_i)(y_i - p_i)>  1 {g(x) = g(x_i)})
S = self_term + sum_{i=1}^t <RFF(x), GLOBAL >  +  <RFF(x), COUNTER FOR i>
- GLOBAL = sum_{i=1}^t RFF(x_i) (y_i-p_i)
- Maintain a counter of per-hospital values
	- COUNTER for HOSPITAL j =  sum_{i belongs to hospital j}^t RFF(x_i) (y_i-p_i)

---

mitigating bias via "forgetting"
- some type of perturbation that makes distribution uniform/random along some biased dimension
- task vectors

yes-man 
- show llm sensitivities to biased prompts --- e.g. "why is this statement true?" vs. "why is this statement false?" vs. "why is this statement true or false?"

problems with representing patients as embeddings
- Domain-specific embeddings: https://arxiv.org/html/2409.18511v3

---
### psych

Tasks:
1. Exam 2 essay section:  Need 3 people 3 x 3 20
2. Anatomy Quiz: Write and Provide review sheet 1 5

TODO:
- [ ] get cogneuro textbook from ivry's office (can walk in and take it)
- [x] set one hour of office hours (time + location)

section:
- quick overview (slides) of week's content + answer questions from lectures
- assigned a reader article every week, split into 4-5 groups
	- each group assigned a figure, one group is the summary group
	- summary: pretend you are the first author of this paper, take 2 minutes to summarize 1) what's the paper, 2) what's the insight, 3) why do we care
	- each figure: why is this figure in the paper? what does it say, what does it add?
	- facilitate discussion!
- count for 10% of overall grade
	- 70% determined by participation (composite of attendance and contribution in attended section)
		- semi-subjective
	- 30%: based on RPP (nothing to do)


```
class VocabComparator:
    """
    Compare vocabulary distributions between two text datasets.
    Supports multiple tokenization strategies and identifies discriminative markers.
    """
    
    def __init__(self, tokenization_method='word', remove_punctuation=True, 
                 lowercase=True, min_freq=2):
        """
        Initialize the comparator with preprocessing options.
        
        Parameters:
        -----------
        tokenization_method : str
            'word': word-level tokenization
            'subword': character n-gram tokenization (2-4 grams)
            'mixed': combination of words and character bigrams
        remove_punctuation : bool
            Whether to remove punctuation marks
        lowercase : bool
            Whether to convert to lowercase
        min_freq : int
            Minimum frequency threshold for including tokens
        """
        self.tokenization_method = tokenization_method
        self.remove_punctuation = remove_punctuation
        self.lowercase = lowercase
        self.min_freq = min_freq
        self.vocab1 = None
        self.vocab2 = None
        self.vocab1_counts = None
        self.vocab2_counts = None
        
    def preprocess_text(self, text: str) -> str:
        """Basic text preprocessing."""
        if pd.isna(text):
            return ""
        
        text = str(text)
        
        if self.lowercase:
            text = text.lower()
        
        # Normalize whitespace
        text = re.sub(r'\s+', ' ', text).strip()
        
        return text
    
    def tokenize_word(self, text: str) -> List[str]:
        """Word-level tokenization."""
        if self.remove_punctuation:
            # Remove punctuation but keep medical abbreviations
            tokens = re.findall(r'\b\w+\b', text)
        else:
            # Keep punctuation attached to words
            tokens = re.findall(r'\S+', text)
        return tokens
    
    def tokenize_subword(self, text: str) -> List[str]:
        """Character n-gram tokenization (2-4 grams)."""
        if self.remove_punctuation:
            text = re.sub(r'[^\w\s]', '', text)
        
        tokens = []
        words = text.split()
        for word in words:
            # Add character n-grams
            for n in [2, 3, 4]:
                if len(word) >= n:
                    tokens.extend([word[i:i+n] for i in range(len(word)-n+1)])
        return tokens
    
    def tokenize_mixed(self, text: str) -> List[str]:
        """Mixed tokenization: words + character bigrams."""
        word_tokens = self.tokenize_word(text)
        
        # Add character bigrams from each word
        char_tokens = []
        for word in word_tokens:
            if len(word) >= 2:
                char_tokens.extend([word[i:i+2] for i in range(len(word)-1)])
        
        return word_tokens + char_tokens
    
    def tokenize(self, text: str) -> List[str]:
        """Apply selected tokenization method."""
        text = self.preprocess_text(text)
        
        if self.tokenization_method == 'word':
            return self.tokenize_word(text)
        elif self.tokenization_method == 'subword':
            return self.tokenize_subword(text)
        elif self.tokenization_method == 'mixed':
            return self.tokenize_mixed(text)
        else:
            raise ValueError(f"Unknown tokenization method: {self.tokenization_method}")
    
    def extract_vocab(self, texts: List[str]) -> Counter:
        """Extract vocabulary from a list of texts."""
        all_tokens = []
        for text in texts:
            tokens = self.tokenize(text)
            all_tokens.extend(tokens)
        
        vocab = Counter(all_tokens)
        
        # Filter by minimum frequency
        vocab = Counter({k: v for k, v in vocab.items() if v >= self.min_freq})
        
        return vocab
    
    def fit(self, df: pd.DataFrame, text_columns: List[str], 
            note_df: pd.DataFrame, note_column: str):
        """
        Fit the comparator on two datasets.
        
        Parameters:
        -----------
        df : pd.DataFrame
            First dataset with multiple text columns
        text_columns : List[str]
            List of column names containing text in df
        note_df : pd.DataFrame
            Second dataset
        note_column : str
            Column name containing text in note_df
        """
        # Extract texts from first dataset
        texts1 = []
        for col in text_columns:
            texts1.extend(df[col].fillna('').tolist())
        
        # Extract texts from second dataset
        texts2 = note_df[note_column].fillna('').tolist()
        
        # Build vocabularies
        print("Building vocabulary for dataset 1...")
        self.vocab1_counts = self.extract_vocab(texts1)
        self.vocab1 = set(self.vocab1_counts.keys())
        
        print("Building vocabulary for dataset 2...")
        self.vocab2_counts = self.extract_vocab(texts2)
        self.vocab2 = set(self.vocab2_counts.keys())
        
        print(f"\nDataset 1 vocabulary size: {len(self.vocab1):,}")
        print(f"Dataset 2 vocabulary size: {len(self.vocab2):,}")
        print(f"Shared vocabulary size: {len(self.vocab1 & self.vocab2):,}")
        
        return self
    
    def compute_discriminative_markers(self, top_n=50, method='chi2') -> pd.DataFrame:
        """
        Identify tokens most indicative of each dataset.
        
        Parameters:
        -----------
        top_n : int
            Number of top markers to return for each dataset
        method : str
            'chi2': Chi-square test (balances frequency and specificity)
            'log_odds': Log odds ratio (emphasizes relative preference)
            'pmi': Pointwise Mutual Information (emphasizes distinctiveness)
            'frequency': Simple frequency difference (high-frequency words)
        
        Returns:
        --------
        pd.DataFrame with discriminative markers and their statistics
        """
        # Get all unique tokens
        all_tokens = self.vocab1 | self.vocab2
        
        results = []
        
        total1 = sum(self.vocab1_counts.values())
        total2 = sum(self.vocab2_counts.values())
        
        for token in all_tokens:
            count1 = self.vocab1_counts.get(token, 0)
            count2 = self.vocab2_counts.get(token, 0)
            
            # Compute relative frequencies
            freq1 = count1 / total1 if total1 > 0 else 0
            freq2 = count2 / total2 if total2 > 0 else 0
            
            # Chi-square test
            contingency = np.array([
                [count1, count2],
                [total1 - count1, total2 - count2]
            ])
            chi2, p_value, _, _ = chi2_contingency(contingency)
            
            # Log odds ratio (emphasizes relative preference)
            odds1 = (count1 + 1) / (total1 - count1 + 1)
            odds2 = (count2 + 1) / (total2 - count2 + 1)
            log_odds_ratio = np.log(odds1 / odds2)
            
            # Pointwise Mutual Information (emphasizes distinctiveness)
            # PMI measures how much more likely a word appears in one dataset vs random
            p_token = (count1 + count2) / (total1 + total2)
            p_ds1 = total1 / (total1 + total2)
            p_ds2 = total2 / (total1 + total2)
            
            pmi_ds1 = np.log2((freq1 / p_token) / p_ds1) if freq1 > 0 and p_token > 0 else -np.inf
            pmi_ds2 = np.log2((freq2 / p_token) / p_ds2) if freq2 > 0 and p_token > 0 else -np.inf
            pmi_score = pmi_ds1 - pmi_ds2  # Positive = DS1, Negative = DS2
            
            # Frequency difference (absolute)
            freq_diff = freq1 - freq2
            
            # Combined score based on method
            if method == 'chi2':
                score = chi2  # Use chi2 directly, sort by magnitude
            elif method == 'log_odds':
                score = abs(log_odds_ratio)
            elif method == 'pmi':
                score = abs(pmi_score)
            elif method == 'frequency':
                score = abs(freq_diff)
            else:
                raise ValueError(f"Unknown method: {method}")
            
            results.append({
                'token': token,
                'count_ds1': count1,
                'count_ds2': count2,
                'freq_ds1': freq1,
                'freq_ds2': freq2,
                'freq_diff': freq_diff,
                'freq_ratio': freq1 / (freq2 + 1e-10),
                'log_odds_ratio': log_odds_ratio,
                'chi2': chi2,
                'p_value': p_value,
                'pmi_score': pmi_score,
                'score': score,
                'dataset_preference': 1 if (log_odds_ratio if method != 'pmi' else pmi_score) > 0 else 2
            })
        
        results_df = pd.DataFrame(results)
        
        # Sort by score (descending for all methods)
        results_df = results_df.sort_values('score', ascending=False)
        
        # Get top markers for each dataset
        ds1_markers = results_df[results_df['dataset_preference'] == 1].head(top_n)
        ds2_markers = results_df[results_df['dataset_preference'] == 2].head(top_n)
        
        return pd.concat([ds1_markers, ds2_markers]).sort_values('score', ascending=False)
    
    def plot_marker_comparison(self, markers_df: pd.DataFrame, top_n=20, method='chi2'):
        """Visualize top discriminative markers."""
        # Get top markers for each dataset
        ds1_markers = markers_df[markers_df['dataset_preference'] == 1].head(top_n)
        ds2_markers = markers_df[markers_df['dataset_preference'] == 2].head(top_n)
        
        fig, axes = plt.subplots(1, 2, figsize=(16, 8))
        
        # Determine what to plot based on method
        if method == 'chi2':
            plot_metric1 = ds1_markers['log_odds_ratio'].tolist()
            plot_metric2 = ds2_markers['log_odds_ratio'].abs().tolist()
            xlabel = 'Log Odds Ratio'
        elif method == 'log_odds':
            plot_metric1 = ds1_markers['log_odds_ratio'].tolist()
            plot_metric2 = ds2_markers['log_odds_ratio'].abs().tolist()
            xlabel = 'Log Odds Ratio'
        elif method == 'pmi':
            plot_metric1 = ds1_markers['pmi_score'].tolist()
            plot_metric2 = ds2_markers['pmi_score'].abs().tolist()
            xlabel = 'PMI Score'
        elif method == 'frequency':
            plot_metric1 = ds1_markers['freq_diff'].tolist()
            plot_metric2 = ds2_markers['freq_diff'].abs().tolist()
            xlabel = 'Frequency Difference'
        
        # Dataset 1 markers
        ax1 = axes[0]
        tokens1 = ds1_markers['token'].tolist()
        ax1.barh(range(len(tokens1)), plot_metric1, color='steelblue')
        ax1.set_yticks(range(len(tokens1)))
        ax1.set_yticklabels(tokens1)
        ax1.set_xlabel(xlabel)
        ax1.set_title(f'Top {top_n} Markers for Dataset 1')
        ax1.invert_yaxis()
        
        # Dataset 2 markers
        ax2 = axes[1]
        tokens2 = ds2_markers['token'].tolist()
        ax2.barh(range(len(tokens2)), plot_metric2, color='coral')
        ax2.set_yticks(range(len(tokens2)))
        ax2.set_yticklabels(tokens2)
        ax2.set_xlabel(f'|{xlabel}|')
        ax2.set_title(f'Top {top_n} Markers for Dataset 2')
        ax2.invert_yaxis()
        
        plt.tight_layout()
        plt.show()
    
    def get_summary_stats(self) -> Dict:
        """Get summary statistics about vocabularies."""
        return {
            'vocab_size_ds1': len(self.vocab1),
            'vocab_size_ds2': len(self.vocab2),
            'shared_vocab': len(self.vocab1 & self.vocab2),
            'unique_to_ds1': len(self.vocab1 - self.vocab2),
            'unique_to_ds2': len(self.vocab2 - self.vocab1),
            'total_tokens_ds1': sum(self.vocab1_counts.values()),
            'total_tokens_ds2': sum(self.vocab2_counts.values()),
            'overlap_ratio': len(self.vocab1 & self.vocab2) / len(self.vocab1 | self.vocab2)
        }


# Example usage:
# Initialize with different configurations

# Word-level, remove punctuation
comparator = VocabComparator(
    tokenization_method='word',
    remove_punctuation=True,
    lowercase=True,
    min_freq=2
)

comparator.fit(df, text_columns, note_df, 'note_text')

# Get discriminative markers using different methods:

# 1. CHI-SQUARE (default): Balances frequency and specificity
#    Good for: Finding words that are both common AND distinctive
markers_chi2 = comparator.compute_discriminative_markers(top_n=50, method='chi2')
print(markers_chi2.head(20))
comparator.plot_marker_comparison(markers_chi2, top_n=20, method='chi2')

# 2. LOG ODDS: Emphasizes relative preference (ratio-based)
#    Good for: Finding words that are much more likely in one dataset
#    Will find words even if rare, as long as they're strongly skewed
markers_log_odds = comparator.compute_discriminative_markers(top_n=50, method='log_odds')
comparator.plot_marker_comparison(markers_log_odds, top_n=20, method='log_odds')

# 3. PMI (Pointwise Mutual Information): Emphasizes distinctiveness
#    Good for: Finding words that are highly specific to one dataset
#    Great for rare but highly indicative markers
markers_pmi = comparator.compute_discriminative_markers(top_n=50, method='pmi')
comparator.plot_marker_comparison(markers_pmi, top_n=20, method='pmi')

# 4. FREQUENCY: Simple frequency difference
#    Good for: Finding the most common words in each dataset
#    Will heavily favor high-frequency words
markers_freq = comparator.compute_discriminative_markers(top_n=50, method='frequency')
comparator.plot_marker_comparison(markers_freq, top_n=20, method='frequency')

# Get summary statistics
stats = comparator.get_summary_stats()
print("\nSummary Statistics:")
for k, v in stats.items():
    print(f"{k}: {v:,}")

```
