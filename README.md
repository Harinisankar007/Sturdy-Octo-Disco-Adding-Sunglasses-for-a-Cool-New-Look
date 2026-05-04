# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

# Name: HARINI S
# Register Number: 212224240049

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:

Detects the face in an image.
Places a stylish sunglass overlay perfectly on the face.
Works seamlessly with individual passport-size photos.
Customizable for different sunglasses styles or photo types.

## Technologies Used:

Python
OpenCV for image processing
Numpy for array manipulations

## How to Use:
Clone this repository.
Add your passport-sized photo to the images folder.
Run the script to see your "cool" transformation!

## Applications:
Learning basic image processing techniques.
Adding flair to your photos for fun.
Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

## Program
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
faceImage = cv2.imread("face.png")
glassPNG=cv2.imread("sunglass.png")
faceImage_rgb = cv2.cvtColor(faceImage, cv2.COLOR_BGR2RGB)
glassBGR = glassPNG[:, :, :3]
grayGlass = cv2.cvtColor(glassBGR, cv2.COLOR_BGR2GRAY)
```
```
_, glassMask1 = cv2.threshold(grayGlass, 240, 255, cv2.THRESH_BINARY_INV)
glassMask = cv2.merge((glassMask1, glassMask1, glassMask1))
glassMask = glassMask / 255.0
```
```
faceWithGlasses = faceImage.copy()
h_img, w_img = faceImage.shape[:2]
glass_height = 40
y1 = int(0.30 * h_img)
y2 = y1 + glass_height
aspect_ratio = glassBGR.shape[1] / glassBGR.shape[0]
glass_width = int(glass_height * aspect_ratio*1.5)
```
```
x_center = w_img // 2
x1 = x_center - glass_width // 2
x2 = x_center + glass_width // 2
```
```
glass_resized = cv2.resize(glassBGR, (x2-x1, y2-y1))
glassMask_resized = cv2.resize(glassMask, (x2-x1, y2-y1))
maskedEye = cv2.multiply(eyeROI.astype(float), (1 - glassMask_resized))
```
```
eyeFinal = cv2.add(maskedEye, maskedGlass)
eyeFinal = np.uint8(eyeFinal)
```
```
faceWithGlasses[y1:y2, x1:x2] = eyeFinal
plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(faceImage_rgb)
plt.title("Original Image")
plt.axis('off')
```

## Output
<img width="616" height="432" alt="image" src="https://github.com/user-attachments/assets/9b44f0b4-eb5f-42da-9c22-ada511d7fd3e" />

```
plt.subplot(1,2,2)
plt.imshow(faceWithGlasses[:,:,::-1])
plt.title("With Sunglasses")
plt.axis('off')
plt.show()
```
<img width="409" height="276" alt="image" src="https://github.com/user-attachments/assets/cee498d4-11a1-4c72-bddf-9a4d441f0f8e" />


