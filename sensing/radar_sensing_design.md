
## Pipeline

![Radar sensing pipeline](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/8d5c15628518173570d3dc16fc8347b1c2346747/sensing/figure/radar_sensing.drawio.svg)

This figure put on <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/master/sensing/figure/radar_sensing.drawio.svg>

## Node
### proprocess node

Radar proprocess use `RadarScan` as message type.
As first prototype of radar preprocess, I suggest

- Radar threshold filter
  - This package remove noise (low intensity and edge angle of sensors) from radar points.
- Radar static points filter
  - This package extract static/dynamic radar point using for dynamic object detection.

### RadarScan to Pointcloud2

To use effectively for LiDAR package, I suggest `RadarScanPointcloud2Convertor`, the message converter package from `ros-perception/radar_msgs/msg/RadarReturn.msg` to `sensor_msgs/msg/Pointcloud2.msg`.

|            |           LiDAR package           |                  Radar package                  |
| :--------: | :-------------------------------: | :---------------------------------------------: |
|  message   | `sensor_msgs/msg/Pointcloud2.msg` | `ros-perception/radar_msgs/msg/RadarReturn.msg` |
| coordinate |             (x, y, z)             |                 (r, theta, phi)                 |
|   value    |             intensity             |           amplitude, doppler velocity           |

For considered use case,
- Use [crop box filter](https://github.com/autowarefoundation/autoware.universe/tree/main/sensing/pointcloud_preprocessor) for radar scan
- Apply low level obstacle detection like [ground segmentation](https://github.com/autowarefoundation/autoware.universe/tree/main/perception/ground_segmentation) to radar points for LiDAR-less (cameras + radars) system
