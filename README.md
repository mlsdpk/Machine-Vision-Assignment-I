[//]: # (Image References)
[image_0]: img/matlab-logo.jpg
[image_1]: img/cat.jpeg
[image_2]: img/tform_table.png
[image_3]: img/tform_table2.png
[image_4]: img/tform_img.jpg

# Machine Vision Lab Assignment

The goal of the assignment is to understand the basic functions of MATLAB to work with images and understanding the affine transformations of images.

![alt text][image_0]

We'll cover four topics in this assignment:

- Reading an image
- Displaying an image
- Writing an image to graphics file
- Affine Transformations

## Reading an image

We can use matlab built in **"imread"** function to read images.

```
img = imread('img/cat.jpeg');
```

## Displaying an image

If we want to view the image, we can use **"imshow"**.
```
imshow(img);
```
![alt text][image_1]
We can get more details information of the image by using **"imfinfo"**.
```
imfinfo('img/cat.jpeg')
```
Output:
```
Filename: 'img/cat.jpeg'
FileModDate: '15-Jan-2019 15:03:11'
FileSize: 123016
Format: 'jpg'
FormatVersion: ''
Width: 1280
Height: 850
BitDepth: 24
ColorType: 'truecolor'
FormatSignature: ''
NumberOfSamples: 3
CodingMethod: 'Huffman'
CodingProcess: 'Sequential'
Comment: {}
```
Additionally, we can use **"whos"** to list the names, sizes, and types of all variables in the currently active workspace.
```
whos
```
Output:

|   Name   |     Size      |   Bytes   |  Class  |  Attributes |
|----------|---------------|-----------|---------|-------------|
|    img   |  850x1280x3   |  3264000  |  uint8  |             |

## Writing an image to graphics file

We can use **"imwrite(A,filename)"** to write image data A to the file specified by filename. It creates the new file in our current folder. The bit depth of the output image depends on the data type of A and the file format.

```
imwrite(img,'new_img.jpeg');
```
This creates a new cat image called **"new_img.jpeg"**.

## Affine Transformation

Affine transformation is a linear mapping method that preserves points, straight lines, and planes. Sets of parallel lines remain parallel after an affine transformation.

The affine transformation technique is typically used to correct for geometric distortions or deformations that occur with non-ideal camera angles. For example, satellite imagery uses affine transformations to correct for wide angle lens distortion, panorama stitching, and image registration. Transforming and fusing the images to a large, flat coordinate system is desirable to eliminate distortion. This enables easier interactions and calculations that don’t require accounting for image distortion.

The following table illustrates the different affine transformations: translation, scale, shear, and rotation.

![alt text][image_2]

To perform a 2-D or 3-D geometric transformation, first create a geometric transformation object that stores information about the transformation. Then, pass the image to be transformed and the geometric transformation object to the **imwarp** function.

![alt text][image_3]

Here, we'll do some 2d affine geometric transformations.

We are going to use an **"affine2d"** object for 2D affine geometric transformation.

### 2D Affine Transformation Object for Rotation

First, we will create an affine2d object that defines a 30 degree rotation in the counterclockwise direction around the origin.

```
theta = 30;
T = [cosd(theta) sind(theta) 0; -sind(theta) cosd(theta) 0; 0 0 1];
tform = affine2d(T);
```
Then, apply the geometric transformation to our original cat image using **imwarp**
```
tform_img = imwarp(img,tform);
imshow(tform_img);
```
![alt text][image_4]

If we know the transformation matrix for the geometric transformation we want to perform, then we can create a **affine2d**, **projective2d**, **affine3d** or other geometric transformation objects directly.

## References

https://www.mathworks.com/help/images/2-d-and-3-d-geometric-transformation-process-overview.html 
