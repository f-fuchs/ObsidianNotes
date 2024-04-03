
## Bias

Bias in machine learning refers to the error that arises from overly simplistic assumptions made by the learning algorithm. These assumptions make the model easier to comprehend and learn, but they may not capture the underlying complexities of the data. Bias is the error that arises from the model's inability to accurately represent the true relationship between the input and output. Poor performance of a model on both training and testing data indicates high bias due to the simple model, which is known as **underfitting**.

## Variance

Variance refers to the error caused by the model's sensitivity to fluctuations in the training data. It is the variability of the model's predictions for different instances of training data. High variance occurs when a model learns the noise and random fluctuations of the training data instead of the underlying pattern. This results in good performance on the training data but poor performance on the testing data, indicating **overfitting**.

![[Bias-and-Variance-in-Machine-Learning.webp]]

## Overfitting

### Example 1

![[example_overfitting1.png]]
When a machine learning model demonstrates a situation where the training loss is low but the validation loss is high, it indicates that the model is overfitting. 

### Example 2
![[example_overfitting2.png]]
If the training loss decreases while the validation loss plateaus or decreases at a slower rate, it suggests the model may be overfitting. The model is becoming too specialized in fitting the training data, but it fails to generalize well to new data.

## Underfitting

![[eP0gppr.png]]
## Resources
- https://wandb.ai/mostafaibrahim17/ml-articles/reports/A-Deep-Dive-Into-Learning-Curves-in-Machine-Learning--Vmlldzo0NjA1ODY0#what-are-accuracy-and-loss-curves?-