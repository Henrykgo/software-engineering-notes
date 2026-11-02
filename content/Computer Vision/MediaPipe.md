MediaPipe is Google's open source library for running ML models on device. 

### MediaPipe Tasks
A collection of pre-built on device ML tasks (body poses, hands, face, object detection) that you can run without 
training a model or building a pipeline. It is accessed through the Tasks API (`mediapipe.tasks`, the python package). 

Each task has 2 parts: a downloadable `.task` file (a bundle containing the model and its metadata) and a class in `mediapipe.tasks` (python here, e.g. `PoseLandmarker`) that you can configure with an options object, including a running mode (image, video, or livestream). You pass in frames and it returns landmarks.

The model used for Pose Landmarker is [[BlazePose]].
### MediaPipe Framework
The low-level component Tasks are built on. Written in C++
### Source
- [[Documentation#MediaPipe Solutions guide]] #source/mediapipe/solutions-guide