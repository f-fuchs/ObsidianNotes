![[comparison_of_different_normalizations.svg|700]]

## Batch Norm

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
print(f"{data_mean_batch.shape}")
data_std_batch = torch.std(data, dim=(0, 2, 3), correction=0)
print(f"{data_std_batch.shape}")
output_batch_hand = torch.zeros_like(data)
for c in range(C):
	output_batch_hand[:, c, :, :] = (data[:, c, :, :]-data_mean_batch[c])/data_std_batch[c]

# compare batch norm to batch norm by hand
print(f"{(output_batch-output_batch_hand).max()}")
```

## Layer Norm

```run-python
import torch

N, C, H, W = 5, 3, 10, 10 
# N = number of images in batch
# C = number of channels
# H = height of image
# W = width of image

# create random data
data = torch.randn(N, C, H, W)

# layer norm
layer_norm = torch.nn.LayerNorm([C, H, W], eps=0, elementwise_affine=False)
output_layer = layer_norm(data)

# check mean and std of every image
for n in range(N):
	print(f"output_layer[{n}, :, :, :].mean()={output_layer[n].mean()}")
	print(f"output_layer[{n}, :, :, :].std()={output_layer[n].std()}")

# calculate layer norm by hand
data_mean_layer = torch.mean(data, dim=(1, 2, 3))
print(f"{data_mean_layer.shape}")
data_std_layer = torch.std(data, dim=(1, 2, 3), correction=0)
print(f"{data_std_layer.shape}")
output_layer_hand = torch.zeros_like(data)
for n in range(N):
	output_layer_hand[n] = (data[n]-data_mean_layer[n])/data_std_layer[n]

print(f"{(output_layer-output_layer_hand).max()}")
```

## Instance Norm

```run-python
import torch

N, C, H, W = 5, 3, 10, 10 
# N = number of images in batch
# C = number of channels
# H = height of image
# W = width of image

# create random data
data = torch.randn(N, C, H, W)

# instance norm
instance_norm = torch.nn.InstanceNorm2d(C, eps=0, momentum=0, affine=False)
output_instance = instance_norm(data)

# check mean and std of each channel separably per image
for n in range(N):
	for c in range(C):
		print(f"output_instance[{n}, {c}, :, :].mean()={output_instance[n, c, :, :].mean()}")
		print(f"output_instance[{n}, {c}, :, :].std()={output_instance[n, c, :, :].std()}")

# calculate batch norm by hand
output_instance_hand = torch.zeros_like(data)
for n in range(N):
	for c in range(C):
		output_instance_hand[n, c, :, :] = data[n, c, :, :] - data[n, c, :, :].mean()
		output_instance_hand[n, c, :, :] /= data[n, c, :, :].std(correction=0)

# compare batch norm to batch norm by hand
print(f"{(output_instance-output_instance_hand).max()}")
```

## Group Norm

### 1 Group -> LayerNorm
```run-python
import torch

N, C, H, W = 5, 3, 10, 10 
# N = number of images in batch
# C = number of channels
# H = height of image
# W = width of image

# create random data
data = torch.randn(N, C, H, W)

# instance norm
G = 1 # number of groups
group_norm = torch.nn.GroupNorm(G, C, eps=0, affine=False)
output_group = group_norm(data)

# check mean and std of each channel separably per image
group_size = C // G
for n in range(N):
	for c in range(0,C,group_size):
		print(f"output_instance[{n}, {c}, :, :].mean()={output_instance[n, c:c+group_size, :, :].mean()}")
		print(f"output_instance[{n}, {c}, :, :].std()={output_instance[n, c:c+group_size, :, :].std()}")

# layer norm
layer_norm = torch.nn.LayerNorm([C, H, W], eps=0, elementwise_affine=False)
output_layer = layer_norm(data)

print(f"{(output_group-output_layer).max()}")

```

### 3 Groups -> Instance Norm

```run-python
import torch

N, C, H, W = 5, 3, 10, 10 
# N = number of images in batch
# C = number of channels
# H = height of image
# W = width of image

# create random data
data = torch.randn(N, C, H, W)

# instance norm
G = 3 # number of groups
group_norm = torch.nn.GroupNorm(G, C, eps=0, affine=False)
output_group = group_norm(data)

# check mean and std of each channel separably per image
group_size = C // G
for n in range(N):
	for c in range(0,C,group_size):
		print(f"output_instance[{n}, {c}, :, :].mean()={output_instance[n, c:c+group_size, :, :].mean()}")
		print(f"output_instance[{n}, {c}, :, :].std()={output_instance[n, c:c+group_size, :, :].std()}")

# instance norm
instance_norm = torch.nn.InstanceNorm2d(C, eps=0, momentum=0, affine=False)
output_instance = instance_norm(data)

print(f"{(output_group-output_instance).max()}")

```
## Resources

- YouTube Yannic Kilcher: https://www.youtube.com/watch?v=l_3zj6HeWUE (9:00-21:00)
- Paper Group Norm: https://arxiv.org/pdf/1803.08494.pdf