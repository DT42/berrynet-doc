# Goal

This tutorial will share how to create a simple surveillance system in your home.

# Hardwares

In this tutorial, we will use these HWs:

* Raspberry Pi 3 or 4
* RPi camera v2

# Setup

After followed the steps in [Installation](../installation), your RPi should be ready to run BerryNet.

# Run BerryNet as Surveillance Application

## Launch BerryNet

BerryNet starts an example detection application by default:

![](https://user-images.githubusercontent.com/292790/61530337-56b32080-aa56-11e9-82f6-eccd0202f630.png)

All the services' status should be "RUNNING".

## Launch Dashboard Client

We will see the detection result on Freeboard by following [the steps](../../#dashboard-freeboard) in README.

## Launch Camera Client

Camera client is started automatically after booted, so RPi camera or USB camera will keep capturing frame in FPS 6 in background.

The dashboard will keep updating the inference image and text results on it:

![](https://user-images.githubusercontent.com/292790/58022834-e87adc00-7b40-11e9-97ce-be1606f91480.png)

## For Raspberry Pi 3

Please change the camera client's FPS from 6 to 2 in the [default configuration](../configuration), and reboot the system.

## Next

To stop the system, you can execute

```
$ sudo supervisorcal stop all
```

If you want to

* Do some data analysis, you can also enable [[Data Collector]] to collect the inference results.
* Know more about Freeboard, please refer to the [open dashboard on your computer](../../clients/dashboard#open-dashboard-on-your-computer) section in the [[Dashboard]] document.
* Send testing images manually instead of using camera stream, please refer to the [Camera Client Configuration](../../#camera-client) in README.
* Know more about camera client, please refer to the [[Cameras]] document for more details.

Hoping that this starting point can help you create your own interesting project!
