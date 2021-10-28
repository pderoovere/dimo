# Dataset of Industrial Metal Objects – utility scripts

## Loader

The [dimo_loader.py](dimo_loader.py) script can be used to load the dimo dataset.

### Dependencies
Make sure `numpy` and `scipy` are installed by running `pip install numpy scipy`.
At the time of development `numpy v1.20.2` and `scipy v1.6.2` are used.

### Usage
The following code can be used to load the dataset.

    from dimo_loader import DimoLoader
    from pathlib import Path
    dimo_loader = DimoLoader()
    dimo_path = Path('...') # Set path to downloaded dataset folder
    dimo_ds = dimo_loader.load(dimo_path)

Then, it is possible to iterate over part models:

    models = dimo_ds['models']
    for model in models:
        model_id = model['id'] # int
        cad = model['cad'] # Path
        # additional entries for size, diameter and symmetries

Or, to iterate over scenes:

    real_jaigo_scenes = dimo_ds['real_jaigo']['scenes']
    for scene in real_jaigo_scenes:
        scene_id = scene['id'] # int
        for image in scene['images']:
            img_id = image['id'] # int
            img_path = cam['path'] # str
            camera = image['camera'] # dict with intrinsics and extrinsics
            scene_info = image['scene_info']
            light_id = scene_info['light_id'] Lightmap id
            carrier_id = scene_info['carrier_id'] Carrier id
            composition_type = scene_info['composition_type'] Composition type
            viewpoint_id = scene_info['viewpoint_id'] Viewpoint id
            for obj in image['objects']:
                obj_id = obj['id'] # int
                model_2world = obj['model_2world'] # Object to world, (4,4)
                model_2cam = obj['model_2cam'] # Object to camera, (4,4)

## Viewer
The [dimo_viewer.ipynb](dimo_viewer.ipynb) notebook can be used to visualize samples.

### Dependencies
In addition to `numpy` and `scipy`, make sure `PIL`, `trimesh`, `pyrender` and `ipywidgets` are installed by running `pip install numpy scipy pillow trimesh pyrender ipywidgets`.
At the time of development, the following versions are used:
* `numpy v1.20.2`
* `scipy v1.6.2`
* `Pillow v8.2.0`
* `trimesh v3.9.34`
* `pyrender v0.1.45`
* `ipywidgets v7.6.5`