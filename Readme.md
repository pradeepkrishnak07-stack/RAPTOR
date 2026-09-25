# **RAPTOR** 

_Autonomous Robot for Integrated Security and Environmental Hazard Monitoring_

Project Documentation Date: 25 September 2026 Designed and Simulated in Tinkercad 

## **1. Problem Statement** 

**In many environments such as offices, warehouses, and campuses, continuous human monitoring for security and obstacle detection is costly, inefficient, and prone to human error. Traditional surveillance systems often require expensive infrastructure or manual operation, while simple locks and alarms provide only limited protection without active patrolling. There is a need for a low-cost, autonomous mobile robot that can patrol a defined area, detect obstacles or intrusions in real time, and provide immediate local alerts. The challenge lies in integrating sensing, decision-making, and actuation into a compact, affordable system that can operate independently yet remain responsive to manual control when required.** 

## **2. Abstract** 

The Patrol Car is an Arduino-based autonomous mobile robot designed to monitor a defined area and detect obstacles or intrusions in its path. The system uses an ultrasonic sensor mounted on a servo motor to continuously scan the area ahead, an L293D motor driver IC to control two DC motors for movement, a buzzer to raise an audible alert whenever an obstacle is detected within a set safety threshold, and a push button to let an operator start or stop the patrol routine on demand. The project demonstrates the integration of sensing, decision-making and actuation on a single low-cost embedded platform, making it a practical foundation for security patrol robots, automated surveillance carts and obstacle-avoiding vehicles. 

## **3. Objectives** 

1. To design a low-cost, autonomous patrol robot using easily available components. 

2. To detect obstacles in real time using ultrasonic distance sensing. 

3. To use a servo-mounted sensor to scan a wider area than a fixed sensor allows. 

4. To alert nearby personnel of a detected obstacle or intrusion using a buzzer. 

5. To allow manual control of the patrol state (active/idle) using a push button. 

6. To control two DC motors bidirectionally through an L293D driver IC for smooth navigation. 

## **4. Components Used** 

The following hardware components are used in this project, based on the circuit design shown in the schematic: 

|**Component**|**Qty**|**Function in this Project**|
|---|---|---|
|Arduino UNO|1|Main microcontroller; runs the control logic for sensing,<br>decision-making and motor actuation|
|L293D Motor Driver IC|1|Dual H-bridge driver that lets the low-current Arduino pins<br>safely control the higher-current DC motors, and enables<br>direction reversal|
|DC Motor (M1, M2)|2|Drive the left and right wheels of the patrol car for forward,<br>reverse and turning motion|



|Ultrasonic Sensor (HC-SR04)|1|Measures distance to obstacles ahead using ultrasonic echo<br>timing|
|---|---|---|
|Micro Servo Motor|1|Rotates the ultrasonic sensor head left/right to scan a wider<br>field of view|
|Buzzer|1|Sounds an audible alert when an obstacle is detected<br>within the danger threshold|
|Push Button|1|Manually starts/stops the patrol routine or toggles between<br>autonomous and idle mode|
|Jumper Wires / Chassis /<br>Wheels / Battery Pack|As<br>needed|Mechanical structure and electrical connections|



## **5. Circuit Description and Pin Connections** 

The Arduino UNO acts as the central controller. The L293D IC drives both DC motors (M1 and M2), receiving direction signals from the Arduino's digital output pins while the motor supply voltage (VCC2) is fed from a separate battery pack to keep motor noise off the logic supply. The ultrasonic sensor's TRIG and ECHO pins connect directly to two digital pins for distance measurement, and the servo motor's signal pin is driven with a PWM-capable pin so it can sweep the ultrasonic sensor across an arc. The buzzer is switched through a digital output pin, and the push button is read as a digital input to toggle the patrol state. 

|**Arduino Pin**|**Connected To**|**Signal**|
|---|---|---|
|D2|Ultrasonic Sensor - TRIG|Digital Output (trigger<br>pulse)|
|D3|Ultrasonic Sensor - ECHO|Digital Input (echo pulse<br>width)|
|D4|L293D - Pin 1A (Motor 1 direction)|Digital Output|
|D5|L293D - Pin 2A (Motor 1 direction)|Digital Output|
|D6|L293D - Pin 3A (Motor 2 direction)|Digital Output|
|D7|L293D - Pin 4A (Motor 2 direction)|Digital Output|
|D9|Servo1 - Signal (SIG)|PWM Output|
|D10|Buzzer - Input|Digital Output|
|A0|Push Button - Output|Digital Input (with pull-<br>down)|
|5V|L293D VCC1 (logic), Servo PWR, Ultrasonic VCC|Power|
|GND|Common ground - L293D, Servo, Ultrasonic,<br>Buzzer, Button|Ground|
|VCC2 (L293D)|External battery pack (motor supply)|Motor Power|



## **6. Working Principle** 

The patrol car operates in the following sequence: 

1. On power-up, the Arduino initializes all sensors, the servo (centered at 90°) and sets the patrol state to idle. 

2. Pressing the push button toggles the patrol state between active and idle. 

3. While active, the ultrasonic sensor continuously measures the distance to any object ahead. 

4. If the measured distance is greater than the safe threshold (e.g. 20 cm), the L293D drives both motors forward. 

5. If an obstacle is detected within the threshold, the motors stop immediately, the buzzer sounds an alert, and the car executes a turning maneuver via the L293D to steer around the obstacle before resuming patrol. 

6. Pressing the button again halts the car and returns it to idle mode. 

This closed loop of sense → decide → act repeats continuously, allowing the car to patrol autonomously while remaining responsive to manual override at any time. 

## **7. System Block Diagram** 

Conceptually, the system can be represented as: 

- Input stage: Ultrasonic Sensor (distance) + Push Button (manual command) 

- Processing stage: Arduino UNO (decision logic) 

- Output stage: L293D → DC Motors (movement), Buzzer (alert), Servo Motor (sensor scanning) 

Signal flow: Sensors and button → Arduino → processing/decision → L293D + Buzzer + Servo → physical motion and alert. 

## **8. Applications** 

- Automated security patrolling in offices, warehouses or campuses during off-hours. 

- Low-cost surveillance rover for restricted or hazardous areas. 

- Educational platform for learning embedded systems, sensor integration and motor control. 

- Base platform for further upgrades such as camera-based monitoring or wireless alerts. 

## **9. Advantages** 

- Low-cost components and simple circuit design. 

- Autonomous operation reduces the need for continuous human monitoring. 

- Wider area coverage using a servo-scanned ultrasonic sensor instead of a fixed one. 

- Manual override button gives the operator direct control when needed. 

### **9.1 Limitations** 

- Ultrasonic sensing can be less reliable on soft, angled or sound-absorbing surfaces. 

- No long-range wireless alert; the buzzer only provides a local, audible warning. 

- Battery-powered motors limit continuous patrol duration. 

## **10. Future Scope** 

- Add a Wi-Fi/Bluetooth module (e.g. ESP8266) to send remote alerts to a phone or dashboard. 

- Integrate a camera module for visual monitoring and recording. 

- Add IR or PIR sensors for more reliable intrusion/motion detection. 

- Use an encoder-based feedback system for more precise navigation. 

## **11. Conclusion** 

The Patrol Car project successfully demonstrates how an Arduino UNO, an L293D motor driver, an ultrasonic sensor with a servo-based scanning mechanism, a buzzer and a push button can be combined into a functional autonomous patrol robot. It provides a practical, low-cost foundation for security and surveillance applications while remaining simple enough to extend with additional sensors, wireless communication or camera-based monitoring in future iterations. 

