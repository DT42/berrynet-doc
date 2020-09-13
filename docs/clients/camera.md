BerryNet camera client (`bn_camera`) supports three types of input sources

* Physically connected camera, e.g. USB camera and Pi camera.
* Internet camera (IP camera) providing RTSP or MJPEG video stream.
* Single image for development or debugging.

We will introduce how to use these different types of input sources below.

# USB Camera

By default, camera client will use physically connected camera as input source:

```
$ bn_camera
```

You can use `FPS` parameter to control its image decoding rate:

```
$ bn_camera --fps 5
```

# RPi Camera

The usage of RPi camera is the same as USB camera above.

[How to verify PiCamera HW](https://projects.raspberrypi.org/en/projects/getting-started-with-picamera/5)

# IP Camera

Before setting RTSP/MJPEG video stream as input source, I recommend to verify that the video stream can be played by a media player (e.g. VLC media player or Totem movie player).

* If input is RTSP video stream

        $ bn_camera --stream-src rtsp://<stream-rtsp-url> [--fps N]

* If input is MJPEG video stream

        $ bn_camera --stream-src http://<stream-mjpeg-url> [--fps N]

To get stream URL of an IP camera, please refer to the user manual of your IP camera, or check the [camera connection database](https://www.ispyconnect.com/sources.aspx).

## Get Nest Camera's Snapshot URL

Follow the [quick start guide](https://codelabs.developers.google.com/codelabs/wwn-api-quickstart/#0) to get snapshot URL. The high-level steps are:

1. Create a "product" (the concept is like a project, we will use it for personal usage).
1. Get access token from Nest cloud service.
1. Get snapshot URL with the access token Nest cloud service.

# Single Image (for Development or Debugging)

```
$ bn_camera --mode file --filepath <image-filepath>
```
