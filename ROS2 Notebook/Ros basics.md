Tag: [[ROS2]], [[node ros2]], [[oop]]
# Ros basics 🤖

1. You must [[Setup]] first.
2. The name of the py file can be different from the name of the node which can be diff from the name of the executable.
    
2.  The location of the node executable is at /ros2_ws/install/my_py_pkg/lib/my_py_pkg
    
3.  It is easier to call the node by ros2 run my_pkg my_node
    
4.  Setup colcon build and bash script [Colcon and bashrc](Colcon%20and%20bashrc.md)
    
5. Essential communications is done through Nodes, publishers, subscribers. See [[ROS2 Communications]]
* * *

### Oop tips

its better to use oop in making a node

- make a node class
- put some code in the **init** function in the class
- Init function will run when a class object is created but wont take callbacks
- callbacks will be allowed if the next line is rclpy.spin(node)
- same for c++
- [OOP template](OOP%20template.md)

* * *

### ROS libraries

RCL- ROS client library in C : to use it use rclcpp and rclpy, rcl...  
DDS- data distribution service
Check out [[ROS library]]

***



- [ ] #TODO Make ros arguments note.
***
### RQT 

GUI tool to visualize nodes and topic communications. [RQT](RQT.md) For more info