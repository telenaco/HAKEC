# Haptic Force Feedback Modeling Framework: Component Overview

Our framework relies on a variety of components designed and built to accurately measure forces and torques. This landing page serves as an introduction to these components, with each having its dedicated page for a more detailed exploration.

## [[Review of Load Cells]]

![[Pasted image 20230530113213.png | 800]]

Load cells play a crucial role in our framework, measuring force and torque. With a vast array of options, making a choice can seem overwhelming. This section provides a concise summary of load cells used in previous studies, including cost estimates, to assist you in understanding the options available. Navigate through this guide to help choose the most suitable load cell for your needs.

## [[Review of Accelerometers]]

![[Pasted image 20230530113344.png | 800]]

Accelerometers, commonly used to measure vibrations, have not yet been incorporated into our framework. Nevertheless, we recognize their potential utility. In this section, we've compiled a list of frequently used accelerometers and their features from extensive literature review. This summary should give you a glimpse of the options.

## [[Bar Cell Comparison and Performance Analysis]]

![[Pasted image 20230530113429.png | 800]]

Diving into our load cell review, you might notice a few things: the vast price range (from around $10 to the thousands), two main categories (single-axis load cells and force/torque sensors measuring six axes), and the frequent use of low-cost load cells in the validation of kinesthetic devices. This section delves into these points, focusing on a performance comparison of three low-cost load cells to assess their suitability for kinesthetic device characterization.

## [[Button Load Cell Comparison and Performance Analysis]]

![[Pasted image 20230530113505.png | 800]]

Button load cells offer unique advantages in certain applications due to their compact size and easy integration into devices or measuring jigs. In this section, we take a similar approach to our bar load cell analysis and compare the performance of three popular button load cells. We compare different button load cells, examining their characteristics and performance to facilitate an informed selection for specific use-cases.

## [[Building a 3-Axis Load Cell]]

![[Pasted image 20230530113622.png | 800]]

Single-axis force sensors, like those presented above, have significant limitations in measuring the operation of a haptic device. While they're suitable for measuring an actuator's direct output, once mounted on a device, users often experience multi-axis forces or torques. As a result, a more sophisticated sensor solution becomes necessary. In this section, we present our first step towards addressing this challenge - a three-axis load cell capable of measuring forces along the X, Y, and Z axes. This sensor provides a more comprehensive picture of the forces at play in haptic devices. 

## [[Building a 6-Axis Load Cell]]

![[Pasted image 20230530113640.png | 800]]

The experience of a haptic actuator differs considerably when it's mounted on a controller at a distance from the hand. Rather than the direct forces, what the user perceives are torques. While characterizing the output of the haptic actuator is a valid approach, it falls short given the variety of controller designs and implementations. For a more standardized and accurate representation of a haptic controller's performance and capabilities, the focus should be on characterizing the perceived haptic experience of the user. This introduces the need for a six-axis load cell capable of measuring not only forces but also torques, as we'll introduce in this section. While there are commercial solutions available, they're mainly targeted at industrial applications. These six-axis sensors are undoubtedly accurate and reliable, but they come with a hefty price tag, often upwards of $5,000. This price point can be prohibitive for small research labs or independent researchers. This section introduces our DIY cost-effective six-axis load cell solution, designed with these challenges in mind.

## [[Design and Implementation of the DAQ]]

![[Pasted image 20230530113718.png | 800 ]]

In the context of haptic device characterization, the role of sensors, such as load cells or force-torque sensors, is paramount in translating physical entities such as force into digitizable signals. However, processing and recording of these signals necessitate an equal robust and suitable Data Acquisition (DAQ) system to convert and process those signals. This section elaborates on the design and implementation of our DAQ system. Custom-designed to handle up to 12 channels, this DAQ system converts the signal from our sensors into quantifiable electrical signals. Consequently, this facilitates rigorous measurement, quantification, and analysis processes integral to assessing the performance of haptic controllers. This discussion provides an in-depth understanding of our DAQ's operation within the larger haptic feedback framework.