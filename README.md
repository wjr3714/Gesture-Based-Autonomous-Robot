# Gesture-Based-Autonomous-Robot
**Repository for RIT Multidisciplinary Senior Design Project ALFRD (P20001), an autonomous gesture recognition robot.**

**Project Website:** https://wiki.rit.edu/display/P20001/Project+Overview 

**Project Description:** The goal of this project was to develop a robot that can process user gestures (e.g., sign language) and perform tasks that the user may not be able to complete on their own. The short term goal of this project was to detect one specific gesture and have the robot do one simple task: deliver an object to the user. In the long-term, this project could support programs such as those that advance medical care and quality of life for those in assisted living.

**Robot Navigation:** The robot will remain at its docking station until a gesture is detected, causing the robot to perform the corresponding task. The robot will use a VFH+ algorithm with a Pixy2 Cam to determine target trajectory and obstacle avoidance. After the task has been completed the robot would return to its docking station.

**Software (Face & Gesture Recognition):** The application was implemented using python’s kivy language to construct a GUI. Several class files were also created to handle various aspects of the project. A brief description of each relevant file and class file are provided below:

**App.py:** defines the layout, and behavior of the main page of the GUI application. Several classes are included in this file which define different aspects of the GUI. This is also the file that should be run to run the application.

**Gesture.kv:** As per the standards of the Kivy language, this file interacts directly with app.py, and more explicitly defines the layout of different elements on the page.

**Humans.py:** defines the human object which is used to encapsulate the attributes of humans in the environment. In the current version of the application (as of May, 2020) these attributes are identity, current pose, and the predicted gesture.

**Robot.py:** handles all interactions between the robot and the docking station. 

**GestureClassification.py:** handles all tasks related to adding features to the gesture queue, normalizing features, and providing predictions.

**GestureSensor.py:** interfaces with the available sensors to return an input image. Currently the two supported sensor types are a kinect version 1, and a web camera. 

**FaceRecognition.py:** handles creating facial embeddings as well as returning identifying users in the environment during runtime. 

**PosePrediction.py:** contains the OpenPose prediction model. Additionally, this class handles the initial assignment of identities and poses to the human object, as well as updating these values for subsequent frames.

**Constants.py:** contains global constants used throughout the code.
