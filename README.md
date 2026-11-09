# scblender

A small Python library that makes Blender scripting feel like plain Python.

Blender's `bpy` API is powerful but verbose: creating an object, renaming it, moving it and keyframing it takes several calls to operators with long names. I built **scblender** while producing animated Physics and Mathematics video lessons, so that each scene could be described in a few readable lines.

> Status: early version (0.0.1), used in my own animation projects.

## What it does

- **Objects as Python classes:** `Sphere`, `Vertice`, `Mesh`, `Camera`, `Path_curve`, `Bezier_curve` and `Timer`, all sharing the same base class (`Particle`) with getters and setters for name, position, rotation, scale and vertices.
- **Animation helpers:** get and set the current frame and insert keyframes for an object or for a single vertex (`scblender.frame`).
- **Scene utilities:** clean the scene and purge orphan data, set the render resolution and timeline, create collections, move objects between them, select, hide, delete and apply transformations (`scblender.setting`).
- **On-screen timer:** a text object that shows the elapsed seconds while the animation plays.

## Example

```python
from scblender import Sphere, Camera
from scblender.setting import clean_scene, set_frame_format
from scblender.frame import set_frame, set_keyframe

clean_scene()
set_frame_format([1920, 1080])

ball = Sphere(name="ball", position=[0, 0, 0])
Camera(name="camera", position=[0, -10, 2], rotation=[1.4, 0, 0])

set_frame(1)
set_keyframe("ball")

set_frame(48)
ball.set_position([4, 0, 2])
set_keyframe("ball")
```

## Installation

scblender runs inside Blender, because it depends on `bpy`, Blender's own Python module.

```bash
pip install git+https://github.com/mlee-code/scblender.git
```

Install it into the Python that Blender uses (or into an environment with the `bpy` package), then run your script from Blender's Scripting tab or with `blender --python your_script.py`.

## Project layout

| Module | Contents |
|---|---|
| `particle.py` | `Particle`, the base class with name, position, rotation, scale and vertices |
| `mesh.py` | `Sphere`, `Vertice`, `Mesh`, `Camera`, `Timer` |
| `curve.py` | `Path_curve`, `Bezier_curve` |
| `frame.py` | Frames and keyframes |
| `setting.py` | Scene, render, selection and collection utilities |

## Author

Allison Bonfim · [LinkedIn](https://www.linkedin.com/in/mlee-contact) · [GitHub](https://github.com/mlee-code)
