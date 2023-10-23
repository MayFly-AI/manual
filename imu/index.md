---
sort: 4
---

# IMU

The sensor is equipped with a [Bosch BMI088 Inertial Measurement Unit](https://www.bosch-sensortec.com/products/motion-sensors/imus/bmi088/). It combines an accelerometer with a gyroscope. This tutorial demonstrates how the IMU data can be streamed to a computer using the sensorleap framework and it shows an application of the IMU data.

![gif not working](https://github.com/MayFly-AI/sensorleap_imu/blob/main/gifs/gl_imu.gif?raw=true)

We have created a [GitHub repository](https://github.com/MayFly-AI/sensorleap_imu) which contains a demo to stream live IMU data from a sensorleap sensor and to use this data to estimate roll, pitch and yaw (assuming constant position). The demo uses a kalman filter to fuse data from the gyroscope with the data from the accelerometer.

To stream data from the IMU, do
```python
from mayfly.sensorcapture import SensorCapture

cap = SensorCapture(list(range(64)),'')
while True:
    capture = cap.read()
    if capture['type'] != 'imu':
        continue
    tstamps = capture['values']['t']
    acc = capture['values']['acc']
    rads = capture['values']['rads']
    N = len(tstamps)
```
Depending on the clock of the sensorleap stream (e.g. 30Hz) and the configured frequency of the IMU (e.g. 100Hz),
the arrays tstamps, acc and rads contains 1 or more sensor readings (N). tstamps contains N timestamps from the IMU in
microseconds since epoch. acc contains N accelerometer readings in the format [ax1,ay1,az1,ax2,ay2,ay2,...] and similarly
for the gyroscope (rads): [gx1,gy1,gz1,gx2,gy2,gy2,...]. The accelerometer when the sensorleap sensor is
level will output values as (0,-g,0) with the y axis down.

It is important to calibrate the IMU before using it for applications. To do this, clone the [GitHub repository](https://github.com/MayFly-AI/sensorleap_imu), put the sensorleap camera on a level surface (or mount on robot and put robot on level
surface) and run:
```bash
python calibrate_imu.py
```
This will dump a file (imu_means.txt) with mean values for the 6 DoF for the BMI088 IMU.

To stream and visualize the IMU data, run
```bash
python show_graph.py
```
You should see a window appear similar to this:
![gif not working](https://github.com/MayFly-AI/sensorleap_imu/blob/main/gifs/show_graph.gif?raw=true)

For your own window, notice that the calibration is off. Accelerometer is not at (0,-1g,0) and gyroscope is drifting a lot.
To take the IMU calibration into account when visualizing the streamed data, run:

```bash
python show_graph.py --means imu_means.txt
```

To record IMU data to text file, run:
```bash
python show_graph.py --record
```
This will create a file: record_imu.txt.

To use the recorded data instead of live streamed data, do:
```bash
python show_graph.py --means imu_means.txt --recording record_imu.txt
```

To see the IMU data visualized with OpenGL, run:
```bash
python gl_imu.py --means imu_means.txt
```
and with recorded data:

```bash
python gl_imu.py --means imu_means.txt --recording record_imu.txt
```




{% include list.liquid all=true %}



