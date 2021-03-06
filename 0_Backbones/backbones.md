Backbones are the most important architecture for the neural networks. 

## 1. Review papers
Many other review papers focused on specific areas are collected under specific topics file.

- Neena Aloysius and Geetha M, A Review on Deep Convolutional Neural Networks, 2017

A bit old and not include many state-of-art research, refer to paper [A Review on Deep Convolutional Neural Networks](https://ieeexplore.ieee.org/abstract/document/8286426/)

- Elhassouny, Azeddine et al, Trends in deep convolutional neural Networks architectures: a review, 2019.

**Recommand**. Reviewed most of the CNN backbones, refer to paper [Trends in deep convolutional neural Networks architectures: a review](https://ieeexplore.ieee.org/abstract/document/8807741?casa_token=NzJx5O4redQAAAAA:OhEtsKL2x8ryRkb21GgeTu9glwuesljMYIWUeYMt7dPyY2vOhrJk8kO0Qh1lMgjRNiC7T2OCaQ)

## 2. History

A brief figure below shows the time line of the nerual network development
![nn_his](https://user-images.githubusercontent.com/42667259/89516735-1b0e0480-d7d9-11ea-8d88-61a3556b0b5f.jpg)

### - Lenet, Yann LeCun et al.
LeNet-5, this is a simple but creative network, originally used for the handwriting recognition. please refer to http://yann.lecun.com/exdb/lenet/
![nn_lenet](https://user-images.githubusercontent.com/42667259/89517382-ec445e00-d7d9-11ea-9b77-cb9493af3d19.png)

### - AlexNet, Alex Krizhevsky et al.
Won the ImageNet Large Scale Visual Recognition Challenge on September 30, 2012. The network achieved a top-5 error of 15.3%, more than 10.8 percentage points lower than that of the runner up. The primary finding was that the depth of the neural network was essential for the high performance of detection. 
网络的深度对于性能的提升具有极其关键的作用，并且伴随着GPU的逐步广泛使用，使用深度大的网络成为现实。

Kernels are relatively large, 11 * 11, 7 * 7, 5 * 5 etc., see from the figure 
refer to paper [ImageNet Classification with Deep Convolutional Neural Networks] (https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)

![nn_lenet](https://user-images.githubusercontent.com/42667259/89520673-80182900-d7de-11ea-8e38-c95c03bbb19c.png)


### - VGGNet, Karen Simonyan, Andrew Zisserman
2014 Imagenet competition 2nd. 

1. Validate that increasing the net depth can improve the performance effectively. But this bring a problem: great amount of parameters. 

2. decrease the flame kernel size, two 3 * 3 replace 5 * 5, decrease the parameters amounts
证明网络深度增加有助于检测，但引入更多的参数；于是发现了使用小卷积核能达到和使用大卷积核同样的目的，同时还能减少参数

refer to paper [Imagenet classification with deep convolutional neural networks](https://arxiv.org/abs/1409.1556)

![nn_vgg](https://user-images.githubusercontent.com/42667259/89520223-d46ed900-d7dd-11ea-9554-99f9603fd6e0.png)

### GoogLeNet, Christian Szegedy, Wei Liu et al.
- v1, 2014 ImageNet competition 1st. 

1. Apart from increasing the network depth, (22 layers for googlenet v1,) increase the width of the network

2. Introduce smaller kernels, 1 * 1 convolution, reduce the dimensions and save parameters. Parameters: AlexNet ~ 12 GoogLeNet, VGG ~ 3 AlexNet

3. Inception module is easy to add or remove, which is to mimic the human brain to create a sparce connection.

Refer to [Going deeper with convolutions](https://static.googleusercontent.com/media/research.google.com/zh-CN//pubs/archive/43022.pdf)

![nn_googlenet_v1](https://user-images.githubusercontent.com/42667259/89532952-e9099c00-d7f2-11ea-9ac3-89cb14c4e1e6.png)

- v2, Christian Szegedy et al. v2, v3 share the same paper.

1. Factorizing Convolutions, use 1 * n and n * 1 to replace 3 * 3, shown as figure below. Theoritically, it can save computational cost dramatically when feature map is large (n is large). But in practice, it can not work well in the early layers, n ranges 12-20 seems to be a reasonable number. 卷积分解不适合早期大的特征层，而适合中期12-20大小的特征层

2. efficient grid size reduction. Use pooling layer (stride 2 in the following figure) and inception(convolution with stride 2 etc.) parallelly. 

3. propose some advices for the design of an efficient network: Avoid representational bottlenecks, especially early in the network; Higher dimensional representations are easier to process locally within a network; Spatial aggregation can be done over lower dimensional embeddings without much or any loss in representational power (like RGB image to gray); Balance the width and depth of the network (This is further concluded in the recent efficientNet 2019). 早期特征尺寸不能急剧减小，避免出现瓶颈；低维特征时进行空间融合，并不会特别明显的增加损失（这感觉也像是可以进行特征融合的一个体现）

Refer to paper [Rethinking the Inception Architecture for Computer Vision](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Szegedy_Rethinking_the_Inception_CVPR_2016_paper.pdf)

![nn_googlenet_v2](https://user-images.githubusercontent.com/42667259/89534536-60d8c600-d7f5-11ea-8f99-afc2d13f2985.png#30x15)
![nn_googlenet_v2_2](https://user-images.githubusercontent.com/42667259/89537049-0d687700-d7f9-11ea-8d91-3a204d7e18a6.png#10*10)

- v3, shares the same paper with v2, minor additions.

Model Regularization via Label Smoothing, reduce the model overfitting. Training method: RMSProp to replace SGD. A resolution test was carried out.

Refer to paper [Rethinking the Inception Architecture for Computer Vision](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Szegedy_Rethinking_the_Inception_CVPR_2016_paper.pdf)

- v4 (pure inception-v4), inception-resnet, together in a paper. So here talk them together, mainly the inception-resnet

1. Combine the inception module with residual module to create a new module: inception-resnet. It increases the net depth and imporves the speed. 

2. Comparison: inception-v3 with inception-resnet-v1; inception-v4 with inception-resnet-v2, have similar accuracies.

Refer to paper [Inception-v4, inception-resnet and the impact of residual connections on learning](https://www.aaai.org/ocs/index.php/AAAI/AAAI17/paper/viewPaper/14806)

### ResNet, He Kaiming
1st place in all 5 competitions of ILSVRC and COCO 2015. 

It was found that deeper CNN is extremely useful for almost all the tasks. But they are difficult to train since the existence of degradation problem. A new architecture with residual module was proposed.

1. deeper network performs worse than shallower network. A creative idea: if nothing is learned, not worse than before: thus identity mapping, also known as a shortcut connection is proposed. H(x) = x + F(x), F(x) = H(x) - x, known as a residual.

2. different depth of ResNet, from 18 layers to 34, 50, 101, to extremely deep 152 layers.

3. different ways of shortcut, if dimension is not changed, identity mapping can be used. But in practice, dimension change, therefore, a "bottleneck" is created. (This is popular in the baselines afterwords, since it can save parameters.)

Refer to paper [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385)

![nn_resnet](https://user-images.githubusercontent.com/42667259/89544188-19a50200-d802-11ea-8bff-88434e5bb831.png)
![nn_resnet_2](https://user-images.githubusercontent.com/42667259/89545365-8bca1680-d803-11ea-8b35-3b824952e96c.png)

### Xception, Chollet, Francois
Based on Inception-v3, if we do not want to design the inception architecture every time, just use the same structure evenly at one module, it will be easier for the network design. (This idea is popular in the other baselines, i.e., mobileNet.)

1. extreme inception. from equivalent inception structure, now only calculate a part of the channels, (group = xx in pytorch).

2. depthwise separable convolution (originally from a phd thesis: Laurent Sifre, Rigid-Motion Scattering For Image Classification), save parameters greatly. By separating features evenly, the parameters in figure below can be m * k + 3 * 3 * k, m is the features, k is the kernels number.
Details can also see mobileNet in ../1_lightweight_network.

Refer to paper [Xception: Deep Learning with Depthwise Separable Convolutions](https://arxiv.org/abs/1610.02357)
![nn_xception](https://user-images.githubusercontent.com/42667259/89560940-17e63900-d818-11ea-95d1-bb73602a132c.png)

### ResNeXt, Xie Saining, He Kaiming
ILSVRC 2016 2nd palce.

A modification of the inception-resnet. Different from the human design of inception-resnet, resnext use the same branches to finish the design.

1. group convolution, cardinality(基数). It is a compromise between normal convolution (all channels) and depthwise separable convolution (each channel). This is a group of channels. 

2. findings: "On the ImageNet-1K dataset, we empirically show that even under the restricted condition of maintaining complexity, increasing cardinality is able to improve classification accuracy. Moreover, increasing cardinality is more effective than going deeper or wider when we increase the capacity." "With cardinality C
increasing from 1 to 32 while keeping complexity, the error rate keeps reducing." "increasing cardinality at the price of reducing width starts to show saturating accuracy when the bottleneck width is small." 增加基数在一定程度上会改善表现，文中实验了从1到32 groups，误差逐步降低。但需要注意的是，这是将dimensions控制在4d以上，更小的dimension下作者认为不值得再实验。

Refer to paper [Aggregated Residual Transformations for Deep Neural Networks](https://arxiv.org/abs/1611.05431)
![nn_resnext](https://user-images.githubusercontent.com/42667259/89551303-19f5cb00-d80b-11ea-9e98-13a7d1df6779.png)

### denseNet, Huang Gao, Liu Zhuang
CVPR2017 best paper, reuse of feature is important for learning, based on Resnet.

1. dense connectivity, current layer has connections with all the previous layers. Traditional CNN, L layer, L connection, denseNet, one dense block, L layers has L*(L+1)/2 connections.

2. growth rate, lth layer has k_0 + k*(l-1) feature maps, k_0 is the input channels number, k is the growth rate (each layer features number).

3. bottleneck layer, the author found this layer is especially effective for densenet. use 1 * 1 conv, feature map 4k (improve efficiency), and then 3 * 3 conv, reduce back to k

4. compression, transition layer feature maps are reduced with \theta. This is also confirmed in the experiments, heat map shows that the dense block is less relevant to the previous transition layer. 说明了transition layer输出了很多冗余信息，去除一些，可以使网络轻量化，但又不至于严重影响精度。

Refer to paper [Densely Connected Convolutional Networks](https://arxiv.org/abs/1608.06993)
![nn_densenet](https://user-images.githubusercontent.com/42667259/89555466-6099f400-d810-11ea-88f5-a8b9543b5225.png)

### SENet, Hu Jie, Li Shen
ILSVRC 2017 1st place. This is an application of "attention" mechanism, more similar to human brain. 

1. Focus on the *channel relationship* and use squeeze and excitation block. 1 * 1 * C, all the channels info together and then rescale (sigmoid), the important channel features can contribute more.

2. squeeze, spatial global average, to use the connections between different channels. 作者利用的是通道间的相关性，而非空间分布

3. excitation, in practice, two fully connected layers are used: first one, compressed the channels from C to C/r and with ReLU, and second layer recover to C channels with sigmoid to scale. Then the important one can contribute more. r is the compression ratio. The author found that 16 is the best choose.

4. SE block can also work together with ResNet and Inception. 

Refer to paper [Squeeze-and-Excitation Networks](https://arxiv.org/abs/1709.01507)
![nn_senet](https://user-images.githubusercontent.com/42667259/89558401-77424a00-d814-11ea-99b2-465ed516ba84.png)

### efficientNet, Tan Mingxing and Quoc V. Le
Are there any laws applicable for the design of the nerual network architecture? The authors proposed some basic points and an empirical equation.

1. "Scaling up any dimension of network width, depth, or resolution improves accuracy, but the accuracy gain diminishes for bigger models". 
单独增加某个参数只能在一定范围内获得好的结果

2. model scaling, balancing the width, depth and resolution can lead to better performance. a highly effective compound coefficient. The coefficient for three main parameters: width, w, depth, d, resolution, r; only if d * w^2 * r^2 = 2, they can achieve a relative balanced architecture. If they want to expand or compress, 2^\phi, \phi is the expansion coefficient, it becomes (d * w^2 * r^2)^\phi, all three parameters changed with exponent \phi.

3. relatively smaller but more efficient and accurate than compared models.

Refer to paper [EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks](https://arxiv.org/pdf/1905.11946.pdf)
![nn_efficientnet](https://user-images.githubusercontent.com/42667259/89571214-9ac2c000-d827-11ea-9863-cdd8824c7f03.png)
![nn_efficientnet_2](https://user-images.githubusercontent.com/42667259/89572219-1cffb400-d829-11ea-9f91-3e64abfb3caa.png)

### NAS
Above are architectures designed from people's empirical observations. Is there any method to design network automatically? In 2016, MIT and google proposed Neural Architecture Search almost at the same time. But the computation cost is extremely expensive.

1. search strategies, reinforcement learning is used here, but there are many other ways, i.e., Evolutionary algorithm, gradient-based method, boosting etc. 

2. speed-up, Hierarchical Representation, weight sharing etc.

Refer to paper [Neural Architecture Search with Reinforcement Learning](https://arxiv.org/abs/1611.01578)
[Designing Neural Network Architectures using Reinforcement Learning](https://arxiv.org/abs/1611.02167)
![nn_nas](https://user-images.githubusercontent.com/42667259/89575120-93061a00-d82d-11ea-89d0-b02a79fbe3c9.png)

### Res2Net, Gao Shanghua et al.

1. Multi-scale fusion. "most existing methods represent the multi-scale features in a layerwise manner. In this paper, we propose a novel building block for CNNs, namely Res2Net, by constructing hierarchical residual-like connections within one single residual block." It is based on the bottleNeck structure, 1 * 1, 3 * 3, and then 1 * 1, now it becomes like the following figure.

2. can combine with other backbones, ResNet, ResNeXt etc. Improve the accuracy significantly. 70% to 73% on COCO from ResNet-50 to Res2Net-50.

3. The author also tried varying kinds of tasks, e.g., object detection, semantic/instance segmentation, key points estimation, all of them show satisfactory results.

Refer to paper [Res2Net: A New Multi-scale Backbone Architecture](https://ieeexplore.ieee.org/abstract/document/8821313?casa_token=87qNMjgrnBYAAAAA:31BsZutpV6YptiDHrA-AOZ9p0b0nQjR-ONrBXX2DwBlFVi4nxwXOnRKcaLrnL0h5ysatVql9Vg)
![nn_res2net](https://user-images.githubusercontent.com/42667259/89580656-fc8a2680-d835-11ea-84c7-59715bdf338f.png)
