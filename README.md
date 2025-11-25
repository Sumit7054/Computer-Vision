How do we see objects?

For a human, seeing process involves few steps in sequence. Firstly, you get an image with color and intensity variations across, and then there is something called as depth.
Colors are made of RGB values with these values determining intensity. Depth is determined narrowing the number of patches for certain object in the image compared to its forefront part, and of course, change in intensity.

For simplicity, we will talk about single channel greyed image. We will take a photo wherein on left side you have green color and on right you have red color.

Say you get an image of M X N pixels in grey scale. It contains some object. Our visual system will try to first identify certain small patch of some unique identity.
Then, it will try to look for all nearby patches with same color pattern. It will then create one single patch in left side and one single path in the left side. Even if it now have only two pixel, it is able to identity two
objects in the picture. It is able to figure out their shapes as well.

# How do we detect corners and edges:

Image I have an image which has all the pixels same except the right most edge where the pixel values in grey color are double in intensity.

When I will look at left patches of same intensity, based on above discussion, I can say that it is all flat. But when it reaches to right edge, we see doubling of light intensity.
Now if I want to detect the edge, what should I do? I should probably need to get the shape of the edge. I will take mean/median of all pixels or patches and will deduct that from all pixel values.

Lets say you had 3 X 3 Matrix. Left 2 columns' pixel values are x. And last column which is double the value is 2x. The median value is x. And if that is extracted from each pixel value, we get x in both places in right most column and 0 everywhere else.

Probably in this case we could get edge easily. For edge detection, we have come kernels which simply removes mean background from entire image and only edges are left. Sobel edge detector kernel is one of them.

Lets have a look at how to detect corner.

We take same example. But in this case, 3 X 3 image has x values in bottom most two rows in first 2 cells each. And in rest of the cells, it has 2x of grey scale pixel value.
The mean is 14/9 x. The median is 2x. If deduct columns from left from all columns, we get first two columns with values in 6 cells. Once we deduct it from last column, we get 0, -x, -x which if we add median of these value becomes
x, 0, 0 in last column. So now entire picture looks like (0, 0, 0), (0, 0, 0), (x, 0, 0) which shoes the corner of the image. This operation involved subtraction of one column followed by addition of median value of that column.
There are many filters for detecting the corners as well. 


# Object Detection

How do we  detect objects?

We can say from the seeing process that we patch similar appearining smaller patches together. And based on our ability to draw boundry based on color intensity or depth, we draw boundaries between objects.

We put together visually similar patches and see anything outside the boundry as separate object. 

Our visual system puts together some patterns of frequent patterns of visually similar patches and then assign a category to that pattern.

This process is called object detection. Here, you detected object in an image. You can detect single object in an image or multiple objects in an image but you will have to show the pictures of those objects to the ML model.

# Image segmentation

Image segmentation is a process of breaking down an image into similar appearing patches. The way we explained above, any image can be segmented into simiar appearing patches or groups.

# How do we patch similar appearing pixels

In above example, we put together same value of pixels and formed bigger patches.
For actual image, you can actually have certain variations in value of each pixel in a patch and you can then just use clustering algoritm to put the pixels in different patches. You can use K-means, K-Median and Hierarchical Clustering for the same.
You can also use KNN if you can figure out how many different objects you really have. But its computationally expensive to use KNN on very large image.

# Object Tracking

If you can form frame around each group of pixels in the image, you know that each of these boxes have object. In a football game, you can detect a player in one image capture.
In next capture of frame, you might have to adjust the previous rectangular frame you built if the object is moved out or has changed its posture. You might even have to expand expand or shrink the frame around the object 
to capture it entirely. You first check if entire object is in the frame. If not, you explore which direction to move stepwise. Once entire object is captured, you have detected the object in second frame as well.
Videos are  sequential frames of image. If you are able to do the first step with accuracy, you're likely to track the object in the video. YOLO is one of the technique for object tracking.

# Computer Vision with Deep Learning

Deep learning does wonders when it comes to computer vision. In a deep learning network, first few neuron layers captures edges and corners, next few captures boundary components which are formed from edges and corners, next layer may unite those boundary components to form the major boundaries sufficeint enough to classify that object.

Deep Learning does feature engineering, feature transformation and feature extraction in previous few layers and then use them to check if new image has those features with high confidence, in case object classification is our primary objective.
If our objective is to get a numerical feature, say the length of trunk of an elephant, then previous layers will have found out the layout of the eyes and last few layers can then do reletive evaluation of eyes width based on the eye width data the DL model is fed with.

Deep Learning can help do many of computer vision tasks with ease - image classification, object tracking, handwriting recognition, text extraction, and image captioning and many more! 
