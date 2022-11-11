# Gesture-Based-Autonomous-Robot
Repository for RIT Multidisciplinary Senior Design Project ALFRD (P20001), an autonomous gesture recognition robot.

Project Website: https://wiki.rit.edu/display/P20001/Project+Overview 


The application was implemented using python’s kivy language to construct a GUI. Several class files were also created to handle various aspects of the project. A brief description of each relevant file and class file are provided below:

App.py: defines the layout, and behavior of the main page of the GUI application. Several classes are included in this file which define different aspects of the GUI. This is also the file that should be run to run the application.
Gesture.kv: As per the standards of the Kivy language, this file interacts directly with app.py, and more explicitly defines the layout of different elements on the page.
Humans.py: defines the human object which is used to encapsulate the attributes of humans in the environment. In the current version of the application (as of May, 2020) these attributes are identity, current pose, and the predicted gesture.
Robot.py handles all interactions between the robot and the batcave. Due to limitations imposed by COVID-19, a majority of this class has yet to be implemented, though a basic layout is provided in the source code.
GestureClassification.py: handles all tasks related to adding features to the gesture queue, normalizing features, and providing predictions.
GestureSensor.py: interfaces with the available sensors to return an input image. Currently the two supported sensor types are a kinect version 1, and a web camera. Documentation for integrating the Kinect can be found here.
FaceRecognition.py: handles creating facial embeddings as well as returning identifying users in the environment during runtime. This application relies heavily on the face_recognition python library, documentation for which can be found here.
PosePrediction.py: contains the OpenPose prediction model. Additionally, this class handles the initial assignment of identities and poses to the human object, as well as updating these values for subsequent frames. Documentation for the OpenPose implementation used in this project are provided here.
Constants.py: contains global constants used throughout the code.
