# Grocery-Shopper  
Camera & Lidar Vision Automated Grocery Shopper  

---

## Features

### Autonomous Mapping  
The robot autonomously explores the environment using its lidar sensor.  
- Simultaneously detects yellow and green color blobs.  
- When a blob is detected, the robot stores its current GPS position as a waypoint.  

### Odometry-Based Positioning  
- Upon reaching a waypoint, the robot calculates bearing and position errors.  
- A proportional controller adjusts movement until errors fall within a threshold.  
- Once aligned, control switches to manual mode for precise manipulation.  

### Computer Vision  
- Captures raw RGB images from Webots and converts to BGR for OpenCV processing.  
- Converts BGR to HSV color space for accurate color filtering.  
- Uses `cv2.inRange()` to create a binary mask for target colors.  
- Detects external contours and filters by area and aspect ratio.  
- Computes blob centroids using image moments and records GPS coordinates if the blob is new.  
- Displays real-time debug visuals using `cv2.imshow()` with bounding boxes and labels.  

### Navigation with RRT  
- Built upon Homework 3’s RRT implementation.  
- Grid-based sampling simplifies collision checking.  
- Converts grid points back to world coordinates for path planning.  
- Includes obstacle avoidance enhancements.  

### Manual Manipulation  
Keyboard control is used to adjust robot joints and torso for pick-and-place tasks.  

**Controls:**  
- `1-7`: Raise arm joints  
- `q-u`: Lower arm joints  
- `Z/X`: Raise/Lower torso  
- `O/C`: Open/Close gripper  
- `D`: Finish manipulation and return to odometry  

---
