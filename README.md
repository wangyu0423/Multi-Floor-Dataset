# Multi-Floor-Dataset
Self-collected, Multi-Floor, Public Datasets

## Introduction

*Y. Wang, G. Zhou, C. Xiang, S. Zhang, S. Xu, X. Ma, Q. X and H. Y. Two-Stage Joint Visual and Wireless Feature based Mechanism for Multi-Floor Indoor Localization, Submitted to IEEE Communications Letters.*

  This is the Github repository for the detailed introduction of the experimental environment and data acquisition process of this letter. The main purpose of the repository is to allow easy discussion and the reporting of issues. All data in this dataset are collected by ourselves.
  
  
## Experimental Scene
  Our proposed two-stage localization scheme is verified in the corridor environment of a typical office building, which contains four floors with 4000 square meters area for each floor. In the following figure, the first line are the layout of a single floor and data acquisition equipment, the following are some examples of image of four floors. In the experimental building with four floors, the 1, 2, 3, floors are used as base floors, the 4 floor is used as novel floor to test.

  As shown in this figure, the layout of each floor is more or less the same with dramatically changing lighting conditions throughout the day. Meanwhile, the WiFi signals are in general unreliable, due to the regular daily activities of working staffs. In the above settings, both the signal feature based localization (SFBL) and the visual based localization (VBL) schemes cannot achieve satisfying localization results, which raises a great challenge for the fusion-based localization schemes. All the experimental results of our work are compared in this challenging scenario.
  
<img src="https://github.com/wangyu0423/Multi-Floor-Dataset/blob/main/Environment.png" width="500" height="600" alt="Environment">

More detailed parameter values of our work are listed in the following table. 
Parameter |Meaning of Parameters|Value|
----|----|----|
<img src="http://chart.googleapis.com/chart?cht=tx&chl={N}_{F}" style="border:none;"> |The number of floors in the experimental building|4|
<img src="http://chart.googleapis.com/chart?cht=tx&chl={N}_{RP}" style="border:none;"> |The number of WiFi reference points (RPs)|24|
<img src="http://chart.googleapis.com/chart?cht=tx&chl={N}_{A}" style="border:none;"> |The number of consecutive areas in the target floor|15|
<img src="http://chart.googleapis.com/chart?cht=tx&chl={H}" style="border:none;"> |The pixel of training image (height) |752|
<img src="http://chart.googleapis.com/chart?cht=tx&chl={W}" style="border:none;"> |The pixel of training image (width) |480|
<img src="http://chart.googleapis.com/chart?cht=tx&chl={N}_{T}" style="border:none;"> |The number of training images per floor|500|
<img src="http://chart.googleapis.com/chart?cht=tx&chl={N}_{Q}" style="border:none;"> |The number of test images|500|

## Data Acquisition

### Configuration Sensors
  The main configuration sensors of the mobile robot contain IMU module、camera module、WiFi module.
  
  * IMU module: Providing acceleration, angular velocity and other information.
 
  * Camera module: Providing clear visual images with a resolution of 752x480/60fps.
  
  * WiFi module: Scaning all the channels to establish connections with the access points, whose working frequency band is 2.4 GHz. 

### Process

  In order to obtain the ground truth positions and establish the WiFi fingerprint databases and the image database, we have done the following implementation work. Firstly, according to the mobile robot's installation location, the relative position coordinate of camera and IMU module is obtained. Secondly, the real-time coordinates of the mobile robot on the floor are calculated by constructing a two-dimensional floor map through robot SLAM. Thirdly, multiple cruise points are set on map of SLAM, enabling the robot to complete the task while moving autonomously on the floor corridor. Fourthly, the mobile robot take multiple s-shaped trajectory routes to collect data and several slopes are placed in the corridor to increase the position changes on Z-axis. In order to ensure the user localization accuracy, the mobile robot will collect the wireless signal and image data periodically to keep the WiFi fingerprint databases and the image database updated. The data training process is conducted on a localization server with NVIDIA Titan X GPU with Pytorch platform. Kindly note that when the offline training process is completed, the online localization service will be provided by the indoor localization server.
  
  In the WiFi fingerprint acquisition process, the data acquisition equipment (mobile robot) and its own configured WiFi module are used to scan the deployed WiFi APs in the current scene, establish communication with multiple access points (APs), receive the received signal strength indications (RSSIs) values from different APs at the current sampling location, and save the RSSI set and location coordinates to the database according to a certain format, e.g., 
  
  <div align=center>
  <img src="http://chart.googleapis.com/chart?cht=tx&chl={\mathbf{DB}}_{W}={(\mathcal{R}(\mathbf{L}_{{RP}}^{i}),\mathbf{L}_{{RP}}^{i},\mathbf{F}_{{RP}}^{i})}" style="border:none;">, 
  </div>
  
where <img src="http://chart.googleapis.com/chart?cht=tx&chl=\mathcal{R}(\mathbf{L}_{{RP}}^{i})" style="border:none;"> denotes the APs measured RSSIs, <img src="http://chart.googleapis.com/chart?cht=tx&chl=\mathbf{L}_{RP}^{i}" style="border:none;"> denotes APs locations, <img src="http://chart.googleapis.com/chart?cht=tx&chl=\mathbf{F}_{RP}^{i}" style="border:none;"> denotes the floor index.
  
  As for the image data acquisition process, the data acquisition equipment (mobile robot) and its own configured camera module are used to take images of the experimental scene, and save the images and its corresponding location coordinates to the database according to a certain format, e.g.,
  
  <div align=center>
  <img src="http://chart.googleapis.com/chart?cht=tx&chl={\mathcal{DB}}_{I}={(\mathcal{I}(\mathbf{L}_{I}), \mathbf{L}_{I}, \mathbf{F}_{I})}" style="border:none;">, 
  </div>
  
  where <img src="http://chart.googleapis.com/chart?cht=tx&chl=\mathcal{I}(\mathbf{L}_{I})" style="border:none;"> denotes currently captured image, <img src="http://chart.googleapis.com/chart?cht=tx&chl=\mathbf{L}_{I}" style="border:none;"> denotes the image’s location, <img src="http://chart.googleapis.com/chart?cht=tx&chl=\mathbf{F}_{I}" style="border:none;"> denotes the floor index.  
