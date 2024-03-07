![[comparison_of_different_normalizations.svg|700]]

```run-python
import torch

N, C, H, W = 5, 3, 10, 10 
# N = number of images in batch
# C = number of channels
# H = height of image
# W = width of image

# create random data
data = torch.randn(N, C, H, W)

# batch norm
batch_norm = torch.nn.BatchNorm2d(C, eps=0, momentum=0, affine=False)
output_batch = batch_norm(data)

# check mean and std of every channel
for c in range(C):
	print(f"output_batch[:, {c}, :, :].mean()={output_batch[:, c, :, :].mean()}")
	print(f"output_batch[:, {c}, :, :].std()={output_batch[:, c, :, :].std()}")

# calculate batch norm by hand
data_mean_batch = torch.mean(data, dim=(0, 2, 3))
print(f"{data_mean_batch}")
data_std_batch = torch.std(data, dim=(0, 2, 3))
print(f"{data_std_batch}")
output_batch_hand = torch.zeros_like(data)
for c in range(C):
	output_batch_hand[:, c, :, :] = (data[:, c, :, :]-data_mean_batch[c])/data_std_batch[c]

# compare batch norm to batch norm by hand
print(f"{(output_batch-output_batch_hand).max()}")
```

```run-python
import torch

N, C, H, W = 5, 3, 10, 10 
# N = number of images in batch
# C = number of channels
# H = height of image
# W = width of image

data = torch.randn(N, C, H* W)

# layer norm
layer_norm = torch.nn.LayerNorm([C, H*W], eps=0, elementwise_affine=False)
output_layer = layer_norm(data)

for n in range(N):
	print(f"{output_layer[n].mean()}")
	print(f"{output_layer[n].std()}")

data_mean_layer = torch.mean(data, dim=(1, 2))
print(f"{data_mean_layer.shape}")
data_std_layer = torch.std(data, dim=(1, 2))
print(f"{data_std_layer.shape}")
output_layer_hand = torch.zeros_like(data)
for n in range(N):
	output_layer_hand[n] = (data[n]-data_mean_layer[n])/data_std_layer[n]

print(f"{torch.isclose(output_layer, output_layer_hand)}")
print(f"{(output_layer-output_layer_hand).max()}")
```


