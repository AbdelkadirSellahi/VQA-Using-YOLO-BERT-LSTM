# VQA Flood Detection

A Visual Question Answering (VQA) system designed to analyze UAV imagery of flood scenes and answer natural language questions about what is visible. The model uses YOLOv8 for object detection and combines BERT with an LSTM to understand questions, fusing visual and textual features to generate precise answers.

---

## Overview

During flood emergencies, quick interpretation of aerial imagery can support life-saving decisions. This system helps responders by answering specific questions about flood conditions — such as “Is the road flooded?” or “How many buildings are affected?” — based solely on an image and a text query.

For example:
- **Input**:  
  - Image: Aerial photo of a flooded neighborhood.  
  - Question: *"Is the entire road flooded?"*  
- **Output**:  
  - *"No."*

The goal is not to generate free-form responses, but to select the most accurate answer from a predefined set of options.

---

## Features

- **Automated Flood Analysis**: Identifies key elements like roads, water, and structures in UAV images.
- **Context-Aware Question Understanding**: Uses BERT and LSTM to interpret the meaning and intent behind user questions.
- **Actionable Outputs**: Delivers clear, binary or numeric answers suitable for rapid decision-making in disaster response.

---

## System Workflow

1. **Input**  
   - An image captured by a UAV showing a flood scene.  
   - A natural language question related to the image (e.g., *“how many buildings are there in the image?”*).

2. **Image Processing**  
   - YOLOv8 detects objects and regions relevant to flooding — including roads, water bodies, buildings, and vehicles — returning bounding boxes and class labels.

3. **Question Understanding**  
   - The question is tokenized and encoded using BERT to produce contextual embeddings.  
   - These embeddings are then processed by an LSTM layer to capture sequential dependencies in the question structure.

4. **Feature Fusion**  
   - Visual features from YOLOv8 and textual features from BERT+LSTM are combined into a single representation that links what is seen in the image with what is being asked.

5. **Answer Prediction**  
   - The fused features are passed through a classification head to predict one of several predefined answers — such as *Yes*, *No*, or a number — based on the content of the image and the nature of the question.

---

## Model Architecture

- **YOLOv8**:  
  Pretrained for detecting flood-related objects in aerial imagery. Outputs bounding boxes and class labels for detected regions.

- **BERT + LSTM**:  
  - BERT encodes the input question into a high-dimensional semantic vector.  
  - The LSTM layer refines this representation by modeling word order and context within the question.

- **Feature Fusion Layer**:  
  Combines the output from YOLOv8 and BERT+LSTM into a unified feature vector. This allows the model to reason across modalities — understanding both the visual scene and the linguistic query together.

---

## Dataset

The system is trained and evaluated using the [FloodNet Challenge 2021 - Track 2](https://github.com/BinaLab/FloodNet-Challenge-EARTHVISION2021?fbclid=IwAR2XIwe5nJg5VSgxgCldM7K0HPtVsDxB0fjd8cJJZfz6WMe3g0Pxg2W3PlE).

### Structure
- **Annotations**: A JSON file mapping each image to its associated questions and correct answers.
- **Images**: Aerial photographs of real-world flood events, captured by UAVs under varying conditions.

### Example Entry
```json
{
  "image_id": "flood_road_01.jpg",
  "question": "Is the road flooded?",
  "answer": "Yes"
}
```

### Answer Mapping
Answers are mapped to integer indices:
- *Yes*: 0  
- *No*: 1  
- ... (other categories as defined in the dataset)

---

## Training the Model

### Setup
- Optimizer: Adam  
- Learning Rate: 0.0001  
- Loss Function: CrossEntropyLoss  

### Steps
1. Load images and corresponding questions from the dataset.
2. Extract visual features using YOLOv8.
3. Encode questions using BERT, followed by LSTM processing.
4. Fuse the two feature sets into a joint representation.
5. Pass the fused features through the final classifier to predict an answer.
6. Compute loss against ground truth and update model weights.

### Logging & Saving
- Training and validation accuracy and loss are logged per epoch.
- Model weights are saved after every epoch to allow checkpointing and selection of the best-performing version.

---

## Testing & Inference

### Evaluation Metrics
- **Question-wise Accuracy**: Performance broken down by question type (e.g., Yes/No vs. counting).
- **Overall Accuracy**: Total percentage of correctly answered questions across the test set.

### Example Usage
```python
from PIL import Image

image_path = "flood_image.jpg"
question = "how many flooded buildings are there in the image?"

image = Image.open(image_path)
predicted_answer = infer(image, question)

print(f"Predicted Answer: {predicted_answer}")
```

---

## Limitations

- Limited to a fixed set of possible answers; cannot generate novel responses.
- Performance depends heavily on the quality and coverage of training annotations.
- Requires GPU acceleration for reasonable training and inference speeds.

---

## Contact

For questions or collaboration, feel free to open an issue or reach out directly.

**Author**: Abdelkadir Sellahi  
**Email**: abdelkadirsellahi@gmail.com  
**GitHub**: [Abdelkadir Sellahi](https://github.com/AbdelkadirSellahi)
