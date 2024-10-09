
2024-10-05 02:25
Tags: 

## Catch-em-turts

### Points to note

- Use turtlesim
- spawn random turtles in random coordinates.
- Have main turtle automatically travel to the nearest turtle in smooth movement.
- When the main turtle catches, the other turtle disappear; then move on to the next turtle
- 3 nodes:
	- 1. Turtlesim node- for the turtlesim window 
	- 2. Turtle_control- to control the turtle
	- 3. Turtle_spawner- a node to spawn turtles.

### Turtle sim node

Ros2 node info:
```
shiv@ubuntuROS:~$ ros2 node info /turtlesim 
/turtlesim
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/color_sensor: turtlesim/msg/Color
    /turtle1/pose: turtlesim/msg/Pose
  Service Servers:
    /clear: std_srvs/srv/Empty
    /kill: turtlesim/srv/Kill
    /reset: std_srvs/srv/Empty
    /spawn: turtlesim/srv/Spawn
    /turtle1/set_pen: turtlesim/srv/SetPen
    /turtle1/teleport_absolute: turtlesim/srv/TeleportAbsolute
    /turtle1/teleport_relative: turtlesim/srv/TeleportRelative
    /turtlesim/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /turtlesim/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /turtlesim/get_parameters: rcl_interfaces/srv/GetParameters
    /turtlesim/list_parameters: rcl_interfaces/srv/ListParameters
    /turtlesim/set_parameters: rcl_interfaces/srv/SetParameters
    /turtlesim/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Service Clients:

  Action Servers:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
  Action Clients:
```

- How to move the turtle? The subscriber /turtle1/cmd_vel: geometry_msgs/msg/Twist
- lets see the message type twist:
```
shiv@ubuntuROS:~$ ros2 interface show geometry_msgs/msg/Twist
# This expresses velocity in free space broken into its linear and angular parts.

Vector3  linear
	float64 x
	float64 y
	float64 z
Vector3  angular
	float64 x
	float64 y
	float64 z

```
- More info on twist message type: [here](https://medium.com/hackernoon/unicycle-to-differential-drive-courseras-control-of-mobile-robots-with-ros-and-rosbots-part-2-6d27d15f2010) and [here](https://davesroboshack.com/the-robot-operating-system-ros/ros2-topics/)
- The linear velocity is the acceleration (m/s) of the robot towards a direction (this case we will use x only)
- Angular velocity shows how fast to turn (rad/s), we will use the z axis
### Turtle control node

- Subscriber for the pose info; (current pose info)
- publisher for cmd_vel (twist msg)
- For the linear velocity; use the distance between the target and pose (greater the distance faster the speed), multipliers may be needed.
- For the angular velocity use a multiplier of the angle adjacent to distance x and y.
- Considered a P controller  (PID) 
- 100 hz update subscriber and publisher
- 
#### Actual radian degrees vs turtlesim
![](https://github.com/shivcc/ROS2_notes_shiv/blob/main/_resources/Rad_circle.png)
Turtle sim's theta angle is different from the actual representation where the top semicircle is taken as positive (0-pi), then flipped top down (-pi-0); so the order starting from right anticlockwise goes 0 to pi/-pi to 0.

### Turtle spawner/killer node

- This node spawns turtles randomly in an interval. Use service /spawn
- Kill turtle when turtle1 coincides with the another turtle. User service /kill
- Make a targeting system based on the nearest turtle.
- Pass the target info to turtle controll node.

## Final RQT graph

![Pasted image 20241009223330.png](https://github.com/shivcc/ROS2_notes_shiv/blob/main/_resources/rqt_catch_em_turt.png)

### Final behaviour
![Pasted image 20241009223541.png](https://github.com/shivcc/ROS2_notes_shiv/blob/main/_resources/catch_em_turt_demo.png)

## Code

- First launch turtlesim node
- Then turtle spawner node

```
#!/usr/bin/env python3

import rclpy

from rclpy.node import Node

from turtlesim.srv import Spawn

from functools import partial

from my_robot_interfaces.msg import TurtleArray

from my_robot_interfaces.msg import Turtle

import random

class TurtSwnKll(Node):

def __init__(self):

super().__init__("turtle_spwn_rm")

self.turtle_count = 1

self.AliveTurts = []

self.AliveTurtsClass = TurtleArray()

self.spawn_timer = self.create_timer(1, self.spawn_timer_callback)

self.alive_turtle_publisher = self.create_publisher(TurtleArray, "turtles_alive", 10)

self.alive_turtle_subscriber = self.create_subscription(TurtleArray,"turtles_alive", self.update_alive, 10 )

def spawn_timer_callback(self):

self.turtle_count= self.turtle_count + 1

turtle_name = "turtle" + str(self.turtle_count)

x = float(random.randrange(0, 11))

y = float(random.randrange(0, 11))

theta = float(random.randrange(0, 3))

self.call_server_spawn(x=x, y=y, theta=theta)

turt = Turtle()

turt.x = x

turt.y = y

turt.theta = theta

turt.name = turtle_name

self.AliveTurts.append(turt)

self.AliveTurtsClass.turtles = self.AliveTurts

self.alive_turtle_publisher.publish(self.AliveTurtsClass)

def update_alive(self, msg):

self.AliveTurtsClass = msg

self.AliveTurts = self.AliveTurtsClass.turtles

def call_server_spawn(self, x, y, theta):

client = self.create_client(Spawn, "spawn")

#logger while waiting for server

while not client.wait_for_service(1.0):

self.get_logger().warn("Waiting for server spawn server")

#define the variables

request = Spawn.Request()

request.x = x

request.y = y

request.theta = theta

#Call the server and store the result in future variable

future = client.call_async(request)

# We can't spin until future complete coz node already spinning

# make a new callback that runs when future done

future.add_done_callback(partial(self.callback_call_future_found, a=x, b=y))

def callback_call_future_found(self, future, a, b):

try:

response = future.result()

self.get_logger().info("turtle at (" + str(a)+ " , " + str(b)+ ") spawned with name: "+ str(response.name))

except Exception as e:

self.get_logger().error("Service call failed %r" % (e,))

def main(args=None):

rclpy.init(args=args)

node = TurtSwnKll()

rclpy.spin(node)

rclpy.shutdown()

if __name__ == "__main__":

main()
```

- Robot_controller node
```
#!/usr/bin/env python3

import rclpy

import math

  

from rclpy.node import Node

from turtlesim.msg import Pose

from turtlesim.srv import Kill

from geometry_msgs.msg import Twist

from my_robot_interfaces.msg import Turtle, TurtleArray

class TurtleControlNode(Node):

def __init__(self):

super().__init__("turtle_control_node")

self.target = [5,5]

self.current_pose = None

self.AliveTurtsClass = TurtleArray()

self.AliveTurts = []

self.pose_subscriber_ = self.create_subscription(Pose, "turtle1/pose", self.pose_callback, 10)

self.control_publisher_ = self.create_publisher(Twist, "turtle1/cmd_vel", 10)

self.alive_turts_subscriber = self.create_subscription(TurtleArray, "turtles_alive", self.alive_turts_callback, 10)

self.alive_turtle_publisher = self.create_publisher(TurtleArray, "turtles_alive", 10)

self.control_loop_ = self.create_timer(0.01, self.timer_callback)

def pose_callback(self, msg):

#self.get_logger().info("got pose")

self.current_pose = msg

def alive_turts_callback(self, msg):

self.AliveTurtsClass = msg

self.AliveTurts = self.AliveTurtsClass.turtles

#Target gets updated

nearest_turt = self.search_target(self.AliveTurts)

self.target[0] = nearest_turt.x

self.target[1] = nearest_turt.y

#Kill turtle if reached target

self.kill_turtle(nearest_turt, self.AliveTurts)

#self.get_logger().info(str(self.AliveTurtsClass.turtles)) #debug

def kill_turtle(self, turtle, AliveTurts):

if self.current_pose == None:

return

if self.target[0] - 0.5 <= self.current_pose.x <= self.target[0] + 0.5 and self.target[1] - 0.5 <= self.current_pose.y <= self.target[1]+ 0.5:

# Check if the turtle name exists in the AliveTurts list before removing

if turtle in AliveTurts:

AliveTurts.remove(turtle)

self.AliveTurtsClass.turtles = AliveTurts

self.alive_turtle_publisher.publish(self.AliveTurtsClass)

client = self.create_client(Kill, "kill")

request = Kill.Request()

request.name = turtle.name

client.call_async(request)

self.get_logger().info("Killed turtle: " + turtle.name)

return

else:

self.get_logger().warn(f"Turtle {turtle.name} not found in AliveTurts list")

def search_target(self, turtles):

if self.current_pose == None:

return 0, 0

turtle = Turtle()

turtle_dist_list = []

for turtle in turtles:

Dist_x = turtle.x - self.current_pose.x

Dist_y = turtle.y - self.current_pose.y

Dist_to_target = math.sqrt((Dist_x * Dist_x) + (Dist_y * Dist_y))

turtle_dist_list.append(Dist_to_target)

nearest_turt = turtles[turtle_dist_list.index(min(turtle_dist_list))]

return nearest_turt

  

def timer_callback (self):

if self.current_pose == None:

return

Dist_x = self.target[0] - self.current_pose.x

Dist_y = self.target[1] - self.current_pose.y

Dist_to_target = math.sqrt((Dist_x * Dist_x) + (Dist_y * Dist_y))

Angle_diff = math.atan2(Dist_y,Dist_x) - self.current_pose.theta

msg = Twist()

if (Dist_to_target > 0.5):

if Angle_diff > math.pi:

Angle_diff -= 2*math.pi

elif Angle_diff < -math.pi:

Angle_diff += 2*math.pi

msg.linear.x = 3 * Dist_to_target

msg.angular.z = 8 * Angle_diff

else:

msg.linear.x = 0.0

msg.angular.z = 0.0

self.control_publisher_.publish(msg)

def main(args=None):

rclpy.init(args=args)

node = TurtleControlNode()

rclpy.spin(node)

rclpy.shutdown()

if __name__ == "__main__":

main()
```
## Reference

Inspired by Edouard Renard
