---
sort: 1
---

# Setup

Recommend dedicated access point. We have good experience with ASUS ZenWiFi Pro ET12. 
On the access point, we disable the 2.4GHz and 6Ghz bands and for the 5Ghz band, we set it to 80MHz bandwith and find an undisturbed channel.
On the RPI4, check the established wifi connection with
```bash
iw dev wlan0 info
```
It should list the channel and 80MHz bandwith.


{% include list.liquid all=true %}
