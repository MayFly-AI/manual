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
Microsoft Visual Studio Community has been proven to build and run the the code including the python API.
It is necessary to have the 'python native development tools' enabled, see also [https://learn.microsoft.com/en-us/visualstudio/python/working-with-c-cpp-python-in-visual-studio].

To install the python package use the menu  `Tools > Python > Python Environments` and optionally create a virtual environment. For the selected environment choose `Open in PowerShell` and simply type:

```
pip install .
```

The mayfly package will now be installed in the selected python environment.


{% include list.liquid all=true %}
