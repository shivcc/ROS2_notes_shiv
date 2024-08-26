# Ros basics 🤖

1.  The name of the py file can be diffrent from the name of the node which can be diff from the name of the executible.
    
2.  The location of the node executible is at /ros2_ws/install/my_py_pkg/lib/my_py_pkg
    
3.  It is easier to call the node by ros2 run my_pkg my_node
    
4.  Setup colcon build and bash script [Colcon and bashrc](../ROS2%20Notebook/Colcon%20and%20bashrc.md)
    

* * *

### Oop tips

its better to use oop in making a node

- make a node class
- put some code in the **init** function in the class
- Init function will run when a class object is created but wont take callbacks
- callbacks will be allowed if the next line is rclpy.spin(node)
- same for c++
- [OOP template](../ROS2%20Notebook/OOP%20template.md)

* * *

### ROS libraries

RCL- ROS client library in C : to use it use rclcpp and rclpy, rcl...  
DDS- data distribution service

### Renaming nodes

- we can run nodes with the same name
    
- but we can also rename the nodes at launch
    
- ros2 run my_py_pkg py_demo_node --ros-args --remap \__node:=abc
    
- refer to ros arguments
    

&nbsp;

- [ ] @TODO Make ros arguments note.

### RQT 

GUI tool to visualize nodes and topic communications. [Turtlesim](../ROS2%20Notebook/Turtlesim.md) for good demo.

### Nodes, publishers and Subscribers
The basic framework/components that make communications work in ROS2. More info in [Nodes, Publishers and Subscribers](../ROS2%20Notebook/Nodes,%20publishers,%20subscribers.md)
