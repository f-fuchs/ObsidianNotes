

## Transformer Block

A transformer block consist of more than just self attention, namely the block applies, in sequence: a self attention layer, layer normalization, a [[Feedforward Neural Network (FNN)|feed forward layer]] (a single MLP applied **independently** to each vector), and another layer normalization. Residual connections are added around both, before the normalization. The order of the various components is not set in stone; the important thing is to combine self-attention with a local feedforward, and to add normalization and residual connections. 

![[transformer-block.svg]]


## Resources

### Used
- Original Paper Attention is all you need: https://arxiv.org/pdf/1706.03762.pdf
-  https://peterbloem.nl/blog/transformers

### Interesting other resources
- Reddit Threads:
	- https://www.reddit.com/r/MachineLearning/comments/pkedi4/d_resources_for_understanding_the_original/
	- https://www.reddit.com/r/learnmachinelearning/comments/lz91o5/i_finally_understand_transformer_neural_networks_d/
	- https://www.reddit.com/r/MachineLearning/comments/qidpqx/d_how_to_truly_understand_attention_mechanism_in/
- Tutorials:
	- http://jalammar.github.io/illustrated-transformer/
	- https://peterbloem.nl/blog/transformers
	- http://nlp.seas.harvard.edu/2018/04/03/attention.html
- YouTube:
	- https://www.youtube.com/watch?v=rBCqOTEfxvg
