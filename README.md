multicamera_acquisition
==============================

Python library for parallel video acquisition. It abstracts Basler (pypylon) and flir (pyspin) libraries to allow simultaneous recording from both.

Acquisition is done in parallel using a microprocessor (we use an arduino) which triggers frame capture. Threads exist for each camera capturing these frames and writing to a video.

In addition, we record input GPIOs on the arduino to sync external data sources to the video frames. 

Authors
- Tim Sainburg and Caleb Weinreb

Sources:
    - [simple_pyspin](https://github.com/klecknerlab/simple_pyspin/) is the basis for the camera object. 
    - [Jarvis Motion Capture](https://github.com/JARVIS-MoCap) is mocap software for flir cameras. We used their synchronization as motivation for this library. 


### Basic usage 
```{python}
from multicamera_acquisition.acquisition import acquire_video

camera_list = [
    {'name': 'top', 'serial': 24535665, 'brand':'basler', 'gain': 12, 'display': False},
    {'name': 'side1', 'serial': 24548223, 'brand':'basler', 'gain': 12, 'display': False},
    {'name': 'side2', 'serial': 22181547, 'brand':'flir', 'gain': 12, 'display': False},
    {'name': 'side3', 'serial': 22181612, 'brand':'flir', 'gain': 12, 'display': False},
]

acquire_video(
    'your/save/location/',
    camera_list,
    framerate = 30,
    exposure_time = 2000,
    recording_duration_s = 10,
    append_datetime=True,
)
```

Project Organization
------------

    ├── LICENSE
    ├── README.md          <- The top-level README for developers using this project.
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── multicamera_acquisition                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    ...

--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
