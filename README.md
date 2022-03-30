# Multi-Floor-Dataset
Self-collected, Multi-Floor, Public Datasets

# Introduction

Our proposed two-stage localization scheme is verified in the corridor environment of a typical office building, which contains four floors with 4000 square meters area for each floor. In this figure, the first line are the layout of a single floor and data acquisition equipment, the following are some examples of image of four floors. In the experimental building with four floors, the 1, 2, 3, floors are used as base floors, the 4 floor is used as novel floor to test.

As shown in this figure, the layout of each floor is more or less the same with dramatically changing lighting conditions throughout the day. Meanwhile, the WiFi signals are in general unreliable, due to the regular daily activities of working staffs. In the above settings, both the signal feature based localization (SFBL) and the visual based localization (VBL) schemes cannot achieve satisfying localization results, which raises a great challenge for the fusion-based localization schemes. All the experimental results of our work are compared in this challenging scenario.

<img src="https://github.com/wangyu0423/Multi-Floor-Dataset/blob/main/Environment.png" width="500" height="600" alt="Environment">

# The Scene of Data acquisition


# The Process of Data acquisition
As for the image data acquisition process, the data acquisition equipment (mobile robot) and its own configured camera module are used to take images of the experimental scene, and save the images and its corresponding location coordinates to the database according to a certain format, e.g., {\mathcal{DB}}_\mathcal{I}={(\mathcal{I}(\mathfrak{L}_\mathcal{I}),\mathfrak{L}_\mathcal{I},\mathcal{F}_\mathcal{I})}, where \mathcal{I}(\mathfrak{L}_\mathcal{I}) denotes currently captured image, \mathfrak{L}_\mathcal{I}\ denotes the image’s location, \mathcal{F}_\mathcal{I} denotes the floor index. 
