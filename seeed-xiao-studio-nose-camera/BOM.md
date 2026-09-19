# BOM — Minimal Prototype

| Ref | Qty | Description | Value / MPN | Notes |
|---|---:|---|---|---|
| U1 | 1 | Seeed Studio XIAO ESP32-S3 Sense module | XIAO-ESP32S3-SENSE | OV3660 and microSD are internal to the module; use the official module footprint |
| J1 | 1 | 1×03, 2.54 mm header | LOGGER TRIGGER / STATUS | TRIGGER_IN_EXT, GND, STATUS_OUT_RESERVED |
| J2 | 1 | 1×04, 2.54 mm header | UART DEBUG (3V3 TTL) | GND, UART_TX, UART_RX, 3V3 |
| R1 | 1 | Resistor | 1 kΩ | Trigger series protection |
| R2 | 1 | Resistor | 10 kΩ | Trigger pulldown |
| R3 | 1 | Resistor | 1 kΩ | 3V3 power LED current limit |
| R4 | 1 | Resistor | 1 kΩ | STATUS_OUT LED current limit |
| D1 | 1 | Indicator LED | PWR_3V3 | Green or other bring-up indicator colour |
| D2 | 1 | Indicator LED | STATUS | Green/yellow or other bring-up indicator colour |
| TP1–TP7 | 7 | Test pads | 5V, 3V3, GND, TRIGGER_IN, STATUS_OUT, UART_TX, UART_RX | Probe access; use the assigned KiCad test-pad footprint |

No separate OV3660, microSD, ESP-NOW, CAN, flight-power, or transceiver parts are included in this module-level prototype.
