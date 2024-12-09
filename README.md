# NHL_Assignment_Submission

## Table of Contents
1. [Introduction](#introduction)
2. [Features](#features)
3. [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
    - [Usage](#usage)
4. [Architecture](#architecture)
5. [Tasks](#tasks)
    - [Task 1: Player Detection](#task-1-player-detection)
    - [Task 2: Puck Tracking](#task-2-puck-tracking)
    - [Task 3: Player Speed Estimation](#task-3-player-speed-estimation)
    - [Task 4: Zone Occupancy Analysis](#task-4-zone-occupancy-analysis)
    - [Task 5: Goal Detection](#task-5-goal-detection)
    - [Task 6: Penalty Event Detection](#task-6-penalty-event-detection)
6. [Datasets Used](#datasets-used)
    - [Home, Away, and Referee Dataset](#home-away-and-referee-dataset)
    - [Jersey Number Dataset](#jersey-number-dataset)
7. [Advancements](#advancements)
8. [Shortcomings](#shortcomings)
9. [Contributions](#contributions)
10. [Acknowledgements](#acknowledgements)

---

## Introduction
**Brief overview of the project.**
- **Purpose:** The project aims to develop a set of computer vision and machine learning tasks to analyze and enhance the experience of watching hockey games.
- **Problem it solves:** Automates key processes such as player detection, puck tracking, and event recognition, saving time for analysts and coaches.
- **High-level benefits:** Provides actionable insights, highlights key moments, and improves the understanding of game dynamics in real-time.

---

## Features
- **Player Detection:** Detect and classify players on the ice.
- **Puck Tracking:** Track the puck’s movement and predict future .
- **Player Speed Estimation:** Calculate player speed based on their movement.
- **Detail Analysis:** Analyze the offensive pressure and distance covered for each  team.
- **Goal Detection:** Automatically detect when a goal is scored during gameplay.


---
# Model Architecture

## TPS_ResNet_BiLSTM_Attn [Model Implementation](code/ocr_implement.ipynb)
![](/assets/ocr_parameters.png)


### Transformation
#### TPS_SpatialTransformerNetwork
- **LocalizationNetwork**:
  - **Conv Layers**:
    - Conv2d (1 → 64) → BatchNorm2d → ReLU → MaxPool2d
    - Conv2d (64 → 128) → BatchNorm2d → ReLU → MaxPool2d
    - Conv2d (128 → 256) → BatchNorm2d → ReLU → MaxPool2d
    - Conv2d (256 → 512) → BatchNorm2d → ReLU → AdaptiveAvgPool2d
  - **Fully Connected Layers**:
    - Linear (512 → 256) → ReLU
    - Linear (256 → 40)
- **GridGenerator**

### FeatureExtraction
#### ResNet_FeatureExtractor
- **Conv Layers**:
  - Conv2d (1 → 32) → BatchNorm2d → ReLU
  - Conv2d (32 → 64) → BatchNorm2d → ReLU → MaxPool2d
- **ResNet Layers**:
  - **Layer 1**:
    - BasicBlock (64 → 128)
  - **Layer 2**:
    - BasicBlock (128 → 256)
  - **Layer 3**:
    - BasicBlock (256 → 512)
  - **Layer 4**:
    - BasicBlock (512 → 512)

### Sequence Modeling
- BiLSTM (Input → Hidden)

### Prediction
- Fully Connected Layer

# CNN Model Architecture for Team Detection

## Model Overview
The CNN architecture consists of three convolutional layers followed by pooling, activation functions, and fully connected layers. It is designed for classifying images into three classes: `team_referee`, `team_away`, and `team_home`.

---

## Layer Details

### 1. **Convolutional Layers**
- **Conv1**: 
  - Input Channels: 3 (RGB image)
  - Output Channels: 32
  - Kernel Size: 3x3
  - Padding: 1
- **Conv2**:
  - Input Channels: 32
  - Output Channels: 64
  - Kernel Size: 3x3
  - Padding: 1
- **Conv3**:
  - Input Channels: 64
  - Output Channels: 128
  - Kernel Size: 3x3
  - Padding: 1

### 2. **Pooling Layers**
- **Max Pooling**:
  - Kernel Size: 2x2
  - Stride: 2
  - Applied after each convolutional layer.

### 3. **Fully Connected Layers**
- **Fully Connected 1**:
  - Input Features: \(128 \times 18 \times 18\) (from the final pooling layer)
  - Output Features: 512
- **Dropout**:
  - Probability: 0.5 (to reduce overfitting)
- **Output Layer**:
  - Input Features: 512
  - Output Features: 3 (for three classes)

---

## Activation Function
- **ReLU (Rectified Linear Unit)**:
  - Applied after each convolutional layer and the first fully connected layer.

---

## Forward Propagation Flow
1. Input Image (\(3 \times 150 \times 150\)).
2. **Conv1 → ReLU → Max Pooling**:
   - Output: \(32 \times 75 \times 75\)
3. **Conv2 → ReLU → Max Pooling**:
   - Output: \(64 \times 37 \times 37\)
4. **Conv3 → ReLU → Max Pooling**:
   - Output: \(128 \times 18 \times 18\)
5. Flatten the tensor for the fully connected layers.
6. **Fully Connected 1 → ReLU → Dropout**:
   - Output: 512
7. **Output Layer**:
   - Output: 3 (class probabilities).

---

## Complete Code Representation
-  ```python
  class CNNModel(nn.Module):
      def __init__(self):
          super(CNNModel, self).__init__()
          self.conv1 = nn.Conv2d(3, 32, kernel_size=3, padding=1)
          self.pool = nn.MaxPool2d(kernel_size=2, stride=2, padding=0)
          self.conv2 = nn.Conv2d(32, 64, kernel_size=3, padding=1)
          self.conv3 = nn.Conv2d(64, 128, kernel_size=3, padding=1)
          self.fc1 = nn.Linear(128 * 18 * 18, 512)
          self.dropout = nn.Dropout(0.5)
          self.fc2 = nn.Linear(512, 3)  # Three classes
          
      def forward(self, x):
          x = self.pool(F.relu(self.conv1(x)))
          x = self.pool(F.relu(self.conv2(x)))
          x = self.pool(F.relu(self.conv3(x)))
          x = x.view(-1, 128 * 18 * 18)
          x = F.relu(self.fc1(x))
          x = self.dropout(x)
          x = self.fc2(x)
          return x 

---
## Tasks

### Task 1: Player Detection  
**Objective:**  
Detect and classify players on the ice in real-time.  

**Approach:**  
<!-- 1. **Preprocessing:** Extracted frames from video footage and converted them to grayscale for computational efficiency.  
2. **Model:** Leveraged YOLO11 for real-time object detection, trained on annotated hockey game datasets.  
3. **Output:** Bounding boxes with player labels (`Team White`, `Team Yellow`, `Referee`).   -->

![Player Detection](/assets/player_name.jpg)  

**Video Demonstration:**  
[![Player Detection Video](path/to/video_thumbnail.png)](/penalty/penalty.mp4)

---

### Task 2: Puck Tracking  
**Objective:**  
Track the movement of the puck throughout the game.  

**Approach:**  
1. **Segmentation:** Used HSV color space to isolate the puck based on its color.  
2. **Model:** Implemented Kalman Filters to predict the puck’s position during occlusions.  
3. **Output:** Real-time trajectory of the puck overlaid on the game footage.  

![Puck Tracking](path/to/puck_tracking_image.png)  

**Video Demonstration:**  
[![Puck Tracking Video](path/to/video_thumbnail.png)](https://youtu.be/puck_tracking_example)

---

### Task 3: Player Speed Estimation  
**Objective:**  
Calculate the speed of players during the game.  

**Approach:**  
1. **Coordinate Extraction:** Used the bounding box center coordinates from YOLOv8 outputs.  
2. **Conversion:** Converted pixel-based movements to real-world distances using camera calibration techniques.  
3. **Output:** Speed in km/h displayed near each player.  

![Speed Estimation](path/to/speed_estimation_image.png)  

**Video Demonstration:**  
[![Speed Estimation Video](path/to/video_thumbnail.png)](https://youtu.be/speed_estimation_example)

---

### Task 5: Goal Detection  
**Objective:**  
Detect when a goal is scored during gameplay.  

**Approach:**  
1. **Event Detection:** Monitored the puck’s position relative to goal coordinates.  
2. **Audio Analysis:** Cross-validated with crowd noise spikes using an audio classifier.  
3. **Output:** Timestamped goal events with video highlights.  

![Goal Detection](path/to/goal_detection_image.png)  

**Video Demonstration:**  
[![Goal Detection Video](path/to/video_thumbnail.png)](https://youtu.be/goal_detection_example)

---

## Datasets Used

### 1. Home, Away, and Referee Dataset
- **Description:** This dataset contains frames of players and referees, in separate folders labeled as home team, away team, and referees. It helps in player detection and classification of team affiliations.
- **Features:** 
  - Annotated frames with labels: `Home`, `Away`, `Referee`
- **Usage in Project:** 
  - This dataset is used to train the CNN model for detecting players on the ice and distinguishing between players from different teams and referees.
  - It provides team-specific information, which is crucial for tasks such as **Player Detection** and **Team Analysis**.
- **Training Dataset**
  - Referee
![Refree](/assets/referee.png)
  - Away Team
![Away Team](/assets/away_team.png)
  - Home Team
![Home Team](/assets/home_team.png)
- **Validation Dataset**
![](/assets/validation.png)

### 2. Jersey Number Dataset
- **Description:** This dataset contains images of hockey players with labeled jersey numbers, enabling the identification and classification of individual players based on their jerseys.
- **Features:** 
  - Labeled frames showing players with clear visibility of their jersey numbers.
  - Txt Files with corresponding coordinates.
- **Usage in Project:**
  - Used to track individual players and identify them based on their unique jersey numbers.
  - Helps in tasks such as **Player Detection** and **Player Speed Estimation**, enabling differentiation between players within the same team and providing personalized data for performance metrics.
- **Dataset Sample**
  - 3_925_1
![Image](/assets/ocr_dataset.png)

### 3. Roboflow Datasets
- Combined Dataset (Self Merged)
  - https://universe.roboflow.com/a-tgxjv/nhl-1996-3k7nm/dataset/3
![Class](/assets/class_distribution.png)
![Split](/assets/dataset_processing.png)
- Hockey Stick Dataset (Available on Roboflow Universe)
  - https://universe.roboflow.com/hokey-stick-recognition/our-da/dataset/4
![Class](/assets/stick_dataset.png)
![Split](/assets/stick_split.png)
---

## Advancements
- Details about any new improvements or features implemented.

## Shortcomings
- Details on any limitations or challenges faced in the project.

## Contributions
- List of contributors and their roles in the project.

## Acknowledgements
- Player Tracking and Identification in Ice-Hockey (https://arxiv.org/pdf/2110.03090)
- FeatureExtractor of CRNN (https://arxiv.org/pdf/1507.05717.pdf)
- FeatureExtractor of GRCNN (https://papers.nips.cc/paper/6637-gated-recurrent-convolution-neural-network-for-ocr.pdf)
- FeatureExtractor of FAN (http://openaccess.thecvf.com/content_ICCV_2017/papers/Cheng_Focusing_Attention_Towards_ICCV_2017_paper.pdf)
- https://github.com/clovaai/deep-text-recognition-benchmark
