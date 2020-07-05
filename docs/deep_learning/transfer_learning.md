## Use Your Data To Train

The original instruction of retraining YOLOv2 model see [github repository of darknet](https://github.com/AlexeyAB/darknet#how-to-train-to-detect-your-custom-objects)

In the current of BerryNet, TinyYolo is used instead of YOLOv2. 
The major differences are:

1. Create file yolo-obj.cfg with the same content as in `tiny-yolo.cfg`
2. Download pre-trained weights of darknet reference model, `darknet.weights.12`, for the [convolutional layers](https://drive.google.com/drive/folders/0B-oZJEwmkAObMzAtc2QzZDhyVGM?usp=sharing) (6.1MB)

The rest parts are the same as retraining YOLO.

If you use [LabelMe](http://labelme.csail.mit.edu/Release3.0/) to annotate data, `utils/xmlTotxt.py` can help convert the xml format to the text format that darknet uses.
