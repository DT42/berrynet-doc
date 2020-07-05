Dashboard is the place for displaying BerryNet's status, and the default dashboard is [Freeboard](https://freeboard.io/) which is a browser-based dashboard.

# Open Dashboard on RPi3 with Touchscreen

Open browser and enter the URL:

    http://localhost/berrynet-dashboard

Your screen will look like

![](https://user-images.githubusercontent.com/292790/58022461-14499200-7b40-11e9-8ec9-a4ce4adb3397.png)

If your BerryNet is running the default detection engine, you can click `LOAD FREEBOARD`

![](https://user-images.githubusercontent.com/292790/58027370-0f3e1000-7b4b-11e9-8a6f-db0bf5a21cad.png)

 and choose the [default configuration](https://raw.githubusercontent.com/DT42/BerryNet/master/config/dashboard-tflitedetector.json) (or at `<berrynet-src>/config/dashboard-tflitedetector.json`). After the configuration is loaded, Freeboard will look like

![](https://user-images.githubusercontent.com/292790/58022824-e31d9180-7b40-11e9-8706-8091d8640920.png)

Now your dashboard is ready to receive the inference results from BerryNet.

# Open Dashboard on Your Computer

Open browser and enter the URL:

    http://<rpi-ip>/berrynet-dashboard

Your screen will look like

![](https://user-images.githubusercontent.com/292790/58022461-14499200-7b40-11e9-8ec9-a4ce4adb3397.png) 

For the steps to load configuration, please refer to [this section](#open-dashboard-on-your-computer) above.

The only difference is that you need to change the `MQTT SERVER` of data source from `localhost` to RPi's IP (gateway IP). Click `Detection Result`

![](https://user-images.githubusercontent.com/292790/58029129-8a54f580-7b4e-11e9-8567-d23630c3c712.png)

and you can save the new configuration by clicking `SAVE FREEBOARD`.

# Frequent Questions

* Q1: I can not see anything on dashboard?
  * A: Please follow the steps in [this section](#open-dashboard-on-your-computer).

* Q2: The status of the data sources look good, but I still can not see anything on dashboard?
  * A: Please [open an issue](https://github.com/DT42/BerryNet/issues/new) and share RPi's system log (`/var/log/syslog`) with us. We will help check the issue.

* Q3: Can BerryNet support any other dashboard?
  * A: Yes, if a dashboard supports MQTT, BerryNet can support it technically. Please [share](https://github.com/DT42/BerryNet/wiki/Troubleshooting-And-Questions) your favorite dashboard with the community, and we can try to integrate it into BerryNet.

# Customization

For more details about configuration (e.g. how to add widgets), please refer to [Freeboard project](https://github.com/Freeboard/freeboard).
