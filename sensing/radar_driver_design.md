

## Radar driver

### Output

![draw.io figure](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/main/sensing/figure/radar_driver.drawio.svg)

As discussed in [ros-perception PR #1](https://github.com/ros-perception/radar_msgs/pull/1) and [survey](https://github.com/radarAaron/radar_msgs/blob/master/ROS%20Message%20format%20comparison.xlsx), there are many kinds of outputs from radar devices.
Pointcloud, tracked objects, and cost map for occupancy grid are considered as common outputs from radar devices.

For now, we suggest that Autoware radar drivers should support `ros-perception/radar_msgs/msg/RadarScan.msg` and `autoware_auto_perception_msgs/msg/TrackedObjects`, because these two outputs are more useful for sensor fusion in the sensing and perception module than others.
In addition, we suggest that `CostMap` should be supported in the future.

### Interface

The radar driver converts the communication data from radars to ROS2 topics.

The following communication types are considered:

- CAN
- CAN-FD
- Ethernet

![draw.io figure](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/main/sensing/figure/radar_communication.drawio.svg)

ROS driver receive the data from radar devices.

- Scan (pointcloud)
- Tracked objects
- Diagnostics results

The ROS drivers receives the following data from the radar device:

- Time synchronization
- Ego vehicle status, which often need for tracked objects calculation
