# Gesture-Based Autonomous Robot
**Repository for Rochester Institute of Technology's Multidisciplinary Senior Design Project ALFRD (P20001), an autonomous gesture recognition robot.**

**Project Website:** https://wiki.rit.edu/display/P20001/Project+Overview

**Technical Paper:** https://wiki.rit.edu/download/attachments/202179597/TechnicalPaper_P20001.docx%20%281%29.pdf?version=1&modificationDate=1587659756233&api=v2)

**Project Description:** The goal of this project was to develop a robot that can process user gestures (e.g., sign language) and perform tasks that the user may not be able to complete on their own. The short term goal of this project was to detect one specific gesture and have the robot do one simple task: deliver an object to the user. In the long-term, this project could support programs such as those that advance medical care and quality of life for those in assisted living.

**Main Loop Overview:**

The process begins when the docking/charging station's processing unit is powered on. This subsystem (the docking station) should be directly connected to a wall outlet and should not draw power from the remainder of the system. Incoming images will be streamed from a Kinect or video camera. These images are passed through a mobile implementation of the OpenPose model, which returns a sequence of 2D coordinates for each person in the environment. The input image is also passed to FaceRecognition.py which uses python's _face_recognition_ library and facial embeddings to predict the user identity (users need to be inputted into the system prior to run time.) The skeletal output from openpose is then correlated with the identities returned from FaceRecognition.py and stored as a human object. A separate human object is created for each person on the screen, and is stored in memory as long as that human remains on screen. Each human object also stores a feature queue which contains multiple frame-level features contained in a feature container. 

The contents of the frame-level, feature container are pushed to the multi-frame feature queue, of fixed length _n_. Here, _n_ is set equal to 15. It is important to note that the contents of the feature container will be treated as a high-level real vector for the purposes of later analysis. (Note: In the current version of the system, the feature container is largely unnecessary, as there is only one feature being outputted. However this architecture supports the addition of multiple features at a later date (facial expression, hand pose, etc., which will be combined in the feature container.)  Frame level features  are added to the feature queue until it is full. At this point, when new features are added to the queue, the oldest element is removed from the queue in a first in, first out (FIFO) configuration. After each update to the queue, the current queue contents are compared to the contents of the Gesture Database using a KNN implementation using dynamic time warping as a distance metric. When a gesture is successfully recognized, the system will output this gesture to the robot, via robot.py. 

**Robot Navigation:** The robot will remain at its docking station until a gesture is detected, causing the robot to perform the corresponding task. The robot will use a VFH+ algorithm with a Pixy2 Cam to determine target trajectory and obstacle avoidance. After the task has been completed the robot would return to its docking station.

**Software (Face & Gesture Recognition):** The application was implemented using python’s kivy language to construct a GUI. Several class files were also created to handle various aspects of the project. A brief description of each relevant file and class file are provided below:

- **App.py:** defines the layout, and behavior of the main page of the GUI application. Several classes are included in this file which define different aspects of the GUI. This is also the file that should be run to run the application.

- **Gesture.kv:** As per the standards of the Kivy language, this file interacts directly with app.py, and more explicitly defines the layout of different elements on the page.

- **Humans.py:** defines the human object which is used to encapsulate the attributes of humans in the environment. In the current version of the application (as of May, 2020) these attributes are identity, current pose, and the predicted gesture.

- **Robot.py:** handles all interactions between the robot and the docking station. 

- **GestureClassification.py:** handles all tasks related to adding features to the gesture queue, normalizing features, and providing predictions.

- **GestureSensor.py:** interfaces with the available sensors to return an input image. Currently the two supported sensor types are a kinect version 1, and a web camera. 

- **FaceRecognition.py:** handles creating facial embeddings as well as returning identifying users in the environment during runtime. 

- **PosePrediction.py:** contains the OpenPose prediction model. Additionally, this class handles the initial assignment of identities and poses to the human object, as well as updating these values for subsequent frames.

- **Constants.py:** contains global constants used throughout the code.

