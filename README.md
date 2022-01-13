## Notes:

Status quo
- dlc.py schema assumes 1:M video:model mapping.
   - The syntax of DLC permits mutliple videos for a given model, and suggests that this is optimal for 3D.
   - DLC does not offer out-of-the-box examples for these cases. I'm actively seeking models try ingesting.
   - Likely solution: make second schema
- dlc.py schema asks user to supply framerate when manually entering recording information.
   - This could be imported via DLC files, but it's more conceptually related to the recording.
   - Framerate isn't used for any current calculations, so it could be dropped as a foreign key.
   - Future work with NWB export might want fps for timeseries data.
- Precursor project inserted as numpy arrays, and current draft follows that convention.
    - Should future drafts should remove this dependency?
    - Precursor projects provides functions to calculate trajectories with those trajectories
- DLC permits multi-animal models (3 free-moving mice in an arena)
   - Structure of element-session and element-animal assume 1:1 animal:session
   - Would multianimal datasets require putting session upstream of animal?

DLC models can be:
- 2D or 3D
- single- or multi-animal

Current tables support:
- 2D, but not 3D
- Single-animal, not sure about multiple


Precursor projects:
- DLC-2-DJ : https://github.dev/vathes/dj-mathis-sharing
- DLC-2-NWB: https://github.com/DeepLabCut/DLC2NWB
- Treadmill: https://github.com/vathes/project-treadmill/

***

# DataJoint Element - Behavior

This repository features a draft of a DataJoint pipeline design for behavior tracking and pose estimation, including ***DeepLabCut***. This project is a part of our U24 itiative.

The pipeline presented here is not a complete pipeline by itself, but rather a modular design of tables and dependencies specific to the behavior tracking workflow. This modular pipeline element can be flexibly attached downstream to any particular design of experiment session, thus assembling a fully functional
behavior pipeline (see the example [workflow-behavior](https://github.com/datajoint/workflow-behavior)).

## The Pipeline Architecture

![element-behavior diagram](images/MISSING_DIAGRAM.svg)

As the diagram depicts, the array ephys element starts immediately downstream from ***Session***.

### DeepLabCut recordings

+ ***DLCModel*** -
+ ***OtherTable*** -


## Installation

+ Install `element-behavior`
    ```
    pip install element-behavior
    ```

+ Upgrade `element-behavior` previously installed with `pip`
    ```
    pip install --upgrade element-behavior
    ```

+ Install `element-data-loader`

    + `element-data-loader` is a dependency of `element-behavior`, however it is not contained within `requirements.txt`.

    ```
    pip install "element-data-loader @ git+https://github.com/datajoint/element-data-loader"
    ```

## Usage

### Element activation

To activate the `element-behavior`, one needs to provide:

1. Schema names
    + schema name for the dlc module
    + optional: schema name for the treadmill module

2. Upstream tables
    + Session table

3. Utility functions
    + get_beh_root_data_dir()
    + get_session_directory()
    + optional: get_beh_root_output_dir()

For more detail, check the docstring of the `element-behavior`:
```python
help(dlc.activate)
```
### Example usage

See [this project](https://github.com/datajoint/workflow-behavior) for an example usage of this Behavior Element.
