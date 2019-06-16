---
title:  "Computer Vision: Face Recognition"
date:   2019-06-16
categories: ['DeepLearning']
tags: ['Computer Vision', 'CNN']
image: /img/cv/cvog.jpg

---
<a name="contents"></a>
- [What is face recognition?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#1)
- [What is Face verification evaluation protocol?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#2)
- [How is face verification solved?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#3)
- [What is a triplet loss training scheme?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#4)
- [What is the re-identification problem?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#5)
- [What are some challenges in person re-identification?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#6)
- [What are some approaches to person re-identification?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#7)
- [What is facial key-point regression?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#8)
- [What are some approaches to key-point regression tasks?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#9)
- [How to build a statistical model of facial shape?](https://www.adhiraiyan.org/deeplearning/computer-vision-face-recognition#10)
<!-- more -->

***
### <a name="1"></a> What is face recognition?

Face recognition performance is reported in three standard tasks:
1. Verification: Two facial images are presented to a system. The system has to decide if the images belong to the same person or to two different persons. This is also called one to one matching. The basic question is, is this person who he claims to be?

2. Open set identification: Build up on verification but extend its formulation. The basic question asked is do we know this face? and the person doesn't have to be somebody in the gallery.

3. Closed set identification: Is the classic performance measure used in automatic face recognition. The basic question asked is whose face is this? and the person is someone in the gallery


***
### <a name="2"></a>What is Face verification evaluation protocol?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

- An image $p_j$ is presented to the system with gallery *G*
- Similarity scores $s_{ij}$ are computed
- Verification rate for gallery probes $p_j \in P_G:$

$$\color{Orange}{P_V(\tau) = \frac{|{p_j:s_{ij} \geq \tau, id(g_i) = id(p_j)}|}{|P_G|} \tag{1}}$$

- False accept rate for non gallery probes $p_j \in P_N:$

$$\color{Orange}{P_{FA}(\tau) = \frac{|{p_j:s_{ij} \geq \tau, id(g_i) \neq id(p_j)}|}{(|P_N|-1)|G|} \tag{2}}$$


***
### <a name="3"></a> How is face verification solved?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

Large scale open set identification tasks bear similarity to the [Content Based Image Recognition task](https://www.adhiraiyan.org/deeplearning/computer-vision-image-retrieval#1), but are restricted to the domain of facial images only.

Following are the standard stages of face verification:
1. The face is detected on the image and its bounding boxes are cropped.
2. The face undergoes alignment to march a certain normalized representation. The reason we do this is because many facial recognition algorithms including deep learning and metric methods can all benefit from applying facial alignment before trying to identify the face.
4. A deep convolutional neural network is applied to extract a feature vector from the facial image.
5. In the same way this was performed in the CBIR task. SUch a feature vector is compared against all feature vectors corresponding to the images in the gallery to find the closest match.

Initially, the deep architecture fee are bootstrapped by considering the problem of recognizing several thousand unique individuals set up as a multiclass classification problem. After learning, a classifier layer can be removed and the score of actors can be used for face identity verification using the Euclidean distance to compare them. However, the scores can be significantly improved by tuning them for verification in the Euclidean space using a triplet loss training scheme.


***
### <a name="4"></a> What is a triplet loss training scheme?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

A triplet consists of 2 matching and 1 non-matching thumbnail images.
- Embed input image *X* into Euclidean space $\mathbb{R}^d$ via *f(x)*
- We want $||f(a) - f(p)||_2^2 + \alpha < ||f(a) - f(n)||_2^2$
- Minimize triplet loss:

$$\color{Orange}{\sum_{i=1}^n [||f(a) - f(p)||_2^2 - ||f(a) - f(n)||_2^2 + \alpha]_+ \rightarrow min_f \tag{3}}$$


***
### <a name="5"></a> What is the re-identification problem?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

Person re-identification is the problem of identifying people across images that have been taken using different cameras or across time using a single camera.

***
### <a name="6"></a> What are some challenges in person re-identification?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

1. The resolution of person images are very low since they are captured by surveillance cameras
2. Lighting conditions are unstable.
3. The direction of cameras and the pose of persons are arbitrary.
4. Human pose across time and space
5. background clutter and occlusions.
6. Different individuals sharing the same appearance.

***
### <a name="7"></a> What are some approaches to person re-identification?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

A standard approach to re-identification generally follows the pipeline sent by face verification algorithms. A typical re-identification system takes as input two images, each of which usually contains a person's full body. And outputs, either a similarity score between the two images or a classification of the pair of images as same if the two images depict the same person, or different if the images are of different people.

Given two person images, they are sent to Siamese convolutional neural network. A neural network architecture which consists of two copies of the same network.

<img src="/img/cv/20190616/20190616a.png" alt="Example of animated convolution" class="center-image">

For two images, x and y, a Siamese network can predict a label to denote whether the image pair comes from the same subject or not. Siamese network is composed of two convolutional neural networks connected by a connection function. Connection function is used to evaluate the relationship between two samples. And cost function is used to convert the relationship into a cost.

How to choose the connection function and cost function is closely related to the performance of the re-identification model. There are many distance, similarity or other functions that can be used as candidates to connect to vectors such as euclidean distance, cosine similarity, absolute difference, vector concatenation and so on.

***
### <a name="8"></a> What is facial key-point regression?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

The objective of key-points regression task is to predict or regress onto positions of certain important locations on face images. Key-points are used as a building block in several applications such as tracking faces in images, in video, analyzing facial expressions, detecting dysmorphic facial signs for medical diagnosis, and biometrics or face recognition.


***
### <a name="9"></a> What are some approaches to key-point regression tasks?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

Approaches to keypoint regression can be generally divided into two categories.
1. Classify local search windows or,
2. Directly predicting keypoint locations, or shape perimeters for entire image.
This bears significant similarity to attribute recognition approaches.

For the first category, a classifier called facial part detector is trained for each keypoint and keypoint location is predicted based on local regions.

There are two matters one has to decide upon:
1. How to construct local detectors for each face part.
2. How to choose right candidate among all outputs predicted as positives by local detectors.

To start with, for each face part, such as eyes, or mouth, we can construct local detectors. Such a detector utilizes a sliding window to search for a location in the image containing the facial part. For each position of the sliding window, image features such as CNN features, or [HOG](https://www.adhiraiyan.org/deeplearning/computer-vision-image-retrieval#6) features are extracted and then classified as related or not related to the facial part.

The second step in recognition would be to gather them into a complete facial shape. We can formulate facial part localization as a bayesian inference that combines the output of local detectors with a prior model of face shape and build a statistical model of facial shape.


***
### <a name="10"></a> How to build a statistical model of facial shape?
<p align="right"><a href="#contents"><sup>▴ Back to top</sup></a></p>

- Point distribution model: scatter keypoints to represent shapes as a sequence of connected landmarks or points in the surface of a face. $x = (x_1 \dots , x_n, y1, \dots , y_n)^T$

- Represent any shape *x* via approximation $x = \bar{x} + P_s b_s$ places landmarks at unique boundary locations such as salient points on the boundary curves.

- Training: apply PCA to labeled images $\rightarrow \bar{x}, P_s, b_s$ helps us answer a few questions such as, what does the average shape looks like and what kinds of variations are normal

To compute a prior model of facial shape, we can use active shape or active appearance models. In active shape model a point distribution model captures the shape variants and gradient distributions for a set of facial keypoints, and describes the local appearance. The shape of the face can then be defined as that property of the configuration of points which is kept unchanged or invariant under some global transformation.

Couple of disadvantages of active shape model are, one, the initial shape may be far from the target position, and the update may end up being in a local minimum. And two, visual features extracted at each step are not discriminative or not reliable enough to predict facial points.


***
### ️⭐️ Coming up Next: Computer Vision: Object Detection (06.30.2019)

If you need more explanations, have any doubts or questions, you can comment below or reach out to me personally via [Facebook](https://www.facebook.com/adhiraiyan) or [LinkedIn](https://www.linkedin.com/in/mukesh-mithrakumar/), I would love to hear from you 🙂.

🔔 [Subscribe](https://www.adhiraiyan.org/subscribe.html) 🔔 so you don't miss any of my future posts!
