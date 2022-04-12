## Whole Pipeline

The radar sensing package processes `RadarScan` topics.
For `RadarTracks` topics, please see [perception architecture design](https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/perception/radar_perception_design.md).

![Radar sensing pipeline](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/main/sensing/figure/radar_sensing.drawio.svg)

This figure can be found at <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/sensing/figure/radar_sensing.drawio.svg>.

## Node

### preprocess node

The radar preprocess node uses the `ros-perception/radar_msgs/msg/RadarScan.msg`  message type.
As a first prototype of radar preprocess, I suggest

- Radar threshold filter
  - This package removes noise (low intensity and edge angle of sensors) from radar points.
- Radar static points filter
  - This package extracts static/dynamic radar point using for object recognition.

### RadarScan to Pointcloud2

For convenient use of radar pointclouds within existing LiDAR packages, I suggest a `radar_scan_to_pointcloud2_convertor` package for conversion from `ros-perception/radar_msgs/msg/RadarScan.msg` to `sensor_msgs/msg/Pointcloud2.msg`.

|            |           LiDAR package           |                 Radar package                 |
| :--------: | :-------------------------------: | :-------------------------------------------: |
|  message   | `sensor_msgs/msg/Pointcloud2.msg` | `ros-perception/radar_msgs/msg/RadarScan.msg` |
| coordinate |             (x, y, z)             |                (r, theta, phi)                |
|   value    |             intensity             |          amplitude, doppler velocity          |

For considered use cases,

- Use [pointcloud_preprocessor](https://github.com/autowarefoundation/autoware.universe/tree/main/sensing/pointcloud_preprocessor) for radar scan.
- Apply obstacle segmentation like [ground segmentation](https://github.com/autowarefoundation/autoware.universe/tree/main/perception/ground_segmentation) to radar points for LiDAR-less (cameras + radar) systems.
