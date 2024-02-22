# Self-Attention

The fundamental operation of any transformer architecture is the *self-attention* operation.

We'll explain where the name "self-attention" comes from later. For now, don't read too much in to it.

Self-attention is a sequence-to-sequence operation: a sequence of vectors goes in, and a sequence of vectors comes out. Let’s call the input vectors $\vec{𝐱_1},\vec{𝐱_2},…,\vec{𝐱_t}$ and the corresponding output vectors $\vec{y_1},\vec{y_2},…,\vec{y_t}$. The vectors all have dimension $k$.

To produce output vector $\vec{𝐲_i}$, the self attention operation simply takes *a weighted average over all the input vectors*

$$
\vec{𝐲_i}=\sum_{j=1}^{k} w_{ij} \vec{𝐱_j}.
$$

Where the weights sum to one over all $j$. The weight $w_{ij}$ is not a parameter, as in a normal neural net, but it is *derived* from a function over $\vec{𝐱_i}$ and $\vec{𝐱_j}$. The simplest option for this function is the dot product:

# Resources

- Original Paper Attention is all you need: https://arxiv.org/pdf/1706.03762.pdf
- Reddit Threads:
	- https://www.reddit.com/r/MachineLearning/comments/pkedi4/d_resources_for_understanding_the_original/
	- https://www.reddit.com/r/learnmachinelearning/comments/lz91o5/i_finally_understand_transformer_neural_networks_d/
	- https://www.reddit.com/r/MachineLearning/comments/qidpqx/d_how_to_truly_understand_attention_mechanism_in/
- Tutorials:
	- http://jalammar.github.io/illustrated-transformer/
	- https://peterbloem.nl/blog/transformers
