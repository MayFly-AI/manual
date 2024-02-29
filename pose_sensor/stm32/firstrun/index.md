---
sort: 3
---

# First run

To verify that everything is working as expected, connect a tag with USB to your host computer. Then run:

```bash
python examples/python/test.py
```

It will output IMU and magnetometer data in the following python dict format:
```bash
{'type': 'imu', 'time': 431513458999, 'dt': 2048, 'acc': [3.29693341255188, -1.6017781496047974, 8.992942810058594], 'gyr': [0.0010652969358488917, 0.003195890923961997, 0.0010652969358488917], 'mag': [13.116678237915039, 12.640318870544434, 48.51506805419922]}
```
time is a local timestamp from the STM32 in microseconds. dt is delta time from the IMU chip (EXPLAIN THIS BETTER).
IMU and magnetometer measurements are output together. This is because the magnetometer data is read inside the IMU interrupt.

To get ranging measurements (distance between tag and basestation), power on a basestation and run test.py again.
In addition to the IMU and magnetometer data, you will now see the following kind of output:
```bash
{'type': 'uwb', 'time': 432774040034, 'id': 6602363, 'dist': 10.875}
```
The id is a unique ID for the basestation and dist is the measured distance in meters between the tag and the basestation.
If you power on more basestations and run test.py again, these will also appear in the output.

{% include list.liquid all=true %}
