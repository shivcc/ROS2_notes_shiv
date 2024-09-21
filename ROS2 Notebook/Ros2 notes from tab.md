	
2024-09-06 16:43
Tags: [[ROS2]]

## Ros2 notes from tab

#### ROS 2  IMPORTANT NOTES  
-  self driving robot  
- simulator  
- Controller commands → wheel control  
- Differential Kinematics  
- measure rotation of the wheels and track the motion of the robot  
 - Odomerry  
 - fusing data from multiple sensors to increase accuracy  
 - sensor fusion  
- noise and filters

### Maping and localization
 - laser scanner → generate map
- SLAM. simultaneous localization and maping
- Localize - estimate its position in map
- maping - generate/update the map
### Planning and Navigation
 - path planning algorithmins
 - Obstacle Avoidance
- Behaviours trees
### Computer vision
- visual odometery  
 - Visual slam  
 - Obj rec and tracking 
### R0S2
 - Person tracking and following
 - diriver and communication with
- hardware is done by ros2 so changes in code/algorithm not needed
 - Fleets
 - serial 10
- is security
 - realtime systems (SLAM)
- DDS communication protocol
- RCL - robot client library 
### Topic communication 

![[Screenshot_20240906_171044_Samsung Notes.jpg]]

### Types of communication 
![[Screenshot_20240906_173811_Samsung Notes.jpg]]
### Package management  

- modular software ( Packages)  
- simulation  
- control  
- vision  
- kinematic  
- voice recoy  
+ Make your own package  
- underlay overlay  
- Bg processes p user developed code  
 - libraries  
 - Default packages  
 - A package will run in ur robot
## Reference
