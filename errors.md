# add an interest point

Error when adding a new interest point in rviz

```
[INFO] [1578675378.877812]: in the get interest point service. itP name = 5
[ERROR] [1578675378.879499]: Error processing request: '5'
['Traceback (most recent call last):\n', '  File "/tmp/gentoo/opt/ros/kinetic/lib/python2.7/site-packages/rospy/impl/tcpros_service.py", line 625, in _handle_request\n    response = convert_return_to_response(self.handler(request), self.response_class)\n', '  File "/home/nao/ros_robocup_ws/src/ros_world_mng/map_manager/scripts/MapManager.py", line 74, in getInterestPoint\n    return self._mapIP_Position[str(req.itP_name)] # return of type InterestPoint\n', "KeyError: '5'\n"]
```

Another linked problem is that the list of interest points is not refreshed. The file is created but the `map_manager` have to be launched again.
