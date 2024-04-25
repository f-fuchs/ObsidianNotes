
## Introduction: Generative Models

Given observed samples $x$ from a distribution of interest, the goal of a generative model is to learn to model its true data distribution $p(x)$. Once learned, we can generate new samples from our approximate model at will. Furthermore, under some formulations, we are able to use the learned model to evaluate the likelihood of observed or sampled data as well.

Types:
- Generative Adversarial Networks (GANs) model the sampling procedure of a complex distribution, which is learned in an adversarial manner. 
- "Likelihood-based" models, seek to learn a model that assigns a high likelihood to the observed data samples. This includes autoregressive models, normalizing flows, and Variational Autoencoders (VAEs).
- Energy-based modeling, in which a distribution is learned as an arbitrarily flexible energy function that is then normalized.
- Score-based generative models learn the score of the energy-based model as a neural network instead of learning to model the energy function itself
## Background: ELBO, VAE, and Hierarchical VAE

### Evidence Lower Bound (ELBO)
