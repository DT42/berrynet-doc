**IMPORTANT: This page is being updated and the content might not be 100% correct.**

# Engine: Movidius

[Movidius neural compute stick](https://software.intel.com/en-us/neural-compute-stick) (NCS) is an USB device containing Myriad 2, the DLA (Deep Learning Accelerator) chip.

![](https://user-images.githubusercontent.com/292790/45946533-bce03a00-c023-11e8-8745-40b787dddd8d.jpg)

| Feature               | Description                                  |
|-----------------------|----------------------------------------------|
| Inference Performance | FPS 7.5 for object detection (MobileNet SSD) |
| Hardware Performance  | 80~150 GFLOPS [[1]](https://www.tomshardware.com/news/movidius-fathom-neural-compute-stick,31694.html) |
| Power Consumption     | 1W power envelope [[2]](https://www.anandtech.com/show/11649/intel-launches-movidius-neural-compute-stick) |

BerryNet Movidius Engine helps user to create edge AIoT applications in minutes, and is powered by [OpenVINO](https://software.intel.com/en-us/openvino-toolkit).

| RPi3 w/ 2-NCS | UP Squared (w/ Myriad 2) |
|---|---|
|[![](http://img.youtube.com/vi/xvOh-1kZ6yU/0.jpg)](http://www.youtube.com/watch?v=xvOh-1kZ6yU "Object detection: RPi3 w/ 2-NCS")|[![](http://img.youtube.com/vi/cLCUdK-at3c/0.jpg)](http://www.youtube.com/watch?v=cLCUdK-at3c "Object detection: UP Squared")|

## Enable Movidius Engine

Here are the steps to enable the support:

1. Install dependencies and inference engine:

        $ bash utils/install-movidius.sh

1. Update BerryNet inference engine settings
    1. Edit `/usr/local/bin/berrynet-manager`
        1. Replace `detection_fast_server.service` by `classify_movidius_server.service`
    1. Edit `/usr/local/berrynet/config.js`
        1. Set `config.inferenceEngine` from `detector` to `classifier`
