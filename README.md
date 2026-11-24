# Lane Detection

## Aim

To implement a basic lane detection pipeline using OpenCV by completing
the missing code segments.

## Learning Objectives

-   Understand each stage of image processing.
-   Learn how to build a complete computer vision pipeline.
-   Practice writing code in guided sections.

## Software Used

-   Anaconda -- Python 3.7
-   Jupyter Notebook / VS Code
-   OpenCV (`cv2`)
-   NumPy
-   Matplotlib

## Algorithm and Explanation

### Step 1: Import Libraries

``` python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### Step 2: Read the Image

``` python
image = cv2.imread("C:/Users/vikam/Downloads/lan_img1.jpg")
```

### Step 3: Convert to Grayscale

``` python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

### Step 4: Display Images

``` python
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.show()
```

### Step 5: Thresholding

``` python
threshold = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)[1]
```

### Step 6: Region of Interest (ROI)

The ROI mask keeps the relevant road region for further processing.

### Step 7: Edge Detection (Canny)

``` python
edges = cv2.Canny(roi, 50, 150)
```

### Step 8: Gaussian Blur

``` python
blur = cv2.GaussianBlur(edges, (5, 5), 0)
```

### Step 9: Hough Transform

``` python
lines = cv2.HoughLinesP(
    blur,
    1,
    np.pi / 180,
    50,
    minLineLength=50,
    maxLineGap=100
)
```

### Step 10: Lane Detection Logic

The lane detection logic uses the detected line segments to draw lane
markings on the image.

## Expected Output

<img width="1037" height="673" alt="image" src="https://github.com/user-attachments/assets/49906df9-7b27-4b69-a99d-aa0253a96f14" />


## Result

Thus, the basic lane detection pipeline is implemented using OpenCV. The
system detects and highlights lane line segments in the road image.

