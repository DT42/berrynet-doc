# Default Configuration File

Default configuration is installed in `/etc/supervisor/conf.d/berrynet-tflite.conf`. Configuration describes what are the services consisting of the AI application.

Configuration examples are available in `<berrynet-dir>/config/supervisor/conf.d/`.

## Raspberry Pi Configurations

If you install BerryNet by image, RPi configurations will have been set.

If you install BerryNet from source, please configure RPi by the steps:

1. Open `raspi-config` in terminal

    ```
    rpi $ sudo raspi-config
    ```

1. Enable RPi camera

    ```
    5 Interfacing Options
    `-- P1 Camera
        `-- Yes
    ```

1. Enable GL Driver

    ```
    7 Advanced Options
    `-- A7 GL Driver
        `-- G2 GL (Fake KMS)
    ```

1. (Optional) Enable SSH

    ```
    5 Interfacing Options
    `-- P2 SSH
        `-- Yes
    ```

1. (Optional) Change locale from UK to US

    ```
    4 Localisation Options
    `-- I1 Change Locale
        `-- Cancel en_GB.UTF-8 and select en_US.UTF-8
            `-- Choose en_US.UTF-8 as default locale
    ```

1. (Optional) Change keyboard layout from UK to US

    ```
    4 Localisation Options
    `-- I3 Change Keyboard Layout
        `-- Generic 105-key (Intl) PC
            `-- English (US)
                `-- The default for the keyboard layout
                    `-- No compose key
                        `-- No X server termination hotkey
    ```

## Wi-Fi Configuration

To configure Wi-Fi manually, there are two methods:

1. Use the `raspi-config` command and the GUI interface.
1. Edit `/etc/wpa_supplicant/wpa_supplicant.conf`.

    A working example looks like below:

    ```
    $ cat wpa_supplicant.conf 
    ctrl_interface=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    country=TW

    network={
            ssid="MyAP"
            psk="B3rryN3t"
            key_mgmt=WPA-PSK
    }
    ```
