# ESP32-Line-Following-Robot
A high-performance Line Following Robot powered by the ESP32. Features PID control for smooth navigation, IR sensor array integration, and expandable wireless capabilities.

# Line Follower 🏎️

ESP32-powered line follower designed for speed and precision. It utilizes the **QTR-8RC** reflectance sensor array and a custom PID control loop to navigate tracks with high accuracy.

## 🛠️ Required Equipment

### Core Components
* **Microcontroller:** ESP32 (30-pin or 38-pin DevKit)
* **Sensor Array:** QTR-8RC (8-Channel Reflectance Sensor)
* **Power:** 2S Li-ion Battery (7.4V)
* **Voltage Regulation:** LM2596 Buck Converter (Step-down to 5V)
* **Chassis:** 4-Wheel Drive + Caster high-speed chassis

### Wiring & Tools
* Jumper Wires (Female-to-Female & Male-to-Female)
* Soldering Iron (for permanent connections)
* Breadboard (for prototyping)

---

## 🔌 Pin Mapping (Wiring Diagram)

To ensure the PID logic functions correctly, the sensors must be wired in the exact order defined in the code array: `{4, 23, 2, 5, 18, 19, 21, 22}`.

### 1. Sensor Data Pins (Signal)
*Viewed from behind the robot, looking forward.*

| Sensor Position | QTR-8RC Pin | ESP32 GPIO |
| :--- | :--- | :--- |
| **Far Left** | Pin 1 | **GPIO 4** |
| **Mid Left** | Pin 2 | **GPIO 23** |
| **Inner Left** | Pin 3 | **GPIO 2** |
| **Center Left** | Pin 4 | **GPIO 5** |
| **Center Right** | Pin 5 | **GPIO 18** |
| **Inner Right** | Pin 6 | **GPIO 19** |
| **Mid Right** | Pin 7 | **GPIO 21** |
| **Far Right** | Pin 8 | **GPIO 22** |

### 2. Power & Control Pins
| QTR Pin | Connection | Note |
| :--- | :--- | :--- |
| **VCC** | **Buck Converter (5V)** | 5V provides better accuracy than 3.3V |
| **GND** | **ESP32 GND** | Common ground is required |
| **LED ON** | **ESP32 3.3V or 5V** | High signal keeps IR LEDs active |

---

## ⚡ Electrical Best Practices

### The "RC" Reading Method
The QTR-8RC works by charging a capacitor and timing its discharge. Because timing is critical:
* **Avoid Long Wires:** Keep sensor wires as short as possible to reduce capacitance interference.
* **Noise Reduction:** Twist the **VCC** and **GND** wires together to cancel out electromagnetic interference from the motors.

### Power Management
* **Star Grounding:** Connect the Sensor GND and Motor Driver GND at a single point (the ESP32 GND) to prevent "ground loops" that can crash Bluetooth or Serial communication.
* **Voltage Stability:** Always use a Buck Converter for the sensors; drawing 5V directly from the ESP32 while motors are running can cause sensor "jitter."

## 🚀 Getting Started
1. Connect the pins according to the table above.
2. Upload the `Automatic.ino` sketch.
3. Perform the **Calibration Sequence** (rotating the robot over the line) to set the threshold for your specific track surface.
4. For the Bluetooth connection upload the 'BluetoothEnable.ino' sketch
