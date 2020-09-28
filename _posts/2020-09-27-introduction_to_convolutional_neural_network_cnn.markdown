---
layout: post
title:      "Introduction to Convolutional Neural Network (CNN)"
date:       2020-09-28 02:17:16 +0000
permalink:  introduction_to_convolutional_neural_network_cnn
---


## How is CNN architecture built up from scratch? 

In this blog post, I will discuss one more useful layer of neurons. And at the end, we will build our first fully working neural network for images. 


Before we dive into the details, let's look at how we deal with color images. When one image has colors, that means that it has three input channels, i.e. Red (R), Green (G) and Blue (B). Owing to the existance of these three colors, one image is regarded as a tensor instead of a matrix. One tensor is a multidimensional arrays, including width (W), height (H) and Cin (channel), e.g. 3 RGB channels.


*How do we apply convolutions?* One convolutional kernel becomes a tensor as well, of size Wk by Hk by Cin. And, to apply a convolution, firstly, we extract one volumetric patche from the image, and we take a inner (aka: dot) product of one volumetric patch with this kernel tensor. Consequently, an output and associated feature map with this convolution result are obtained. Then, we slide the same volumetric patch to the adjecent column (right next to the first, leftmost column), we will get another different convolution output (a different feature map included) in a different location of this input image. To gain more information embedded underneath the image along its depth direction, we need more volumetric kernels to dig it out. And that means that we need to train more Cout at the size Wk by Hk by Cin. Having a stride of 1 and enough zero padding, we can have W by H by Cout output neurons. So actually, we can slice one image into slices. Every depth slice of the convoluted volume corresponds to a feature map, to one convolutional kernel. The overall training parameters is obtained using Wk by Hk by Cout, plus one, which is the biase term.


*But is one convolutional layer good enough?* Let's say neurons of the first convolutional layer look at the patches of the image of size 3 by 3. But what if an object of interest is bigger than that? Then, it looks like we need a second convolutional layer on top of the first. The first 3 by 3 convolutional layer will have a local receptive field of 3 by 3. If we take the second convolutional layer on top of the first, then the neurons of the second convolutional layer will actually have a receptive field of 5 by 5, because of the underlying neurons and their receptive field. Let's look at what happens if we stack N convolutional layers. For simplicity, let's look at one-dimensional inputs. A one by three convolutional layer will have a reception field of 1 by 3. When we take a second convolutional layer with the same size, then we have a receptive field of 1 by 5. If it continued after the fourth level, then we have a receptive field of 1 by 9. Can you derive a formula from this? Of course, if we stack N convolutional layers with the same kernel size 3 by 3, the receptive field on N layer will be 2N + 1 by 2N +1. What does it mean? It looks like we need to stack a lot of convolutional layers to be able to identify objects as big as the input image. Take 300 by 300, we will need 150 convolutional layers. What if we need to grow the receptive field faster? We can increase a stride in our convolutional layer to reduce the output dimensions. Let's see how it works for 2 by 2 convolution with stride 2. We're effectively splitting the image into non-overlapping patches of color pink, red, yellow, and blue. If we use one back slash kernel, then we will have the result of 7, 9, 4 and 6. That's how our convolution works. If we add a second convolutional layer of the same size 2 by 2, then those layers will effectively double their receptor field, because we use the stride of 2. 


*But how do we maintain the translation invariance?* Actually, we will introduce a new layer that is called a pooling layer. This layer works like a convolutional, but doesn't have a kernel. Instead, it calculates maximum or 
average of its inputs. Let's look at the example. We have a 200 by 200 by 64 input volume, let's take a single depth
slice from that volume. Let's apply 2 by 2 max pooling with stride 2. How does one max pooling work? We take a maximum value from there, and that is our output. In this case, it is 6. Then we slide the pooling layer to the next patch, and we take the maximum value from the current patch to get 8. That's exactly how the max pooling works. If you look at the feature map, it actually means that we downsample our image. As a consequence, we're losing some details, but it actually stays kind of the same. And notice one more thing, when we apply the pooling layer, we do it depth-wise. It means that we don't change the number of output channels. We simply change the dimensions. So the volume of 200 by 200 by 64 becomes the volume of 100 by 100 by 64. 



