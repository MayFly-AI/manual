---
sort: 1
---


# Configuration of Applications and API

The behavior of the applications **mayfly** and **viewer** as well as the python API for mayfly is controlled using a json configuration file. The executables take the config file as an argument on the command line, while the python API is configured at when starting an instance of the python class **AppSensor**.

In the following we’ll break down the layout and options when configuring an application or API.

Firstly an identifier for the application is given using the “**id**” - mainly for ease of reference.

Then a list of **services** is specified. Any number of services can be run; however, the overall performance will depend on the number of running services.

A number of example configuration files can be found in the code examples. Below is another example. Sending clock and status messages from a server to a client locally.


# Example Config
```
{
    "id":"server_and_client",
    "services":[
        {
            "type":"sensorServer",
            "id":"server_1",
            "errorCorrection":{
                "type":"arq"
            },
            "transfer":{
                "protocol":"udp",
                "bindAddress":{
                    "ip":"0.0.0.0",
                    "port":8999
                }
            },
            "sources":[
                {
                    "id":0,
                    "type":"clock"
                },
                {
                    "id":1,
                    "type":"status",
                    "clockDivider":4
                }
            ]
        },
        {
            "type":"sensorClient",
            "id":"client_1",
            "decoder":{
                "type":"openh264"
            },
            "transfer":{
                "protocol":"udp",
                "bindAddress":{
                    "ip":"0.0.0.0",
                    "port":6000
                },
                "hostAddress":{
                    "ip":"127.0.0.1",
                    "port":8999
                }
            }
        }
    ]
}
```


# Services

Services fall into two categories: “**sensorServer**” and “**sensorClient**”.

A sensor server is typically configured on the sensor device (e.g. a Raspberry Pi with a camera attached to it).

A sensor client is typically configured for the **viewer** or the python scripting API (e.g. on your workstation, for running image processing).

# Sensor Server

In addition to the type **sensorServer** and its identity “**id**” the sensor server specifies:

**errorCorrection** method applied for robust data transfer. The options here are “**fec**” for forward error correction, and “**arq**” for (automatic repeat request).

A “**transfer**” part controls the protocol and addressing of communication for the sensor. See also _Transfer _below.

“**sources**” defines a list of available data inputs to process and and send. Each sensor is represented by a source. A local sensor client can also be added as a source, this is useful for relaying data from one computer to another. There are a number of sources available such as camera, imu, and tof - each name identifies one **type** of sensor.

Each source must have a unique identifier “**id**” which is used throughout the pipeline for data reconstruction, deduplication, and verification.

Some source types support controlling the interval between transmitting sensor data using the “**clock**” setting - e.g. the camera clock set to 30 means it pushes video frames 30 times per second. Only one source can control the clock - other sources must follow that clock - but may skip pushing sensor data via the “**clockDivider**” - e.g. an IMU source could be configured with “**clockDivider**” value of 2 in addition to the aforementioned camera source. This way the camera will provide 30 frames per second while the provides data 15 times per second.

# Sensor Client

The job of the sensor client is to receive, verify, and decode the data coming from a sensor server. The type is “**sensorClient**” and it has an “**id**” which must be used if relaying data to a local sensor server.

“**decoder**” selects the h264 decoding method. If you need video data to be available in graphics memory on a CUDA device it is necessary to choose the type “**nvdecode**” and the **device** must be “**cuda**”. Also available is a purely software based video decoder “**openh264**” and a libavcodec based decoder “**avdecode**” (if available on your system).

# Transfer

The communication between services is provided for by ‘**transfer**’ which specifies the protocol and addresses of the communication endpoints.

The **protocol** controls whether the communication should be done using UDP packets over ipv4: “**udp” **or - alternatively using packet injection with the pcap library: “**pcap”**. Each of these methods needs to specify the address of their local and remote endpoints.

Transfer communication is typically set up for sensor servers, sensor clients, and debugging functionality.

# Debugging

Additional meta information useful for stream latency timing and data bandwidth can be communicated via ‘debugTiming’ and ‘debugTransfer’ when enabled.

# HTTP server

An HTTP server provides a web interface for the sensor when enabled.
