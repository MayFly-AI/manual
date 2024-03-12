---
sort: 2
---

# STM32 installation

Updating the Pose Sensor firmware is most easily done using STM32 Cube Programmer.


# stm32 cube programmer usage

The utility is available for multiple platform (with registration) at https://www.st.com/en/development-tools/stm32cubeprog.html

After installing the STM32 Cube Programmer, use the following steps to update the Pose Sensor:

1. switch the pose sensor to boot mode using the switch.
1. attach the sensor via to USB to your computer (ensure the cable can transfer data - not just power)
1. The power (green) and boot (red) diodes should light continuously
1. start cube programmer (you might need super-user rights on Linux for configuring USB).
1. Select the "Erasing & Programming" tab.
1. Refresh the USB configuration dropdown and connect (e.g. "Port" dropdown selected "USB1")
1. Locate the .elf or .bin file built using - e.g. using Cube IDE in "File path"
1. Press the "Start Programming"
1. When done switch the pose sensor away from boot mode.
1. detach the pose sensor USB cable
1. re-attach the the pose sensor usage with the newly deployed software


{% include list.liquid all=true %}
