# Dashboard Client

Dashboard is the place for displaying BerryNet's inference image and text results.

BerryNet provides two dashboard clients: [FBDashboard](#fbdashboard) and [Freeboard](#freeboard).

## FBDashboard

FBDashboard (framebuffer dashboard) is easy-to-use by only one command:

```
$ bn_dashboard --no-full-screen --no-decoration --topic berrynet/engine/tflitedetector/result
```

FBDashboard shows a black screen initially and shows the inference image after received the inference result.

![bn-dashboar-window](https://user-images.githubusercontent.com/292790/98456531-cbfdb400-21b9-11eb-8f00-133aa11f3f9f.png)

In the example above, the inference engine pasted the text results (bounding boxes and labels) on the image. We use the `no-decoration` parameter, and FBDashboard will only display the inference image without pasting the text result again.

This makes debugging easy because FBDashboard can

* listen to an inference engine and display the inference image with or without inference text result flexibly.
* show the inference text result on console by using the `--debug` parameter
* listen to an input client (e.g., camera) and display the input image to see if the input client works as expected.

    ![bn-dashboard-cli-debug](https://user-images.githubusercontent.com/292790/98456704-e173dd80-21bb-11eb-86c0-a0aaa5ab3323.png)

## Freeboard

[Freeboard](https://freeboard.io/) is a browser-based dashboard and displays user-defined widgets (inference image, inference text result, execution logs, etc.)

### Open Freeboard on RPi3 with Touchscreen

Open browser and enter the URL:

    http://localhost/berrynet-dashboard

Your screen will look like

![](https://user-images.githubusercontent.com/292790/58022461-14499200-7b40-11e9-8ec9-a4ce4adb3397.png)

If your BerryNet is running the default detection engine, you can click `LOAD FREEBOARD`

![](https://user-images.githubusercontent.com/292790/58027370-0f3e1000-7b4b-11e9-8a6f-db0bf5a21cad.png)

 and choose the [default configuration](https://raw.githubusercontent.com/DT42/BerryNet/master/config/dashboard-tflitedetector.json) (or at `<berrynet-src>/config/dashboard-tflitedetector.json`). After the configuration is loaded, Freeboard will look like

![](https://user-images.githubusercontent.com/292790/58022824-e31d9180-7b40-11e9-8706-8091d8640920.png)

Now your Freeboard is ready to receive the inference results from BerryNet.

### Open Freeboard on Your Computer

Open browser and enter the URL:

    http://<rpi-ip>/berrynet-dashboard

Your screen will look like

![](https://user-images.githubusercontent.com/292790/58022461-14499200-7b40-11e9-8ec9-a4ce4adb3397.png) 

For the steps to load configuration, please refer to [this section](#open-dashboard-on-your-computer) above.

The only difference is that you need to change the `MQTT SERVER` of data source from `localhost` to RPi's IP (gateway IP). Click `Detection Result`

![](https://user-images.githubusercontent.com/292790/58029129-8a54f580-7b4e-11e9-8567-d23630c3c712.png)

and you can save the new configuration by clicking `SAVE FREEBOARD`.

### Customization

For more details about configuration (e.g. how to add widgets), please refer to [Freeboard project](https://github.com/Freeboard/freeboard).

## Frequent Questions

* Q1: I can not see anything on Freeboard?
    * A: Please follow the steps in [this section](#open-dashboard-on-your-computer).

* Q2: The status of the data sources look good, but I still can not see anything on Freeboard?
    * A: Please [open an issue](https://github.com/DT42/BerryNet/issues/new) and share RPi's system log (`/var/log/syslog`) with us. We will help check the issue.

* Q3: Can BerryNet support any other dashboard?
    * A: Yes, if a dashboard supports MQTT, BerryNet can support it technically. Please [share](../../community/qa) your favorite dashboard with the community, and we can try to integrate it into BerryNet.
