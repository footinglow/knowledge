
```
source /opt/ros/humble/setup.bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
printenv | grep -i ROS
```

```
export ROS_DOMAIN_ID=<your_domain_id>
echo "export ROS_DOMAIN_ID=<your_domain_id>" >> ~/.bashrc
```

```
export ROS_LOCALHOST_ONLY=1
echo "export ROS_LOCALHOST_ONLY=1" >> ~/.bashrc
```


```
ros2 run <package_name> <executable_name>
ros2 run turtlesim turtlesim_node
```

```
ros2 node list
```
```
ros2 topic list
```
```
ros2 service list
```
```
ros2 action list
```

```
rqt
rqt --force-discover
  If you click on Plugins but don’t see Services or any other options,
  you should close rqt and enter the command rqt --force-discover in your terminal.
```
Plugins > Services > Service Caller

```
rqt_graph
```

```
ros2 run turtlesim turtle_teleop_key --ros-args --remap turtle1/cmd_vel:=turtle2/cmd_vel
```

## Topic
```
ros2 topic list
```
```
ros2 topic list -t
  ros2 topic list -t will return the same list of topics, this time with the topic type appended in brackets:
```
```
ros2 topic echo <topic_name>
```
```
ros2 topic info /turtle1/cmd_vel
```
```
ros2 interface show geometry_msgs/msg/Twist
```

```
ros2 topic pub <topic_name> <msg_type> '<args>'
ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
```
```
ros2 topic hz /turtle1/pose

average rate: 59.354
  min: 0.005s max: 0.027s std dev: 0.00284s window: 58
```

## Service
```
ros2 service type <service_name>
ros2 service type /clear
```
```
ros2 service list -t
```
```
ros2 service find <type_name>
```
```
ros2 interface show <type_name>
ros2 interface show std_srvs/srv/Empty
```

```
ros2 service call <service_name> <service_type> <arguments>
ros2 service call /clear std_srvs/srv/Empty
ros2 service call /spawn turtlesim/srv/Spawn "{x: 2, y: 2, theta: 0.2, name: ''}"
```
## Parameter
```
ros2 param list
```
```
ros2 param get <node_name> <parameter_name>
ros2 param get /turtlesim background_g
```
```
ros2 param set <node_name> <parameter_name> <value>
ros2 param set /turtlesim background_r 150
```
```
ros2 param dump <node_name>
ros2 param dump /turtlesim > turtlesim.yaml
```
```
/turtlesim:
  ros__parameters:
    background_b: 255
    background_g: 86
    background_r: 150
    qos_overrides:
      /parameter_events:
        publisher:
          depth: 1000
          durability: volatile
          history: keep_last
          reliability: reliable
    use_sim_time: false
```


```
ros2 param load <node_name> <parameter_file>
ros2 param load /turtlesim turtlesim.yaml
```
```
ros2 run <package_name> <executable_name> --ros-args --params-file <file_name>
ros2 run turtlesim turtlesim_node --ros-args --params-file turtlesim.yaml
```
## Action
```
ros2 action list
ros2 action list -t
```
```
ros2 action info /turtle1/rotate_absolute
```
```
ros2 interface show turtlesim/action/RotateAbsolute
```
```
ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: 1.57}"
```

## rqt_console
```
ros2 run rqt_console rqt_console
```

## launch
```
ros2 launch turtlesim multisim.launch.py
```

- XML
  - Migrating Launch Files
    - https://docs.ros.org/en/humble/How-To-Guides/Migrating-from-ROS1/Migrating-Launch-Files.html
  - ROS 2 Launch XML Format v0.1.0
    - https://design.ros2.org/articles/roslaunch_xml.html

## Recording and playing back data
```
ros2 topic list
```
```
ros2 bag record <topic_name>
ros2 bag record /turtle1/cmd_vel
```
```
ros2 bag record -o subset /turtle1/cmd_vel /turtle1/pose
```
```
ros2 bag info <bag_file_name>
```
```
ros2 bag play subset
```

## Cord Style and Language Version
- ROS2
  - https://docs.ros.org/en/humble/The-ROS2-Project/Contributing/Code-Style-Language-Versions.html
- Google C++ Stype Guide
  - Original 
    - https://google.github.io/styleguide/cppguide.html
  - Japanese
    - https://ttsuki.github.io/styleguide/cppguide.ja.html
