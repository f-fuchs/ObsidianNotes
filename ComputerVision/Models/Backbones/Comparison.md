# Comparison

## ImageNet-1k Pre-training

| name        | model                                         | params | Resolution | acc@1 (INet-1k) | training dataset | training method    |
| ----------- | --------------------------------------------- | ------ | ---------- | --------------- | ---------------- | ------------------ |
| DeiT III    | ViT-S                                         | 22.0   | 224x224    | 81.4            | ImageNet-1k      | supervised         |
| DeiT III    | ViT-S                                         | 22.0   | 384x384    | 83.4            | ImageNet-1k      | supervised         |
| DeiT III    | ViT-M                                         | 38.8   | 224x224    | 83.0            | ImageNet-1k      | supervised         |
| DeiT III    | ViT-B                                         | 86.6   | 224x224    | 83.8            | ImageNet-1k      | supervised         |
| DeiT III    | ViT-B                                         | 86.9   | 384x384    | 85.0            | ImageNet-1k      | supervised         |
| DeiT III    | ViT-L                                         | 304.4  | 224x224    | 84.9            | ImageNet-1k      | supervised         |
| DeiT III    | ViT-L                                         | 304.8  | 384x384    | 85.8            | ImageNet-1k      | supervised         |
| DeiT III    | ViT-H                                         | 632.1  | 224x224    | 85.2            | ImageNet-1k      | supervised         |
| DeiT III    | ViT-S                                         | 22.0   | 224x224    | 83.1            | ImageNet-21k     | supervised         |
| DeiT III    | ViT-S                                         | 22.0   | 384x384    | 84.8            | ImageNet-21k     | supervised         |
| DeiT III    | ViT-M                                         | 38.8   | 224x224    | 84.5            | ImageNet-21k     | supervised         |
| DeiT III    | ViT-B                                         | 86.6   | 224x224    | 85.7            | ImageNet-21k     | supervised         |
| DeiT III    | ViT-B                                         | 86.9   | 384x384    | 86.7            | ImageNet-21k     | supervised         |
| DeiT III    | ViT-L                                         | 304.4  | 224x224    | 87.0            | ImageNet-21k     | supervised         |
| DeiT III    | ViT-L                                         | 304.8  | 384x384    | 87.7            | ImageNet-21k     | supervised         |
| DeiT III    | ViT-H                                         | 632.1  | 224x224    | 87.2            | ImageNet-21k     | supervised         |
| ConvNeXt V2 | ConvNeXt V2-A                                 | 3.7M   | 224x224    | 76.7            | ImageNet-1k      | FCMAE + finetuning |
| ConvNeXt V2 | ConvNeXt V2-F                                 | 5.2M   | 224x224    | 78.5            | ImageNet-1k      | FCMAE + finetuning |
| ConvNeXt V2 | ConvNeXt V2-P                                 | 9.1M   | 224x224    | 80.3            | ImageNet-1k      | FCMAE + finetuning |
| ConvNeXt V2 | ConvNeXt V2-N                                 | 15.6M  | 224x224    | 81.9            | ImageNet-1k      | FCMAE + finetuning |
| ConvNeXt V2 | ConvNeXt V2-T                                 | 28.6M  | 224x224    | 83.0            | ImageNet-1k      | FCMAE + finetuning |
| ConvNeXt V2 | ConvNeXt V2-B                                 | 89M    | 224x224    | 84.9            | ImageNet-1k      | FCMAE + finetuning |
| ConvNeXt V2 | ConvNeXt V2-L                                 | 198M   | 224x224    | 85.8            | ImageNet-1k      | FCMAE + finetuning |
| ConvNeXt V2 | ConvNeXt V2-H                                 | 660M   | 224x224    | 86.3            | ImageNet-1k      | FCMAE + finetuning |
| SwinV2-T    | SwinV2-T 8x8 Window Size                      | 28M    | 256x256    | 81.8            | ImageNet-1K      | SimMIM             |
| SwinV2-S    | SwinV2-S 8x8 Window Size                      | 50M    | 256x256    | 83.7            | ImageNet-1K      | SimMIM             |
| SwinV2-B    | SwinV2-B 8x8 Window Size                      | 88M    | 256x256    | 84.2            | ImageNet-1K      | SimMIM             |
| SwinV2-T    | SwinV2-T 16x16 Window Size                    | 28M    | 256x256    | 82.8            | ImageNet-1K      | SimMIM             |
| SwinV2-S    | SwinV2-S 16x16 Window Size                    | 50M    | 256x256    | 84.1            | ImageNet-1K      | SimMIM             |
| SwinV2-B    | SwinV2-B 16x16 Window Size                    | 88M    | 256x256    | 84.6            | ImageNet-1K      | SimMIM             |
| SwinV2-B*   | SwinV2-B* 16x16 Window Size, PreTrained@192^2 | 88M    | 256x256    | 86.2            | ImageNet-22K     | SimMIM             |
| SwinV2-B*   | SwinV2-B* 24x24 Window Size, PreTrained@192^2 | 88M    | 384x384    | 87.1            | ImageNet-22K     | SimMIM             |
| SwinV2-L*   | SwinV2-L* 16x16 Window Size, PreTrained@192^2 | 197M   | 256x256    | 86.9            | ImageNet-22K     | SimMIM             |
| SwinV2-L*   | SwinV2-L* 24x24 Window Size, PreTrained@192^2 | 197M   | 384x384    | 87.6            | ImageNet-22K     | SimMIM             |
