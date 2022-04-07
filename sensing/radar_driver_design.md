

## Radar driver

### Output

![draw.io figure](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/main/sensing/figure/radar_driver.drawio.svg)

As discussed in [ros-perception PR #1](https://github.com/ros-perception/radar_msgs/pull/1) and [survey](https://github.com/radarAaron/radar_msgs/blob/master/ROS%20Message%20format%20comparison.xlsx), there are many kinds of outputs from radar devices.
Heatmap, pointcloud, tracked objects, and cost map for occupancy grid are considered for an output from radar devices.

For now, I suggest Autoware should support `ros-perception/radar_msgs/msg/RadarScan.msg` and `ros-perception/radar_msgs/msg/RadarTracks.msg` for radar driver because these two outputs are more useful for sensor fusion in sensing and perception module than others.
In addition, I suggest that `CostMap` should support in the future.

### Interface

Radar driver convert the communication data from radars to ROS2 topics.

Communication type are considered as below.

- CAN
- CAN-FD
- Ethernet

![draw.io figure](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/main/sensing/figure/radar_communication.drawio.svg)

ROS driver receive the data from radar devices.

- Scan (pointcloud)
- Tracked objects
- Diagnostics results

ROS driver send the data to need for radar devices.

- Time synchronization
- Ego vehicle status, which often need for tracked objects calculation
