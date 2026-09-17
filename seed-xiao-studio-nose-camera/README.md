# Rocket Nose Selfie Camera — Minimal Prototype Schematic

This first prototype treats the Seeed Studio XIAO ESP32-S3 Sense as a module-level part. Its OV3660 camera, microSD, USB power handling, ESP32-S3, and radio circuitry are intentionally not redrawn.

## Interfaces

| Function | Schematic net / connection |
|---|---|
| Logger trigger | J1 `TRIGGER_IN_EXT` → R1 1 kΩ → `TRIGGER_IN` → U1 D0 / GPIO1; R2 10 kΩ pulldown to GND |
| Status output | U1 D1 / GPIO2 = `STATUS_OUT`; R4 1 kΩ + D2 status LED; TP5 |
| UART debug | J2: GND, `UART_TX`, `UART_RX`, 3V3; U1 D6 / GPIO43 = TX and D7 / GPIO44 = RX |
| Prototype power | XIAO USB VBUS = `5V`; XIAO 3V3 output = `3V3`; D1/R3 power LED |
| Test points | TP1 5V, TP2 3V3, TP3 GND, TP4 TRIGGER_IN, TP5 STATUS_OUT, TP6 UART_TX, TP7 UART_RX |

J1 is a 3-pin logger header: `TRIGGER_IN_EXT`, GND, and `STATUS_OUT_RESERVED`. The reserved pin is not connected to the MCU in this revision.

## Block summary

1. **XIAO ESP32-S3 Sense** — module boundary; camera and microSD remain internal.
2. **Logger trigger input** — common-ground 3.3 V CMOS active-high input with a conservative series resistor and defined low default.
3. **Status output** — GPIO2 is exposed and drives a visible LED through R4.
4. **Power indication** — 3V3 power LED; USB 5V is the prototype source.
5. **UART debug** — 3.3 V TTL header, no level shifter or bus transceiver.
6. **Test points** — direct probing access to all bring-up nets.

## Design notes

- Prototype power is supplied through the XIAO USB 5V path. A formal flight-power interface is TBD and outside this revision.
- The logger trigger is assumed to be wired 3.3 V CMOS, active high, with a shared ground.
- Firmware is expected to latch recording on the trigger rising edge and continue recording after the trigger is deasserted.
- This revision contains no ESP-NOW, CAN, logger return channel, or UART/CAN transceiver.
- D0/D1/D6/D7 assignments are provisional recommendations and must be checked against the exact Seeed XIAO ESP32-S3 Sense hardware revision before flight use.

The schematic passed the generation ERC, static-integrity, round-trip, presentation, evidence-closure, immutable-publish, and independent sch-review gates. sch-review reports `sch2pcb_allowed=true`; update the PCB manually in KiCad when ready.
