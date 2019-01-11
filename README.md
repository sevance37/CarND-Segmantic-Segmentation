# CarND-Segmantic-Segmentation

The goal of this project is to label the pixels of the road using a Fully Convolutional Network (FCN). An example image where the road pixels are overlayed on the image is shown below.

<img src="output_images/uu_000057.jpg" width="100px" align="left"/>

## Approach
A Fully Convoluational Network (FCN) is created following the approach in the paper ["Fully Convoluational Netowrks for Semantic Segmantation"](https://arxiv.org/abs/1605.06211) by E. Shelhamer, J. Long and T. Darrell.  

The architecture of this FCN starts with a pre-trained, fully convolution version of VGG-16 model. A 1x1 convolution with 2 filters (road and not-road) is then performed on Layer 7. This 1x1 convolution is then upsampled and added to a 1x1 convolution of Layer 4. This combination of Layers 7 and 4 is then upsampled and added to a 1x1 convolution of Layer 3. The resulting combination of Layers 7, 4 and 3 is then upsampled again creating the final layer. A truncated normal kernal initializer and a L2 kernal regularizer was used in each 1x1 convolution and transpose.

The Adams optimizer with a cross entropy loss function that included losses from regularization was used to train the model on the Kitti Road dataset.

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
<img src="writeup_images/example_sign.jpg" width="100px" align="left"/>


