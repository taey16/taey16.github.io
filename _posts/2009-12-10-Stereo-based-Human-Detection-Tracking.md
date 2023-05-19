## Realtime Stereo-based Human Detection and Tracking for Robot-Vision.

### Introduction
By RGB-D sensory inputs, we design 4 directional 2D elliptical filters (4D2DEFs) and convolve them on a disparity-map so as to localize multiple humans. Resulting candidate blobs are further verified by either  detecting the face or matching head-shoulder shapes. To preserve person's ID, we make use of the particle filtering for robust tracking. Note that this algorithm is dedicated to applying mobile robots so that we do not use any background modeling technique, and works in real-time.

#### Keywords:
Robot Vision, Human Detection/Tracking

To get further details, check out our paper: <br>
[Pose Robust Human Detection in Depth Image Using Four Directional 2D Elliptical Filters](https://github.com/taey16/taey16.github.io/blob/main/assets/papers/2009_PoseRobustHumanDetectionInDepthImage.pdf), IEEE ISM, 2009
