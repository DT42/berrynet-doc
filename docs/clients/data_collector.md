# Enable Data Collector

Data collector (`bn_data_collector`) is useful if you want to store the snapshot and inference results for data analysis.

Steps to enable data collector:

1. Prepare config file including the topic where AI engine will send inference results to:

    For the default detection engine, you can create a `data_collector.json`

    ```
    {
        "berrynet/engine/tflitedetector/result": "self.update"
    }
    ```

1. Run data collector:

    ```
    $ bn_data_collector --data-dirpath /tmp/bn-outdir --topic-config data_collector.json
    ```

1. Check collected results in the indicated directory: 

    Every inference result will be saved to two files:

    * image, w/ or w/o inference result overlay, depending on the output parameter set to AI engine.
    * text in JSON format, w/o image string in base64 format.

    ```
    $ ls /tmp/bn-outdir
    2019-05-26T13:33:52.277898.jpg
    2019-05-26T13:33:52.277898.json
    ...
    ```
