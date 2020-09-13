# Installation

Run the `install_darknet` function in `configure`. BerryNet dev team is making this to be easier and clearer.

# Test Darknet Engine Manually

Use Darknet detector service and `tinyyolovoc` model package as example.

1. Start detector service

        $ bn_darknet \
            -p tinyyolovoc-20170816 \
            --service_name darknet \
            --num_threads 4 \
            --draw \
            --debug
        [D 191206 21:20:42 darknet_service:109] model filepath: /usr/share/dlmodels/tinyyolovoc-20170816/tiny-yolo-voc.weights
        [D 191206 21:20:42 darknet_service:110] label filepath: /usr/share/dlmodels/tinyyolovoc-20170816/voc.names
        layer     filters    size              input                output
            0 conv     16  3 x 3 / 1   416 x 416 x   3   ->   416 x 416 x  16
            1 max          2 x 2 / 2   416 x 416 x  16   ->   208 x 208 x  16
            2 conv     32  3 x 3 / 1   208 x 208 x  16   ->   208 x 208 x  32
            3 max          2 x 2 / 2   208 x 208 x  32   ->   104 x 104 x  32
            4 conv     64  3 x 3 / 1   104 x 104 x  32   ->   104 x 104 x  64
            5 max          2 x 2 / 2   104 x 104 x  64   ->    52 x  52 x  64
            6 conv    128  3 x 3 / 1    52 x  52 x  64   ->    52 x  52 x 128
            7 max          2 x 2 / 2    52 x  52 x 128   ->    26 x  26 x 128
            8 conv    256  3 x 3 / 1    26 x  26 x 128   ->    26 x  26 x 256
            9 max          2 x 2 / 2    26 x  26 x 256   ->    13 x  13 x 256
           10 conv    512  3 x 3 / 1    13 x  13 x 256   ->    13 x  13 x 512
           11 max          2 x 2 / 1    13 x  13 x 512   ->    13 x  13 x 512
           12 conv   1024  3 x 3 / 1    13 x  13 x 512   ->    13 x  13 x1024
           13 conv   1024  3 x 3 / 1    13 x  13 x1024   ->    13 x  13 x1024
           14 conv    125  1 x 1 / 1    13 x  13 x1024   ->    13 x  13 x 125
           15 detection
        mask_scale: Using default '1.000000'
        Loading weights from /usr/share/dlmodels/tinyyolovoc-20170816/tiny-yolo-voc.weights...Done!
        [D 191206 21:20:45 darknet_engine:150] inference time: 1.9036920070648193 s
        [D 191206 21:20:45 __init__:11] Connected with result code 0
        [D 191206 21:20:45 __init__:13] Subscribe topic berrynet/data/rgbimage

1. Send image to service by camera client

        $ bn_camera --mode file --filepath <image-filepath>

1. You should see the inference results on detector's terminal

        [D 191206 21:21:45 __init__:20] Receive message from topic berrynet/data/rgbimage
        [D 191206 21:21:47 darknet_engine:150] inference time: 1.8199963569641113 s
        [D 191206 21:21:47 darknet_service:66] result_hook, annotations: [{'bottom': 342.45084381103516, 'confidence': 0.48404842615127563, 'left': 56.02063751220703, 'label': 'dog', 'right': 198.14881134033203, 'id': -1, 'top': 265.13106536865234, 'type': 'detection'}, {'bottom': 350.23523712158203, 'confidence': 0.32306814193725586, 'left': 107.26636505126953, 'label': 'dog', 'right': 225.97444915771484, 'id': -1, 'top': 275.51012420654297, 'type': 'detection'}, {'bottom': 360.5461120605469, 'confidence': 0.7337859272956848, 'left': 169.8051300048828, 'label': 'person', 'right': 280.67076110839844, 'id': -1, 'top': 94.009033203125, 'type': 'detection'}, {'bottom': 346.7984390258789, 'confidence': 0.6094380021095276, 'left': 412.9965133666992, 'label': 'sheep', 'right': 541.2455520629883, 'id': -1, 'top': 156.6410140991211, 'type': 'detection'}, {'bottom': 359.8292579650879, 'confidence': 0.39942821860313416, 'left': 69.68604278564453, 'label': 'sheep', 'right': 191.7149887084961, 'id': -1, 'top': 254.3123435974121, 'type': 'detection'}]
        [D 191206 21:21:47 __init__:50] Send message to topic berrynet/engine/darknet/result

1. To visualize the received inference result

        $ bn_dashboard --no-decoration --no-full-screen --topic berrynet/engine/darknet/result --debug
