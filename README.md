# Candy Detection Using YOLO11s

## Overview

This project uses **YOLO11s**, a pretrained object detection model from Ultralytics, fine-tuned to detect and classify 11 types of candy in images.

The project covers dataset preparation, annotation handling, model training, validation, and prediction.

## Technologies Used

- Python
- Ultralytics YOLO11s
- PyTorch
- Google Colab
- Object Detection

## Candy Classes

The model detects 11 candy classes:

1. MMs_peanut
2. MMs_regular
3. airheads
4. gummy_worms
5. milky_way
6. nerds
7. skittles
8. snickers
9. starbust
10. three_musketeers
11. twizzlers

*Note: `starbust` retains the spelling used in the original dataset.*

## Dataset

The dataset contains 162 images with corresponding YOLO-format annotation files.

| Dataset split | Images |
|---|---:|
| Training | 145 |
| Validation | 17 |
| Total | 162 |

The `train_val_split.py` script divides the dataset into training and validation sets. Each annotation file contains a class ID and normalized bounding box coordinates for the objects in its corresponding image.

The dataset is not included in this repository. Ensure that you have permission to redistribute it before sharing the images publicly.

## Model Training

The model was initialized with pretrained YOLO11s weights and fine-tuned on the custom candy dataset.

**Training configuration:**

- Model: YOLO11s
- Epochs: 60
- Image size: 640 × 640
- Batch size: 16
- Number of classes: 11

## Validation Results

The model achieved the following metrics on the 17-image validation set:

| Metric | Score |
|---|---:|
| Precision | 0.979 |
| Recall | 0.968 |
| mAP@50 | 0.972 |
| mAP@50–95 | 0.886 |

These results are from a small validation set and should not be interpreted as a guarantee of performance on unseen, real-world images. Further testing on a larger and more diverse dataset is recommended.

## Repository Structure

```text
candy-detection-yolo/
├── README.md
├── candy_detection.ipynb
├── train_val_split.py
├── data.yaml
├── classes.txt
└── my_model.pt
```

- `README.md`: Project description, setup instructions, and validation metrics.
- `candy_detection.ipynb`: Notebook containing dataset preparation, training, validation, and prediction.
- `train_val_split.py`: Script for splitting the dataset.
- `data.yaml`: YOLO dataset configuration.
- `classes.txt`: List of candy class names.
- `my_model.pt`: Trained model weights.

## Installation

Install the required dependency:

```bash
pip install ultralytics
```

## Run Predictions

Load the trained model and run it on an image:

```python
from ultralytics import YOLO

model = YOLO("my_model.pt")

results = model.predict(
    source="candy.jpg",
    conf=0.25,
    save=True
)
```

Replace `candy.jpg` with the path to your image. The prediction image, including detected objects and bounding boxes, is saved by Ultralytics in its output directory.

## Future Improvements

- Expand the dataset with more varied candy images.
- Evaluate performance on a larger unseen test set.
- Improve detection of weaker-performing classes.
- Explore real-time inference and deployment.

## License and Attribution

Add the appropriate project license and dataset attribution after checking the original dataset's terms of use.

---

**Author:** Shreyansh Bhalla
