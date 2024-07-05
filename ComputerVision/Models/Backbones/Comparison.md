---
dg-publish: true
---

# Comparison

## ImageNet 1k

| name             | model                      | params | Resolution | acc@1 (INet-1k) | training method                            |
| ---------------- | -------------------------- | ------ | ---------- | --------------- | ------------------------------------------ |
| MetaFormer       | caformer_b36_384           | 99M    | 384        | 86.4            | supervised at 224^2 and finetuned at 384^2 |
| ConvNeXt V2      | ConvNeXt V2-H              | 660M   | 224x224    | 86.3            | FCMAE + finetuning                         |
| MetaFormer       | caformer_m36_384           | 56M    | 384        | 86.2            | supervised at 224^2 and finetuned at 384^2 |
| ConvNeXt V2      | ConvNeXt V2-L              | 198M   | 224x224    | 85.8            | FCMAE + finetuning                         |
| DeiT III         | ViT-L                      | 304.8  | 384x384    | 85.8            | supervised                                 |
| MetaFormer       | convformer_b36_384         | 100M   | 384        | 85.7            | supervised at 224^2 and finetuned at 384^2 |
| MetaFormer       | caformer_s36_384           | 39M    | 384        | 85.7            | supervised at 224^2 and finetuned at 384^2 |
| MetaFormer       | convformer_m36_384         | 57M    | 384        | 85.6            | supervised at 224^2 and finetuned at 384^2 |
| MetaFormer       | caformer_b36               | 99M    | 224        | 85.5            | supervised                                 |
| MetaFormer       | convformer_s36_384         | 40M    | 384        | 85.4            | supervised at 224^2 and finetuned at 384^2 |
| DeiT III         | ViT-H                      | 632.1  | 224x224    | 85.2            | supervised                                 |
| MetaFormer       | caformer_m36               | 56M    | 224        | 85.2            | supervised                                 |
| DeiT III         | ViT-B                      | 86.9   | 384x384    | 85.0            | supervised                                 |
| MetaFormer       | caformer_s18_384           | 26M    | 384        | 85.0            | supervised at 224^2 and finetuned at 384^2 |
| ConvNeXt V2      | ConvNeXt V2-B              | 89M    | 224x224    | 84.9            | FCMAE + finetuning                         |
| DeiT III         | ViT-L                      | 304.4  | 224x224    | 84.9            | supervised                                 |
| MetaFormer       | convformer_b36             | 100M   | 224        | 84.8            | supervised                                 |
| DaViT            | DaViT-B                    | 87.9M  | 224x224    | 84.6            | supervised                                 |
| SwinV2-B         | SwinV2-B 16x16 Window Size | 88M    | 256x256    | 84.6            | SimMIM                                     |
| MetaFormer       | convformer_m36             | 57M    | 224        | 84.5            | supervised                                 |
| MetaFormer       | caformer_s36               | 39M    | 224        | 84.5            | supervised                                 |
| MetaFormer       | convformer_s18_384         | 27M    | 384        | 84.4            | supervised at 224^2 and finetuned at 384^2 |
| DaViT            | DaViT-S                    | 49.7M  | 224x224    | 84.2            | supervised                                 |
| SwinV2-B         | SwinV2-B 8x8 Window Size   | 88M    | 256x256    | 84.2            | SimMIM                                     |
| MetaFormer       | convformer_s36             | 40M    | 224        | 84.1            | supervised                                 |
| SwinV2-S         | SwinV2-S 16x16 Window Size | 50M    | 256x256    | 84.1            | SimMIM                                     |
| FocalTransformer | Focal-B                    | 89.8M  | 224x224    | 84.0            | supervised                                 |
| FocalTransformer | Focal-fast-B               | 91.2M  | 224x224    | 84.0            | supervised                                 |
| VMamba           | VMamba-B[`s2l15`]          | 89M    | 224x224    | 83.9            | supervised                                 |
| DeiT III         | ViT-B                      | 86.6   | 224x224    | 83.8            | supervised                                 |
| VMamba           | VMamba-B[`s1l20`]          | 87M    | 224x224    | 83.8            | supervised                                 |
| SwinV2-S         | SwinV2-S 8x8 Window Size   | 50M    | 256x256    | 83.7            | SimMIM                                     |
| VMamba           | Vanilla-VMamba-B           | 76M    | 224x224    | 83.7            | supervised                                 |
| FocalTransformer | Focal-S                    | 51.1M  | 224x224    | 83.6            | supervised                                 |
| FocalTransformer | Focal-fast-S               | 51.5M  | 224x224    | 83.6            | supervised                                 |
| MetaFormer       | caformer_s18               | 26M    | 224        | 83.6            | supervised                                 |
| VMamba           | VMamba-S[`s2l15`]          | 50M    | 224x224    | 83.6            | supervised                                 |
| VMamba           | Vanilla-VMamba-S           | 44M    | 224x224    | 83.5            | supervised                                 |
| DeiT III         | ViT-S                      | 22.0   | 384x384    | 83.4            | supervised                                 |
| VMamba           | VMamba-S[`s1l20`]          | 49M    | 224x224    | 83.3            | supervised                                 |
| ConvNeXt V2      | ConvNeXt V2-T              | 28.6M  | 224x224    | 83.0            | FCMAE + finetuning                         |
| DeiT III         | ViT-M                      | 38.8   | 224x224    | 83.0            | supervised                                 |
| MetaFormer       | convformer_s18             | 27M    | 224        | 83.0            | supervised                                 |
| DaViT            | DaViT-T                    | 28.3M  | 224x224    | 82.8            | supervised                                 |
| SwinV2-T         | SwinV2-T 16x16 Window Size | 28M    | 256x256    | 82.8            | SimMIM                                     |
| VMamba           | VMamba-T[`s1l8`]           | 30M    | 224x224    | 82.6            | supervised                                 |
| VMamba           | VMamba-T[`s2l5`]           | 31M    | 224x224    | 82.5            | supervised                                 |
| FocalTransformer | Focal-fast-T               | 30.2M  | 224x224    | 82.4            | supervised                                 |
| FocalTransformer | Focal-T                    | 28.9M  | 224x224    | 82.2            | supervised                                 |
| VMamba           | Vanilla-VMamba-T           | 23M    | 224x224    | 82.2            | supervised                                 |
| ConvNeXt V2      | ConvNeXt V2-N              | 15.6M  | 224x224    | 81.9            | FCMAE + finetuning                         |
| SwinV2-T         | SwinV2-T 8x8 Window Size   | 28M    | 256x256    | 81.8            | SimMIM                                     |
| DeiT III         | ViT-S                      | 22.0   | 224x224    | 81.4            | supervised                                 |
| ConvNeXt V2      | ConvNeXt V2-P              | 9.1M   | 224x224    | 80.3            | FCMAE + finetuning                         |
| ConvNeXt V2      | ConvNeXt V2-F              | 5.2M   | 224x224    | 78.5            | FCMAE + finetuning                         |
| ConvNeXt V2      | ConvNeXt V2-A              | 3.7M   | 224x224    | 76.7            | FCMAE + finetuning                         |

## ImageNet 21k/22k

| name        | model                                         | params | Resolution | acc@1 (INet-1k) | training dataset | training method                                                     |
| ----------- | --------------------------------------------- | ------ | ---------- | --------------- | ---------------- | ------------------------------------------------------------------- |
| ConvNeXt V2 | ConvNeXt V2-H                                 | 660M   | 512x512    | 88.9            | IN-22K           | FCMAE + finetuning                                                  |
| ConvNeXt V2 | ConvNeXt V2-H                                 | 660M   | 384x384    | 88.7            | IN-22K           | FCMAE + finetuning                                                  |
| ConvNeXt V2 | ConvNeXt V2-L                                 | 198M   | 384x384    | 88.2            | IN-22K           | FCMAE + finetuning                                                  |
| MetaFormer  | caformer_b36_384_in21ft1k                     | 99M    | 384        | 88.1            | IN-21K           | supervised on IN-21K at 222^2 and finetuned on ImageNet 1k at 384^2 |
| DeiT III    | ViT-L                                         | 304.8  | 384x384    | 87.7            | IN-21K           | supervised                                                          |
| ConvNeXt V2 | ConvNeXt V2-B                                 | 89M    | 384x384    | 87.7            | IN-22K           | FCMAE + finetuning                                                  |
| MetaFormer  | convformer_b36_384_in21kft1k                  | 100M   | 384        | 87.6            | IN-21K           | supervised on IN-21K at 222^2 and finetuned on ImageNet 1k at 384^2 |
| SwinV2-L*   | SwinV2-L* 24x24 Window Size, PreTrained@192^2 | 197M   | 384x384    | 87.6            | IN-22K           | SimMIM                                                              |
| MetaFormer  | caformer_m36_384_in21ft1k                     | 56M    | 384        | 87.5            | IN-21K           | supervised on IN-21K at 222^2 and finetuned on ImageNet 1k at 384^2 |
| MetaFormer  | caformer_b36_in21ft1k                         | 99M    | 224        | 87.4            | IN-21K           | supervised on IN-21K and finetuned on ImageNet 1k                   |
| ConvNeXt V2 | ConvNeXt V2-L                                 | 198M   | 224x224    | 87.3            | IN-22K           | FCMAE + finetuning                                                  |
| DeiT III    | ViT-H                                         | 632.1  | 224x224    | 87.2            | IN-21K           | supervised                                                          |
| SwinV2-B*   | SwinV2-B* 24x24 Window Size, PreTrained@192^2 | 88M    | 384x384    | 87.1            | IN-22K           | SimMIM                                                              |
| DeiT III    | ViT-L                                         | 304.4  | 224x224    | 87.0            | IN-21K           | supervised                                                          |
| MetaFormer  | convformer_b36_in21ft1k                       | 100M   | 224        | 87.0            | IN-21K           | supervised on IN-21K and finetuned on ImageNet 1k                   |
| MetaFormer  | caformer_s36_384_in21ft1k                     | 39M    | 384        | 86.9            | IN-21K           | supervised on IN-21K at 222^2 and finetuned on ImageNet 1k at 384^2 |
| MetaFormer  | convformer_m36_384_in21ft1k                   | 57M    | 384        | 86.9            | IN-21K           | supervised on IN-21K at 222^2 and finetuned on ImageNet 1k at 384^2 |
| SwinV2-L*   | SwinV2-L* 16x16 Window Size, PreTrained@192^2 | 197M   | 256x256    | 86.9            | IN-22K           | SimMIM                                                              |
| ConvNeXt V2 | ConvNeXt V2-B                                 | 89M    | 224x224    | 86.8            | IN-22K           | FCMAE + finetuning                                                  |
| DeiT III    | ViT-B                                         | 86.9   | 384x384    | 86.7            | IN-21K           | supervised                                                          |
| MetaFormer  | caformer_m36_in21ft1k                         | 56M    | 224        | 86.6            | IN-21K           | supervised on IN-21K and finetuned on ImageNet 1k                   |
| MetaFormer  | convformer_s36_384_in21ft1k                   | 40M    | 384        | 86.4            | IN-21K           | supervised on IN-21K at 222^2 and finetuned on ImageNet 1k at 384^2 |
| SwinV2-B*   | SwinV2-B* 16x16 Window Size, PreTrained@192^2 | 88M    | 256x256    | 86.2            | IN-22K           | SimMIM                                                              |
| MetaFormer  | convformer_m36_in21ft1k                       | 57M    | 224        | 86.1            | IN-21K           | supervised on IN-21K and finetuned on ImageNet 1k                   |
| MetaFormer  | caformer_s36_in21ft1k                         | 39M    | 224        | 85.8            | IN-21K           | supervised on IN-21K and finetuned on ImageNet 1k                   |
| DeiT III    | ViT-B                                         | 86.6   | 224x224    | 85.7            | IN-21K           | supervised                                                          |
| MetaFormer  | caformer_s18_384_in21ft1k                     | 26M    | 384        | 85.4            | IN-21K           | supervised on IN-21K at 222^2 and finetuned on ImageNet 1k at 384^2 |
| MetaFormer  | convformer_s36_in21ft1k                       | 40M    | 224        | 85.4            | IN-21K           | supervised on IN-21K and finetuned on ImageNet 1k                   |
| ConvNeXt V2 | ConvNeXt V2-T                                 | 28.6M  | 384x384    | 85.1            | IN-22K           | FCMAE + finetuning                                                  |
| MetaFormer  | convformer_s18_384_in21ft1k                   | 27M    | 384        | 85.0            | IN-21K           | supervised on IN-21K at 222^2 and finetuned on ImageNet 1k at 384^2 |
| DeiT III    | ViT-S                                         | 22.0   | 384x384    | 84.8            | IN-21K           | supervised                                                          |
| DeiT III    | ViT-M                                         | 38.8   | 224x224    | 84.5            | IN-21K           | supervised                                                          |
| MetaFormer  | caformer_s18_in21ft1k                         | 26M    | 224        | 84.1            | IN-21K           | supervised on IN-21K and finetuned on ImageNet 1k                   |
| ConvNeXt V2 | ConvNeXt V2-T                                 | 28.6M  | 224x224    | 83.9            | IN-22K           | FCMAE + finetuning                                                  |
| MetaFormer  | convformer_s18_in21ft1k                       | 27M    | 224        | 83.7            | IN-21K           | supervised on IN-21K and finetuned on ImageNet 1k                   |
| ConvNeXt V2 | ConvNeXt V2-N                                 | 15.6M  | 384x384    | 83.4            | IN-22K           | FCMAE + finetuning                                                  |
| DeiT III    | ViT-S                                         | 22.0   | 224x224    | 83.1            | IN-21K           | supervised                                                          |
| ConvNeXt V2 | ConvNeXt V2-N                                 | 15.6M  | 224x224    | 82.1            | IN-22K           | FCMAE + finetuning                                                  |
