# Installation

1. [Setup BerryNet repository](https://github.com/DT42/BerryNet-repo)
1. Install OpenVINO packages

        # Ubuntu xenial and bionic
        $ sudo apt-get install openvino
    
        # Raspbian
        $ sudo apt-get install openvino-rpi

1. (Optional) Install example classification or detection models for Intel NCS2 (FP16 model)

        # classification
        $ sudo apt-get install mobilenet-1.0-224-fp16-openvino
    
        # detection
        $ sudo apt-get install mobilenet-ssd-openvino

# Setup

1. Initialize OpenVINO execution environment

    Add this line below into shell's config file, e.g. `$HOME/.bashrc`, or run it manually in your console every time:

        $ source /opt/intel/openvino_2019.1.144/bin/setupvars.sh

# Test OpenVINO Engine Manually

Use OpenVINO detector service and mobilenet-ssd-openvino model package as example.

1. Insert NCS2 to your computer.
1. Start detector service

        $ source /opt/intel/openvino_2019.1.144/bin/setupvars.sh 
        $ python3 /usr/lib/python3/dist-packages/berrynet/service/openvino_service.py \
            --service detector \
            --model /usr/share/dlmodels/mobilenet-ssd-openvino-1.0.0/mobilenet-ssd.xml \
            --label /usr/share/dlmodels/mobilenet-ssd-openvino-1.0.0/labels.txt \
            --service_name ovdetector \
            -d MYRIAD \
            --draw \
            --debug
        [D 190617 21:30:13 openvino_service:177] model filepath: /usr/share/dlmodels/mobilenet-ssd-openvino-1.0.0/mobilenet-ssd.xml
        [D 190617 21:30:13 openvino_service:178] label filepath: /usr/share/dlmodels/mobilenet-ssd-openvino-1.0.0/labels.txt
        [D 190617 21:30:13 openvino_engine:167] Loading network files:
                /usr/share/dlmodels/mobilenet-ssd-openvino-1.0.0/mobilenet-ssd.xml
                /usr/share/dlmodels/mobilenet-ssd-openvino-1.0.0/mobilenet-ssd.bin
        [D 190617 21:30:13 openvino_engine:184] Preparing input blobs
        [D 190617 21:30:15 __init__:11] Connected with result code 0
        [D 190617 21:30:15 __init__:13] Subscribe topic berrynet/data/rgbimage

1. Send image to service by camera client

        $ bn_camera --mode file --filepath <image-filepath>

1. You should see the inference results on detector's terminal

        [D 190617 21:31:34 __init__:20] Receive message from topic berrynet/data/rgbimage
        [D 190617 21:31:34 openvino_service:95] payload size: 162264
        [D 190617 21:31:34 openvino_service:96] payload type: <class 'bytes'>
        [D 190617 21:31:34 openvino_service:99] destringify_jpg: 1.29 ms
        [D 190617 21:31:34 openvino_service:103] jpg2bgr: 5.436 ms
        [D 190617 21:31:34 openvino_engine:241] Inference time: 37.625 ms
        [D 190617 21:31:34 openvino_engine:257] Processing output blob
        [D 190617 21:31:34 openvino_engine:258] Threshold: 0.3
        [D 190617 21:31:34 openvino_service:109] Result: {'annotations': [{'top': 261, 'left': 70, 'label': 'dog', 'right': 200, 'bottom': 345, 'confidence': 0.7890625}, {'top': 138, 'left': 398, 'label': 'horse', 'right': 602, 'bottom': 336, 'confidence': 0.3623046875}, {'top': 104, 'left': 174, 'label': 'person', 'right': 274, 'bottom': 366, 'confidence': 0.9931640625}, {'top': 136, 'left': 404, 'label': 'sheep', 'right': 606, 'bottom': 335, 'confidence': 0.6171875}]}
        [D 190617 21:31:34 openvino_service:110] Detection takes 43.864 ms
        [D 190617 21:31:34 openvino_service:115] draw = True
        [D 190617 21:31:34 openvino_service:126] result_hook, annotations: [{'top': 261, 'left': 70, 'label': 'dog', 'right': 200, 'bottom': 345, 'confidence': 0.7890625}, {'top': 138, 'left': 398, 'label': 'horse', 'right': 602, 'bottom': 336, 'confidence': 0.3623046875}, {'top': 104, 'left': 174, 'label': 'person', 'right': 274, 'bottom': 366, 'confidence': 0.9931640625}, {'top': 136, 'left': 404, 'label': 'sheep', 'right': 606, 'bottom': 335, 'confidence': 0.6171875}]
        [D 190617 21:31:34 __init__:50] Send message to topic berrynet/engine/ovdetector/result
