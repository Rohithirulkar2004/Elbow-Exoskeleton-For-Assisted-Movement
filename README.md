# Development and Motion Analysis of an Elbow Exoskeleton for Assisted Movement
### Project Implementation Manual

---

## 1. Introduction
The Cable-Driven Elbow Exoskeleton is a wearable robotic system designed to support, aid, and rehabilitate human arm movement. Operating on a single degree of freedom (1 DOF), the device specifically aids in the palmar flexion and dorsiflexion of the elbow joint. The system integrates a back-mounted actuation unit with a human-in-the-loop assistance-as-needed approach, where mechanical support is triggered by real-time sensor data based on the user's intentional movements. 

## 2. System Requirements

**Hardware Requirements**
* Arduino Nano R3 (with CH340)
* 2x DC 12V 30RPM High Torque Quad Encoder Motors (7.5 Nm and 2.5 Nm applications)
* 2x MPU6050 IMU Sensors
* 1x FSR 402 (Force Sensitive Resistor)
* 2x BTS7960 (IBT-2) High-Current Motor Drivers
* 3S Li-po Battery (11.1V) & B3 Charger
* Bowden Cables & Sheaths
* 3D Printed PLA Cuffs and differential spool gears

**Software Requirements**
* Arduino IDE
* Wire Library (for I2C communication)
* MPU6050 Library

## 3. System Setup

### 3.1 Hardware Configuration
* Mount the control unit, high-torque DC motors, BTS7960 motor drivers, and Li-po battery onto the back-mounted assembly to minimize the inertia experienced by the arm.
* Attach the 3D-printed ABS cuffs securely to the user's upper arm and forearm.
* Route the Bowden cables from the back-mounted motor spools directly to the arm cuffs for smooth force transmission.

### 3.2 Sensor & Electronics Setup
* Connect the two MPU6050 sensors and the ACS712 current sensors to the Arduino Nano using the I2C protocol.
* Place the FSR 402 inside the cuff so it detects muscle expansion when the user initiates a lifting motion.
* Wire the Arduino Nano to the two BTS7960 motor drivers using PWM pins to enable variable torque control for both motors.

## 4. Operation and Calibration Setup
1. Attach the MPU6050 sensors to the upper arm and forearm to establish a natural kinematic baseline of normal elbow movement.
2. Perform basic elbow movements (bending and straightening) to allow the system to collect initial data on pitch, roll, yaw, and angular velocity.
3. The system enforces a predefined safe motion limit between 0° and 145° to match the natural elbow range and prevent mechanical hyperextension.

## 5. Module Descriptions

### 5.1 Intent Detection 
* The system utilizes the Force Sensitive Resistor (FSR) to track user intent. 
* Once the muscle pressure meets the required threshold, it acts as the primary trigger to generate PWM signals and activate the motors.

### 5.2 Active Feedback Monitoring
* The Arduino acts as the central brain, continuously reading the joint angles calculated from the two MPU6050 IMUs to ensure smooth operation.
* Current sensors continuously monitor the load, allowing the system to estimate cable tension and detect mechanical blockages.

### 5.3 Antagonistic Actuation Mechanism
* The dual-motor setup works synchronously to manage cable slack and provide smooth motion. To bend the elbow, the system guides the first servo motor to pull (wind) the Bowden cable, while the second motor simultaneously releases (unwinds) its cable to facilitate the flexion.

## 6. System Limitations
* The prototype is designed for experimental use and is not capable of continuous high-load usage or heavy industrial lifting.
* The system relies on basic force and IMU sensing methods rather than advanced medical-grade sensors or high-density EMG due to cost barriers.
* The control algorithm provides simplified assistance and currently lacks adaptive learning capabilities.

## 7. Applications and Improvements

**Applications**
* **Rehabilitation:** Facilitates repetitive and precise movement of the elbow joint necessary for therapy.
* **Industrial Aid:** Reduces muscular activity and workload during repetitive lifting tasks, mitigating occupational tiredness.

**Future Improvements**
* **EMG Integration:** Transitioning to intent-based control via Electromyography to read muscle signals directly for more natural actuation triggering.
* **Material Upgrades:** Replacing PLA with medical-grade nylon or utilizing fabric-based exosuits/soft pneumatic actuators to increase comfort and reduce weight.
* **IoT Monitoring:** Adding Bluetooth or Wi-Fi to allow physiotherapists to remotely access joint angle logs, usage duration, and motor load data.

## 8. Conclusion
The Cable-Driven Upper Limb Exoskeleton successfully demonstrates a low-cost, accessible assistive device for individuals struggling with arm movement. By isolating heavy components to a backpack and utilizing precise MPU6050 feedback combined with DC motor encoders, the 1 DOF mechanism safely generates enough torque to comfortably assist with daily activities, such as lifting a 2kg payload.
