# Sign Language to Text Conversion: Real-Time Application

## Overview
This project implements a real-time sign language-to-text conversion system. Using computer vision and deep learning, the system captures sign language gestures via a webcam, processes the images using several CNN-based models, and converts recognized gestures into text. A layered prediction strategy refines ambiguous cases by using multiple specialized models, and a suggestion engine (via Hunspell) enhances word formation. The system is designed as a user-friendly desktop application with a graphical interface built using Tkinter.

---

## Dataset Description
- **Source & Structure:**  
  The dataset consists of sign language gesture images organized into training and testing directories. The folder structure (automatically created by the `FoldersCreation.py` script) contains separate subdirectories for each letter (A–Z) and a 'blank' class for non-gesture frames.
  
- **Data Characteristics:**  
  - **Image Format:** Grayscale images resized to 128×128 pixels.
  - **Classes:** 27 categories (26 letters + blank) representing different sign language gestures.
  - **Preprocessing:** Images are normalized and augmented during training to improve the model's robustness.

---

## Methodology
1. **Data Preparation & Organization:**
   - The `FoldersCreation.py` script automatically creates the required directory structure for storing training and testing images.
   - Images are collected and organized into folders labeled A–Z (and a blank folder) to facilitate supervised learning.

2. **Model Training:**
   - **Architecture:**  
     A Convolutional Neural Network (CNN) is used for gesture recognition. The primary model (loaded from `model_new.json`) consists of multiple convolutional layers with ReLU activations, followed by max-pooling, flattening, and dense layers with dropout for regularization. The final output layer uses a softmax activation to classify into 27 classes.
   - **Layered Predictions:**  
     To handle ambiguous cases, additional specialized models (e.g., those loaded from `model-bw_dru.json`, `model-bw_tkdi.json`, and `model-bw_smn.json`) are employed. These secondary models refine predictions when the primary model’s output belongs to specific ambiguous groups (e.g., letters with similar hand shapes).
   - **Training Environment:**  
     Models are trained using Keras with TensorFlow as the backend. Training includes data augmentation and optimization techniques to improve classification accuracy.

3. **Real-Time Application:**
   - **Video Capture & Preprocessing:**  
     The application (implemented in `Application.py`) captures frames from the webcam using OpenCV. Frames are flipped, cropped, resized, and thresholded to extract the hand gesture region.
   - **Prediction Pipeline:**  
     The processed frame is fed into the primary and (if needed) secondary models to obtain the predicted gesture. The system aggregates predictions over time to determine stable outputs.
   - **User Interface:**  
     A Tkinter-based GUI displays the live video feed, processed image, current predicted symbol, word, and sentence. Hunspell is used to provide word suggestions to assist in forming coherent text.

---

## Technical Findings
- **Model Architecture & Performance:**
  - The CNN architecture efficiently classifies 128×128 grayscale images into 27 classes.
  - Layered prediction improves overall system accuracy by addressing ambiguous predictions through specialized models.
  - Real-time processing is achieved by optimizing image preprocessing and model inference pipelines.
  
- **Processing Efficiency:**
  - The system leverages OpenCV for rapid frame capture and image transformations.
  - Tkinter provides a lightweight yet effective graphical interface for real-time feedback.
  
- **Robustness & Accuracy:**
  - The integration of multiple models and temporal aggregation of predictions reduces the impact of noise and transient misclassifications.
  - The use of Hunspell enhances text formation by offering context-aware suggestions.

---

## Business Insights & Findings
- **Accessibility & Communication:**  
  This application serves as an assistive technology tool, enabling effective communication for individuals who rely on sign language. It has potential applications in education, accessibility, and customer support.
  
- **Enhanced User Interaction:**  
  The real-time conversion of sign language into text enables seamless communication and can be integrated into broader platforms (e.g., virtual assistants or teleconferencing tools) to improve user engagement.
  
- **Scalability & Commercialization:**  
  With further refinement and robust training on larger datasets, the system can be deployed in commercial settings such as call centers, healthcare, and educational institutions to facilitate inclusive communication.
  
- **Data-Driven Improvements:**  
  The project demonstrates the importance of combining multiple specialized models and user feedback (via suggestion systems) to enhance system performance—a strategy that can be applied to other real-time gesture or speech recognition systems.

---

## Hardware, Software Requirements & Libraries

### Hardware Requirements
- **Minimum:**  
  A standard desktop or laptop with at least 8 GB of RAM and a built-in or external webcam.
- **Recommended:**  
  A system with a multi-core CPU; GPU support is advantageous for faster model inference but not mandatory for deployment.

### Software Requirements
- **Operating System:**  
  Windows, macOS, or Linux
- **Development Environment:**  
  Python 3.x, Jupyter Notebook or any Python IDE
- **User Interface:**  
  Tkinter (for the GUI)

### Libraries & Tools
- **Computer Vision & Image Processing:**  
  - OpenCV
  - PIL (Pillow)
- **Deep Learning & Model Handling:**  
  - Keras
  - TensorFlow
- **GUI Development:**  
  - Tkinter
- **Spell Checking & Suggestions:**  
  - Hunspell
  - PyEnchant
- **Utilities:**  
  - NumPy
  - OS, sys, time, operator, string (standard libraries)

Refer to the `requirements.txt` for a complete list of dependencies.

---

## How to Run
1. **Clone the Repository:**  
   ```bash
   git clone https://github.com/your-repo/Sign-Language-To-Text-Conversion.git
   cd Sign-Language-To-Text-Conversion
