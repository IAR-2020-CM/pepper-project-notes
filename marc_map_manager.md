# Launch

additionnal dependencies :
- [rospy_message_converter](https://github.com/uos/rospy_message_converter)

start using the command
```
rosrun map_manager MapTools.py _confPath:="/home/nao/interest_points/"
```

# Add intererest points

Add files in `/home/nao/interest_points`

example.coord
```

```


# Warnings

- Don't forget to verify hosts and ip
- `ROS_HOSTNAME` should be set to the ip of the host as the `/etc/hosts` can't be modified on the robot
- config path for the map_manager must be set with the final '/'

# Improvement ideas
- use python path library to avoid errors when forget '/' in path
