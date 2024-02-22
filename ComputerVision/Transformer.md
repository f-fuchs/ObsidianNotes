## Self-Attention

### Theory

The fundamental operation of any transformer architecture is the *self-attention* operation.

We'll explain where the name "self-attention" comes from later. For now, don't read too much in to it.

Self-attention is a sequence-to-sequence operation: a sequence of vectors goes in, and a sequence of vectors comes out. Let’s call the input vectors $\vec{𝐱_1},\vec{𝐱_2},…,\vec{𝐱_t}$ and the corresponding output vectors $\vec{y_1},\vec{y_2},…,\vec{y_t}$. The vectors all have dimension $k$.

To produce output vector $\vec{𝐲_i}$, the self attention operation simply takes *a weighted average over all the input vectors*

$$
\vec{𝐲_i}=\sum_{j=1}^{k} w_{ij} \vec{𝐱_j}
\text{.}
$$


Where the weights sum to one over all $j$. The weight $w_{ij}$ is not a parameter, as in a normal neural net, but it is *derived* from a function over $\vec{𝐱_i}$ and $\vec{𝐱_j}$. The simplest option for this function is the dot product:

$$
w_{ij}^{′}=\vec{𝐱_i}^T \vec{𝐱_j}= \sum_{l=1}^{k} 𝐱_{il} 𝐱_{jl}
\text{.}
$$


Where $\vec{𝐱_i}$ is the input vector at the same position as the current output vector $\vec{𝐲_i}$. For the next output vector, we get an entirely new series of dot products, and a different weighted sum.

The dot product gives us a value anywhere between negative and positive infinity, so we apply a *softmax* to map the values to $[0,1]$ and to ensure that they sum to $1$ over the whole sequence:
$$
w_{ij} = \frac{e^{w_{ij}^{′}}}{\sum_{j=1}^{k} e^{w_{ij}^{′}}}
\text{.}
$$

![[self-attention.svg]]

If we combine our sequence of vectors to a matrix $X=\begin{bmatrix} \vec{𝐱_1}^T \\ \vec{𝐱_2}^T \\ … \\ \vec{𝐱_t}^T \end{bmatrix}$ with dimension $(t, k)$ , we can calculate all weights by multiplying $X$ with its transpose $X^T$. Therefore the raw weight matrix $W^{′}=X \times X^T$ has dimension $(t, t)$ where $W^{′}_{ij}$ is the same as $w_{ij}^{′}$ defined above. Next we can rescale $W^{′}$ by applying the  *softmax* function *row-wise*.

### Intuition

Let’s say we are faced with a sequence of words. To apply self-attention, we simply assign each word $t$ in our vocabulary an *embedding vector* $\vec{x_t}$ (the values of which we’ll learn). This is what’s known as an *embedding layer* in sequence modeling. It turns the word sequence the,cat,walks,on,the,street into the vector sequence $\vec{x}_{the}$, $\vec{x}_{cat}$, $\vec{x}_{walks}$, $\vec{x}_{on}$, $\vec{x}_{the}$, $\vec{x}_{street}$.

If we feed this sequence into a self-attention layer, the output is another sequence of vectors $\vec{y}_{the}$, $\vec{y}_{cat}$, $\vec{y}_{walks}$, $\vec{y}_{on}$, $\vec{y}_{the}$, $\vec{y}_{street}$, where $\vec{y}_{cat}$ is a weighted sum over all the embedding vectors in the first sequence, weighted by their (normalized) dot-product with $\vec{x}_{cat}$.

Since we are *learning* what the values in $\vec{x_t}$ should be, how "related" two words are is entirely determined by the task. In most cases, the definite article *the* is not very relevant to the interpretation of the other words in the sentence; therefore, we will likely end up with an embedding $\vec{x_t}$ that has a low or negative dot product with all other words. On the other hand, to interpret what *walks* means in this sentence, it's very helpful to work out *who* is doing the walking. This is likely expressed by a noun, so for nouns like *cat* and verbs like *walks*, we will likely learn embeddings $\vec{x}_{cat}$ and $\vec{x}_{walks}$ that have a high, positive dot product together.

This is the basic intuition behind self-attention. The dot product expresses how related two vectors in the input sequence are, with “related” defined by the learning task, and the output vectors are weighted sums over the whole input sequence, with the weights determined by these dot products.

### Properties
- There are no parameters (yet). What the basic self-attention actually does is entirely determined by whatever mechanism creates the input sequence. Upstream mechanisms, like an embedding layer, drive the self-attention by learning representations with particular dot products.
- Self attention sees its input as a *set*, not a sequence. If we permute the input sequence, the output sequence will be exactly the same, except permuted also (i.e. self-attention is *permutation equivariant*). Therefore self-attention by itself actually *ignores* the sequential nature of the input.


### Resources
- https://peterbloem.nl/blog/transformers

## Resources

- Original Paper Attention is all you need: https://arxiv.org/pdf/1706.03762.pdf
- Reddit Threads:
	- https://www.reddit.com/r/MachineLearning/comments/pkedi4/d_resources_for_understanding_the_original/
	- https://www.reddit.com/r/learnmachinelearning/comments/lz91o5/i_finally_understand_transformer_neural_networks_d/
	- https://www.reddit.com/r/MachineLearning/comments/qidpqx/d_how_to_truly_understand_attention_mechanism_in/
- Tutorials:
	- http://jalammar.github.io/illustrated-transformer/
	- https://peterbloem.nl/blog/transformers
