# moonhelp: Helper Class for the Moon Dream Image Recognition Model

This repository contains a Python class, `moonhelp`, designed to simplify interaction with the [Moon Dream](https://github.com/vikhyat/moondream) image recognition model. It provides a convenient way to load images, generate captions, detect objects, and query the model.

## Purpose

The `moonhelp` class aims to streamline the process of using the Moon Dream model for various image analysis tasks. It encapsulates common operations into easy-to-use methods, allowing you to quickly integrate Moon Dream's capabilities into your projects.

## Key Features

* **Image Loading:** Supports loading images from local file paths or directly from URLs.
* **Caption Generation:** Automatically generates captions for loaded images.
* **Object Detection:** Detects specified objects within an image, drawing bounding boxes and providing cropped images of the detected objects.
* **Querying:** Allows you to ask questions about the content of an image and receive answers from the model.
* **Easy Access to Results:** Provides attributes to access the generated caption, detection results (bounding boxes, points, crops), and query answers.
* **Duplicate Removal:** Includes a utility function to remove duplicate object detections.

## Installation

1.  **Prerequisites:**
    * **Python 3.6+**
    * **PIL (Pillow):** Install using pip:
        ```bash
        pip install Pillow
        ```
    * **moondream:** Install the Moon Dream library:
        ```bash
        pip install moondream
        ```
    * **requests:** Install for loading images from URLs:
        ```bash
        pip install requests
        ```

2.  **Clone the Repository (Optional):** While not strictly necessary to use the `moonhelp.py` file, you can clone this repository if you want to keep a local copy:
    ```bash
    git clone [repository_url]
    cd [repository_name]
    ```

## Usage

1.  **Import the `moonhelp` class:** In your Python script, import the `moonhelp` class from the `moonhelp.py` file.

    ```python
    from moonhelp import moonhelp
    ```

2.  **Initialize the `moonhelp` object:** Create an instance of the `moonhelp` class, providing the image path or URL.

    ```python
    # Load image from a local file with captioning enabled (default)
    image_helper = moonhelp('path/to/your/image.jpg')

    # Load image from a local file without captioning
    image_helper_no_caption = moonhelp('path/to/your/image.jpg', caption=False)

    # Load image from a URL
    image_helper_url = moonhelp('[https://example.com/image.png](https://www.google.com/search?q=https://example.com/image.png)', NonLocal=True)
    ```

3.  **Access the generated caption:** If captioning is enabled, you can access the caption through the `caption` attribute.

    ```python
    print(image_helper.caption)
    ```

4.  **Detect objects:** Use the `detect()` method to find specific objects in the image. This method draws bounding boxes around the detected items on a copy of the image and returns the modified PIL Image object. It also populates the `boxes`, `points`, and `detected` attributes.

    ```python
    image_with_onions = image_helper.detect('onions', outlinecolor=(255, 0, 0))
    image_with_onions.show() # Display the image with bounding boxes
    print(image_helper.detected) # Print the raw detection dictionary
    print(image_helper.boxes) # Print the list of bounding box coordinates
    print(image_helper.points) # Print the list of center points of the bounding boxes
    ```

5.  **Detect and crop objects:** Use the `detect_crops()` method to detect objects and return a list of cropped PIL Image objects.

    ```python
    onion_head_crops = image_helper.detect_crops('heads')
    if onion_head_crops:
        onion_head_crops[0].show() # Display the first cropped image
    ```

6.  **Query the image:** Use the `query()` method to ask questions about the image.

    ```python
    answer = image_helper.query('why do butter fly?')
    print(answer)
    ```

7.  **Access various attributes:** The `moonhelp` object provides access to the original image, encoded image, detected image, caption, query results, and detection information through its attributes:

    ```python
    # Images
    original_image = image_helper.img
    encoded_image = image_helper.encoded_img
    detected_image = image_helper.detect_image

    # Text
    caption_text = image_helper.caption
    query_question = image_helper.querys_quest
    query_answer = image_helper.querys

    # Detection Information
    detected_item_name = image_helper.detected_item
    bounding_boxes = image_helper.boxes
    center_points = image_helper.points
    cropped_images = image_helper.crops
    raw_detection_data = image_helper.detected
    ```

## Example Usage (from `moonhelp.py`)

```python
import moonhelp

# Load image from a file with caption
moontom = moonhelp.moonhelp('image.jpg')
print(moontom.caption)

# Load image from a file without caption
moontom_no_caption = moonhelp.moonhelp('image.jpg', caption=False)

# Load image from a URL
moontom_url = moonhelp.moonhelp('url', NonLocal=True)

# Detect 'heads' and draw red bounding boxes
onions = moontom.detect('heads', outlinecolor=(255, 0, 0))
onions.show()

# Detect and crop 'heads'
onions_heads = moontom.detect_crops('heads')
if onions_heads:
    onions_heads[0].show()

# Query the image
print(moontom.query('why do butter fly?'))

# Access attributes
# print(moontom.img)
# print(moontom.encoded_img)
# print(moontom.detect_image)
# print(moontom.caption)
# print(moontom.querys_quest)
# print(moontom.querys)
# print(moontom.detected_item)
# print(moontom.boxes)
# print(moontom.points)
# print(moontom.crops)
# print(moontom.detected)
