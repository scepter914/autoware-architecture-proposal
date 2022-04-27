## Summary

We would like to initiate the discussion for sensing architecture with radars for Autoware.
The target of this discussion is the messaging systems used with radar sensors and sensing pipeline for radars.

We would like to make a separate discussion for the perception architecture including radar.

### Messages

To summarize, We suggest

- [ros-perception/radar_msgs/msg/RadarScan.msg](https://github.com/ros-perception/radar_msgs/blob/ros2/msg/RadarScan.msg) for radar pointcloud.
- [ros-perception/radar_msgs/msg/RadarTracks.msg](https://github.com/ros-perception/radar_msgs/blob/ros2/msg/RadarTracks.msg) for radar object.

For more detail, please see [radar pointcloud message design](https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/sensing/radar_pointcloud_message_design.md) and [radar object message design](https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/perception/radar_object_message_design.md).

### Whole pipeline

The proposed pipeline follows the [Sensing and perception architecture proposal](https://github.com/autowarefoundation/autoware/discussions/3).

![The pipeline figure for design document](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/main/sensing/figure/sensing_pipeline.drawio.svg)

This figure can be found at <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/sensing/figure/sensing_pipeline.drawio.svg>.

### Radar driver

For now, We suggest that Autoware radar drivers should support `ros-perception/radar_msgs/msg/RadarScan.msg` and `autoware_auto_perception_msgs/msg/TrackedObjects.msg`, because these two outputs are more useful for sensor fusion in the sensing and perception module than others.

![draw.io figure](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/main/sensing/figure/radar_driver.drawio.svg)

This can be found at <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/sensing/figure/radar_driver.drawio.svg>.

For more detail, please see [radar driver design](https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/sensing/radar_driver_design.md).

### Radar sensing pipeline

To sum up, We suggest:

- In the sensing layer, the radar preprocess package filters noise through the `ros-perception/radar_msgs/msg/RadarScan.msg` message type.
- For use of radar pointcloud data by LiDAR packages, we would like to propose a converter for creating `sensor_msgs/msg/Pointcloud2.msg`from `ros-perception/radar_msgs/msg/RadarScan.msg`.

For more detail, please see [radar sensing design](https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/sensing/radar_sensing_design.md).

![Radar sensing pipeline](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/main/sensing/figure/radar_sensing.drawio.svg)

This figure can be found at <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/sensing/figure/radar_sensing.drawio.svg>.

## Discussion list

- [ ] Message definition
- [ ] Radar driver design
- [ ] Radar sensing pipeline design
- [ ] Document location
  - We see [autoware-documentation](https://github.com/autowarefoundation/autoware-documentation/), but it is not clear where to put the architecture design document.
  - After discussions and if maintainers can instruct where to put the document, we will send a PR for it.
