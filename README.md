# 🤖 Multi-Functional Arduino Robot Car

<div align="center">

![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white)
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![Bluetooth](https://img.shields.io/badge/Bluetooth-0082FC?style=for-the-badge&logo=bluetooth&logoColor=white)
![MIT License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)

**An intelligent Arduino-based robot car with autonomous obstacle avoidance, wireless Bluetooth control, and voice command functionality**

[📋 Features](#-features) •
[🛠️ Hardware](#️-hardware-requirements) •
[🔧 Setup](#-setup-installation) •
[🎮 Control Methods](#-control-methods) •
[📱 Mobile App](#-mobile-app-setup) •
[🔊 Voice Commands](#-voice-commands)

</div>

---

## 🌟 **Project Highlights**

This advanced Arduino robot car combines multiple control systems and autonomous navigation capabilities, making it perfect for robotics enthusiasts, students, and educational demonstrations.

### 🎯 **Key Capabilities**
- 🚗 **Autonomous Navigation** - Intelligent obstacle detection and avoidance
- 📱 **Bluetooth Control** - Wireless smartphone control via custom app
- 🎤 **Voice Commands** - Hands-free voice-activated control
- 🔄 **Multi-Mode Operation** - Switch between manual and autonomous modes
- 🎛️ **Real-time Control** - Responsive movement and precise servo control

---

## ✨ Features

### 🤖 **Autonomous Mode**
- **Ultrasonic Obstacle Detection** - 360° scanning with servo-mounted sensor
- **Smart Navigation** - Automatic path planning and obstacle avoidance
- **Distance Threshold** - Configurable safety distance (12cm default)
- **Intelligent Turning** - Scans left/right to find optimal path

### 📱 **Bluetooth Control Mode**
- **Real-time Commands** - Instant response to smartphone inputs
- **Directional Control** - Forward, backward, left, right, and stop
- **Custom Mobile App** - Dedicated Android application
- **Connection Status** - Visual feedback for connection state

### 🗣️ **Voice Control Mode**
- **Speech Recognition** - Natural language command processing
- **Voice Commands** - Simple spoken instructions
- **Hands-free Operation** - No physical interaction required
- **Command Feedback** - Audio/visual confirmation

---

## 🛠️ Hardware Requirements

### 📋 **Bill of Materials**

| Component | Quantity | Description |
|-----------|----------|-------------|
| 🔧 **Arduino UNO Board** | 1 | Main microcontroller |
| 🔋 **L293D Motor Driver Shield** | 1 | Motor control and power management |
| 📡 **HC-05 Bluetooth Module** | 1 | Wireless communication |
| 📏 **HC-SR04 Ultrasonic Sensor** | 1 | Distance measurement and obstacle detection |
| 🔄 **SG90 Servo Motor** | 1 | Sensor rotation and scanning |
| ⚙️ **DC Gear Motors** | 4 | Wheel drive motors |
| 🛞 **Robot Wheels** | 4 | Movement and traction |
| 🔋 **18650 Li-ion Battery Holder** | 1 | Power supply housing |
| 🔋 **18650 Li-ion Batteries** | 2 | Power source (7.4V) |
| 🔌 **Jumper Wires** | Set | Connections and wiring |
| 🛡️ **Foam Board/Chassis** | 1 | Robot frame and component mounting |

### 🔧 **Tools Required**
- Soldering iron and solder
- Wire strippers
- Hot glue gun
- Screwdriver set
- Multimeter (for testing)

---

## 🏗️ Assembly Guide

### **Step 1: Chassis Preparation**
1. Cut foam board to create robot chassis
2. Mark mounting points for all components
3. Create holes for wiring and component placement

### **Step 2: Motor Installation**
1. Mount 4 DC gear motors to chassis corners
2. Attach wheels to motor shafts
3. Secure motors with hot glue or screws

### **Step 3: Electronics Assembly**
1. Mount Arduino UNO to chassis center
2. Attach L293D motor driver shield to Arduino
3. Connect motors to motor driver outputs
4. Wire power connections (7.4V from batteries)

### **Step 4: Sensor Setup**
1. Mount servo motor at front of chassis
2. Attach ultrasonic sensor to servo horn
3. Connect servo to Arduino pin 10
4. Wire ultrasonic sensor (Trig: A1, Echo: A0)

### **Step 5: Communication Module**
1. Mount Bluetooth module on chassis
2. Connect to Arduino serial pins
3. Ensure proper antenna positioning

### **Step 6: Power System**
1. Install battery holder
2. Connect power switch
3. Wire power distribution to all components

---

## ⚡ Wiring Diagram

```
Arduino UNO + L293D Shield Connections:
├── Motors (via L293D Shield)
│   ├── Motor 1 (Front Left)  → M1 terminals
│   ├── Motor 2 (Front Right) → M2 terminals  
│   ├── Motor 3 (Rear Left)   → M3 terminals
│   └── Motor 4 (Rear Right)  → M4 terminals
├── Ultrasonic Sensor
│   ├── VCC → 5V
│   ├── GND → Ground
│   ├── Trig → Pin A1
│   └── Echo → Pin A0
├── Servo Motor
│   ├── VCC → 5V
│   ├── GND → Ground
│   └── Signal → Pin 10
├── Bluetooth Module (HC-05)
│   ├── VCC → 5V
│   ├── GND → Ground
│   ├── RX → Pin 0 (TX)
│   └── TX → Pin 1 (RX)
└── Power Supply
    ├── 7.4V → VIN (Arduino)
    └── GND → Ground
```

---

## 🔧 Setup & Installation

### **1. Arduino IDE Setup**
```bash
# Install required libraries
1. Open Arduino IDE
2. Go to Sketch → Include Library → Manage Libraries
3. Install: "Servo" library
4. Install: "AFMotor" library
```

### **2. Code Upload**
1. Connect Arduino to computer via USB
2. Select correct board: `Tools → Board → Arduino UNO`
3. Select correct port: `Tools → Port → COM[X]`
4. Upload the provided code

### **3. Hardware Assembly**
- Follow the wiring diagram above
- Double-check all connections
- Ensure proper power supply connections

### **4. Testing**
```cpp
// Test each component individually:
// 1. Motor movement test
// 2. Ultrasonic sensor readings
// 3. Servo rotation test
// 4. Bluetooth connectivity test
```

---

## 🎮 Control Methods

### 🤖 **Autonomous Mode (Default)**
The robot automatically navigates and avoids obstacles:

```cpp
void Obstacle() {
    distance = ultrasonic();
    if (distance <= 12) {
        Stop();
        backward();
        delay(100);
        Stop();
        // Scan left and right for best path
        L = leftsee();
        R = rightsee();
        // Choose direction with more space
        if (L < R) right();
        else if (L > R) left();
        else forward();
    } else {
        forward(); // Clear path ahead
    }
}
```

### 📱 **Bluetooth Control Mode**
Control via smartphone app with these commands:

| Command | Action |
|---------|--------|
| `F` | Move Forward |
| `B` | Move Backward |
| `L` | Turn Left |
| `R` | Turn Right |
| `S` | Stop |

### 🎤 **Voice Control Mode**
Voice commands for hands-free operation:

| Voice Command | Action |
|---------------|--------|
| "Forward" / "^" | Move Forward |
| "Backward" / "-" | Move Backward |
| "Left" / "<" | Turn Left |
| "Right" / ">" | Turn Right |
| "Stop" / "*" | Stop Movement |

---

## 📱 Mobile App Setup

### **Bluetooth Control App**
1. Download and install the companion Android app
2. Enable Bluetooth on your smartphone
3. Open the app and go to Settings
4. Tap "Connect to Car"
5. Select your HC-05 module from the list
6. Wait for green connection indicator
7. Use directional buttons to control the robot

### **Voice Control App**
1. Install the voice control application
2. Go to Settings → Voice Commands Configuration
3. Add your preferred voice commands:
   - Forward command
   - Backward command  
   - Left/Right commands
   - Stop command
4. Test voice recognition
5. Start voice control mode

---

## 💻 Code Structure

### **Main Functions Overview**

```cpp
// Core Functions
void setup()           // Initialize all components
void loop()           // Main program loop with mode selection

// Movement Functions  
void forward()        // Move robot forward
void backward()       // Move robot backward  
void left()          // Turn robot left
void right()         // Turn robot right
void Stop()          // Stop all motors

// Control Modes
void Obstacle()       // Autonomous obstacle avoidance
void Bluetoothcontrol() // Bluetooth command processing
void voicecontrol()   // Voice command processing

// Sensor Functions
int ultrasonic()      // Get distance reading
int leftsee()        // Scan left side
int rightsee()       // Scan right side
```

### **Configuration Parameters**

```cpp
#define Echo A0        // Ultrasonic echo pin
#define Trig A1        // Ultrasonic trigger pin  
#define motor 10       // Servo motor pin
#define Speed 170      // Motor speed (0-255)
#define spoint 103     // Servo center position
```

---

## 🔊 Voice Commands

### **Command Configuration**
Configure voice commands in the mobile app:

```
Movement Commands:
├── "Move forward"    → ^
├── "Go forward"      → ^  
├── "Move back"       → -
├── "Go backward"     → -
├── "Turn left"       → <
├── "Go left"         → <
├── "Turn right"      → >
├── "Go right"        → >
├── "Stop"            → *
└── "Halt"            → *
```

### **Voice Recognition Tips**
- Speak clearly and at normal pace
- Ensure minimal background noise
- Wait for command confirmation
- Use consistent pronunciation

---

## 🚀 Usage Instructions

### **Quick Start Guide**

1. **Power On**
   - Insert charged batteries
   - Turn on power switch
   - Wait for initialization (LED indicators)

2. **Mode Selection**
   - **Autonomous**: Default mode on startup
   - **Bluetooth**: Uncomment `//Bluetoothcontrol();` in code
   - **Voice**: Uncomment `//voicecontrol();` in code

3. **Operation**
   ```cpp
   // For Autonomous Mode:
   // Simply power on - robot will start avoiding obstacles
   
   // For Bluetooth Mode:
   // 1. Connect via mobile app
   // 2. Use directional controls
   
   // For Voice Mode:  
   // 1. Connect via voice app
   // 2. Speak commands clearly
   ```

### **Troubleshooting**

| Issue | Solution |
|-------|----------|
| Robot not moving | Check battery charge and motor connections |
| No Bluetooth connection | Verify HC-05 wiring and pairing |
| Sensor not working | Check ultrasonic sensor connections |
| Servo not rotating | Verify servo power and signal connections |
| Voice commands not recognized | Check microphone permissions and app settings |

---

## 🔧 Advanced Customization

### **Speed Adjustment**
```cpp
#define Speed 170  // Adjust value (0-255)
// Lower values = slower movement
// Higher values = faster movement
```

### **Detection Distance**
```cpp
if (distance <= 12) {  // Change threshold distance
    // Obstacle detected - avoid
}
```

### **Servo Scan Range**
```cpp
int leftsee() {
    servo.write(180);  // Left scan position
    delay(800);
    // Adjust angle for scan range
}

int rightsee() {
    servo.write(20);   // Right scan position  
    delay(800);
    // Adjust angle for scan range
}
```

---

## 📊 Performance Specifications

| Parameter | Value | Notes |
|-----------|-------|-------|
| **Operating Voltage** | 7.4V | Dual 18650 batteries |
| **Current Consumption** | 800-1200mA | Varies with motor load |
| **Detection Range** | 2-400cm | Ultrasonic sensor range |
| **Movement Speed** | Adjustable | 0-255 PWM control |
| **Bluetooth Range** | 10-15m | Class 2 Bluetooth |
| **Battery Life** | 2-4 hours | Depends on usage |
| **Response Time** | <100ms | Command to action |

---

## 🛡️ Safety Guidelines

### **⚠️ Important Safety Notes**
- Always supervise robot operation
- Ensure clear operating space
- Check battery connections regularly
- Avoid water and moisture exposure
- Handle electronics components carefully

### **🔋 Battery Safety**
- Use appropriate battery charger
- Never short-circuit batteries
- Store in cool, dry place
- Check for damage before use
- Dispose of batteries properly

---

## 🤝 Contributing

We welcome contributions to improve this project! Here's how you can help:

### **Ways to Contribute**
- 🐛 **Bug Reports**: Submit detailed issue reports
- 💡 **Feature Requests**: Suggest new capabilities
- 📝 **Documentation**: Improve guides and tutorials
- 🔧 **Code Improvements**: Optimize performance and functionality
- 📱 **Mobile App**: Enhance smartphone applications

### **Contribution Process**
1. Fork the repository
2. Create a feature branch
3. Make your improvements
4. Test thoroughly
5. Submit a pull request

---

## 📚 Educational Resources

### **Learning Objectives**
- Arduino programming fundamentals
- Motor control and PWM concepts
- Sensor integration and data processing
- Wireless communication protocols
- Autonomous navigation algorithms
- Voice recognition technology

### **Recommended Reading**
- Arduino Programming Handbook
- Robotics and Automation Principles
- Bluetooth Communication Protocols
- Sensor Fusion Techniques

---

## 🏆 Project Extensions

### **Possible Enhancements**
- 📸 **Camera Integration** - Add visual navigation
- 🌐 **WiFi Control** - Internet-based remote control
- 🗺️ **Mapping** - SLAM implementation
- 🔊 **Audio Feedback** - Voice response system
- 📊 **Data Logging** - Performance monitoring
- 🎯 **Object Following** - Target tracking capability

### **Advanced Features**
- Machine learning obstacle classification
- GPS navigation integration  
- Multi-robot coordination
- Remote video streaming
- Mobile app with advanced controls

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### **MIT License Summary**
- ✅ Commercial use allowed
- ✅ Modification allowed
- ✅ Distribution allowed
- ✅ Private use allowed
- ❌ No warranty provided
- ❌ No liability accepted

---

### **Acknowledgments**
- Arduino Community for extensive library support
- Contributors to open-source robotics projects
- Educational institutions promoting STEM learning
- All beta testers and early adopters

---

<div align="center">

### **⭐ Star this repository if you found it helpful!**

**🔧 Built with Arduino • 📱 Controlled by Smartphone • 🎤 Powered by Voice**

*Happy Building! 🤖*

</div>
