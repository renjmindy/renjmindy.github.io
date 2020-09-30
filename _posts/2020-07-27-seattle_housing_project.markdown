---
layout: post
title:      "Where do we implement tricks to help use pretrained neural network?"
date:       2020-07-27 16:43:01 -0400
permalink:  seattle_housing_project
---


## Introduction to Convolutional Neural Network (CNN)


In this blog post, we will talk about tricks that will make training of new neural networks much faster. 


The first one is the **transfer learning**. Remember that deep networks learn complex feature extractors for which we need lots of data to train the deep neural network from scratch. Let's look at the **ImageNet** classification architecture. There're lots of convolutional layers, and we call them, feature extractors. The last convolutional layer extracts features that are useful for classification with MOP. This architecture is trained on ImageNet dataset. But what if we can reuse an existing feature extractor for a new task? How do we do that? We add a new classifier on the top of previous convolution layers regarded as feature extractors, and associated weights with the new classifier is all we need to train. In such a way, we need less data to train, because we train only the final MLP layer as the new classifier. The employment of pretrained ImageNet's feature extractors works, if a domain of a new task is similar to ImageNet's. That being said, ImageNet's pretrained feature extractors won't work for the human emotion classification, because ImageNet doesn't have any people faces in the dataset. Hence, ImageNet's pretrained feature extractors have no clue about any concepts of a human face. But what if we need to classify human emotions? Perhaps we can partially reuse
ImageNet's feature extractors. 


Let's look at the perfect feature extractor that we need for the classification of human emotions. It looks like a bunch of
convolutional layers, and let's look at what activation stimuli we actually want to get. The *first convolutional layer* will have highest activations for *edge detectors* that have different rotations. When we go deeper than those convolutional
layers along the concept of a human eye, or nose, or throat, we will have layers that learn the representation of a human face. That is our perfect feature extractors that we really want to obtain. Lets compare it with ImageNet's feature extractors. ImageNet definitely has those *edge detectors* as well, but, provided that it doesn't have human faces in the data set, it doesn't know the concept of a nose or throat, so that we will need to train this. Lets look at how an architecture for the human emotion classification might look like. What we need to do is that we actually reuse first convolutional layers as edge detectors followed by newly added convolutional layers together with a new multi-layer perceptron as the new classifier to train for our new task. All we need to train is those latest convolutions, plus full connected layers. It works much better, because we train much less number of parameters. What if we don't start from scratch and don't initialize those convolutions with random numbers, but rather we cutomize the initialization from
pre-trained ImageNet network? That leads us to so called, **fine-tuning** technique, because we don't start with the random initialization, but rather we reuse those complex representations that is suitable for the ImageNet classification. 


What is the intuition behind this? We don't start with random features, but we start with features that are useful for
some other task. They are not 100% perfect for our task, but they might be much better than random. What we do next is that we propagate all the gradients but with a way much smaller learning rate, so that we don't lose the initialization that we borrowed from ImageNet from the beginning. The fine-tuning is very frequently used thanks to wide spectrum of ImageNet classes. **Keras, a deep learning framework, has the weights of pre-trained VGG, Inception, and ResNet architectures**. *What is so special about that you can fine-tune a bunch of different architectures and thus make an ensemble out of them*? Most importantly, you don't have to wait for two or three weeks to train your neural network on ImageNet dataset. 


Lets summarize a little bit. If we have a *small* dataset which is from ImageNet domain, all we will need to do is to use **transfer learning** and train lastest MLP layers. On one hand, if we have a *bigger* data set from ImageNet, it will make sense to fine-tune deeper layers so as to squeeze a little bit more of quality from this pretrained neural network. On the other, if we have a big dataset which is *not similar to ImageNet domain*, it will make sense to train from scratch. Most likely, we can't reuse the features extracted from ImageNet. However, if we have a *small dataset which is not similar to ImageNet*, we won't consider it, and most likely, we will have to collect more data. 

