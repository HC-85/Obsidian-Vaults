#Pending #Paper 
https://arxiv.org/pdf/2205.11380.pdf

Dropping 48 out of 110M parameters in BERT-base drops its performance by nearly 30% on some tests.
The magnitude of hidden state coefficients of outlier dimensions correlates with the frequency of encoded tokens in pre-training data.
It also contributes to the “vertical” self-attention pattern enabling the model to focus on the special tokens.
To decrease anisotropicity one needs pre-training schemas to take into account the skewedness of token distributions.

Transformer models are overparameterized, allowing one to heavily prune without much performance drop.
Nonetheless this is not the case for a few parameters in the output element whose magnitude is unusually large (consistently in the same dimension across multiple layers).
These dimensions affect the vector representation of different tokens in the same way, making the embedding space less isotropic and thus reducing its representational power
Direct link between outliers and the frequency of tokens in the pre-training data was found, as well as self-attention focusing on special tokens.

In ViT it was found that the degradation was higher, the more complex the task. 

Models whose outliers were disabled tend to predict tokens which are more frequent, that is, they have lower perplexity.

Tokens with high hidden state outlier dimension value tend to also have high average value over attention columns.

Outliers in protein and audio Transformers could not be found, possibly due to a smaller vocabulary.

It has been shown that low frequency tokens lie further away from high frequency ones in the embedding space.

Outlier contributes to the vertical attention patterns, which is consistent with the attention being a bilinear form.