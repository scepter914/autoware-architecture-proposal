## Summary

I would like to initiate the discussion for perception architecture with radars for Autoware.
This proposal follow [Perception architecture discussion](https://github.com/autowarefoundation/autoware/discussions/3).
As said in radar sensing proposal, radar output divide two types; scan and objects.
According to the output types, I suggest two sensor fusion types as radar output.

- The radar fusion in object layer in tracking module
- The radar fusion in `RadarScan` layer in detection module

### Perception pipeline with radar

![The pipeline figure for design document](https://raw.githubusercontent.com/scepter914/autoware-radar-architecture-proposal/8d5c15628518173570d3dc16fc8347b1c2346747/perception/figure/perception_pipeline.drawio.svg)

This figure put on <https://github.com/scepter914/autoware-radar-architecture-proposal/blob/master/perception/figure/perception_pipeline.drawio.svg>

In detail, please see [radar perception design](https://github.com/scepter914/autoware-radar-architecture-proposal/perception/radar_perception_design.md).

## Discussion

- [ ] Radar perception pipeline
- [ ] Document location
  - I see [autoware-documentation](https://github.com/autowarefoundation/autoware-documentation/), but I do not grasp where to put the architecture design document.
  - After discussions and if maintainers instruct where to put the document, then I'll send PR for it.
