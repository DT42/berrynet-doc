**NOTE: This page is not completed yet**

# System Architecture

Work in Progress

## Overview

Work in Progress

## Communication

MQTT topic format is based on the concept:

    berrynet/<component-type>/<component-name>/<message-type>[/message-additional-info...]

MQTT topics using in BerryNet

* AI services
  * `berrynet/engine/darknet/result`
  * `berrynet/engine/ovclassifier/result`
  * `berrynet/engine/ovdetector/result`
  * `berrynet/engine/pipeline/result`
  * `berrynet/engine/tensorflow/result`
  * `berrynet/engine/tfliteclassifier/result`
  * `berrynet/engine/tflitedetector/result`
* Clients
  * `berrynet/data/rgbimage`
  * `berrynet/dashboard/snapshot`
  * `berrynet/dashboard/inferenceResult`

## Generic Inference Result Format

Generic inference result format makes AI inference services to follow the same rule.

### Classification

```
{
    "timestamp": STRING,
    "bytes": STRING,
    "annotations": [
        {
           "type": "classification",
           "label": STRING,
           "confidence": FLOAT32
        },
        ...
    ]
}
```

### Detection

```
{
    "timestamp": STRING,
    "bytes": STRING,
    "annotations": [
        {
           "type": "detection",
           "label": STRING,
           "confidence": FLOAT32,
           "top": UINT32,
           "bottom": UINT32,
           "left": UINT32,
           "right", UINT32,
        },
        ...
    ]
}
```

### Field Description

|Field|Description|Type|
|---|---|---|
|timestamp|Datetime string in ISO format.|STRING|
|bytes|Raw image or image with inference results in base64 format.|STRING|
|type|Inference type.<br>Valid values: {classification, detection}|STRING|
|label|Inference result label.|STRING|
|confidence|Inference result confidence.<br>Valid value: 0.00 <= confidence <= 1.00|FLOAT32|
|left|x of the top-left point.|UINT32|
|top|y of the top-left point.|UINT32|
|right|x of the bottom-right point.|UINT32|
|bottom|y of the bottom-right point.|UINT32|
