
2024-09-23 19:29
Tags: [[ROS2 Communications]]

## Plus 2 project (ROS2 communication demo)

### Goals
1. Make a node that is a publisher and a subscriber at the same time.
2. Have an operation at each node.
3. Write the code and make brand new package; package name: 2series_py
---
#### The ideal/initial vision
- First a node Publisher will publish a series of numbers +2 series.
- The second node will subscribe the first series and will times 2 and publish.
- The third will subscribe the second series and display it.
---
#### Node and topic names
- 1st node name: series_gen
- 1st topic: series_2
- 2nd node name: modify_series
- 2nd topic: series_4
- 3rd node name: final_series
---
### Steps
1. Making a new package: [[Making new package]], we will use python package.
2. Make the codes.
3. Test the codes.
--- 
### Code
Node 1: series_gen

```
#!/usr/bin/env python3

import rclpy

from rclpy.node import Node

from example_interfaces.msg import String

class series_gen(Node): #

def __init__(self):

super().__init__("series_gen")

self.counter = 0 # initializing counter

self.publisher_ = self.create_publisher(String,"series_2",10)

self.timer_ = self.create_timer(1.0,self.timer_callback)

self.get_logger().info("Series gen have started generating...")

def timer_callback(self):

self.counter += 2

msg = String()

msg.data = str(self.counter)

self.publisher_.publish(msg)

def main(args=None):

rclpy.init(args=args)

node = series_gen()

rclpy.spin(node)

rclpy.shutdown()

if __name__ == "__main__":

main()
```
---
Node 2: Modify series
```
#!/usr/bin/env python3

import rclpy

from rclpy.node import Node

from example_interfaces.msg import String

class modify_series(Node): #

def __init__(self):

super().__init__("modify_series")

self.subscriber_= self.create_subscription(String,"series_2", self.subscriber_callback, 10)

self.publisher_ = self.create_publisher(String,"series_4",10)

self.get_logger().info("Series have started modifying...")

def subscriber_callback(self, msg):

#msg = String()

#self.get_logger().info(msg.data) #for debug

msg_int = int(msg.data)

msg.data = str(msg_int*2)

self.publisher_.publish(msg)

def main(args=None):

rclpy.init(args=args)

node = modify_series()

rclpy.spin(node)

rclpy.shutdown()

if __name__ == "__main__":

main()
```
---
Node 3: final_series
```
#!/usr/bin/env python3

import rclpy

from rclpy.node import Node

from example_interfaces.msg import String

class final_series(Node):

def __init__(self):

super().__init__("final_series")

self.subscriber_= self.create_subscription(String,"series_4", self.callback_subscriber, 10)

self.get_logger().info("Robot receiver is listening...")

  

def callback_subscriber(self, msg):

self.get_logger().info(msg.data)

  
  

def main(args=None):

rclpy.init(args=args)

node = final_series()

rclpy.spin(node)

rclpy.shutdown()

if __name__ == "__main__":

main()
```
---
### RQT graph

![c](https://github.com/shivcc/ROS2_notes_shiv/blob/main/_resources/2_series_rqt.png)

### Lessons learnt

1. You should use the appropriate message type; I used string type and had problems casting to int.

2. Tip: Once you define msg type eg-`msg = String()` then you can not do casting eg:
 - [c]  `int(msg.data)`

3. Topic names must not start with a number.

## Reference
