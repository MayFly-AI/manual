---
sort: 1
---


# Programs

The software or applications available with mayfly comes in three parts.

1. The `mayfly` application, which is typically run on the sensor device and possibly as a base-station for relaying sensor data

1. The `mayfly` python package, which provides an API for receiving the streaming data within python.

1. The `viewer` application, which is useful for monitoring streaming meta-data such as latency and data bandwidth.


# Architecture

The flexibility of the programs offers many possible configurations. Bellow is an illustration of two example setups.

<img src="architecture.svg" alt="Architecture examples" />

Arrows show the direction of streaming sensor data, such as video.
