# Engine: TensorFlow Lite

## Demo Video

[![Demo: BerryNet object detection on Raspberry Pi 4](https://img.youtube.com/vi/zgDwGA90P6k/0.jpg)](https://www.youtube.com/watch?v=zgDwGA90P6k)

## Installation

Run the `install_tensorflow` function in `configure`. BerryNet dev team is making this to be easier and clearer.

## Test TFLite Engine Manually

Use TFLite detector service and `mobilenet-ssd-coco-tflite` model package as example.

1. Start detector service

        $ python3 tflite_service.py \
            --service detector \
            --model /usr/share/dlmodels/mobilenet-ssd-coco-tflite-2.0.0/model.tflite \
            --label /usr/share/dlmodels/mobilenet-ssd-coco-tflite-2.0.0/labels.txt \
            --service_name tfdetector \
            --num_threads 4 \
            --draw \
            --debug
        /usr/lib/python3.7/importlib/_bootstrap.py:219: RuntimeWarning: compiletime version 3.5 of module 'tensorflow.python.framework.fast_tensor_util' does not match runtime version 3.7
          return f(*args, **kwds)
        [D 190711 11:50:17 tflite_service:174] model filepath: /usr/share/dlmodels/mobilenet-ssd-coco-tflite-2.0.0/model.tflite
        [D 190711 11:50:17 tflite_service:175] label filepath: /usr/share/dlmodels/mobilenet-ssd-coco-tflite-2.0.0/labels.txt
        INFO: Initialized TensorFlow Lite runtime.
        [D 190711 11:50:17 __init__:11] Connected with result code 0
        [D 190711 11:50:17 __init__:13] Subscribe topic berrynet/data/rgbimage

1. Send image to service by camera client

        $ bn_camera --mode file --filepath <image-filepath>

    Example image: `wget https://github.com/pjreddie/darknet/raw/master/data/dog.jpg`

1. You should see the inference results on detector's terminal

        [D 190705 15:39:20 __init__:20] Receive message from topic berrynet/data/rgbimage
        [D 190705 15:39:20 tflite_service:46] payload size: 161232
        [D 190705 15:39:20 tflite_service:47] payload type: <class 'bytes'>
        [D 190705 15:39:20 tflite_service:50] destringify_jpg: 4.505 ms
        [D 190705 15:39:20 tflite_service:54] jpg2bgr: 10.444 ms
        [D 190705 15:39:21 tflite_service:60] Result: {'annotations': [{'label': 'person', 'confidence': 0.9751802682876587, 'left': 187, 'top': 99, 'right': 273, 'bottom': 384}, {'label': 'sheep', 'confidence': 0.9385143518447876, 'left': 401, 'top': 135, 'right': 600, 'bottom': 339}, {'label': 'dog', 'confidence': 0.7179926037788391, 'left': 68, 'top': 263, 'right': 200, 'bottom': 349}]}
        [D 190705 15:39:21 tflite_service:61] Detection takes 527.504 ms
        [D 190705 15:39:21 tflite_service:66] draw = True
        [D 190705 15:39:21 tflite_service:77] result_hook, annotations: [{'label': 'person', 'confidence': 0.9751802682876587, 'left': 187, 'top': 99, 'right': 273, 'bottom': 384}, {'label': 'sheep', 'confidence': 0.9385143518447876, 'left': 401, 'top': 135, 'right': 600, 'bottom': 339}, {'label': 'dog', 'confidence': 0.7179926037788391, 'left': 68, 'top': 263, 'right': 200, 'bottom': 349}]
        [D 190705 15:39:21 __init__:50] Send message to topic berrynet/engine/tflitedetector/result

1. To visualize the received inference result

        $ bn_dashboard --no-decoration --no-full-screen --topic berrynet/engine/tflitedetector/result --debug
