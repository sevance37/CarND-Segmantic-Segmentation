# CarND-Segmantic-Segmentation

The goal of this project is to label the pixels of the road using a Fully Convolutional Network (FCN). An example of the identified road is shown below. 

<img src="output_images/um_000057.png" width="100%" align="center"/>


## Approach
A Fully Convolutional Network (FCN) is created following the approach in the paper ["Fully Convolutional Networks for Semantic Segmentation"](https://arxiv.org/abs/1605.06211) by E. Shelhamer, J. Long and T. Darrell.  

The architecture of this FCN starts with a pre-trained, fully convolution version of VGG-16 model. A 1x1 convolution with 2 filters (road and not-road) is then performed on Layer 7. This 1x1 convolution is then up-sampled and added to a 1x1 convolution of Layer 4. This combination of Layers 7 and 4 is then up-sampled and added to a 1x1 convolution of Layer 3. The resulting combination of Layers 7, 4 and 3 is then up-sampled again creating the final layer. A truncated normal kernel initializer and a L2 kernel regularizer was used in each 1x1 convolution and transpose.

The Adams optimizer with a cross entropy loss function that included losses from regularization was used to train the model on the Kitti Road data set.

The hyperparameter space was explored and the best values found were:

| Hyperparameter | Value | 
|---|---|
| Epochs | 40 | 
| Batch Size | 10 | 
| Learning Rate | 1e-4 |
| Dropout Keep Probability | 70% |
| L2 Regularizer Scale | 1e-3 |
| Truncated Normal Standard Deviation | 0.01 |

During training, the average loss per batch for is shown for several epochs in the following table:

|Epoch| Average Loss per Batch| 
|---|---| 
|1 | 0.7436 | 
|10 |0.0843 | 
|20 | 0.0522| 
|30 | 0.0406|
|40 | 0.0322|

## Results
Examples from this model are shown below where the identified road pixels are overlayed in green.

<img src="output_images/um_000035.png" width="90%" align="center"/>
<img src="output_images/umm_000042.png" width="90%" align="center"/>
<img src="output_images/uu_000031.png" width="90%" align="center"/>
