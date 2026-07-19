# OpenCV: Google Colab ↔ Windows (VS Code / Cursor)

This guide explains how to convert OpenCV programs between **Google Colab** and **Windows (VS Code/Cursor)**.

---

# 1. Displaying Images

## Google Colab

```python
from google.colab.patches import cv2_imshow

cv2_imshow(image)
```

## Windows

```python
cv2.imshow("Image", image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

# 2. Reading Images

## Google Colab

Upload an image or download it.

```python
from google.colab import files

uploaded = files.upload()

image = cv2.imread("cat.jpg")
```

or

```python
import urllib.request

urllib.request.urlretrieve(image_url, "cat.jpg")
```

---

## Windows

Simply keep the image in the project folder.

```python
image = cv2.imread("cat.jpg")
```

---

# 3. Display Function

| Google Colab | Windows |
|--------------|----------|
| cv2_imshow(image) | cv2.imshow("Window", image) |

---

# 4. Downloading Files

## Google Colab

```python
import urllib.request

urllib.request.urlretrieve(url, "image.jpg")
```

---

## Windows

Download the file manually and place it in the project folder.

---

# 5. Haar Cascade XML File

## Google Colab

```python
import urllib.request

urllib.request.urlretrieve(
    cascade_url,
    "haarcascade_frontalface_default.xml"
)

face_detector = cv2.CascadeClassifier(
    "haarcascade_frontalface_default.xml"
)
```

---

## Windows

OpenCV already provides the XML files.

```python
face_detector = cv2.CascadeClassifier(
    cv2.data.haarcascades +
    "haarcascade_frontalface_default.xml"
)
```

---

# 6. Google Colab Imports

Remove these when running in Windows.

```python
from google.colab.patches import cv2_imshow

from google.colab import files
```

---

# 7. Windows Only

These lines should not be used in Google Colab.

```python
cv2.imshow()

cv2.waitKey()

cv2.destroyAllWindows()
```

---

# 8. Working Directory

## Windows

```python
import os

print(os.getcwd())
```

Useful for checking where Python is looking for images.

---

## Google Colab

```python
import os

print(os.getcwd())
```

Usually returns

```
/content
```

---

# 9. Common Conversion

## Windows → Colab

Replace

```python
cv2.imshow("Image", image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

with

```python
from google.colab.patches import cv2_imshow

cv2_imshow(image)
```

---

## Colab → Windows

Replace

```python
cv2_imshow(image)
```

with

```python
cv2.imshow("Image", image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

# 10. Summary

| Task | Google Colab | Windows |
|------|--------------|----------|
| Display Image | cv2_imshow() | cv2.imshow() |
| Upload Image | files.upload() | Copy image to folder |
| Download Image | urllib.request | Manual download |
| Haar Cascade | Download XML | cv2.data.haarcascades |
| Wait for Key | Not Required | cv2.waitKey() |
| Close Window | Not Required | cv2.destroyAllWindows() |

---

# Best Practice

Whenever possible, write OpenCV programs so that only the image display section changes between Google Colab and Windows. The image processing logic (reading images, grayscale conversion, edge detection, face detection, etc.) should remain the same.

This keeps your code portable and easier to maintain across different environments.