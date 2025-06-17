# Grocery-Shopper
Camera &amp; lidar vision automated grocery shopper 

----------------------------------------------------

Our robot implements the following features:

Autonomous Mapping :
The robot moves autonomously capturing the whole map using its lidar sensor. Color blob detection is called simultaneously, which stores the position of the robot at the time it detects yellow or green blobs as an initial waypoint. 

Odometry :
Once the robot reaches an initial waypoint near a cube, it repeatedly runs calculations on its bearing and position errors. These error values are fed into a proportional controller. When error values are within the threshold, the program runs manual mode for pick and place. 

Computer Vision :
The robot’s camera captures an image, which is retrieved as raw RGB pixel data from Webots and manually converted to a NumPy array in BGR format (as OpenCV expects BGR, not RGB). The BGR image is then converted to HSV (Hue, Saturation, Value) color space for higher accuracy (BGR threshold wasn’t working well). A binary mask is created using cv2.inRange() that filters out everything except pixels within the color range. Using cv2.findContours(), external contours are identified in the binary mask. Each contour's area is checked to filter out noise. The centroid of the blob is computed using image moments (cv2.moments()). A bounding box is drawn, and the aspect ratio of each blob is checked (should be around 1:1 for cubes). The GPS coordinates of the robot at the time of detection are recorded and stored if the centroid corresponds to a new, unique cube position (checked via a spatial threshold in a function called is_new_waypoint()). The mask and the frame are displayed using cv2.imshow(), showing detected rectangles and labeled centroids dot for real-time debugging and validation.

Navigation using RRT : 
Homework 3 was used as a base code for the RRT algorithm. Jack built a base code to work on our map, then Anja added the obstacle avoidance logic. Algorithm takes in grid points instead of the world, making it less complex. Code converts back to world coordinates for odometry.

Manual Manipulation : 
Keyboard input was used  to increment or decrement the robot's arm joint and torso by 0.025 radians. 
Manual key command follows:
 - 1-7 = Raise arm joints
 - q-u = Lower arm joints
 - Z/X = Raise/Lower torso
 - D = Done with pick and place. (switches back to odometry)
 - O/C = Open/Close gripper



