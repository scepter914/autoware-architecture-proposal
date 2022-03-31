## Summary

I would like to initiate the discussion for sensing architecture with radars for Autoware.
The target of this discussion is message definition and sensing pipeline for radars.
I would like make another discussion for perception architecture with radar.

### Messages

To sum up, I suggest

- [ros-perception/radar_msgs/msg/RadarScan.msg](https://github.com/ros-perception/radar_msgs/blob/ros2/msg/RadarScan.msg) and [ros-perception/radar_msgs/msg/RadarReturn.msg](https://github.com/ros-perception/radar_msgs/blob/ros2/msg/RadarReturn.msg) for radar pointcloud.
- [autoware_auto_perception_msgs/msg/TrackedObjects](https://gitlab.com/autowarefoundation/autoware.auto/autoware_auto_msgs/-/blob/master/autoware_auto_perception_msgs/msg/TrackedObjects.idl) for radar object.

In detail, please see [radar pointcloud message design](https://github.com/scepter914/autoware-radar-architecture-proposal/sensing/radar_pointcloud_message_design.md) and [radar object message design](https://github.com/scepter914/autoware-radar-architecture-proposal/sensing/radar_object_message_design.md).

### Whole pipeline

The proposal pipeline follow [Sensing and perception architecture proposal](https://github.com/autowarefoundation/autoware/discussions/3).

![The pipeline figure for design document](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/8d5c15628518173570d3dc16fc8347b1c2346747/sensing/figure/sensing_pipeline.drawio.svg)

This figures put on <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/master/sensing/figure/sensing_pipeline.drawio.svg>.

### Radar driver

As discussed in [ros-perception PR #1](https://github.com/ros-perception/radar_msgs/pull/1) and [survey](https://github.com/radarAaron/radar_msgs/blob/master/ROS%20Message%20format%20comparison.xlsx), there are many kinds of outputs from radar devices.
Heatmap, pointcloud, tracked objects, cost map for occupancy grid, and vehicle command are considered for an output from radar devices.

For now, I suggest Autoware should support `ros-perception/radar_msgs/msg/RadarScan.msg` and `autoware_auto_perception_msgs/msg/TrackedObjects` for radar driver because these two outputs are more useful for sensor fusion in sensing and perception module than others.

![draw.io figure](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/8d5c15628518173570d3dc16fc8347b1c2346747/sensing/figure/radar_driver.drawio.svg)

This figure put on <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/master/sensing/figure/radar_driver.drawio.svg>.

### Radar sensing pipeline

To sum up, I suggest

- In sensing layer, radar preprocess package filters noise using `RadarScan` message type.
- To use effectively for LiDAR package, I would like to propose convertor from `RadarScan` to `sensor_msgs/msg/Pointcloud2.msg`.

In detail, please see [radar sensing design](https://github.com/scepter914/autoware-radar-architecture-proposal/sensing/radar_sensing_design.md).

![Radar sensing pipeline](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/8d5c15628518173570d3dc16fc8347b1c2346747/sensing/figure/radar_sensing.drawio.svg)

This figure put on <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/master/sensing/figure/radar_sensing.drawio.svg>

## Discussion list

- [ ] Message definition
- [ ] Radar driver design
- [ ] Radar sensing pipeline design
- [ ] Document location
  - I see [autoware-documentation](https://github.com/autowarefoundation/autoware-documentation/), but I do not grasp where to put the architecture design document.
  - After discussions and if maintainers instruct where to put the document, then I'll send PR for it.
