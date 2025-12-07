### Qualitative Analysis Part 1: Image & Text Retrieval

* Report 2 examples where image retrieval fails. For each example, briefly describe why you think this failure might have occurred.

**Example 1**
Caption: Harlem resident Gladys Bentley was renowned for her blues songs about her affairs with women.
![[Pasted image 20251204123222.png]]

I think this failure occurred because it requires prior domain knowledge of who Gladys Bentley is and what she looks like. Additionally, even though the photo is signed with her name, the image processor likely cannot process text in image data.

**Example 2**
Caption: Karl Bodmer, Fort Pierre and the Adjacent Prairie, c. 1833
![[Pasted image 20251204123427.png]]

Although the caption provides historical context of the significance of the image, it does not necessarily relate too well to the actual image composition, making it difficult for the model to retrieve based on caption alone. The way it is described, one would expect the man, Karl Bodmer, and the fort to be more prominently featured. 

* Report 2 examples where the paired caption scores more highly than the paired description for an image. Are there any patterns you observe that determine whether the caption or the description scores more highly?

**Example 1**
Caption: Two USB3.0 Standard-A receptacles (left) and two USB2.0 Standard-A receptacles (right) on a computer's front panel 

Description: Rectangular opening where the width is twice the height. The opening has a metal rim, and within the opening a flat rectangular bar runs parallel to the top side.
![[Pasted image 20251204123850.png]]

**Example 2**

Caption: Trabant 1.1 with VW Polo four-stroke engine 
Description: Two-door sedan with a man standing behind it

![[Pasted image 20251204123923.png]]

In both of the examples provided, the caption offers more precise descriptions of the items in the photo, whereas the description is quite vague. For example, "Trabant 1.1." vs. "two-door sedan" and "USB3.0 Standard-A" vs. "rectangular opening". This dataset may contain multiple images matching the broad descriptions of these examples, causing description-based retrieval to fail. These examples also suggest that the model does have some more specific domain knowledge, such as knowledge of specific car models or port types. The success of caption-based retrieval is then possible dependent on the model and the data the model was trained on.


## Qualitative Analysis Part 2: RSA

23 / 89 of the previously incorrect samples were now correct by RSA.

**Discuss 1 qualitative example that provides an intuition of why RSA fixes these issues (e.g. compare the literal listener probabilities to the pragmatic listener probabilities and think about why they changed).**

Caption: The Missouri in North Dakota, which was the furthest upstream that French explorers traveled on the river

![[Pasted image 20251205134028.png]]

This image is quite vague, it's difficult to tell which river this is and why it's significant. This is probably why a literal listener fails to retrieve the image based on the given caption. However, when we consider the pragmatics caption itself against the set of available images to retrieve, it becomes much more plausible why this caption would go along with this image. 

While this image is not clearly the Missouri River, it is more likely to be the Missouri River than any other image in the dataset, which is why a pragmatic listener would choose it.



## [BONUS] Qualitative Analysis Part 3: Captioning

One qualitative trend I observe is that the pragmatic captions tend to be more descriptive than the literal captions. Two examples of this trend are included below. While in both examples the literal captions are accurate to the image, they are quite vague, whereas their pragmatic counterparts are more precise, allowing for more confident and accurate retrieval. For example, "a drawing" becomes "a *black and white* drawing". 

![[Pasted image 20251206184533.png]]
Literal caption: a drawing of a boat with a man on it 
Pragmatic caption: the sea is a black and white drawing with a boat in the middle

![[Pasted image 20251206184607.png]]
Literal caption: a group of people sitting in a room 
Pragmatic caption: a group of people sit on couches in a room with two men reading and one woman sitting on

A second trend I observe is that when multiple images of similar subjects exist in the dataset, the literal captions tend to be quite similar. In comparison, the pragmatic captions tend to differ more greatly, making it easier for a listener to differentiate between similar images. An example is provided below of two images of men on bikes. While one caption stays the same, the other becomes more descriptive to include that the image is black and white.

![[Pasted image 20251206185620.png]]
Literal caption: a man riding a bike down a road 
Pragmatic caption: black and white photograph of a man riding a bike

![[Pasted image 20251206185638.png]]
Literal caption: a man riding a bike down a street 
Pragmatic caption: a man riding a bike down a street
