# System Architecture

The core concept of BerryNet is to create an AIoT (AI + IoT) network:

* An IoT network that devices can communicate with each other.
* Some of the devices are more powerful and can execute edge AI computation.

![bn-slide-aiot-network](https://user-images.githubusercontent.com/292790/99162257-ab43da00-2736-11eb-8f62-a2e20db656d3.png)

Based on the concept, user can create an AI application by constructing a data network/pipeline.

![bn-slide-core-concept](https://user-images.githubusercontent.com/292790/99162253-a54df900-2736-11eb-8dee-43ef4261dfc4.png)

![bn-slide-basic-topoloty](https://user-images.githubusercontent.com/292790/99162254-a848e980-2736-11eb-910e-9240d6711a07.png)

## Communication

BerryNet uses [MQTT](https://mqtt.org/) as the default IoT communication mechanism because MQTT is a de-factor IoT industry protocol.

MQTT topic format is based on the concept:

    berrynet/<component-type>/<component-name>/<message-type>[/message-additional-info...]

MQTT topics using in BerryNet

|MQTT Topic|Description|
|--|--|
|berrynet/engine/darknet/result|Inference result from the Darknet engine|
|berrynet/engine/tfliteclassifier/result|Inference result from the TFLite classification engine|
|berrynet/engine/tflitedetector/result|Inference result from the TFLite detection engine|
|berrynet/engine/ovclassifier/result|Inference result from the OpenVINO classification engine|
|berrynet/engine/ovdetector/result|Inference result from the OpenVINO detection engine|
|berrynet/engine/pipeline/result|Inference result from the Dyda pipeline engine|
|berrynet/engine/tensorflow/result|Inference result from the TensorFlow engine|
|berrynet/data/rgbimage|Input image from the camera client|
|berrynet/dashboard/snapshot|Relay input image to Freeboard snapshot widget|
|berrynet/dashboard/inferenceResult|Relay inference text result to Freeboard inferneceResult widget|

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
