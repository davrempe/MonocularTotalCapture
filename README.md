# Fork of Monocular Total Capture for "Contacts and Human Dynamics from Monocular Video"

The original README is below with dependencies and installation instructions. These must be followed in order to run this code as part of the contacts and human dynamics pipeline.

For installation, it is helpful to look at the provided [docker file](https://github.com/CMU-Perceptual-Computing-Lab/MonocularTotalCapture/blob/master/Dockerfile). A few other installation tips:
* In order to use the required version of OpenCV with CUDA 9.0, you need to patch the source with the changed specified [in this repository](https://github.com/davidstutz/opencv-2.4-cuda-9-patch).
* Build Caffe from source rather than along with OpenPose

## Notable Changes from the Original Repo
* New [program to visualize total capture results](./FitAdam/viz_results.cpp).
* New [program to process total capture results](./FitAdam/process_results.cpp) and write them out to be used in the contacts and human dynamics pipeline.

==================================================================================================================

# Monocular Total Capture
Code for CVPR19 paper "Monocular Total Capture: Posing Face, Body and Hands in the Wild"

Project website: [<http://domedb.perception.cs.cmu.edu/mtc.html>]

# Dependencies
This code is tested on a Ubuntu 16.04 machine with a GTX 1080Ti GPU, with the following dependencies.
1. ffmpeg
2. Python 3.5 (with TensorFlow 1.5.0, OpenCV, Matplotlib)
3. cmake >= 2.8
4. OpenCV 2.4.13 (compiled with CUDA)
5. Ceres-Solver 1.13.0 (with SuiteSparse)
6. OpenGL, GLUT, GLEW
7. libigl <https://github.com/libigl/libigl>
8. wget
9. OpenPose

# Installation
1. git clone this repository; suppose the main directory is ${ROOT} on your local machine.
2. "cd ${ROOT}"
3. "bash download.sh"
4. git clone OpenPose <https://github.com/CMU-Perceptual-Computing-Lab/openpose> and compile. Suppose the main directory of OpenPose is ${openposeDir}, such that the compiled binary is at ${openposeDir}/build/examples/openpose/openpose.bin
5. Edit ${ROOT}/run_pipeline.sh: set line 13 to you ${openposeDir}
4. Edit ${ROOT}/FitAdam/CMakeLists.txt: set line 13 to the "include" directory of libigl (this is a header only library)
5. "cd ${ROOT}/FitAdam/ && mkdir build && cd build"
6. "cmake .."
7. "make -j12"

# Usage
1. Suppose the video to be tested is named "${seqName}.mp4". Place it in "${ROOT}/${seqName}/${seqName}.mp4".
2. If the camera intrinsics is known, put it in "${ROOT}/${seqName}/calib.json" (refer to "POF/calib.json" for example).
3. In ${ROOT}, run "bash run_pipeline.sh ${seqName}"; if the subject in the video shows only upper body, run "bash run_pipeline.sh ${seqName} -f".

# Examples
"download.sh" automatically download 2 example videos to test. After successful installation run
```
bash run_pipeline.sh example_dance
```
or
```
bash run_pipeline.sh example_speech -f
```

Note: Facial expression of Adam model is unavailable to copyright issue.
