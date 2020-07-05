**IMPORTANT: This page is being updated and the content might not be 100% correct.**

# Description

BerryNet LINE client helps send the texts and images of the inference results to your mobile LINE app. So you can receive instant notifications no matter where you are with Internet connection.

<img src="https://user-images.githubusercontent.com/292790/46901080-83427680-cedf-11e8-803a-4b9ed8a23e42.png" alt="LINE agent example" width=30%>

# Steps to setup LINE mobile app

1. Create a LINE channel
    * Follow the [official document](https://developers.line.me/en/docs/messaging-api/getting-started/).
    * Choose **Messaging API** channel.
1. Add the channel as your LINE friend
    * Scan the channel QR code by your LINE mobile app.
1. Get 3 channel settings: **user ID**, **channel secret**, and **channel access token**
    * In Channel settings, go to the Message settings section, and generate a Channel access token by clicking the issue button.
    * BerryNet LINE client needs the settings to send results to this LINE channel.

# Steps to use BerryNet LINE client

1. Add the 3 channel settings into BerryNet configuration file (`/usr/local/berrynet/config.js`)

    ```
    config.LINETargetUserID = 'your-user-id';
    config.LINEChannelSecret = 'your-channel-secret';
    config.LINEChannelAccessToken = 'your-channel-access-token';
    ```

1. Run BerryNet LINE client

    ```
    $ nodejs /usr/local/berrynet/line.js
    ```

1. Now, you can receive BerryNet inference results from your LINE mobile app.
