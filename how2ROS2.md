# How to do ROS shit because I'm forgetful

## Robot Localization

**START MAP SERVER**  
`ros2 launch robot_localization test_pf.py map_yaml:=/home/bgrant/ros2_ws/src/robot_localization/maps/mac_1st_floor_final.yaml `

**PLAY ROSBAG**
`ros2 bag play macfirst_floor_take_1/`

**RUN PARTICLE FILTER**  
`ros2 launch robot_localization test_pf.py map_yaml:=/home/bgrant/ros2_ws/src/robot_localization/maps/test_map_2.yaml`
'ros2 launch robot_localization launch_map_server.py map_yaml:=gauntlet.yaml'
## Terminal commands

**BUILD**  
```bash
source ~/ros2_ws/install/setup.bash
cd ~/ros2_ws
colcon build --symlink-install
```

**Create Package**  
`ros2 pkg create <pkg_name> --build-type ament_python --node-name <node_name> --dependencies rclpy std_msgs geometry_msgs sensor_msgs`

**Connect to Neato**  
`ros2 launch neato_node2 bringup.py host:=IP_ADDRESS_OF_YOUR_ROBOT`

**Start Simulator**  
`ros2 launch neato2_gazebo neato_gauntlet_world.py`

**Run Teleop**  
`ros2 run teleop_twist_keyboard teleop_twist_keyboard`

**View Neato Camera With rqt**  
`rqt`

**riviz**  
`rviz2`

**Run a Node**  
```bash
ros2 run <pkg_name> <node name>
```

## Simple examples



**Define and Run a Node from Python**  
```python
import rclpy
from rclpy.node import Node

def main(args=None):
    rclpy.init(args=args) # Initialize communication with ROS
    node = SimpleNode()   # Create our Node
    rclpy.spin(node)      # Run the Node until ready to shutdown
    rclpy.shutdown()      # cleanup

if __name__ == '__main__':
main()
```
In order to run the node, we have to add it to our `setup.py` file, which is located in `~/ros2_ws/src/in_class_day02/setup.py`

Once you’ve modified setup.py, you’ll need to do another `colcon build`
```bash
cd ~/ros2_ws
colcon build --symlink-install
```

**Create Publisher Node**  
```python
import rclpy
from rclpy.node import Node

class SimplePub(Node):
    def __init__(self):
        # call super constructor
        super().__init__('node_name')

        # Publisher timer that fires @ 10Hz
        timer_period = 0.1
        self.timer = self.create_timer(timer_period, self.publish_msg)

        # publisher
        self.publisher = self.create_publisher(MsgType, 'publisher_name', 10) # 10 = queue size

    def publish_msg(self):
        # create message to publish
        my_msg = MsgType()

        # publish message
        self.publisher.publish(my_msg)
```

**Create Subscriber Node**  
```python
class SimpleSub(Node):
    def __init__(self):
        # call super constructor
        super().__init__('node_name')

        # subscriber
        self.subscriber = self.create_subscription(MsgType, 'publisher_name', self.process_msg, 10) # 10 = queue size

    def process_msg(self, msg):
        print(msg.header)
```

**Create ROS message**  
```python
from geometry_msgs.msg import PointStamped
from std_msgs.msg import Header
from geometry_msgs.msg import Point

my_header = Header(stamp=self.get_clock().now().to_msg(), frame_id="odom")
my_point = Point(x=1.0, y=2.0, z=0.0)

my_point_stamped = PointStamped(header=my_header, point=my_point)
```

