---
sort: 1
---

# YOLOv7

This tutorial shows how to run YOLOv7 real-time 30fps on a low latency wireless video stream using our sensorleap wireless camera and a computer with a RTX3090.

INSERT VIDEO HERE

**Optional:** Steer iRobot Create3 around while running yolov7 live

**Assumptions:** Complete the guide to stream wirelessly to your desktop or laptop: [Setup guide](/sensorleap_manual/setup)

Launch or make sure sensorleap wireless stream is running. See guide: [Setup guide](/sensorleap_manual/setup). We set the resolution to 720p (1280x720). Other resolutions also works for this demo.

Clone yolov7 code from official repo:

```bash
git clone https://github.com/WongKinYiu/yolov7.git
```

Download our file `detect_sensorleap.py` into yolov7 folder:
```bash
cd yolov7
wget https://raw.githubusercontent.com/MayFly-AI/yolov7/main/detect_sensorleap.py -P .
```

Run the demo:
```bash
python detect_sensorleap.py --weights yolov7.pt --conf 0.25 --img-size 640 --view-img
```

**Optional** If you have an iRobot Create3 and wish to drive around while running YOLOv7 live, run in another terminal:
```bash
python send_keys.py
```
NOT DONE

**Additional info**
Sensorleap provides frames in BGR(A) format. If using the nvdecode H264 decoder (default), the frames are delivered in GPU memory. 
The detect.py in YOLOv7 does a bit of preprocessing on the frames which is code that runs on the CPU. Therefore frames are copied from
CUDA to CPU before running the YOLOv7 letterbox function and the typical BGR->RGB and =/255 conversions. A snippet that shows this preprocessing is
shown below:

```python
config = ''
frame_idx = -1
cap = VideoCapture(list(range(64)), config)
while True:
    frames = cap.read()
    frame_idx += 1
    frm = frames[0] # It may have more than 1 frame if sync cameras or ToF. We assume 1 frame
    if use_cuda:
        arr = torch.from_dlpack(frm['image']).cpu().numpy()
    else:
        arr = np.from_dlpack(frm['image']).copy()
    arr = arr[:,:,:3]
    im0s = np.copy(arr)

    # Letterbox
    img = letterbox(arr, 640, stride=32)[0]

    # Convert
    img = img[:, :, ::-1].transpose(2, 0, 1)  # BGR to RGB
    img = np.ascontiguousarray(img)

    img = torch.from_numpy(img).to(device) # copy image to gpu
    img = img.half() if half else img.float()  # uint8 to fp16/32
    img /= 255.0  # 0 - 255 to 0.0 - 1.0
    ...
```


We forked the official yolov7 repo to have a timestamp of the code with our few additions. The fork is located at

`https://github.com/MayFly-AI/yolov7.git`

{% include list.liquid all=true %}
