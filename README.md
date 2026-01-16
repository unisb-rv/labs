# Introduction to Jupyter Notebook

A Jupyter Notebook consists of two types of cells: text and code. You are currently reading a text cell, which can contain text, markdown, or HTML. It is useful for adding more information about your code, allowing the notebook to be read as a narrative, which is where the name Jupyter Notebook comes from.

Code cells contain Python code or command-line commands.
```
text = "You write your code in code block like this one"
# These code cells will always display the result of the last line of code below the cell.
text
```

You can execute code cells by selecting them with your mouse and pressing the play button in the upper left corner of the cell. You can also run the cell and move to the next one with the shortcut **Shift+Enter**. **Control+Enter** will execute the current cell and keep it selected.

The output of code cells appears below the cell. It can include outputs from ,print statements, as well as graphs and images generated using libraries like OpenCV or matplotlib.

Additionally, the result of the last line of code is always displayed at the end of the output.

Feel free to experiment with the code cells and modify this notebook however you like!

**For more tips** check out the following notebook: https://colab.research.google.com/notebooks/basic_features_overview.ipynb

## Order of execution

It's important to remember that cells are executed in the order in which you run them. For example, take a look at the following 3 cells:
```
a = 3 # Block 1
```

```
a = 2 # Block 2
```

```
a # Block 3
```

Try running cell 2 first, then cell 1, and finally cell 3. You will notice that the output of cell 3 changes because cell 1 was executed and a was assigned a new value. This behavior can lead to bugs in your code. Therefore, it is good practice to periodically, and especially before submission, run all cells in order again. You can do this by clicking ***Runtime > Run** all or pressing F9.

## Importing libraries

For completing lab exercises, you'll need various libraries such as numpy, OpenCV, matplotlib, etc. It's good practice to have a separate cell for importing all the required libraries at the beginning of the notebook. Example:

```
import numpy as np
import cv2 as cv
import matplotlib.pyplot as plot
```

This way, you ensure that the cell is always executed, and all the necessary libraries are loaded. Additionally, once these libraries are loaded, Google Colab will provide suggestions (auto-complete) as you type, which will significantly ease your work.

# Digital Image Processing vs. Computer Vision

To begin with, Computer Graphics creates a mathematical or geometric model from an original captured image to produce a digital image. However, it's important not to confuse this with Digital Image Processing or the field of Computer Vision, even though they complement each other. Digital Image Processing results in a modified version of the image, whereas Computer Vision provides a meaningful interpretation of the image using Artificial Intelligence techniques.

Nevertheless, to sucessfully deal with Computer Vision, we need to know some stuff from Image Processing field.

## So, how we digitize an image?
Simply put, the process of sampling (digitizing coordinate values of) + quantization (digitizing amplitude values) will generate an digital image, where the function represents intesity / gray level and the coordinate represents picture element (known as pixel).

![digitizing](https://i.postimg.cc/G2r5cPg3/digitizing.png)

Therefore, the digital image can be simply coded in a matrix form as:

![image](https://github.com/user-attachments/assets/bb47cf76-7549-4b94-97da-d0bb7a1c3c8c)

where M is number of rows and N is number of columns. Since we'll use Python, the pixel starts from (0,0) and ends in (M-1, N-1).

## Bits Required for Digital Image Storage

Number of gray levels ($L$) allowed in each pixel formulated as $L = 2^k \iff k = \frac{ln(L)}{ln(2)}$, where $k$ denotes a bit (binary digit). Therefore, a ***k-bit image*** requires $N \times M \times k$ bits to store a digitized image. If in case $M == N$ (height and weight of pixel are the same), its formula can be simplified as $N^2 \times k$. For example, an image with
**L = 256 possible gray-level values** is called an $2^k = 2^8 = $ **8-bit** image; and if this 8-bit image has 32x32 dimension thus it'll need $32 \times 32 \times 8 = 8,912$ bit or equivalent to **1,024 byte = 1 KB** (remember: 8 bit = 1 byte and 1,024 byte = 1 kilobyte / KB).

## Image Aquisition and Image Loading

Image acquisition process can be as simple as image capturing (e.g. with camera), loading, and saving.

TO BE NOTICED
* **matplotlib.pyplot** represents **<font color="red">R</font><font color="limegreen">G</font><font color="blue">B</font>** image
* **cv2** represents **<font color="blue">B</font><font color="limegreen">G</font><font color="red">R</font>** image (reversed)

Therefore, if you want to use **cv.imread()** to load an image and **plt.imshow()** to show it, convert the image first.
<br>Otherwise, the use of **cv2.imshow()** will open a new window to show up an image (rather than directly showed on your IPYNB cell).

# Tasks about Image Manipulation
 
In these exercises, you will familiarize yourself with the basics of image manipulation in Python. 

## Tasks

Solve the following tasks within this Jupyter Notebook, ensuring that the result of each task is displayed below the respective code cell. **Add at least one code cell for each task.**


1. Write a program that loads an image and displays three separate images, one for each channel. (Hint: When displaying one channel, set the other two channels to 0)

2. Write a program that loads an image and creates a border of 10 pixels around the image. Display the resulting image.

3. Write a program that loads an image and creates three new images from it. The first should have half the vertical pixels (rows) of the original, the second should have half the horizontal pixels (columns), and the third should have half of both. (Hint: take every other pixel). Display all three images.

# Color spaces

In this part of a lab, you'll get familiar with image color spaces. On the web and in general usage, most images are encoded as **RGB**: **R**ed, **G**reen, and **B**lue. OpenCV generally uses **BGR**: Blue, Green, Red.

This is just one of the many ways we can represent an image. In an RGB image, we get a pixel by mixing the three colors. We can get the same pixel by using different numbers and formulae to combine them. For instance, the **CMYK** color space encodes each pixel in 4 primary colors: **C**yan, **M**agenta, **Y**ellow and **K**ey (Black). Since printers use these primary colors, CMYK is often used when preparing images for print.

Not all color spaces consist only of primary colors. For instance, **HSV** (**H**ue, **S**aturation, **V**alue) stores the color in Hue, the color's intensity in Saturation, and the general brightness of that pixel in Value. The Hue portion is a number in [0, 179] (in OpenCV, usually it's an arc around a circle, so [0, 360)) where 0 is red, and the hue slowly shifts to green and then blue as you get to higher numbers.

![hsv](https://i.postimg.cc/XqdVJn2Y/rgb-to-hsv.jpg)

You can think of the whole HSV color space as a cylinder. The height on the cylinder corresponds to how dark the pixel is, the distance from the center tells you how non-gray it is, and the angle tells you which color the pixel is.

There are many color spaces each with its uses. One other color space we'll mention is **YCbCr**. Y is the **luma** component, similar to the Value in HSV. Cb is the **blue-difference chroma component**, i.e. how blue should this pixel be tinted. Similarly, Cr is the **red-difference chroma component**, which tells you how much should a pixel be tinted red. Even with a different type of representation, each YCbCr is capable of showing all RGB images.

![ycbc](https://i.postimg.cc/w38tBfgD/rgb-to-ycrcb.png)

The reason YCbCr is important is because of the human eye. Our eyes are much more sensitive to luminance than actual color differences. Therefore, when compressing images, it's better to compress the chroma components than luminance if you want the image to look the same to a human observer.  This is called **chroma subsampling** and is used heavily in image and video compression, including MPEG, JPEG, DVD and Blu-Rays, and many others.

## In OpenCV

OpenCV supports a plethora of color spaces for images. The main function to convert color spaces is: [img = cv.cvtColor(img, code)](https://docs.opencv.org/master/d8/d01/group__imgproc__color__conversions.html#ga397ae87e1288a81d2363b61574eb8cab). The `code` tells OpenCV **from** which format to convert the image, as well as **to** which format. You can see all the color conversion codes [here](https://docs.opencv.org/master/d8/d01/group__imgproc__color__conversions.html#ga4e0972be5de079fed4e3a10e24ef5ef0). For example:

- cv.COLOR_BGR2YCrCb (BGR to YCbCr)
- cv.COLOR_YCrCb2BGR (back to BGR as the name suggests)
- cv.COLOR_RGB2HSV
- etc.

Note: You'll have to convert the image back to RGB if you want to use matplotlib to display it in its original form. 

# Tasks about Color spaces
In these exercises, you will familiarize yourself with the basics of different color spaces. 

## Task 1

Load the image `images/peppers.png` using OpenCV and convert it to the HSV color space using the aforementioned function. Then, add 30 to the H (hue) channel of the HSV image for each pixel. Convert that image back to RGB and display it.

## Task 2

Load the image `images/peppers.png` using OpenCV and convert it to the HSV color space using the aforementioned function. Then, set the H (hue) channel of the HSV image to 0 for each pixel. Convert that image back to RGB and display it.
