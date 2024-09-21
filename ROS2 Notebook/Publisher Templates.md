
2024-08-29 03:31
Tags: [[Publisher]]

This template is for a simple ROS2 publisher that prints hello in intervals
## Publisher Templates

For python
```
#!/usr/bin/env python3

import rclpy

from rclpy.node import Node

from example_interfaces.msg import String

class NewsStationNode(Node):

def __init__(self):

super().__init__("robot_station_publisher")

self.publisher_ = self.create_publisher(String,"robot_news",10)

self.timer_ = self.create_timer(0.5,self.publish_news)

self.get_logger().info("Robot news started to publish")

  

def publish_news(self):

msg = String()

msg.data ="Hello"

self.publisher_.publish(msg)

def main(args=None):

rclpy.init(args=args)

node = NewsStationNode()

rclpy.spin(node)

rclpy.shutdown()

if __name__ == "__main__":

main()
```

 c++ tempelate
```
#include "rclcpp/rclcpp.hpp"

#include "example_interfaces/msg/string.hpp"

class Robot_station_node : public rclcpp::Node

{

public:

Robot_station_node() : Node("Robot_news_station")

{

RCLCPP_INFO(this->get_logger(), "Node has started");

publisher_ = this->create_publisher<example_interfaces::msg::String>("robot_news", 10);

timer_ = this->create_wall_timer(std::chrono::seconds(1), std::bind(&Robot_station_node::timer_callback, this));

}

private:

void timer_callback()

{

auto message = example_interfaces::msg::String();

message.data = "Hello, world! " + std::to_string(count_++);

RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", message.data.c_str());

publisher_->publish(message);

}

rclcpp::TimerBase::SharedPtr timer_;

rclcpp::Publisher<example_interfaces::msg::String>::SharedPtr publisher_;

int count_;

};

int main(int argc, char **argv)

{

rclcpp::init(argc, argv);

auto node = std::make_shared<Robot_station_node>();

rclcpp::spin(node);

rclcpp::shutdown();

return 0;

}
```
## Reference
