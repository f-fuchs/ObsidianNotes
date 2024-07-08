# Linear Probing

Linear probing involves training a simple linear classifier (like a logistic regression) on the features extracted by a pre-trained model, without updating the model's weights.

## Dense Prediction

Train only the added segmentation head (linear classifier), while keeping the pre-trained Encoder unchanged. The training process adjusts the weights of the segmentation head to fit the new segmentation task.
