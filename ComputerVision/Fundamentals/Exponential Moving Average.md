# Exponential Moving Average (EMA)

## Recursive Definition

The recursive equations is as follows:

$$
v_t = \beta v_{t-1} + (1 - \beta) \theta_t
$$

where $v_t$ is a time series that approximates a given variable indexed by time $t$, $\theta$ is the current observation and $\beta$ is a hyperparameter between $0$ and $1$.

## Iterative

$$
v_t = (1-\beta) \sum_{i=0}^{t} \beta^{t-1} \theta_i
$$
