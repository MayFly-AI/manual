---
sort: 1
---

# DROID-SLAM

[DROID-SLAM](https://github.com/princeton-vl/DROID-SLAM) is a state-of-the-art neural network based visual SLAM for monocular, stereo and RGB-D cameras. It requires substantial GPU compute to run real-time. We are using an RTX3090 for this tutorial. The DROID-SLAM initial code release requires some alterations to be used as a complete SLAM solution. The initial code release is written for single GPU where 2 stages are carried out in sequence: first tracking
and local bundle adjustment, then global bundle adjustment and loop closure. To run it real-time 2x RTX3090 GPUs are required, where the two stages
are run simultaneously on each GPU. See the [paper](https://arxiv.org/abs/2108.10869) for details. For this tutorial we have not yet made the required
alterations to run on 2 GPUs simultaneously, meaning only the tracking and local bundle adjustment is run in real-time, followed by a second stage
afterwards with global bundle adjustment and loop closure.

{% include youtube.html id="Dxfzh6TdJvw" %}

<br/><br/>


We forked the DROID-SLAM GitHub repo to fix some problems we had with visualization. DROID-SLAM uses Open3D for visualization and every time new
data was added or removed for rendering, the viewer reset the camera view making it impossible to inspect the SLAM process while it was ongoing.
We fixed this in our fork. Start by:
```bash
git clone --recursive https://github.com/MayFly-AI/DROID-SLAM.git
```

Now you can choose to use anaconda by following the install instructions in the [README.md](https://github.com/MayFly-AI/DROID-SLAM) (Getting Started section) but it is not necessary. We had problems with resolving the conda environment so we proceeded without anaconda:

```bash
pip install evo --upgrade --no-binary evo
pip install gdown
```

and then:

```bash
python setup.py install
```

To run DROID-SLAM with a MayFly AI sensor, first you need to calibrate the camera and put the intrinsic camera model into a txt file with the following
content:
```bash
fx fy cx cy [k1 k2 p1 p2 [ k3 [ k4 k5 k6 ]]]
```

See our calibration file: ./calib/sensorleap.txt. Follow this [guide](/sensorleap_manual/setup/calib_cam) for camera calibration.

To run DROID-SLAM live on stream from MayFly AI sensor, run:

```bash
python sensorleap.py --calib=calib/sensorleap.txt --stride=1
```

Note that sensorleap.py only runs the frontend part with tracking and local bundle adjustment. To do global bundle adjustment on a recording, use demo.py.

{% include list.liquid all=true %}
