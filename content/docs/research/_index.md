---
title: Research
type: docs
---



# Research 

**by [Kartik Thakore](https://twitter.com/KartikThakore)**

Glaðsheimr research is based around a vision:

*Orchestrating and integrating ML, devices and engineering principles to provide complete stack applications as opposed to full stack*

## Cybernetics and Mobile Health 
**An Complete Stack Application**

Defining cybernetics as a merger between hardware, software and biology we can imagine health (behavior change) apps today
as such a device. 

{{< mermaid >}}
sequenceDiagram
    Alice->>App: Sets goal
        App->>Alice: recommends caloric tracking program
    Alice->>Alice's Biology: Implements program
        Alice's Biology->>Alice: Homeostatic and Physiological Resistance 
        Alice's Biology->>Alice's Devices: Automated Tracking
        Alice's Devices->>App: Tracking integrated
        App->>Alice: Updated recommendations
{{< /mermaid >}}

### Inefficient Integrations

In this case Alice, her biology, software on the app and wearable devices are integrated into an overall goal; Making Alice Healthy. This type of complete stack application
are requires extra steps to provide a lack luster solution (mobile health apps are notoriously bad at achieving results and health is hard). Data used to determine successes of the application is derivative and the end results of numerous processes.  

There are a plethora of moving parts and engineering wise this solution is not idea. In integration we want to have a simple critical path that allows:

1. Measurable feedback independent of human bias (people lie about their weight regularly)
2. Reduce unnecessary interfacing components 
3. Remove artificial boundaries in development 
    1. Biology is not understood at app development level 
    2. Algorithms are unaware of how to determine a success/failure 
    3. Alice has to understand how to implement the program


### Back to the Drawing Board

Focusing on the goal "Making Alice Healthy" we can start to re-engineer a concrete solution. For the purpose of this exercise let's 
determine health based on most common diseases for Alice's cohort (54F, High BMI, Hyperglycimia). Although Health could be defined medically, 
we also have to consider how Alice determines healthy and thus focusing on quality of life makes more sense. Alice's overall lifestyles 
plays a larger part in determining what Health means.

Let's say that top causes of loss of quality of life for Alice's cohort 
are metabolic syndrome[^1] (which wouldn't be too unreasonable). 
Digesting these diseases into biological signals would provided the most efficient interface
to measuring success of our complete stack application. 

*Measuring with Biological Signals*

1. Waist Circumference 
2. Triglycerides
3. HDL Cholesterol
4. Blood Pressure
5. Fasting Glucose

Using these signals gives a clearer picture of "health", and treating these as outputs from "Alice's Biology" is a good starting point. The most frequent signal used is Waist Circumference which should be simple to collected in the morning when Alice wakes up. Waist circumference can be measured in the bathroom and to meet privacy concerns with a disconnected smart device (this device would not connect to any server). 

The waist circumference measurements (with measurement errors) would then be collected to a device that is able to aggregate with other signals (either from external sources or locally). In the case of Alice, let's imagine the solution to have:

1. Waister: Waist Circumference - FPGAs + Camera in washroom
2. GoodFood: Food Quality - FPGAs + Cameras in Kitchen
3. TooManyCooks: Cooking Frequency - Presence detection TinyML Device
4. AliceHealth: Labeling and Data Update - Mobile App

Each of these services can be put into a local cloud or more apt endpoint cloud.


## Endpoint Cloud
{{< mermaid >}}
graph TD
  A[Alice] -->| Labels | B(Alice Health App)
  B --> R{should retrain ?}
  R --> C(Training Device)
  C -->| Deploys | D[TooManyCooks]
  C -->| Deploys | E[Waister]
  C -->| Deploys | F[GoodFood]
  D -->| Presence Detected<br />in Kitchen | F[Signal Aggregrator]
  E -->| Waist<br /> Circumference<br /> Measurement | F
  F -->| Low Power Bluetooth <br /> Collection | B
{{< /mermaid >}}

In this scenario locality of computation, modelling and data is kept to where Alice is and where her health matters. Developing such an application requires a few underlying components:

1. Signal Aggregator - Arudino BLE 
2. Training Device - Raspberry Pi or Coral Device

These components need to part of the orchestration fabric. The major advantages to this step is the fewest number of integrations back to a central server that is out of control/hand for Alice. Additionally, in this complete stack the focus is completely relevant to specific biological signals that don't require integration with other partners. Finally, Alice has complete control of her data and models that are used to help her. Everything is owned by her. 


In the next chapter we will explore developing this usecase. 








[^1]: https://www.mayoclinic.org/diseases-conditions/metabolic-syndrome/symptoms-causes/syc-20351916
[^2]: http://www.cqaimh.org/pdf/tool_metabolic.pdf
