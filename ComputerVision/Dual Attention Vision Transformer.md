
Dual Attention Vision Transformers (DaViT) is a vision transformer architecture that is able to capture global context while maintaining computational efficiency. It uses the self-attention mechanisms with both "spatial tokens" and "channel tokens". 

Since each channel token contains an abstract representation of the entire image, the channel attention naturally captures global interactions and representations by taking all spatial positions into account when computing attention scores between channels. (ii) The spatial attention refines the local representations by performing fine-grained interactions across spatial locations, which in turn helps the global information modeling in channel attention.
$$
Spatial Attention(Q, K, V) = softmax(\frac{QK^T}{\sqrt{d_k}})V
$$
$$
Channel Attention(Q, K, V) = \left(softmax\left(\frac{K^T V}{\sqrt{d_k}}\right)Q^T\right)^T
$$

![](https://github.com/dingmyu/davit/raw/main/figures/teaser.png)
![](https://github.com/dingmyu/davit/raw/main/figures/architecture.png)