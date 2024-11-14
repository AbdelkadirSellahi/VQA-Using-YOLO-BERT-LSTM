# **VQA Flood Detection** 🌊💡

A cutting-edge **Visual Question Answering (VQA)** system combining **YOLOv8** for object detection, **BERT + LSTM** for question understanding, and advanced feature fusion to analyze UAV-captured flood imagery and answer context-specific questions.

---

## 🌟 **Overview**

In flood disaster scenarios, rapid analysis of UAV imagery is critical for effective decision-making. This project bridges the gap between **image understanding** and **question answering**, enabling actionable insights for emergency response teams.  

For example:
- **Input**:  
  - Image: A flooded area captured by UAV.  
  - Question: *"Is the entire road flooded?"*  
- **Output**:  
  - *"No."*

---

## 🛠️ **Features**

- **Automated Flood Analysis**: Detect and analyze key flood attributes (roads, water, etc.).  
- **Natural Language Understanding**: Answer user queries with contextual accuracy.  
- **Real-Time Insights**: Ideal for quick and actionable disaster response.  

---

## 🔧 **System Workflow**

1. **Input**:  
   - Image (UAV-captured flood imagery).  
   - User question (e.g., *"how many buildings are there in the image?"*).  

2. **Image Processing**:  
   - **Object Detection (YOLOv8)**: Detects roads, water, cars, and other objects.  

3. **Question Understanding**:  
   - Tokenize and encode the question using **BERT**.  
   - Extract contextual features via **LSTM**.

4. **Feature Fusion**:  
   - Combines image and question features into a joint representation.

5. **Answer Prediction**:  
   - Outputs an answer (*Yes*, *No*, or specific numeric details).  

---

## 🎨 **Model Architecture**

- **YOLOv8**:
  - Pretrained for flood-specific object detection.
- **BERT + LSTM**:
  - **BERT** encodes the question into embeddings.  
  - **LSTM** captures sequential dependencies.
- **Feature Fusion**:
  - Combines textual and visual features for reasoning.

---

## 📂 **Dataset**
[**FloodNet Challenge 2021 - Track 2**](https://github.com/BinaLab/FloodNet-Challenge-EARTHVISION2021?fbclid=IwAR2XIwe5nJg5VSgxgCldM7K0HPtVsDxB0fjd8cJJZfz6WMe3g0Pxg2W3PlE)

### **Structure**:
- **Annotations**:
  - JSON file linking questions, image paths, and answers.  
- **Images**:  
  - UAV-captured flood scenes with diverse scenarios.

### **Example**:
```json
{
  "image_id": "flood_road_01.jpg",
  "question": "Is the road flooded?",
  "answer": "Yes"
}
```

### **Answer Mapping**:
- *Yes*: 0  
- *No*: 1
- ...
---

## 🚀 **Training the Model**

1. **Setup**:
   - Optimizer: Adam  
   - Learning Rate: 0.0001  
   - Loss Function: CrossEntropyLoss  

2. **Steps**:
   - Extract visual features using YOLOv8.  
   - Process textual features using BERT + LSTM.  
   - Fuse features and pass through the VQA module.  
   - Compute loss and update weights.

3. **Logging**:
   - Tracks accuracy and loss per epoch.  

4. **Model Saving**:
   - Saves weights after every epoch.  

---

## 🧪 **Testing & Inference**

### **Evaluation Metrics**:
- **Question-wise Accuracy**: Measures answer correctness per question type.  
- **Overall Accuracy**: Evaluates the model's performance across the dataset.

### **Testing Example**:
```python
from PIL import Image

image_path = "flood_image.jpg"
question = "how many flooded buildings are there in the image?"

# Load the image
image = Image.open(image_path)

# Perform inference
predicted_answer = infer(image, question)

print(f"Predicted Answer: {predicted_answer}")
```

---

## ⚠️ **Limitations**

- Relies on predefined answer categories (*Yes*, *No*, etc.).  
- Requires high-quality annotations for optimal performance.  
- Needs GPU for efficient training and inference.  

---

## 💬 **Contact**

Feel free to open an issue or reach out for collaboration!  

**Author**: *Abdelkadir Sellahi*

**Email**: *abdelkadirsellahi@gmail.com* 

**GitHub**: [Abdelkadir Sellahi](https://github.com/AbdelkadirSellahi)
