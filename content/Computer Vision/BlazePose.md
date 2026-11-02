A lightweight convolutional neural network architecture for [[Pose Estimation]], designed for real-time inference.

During inference it predicts 33 body key points for one person, making it useful for cases like fitness tracking. It is the landmark model used in [[MediaPipe]], a variant using GHUM (Generative 3D Human Shape and Articulated Pose Models), a 3D human shape modelling pipeline that estimates the full 3D body pose of a person in images or videos.

### Pipeline
Blazepose is a 2 model pipeline. Both models are bundled together in the `pose_landmarker` bundle.
- **Pose detector**: looks at the whole frame and finds the person and outputs a bounding box and alignment key points.
- **Pose landmarker**: Adds a complete mapping of the pose. The model outputs an estimate of 33 3D pose landmarks. 


![[blazepose-inference-pipeline.png]]

*Figure 1: BlazePose inference pipeline. Source: [[Documentation#BlazePose: On-device Real-time Body Pose tracking (Bazarevsky et al., 2020)|Bazarevsky et al., 2020, Fig. 1]]*

For video the detector is run only on the first frame. After that the previous frames key points are used to provide alignment (figure 1) for the next frame. If the tracker indicates there is no human present in the frame it will be rerun.
### Sources:
- [[Documentation#Pose Landmarker]] #source/mediapipe/pose-landmarker
- [[Documentation#BlazePose: On-device Real-time Body Pose tracking (Bazarevsky et al., 2020)]] #source/blazepose/paper
- [[Documentation#On-device, Real-time Body Pose Tracking with MediaPipe BlazePose (Google Research blog, 2020)]] #source/blazepose/blog

