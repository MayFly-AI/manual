---
sort: 1
---

# Setup

NOT DONE

Remember to switch to external antenna in /boot/config.txt by adding:
```bash
dtparam=ant2
```

Recommend dedicated access point. We have good experience with ASUS ZenWiFi Pro ET12. 
On the access point, we disable 2.4GHz and 6Ghz and for the 5Ghz we find an undisturbed channel and set it to 80Mhz bandwith.
On the RPI4, check the established wifi connection with
```bash
iw dev wlan0 info
```
It should list the channel and 80MHz bandwith.

To enable i2c, enable it in /boot/config.txt and add the following line to /etc/modules-load.d/modules.conf
```bash
i2c-dev
```
Then reboot RPI4.

{% include list.liquid all=true %}
