
"For complete information on the selection process and specific components of our Data Acquisition System (DAQ), you can refer to our comprehensive [thesis here]([www.google.com](https://www.google.com/)). This summary will provide an overview of the DAQ, the operation of our controller board, and how to load the firmware.

The DAQ design comprises two distinct Printed Circuit Boards (PCBs): the primary shield and the extension shield. The primary shield includes voltage regulation, power filtering, three amplifiers, and the Teensy 3.6 microcontroller. This board is suitable for applications that require single 3-axis load cell or single load cells. For more complex applications, we've designed an extension shield, housing an additional nine amplifiers. The combined system meets the requirements for a six-degree-of-freedom plate sensor, providing comprehensive data acquisition and processing.

Power is supplied via a USB connector, and voltage regulation is managed through a Low Dropout (LDO) regulator to stabilize voltage. The signal from the load cells is amplified using an INA333 amplifier, with gain finely tuned via a multiturn trimmer potentiometer. The output of the amplifier is clamped to 3.3 volts to prevent potential damage from overvoltage. The microcontroller performs additional processing, data filtering, and oversampling operations, and it transmits the results for further analysis.

Please refer to the Github repository for the implementation, calibration, and reading from load cells code, with detailed instructions on usage and modification."](<For an in-depth exploration of our Data Acquisition System (DAQ), including component selection and the decision-making process, refer to our detailed thesis. In this summary, I'll outline the integral components, how they contribute to our DAQ operation, and briefly cover the firmware loading process.

## **Amplifier**

At the heart of our DAQ's signal conditioning is the Instrumentation Amplifier (INA333). This amplifier receives the signal from the load cells, which are typically small and necessitate amplification for further processing. The INA333 was chosen for its precise and low noise amplification capabilities, crucial for accurate data acquisition in our system.

The gain of the INA333 is finely adjustable using a multiturn trimmer potentiometer as the gain-setting resistor. This type of resistor allows us to fine-tune the amplifier's gain to a specific force range applied to the load cells. Calibration is recommended using the maximum expected force for optimal performance.

To ensure the safety of the downstream components and prevent potential overvoltage damage, the amplifier's output is clamped to 3.3 volts using filtering components at the amplifier's output.

## **Signal Conditioning**

Signal conditioning prepares the load cell's output for digital conversion by the microcontroller. After amplification, the signal is passed through a series of filter components. These filter components serve to eliminate unwanted noise that may distort the signal and affect the accuracy of the data.

A Low Dropout (LDO) regulator and a band-pass filter work in tandem to stabilize the voltage and eliminate power line noise at 50 and 60 Hz, respectively. This treatment ensures a clean supply voltage for the microcontroller and the excitation voltage for the load cells.

## **Microcontroller**

The Teensy 3.6 microcontroller serves as the powerhouse of our DAQ. Its high-speed 180 MHz ARM Cortex-M4 processor, equipped with 256K RAM and 1M Flash memory, facilitates the efficient management of multi-channel load cell data.

This microcontroller also hosts the Analog-to-Digital Converter (ADC). The ADC's role is to sample the conditioned analog signal and convert it into a digital representation. The Teensy 3.6's ADC can clock at 24 MHz for lower precision and 12 MHz for 16-bit precision. The resolution of the ADC is significant as it determines the precision of the digital representation. For our purposes, a 13-bit resolution, representing one of 8192 distinct values, provides the necessary detail. 

Our DAQ's primary component is the Teensy 3.6 microcontroller. It boasts a 180 MHz ARM Cortex-M4 processor, 256K RAM, and 1M Flash memory, providing ample processing power to handle multi-channel load cell data.

The DAQ's Analog-to-Digital Converter (ADC) plays a significant role. The Teensy 3.6's ADC is designed for speed and precision, capable of clocking at 24 MHz for lesser precision and 12 MHz for 16-bit precision. In testing, we could read up to 12 channels at over 5kHz with 13 bits of resolution, surpassing the 1kHz baseline. The ADC can represent an analog voltage with 8192 (2^13) distinct values, providing detailed digital representation of the analog signal. The Teensy 3.6 has 25 pins available for analog inputs, enhancing read time optimization.

## **Final Design**

Our final DAQ design includes two distinct Printed Circuit Boards (PCBs) - a primary shield and an extension shield. The primary shield, equipped with voltage regulation, power filtering, the microcontroller, and three INA333 amplifiers, caters to applications requiring single or 3-axis load cells. 

For more complex data acquisition needs, an extension shield, equipped with nine additional amplifiers, can be attached below the primary shield. Together, the shields can meet the needs of a six-degree-of-freedom plate sensor.

This design choice offers users flexibility and scalability. They can opt for the primary shield for simpler applications or expand their system with the extension shield for more advanced, multi-axis sensor applications. 

Power is supplied via a USB connector. The microcontroller performs data filtering, oversampling, and further processing of the signals. After computation, the resultant forces and moments are transmitted to a computer for interpretation and analysis.

For calibration and reading from load cells, the required code and detailed instructions are available in our Github repository. Our goal is to facilitate a seamless user experience and make modifications and use as straightforward as possible. This modular and robust design ensures that our DAQ system is suitable for a wide range of applications, balancing performance, cost, and ease of use.>)



```cpp
#include <ArduinoOSC.h>
#include <Wire.h>

#define NUM_CHANNELS 12 // Number of channels

// Variables to store the filtered values
int filteredValues[NUM_CHANNELS] = {0};

// Low pass filter factor
float alpha = 0.5;

// Create an OscSender object
OscSender sender;

void setup() {
  // Setup your Serial Communication
  Serial.begin(9600);
  
  // Setup your OSC Sender
  sender.begin("<IP_ADDRESS>", 10000); // Replace <IP_ADDRESS> with your computer's IP
}

void loop() {
  for (int i = 0; i < NUM_CHANNELS; i++) {
    // Read the raw value from the sensor
    int rawValue = analogRead(i);

    // Apply a simple low-pass filter
    filteredValues[i] = alpha * rawValue + (1.0 - alpha) * filteredValues[i];
    
    // Prepare the OSC message
    char buffer[50];
    sprintf(buffer, "/loadCell/%d", i);
    
    // Send the filtered value over OSC
    sender.send(buffer).add(filteredValues[i]).end();
  }
}

```