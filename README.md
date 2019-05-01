# [Neural Style Transfer](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf) using  [Swift for TensorFlow](https://github.com/tensorflow/swift)
This is a Jupyter notebook project that implements Neural Style Transfer using Swift for TensorFlow.

![Alt text](/StyleGraphic.jpg?raw=true "Style Graphic")

Attribution from left to right:

* King of Hearts / Wikimedia Commons / CC-BY-SA-3.0 [CC BY-SA 3.0 (https://creativecommons.org/licenses/by-sa/3.0)]
* A Starry Night by Vincent van Gogh, c. June 1889
* Image generated by employing the Neural Style Transfer algorithm [detailed by Gatys et al.](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf)

## What _is_ Neural Style Transfer?

Simply put, Neural Style Transfer [[Gatys et al.]](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf)  is a process by which we take the _style_ of one image, the _content_ of another image and generate a new image that exhibits the same stylistic features as the style image while preserving the high-level structure of the content image.

The neural part, as you might expect, is where the real magic happens. If you've read about or taken a course on Convolutional Neural Networks, you've probably encountered the wonderful paper [Visualizing and Understanding Convolutional Networks](http://openaccess.thecvf.com/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf) by Zeiler and Fergus. This paper keenly illustrates the fact that each kernel in a conv net acts as a sort of feature extractor. The features start out primitive and local but as the net goes deeper, the features become more abstract and global. Neural Style Transfer exploits this fact, extracting style information from the activations of various layers. We also extract _content_ information from the higher layers of the network. We use this information to compute what is referred to in the literature as the "Perceptual Loss".

Given an input image, our goal is to minimize Perceptual Loss with respect to that image. In order to compute the Perceptual Loss, we need the following:
* A style image
* A content image
* A styled image. This is the output. We can initialize it a number of ways (which we'll explore below).
* A way of extracting style information from layer activations. 
* A pretrained conv net (we'll use [VGG-19](https://arxiv.org/abs/1409.1556) [Karen Simonyan, Andrew Zisserman]).

We'll use the [Adam optimizer](https://arxiv.org/abs/1412.6980) [Diederik P. Kingma, Jimmy Ba] to optimize our "styled" image.
