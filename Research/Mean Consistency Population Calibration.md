**Setup:**
- $\mu_a$  : mean/expected value of outcome labels $Y_a$ in source $a$
- $\mu_b$   : mean/expected value of outcome labels $Y_b$ in source $b$
- $f_{\mathcal{D}_a}$ : predictor trained on source $a$ 
- $\mu_{f_{\mathcal{D}_a}}$: mean/expected value of predictions made by $f_{\mathcal{D}_a}$ 

We care specifically about the performance of the predictor on $a$.

Base: start with a predictor $f_{\mathcal{D}_{a+b}}$, where
- Source $a$: target subgroup (e.g. White) within Hos N
- Source $b$: all other subgroups (e.g. Black & Other) within Hos N

Original mean consistency value is $|\mu_{f_{\mathcal{D}_{a+b}}} - \mu_{a}|$ 
- Case 1: $|\mu_{f_{\mathcal{D}_{a+b}}} - \mu_{a}| = 0$ , our predictor is mean consistent
- Case 2: $|\mu_{f_{\mathcal{D}_{a+b}}} - \mu_{a}| > 0$, our predictor is not mean consistent

Visualization: mean consistency of each subgroup across all hospitals and correlation with subgroup AUC (left) and subgroup ACC( right). Accuracy is highly negatively correlated with mean consistency across all subgroups.

![[Pasted image 20250124163747.png]]

### Data Addition
Add source $c$ (could be a whole hospital or subgroup from a hospital) and train predictor $f_{\mathcal{D}_{a+b+c}}$. The new mean consistency value is $|\mu_{f_{\mathcal{D}_{a+b+c}}} - \mu_{a}|$.

**Visualization**: Change in mean consistency vs. Change in subgroup AUC(left)/ACC(right). 
- Change in mean consistency formula:
$$|\hat\mu_{f_{\mathcal{D}_{a+b+c}}} - \mu_{a}| - |\mu_{f_{\mathcal{D}_{a+b}}} - \mu_{a}| \tag{1}$$
##### Whole Hospital Data Addition

![[Pasted image 20250124164146.png]]

##### Subgroup Level Data Addition
![[Pasted image 20250127172635.png]]

#### Mean Consistency without Predictor Mean
In practice, the difference in mean consistency formula used in the previous section is infeasible because it requires each predictor to be trained. In this section, we will see if it is feasible to substitute $\mu_{f_{\mathcal{D}_{a+b+c}}}$ with a term that only uses the means of the data sources ($\mu_a$, $\mu_b$, $\mu_c$) and the mean of pre-existing predictors ($\mu_{f_{\mathcal{D}_{a+b}}}$). 

Where $c$ is the added source, our new mean consistency metric is
$$\bigg|\frac{\mu_{f_{\mathcal{D}_{a+b}}} + \mu_c}{2} - \mu_{a} \bigg| - |\mu_{f_{\mathcal{D}_{a+b}}} - \mu_{a}| \tag{2}$$

**Visualization**: Correlation between Equation (1) and Equation (2) to see if it's a compatible approximation
![[Pasted image 20250130134116.png]]

>[!question] Do we need to take into account the size of each source?

If yes, then denoting $|a|$ as the size of source $a$, we would have
- $p_c = \frac{|c|}{|a+b+c|}$
- $p_{a+b} = \frac{|a+b|}{|a+b+c}$ 

$$\bigg|p_{a+b} \cdot \mu_{f_{\mathcal{D}_{a+b}}} + p_c \cdot \mu_c - \mu_{a} \bigg| - |\mu_{f_{\mathcal{D}_{a+b}}} - \mu_{a}| \tag{3}$$

**Visualization:** Correlation between Equation (1) and Equation (3) to see if it's a compatible approximation 

![[Pasted image 20250130144817.png]]

The above plots show that there is a statistically significant positive correlation between the true mean consistency change (Equation 1) and the proxy expressions (Equations 2 and 3).

However, when we recreate the data addition plots using Equations 2 and 3, the correlation between mean consistency and ACC change goes away for the Black and White subgroups:

![[Pasted image 20250130145651.png]]

**02/04**: Instead of using these weighted average methods, we instead train a Linear Regression model to create an estimator $\hat{\mu}_{f_{\mathcal{D}_{a+b+c}}}$ using features
- $\mu_{f_{\mathcal{D}_{a+b}}}$, pred mean base
- $\mu_a$, true mean base
- $\mu_c$, true mean added
- $|c|$, size of added source

This resulted in a statistically significant negative correlation between the mean discrepancy correction and the ACC improvement.

![[Pasted image 20250204135243.png]]

---
## Correlations by Test Hospital
In this section, re-examine all the plots above, instead grouping by **test hospital** as opposed to target subgroup.

**Whole hospital data addition**
![[Pasted image 20250130163424.png]]

**Subgroup only data addition**
![[Pasted image 20250130164142.png]]
![[Pasted image 20250130164203.png]]


![[Pasted image 20250130165515.png]]

![[Pasted image 20250130165409.png]]
![[Pasted image 20250130165800.png]]



## LGBM
![[Pasted image 20250206015712.png]]
