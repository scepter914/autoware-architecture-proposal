## Summary

I would like to initiate the discussion for perception architecture with radars for Autoware.
This proposal follows the [Perception architecture discussion](https://github.com/autowarefoundation/autoware/discussions/3).
As described in the radar sensing proposal, radar output can be divided into two types; scan and objects.
According to these output types, I suggest two sensor fusion types for radar output:

- Radar fusion in the object layer in the tracking module
- Radar fusion in the `RadarScan` layer in the detection module

### Perception pipeline with radar

![The pipeline figure for design document](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/main/perception/figure/perception_pipeline.drawio.svg)

This figure can be found at <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/perception/figure/perception_pipeline.drawio.svg>

For more detail, please see [radar perception design](https://github.com/scepter914/autoware-radar-architecture-proposal/blob/main/perception/radar_perception_design.md).

## Discussion

- [ ] Radar perception pipeline
- [ ] Document location
  - I see [autoware-documentation](https://github.com/autowarefoundation/autoware-documentation/), but it is not clear where to put the architecture design document.
  - After discussions and if maintainers can instruct where to put the document, I will send a PR for it.
