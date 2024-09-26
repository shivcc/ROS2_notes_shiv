
2024-09-23 20:10
Tags: [[Ros basics]]

## Making new package

1. Go to your workspace source folder in terminal `cd ros2_ws/src/`
2. You can list packages with`ros2 pkg list`
3. You can filter select packages with `ros2 pkg list | grep filter_word`
### C++ package

- To create a cpp package use the command:
    `ros2 pkg create pkg_name --build-type ament_cmake --dependencies rclcpp`

### Python package

To create a python package use the command:
	`ros2 pkg create pkg_name --build-type ament_python --dependencies rclpy`
	
### Further tips

- Check the dependency in the CMakeLists.txt and package.xml files for cpp
- and setup.py, setup.cfg and package.xml for python
- Refer to [[Setup]] for sample
- write your code under the package name folder.

## Reference
