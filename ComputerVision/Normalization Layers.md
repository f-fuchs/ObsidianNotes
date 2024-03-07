![[comparison_of_different_normalizations.svg|700]]
```run-python
# Import libraries
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import numpy as np

print("test")
# Create axis
axes = [5, 5, 5]

# Create Data
data = np.ones(axes, dtype=bool)

# Control colour
colors = np.empty(axes, dtype=str)
colors.fill("grey")
colors[:,:, 0] = "blue"

# Plot figure
ax = plt.figure().add_subplot(projection="3d")
# Voxels is used to customizations of
# the sizes, positions and colors.
ax.voxels(data, facecolors=colors, edgecolors='grey')
print("test")
plt.show()
print("test")
```
