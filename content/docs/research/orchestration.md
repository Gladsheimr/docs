---
title: Orchestration
type: docs
---

# Hybrid Device Applications

The ability to leverage FPGA, Microcontrollers and ASIC devices is that TinyML application can take advantage 
of each devices' specialties. 

FPGAs can provide low latency (<= 1ms), amazing connectivity (direct pin access) and potential low power consumption depending on the application. One the other hand micro-controller significantly reduce engineering time. (See other [advantages of other device types](https://www.arrow.com/en/research-and-events/articles/fpga-vs-cpu-vs-gpu-vs-microcontroller)).


## Concept 

*Predicting water pouring in a room*

Collecting audio and classification can be currently done using TinyML and PDM devices ([Tensorflow Lite Micro](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/micro/examples/micro_speech)). On the Arduino Nano Sense 33 there is a delay in the inference from the input to after the processing. 

Imagining a simple application deployed on an FPGA and Arduino device. Using orchestration we can see what services are live and even capture logs from devices for inspection. 

Known deployed services:

```bash
$ mjl services

NAME               TYPE            PROTOCOLS   AGE

AudioClassifier    TinyFPGA        GPIO        2m0s
MjlDriver          ArduinoBLE33    BLE         2m1s 

```

Looking for devices:

```bash
$ mjl devices

NAME                     TYPE            PROTOCOLS   AGE
AudioClassifier-a2a3fb   TinyFPGA        GPIO        2m0s
MjlDriver-12e21b         ArduinoBLE33    BLE         2m1s 

```

Inspecting devices:

```bash
$ mjl inspect --device AudioClassifier-12e21b --proto GPIO --format pickle

> Discovering AudioClassifier-12e21b > Found trough MjlDriver-12e21b 
> Connecting to MjlDriver-12e21b 
> Inspecting AudioClassifier-12e21b
> Found input and output stream at BLE service a369d1b3-fcf2-4159-84a8-a5751c7b657c
   > Input BLECharacteristic 347f9f7b-a71d-4d8d-b6dd-8c416270b329
   > Ouput BLECharacteristic ae2e723e-c297-4f13-8500-181d01bf2779
Writing binary stream to inspections/AudioClassifier-12e21b/347f9f7b.pickle
Writing binary stream to inspections/AudioClassifier-12e21b/ae2e723e.pickle
```


## Horizontal Scaling

With horizontal scaling the same application can be deployed over several devices. These devices can be placed in multiple locations:

```bash
$ mjl devices

NAME                          TYPE            PROTOCOLS   AGE
AudioClassifier-8675c4e7      TinyFPGA        GPIO        2m0s
MjlDriver-82f85197            ArduinoBLE33    BLE         2m1s 
AudioClassifier-a369d1b3      TinyFPGA        GPIO        2m0s
MjlDriver-9a9c1082            ArduinoBLE33    BLE         2m1s 
AudioClassifier-129c0801      TinyFPGA        GPIO        2m0s
MjlDriver-9a9c1082            ArduinoBLE33    BLE         2m1s 

```

Inspection can aggregate across devices and get a quorum of results. 

```bash
$ mjl inspection --service AudioClassifier 

AudioClassifier service aggregating results across 3 devices.

Writing to inspections/AudioClassifier/out-9c0db0f2.pickle

```

```python
import pickle
from mjl.aggregator import Aggregator

filename = "./inspections/AudioClassifier/out-9c0db0f2.pickle"

results = open(filename,'wb')

results_tuples = pickle.load(results)

# (
#    (1582405387.819107, 1, "AudioClassifier-129c0801"), 
#    (1582405387.819125, 1, "AudioClassifier-a369d1b3"), 
...
#    (1582405387.8191419, 0, "AudioClassifier-a369d1b3"), 
#    (1582405387.819145, 1, "AudioClassifier-8675c4e7")
# )

quorum = Aggregator(quorum=True, window="3ms").results(results_tuple)

# (
#    (1582405387, 1)
...
#    (1582435389, 0), 
#    (1582435399, 1)
# )


results.close()
```
These results can be put together on a raspberry pi or even on a mobile device when in locale area. The `mjl` tool 
allows for development and testing. Testing can be done in this case with a laptop playing sample sounds randomly.
The raw results allows for retraining the models and deploying them. 


## Vertical Scaling 

Vertical scaling would be the process of letting multiple devices run the same application by distributing processing. For example:
having devices request resources and processing from each other over BLE or Direct pin access. 

