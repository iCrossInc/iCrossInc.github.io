---
layout: post
title:  "Creating the Algorithm"
author: "Sean Miller"
---

Now that Thomas had delivered the board to me, I could begin developing and testing the algorithm that will be used to aggregate the data from the pressure sensors and thermo sensors and decide based upon this data whether it should signal that a pedestrian has been detected. The algorithm itself is very simple: in a continuous, constant loop, the algorithm will attempt to break down each sensor's data into a probability between 0 and 1 corresponding to how "certain" the given sensor is that a pedestrian is present and wants to cross. With these probabilities, the algorithm will then simply find the best way to output whether a pedestrian is present or not. This aggregation step will most likely involve taking the weighted average of different sensors probabilities, taking only the maximum probability of the set of probabilities (or taking the average of the *n* highest probabilities where *n* is some number greater than 0), among other typical data fusion techniques. The algorithm I hypothesized I would use for this project is shown below, represented as a flowchart.

![Algorithm Flowchart](/../assets/FYDP-Software-Flowchart.png)

Luckily, this algorithm is very simple to implement in Arduino. After a quick initial setup, I was able to get the board responding quite well to pressing on the pressure sensors. When I wasn't pressing on any the pressure pads, the algorithm was "outputting a 0" (meaning that it was not detecting any pedestrians), and when I began pressing on one or more of the pressure pads, the algorithm began outputting a 1 (meaning that it detected a pedestrian).

The next step was to interface the board with the thermopile - it so happens that it is much easier to read in data from the pressure sensors than the thermpoile due to the different communication protocols used between each type of sensors and the board. After a long session of work, I was able to get the thermopile successfully hooked up to the system and outputting reasonable data that could be used in the algorithm.

Now that the board is able to read in data from both types of sensors and output reasonable results based on the input data, all that remains for work on the software side of this project is continuing to test and refine the parameters used in the algorithm to get it to become as accurate and reliable as possible.