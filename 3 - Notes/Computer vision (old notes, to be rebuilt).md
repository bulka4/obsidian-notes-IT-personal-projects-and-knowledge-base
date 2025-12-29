Tags: [[__Machine_Learning]]

# Introduction
Computer vision refers to tasks related to images such as:
- Image Classification - Assigning a single class to an entire image
- Object Detection - Detecting objects in an image
- Semantic Segmentation - Classifying each pixel in an image
- Instance Segmentation - Like in case of Semantic Segmentation, we classify each pixel, but additionally, we differentiate different objects. 
# Useful links
- TensorFlow object detection - [youtube](https://www.youtube.com/watch?v=yqkISICHH-U)
	- GitHub repo with code for the above video: [github](https://github.com/nicknochnack/TFODCourse)
- Documents about R-CNN and fast R-CNN:
	- [huppelen.nl]([http://www.huppelen.nl/publications/selectiveSearchDraft.pdf](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf))
	- [arxiv]([https://arxiv.org/pdf/1311.2524.pdf](https://arxiv.org/pdf/1311.2524.pdf))
- Mask R-CNN
	- Youtube explanation: [youtube](https://www.youtube.com/watch?v=4tkgOzQ9yyo)
	- GitHub repo with Detectron from Facebook: [github](https://github.com/facebookresearch/Detectron)
	- Arxiv document: [arxiv](https://arxiv.org/pdf/1703.06870)
- Document about Instance segmentation: [openreview.net](https://openreview.net/pdf?id=C3ukgkqJuh0)
- Multiple object detection with anchor boxes: [d2l.ai](https://d2l.ai/chapter_computer-vision/anchor.html)
# RPN (region proposal network)

In this method we take an image, apply cnn to create a feature map and then we create anchor boxes (rectangles) with different scales and ascept ratios for each point of a feature map. Those anchor boxes are part of an image, not a feature map.

RPN (region proposal network) takes those anchor boxes and outputs a set of good proposals which might contain an object which we want to detect.

For each anchor RPN outputs 2 different things:
- Probability that anchor contains an object which we want to detect but it doesn't predict what class it is
- Set of 4 numbers: x_center, y_center, width, height which indicates how much we need to change a position and size of an anchor box in order to fit better to an object.

# RoI Pooling (region of interest pooling)

[https://erdem.pl/2020/02/understanding-region-of-interest-ro-i-pooling](https://erdem.pl/2020/02/understanding-region-of-interest-ro-i-pooling)

We take an image and create a feature map using cnn.

Then we create different RoIs (regions of interest) using for example RPN (region proposal network). Those RoIs are part of an image, not feature map. Then we map those RoIs onto a feature map.
![[2 - Images/Computer vision 1/Screenshot 1.png]]

Let’s take a RoI which has (296, 192) coordinates of a top left corner, height = 145, width = 200. Feature map is 32 times smaller then the image so coordinates of a top left corner of the RoI, its width and height are also 32 times smaller.
- width: 200/32 = 6.25
- height: 145/32 = ~4.53
- x: 296/32 = 9.25
- y: 192/32 = 6

When we put a RoI on a feature map it looks like this
![[2 - Images/Computer vision 1/Screenshot 2.png]]

We cannot apply pooling because some of the cells are divided so we need to round parameters of the RoI
![[2 - Images/Computer vision 1/Screenshot 3.png]]

Blue section is the section which we lost and the green one is the one which we have added.

Now we want to apply max pooling such that we obtain 3x3 RoI pooling matrix. We cant divide 4 by 3 so again we need to round that number so we will take only a part of our RoI and apply max pooling to that
![[2 - Images/Computer vision 1/Screenshot 4.png]]

# RoI Allign (modification of RoI Pooling)

[https://erdem.pl/2020/02/understanding-region-of-interest-part-2-ro-i-align](https://erdem.pl/2020/02/understanding-region-of-interest-part-2-ro-i-align)

We create a feature map and create on it a section corresponding to a RoI in the image.
![[2 - Images/Computer vision 1/Screenshot 5.png]]

This is our RoI in the feature map
![[2 - Images/Computer vision 1/Screenshot 6.png]]

Now we divide our RoI into 9 boxes
![[2 - Images/Computer vision 1/Screenshot 7.png]]

We sample 4 points inside each box
![[2 - Images/Computer vision 1/Screenshot 8.png]]

To calculate coordinates of those points we use this formula:

Top left point:

§ X = X_box + (width/3) * 1 = 9.94

§ Y = Y_box + (height/3) * 1 = 6.50

Bottom left point:

§ X = X_box + (width/3) * 1 = 9.94

§ Y = Y_box + (height/3) * 2 = 7.01

And the rest of points we calculate analogically.

Now we will use bilinear interpolation to calculate values for each point.
$$
P \approx \frac{y_2 - y}{y_2 - y_1}(\frac{x_2 - x}{x_2 - x_1}Q_{11} + \frac{x - x_1}{x_2 - x_1}Q_{21}) + \frac{y - y_1}{y_2 - y_1}(\frac{x_2 - x}{x_2 - x_1}Q_{12} + \frac{x - x_1}{x_2 - x_1}Q_{22})
$$

Here is the example of how those calculations looks like:
![[2 - Images/Computer vision 1/Screenshot 9.png]]

Now for each box we have created 4 points with assigned values. If we are using max pooling then for each box we are choosing max value and this gives us a RoI Align
![[2 - Images/Computer vision 1/Screenshot 10.png]]
