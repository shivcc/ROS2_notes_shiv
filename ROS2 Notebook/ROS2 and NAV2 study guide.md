
2024-09-11 21:24
Tags:  [[ROS2]]

## ROS2 and NAV2 study guide
### 1. Introduction to ROS2 and Nav2 Stack

- *What is ROS2?*: Learn about ROS2, its architecture, and the differences from ROS1.
- *Overview of Nav2*: Understand the purpose of the Nav2 stack in mobile robotics, focusing on autonomous navigation in known and unknown environments.
- *Use cases*: Explore how Nav2 is used in applications like delivery robots, hospital aids, and warehouse automation.

### 2. Prerequisites

- *ROS2 Installation*: Set up ROS2 (preferably the latest distribution) on Ubuntu Linux. Understand workspaces and package management.
- *Basic ROS2 Concepts*: Topics, services, actions, and node management (managed nodes).
- *Tools Setup*: Install simulation environments like Gazebo or RViz for testing.

### 3. Map Creation

- *SLAM Basics*: Learn about SLAM (Simultaneous Localization and Mapping) for generating maps using sensors like LIDAR.
- *Mapping Tools*: Use `slam_toolbox` or Cartographer to generate maps in simulation environments.
- *Hands-on*: Create and save a map using a TurtleBot3 in Gazebo​([Automatic Addison](https://automaticaddison.com/the-ultimate-guide-to-the-ros-2-navigation-stack/))​([Robotics Backend](https://roboticsbackend.com/ros2-nav2-generate-a-map-with-slam_toolbox/)).

### 4. Localization

- *Introduction to Localization*: Learn about AMCL (Adaptive Monte Carlo Localization) for determining a robot's position in a known map.
- *Map Server*: Understand the role of `map_server` in providing maps to the navigation stack.
- *Hands-on*: Set up AMCL in Gazebo or with a real robot​([The Construct](https://www.theconstruct.ai/robotigniteacademy_learnros/ros-courses-library/ros2-navigation/)).

### 5. Path Planning

- *Path Planning Concepts*: Study how the robot plans a path from its current location to a goal while avoiding obstacles.
- *Global and Local Planning*: Learn about the global planner for long-range paths and the local planner for short-term corrections.
- *Hands-on*: Implement and test path planning with a TurtleBot3 simulation in Gazebo​([The Construct](https://www.theconstruct.ai/robotigniteacademy_learnros/ros-courses-library/ros2-navigation/)).

### 6. Navigation Control

- *Costmaps*: Learn about the `costmap_2d` package for representing free and occupied space.
    - *Global and Local Costmaps*: Study how the navigation system builds a real-time map of its environment.
    - *Obstacle Avoidance*: Understand how costmaps help avoid obstacles during navigation.
- *Behavior Trees*: Explore how behavior trees are used to control the decision-making process in the Nav2 stack​( [The Construct](https://www.theconstruct.ai/robotigniteacademy_learnros/ros-courses-library/ros2-navigation/)).

### 7. Obstacle Avoidance

- **Dynamic Obstacle Handling**: Learn about layers of the costmap that handle static and dynamic obstacles.
- **Hands-on**: Set up obstacle avoidance using real-time costmap updates during navigation​([The Construct](https://www.theconstruct.ai/robotigniteacademy_learnros/ros-courses-library/ros2-navigation/))​([Automatic Addison](https://automaticaddison.com/the-ultimate-guide-to-the-ros-2-navigation-stack/)).

### 8. Final Projects

- *Full Navigation System*: Combine all the elements to create a fully autonomous navigation system.
- *Custom Package Development*: Develop your own package to implement navigation for a robot in a simulated or real-world environment​([Automatic Addison](https://automaticaddison.com/the-ultimate-guide-to-the-ros-2-navigation-stack/))​([Robotics Backend](https://roboticsbackend.com/ros2-nav2-generate-a-map-with-slam_toolbox/)).



## Tutorials from official docs


The tutorials are a collection of step-by-step instructions meant to steadily build skills in ROS 2.

The best way to approach the tutorials is to walk through them for the first time in order, as they build off of each other and are not meant to be comprehensive documentation.

For quick solutions to more specific questions, see the [How-to Guides](https://docs.ros.org/en/humble/How-To-Guides.html).
### Beginner: CLI tools
- [Configuring environment](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Configuring-ROS2-Environment.html)
- [Using `turtlesim`, `ros2`, and `rqt`](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Introducing-Turtlesim/Introducing-Turtlesim.html)
- [Understanding nodes](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Nodes/Understanding-ROS2-Nodes.html)
- [Understanding topics](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Topics/Understanding-ROS2-Topics.html)
 - [Understanding services](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Services/Understanding-ROS2-Services.html)   
 - [Understanding parameters](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Parameters/Understanding-ROS2-Parameters.html)
- [Understanding actions](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Actions/Understanding-ROS2-Actions.html)
- [Using `rqt_console` to view logs](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Using-Rqt-Console/Using-Rqt-Console.html)
- [Launching nodes](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Launching-Multiple-Nodes/Launching-Multiple-Nodes.html)
- [Recording and playing back data](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Recording-And-Playing-Back-Data/Recording-And-Playing-Back-Data.html)
### Beginner: Client libraries
- [Using `colcon` to build packages](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html)
- [Creating a workspace](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Creating-A-Workspace/Creating-A-Workspace.html)
- [Creating a package](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Creating-Your-First-ROS2-Package.html)
- [Writing a simple publisher and subscriber (C++)](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Cpp-Publisher-And-Subscriber.html)
- [Writing a simple publisher and subscriber (Python)](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Py-Publisher-And-Subscriber.html)
- [Writing a simple service and client (C++)](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Cpp-Service-And-Client.html)
- [Writing a simple service and client (Python)](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Py-Service-And-Client.html)
- [Creating custom msg and srv files](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Custom-ROS2-Interfaces.html)
- [Implementing custom interfaces](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Single-Package-Define-And-Use-Interface.html)
- [Using parameters in a class (C++)](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Using-Parameters-In-A-Class-CPP.html)
- [Using parameters in a class (Python)](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Using-Parameters-In-A-Class-Python.html)
- [Using `ros2doctor` to identify issues](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Getting-Started-With-Ros2doctor.html)
- [Creating and using plugins (C++)](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Pluginlib.html)
- [Intermediate](https://docs.ros.org/en/humble/Tutorials/Intermediate.html)
- [Managing Dependencies with rosdep](https://docs.ros.org/en/humble/Tutorials/Intermediate/Rosdep.html)
- [Creating an action](https://docs.ros.org/en/humble/Tutorials/Intermediate/Creating-an-Action.html)
- [Writing an action server and client (C++)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Writing-an-Action-Server-Client/Cpp.html)
- [Writing an action server and client (Python)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Writing-an-Action-Server-Client/Py.html)
- [Writing a Composable Node (C++)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Writing-a-Composable-Node.html)
- [Composing multiple nodes in a single process](https://docs.ros.org/en/humble/Tutorials/Intermediate/Composition.html)
- [Monitoring for parameter changes (C++)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Monitoring-For-Parameter-Changes-CPP.html)
- [Launch](https://docs.ros.org/en/humble/Tutorials/Intermediate/Launch/Launch-Main.html)
- [`tf2`](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Tf2-Main.html)
- [Testing](https://docs.ros.org/en/humble/Tutorials/Intermediate/Testing/Testing-Main.html)
- [URDF](https://docs.ros.org/en/humble/Tutorials/Intermediate/URDF/URDF-Main.html)
- [RViz](https://docs.ros.org/en/humble/Tutorials/Intermediate/RViz/RViz-Main.html)

### Advanced
- [Using Fast DDS Discovery Server as discovery protocol [community-contributed]](https://docs.ros.org/en/humble/Tutorials/Advanced/Discovery-Server/Discovery-Server.html)
- [Implementing a custom memory allocator](https://docs.ros.org/en/humble/Tutorials/Advanced/Allocator-Template-Tutorial.html)
- [Unlocking the potential of Fast DDS middleware [community-contributed]](https://docs.ros.org/en/humble/Tutorials/Advanced/FastDDS-Configuration.html)
- [Recording a bag from a node (C++)](https://docs.ros.org/en/humble/Tutorials/Advanced/Recording-A-Bag-From-Your-Own-Node-CPP.html)
- [Recording a bag from a node (Python)](https://docs.ros.org/en/humble/Tutorials/Advanced/Recording-A-Bag-From-Your-Own-Node-Py.html)
- [How to use ros2_tracing to trace and analyze an application](https://docs.ros.org/en/humble/Tutorials/Advanced/ROS2-Tracing-Trace-and-Analyze.html)
- [Reading from a bag file (C++)](https://docs.ros.org/en/humble/Tutorials/Advanced/Reading-From-A-Bag-File-CPP.html)
- [Simulators](https://docs.ros.org/en/humble/Tutorials/Advanced/Simulators/Simulation-Main.html)
- [Security](https://docs.ros.org/en/humble/Tutorials/Advanced/Security/Security-Main.html)

### Demos
- [Using quality-of-service settings for lossy networks](https://docs.ros.org/en/humble/Tutorials/Demos/Quality-of-Service.html)
- [Managing nodes with managed lifecycles](https://docs.ros.org/en/humble/Tutorials/Demos/Managed-Nodes.html)
- [Setting up efficient intra-process communication](https://docs.ros.org/en/humble/Tutorials/Demos/Intra-Process-Communication.html)
- [Recording and playing back data with `rosbag` using the ROS 1 bridge](https://docs.ros.org/en/humble/Tutorials/Demos/Rosbag-with-ROS1-Bridge.html)
- [Understanding real-time programming](https://docs.ros.org/en/humble/Tutorials/Demos/Real-Time-Programming.html)
- [Experimenting with a dummy robot](https://docs.ros.org/en/humble/Tutorials/Demos/dummy-robot-demo.html)    
- [Logging](https://docs.ros.org/en/humble/Tutorials/Demos/Logging-and-logger-configuration.html)
- [Creating a content filtering subscription](https://docs.ros.org/en/humble/Tutorials/Demos/Content-Filtering-Subscription.html)
- [External resources](https://docs.ros.org/en/humble/Tutorials/Demos.html#external-resources)

### Miscellaneous
- [Deploying on IBM Cloud Kubernetes [community-contributed]](https://docs.ros.org/en/humble/Tutorials/Miscellaneous/Deploying-ROS-2-on-IBM-Cloud.html)
- [Using Eclipse Oxygen with `rviz2` [community-contributed]](https://docs.ros.org/en/humble/Tutorials/Miscellaneous/Eclipse-Oxygen-with-ROS-2-and-rviz2.html)
- [Building a real-time Linux kernel [community-contributed]](https://docs.ros.org/en/humble/Tutorials/Miscellaneous/Building-Realtime-rt_preempt-kernel-for-ROS-2.html)
- [Building a package with Eclipse 2021-06](https://docs.ros.org/en/humble/Tutorials/Miscellaneous/Building-ROS2-Package-with-eclipse-2021-06.html)




## Reference

ChatGPT