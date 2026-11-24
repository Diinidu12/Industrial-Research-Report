# Industrial-Research-Report

## Copper Guard & Smart Power Monitoring System (SPMS)

Embedded hardware and firmware developed during an industrial research internship at **Sri Lanka Telecom's Digital Lab**, addressing real-time copper line theft/damage detection and MSAN power monitoring across SLT's telecommunications infrastructure.

### Overview

This project covers two interconnected IoT devices:

- **Copper Guard** — Detects copper telecom line disconnection (theft/damage) and sends real-time SMS alerts via GSM.
- **Smart Power Monitoring System (SPMS)** — Monitors 230V power presence at field-deployed MSAN equipment and streams telemetry to a cloud dashboard.

### Copper Guard
<img width="1280" height="960" alt="device" src="https://github.com/user-attachments/assets/62542ed0-5038-48a7-a29f-53834a2ad9a7" />

- **MCU:** ESP-12F (ESP8266)
- **GSM Module:** SIM800C (SMS alerts on line disconnection)
- **Display:** 0.96" I2C OLED for on-site status
- **Isolation:** PC817 optocoupler-based input circuit (48V line sensing)
- **Power Supply:** MP1584EN buck converter (replacing an LM7805 that failed under GSM transmission load) + AMS1117 3.3V regulation
- **Minimized Variant:** STM8S103F3P6-based version for reduced size/cost, using an external GSM module

Key fixes included correcting ESP-12F boot mode pin configuration and adding a boot-delay capacitor on the EN pin to prevent resets caused by SIM800C inrush current.

### Smart Power Monitoring System (SPMS)
<img width="1000" height="750" alt="11" src="https://github.com/user-attachments/assets/18935dc3-7a80-4716-b14b-d7008ebf5b42" />


- **MCU:** ESP32-S (4G IoT board)
- **Modem:** A7680C (LTE)
- **Isolation:** Optocoupler-based sensing across up to 8 × 230V AC lines, with a step-down transformer for voltage measurement
- **Cloud Platform:** [ThingsBoard](https://thingsboard.io/) via HTTP POST (JSON telemetry payload)
- **Firmware:** Migrated from MQTT to HTTP POST for improved reliability on intermittent cellular connections; added exponential backoff and multi-step fault recovery

Also included diagnosis, repair, and firmware upgrades of field-deployed SPMS units, including burnt chips, GSM antenna faults, and SIM incompatibility issues.

### Tools & Technologies

| Category | Tools / Technologies |
|---|---|
| Microcontrollers | ESP-12F, ESP32-S, ESP-01S, STM8S103F3P6 |
| GSM/LTE | SIM800C, A7680C |
| PCB Design | EasyEDA |
| Circuit Simulation | Proteus |
| Firmware | Arduino IDE |
| IoT Platform | ThingsBoard |
