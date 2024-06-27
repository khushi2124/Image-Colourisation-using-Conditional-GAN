# Image-Colorization-using-cGAN
Grayscale image colourisation using a conditional GAN(Generative Adversarial Networks) built on PyTorch framework

## Dataset 
The dataset used is the [celebrity faces dataset](https://www.kaggle.com/datasets/jessicali9530/celeba-dataset). This dataset consists of 200,000+ RGB images of size 218x178 pixels. For this project, only a small subset of 10,000 randomly chosen images was used. 80% of this data was used for training the models.

## Preprocessing and LAB colour space
LAB is a color space just like RGB but here the 3 channels represent Lightness(L), Green-Redness (a) and Yellow-blueness (b) of each pixel. The Lightness(L) channel is effectively a grayscale image.

<img src="https://github.com/aditya-gupta-04/Image-Colourisation-using-Conditional-GAN/blob/main/rgb-lab.jpg" width="500">

- For this task, I have used LAB colour space instead of RGB colour space as it reduces the number of output channels required for our generator. This allows for better image generation and fast training and inference times.
- Instead of using 1 grayscale channel as input and 3 RGB channels input, we can use the **single L channel as input** and generate the **A and B channels as output**, the input L channel and output A,B channels can be used to generate an RGB output.
- For training, RGB images are taken from the dataset and transformed to the LAB colour space, the L channel is used as inputs for the generator and the A,B channel are ground truths for training the generator.
- Before training, the images are resized to 256x256 and normalised.

Samples of training images

<img src="https://github.com/aditya-gupta-04/Image-Colourisation-using-Conditional-GAN/blob/main/train_samples.jpeg" width="500">

## GAN Architecture
<img src="https://github.com/aditya-gupta-04/Image-Colourisation-using-Conditional-GAN/blob/main/models.jpg" width="500">

- Both the generator and the discriminator are neural networks. The generator output is connected directly to the discriminator input. The generator learns to generate plausible data and the discriminator learns to distinguish the generator's fake data from real data.
- In the case of image colourisation we use a conditional GAN setup and provide additional information to the generator and discriminator models in the form of the grayscale image input.
