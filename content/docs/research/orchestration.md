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

Collecting audio and classification can be currently done using TinyML and PDM devices ([Tensorflow Lite Micro](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/micro/examples/micro_speech)). On the Arduino Nano Sense 33 there is a delay in the inference from the input to after the processing. By 

```bash
$ mjl services

NAME            TYPE            PROTOCOLS   AGE

AudioProcess    TinyFPGA        GPIO        2m0s
ArdConnector    ArduinoBLE33    BLE         2m1s 

```

```bash
$ mjl devices

NAME        TYPE            PROTOCOLS   AGE
AP-a2a3fb   TinyFPGA        GPIO        2m0s
AC-12e21b   ArduinoBLE33    BLE         2m1s 

```

```bash
$ mjl inspect --device AP-a3a3fb --proto GPIO --format pickle
> Discovering AP-a3a3fb > Found with AC-12e21b
> Connecting to AC-12e21b 
> Inspecting AP-a3a3fb
> Found input and output stream at BLE service a369d1b3-fcf2-4159-84a8-a5751c7b657c
   > Input BLECharacteristic 347f9f7b-a71d-4d8d-b6dd-8c416270b329
   > Ouput BLECharacteristic ae2e723e-c297-4f13-8500-181d01bf2779
Writing binary stream to inspections/AP-a3a3fb/347f9f7b.pickle
Writing binary stream to inspections/AP-a3a3fb/ae2e723e.pickle
```


## Horizontal Scaling


## Vertical Scaling 

