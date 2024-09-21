
2024-08-29 03:26
Tags: [[node ros2]], [[ROS2 Communications]]

## Publisher

- Puts/updates a topic
- on init function:
- self.publisher_ = self.create_publisher(String,"Robot_news",10)
- where publisher(message_type, topic_name, q_size)
- q_size qos -quality of settings remain default 10

### [[Publisher Templates]]


## Reference
[more info QOS](https://docs.ros.org/en/rolling/Concepts/Intermediate/About-Quality-of-Service-Settings.html)