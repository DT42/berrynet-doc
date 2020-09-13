You can receive the notification images (image with classification or detection results) in your Telegram app.

1. Create Your Telegram Bot and Get Its Access Token.

    1. Install a Telegram app on your mobile or desktop.
    1. Search `@botfather` and start a conversation.
    1. Send `/newbot`.
    1. Enter the bot name，the end of the name has to be `bot`. E.g., `bntest1_bot`.
    1. BotFather will sends a message including:

        * Bot link: You can start a conversation with the bot by clicking the link.
        * HTTP API Token (Access Token): Write down the token. It is necessary to run the BerryNet Telegram client.

1. Get The Chat ID (skip the step currently).

    1. Send a message to the bot.
    1. Open the URL `https://api.telegram.org/bot<yourtoken>/getUpdates`.
    1. You will find the chat ID in the returned data.

1. Run BerryNet Telegram Client.

        $ bn_telegram --token <token>

    The token parameter can be a token string or a token filepath:

      * Token string
        * Example: `1234567890:ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghi`
      * The filepath of the configuration file
        * Any filepath is okay and we suggest `$HOME/.config/berrynet/telegram.json`.
        * Configuration file format

                $ cat $HOME/.config/berrynet/telegram.json
                {
                    "token": "<telegram-token>"
                }

    Note: `bn_telegram` is not in the latest system image. You can download the [source code](https://github.com/DT42/BerryNet/blob/master/berrynet/client/telegram_bot.py) and run `python3 telegram_bot.py ...` before we update the system image.

1. Send `/camera` to your bot.

    If you receive the message: 

    `Dear, I am ready to help send notification`

    You will receive notification images in your mobile/desktop Telegram app.
