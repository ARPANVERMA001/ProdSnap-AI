# Product Entity Extraction from Images

## Project Overview

This project focuses on extracting key entity values such as dimensions, weight, volume, voltage, and wattage from product images using a combination of image processing techniques and Optical Character Recognition (OCR). The project aims to fill the gap where product details are not available in text format and can only be derived from the image itself. It is useful in a variety of domains, including:

- **Healthcare:** Extracting product details like expiration dates, dosage, etc.
- **E-Commerce:** Extracting critical information like size, weight, voltage, wattage from product images for online catalogs.
- **Content Moderation:** Automating product categorization and moderation based on image-based information.

The goal is to develop a machine learning model that enhances entity value extraction from images, which is essential as digital marketplaces and other sectors scale.

---

## Features

### 1. Image Preprocessing
- **Grayscale Conversion:** Converts color images into grayscale for easier processing.
- **Thresholding:** Applies adaptive thresholding to simplify images for contour and edge detection.
- **Edge Detection:** Uses Canny edge detection to identify boundaries for object detection.

### 2. OCR (Optical Character Recognition)
- **Rotation Support:** OCR is performed on rotated versions of the image (0°, 90°, 180°, and 270°) to handle text at different orientations.
- **Text Recognition:** Extracts numeric and text information using two different OCR models (`--psm 6` and `--psm 11 --oem 3`) to maximize accuracy.
  
### 3. Contour and Bounding Box Detection
- **Contour Detection:** Finds and analyzes contours to identify bounding boxes around objects.
- **Bounding Box Analysis:** Calculates the largest bounding box in the image and identifies the width and height of the object.
  
### 4. Line Detection
- **Hough Line Transform:** Detects vertical and horizontal lines for extracting dimension-related information.
- **Classify Lines:** Classifies lines into vertical and horizontal with strict thresholds to determine product dimensions (e.g., height, width).

### 5. Text Extraction Based on Line Detection
- Extracts text around detected lines (both vertical and horizontal) to infer product-related metrics such as dimensions.

---

## Installation and Setup

### Prerequisites

- Python 3.x
- OpenCV (`cv2`)
- NumPy
- pytesseract (Tesseract OCR)
- PIL (Pillow library for image handling)

### Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/your-repo/image-entity-extraction.git
    ```

2. Install the required dependencies:
    ```bash
    pip install opencv-python-headless numpy pytesseract Pillow
    ```

3. Ensure you have Tesseract OCR installed:
    - For macOS:
      ```bash
      brew install tesseract
      ```
    - For Ubuntu:
      ```bash
      sudo apt-get install tesseract-ocr
      ```

---

## Usage

1. **Input Image:** Provide a product image (e.g., packaging or label).
2. **Run OCR and Detection:**
    - The script automatically processes the image, detects the largest bounding box, and extracts relevant product information (e.g., dimensions, weight, voltage).
3. **Extracted Information:** The final output provides product metrics such as length, height, and detected numeric values.

```python
# Sample usage of the main function
result = WDH(img)
print(f"Detected Length: {result[0]}, Detected Height: {result[1]}, Bounding Box Width: {result[2]}, Bounding Box Height: {result[3]}")
