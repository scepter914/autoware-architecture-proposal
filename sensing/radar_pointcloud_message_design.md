
## Summary

`ros-perception/radar_msgs/msg/RadarScan.msg` aims to standardization in raw data of radar, so I suggest that Autoware adopt `ros-perception/radar_msgs/msg/RadarScan.msg`.

As another idea,

- Make Autoware original message for radar pointclouds
- `sensor_msgs/msg/Pointcloud2.msg`

are considered.
Compared with theses, `ros-perception/radar_msgs/msg/RadarScan.msg` aims to standardization in raw data of radar as discussed in [PR #1](https://github.com/ros-perception/radar_msgs/pull/1).
I think following ROS standard is better architecture for open source softwares.

## survey

Although there are many kinds of outputs, radar mainly adopt two types as outputs, pountcloud and objects.
Related discussion in ros-perception are [PR #1](https://github.com/ros-perception/radar_msgs/pull/1), [PR #2](https://github.com/ros-perception/radar_msgs/pull/2), and [PR #3](https://github.com/ros-perception/radar_msgs/pull/3) and existing open source softwares for radar are summarized in these PR.

### ros-perception/radar_msgs/msg/RadarScan.msg

- <https://github.com/ros-perception/radar_msgs/blob/ros2/msg/RadarScan.msg>

```
std_msgs/Header header
radar_msgs/RadarReturn[] returns
```

- <https://github.com/ros-perception/radar_msgs/blob/ros2/msg/RadarReturn.msg>

```
# All variables below are relative to the radar's frame of reference.
# This message is not meant to be used alone but as part of a stamped or array message.

float32 range                            # Distance (m) from the sensor to the detected return.
float32 azimuth                          # Angle (in radians) in the azimuth plane between the sensor and the detected return.
                                         #    Positive angles are anticlockwise from the sensor and negative angles clockwise from the sensor as per REP-0103.
float32 elevation                        # Angle (in radians) in the elevation plane between the sensor and the detected return.
                                         #    Negative angles are below the sensor. For 2D radar, this will be 0.
float32 doppler_velocity                 # The doppler speeds (m/s) of the return.
float32 amplitude                        # The amplitude of the of the return (dB)
```

### common_interfaces/sensor_msgs/msg/PointCloud2.msg

- <https://github.com/ros2/common_interfaces/blob/master/sensor_msgs/msg/PointCloud2.msg>

```
# Time of sensor data acquisition, and the coordinate frame ID (for 3d points).
std_msgs/Header header

# 2D structure of the point cloud. If the cloud is unordered, height is
# 1 and width is the length of the point cloud.
uint32 height
uint32 width

# Describes the channels and their layout in the binary data blob.
PointField[] fields

bool    is_bigendian # Is this data bigendian?
uint32  point_step   # Length of a point in bytes
uint32  row_step     # Length of a row in bytes
uint8[] data         # Actual point data, size is (row_step*height)

bool is_dense        # True if there are no invalid points
```
