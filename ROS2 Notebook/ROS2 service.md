
2024-09-24 17:48
Tags: [[ROS2 Communications]]

## ROS2 service

- A service is a client/server system. There is *service server* and *service client*
- A service acts as a function/process block. Input->process->output->feedback
- The input and output must have a specific *service type*. The structure of values passed is predefined.
- A service is defined by a name and a service type.
- The service type are interfaces which includes *request and response* variables whose type are defined.
#### Analogy; Weather service

![[ros2-service-analogy.png]]

### Write a service client and server
#### Service server
Example service server for python:
```
#!/usr/bin/env python3

import rclpy

from rclpy.node import Node

from example_interfaces.srv import AddTwoInts

class Add_two_ints_node(Node):

def __init__(self):

super().__init__("add_two_int_node")

self.server_ = self.create_service(AddTwoInts, "add_two_ints", self.add_two_ints_callback_function)

self.get_logger().info("Add two int node have started")

def add_two_ints_callback_function(self, request, response):

response.sum = request.a + request.b

self.get_logger().info(str(request.a)+ " + " + str(request.b)+ " = "+ str(response.sum))

return response

def main(args=None):

rclpy.init(args=args)

node = Add_two_ints_node()

rclpy.spin(node)

rclpy.shutdown()

if __name__ == "__main__":

main()
```
#### Call service without client node

Using the ros2 service call feature eg:
`ros2 service call /add_two_ints example_interfaces/srv/AddTwoInts {"a: 4, b: 6"}
`
#### Service client
Example service client for python:

## Reference
