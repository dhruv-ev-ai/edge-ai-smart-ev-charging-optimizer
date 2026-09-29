⚡ Edge AI Smart EV Charging Optimizer

«An ESP32-based Edge AI system for intelligent, real-time EV charging control and monitoring.»

The Edge AI Smart EV Charging Optimizer is an embedded EV charging management prototype designed to perform intelligent charging decisions locally at the edge.

The system monitors voltage and current, calculates charging power, evaluates the charging condition using Edge AI decision logic, and controls the EV charging path through a relay. Relevant operating data can also be transmitted to ThingsBoard Cloud using MQTT for real-time monitoring and visualization.

---

🚗 Project Overview

The system is built around an ESP32 DevKit, which acts as the main edge controller.

The ESP32 receives charging-related inputs, processes the data locally, determines the charging state, controls the corresponding status indicators and relay, and sends selected telemetry to the ThingsBoard dashboard.

The local decision-making approach reduces dependence on continuous cloud connectivity for immediate charging-control decisions.

🔋 Charging Status

Status| Indicator| Meaning
🟢 BAY FREE| Green LED| Charging bay is available and EV charging is inactive
🟡 CHARGING| Yellow LED| EV charging is currently active
🔴 OVERLOAD| Red LED| Current/power condition has exceeded the defined limit
🔌 RELAY| Relay| Controls the EV charging load/control path

---

✨ Key Features

- ⚡ Real-time voltage monitoring
- 🔌 Real-time current monitoring
- 📊 Charging power calculation
- 🧠 Edge AI-based decision logic
- 🚗 EV charging-state management
- 🔌 Relay-based charging control
- 🟢 Green LED for Bay Free
- 🟡 Yellow LED for Charging
- 🔴 Red LED for Overload
- 📡 MQTT communication
- ☁️ ThingsBoard Cloud monitoring
- 💻 ESP32-based embedded implementation
- 🧪 Wokwi-based simulation
- 🌐 Local edge decision-making with reduced cloud dependency

---

🧩 Hardware Components

🧠 1. ESP32 DevKit

The ESP32 DevKit (38/30-pin board) is used as the main controller of the system.

Functions

- Reads voltage and current inputs
- Processes the input data
- Performs local charging decision logic
- Calculates charging power
- Controls the status LEDs
- Controls the relay
- Communicates with ThingsBoard through Wi-Fi and MQTT

---

⚡ 2. Voltage Potentiometer

The voltage potentiometer provides an analog voltage input for the EV charging simulation.

The ESP32 reads the potentiometer through an ADC input and converts the ADC value into a representative charging-voltage value.

Purpose

«Simulates changing EV charging voltage conditions during testing.»

---

🔌 3. Current Potentiometer

The second potentiometer provides an analog current input.

The ESP32 reads the ADC value and converts it into a representative charging-current value.

Purpose

«Simulates changing EV charging current conditions during testing.»

---

🟢 4. Green LED — BAY FREE

The green LED represents an available charging bay.

Green LED = BAY FREE

It indicates that:

- EV charging is inactive
- The charging load is not currently active
- The charging bay is available

---

🟡 5. Yellow LED — CHARGING

The yellow LED represents an active charging condition.

Yellow LED = CHARGING

It indicates that:

- EV charging is active
- The charging relay/control path is enabled
- The system is operating in the charging state

---

🔴 6. Red LED — OVERLOAD

The red LED represents an overload condition.

Red LED = OVERLOAD

It can be activated when the measured current or calculated power exceeds the configured limit.

The system can then take the required protection/control action through the relay logic.

---

🔌 7. Relay Module — EV Charging Control

The relay acts as the switching/control interface for the simulated EV charging load.

The ESP32 controls the relay according to the charging decision.

              ESP32
                │
                │ Control Signal
                ▼
             ┌──────┐
             │ Relay│
             └──┬───┘
                │
                │ Switching
                ▼
        EV Charging Load

«⚠️ Safety Note: In this prototype/simulation, the relay represents the control of the EV charging load. Real EV charging infrastructure requires appropriately rated contactors, protection devices, isolation, wiring, and safety systems. A hobby relay module should not be directly used to switch a high-power EV charging load.»

---

🔧 Circuit Diagram

The prototype circuit consists of:

- ESP32 DevKit
- Voltage potentiometer
- Current potentiometer
- Green LED — Bay Free
- Yellow LED — Charging
- Red LED — Overload
- Relay module — Charging control

📷 Circuit

"Edge AI Smart EV Charging Optimizer Circuit" (IMG-20260929-WA0007.jpg)

Circuit Functions

Component| Function
⚡ Voltage Potentiometer| Simulates charging voltage
🔌 Current Potentiometer| Simulates charging current
🟢 Green LED| Bay Free
🟡 Yellow LED| Charging
🔴 Red LED| Overload
🔌 Relay| EV charging load/control
🧠 ESP32| Processing and control

---

⚙️ Operating Logic

The system continuously monitors the simulated charging parameters and evaluates the charging condition.

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
             ┌────────┼────────┐
             │        │        │
             ▼        ▼        ▼
           FREE    CHARGING  OVERLOAD
             │        │        │
             ▼        ▼        ▼
          🟢 LED    🟡 LED    🔴 LED
             │        │        │
             └────────┼────────┘
                      ▼
                Control Relay
                      │
                      ▼
                Send Telemetry
                      │
                      ▼
              ThingsBoard Cloud

---

🧠 Edge AI Decision Layer

A key part of the project is the local decision-making layer.

The ESP32 receives the charging parameters and evaluates the operating condition locally.

Based on the defined decision logic, the system can determine an appropriate charging response such as:

ALLOW
THROTTLE
DEFER

Decision Flow

       Voltage + Current
                │
                ▼
        Edge AI Decision
                │
                ▼
        Charging Condition
                │
       ┌────────┼────────┐
       ▼        ▼        ▼
    ALLOW    THROTTLE   DEFER
       │        │        │
       └────────┼────────┘
                ▼
          Relay / Control

This architecture allows immediate control decisions to be made locally instead of requiring every control decision to be processed by the cloud.

---

📡 IoT Communication

The system uses Wi-Fi and MQTT to transmit relevant operating data to ThingsBoard Cloud.

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

Dashboard Monitoring

The ThingsBoard dashboard can be used to monitor:

- ⚡ Voltage
- 🔌 Current
- 📊 Power
- 🚗 Charging status
- 🧠 AI decision
- 🚨 Overload status

---

📊 Charging Power Calculation

The charging power is calculated using:

[
P = V \times I
]

Where:

- P = Charging power in watts (W)
- V = Voltage in volts (V)
- I = Current in amperes (A)

The calculated power can be used as an additional parameter for charging-state evaluation and monitoring.

---

🛠️ Technology Stack

Category| Technology
🧠 Microcontroller| ESP32 DevKit
💻 Programming| C/C++
🧪 Simulation| Wokwi
📡 Communication| MQTT
☁️ Cloud Platform| ThingsBoard
🤖 Edge Processing| Edge AI Decision Logic
🔌 Control| Relay Module
⚡ Inputs| Voltage & Current Analog Inputs
💡 Indicators| Green / Yellow / Red LEDs

---

🚀 Project Workflow

      Voltage Input ─────┐
                         │
      Current Input ─────┤
                         ▼
                      ESP32
                         │
                         ▼
                Edge AI Processing
                         │
                         ▼
                 Charging Decision
                         │
              ┌──────────┼──────────┐
              ▼          ▼          ▼
           ALLOW      THROTTLE     DEFER
              │          │          │
              └──────────┼──────────┘
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

The project can be tested in Wokwi before physical hardware deployment.

The voltage and current potentiometers can be adjusted to simulate different charging conditions. The ESP32 processes these inputs and responds through the LEDs and relay according to the configured decision logic.

Simulation Demonstrates

- Analog input acquisition
- Voltage simulation
- Current simulation
- Charging power calculation
- Charging-state detection
- Overload detection
- LED status indication
- Relay control
- ESP32 local decision-making
- MQTT telemetry transmission

---

📸 Project Dashboard

The ThingsBoard dashboard provides a visual representation of the EV charging system and its real-time operating parameters.

"ThingsBoard Dashboard" (IMG-20260929-WA0004.jpg)

---

🎯 Potential Applications

The concept can be extended to:

- 🚗 EV charging stations
- 🅿️ Smart EV charging bays
- ⚡ Charging-load management
- 🔋 Smart energy management
- 🏢 Commercial EV charging infrastructure
- 🌐 IoT-enabled charging systems
- 🔌 Multi-bay EV charging management

---

🔮 Future Improvements

- 🔋 Battery State-of-Charge (SoC) integration
- 🚗 Multi-EV charging coordination
- ⚡ Dynamic load balancing
- ☀️ Solar PV integration
- 🌱 Renewable-energy-aware charging
- 💰 Real-time electricity tariff integration
- 📈 Advanced charging prediction
- 🔌 CAN-based EV communication
- 📏 Dedicated voltage/current sensors instead of potentiometer-based simulation
- 🅿️ Multiple charging-bay management
- ☁️ Improved cloud-edge coordination

---

👨‍💻 Author

Dhruv Suthar

Electrical Engineering
Vishwakarma Government Engineering College (VGEC)

Areas of Interest

⚡ Electric Vehicles • 🔋 Battery Management • ⚙️ Electric Drives • 🔌 Power Electronics • 💻 Embedded Systems

---

⭐ Project Highlights

«Sense → Analyze → Decide → Control → Monitor»

This project demonstrates the integration of:

Embedded Systems + Edge AI + EV Charging + IoT + MQTT + Cloud Monitoring

using an ESP32-based prototype.

---

📌 Disclaimer

This project is a prototype/simulation-oriented implementation of an intelligent EV charging optimizer.

The potentiometers are used to simulate voltage and current inputs. Actual EV charging infrastructure requires appropriately rated electrical equipment, protection systems, isolation, contactors, communication interfaces, and compliance with applicable electrical and EV-charging safety standards.
