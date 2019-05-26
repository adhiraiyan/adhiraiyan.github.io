---
title:  "Computer Vision: Image Classification"
date:   2019-05-26
categories: ['DeepLearning']
tags: ['Computer Vision', 'CNN']
image: /img/cv/cvog.jpg

---

<a name="contents"></a>
- [What is Image Classification?](https://www.adhiraiyan.org/deeplearning/computer-vision-image-classification#1)
- [How does humans perform Image Classification?](https://www.adhiraiyan.org/deeplearning/computer-vision-image-classification#2)
- [What are some challenges in Image Classification?](https://www.adhiraiyan.org/deeplearning/computer-vision-image-classification#3)
- [What are some Neural Network architectures for computer vision?](https://www.adhiraiyan.org/deeplearning/computer-vision-image-classification#4)
- [What is fine grained Image classification?](https://www.adhiraiyan.org/deeplearning/computer-vision-image-classification#5)
<!-- more -->

***
### <a name="1"></a> What is Image Classification?

Understanding the contents of an image or an image region is fundamental to image and scene understanding. Many other vision problems such as object detection and semantic segmentation can be reduced to image classification.

The goal of image classification is to assign the input image one or more labels from some predefined set of categories. Classification can be thought of as two separate problems:

1. Binary Classification: where only two classes are involved.
2. Multi-class Classification: involves assigning an object to one of several classes.

***
### <a name="2"></a> How does humans perform image classification?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

Research has revealed two fundamental aspects influencing the image recognition process. That is, image resolution and duration of image exposure to the viewer. This is replicated in machine learning approach to image classification.

<img src="/img/cv/20190526/20190526a.PNG" alt="Machine Learning Pipeline" class="center-image">

The first step of the pipeline corresponds to extraction and encoding of meaningful features from the image pixels and the second step performs image classification in the space of features extracted from the image.

Machine learning methods for image classification build the decision function over features that are extracted from the image, while deep learning methods learn both the features and the decision functions in an end-to-end fashion.


***
### <a name="3"></a> What are some challenges in Image Classification?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

Humans don't consider image classification as a challenge, even babies are able to classify what they see to an extent, you probably would have seen these funny videos where a baby reacts to seeing his/her father without a beard for the first time, initially the baby doesn't classify the person as their father, meaning, they were able to classify before but for a computer, this task is still a huge challenge.

<img src="/img/cv/20190526/20190526h.jpg" alt="Baby doesn't recognize dad without beard" class="center-image">

If you haven't watched the video, you can watch the video [here](https://www.newsflare.com/video/87786/health-education/baby-girl-doesnt-recognise-her-father-without-a-beard), it's adorable but make sure you come back.

So, back to why image classification can be challenging, I list below few of the most common challenges in image classification and if you see the development of image classification algorithms, they are a response to these challenges:

- Viewpoint variant: meaning an object in an image can be captured in many ways respect to the camera.
- Scale variation: images can't represent real world sizes accurately and even among two images, the sizes an object represent can vary.
- Deformation: many objects can be deformed in various ways.
- Occlusion: An object can be covered or hidden by other objects.
- Illumination conditions: Lighting conditions may defer.
- Background clutter: Objects may blend into the background making them hard to identify.
- Intra class variation: An object such as a chair comes in different shapes, sizes and colors and this can be a challenge.

Below is an example for these challenges:

<img width="70%" src="/img/cv/20190526/20190526i.jpeg" alt="Image classification challenges" class="center-image">


***
### <a name="4"></a> What are some neural network architectures for computer vision?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

- LeNet (1998) : 32x32 gray scale input image, 5-layer convolutional feature extractor.

<img src="/img/cv/20190526/20190526b.PNG" alt="LeNet architecture" class="center-image">

- AlexNet (2012) : 11x11, 5x5, 3x3 convolutions, max pooling, dropout, data augmentation, ReLU activations, SGD with momentum.

<img src="/img/cv/20190526/20190526c.PNG" alt="AlexNet architecture" class="center-image">

- VGG (2014) : 138 million parameters, 18 layers. Used 3x3 layers for more non linearity and less parameters to learn.

<img src="/img/cv/20190526/20190526d.PNG" alt="VGG architecture" class="center-image">

- Inception V3 (2015) : 25 million parameters, 22 layers. The idea of having inception blocks is connected to both the reduction of computational complexity and the efficient use of local image structure. The correlation statistics over the last layer is analyzed and clustered into groups of units with high correlations. In the layers close to the input, correlated units would concentrate in local regions. Thus we would end up with a lot of clusters concentrated in a single region, and then can be covered by a layer of one by one convolutions in the next layer.

<img width="80%" src="/img/cv/20190526/20190526e.png" alt="Inception architecture" class="center-image">

The idea of having one by one convolution is that such convolutions can capture interactions of local channels in one pixel of the feature map. They form sort of dimensionality reduction with added ReLU activation that is necessary to remove redundant feature maps from the previous layer.

- ResNet: Deeper models achieve better results in recognition because it allows the network to learn features at various levels of abstraction. But deeper models suffer from vanishing gradients problem and their training error starts increasing due to this resulting in a saturation of accuracy.

ResNet solves this by using something called a skip connection:

<img width="80%" src="/img/cv/20190526/20190526f.PNG" alt="Skip Connection architecture" class="center-image">


***
### <a name="5"></a> What is fine grained Image classification?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

Fine grained image classification/recognition classify visually very similar objects. They aim to distinguish objects from different subordinate level categories within a general category. They have high intra-class and low inter-class variance.

Part localization can be used for fine grained image recognition.  What part localization does is it explicitly isolate differences associated with object parts and then classify features extracted from aligned parts.

<img width="50%" src="/img/cv/20190526/20190526g.PNG" alt="Fine grained localization" class="center-image">

Dividing the fine-grained dataset into multiple visually similar subsets or directly using multiple neural networks to improve the performance of classification is another widely used method in many deep learning based fine-grained image classification systems.


***
### ️⭐️ Coming Up Next: Computer Vision: Image Retrieval (06.09.2019)

This post is meant to be an introduction to image classification, in my future posts, we will delve deeper into the architectures and other important concepts in Image Classification.

If you need more explanations, have any doubts or questions, you can comment below or reach out to me personally via [Facebook](https://www.facebook.com/adhiraiyan), I would love to hear from you 🙂.

🔔 [Subscribe](https://www.adhiraiyan.org/subscribe.html) 🔔 so you don't miss any of my future posts!
