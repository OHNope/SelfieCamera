# Rocket Nose Selfie Camera — Remote Camera Module Schematic

This revision treats the Seeed Studio XIAO ESP32-S3 Sense stack as a purchased camera subassembly.  The Sense expansion board contains the board-to-board camera interface and its camera module; those internal DVP/SCCB signals are not redrawn on this custom carrier PCB.

## Interfaces

| Function | Schematic net / connection |
|---|---|
| Logger trigger | J1 `TRIGGER_IN_EXT` → R1 1 kΩ → `TRIGGER_IN` → U3 D0 / GPIO1; R2 10 kΩ pulldown to GND |
| Status output | U3 D1 / GPIO2 = `STATUS_OUT`; R4 1 kΩ + D2 status LED; TP5 |
| Platform CAN | U3 D4 / GPIO5 = `CAN_TX` → U2 SN65HVD230D; U2 `CAN_RX` → U3 D5 / GPIO6; J3 is the local CANH/CANL/GND service header |
| Remote camera harness | J4 pin 1 CANH, pin 2 CANL, pin 3 +5V, pin 4 GND; this is the parachute-side camera module’s connection to the rocket electrical bay |
| Prototype power | J4 +5V → U3 VBUS; U3 3V3 output → U2/C1 local 3.3V rail; D1/R3 power LED |

J1 is a 3-pin logger header: `TRIGGER_IN_EXT`, GND, and `STATUS_OUT_RESERVED`. The reserved pin is not connected to the MCU in this revision.

## Block summary

1. **XIAO ESP32-S3 Sense stack** — purchased module boundary; camera and microSD remain internal to the Sense expansion board.
2. **Logger trigger input** — common-ground 3.3 V CMOS active-high input with a conservative series resistor and defined low default.
3. **Status output** — GPIO2 is exposed and drives a visible LED through R4.
4. **Power indication** — 3V3 power LED; USB 5V is the prototype source.
5. **Platform CAN** — 3.3 V SN65HVD230D transceiver, 100 nF local decoupling, and a three-pin CANH/CANL/GND service header. R5 is a 120 Ω DNP endpoint terminator.
6. **Remote camera harness** — J4 carries CANH, CANL, +5V, and GND between the parachute-side camera module and the rocket electrical bay.

## Design notes

- J4 is the flight-facing camera harness: one twisted CAN pair plus +5V and its return. It is not a DVP/FPC cable.
- The Sense expansion board’s B2B connector and camera DVP/SCCB signals remain inside the purchased subassembly. Per Seeed’s published mapping these include XCLK (GPIO10), Y2–Y9, PCLK (GPIO13), VSYNC (GPIO38), HREF (GPIO47), and camera SCL/SDA (GPIO39/GPIO40). See [the official Sense camera guide](https://wiki.seeedstudio.com/xiao_esp32s3_camera_usage/).
- A custom FPC camera board is deliberately not invented here. It requires the final sensor/camera MPN, FPC part number and orientation, and parachute mechanical mounting; its DVP must stay on that camera board, never traverse J4.
- Prototype power may be supplied through the XIAO USB 5V path. J4 supplies the same +5V entry for the parachute-side deployment.
- The logger trigger is assumed to be wired 3.3 V CMOS, active high, with a shared ground.
- Firmware is expected to latch recording on the trigger rising edge and continue recording after the trigger is deasserted.
- J1 remains a local logger trigger/status prototype header. Communication with the ログ解放基盤 is CAN through J3/J4.
- Populate R5 only when this unit is at a physical CAN-bus endpoint. Select the final connector family, cable, and bus bitrate with the platform integration owner.
- D0/D1/D4/D5/D6/D7 assignments are provisional recommendations and must be checked against the exact Seeed XIAO ESP32-S3 Sense hardware revision before flight use.

The new J4 harness and corrected local 3.3V connection have a clean connectivity contract.  The staged workflow’s final static-integrity gate remains blocked by 72 pre-existing off-grid objects in the legacy CAN drawing; they are not new J4 or camera-harness findings and have not been waived.
