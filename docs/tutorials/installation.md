There are two ways to install BerryNet:

1. Install from pre-built image
1. Install from source

If the reference command listed below starts with

* `host`: it means you should do it on the host machine (a Linux PC is preferred). 
* `rpi`: it means you should do it on Raspberry Pi.

# Install From Pre-Built Image

1. Download the [latest image](https://berrynet.s3.amazonaws.com/images/2019-07-15-raspbian-buster-berrynet.zip). To check the integrity of the downloaded image, you can check the md5sum of the image and compare it with the [checksum file](https://berrynet.s3.amazonaws.com/images/2019-07-15-raspbian-buster-berrynet.md5sum).

    Assuming that the image is saved to `/home/DT42/Downloads/` directory.

    ```
    host $ md5sum /home/DT42/Downloads/2019-07-15-raspbian-buster-berrynet.zip
    8bda8053a69995814a0ca6fa60b1d49e  2019-07-15-raspbian-buster-berrynet.zip
    ```
    
    You can get older releases from [prior release notes](https://github.com/DT42/BerryNet/releases)

1. Write image to SD card

    Assuming that the inserted SD card is represented as `/dev/sdb` on system. (If you see other similar device notes like `/dev/sdb1` or `/dev/sdb2`, you can ignore them without causing any problem.)

    ```
    host $ unzip -p 2019-07-15-raspbian-buster-berrynet.zip | sudo dd of=/dev/sdb bs=4M conv=fsync status=progress
    ```

    Your SD card size has to be >= **8GB**.

1. Boot RPi with the SD card, and login.

    1. Connect keyboard, mouse, and monitor to RPi.
    1. Insert SD card to RPi.
    1. Connect camera to RPi.
    1. Connect power adapter to RPi.
    1. Login, the default user name and password are

        * username: `pi`
        * password: `raspberry`

1. (Optional) Setup Wifi, if you plan to use Wifi to send out inference results or if you plan check the dashboard from another machine instead of connecting the monitor directly to Raspberry Pi.

    Click the network icon at top-right of desktop, and select your country code and Wifi AP.

1. (Optional) Resize filesystem size manually, if your SD card size is > 8GB and want to use its all storage

    Launch `raspi-config`

    ```
    rpi $ sudo raspi-config
    ```

    and choose "Advanced Options" -> "Expend Filesystem".

1. (Optional) Update to the latest BerryNet

    The default BerryNet in the image is verified. If you are interested in the latest features, you can update BerryNet by executing the commands:

    ```
    rpi $ sudo apt update
    rpi $ sudo apt install -y berrynet
    ```

1. Reboot RPi and login again.
1. BerryNet default detection application is running in background after booting.

# Install From Source

Before BerryNet installation, please creating a system SD card by following the [RPi official installation guide](https://www.raspberrypi.org/downloads/raspbian/).

Here are the steps to install BerryNet on RPi:

1. Get BerryNet source codes

    ```
    rpi $ git clone https://github.com/DT42/BerryNet.git
    rpi $ cd BerryNet
    ```

1. Execute installation script

    ```
    rpi $ ./configure
    ```

The installation will take a while.

If the installation is completed successfully, next step is to [configure](../configuration) your BerryNet.

# Meet Troubles

If the installation fails, you can

1. Check is it an [known issue](https://github.com/DT42/BerryNet/issues)
1. [Create an issue report](https://github.com/DT42/BerryNet/issues/new) and attach `<berrynet-dir>/berrynet-install.log`
1. Share the problem with the [community](../../community/qa)

and we will try our best to check it.

# Release History

All the Raspbian images is available on https://downloads.raspberrypi.org/

BerryNet releases base

* v3.7.0: 2019-07-10 buster
* v3.5.1: 2019-04-08 stretch

# In The Future

We are packaging BerryNet and its dependencies to be Debian packages. The long-term goal is to make all the packages followed Debian policy can be available in Debian by default.
