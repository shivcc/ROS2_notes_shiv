
2024-08-29 04:05
Tags: [[node ros2]], [[Topic]]

## Renaming Nodes ROS2

### Renaming nodes

- we can run nodes with the same name
    
- but we can also rename the nodes at launch
    
```ros2 run my_py_pkg py_demo_node --ros-args --remap __node:=abc```

### Renaming topics

`ros2 run my_py_pkg py_demo_node --ros-args -r old_topic_name:=new_topic_name

### Rename both
`ros2 run my_py_pkg py_demo_node --ros-args -r __node:=node_name -r topic_name:=new_topic_name

- refer to [[Arguments_ROS]]
---
### Tips
- Once a topic is renamed then its considered a different topic, may effect subscribers

## Reference
