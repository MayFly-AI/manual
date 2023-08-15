---
sort: 1
---

# FastSAM

This tutorial shows how to run Fast Segment Anything real-time 15-16fps on a low latency wireless video stream using MayFly wireless camera and a computer with a powerful GPU (we use RTX3090 but smaller should also work).

[Fast Segment Anything](https://github.com/CASIA-IVA-Lab/FastSAM) is a follow up work on [META's Segment Anything](https://github.com/facebookresearch/segment-anything). Segment Anything is able to perform instance segmentation on objects without being trained on that specific object class. Furthermore it enables inputting a descriptive text prompt to identify a desired object segmentation.

META's Segment Anything is too computationally expensive to run real-time. Fast Segment Anything has alleviated this problem by switching out an expensive transformer neural network with a faster CNN (for the segmentation) and combined this with [CLIP](https://github.com/openai/CLIP) (Contrastive Language-Image Pre-Training) by OpenAI for text prompting.

To enable FastSAM real-time with visualization of the result, we had to make a version of the plotter that does not use matplotlib (which is slow). This plotter is included in our fork of FastSAM on github.

{% include youtube.html id="vzdK8RTalmg" %}

 <br/><br/>

**Assumptions:** Complete the guide to stream wirelessly to your desktop or laptop: [Setup guide](/sensorleap_manual/setup)

Launch or make sure sensorleap wireless stream is running. See guide: [Setup guide](/sensorleap_manual/setup). We set the resolution to 720p (1280x720) and 30 FPS. On RTX3090 FastSAM is not able to run 30 FPS (only 15-16 FPS), which means frames are skipped to provide you with the latest frame at all times.

Clone FastSAM code from official repo:

```bash
https://github.com/CASIA-IVA-Lab/FastSAM.git
```

Download our file `Inference_sensorleap.py` into the FastSAM folder:
```bash
cd FastSAM
wget https://raw.githubusercontent.com/MayFly-AI/FastSAM/main/Inference_sensorleap.py -P .
```

Run the demo (it automatically downloads the weights into the ./weights folder):
```bash
python Inference_sensorleap.py --model_path ./weights/FastSAM-x.pt --imgsz 640
```

The above command segments anything in real-time. If you wish to supply a text prompt to segment a specific object of interest, use

```bash
python Inference_sensorleap.py --model_path ./weights/FastSAM-x.pt --imgsz 640 --text_prompt "the white chair"
```

It is also possible to use box prompt which given a bounding box (xywh) outputs the segmentation of the object inside it or to use a point prompt which given a pixel coordinate outputs the segmentation of the object you point at.

**Optional** If you have an iRobot Create3 and wish to drive around while running FastSAM live, follow this guide [Drive iRobot Create3](/sensorleap_manual/create3/teleop)

We forked the official FastSAM repo to have a timestamp of the code with our few additions. The fork is located at

`https://github.com/MayFly-AI/FastSAM`

{% include list.liquid all=true %}
