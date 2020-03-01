---
title: Proof of Concepts
type: docs
---

# Audio, Arduino and FPGA

In this proof of concept we want to showcase how multiple devices can be used to build the 
an application (detect keywords in sounds). 

## Overview 

The application will replicate another TinyML proof of concept that was demonstrated in Tensorflow Lite Micro. The PoC infers command words on PDM (Pulse Density Modulation) signals. The code and 
documentation for this application is available on the [Tensorflow github repo](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/micro/examples/micro_speech).

The proposed approach is to showcase how Mjolnir can help template, configure and orchestrate the application over two devices the [Arduino 33 BLE Nano Sense](https://store.arduino.cc/usa/nano-33-ble-sense) and [TinyFPGA BX](https://tinyfpga.com/). 

{{< mermaid >}}
sequenceDiagram
    Mjolnir->>Arduino33BLE: Deploys configuration
    Arduino33BLE->>TinyFPGA: Sends PDM data
    TinyFPGA->>Arduino33BLE: Infers command word
    Arduino33BLE->>Mjolnir: Collects inferences and raw data
{{< /mermaid >}}

## Steps:

1. Collect the tensorflow micro speech data and inference over BLE to Mjolnir
    0. Iterate the [BLE collector example](https://github.com/Gladsheimr/mjolnir/tree/v0.0.1_MjlOrc/poc/ble-collector) 
    1. The hard coded UUID for the service and characteristics 
2. Wire the Arudino 33 BLE nano to TinyFPGA BX and collect and send BLE data to Mjolnir
3. Deploy the model to TinyFPGA BX and collect over BLE




