# Launch
In order to launch the nodes, you will have to launch the following commands

```
source ${HOME}/gentoo/opt/ros/kinetic/setup.bash
source ${HOME}/ros_robocup_ws/devel/setup.bash
roslaunch pepper_bringup pepper_full.launch nao_ip:=192.168.43.20 roscore_ip:=192.168.43.20 network_interface:=wlan0
``
