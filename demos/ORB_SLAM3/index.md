---
sort: 1
---

# ORB-SLAM3
[ORB-SLAM3](https://github.com/UZ-SLAMLab/ORB_SLAM3) is a real-time SLAM library able to perform Visual, Visual-Inertial and Multi-Map SLAM with monocular, stereo and RGB-D cameras, using pin-hole and fisheye lens models. ORB-SLAM3 is not based on neural networks and it does not need a GPU.

ORB-SLAM3 is a C++ code. To use it easily in combination with other python based AI and our SensorLeap Python API, we have made a fork of ORB-SLAM3 with python bindings using pybind11. The python bindings is an add-on to the C++ ORB-SLAM3 code. It does not change any of the 
original ORB-SLAM3 code, it only provides a 1:1 python interface with the same functions used in the C++ examples in ORB-SLAM3. Clone our forked repo here:
```bash
git clone https://github.com/MayFly-AI/ORB_SLAM3_pybind11.git
```

Install Pangolin in a separate place. ORB-SLAM3 cmake will locate it.

We use C++14 compatible compiler (we are using Ubuntu 22.04). To build ORB-SLAM3, do:
```bash
chmod +x build.sh
./build.sh
```

The above step also compiles the pybind11 Python bindings and puts the resulting bindings in a .so file in the ./lib folder.

Now check if you can run one of the examples in the /Examples folder. For example, run the monocular EuRoC example by
first downloading the EuRoC MAV dataset sequence: MH01 in ASL format:
```bash
mkdir euroc
cd euroc
wget http://robotics.ethz.ch/~asl-datasets/ijrr_euroc_mav_dataset/machine_hall/MH_01_easy/MH_01_easy.zip -P .
unzip MH_01_easy.zip 
```

By default, the mono_euroc.cc example does not visualize the SLAM process. To turn on visualization, change the following line of code in ./Examples/Monocular/mono_euroc.cc
```c++
ORB_SLAM3::System SLAM(argv[1],argv[2],ORB_SLAM3::System::MONOCULAR, false);
```
from false to true. Recompile by:
```bash
cd build
make
```

Now run the example (from the root of the repo):
```bash
./Examples/Monocular/mono_euroc ./Vocabulary/ORBvoc.txt ./Examples/Monocular/EuRoC.yaml ./euroc/ ./Examples/Monocular/EuRoC_TimeStamps/MH01.txt 
```
You should see the ORB descriptors overlaid the current image and another window with landmarks and camera poses.

We have ported the Monocular EuRoC example to Python. To run this, do:
```bash
python ./Examples_python/mono_euroc.py ./Vocabulary/ORBvoc.txt ./Examples/Monocular/EuRoC.yaml ./euroc/ ./Examples/Monocular/EuRoC_TimeStamps/MH01.txt 
```

Note: To compile ORB-SLAM3 with a C++14 compatible compiler (we are using Ubuntu 22.04), we ran the following command to edit the CMakeLists.txt file.
The fork already contains this change to the CMakeLists.txt file, so you don't need to do it.
```bash
sed -i 's/++11/++14/g' CMakeLists.txt
```



{% include list.liquid all=true %}
