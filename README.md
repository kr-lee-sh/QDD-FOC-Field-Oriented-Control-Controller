<img width="2252" height="1833" alt="Image" src="https://github.com/user-attachments/assets/742f8af0-085f-4f3b-8b7b-b464cdb11802" />

# QDD-FOC-Field-Oriented-Control-Controller

Open-source FOC motor controller designed for
a quasi-direct-drive (QDD) actuator.

## Overview

This project focuses on the design and development
of a custom FOC motor controller for a QDD actuator.

The main focus of this project is the electrical
and control system rather than the mechanical design
of the actuator.

The mechanical system is documented primarily in
the following areas:

- Reduction mechanism
- Output shaft position sensing


## Exploded View

<img width="2137" height="1345" alt="Image" src="https://github.com/user-attachments/assets/e5b00187-19f0-410f-8a91-6aa565b95e28" />

## System Architecture

<img width="815" height="454" alt="Image" src="https://github.com/user-attachments/assets/13b7e828-e8c0-43e2-875e-7c0ae10ffcc6" />

The configuration for controlling the QDD actuator is as follows:

1. It receives commands to be executed from an external device via the interface.
- Communication utilizes the RS485 standard, which ensures reliable operation even in the presence of external noise; data transmission distances of up to 1,200 meters are achievable when a terminal resistor is installed.

2. The MCU interprets the received data and executes the corresponding commands.
- Critical data can be stored in the EEPROM for semi-permanent retention.

3. The MCU sends drive commands to the inverter in the form of SVPWM signals.
- SVPWM is an efficient PWM control method designed to control motors using three-phase inverters.
- An NTC thermistor is installed near the inverter's MOSFETs, allowing the MCU to monitor MOSFET temperatures in real time; this feature enables system shutdown in the event of overheating.

4. Since the actuator is equipped with a reduction gear, the position of the motor rotor does not align with the position of the actual output shaft.
- To address this, encoders are installed on both the motor and the output shaft to transmit their respective positions to the MCU in real time.
- The output shaft encoder is used to determine the position upon initial startup.
The motor shaft encoder is subsequently used to drive the motor via FOC control.

## Main Features
1. 3-phase BLDC/PMSM FOC
<img width="1163" height="341" alt="Image" src="https://github.com/user-attachments/assets/eca35c09-0e9a-4c69-b991-978b8e5a7e85" />

- This method employs Field Oriented Control (FOC), which controls the motor by transforming phase currents into d-axis and q-axis currents referenced to the rotor. The three-phase currents (Ia, Ib, Ic) measured from the motor are converted into d-q axis currents (Id, Iq) using the electrical angle (theta). Each current is compared against a reference value, and a PI current controller generates voltage commands (Vd, Vq). Subsequently, the d-q axis voltages are converted back into three-phase voltages, and PWM is used to generate inverter switching signals to drive the PMSM. Additionally, feed-forward compensation is applied to compensate for coupling components between the d-axis and q-axis.

2. Gate driver
3. STM32-based control
4. Current sensing
5. Magnetic encoder
6. Output shaft position sensing
7. Reduction mechanism
8. RS485 communication

## Hardware

- NTC
- EEPROM
- ROTOR ENCODER
- OUTPUT ENCODER
- RS485 COMMUNICATION
- DC-DC CONVERTER
- REGULATOR 3.3V, 5V
- 3-PHASE INVERTER
- CURRENT SENSING

## Firmware

- Inverter drive test using open-loop control
- Rotor encoder sensing test
- 
## License

## References
