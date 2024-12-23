## Summary

The pipeline of perception module in Autoware has become filled with many additional functions through repeated development.
It lead to be hard to tune many parameters and debug especially for rule based complicated pipeline.

This proposal aims to simplify the perceptionp ipeline and solve hardness of tuning and debug.

## Whole pipeline for object recognition

![](fig/new_autoware_design.drawio.svg)

## Component
### Priority object merger

Priority object merger has new features different from existing [object_merger](https://github.com/autowarefoundation/autoware.universe/tree/main/perception/autoware_object_merger).

- Multiple input

Priority object merger can use for multiple input.
It prevents from multiple `object_merger`, which makes the pipeline too complicated to debug.

- Merge with priority

Existing `object_merger` use approximate sync by message filter, which makes time delay.
If the amount of input is increasing, the time delay is more and more, and availability of autonomous driving disappears.
In addition to it, if some detection fail, `object_merger` fail to merge by the message filter and cannot publish the objects.
Even if main detection like ML-based detection (like CenterPoint) can succeed to detect, the result of merge fail.
It decrease availability of autonomous driving a lot.

So priority object merger dismiss the message filter and use priority for main detection.
When subscribing from the output of main detection, priority object merger gather the all outputs from detection.
If some detection other than main detection fail, priority object merger can merge from other detection results and publish the result.
It can increase availability of autonomous driving.

### Base 3D detection

For now, Autoware use mainly ML-based method for 3D detection and We name this as base 3D detection.
We can choose from

- [CenterPoint](https://github.com/autowarefoundation/autoware.universe/tree/main/perception/autoware_lidar_centerpoint)
- [TransFusion-L](https://github.com/autowarefoundation/autoware.universe/tree/main/perception/autoware_lidar_transfusion)
- BEVFusion-L (TBD)

The detection range of base 3D detection depends on the cases, but it is often 90m-120m.

If you want to use with Camera-LiDAR fusion, you can use fusion model like BEVFusion-CL (BEVFusion Camera-LiDAR-fusion model).
However, base 3D detection need stable detection because it is more important component for new architecture than before.
Therefore if sensor data often drop, we don't recommend to use Camera-LiDAR fusion methods.

### Near object 3D detection

To enhance detection for near object especially for pedestrian and cyclist, we add near object 3D detection.
It can be used as supplemental detection with base 3D detection.
We can use ML-based method for near object 3D detection, especially CenterPoint, which is strong to detect for small objects.
We use high resolution of the voxel of ML model to detect to be better detection for small objects.
The detection range of base 3D detection depends on the cases, but it is often 30m-50m.

### Camera-only 3D detection

To enhance detection for the objects that LiDAR-only detection is not good to detect, we add camera-only 3D detection.

### Radar-only faraway object 3D detection

To enhance faraway detection, we use radar-only 3D detection.
Please see [the document of faraway radar object detection](https://github.com/autowarefoundation/autoware-documentation/blob/main/docs/design/autoware-architecture/perception/reference-implementations/radar-based-3d-detector/faraway-object-detection.md).

### Cluster based Camera-LiDAR fusion 3D detection

To enhance detection for the objects that LiDAR-only detection is not good to detect, we can use cluster based Camera-LiDAR fusion 3D detection.
The fusion consists of non-ground LiDAR pointcloud filtered by ground segmentation and the result of 2D detection or 2D semantic segmentation.
It can be used as supplemental detection with base 3D detection.
When data of pointcloud and images is increasing the processing time increase and it is better to avoid using this pipeline.

### 3D segmentation

To enhance detection for the objects that is difficult for 3D detection method, especially for vegetation, we can 3D semantic segmentation.
To adapt Autoware interface, we use clustering method for 3D segmentation output.

### Multi object tracking

The inner algorithm is following.

![](fig/multi_object_tracking.drawio.svg)

The base algorithm is [multi_object_tracker](https://github.com/autowarefoundation/autoware.universe/tree/main/perception/autoware_multi_object_tracker).
In addition to this, since the processing time increase when input data is increasing, we reduce to calculation cost by adding stationary detection.

### Motion prediction

The inner algorithm is following.

![](fig/motion_prediction.drawio.svg)

We can choose algorithm from

- [Map based prediction](https://github.com/autowarefoundation/autoware.universe/tree/main/perception/autoware_map_based_prediction)
- MTR (TBD)
- SIMPE (TBD)

Since the processing time increase when input data is increasing, we reduce to calculation cost by adding stationary detection.

## Development item list

- [ ] Make priority object merger
- [ ] Make new model for near object 3D detection
- [ ] Make camera-only 3D detection package
- [ ] Make 3D semantic segmentation package
- [ ] Make clustering for 3D semantic segmentation output
- [ ] Arrange perception launcher for detection
- [ ] Add feature of stationary detection in `multi_object_tracker`
- [ ] Add feature of skipping for stationary object in motion prediction
