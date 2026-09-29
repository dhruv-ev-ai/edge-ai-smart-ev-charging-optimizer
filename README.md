⚡ Edge AI Smart EV Charging Optimizer

«An ESP32-based Edge AI system for intelligent, real-time EV charging control and monitoring.»

The Edge AI Smart EV Charging Optimizer is an embedded EV charging management system designed to make charging decisions locally at the edge.

The system monitors voltage and current, calculates charging power, evaluates the charging condition using Edge AI decision logic, and controls the EV charging path through a relay. Real-time operating information can also be transmitted to ThingsBoard Cloud using MQTT for remote monitoring and visualization.

---

🚗 Project Overview

The system is designed around an ESP32 microcontroller that acts as the main edge controller.

Instead of depending completely on cloud-based processing, the charging decision can be performed locally on the ESP32. This enables faster response and reduces dependency on continuous cloud connectivity.

Core Decision States

Status| LED Indicator| Meaning
🟢 BAY FREE| Green LED| Charging bay is available / EV is not charging
🟡 CHARGING| Yellow LED| EV charging is currently active
🔴 OVERLOAD| Red LED| Current/power condition exceeds the defined limit
🔌 RELAY| Relay| Controls the EV charging load

---

✨ Key Features

- ⚡ Real-time voltage monitoring
- 🔋 Real-time current monitoring
- 📊 Charging power calculation
- 🧠 Edge AI-based charging decision
- 🚗 EV charging load control
- 🔌 Relay-based charging control
- 🟢 Green / 🟡 Yellow / 🔴 Red status indication
- 📡 MQTT communication
- ☁️ ThingsBoard Cloud monitoring
- 💻 ESP32-based embedded implementation
- 🧪 Wokwi simulation
- 🌐 Reduced dependency on cloud-based decision making

---

🧩 Hardware Components

🧠 1. ESP32 DevKit

ESP32 DevKit (38/30-pin board) is used as the main controller.

It is responsible for:

- Reading voltage and current inputs
- Processing sensor data
- Running the local decision logic
- Controlling LEDs
- Controlling the relay
- Communicating with the cloud through Wi-Fi/MQTT

---

⚡ 2. Voltage Potentiometer

The potentiometer is used as an analog voltage input for the EV charging simulation.

The ESP32 reads the potentiometer through an ADC input and converts the value into a representative charging voltage.

Purpose:

«Simulates changing EV charging voltage conditions.»

---

🔌 3. Current Potentiometer

The second potentiometer is used as an analog current input.

The ESP32 reads the ADC value and converts it into a representative charging current.

Purpose:

«Simulates changing EV charging current conditions.»

---

🟢 4. Green LED — BAY FREE

The green LED indicates that the charging bay is available.

Green LED = BAY FREE

It can indicate that:

- No EV is currently charging
- Charging load is inactive
- The system is ready for the next charging session

---

🟡 5. Yellow LED — CHARGING

The yellow LED indicates an active charging condition.

Yellow LED = CHARGING

It indicates that:

- EV charging is active
- The charging relay is enabled
- The system is operating under normal charging conditions

---

🔴 6. Red LED — OVERLOAD

The red LED indicates an overload or unsafe charging condition.

Red LED = OVERLOAD

It can be activated when the measured current/power exceeds the configured safe limit.

The system can then take an appropriate protection action through the relay/control logic.

---

🔌 7. Relay Module — EV Charging Control

The relay acts as the switching/control interface for the EV charging load.

The ESP32 controls the relay according to the charging decision.

Conceptually:

ESP32
  │
  │ Control Signal
  ▼
Relay
  │
  │ Switching
  ▼
EV Charging Load

«⚠️ In the simulation, the relay represents the control of the EV charging load. A real EV charging system requires appropriate contactors, protection devices, isolation, and safety-rated hardware rather than directly switching a high-power EV load with a hobby relay module.»

---

🔧 Circuit / Wiring

The circuit is implemented using the ESP32, two analog potentiometers, three status LEDs and a relay.

📷 Circuit Diagram

"Edge AI Smart EV Charging Optimizer Circuit" (IMG-20260929-WA0007.jpg)

Circuit functions:

- Voltage potentiometer → ESP32 ADC
- Current potentiometer → ESP32 ADC
- Green LED → Bay Free indication
- Yellow LED → Charging indication
- Red LED → Overload indication
- Relay → EV charging load control
- ESP32 → Main processing and control unit

---

⚙️ Operating Logic

The system continuously monitors the simulated charging parameters.

        START
          │
          ▼
   Read Voltage
          │
          ▼
    Read Current
          │
          ▼
 Calculate Power
          │
          ▼
   Edge AI Decision
          │
    ┌─────┼─────┐
    │     │     │
    ▼     ▼     ▼
  FREE  CHARGE OVERLOAD
    │     │     │
    ▼     ▼     ▼
 Green Yellow  Red
  LED    LED    LED
    │     │     │
    └─────┼─────┘
          ▼
   Control Relay
          │
          ▼
   Send Telemetry
          │
          ▼
     ThingsBoard

---

🧠 Edge AI Decision Layer

The key feature of this project is the local decision-making layer.

The ESP32 receives the charging parameters and evaluates the operating condition locally.

Depending on the input conditions, the system can determine an appropriate charging state such as:

ALLOW
THROTTLE
DEFER

This approach reduces the need to send every decision to the cloud before taking action.

Example

Voltage + Current
       │
       ▼
   Edge AI Model
       │
       ▼
 Decision Output
       │
 ┌─────┼────────┐
 ▼     ▼        ▼
ALLOW THROTTLE DEFER

---

📡 IoT Communication

After local processing, relevant operating data can be transmitted using MQTT.

ESP32
  │
  │ Wi-Fi
  ▼
 MQTT
  │
  ▼
ThingsBoard Cloud
  │
  ▼
Dashboard

The cloud dashboard can be used for monitoring parameters such as:

- ⚡ Voltage
- 🔌 Current
- 🔋 Power
- 🚗 Charging status
- 🧠 AI decision
- 🚨 Overload status

---

📊 Charging Power

The charging power is calculated from voltage and current:

[
P = V \times I
]

Where:

- P = Power in watts (W)
- V = Voltage in volts (V)
- I = Current in amperes (A)

The calculated power can be used as an additional parameter for charging-state evaluation and monitoring.

---

🛠️ Technology Stack

Category| Technology
Microcontroller| ESP32
Programming| C/C++
Simulation| Wokwi
Communication| MQTT
Cloud Platform| ThingsBoard
Edge Processing| Edge AI
Hardware Control| Relay
Inputs| Voltage & Current analog inputs
Indicators| Green / Yellow / Red LEDs

---

🚀 Project Workflow

Voltage Input ─┐
               │
Current Input ─┤
               ▼
            ESP32
               │
               ▼
        Edge AI Processing
               │
               ▼
       Charging Decision
               │
       ┌───────┼────────┐
       ▼       ▼        ▼
     ALLOW  THROTTLE   DEFER
       │       │        │
       └───────┼────────┘
               ▼
          Relay Control
               │
               ▼
        EV Charging Load
               │
               ▼
        MQTT Telemetry
               │
               ▼
       ThingsBoard Cloud

---

🧪 Simulation

The project can be tested using Wokwi before hardware deployment.

The simulation allows the charging conditions to be changed through the voltage and current potentiometers while observing the ESP32's response through the LEDs and relay.

Simulation Demonstrates

- Analog input acquisition
- Voltage/current simulation
- Charging-state detection
- Overload detection
- LED status indication
- Relay control
- ESP32 decision logic

---

📸 Project Images

ThingsBoard Dashboard

"ThingsBoard Dashboard" (IMG-20260929-WA0004.jpg)

---

🎯 Applications

The concept can be extended to:

- 🚗 EV charging stations
- 🅿️ Smart parking and charging bays
- ⚡ Charging-load management
- 🔋 Smart energy management
- 🏢 Commercial EV charging infrastructure
- 🌐 IoT-enabled charging stations

---

🔮 Future Improvements

- Multi-EV charging coordination
- Dynamic load balancing
- Battery State-of-Charge integration
- Renewable-energy-aware charging
- Solar PV integration
- Real-time electricity tariff integration
- Advanced charging prediction
- CAN-based EV communication
- Hardware current/voltage sensors instead of potentiometer simulation
- Integration with multiple charging bays

---

👨‍💻 Author

Dhruv Suthar

Electrical Engineering
Vishwakarma Government Engineering College (VGEC)

Areas of Interest:
⚡ Electric Vehicles • 🔋 Battery Management • ⚙️ Electric Drives • 🔌 Power Electronics • 🤖 Embedded Systems

---

⭐ Project Highlights

«Sense → Analyze → Decide → Control → Monitor»

The project demonstrates how an ESP32-based Edge AI system can combine embedded control, EV charging management, IoT communication and local intelligent decision-making into a single prototype.

---

📌 Note

This repository represents a prototype/simulation-oriented implementation of an intelligent EV charging optimizer. Actual EV charging infrastructure requires compliance with applicable electrical, charging, isolation, protection and safety standards.
