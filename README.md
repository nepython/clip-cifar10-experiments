# Exploring multimodal vision-language models with CLIP

## `1. Implementation Overview`
Our implementation follows the evaluation protocols detailed in the original CLIP paper [1] and leverages the official OpenAI CLIP repository. Two primary evaluation modes were adopted:
Zero-shot classification: Where class labels are expressed as natural language prompts and image-text similarity is used for prediction.
Linear probing: Where image features from CLIP’s visual encoder are frozen, and a linear classifier is trained on top using CIFAR-10 training data.
We used the "ViT-B/32" model variant and reported the following performances:
| Method        | Accuracy (reported) | Accuracy (observed) |
| ------------- | ------------------- | ------------------- |
| Zero-shot     | 89.83%*             | 89.59%              |
| Linear probe  | 95.1%               | 95.02%              |
While attempts were made to get the same results as reported, a small reduction was observed.
*This is based on statistics shared by OpenClip, a third part library

## `2. Experimental Studies`
To deepen our understanding of CLIP’s zero-shot performance, we conducted several experiments exploring variations in:
* **Text Descriptions**: We evaluated the effect of altering the prompt structure (e.g., “This is a photo of a dog” vs. “An image showing a dog”). The best performance (89.59%) was observed with the variant “An image showing a {label}.”
* **Class Names**: Replacing the original CIFAR-10 class names with synonyms or closely related terms (e.g., “airplane” → “aircraft”, “dog” → “canine”) produced a small improvement, highlighting CLIP’s sensitivity to prompt formulation.
Combined Prompts: We combined the best-performing text structure with the best-performing class variants, expecting additive gains. However, the resulting accuracy (89.31%) was slightly lower than the standalone best cases.

## `3. Augmentation-based Attempt`
We experimented with using two image versions, i) the original and ii) an augmented one (horizontal flip + rotation) and averaged their cosine similarity scores with the text embeddings. This ensemble-like approach slightly reduced accuracy (from 89.59% to 89.42%), suggesting the limitations of naive augmentation strategies when working with pre trained contrastive models like CLIP.

-----------------------------------
More details in the report.