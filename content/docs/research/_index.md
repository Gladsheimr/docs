---
title: Introduction
type: docs
---

# Research 

Glaðsheimr research is based around a vision:

*Orchestrating and integrating computation, biology and engineering principals*

## Cybernetics: Complete Stack Applications

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
are requiring extra steps to provide a lack luster solution (mobile health apps are notoriously bad at achieving results and health is hard). Data used to determine successes of the application is derivative and the end results of numerous processes.  

There are a plethora of moving parts and engineering wise this solution is not idea. In integration we want to have a simple critical path that allows:

1. Measurable feedback independent of human bias (people lie about their weight regularly)
2. Reduce unnecessary interfacing components 
3. Remove artificial boundaries in development 
    1. Biology is not understood at app development level 
    2. Algorithms are unaware of how to determine a success/failure 
    3. Alice has to understand how to implement the program


### Back to the Drawing Board

Focusing on the goal "Making Alice Healthy" we can start to re-engineer a concrete solution. For the purpose of this exercise let's 
determine health based on most common diseases for Alice's cohort (24F, High BMI, Hyperglycimia). Although Health could be defined medically, 
we also have to consider how Alice determines healthy and thus focusing on quality of life makes more sense. Alice's overall lifestyles 
plays a larger part in determining what Health means.

 Top causes of loss of quality of life for Alice's cohort 
are cardiovascular diseases and diabetes. 

*Measuring Health with Biological Signals*