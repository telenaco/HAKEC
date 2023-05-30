
This work emphasizes accelerometer setups for measuring vibrations due to their cost-effectiveness, accessibility, and widespread use in haptic research. Table X documents various accelerometers employed in characterizing haptic devices. The literature review outlines the characterization process, beginning with transducers (accelerometers), followed by coupling, data acquisition, and data processing.

Commercial accelerometers, or Inertial Motion Units (IMUs), utilize microelectromechanical systems (MEMS) technology, integrating electrical and mechanical components on a single chip to detect acceleration. The accelerometer measures capacitance changes caused by an internal mass's movement, converting it into an electrical signal. When characterizing haptic devices using accelerometers, several properties should be considered:

The measuring range of an accelerometer is crucial for devices that produce large vibrations, as it indicates the maximum acceleration the sensor can measure. A broader measuring range ensures that the device can accurately capture the full extent of the vibrations produced by the haptic interface.

The frequency range of the accelerometer determines the range of detectable vibration frequencies, which is essential for devices generating vibrations across a wide frequency range. However, it is important to note that human vibration perception is limited to frequencies below 1 kHz, rendering frequencies above this range imperceptible [63]. Due to human perception limitations in discerning the direction of high-frequency vibrations, data from the three axes can be combined using the DFT321 algorithm to produce a single, comprehensive signal.

Data output, which can be either analog or digital, impacts data processing and analysis. When working with digital sensors, the resolution is limited by the ADC, and the data update rate is constrained by the digital protocol. These factors must be considered when integrating the sensor with microcontrollers or data acquisition systems (DAQs).

Sensitivity refers to the minimum detectable acceleration, which is vital for capturing the full expressiveness of haptic stimuli. In analog accelerometers, sensitivity determines the analog voltage output per axis, which is based on the mV/g ratio.

Finally, the dimensions and physical properties of the accelerometer are crucial factors when selecting a sensor for a haptic device. The sensor may need to fit within space-constrained devices, and its dimensions are closely related to its weight. Higher mass can potentially affect the performance of the actuator. By carefully selecting an accelerometer with appropriate dimensions and weight, accurate and reliable measurements can be obtained without compromising the actuator's performance.


|               |                 |                            |                       |        |              |                                   |           |
| ------------- | --------------- | -------------------------- | --------------------- | ------ | ------------ | --------------------------------- | --------- |
| Accelerometer | Measuring Range | Frequency Range (Khz)      | Data<br><br>Type      | Cost 1 | Sensitivity  | Dimmensions (Mm)<br><br>- Package | Citations |
| LIS344ALH     | ±6 G            | 1.8                        | Analog                | $14    | Vdd/15       | 4x4x1.5<br><br>Lga-16l            |           |
| 352C23 ICP    | ±1000 G Pk      | 10                         | Analog                | $200   | 5 Mv/G       | 4.1x8.6x2.8                       |           |
| LSM6DS3       | ±16 G           | 6.7                        | I2c<br><br>16bit      | $9.43  | 0.488 Mg/Lsb | 2.5x3x0.86<br><br>Lga-14l         |           |
| ADXL335       | ±3 G            | 1.6 (X, Y)<br><br>0.55 (Z) | Analog                | $ 9.6  | 300 Mv/G     | 4x4x1.5<br><br>Lfcsp-16           |           |
| ADXL345       | ±16g            | 3.2hz                      | Spi, I²C<br><br>13bit | $1.9   | 256lsb/G     | 3x5x1.5<br><br>Lga-14             |           |
| ADXL356       | ±40g            | 2.4hz                      | Analog                | $24    | 80  Mv/G     | 6x5.6x2.05<br><br>Lcc-14          |           |

_Table_ _1_ _Summary of accelerometers used on previous work to meassure vibrations of vivrotactile actuators.Cost might vary depending on the package of the chip. *1 prices based on_ [_https://www.lcsc.com/_](https://www.lcsc.com/) _as 01/23_