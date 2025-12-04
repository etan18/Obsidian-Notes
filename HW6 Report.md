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