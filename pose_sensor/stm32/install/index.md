---
sort: 1
---

# Installation

All source code is open-source. The code is located in 2 GitHub repositories. One repository for the STM32 code and one
repository for the host code and applications

- [STM32 code repository](https://github.com/MayFly-AI/stm32-sensorleap)
- [Host and applications code repository](https://github.com/MayFly-AI/mayfly)

The devices are shipped already flashed and ready with the STM32 code. If you need to update or change the STM32 code, have a look at the [STM32 installation](/manual/pose_sensor/stm32/stm32_install)

For the host and applications code, start by cloning the repository:
```bash
git clone https://github.com/MayFly-AI/mayfly.git
```

Then install with:
```bash
pip install .
```

### Linux
The code needs access to `/dev/ttyACM0`, which is owned by root with read/write permissions for the group dialout. To run without sudo, add your user to the dialout group:

```bash
sudo usermod -a -G dialout <user>
```
Log out and back in for this to take effect. It is not enough to open a new terminal window.

### Mac
on macOS the the code needs access to `/dev/cu.usbmodem-*` which this should just work with no change of permissions.


### Windows
For windows, Visual Studio Code can be used..... FINISH THIS


{% include list.liquid all=true %}
