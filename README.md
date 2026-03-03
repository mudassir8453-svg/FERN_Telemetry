<img width="1916" height="877" alt="image" src="https://github.com/user-attachments/assets/d97f8b21-a576-4368-be9c-4018df076aa2" />
🏎️⚡ FERN EV Powertrain Telemetry System | Engineering Showcase
A high-performance, real-time CAN bus telemetry and data acquisition system designed for the FERN Formula Student Electric Vehicle. > ⚠️ Portfolio Notice: This repository serves as a technical showcase and portfolio piece. The ESP32 firmware (.ino) is uniquely hardcoded to parse the specific CAN bus matrices of our vehicle's Cascadia Motion Controller and Orion BMS. It is not intended as a plug-and-play library, but rather as a demonstration of embedded systems programming, IoT architecture, and full-stack telemetry design.

🎯 Project Overview
As the Powertrain Lead, I developed this system to bridge the gap between the vehicle's core electrical components and the pit wall. The objective was to create a zero-latency, secure, and highly reliable data pipeline that allows engineers to monitor critical EV metrics in real-time and log them for post-session analysis.

🧠 Core Engineering Achievements
RTOS Dual-Core Processing: Utilized the ESP32's dual-core architecture to prevent data bottlenecks. Core 0 is strictly dedicated to polling the CAN Bus (TWAI) at 500kbps to ensure zero dropped frames, while Core 1 handles WiFi handling, MQTT publishing, and I2C OLED rendering.

Custom CAN Parsing: Engineered custom Little-Endian and Big-Endian bit-shifting logic to decode raw CAN frames from the Motor Controller and BMS into human-readable floats and integers.

Secure IoT Architecture: Implemented an isolated Read/Write MQTT architecture via HiveMQ Cloud. The vehicle uses hidden credentials to publish data, while the public-facing dashboard utilizes a strict "Subscribe-Only" role, completely neutralizing command-injection vulnerabilities.

In-Car Hardware Multiplexing: Overcame the ESP32's hardware limitations by utilizing a TCA9548A I2C multiplexer to drive up to 8 separate OLED displays simultaneously for the driver's local dashboard.

🏗️ System Architecture
1. Hardware Layer (In-Car)
Microcontroller: ESP32 NodeMCU

CAN Transceiver: SN65HVD230 (3.3V) via ESP-IDF TWAI driver.

Data Sources:

Cascadia Motor Controller: RPM, Phase Current, Bus Voltage, Commanded/Actual Torque, Inverter Module & Motor Temps.

Orion BMS: Pack Voltage, Pack Current, SOC, Cell Imbalance (High/Low IDs), and Pack Temperature.

2. Communication Layer
Protocol: MQTT over WSS (Secure WebSockets).

Payload Optimization: Instead of heavy JSON, data is packed into a lightweight, comma-separated string (/*val1,val2...*/) to minimize bandwidth and maximize the update frequency (10Hz+).

3. Presentation Layer (Pit Wall)
Framework: Pure HTML5, CSS3, Vanilla JavaScript (No heavy frameworks required).

Data Visualization: Utilized Chart.js for plotting Phase Amps & Torque Maps, and canvas-gauges for a highly responsive, zero-lag motor tachometer.

Local Data Logging: Engineered a browser-side caching system that allows race engineers to record live data streams and instantly export them as formatted .csv files for MATLAB or Python analysis.

📊 The Live Dashboard
The web dashboard decodes the telemetry string in real-time, calculating live metrics such as Cell Voltage Delta (imbalance) on the fly, and displaying 18 unique data points.

Key Dashboard Features:

Interactive Tachometer: Live Motor RPM with redline scaling.

Dynamic Charts: Dual-line Torque Map (Commanded vs. Actual) and DC Bus Current.

Battery Grid: Pack Voltage, high-precision SOC, Min/Max Cell data (with dynamic ID tracking), and BMS Temperature.

Thermal Grid: Motor Temp, Coolant Temp, Hot Spot Temp, and individual Inverter IGBT Module temperatures.

🛠️ Technical Skills Demonstrated
Languages: C++, JavaScript, HTML/CSS.

Protocols: CAN Bus 2.0B, I2C, MQTT, WebSockets.

Hardware: ESP32, Embedded Systems, Multi-display rendering.

Concepts: Real-Time Operating Systems (FreeRTOS), Data Acquisition (DAQ), Bitwise Operations, Cybersecurity (Role-Based Access Control).

Designed and engineered for FERN Racing.
