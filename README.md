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
plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.show()
```

### Step 5: Thresholding

``` python
_, threshold = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)
```

### Step 6: Region of Interest (ROI)

``` python
h, w = threshold.shape
mask = np.zeros_like(threshold)

polygon = np.array([[(0,h), (w,h), (w//2,h//2)]])
cv2.fillPoly(mask, polygon, 255)

roi = cv2.bitwise_and(threshold, mask)
```

### Step 7: Edge Detection (Canny)

``` python
edges = cv2.Canny(roi, 50, 150)
```

### Step 8: Gaussian Blur

``` python
blur = cv2.GaussianBlur(edges, (5,5), 0)
```

### Step 9: Hough Transform

``` python
lines = cv2.HoughLinesP(blur, 1, np.pi/180, 50,
                        minLineLength=50, maxLineGap=100)
```

### Step 10: Lane Detection Logic and Display Results

``` python
output = image.copy()
line_image = np.zeros_like(image)

if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = np.array(line).flatten()[:4]
        cv2.line(line_image, (x1,y1), (x2,y2), (0,255,0), 3)
        cv2.line(output, (x1,y1), (x2,y2), (0,255,0), 3)

images = [image, gray, threshold, roi, edges, blur, line_image, output]

titles = ['Original Image', 'Grayscale Image',
          'Thresholded Image', 'ROI Masked Image',
          'Edge Detected Image', 'Smoothed Image',
          'Detected Lines', 'Final Lane Detection']

plt.figure(figsize=(15,10))

for i in range(8):
    plt.subplot(3,3,i+1)

    if i == 0 or i == 6 or i == 7:
        plt.imshow(cv2.cvtColor(images[i], cv2.COLOR_BGR2RGB))
    else:
        plt.imshow(images[i], cmap='gray')

    plt.title(titles[i])
    plt.axis('off')

plt.tight_layout()
plt.show()

print("Lane Detection Completed Successfully!")
```

## Expected Output

<img width="1022" height="687" alt="image" src="https://github.com/user-attachments/assets/2d2e810a-6e4d-44bd-bb7d-ca1dbff149a9" />


## Result

Thus, the basic lane detection pipeline is implemented using OpenCV. The
system detects and highlights lane line segments in the road image.


