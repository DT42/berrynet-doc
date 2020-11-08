# Gmail Client

Gmail client can send the targeting inference result to your Gmail.

## Pre-Condition

There are two configuration requirements for your Gmail account:

1. 2-Step Verification is `Off`.
1. Less secure app access is `On`.

You can check these two configurations from [here](https://myaccount.google.com/security).

## Usage

For example, Alice has a people detection system made by BerryNet, and wants to use her Gmail to send a notification to Bob if there is any person is detected by the system. 

Alice sets a target label `person`:

    $ python3 gmail.py \
          --sender-address alice@gmail.com \
          --sender-password <sender-address-password> \
          --receiver-address bob@dt42.io \
          --target-label person
