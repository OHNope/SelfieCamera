# BOM — Minimal Prototype

| Ref | Qty | Description | Value / MPN | Notes |
|---|---:|---|---|---|
| U3 | 1 | Seeed Studio XIAO ESP32-S3 Sense module | XIAO-ESP32S3-SENSE | OV3660 and microSD are internal to the module; use the official module footprint |
| U2 | 1 | CAN transceiver | MCP2562-E/SN (SOIC-8) | VDD = 5V_IN, VIO = 3.3 V, STBY tied to GND |
| J1 | 1 | 1×03, 2.54 mm header | LOGGER TRIGGER / STATUS | TRIGGER_IN_EXT, GND, STATUS_OUT |
| J3 | 1 | 1×03, 2.54 mm header | LOGGER CAN | CANH, CANL, GND |
| J4 | 1 | 1×02, 2.54 mm header | POWER IN | +5V, GND from power-management board |
| D3 | 1 | Schottky diode, SOD-123 | B5819W | Reverse-feed protection, J4 +5V → XIAO VBUS |
| C1 | 1 | Capacitor, 0603 | 100 nF | U2 VDD decoupling (5V_IN) |
| C2 | 1 | Capacitor, 0603 | 100 nF | U2 VIO decoupling (3.3 V) |
| R1 | 1 | Resistor, 0603 | 1 kΩ | Trigger series protection |
| R2 | 1 | Resistor, 0603 | 10 kΩ | Trigger pulldown |
| R3 | 1 | Resistor, 0603 | 1 kΩ | 3V3 power LED current limit |
| R4 | 1 | Resistor, 0603 | 1 kΩ | STATUS_OUT LED current limit |
| R5 | 1 | Resistor, 0603 | 120 Ω | CAN bus termination (this board is a bus endpoint) — fitted |
| D1 | 1 | Indicator LED, 0603 | PWR_3V3 | Green or other bring-up indicator colour |
| D2 | 1 | Indicator LED, 0603 | STATUS | Green/yellow or other bring-up indicator colour |
