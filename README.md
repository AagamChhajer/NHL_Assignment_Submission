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

## Getting Started

## Tasks

### Task 1: Player Detection  
**Objective:**  
Detect and classify players on the ice in real-time.  

**Approach:**  
1. **Preprocessing:** Extracted frames from video footage and converted them to grayscale for computational efficiency.  
2. **Model:** Leveraged YOLOv8 for real-time object detection, trained on annotated hockey game datasets.  
3. **Output:** Bounding boxes with player labels (`Team White`, `Team Yellow`, `Referee`).  

![Player Detection](/output/player_name.jpg)  

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

### Task 4: Zone Occupancy Analysis  
**Objective:**  
Analyze how much time each team spends in different zones of the rink.  

**Approach:**  
1. **Zone Division:** Divided the rink into three zones (defensive, neutral, offensive).  
2. **Tracking:** Mapped player positions to zones using pre-defined coordinates.  
3. **Output:** Heatmaps showing occupancy percentage by team.  

![Zone Occupancy](path/to/zone_occupancy_image.png)  

**Video Demonstration:**  
[![Zone Occupancy Video](path/to/video_thumbnail.png)](https://youtu.be/zone_occupancy_example)

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

### Task 6: Penalty Event Detection  
**Objective:**  
Identify and categorize penalty events during the game.  

**Approach:**  
1. **Player Behavior Analysis:** Used pose estimation to detect specific gestures indicating penalties (e.g., high stick).  
2. **Referee Signal Recognition:** Detected referee’s gestures and validated with game logs.  
3. **Output:** Highlighted video clips of penalty events with descriptive labels.  

![Penalty Detection](path/to/penalty_detection_image.png)  

**Video Demonstration:**  
[![Penalty Detection Video](path/to/video_thumbnail.png)](https://youtu.be/penalty_detection_example)

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
!(/assets/validation.png)

### 2. Jersey Number Dataset
- **Description:** This dataset contains images of hockey players with labeled jersey numbers, enabling the identification and classification of individual players based on their jerseys.
- **Features:** 
  - Labeled frames showing players with clear visibility of their jersey numbers.
  - Annotations for player tracking and identification.
- **Usage in Project:**
  - Used to track individual players and identify them based on their unique jersey numbers.
  - Helps in tasks such as **Player Detection** and **Player Speed Estimation**, enabling differentiation between players within the same team and providing personalized data for performance metrics.

---

## Advancements
- Details about any new improvements or features implemented.

## Shortcomings
- Details on any limitations or challenges faced in the project.

## Contributions
- List of contributors and their roles in the project.

## Acknowledgements
- Recognition for resources or individuals that have helped with the project.
- Player Tracking and Identification in Ice-Hockey (https://arxiv.org/pdf/2110.03090)
- FeatureExtractor of CRNN (https://arxiv.org/pdf/1507.05717.pdf)
- FeatureExtractor of GRCNN (https://papers.nips.cc/paper/6637-gated-recurrent-convolution-neural-network-for-ocr.pdf)
- FeatureExtractor of FAN (http://openaccess.thecvf.com/content_ICCV_2017/papers/Cheng_Focusing_Attention_Towards_ICCV_2017_paper.pdf)
- https://github.com/clovaai/deep-text-recognition-benchmark
