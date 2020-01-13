# Initialisation and wifi connection

To be able to communicate with pepper, you will have to configure a DHCP server

First install the `dhcp` packet

Configure dhcpd by editing the `/etc/dhcpd.conf` file

```
# dhcpd.conf
#
# Sample configuration file for ISC dhcpd
#

option domain-name-servers 9.9.9.9, 9.9.9.10;

subnet 10.142.0.0 netmask 255.255.0.0 {
    option routers 10.142.0.1;
    range 10.142.254.1 10.142.254.254;

    host pepper {
        hardware ethernet 00:1a:a0:2b:da:af;
        fixed-address 10.142.42.48;
    }
}
```

Add the `10.142.0.1` ip to your computer and set the interface up

```bash
sudo ip a add 10.142.0.1/16 dev <INTERFACE>
sudo ip l set <INTERFACE> up
```

Then start the dhcp daemon using :
```bash
sudo systemctl start dhcpd4.service
```

You will then have to enable ip transmission
```bash
# TODO: WRITE
```

# Launch
In order to launch the nodes, you will have to launch the following commands

You should use them in a screen : `screen -S name_of_the_screen`
You can exit the screen using 'Ctrl+a D' and resume it using the `screen -r name_of_the_screen`
```
source ${HOME}/gentoo/opt/ros/kinetic/setup.bash
source ${HOME}/ros_robocup_ws/devel/setup.bash
roslaunch pepper_bringup pepper_full.launch nao_ip:=192.168.43.20 roscore_ip:=192.168.43.20 network_interface:=wlan0
```

In order to launch the navigation stack, use
```
source ${HOME}/gentoo/opt/ros/kinetic/setup.bash
source ${HOME}/ros_robocup_ws/devel/setup.bash
roslaunch navigation_manager navigation_mng_overall.launch
```

Make sure that `NAO_IP` is set to the correct IP.


# Modules

## Map manager

### Launch

additionnal dependencies :
- [rospy_message_converter](https://github.com/uos/rospy_message_converter)

Add points start the map manager tool using the command
```
source ${HOME}/gentoo/opt/ros/kinetic/setup.bash
source ${HOME}/ros_robocup_ws/devel/setup.bash
rosrun map_manager MapTools.py _confPath:="/home/nao/interest_points/"
```

In order to run the map manager, use
```
source ${HOME}/gentoo/opt/ros/kinetic/setup.bash
source ${HOME}/ros_robocup_ws/devel/setup.bash
rosrun map_manager MapManager.py _confPath:="/home/nao/interest_points/"
```

### Add interest points

Add files in `/home/nao/interest_points`, or mark with rviz

example.coord
```

```

### Warnings

- Don't forget to verify hosts and ip
- `ROS_HOSTNAME` should be set to the ip of the host as the `/etc/hosts` can't be modified on the robot
- config path for the map_manager must be set with the final '/'

### Improvement ideas
- use python path library to avoid errors when forget '/' in path

## Navigation manager

### Different strategy types

AbstractNavStrategy
: abstract model to implement strategies

CmdTwist
: ??

GoAndRetryNavStrategy
: ??

GoCleanRetryNavStrategy
: normal navigation

GoCleanRetryReplayLastNavStrategy
: adds an emergency avoidance to `GoCleanRetryNavStrategy` in order to reverse last twist command when the base link is in a critical position

GoCRRCloseToGoal
: ??

SimplyGoNavStrategy
: ??

`GoCleanRetryReplayLastNavStrategy` have been used

### Usage

Usage of the navigation manager

The following messages must be sent on the `/gm_bus_command` topic.

Action will be "go to interest point"
TODO: find how to use and add examples (look in `NavMng.action`)


```
string action
string action_id
string payload
int64 result
```

# Door detection

## Problem with current implementation
- easy possibility of error detection (example : if the final dest of the robot is in front of the door)
    - therefore, the door detection must be improved

# Improvements

- better « door on path » detection
- better documentation for navigation_manager
- remove useless strategies
- remove dead code
