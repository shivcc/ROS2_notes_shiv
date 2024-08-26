## Setup files Python
setup file is automatically created ie setup.py however you need to add the node in the entry point for the node to be compiled. For python the following is used;

``` 
from setuptools import find_packages, setup

package_name = 'my_py_pkg'

setup(
    name=package_name,
    version='0.0.0',
    packages=find_packages(exclude=['test']),
    data_files=[
        ('share/ament_index/resource_index/packages',
            ['resource/' + package_name]),
        ('share/' + package_name, ['package.xml']),
    ],
    install_requires=['setuptools'],
    zip_safe=True,
    maintainer='shiv',
    maintainer_email='shiv@todo.todo',
    description='TODO: Package description',
    license='TODO: License declaration',
    tests_require=['pytest'],
    entry_points={
        'console_scripts': [
            "py_demo_node = my_py_pkg.test_py:main"
            "NewsStationNode = my_py_pkg.robot_station:main"
        ],
    },
)

```

Where the the format is as follows
`
"node_name = pkg_name.file_name:main_func"
`

---
In the setup.cfg you must indicate the path to the pakage;
```
[develop]
script_dir=$base/lib/my_py_pkg
[install]
install_scripts=$base/lib/my_py_pkg

```

---
You must define the dependencies usually rclcpp in the pakage.xml file
```
<?xml version="1.0"?>
<?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
<package format="3">
  <name>my_py_pkg</name>
  <version>0.0.0</version>
  <description>TODO: Package description</description>
  <maintainer email="shiv@todo.todo">shiv</maintainer>
  <license>TODO: License declaration</license>

  <depend>rclpy</depend>

  <test_depend>ament_copyright</test_depend>
  <test_depend>ament_flake8</test_depend>
  <test_depend>ament_pep257</test_depend>
  <test_depend>python3-pytest</test_depend>

  <export>
    <build_type>ament_python</build_type>
  </export>
</package>

```

## Setup files C++
- [ ] @TODO Make C++ setup notes