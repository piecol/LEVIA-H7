# LEVIA H7
Open hardware STM32H743 drone flight controller designed in KiCad.
LEVIA H7 is a six-layer flight controller built around the STM32H743, developed as an open hardware platform for multirotor, fixed-wing and experimental UAV applications.
The repository includes the complete editable KiCad design files, schematics, PCB layout, 3D model, bill of materials and manufacturing files.

![Front](https://github.com/piecol/LEVIA-H7/blob/main/plots/1.png)
![Back](https://github.com/piecol/LEVIA-H7/blob/main/plots/2.png)
![Layers](https://github.com/piecol/LEVIA-H7/blob/main/plots/levia_h7_layers.png)

[!WARNING]
LEVIA H7 is currently an unvalidated hardware design.
Prototype bring-up and flight testing are still pending.
Review the design independently before manufacturing or using it in an aircraft.

![Render_F](https://github.com/piecol/LEVIA-H7/blob/main/plots/3.png)
![Render_B](https://github.com/piecol/LEVIA-H7/blob/main/plots/4.png)

## Main features

* STM32H743 high-performance microcontroller
* Six-layer PCB
* Eight motor outputs
* Dual ICM-42688-P inertial measurement units
* DPS368 barometric pressure sensor
* IST8310 magnetometer
* microSD interface for onboard logging
* Analog video interface with AT7456E-compatible OSD
* Digital VTX connector for DJI O3/O4-class systems
* CAN interface with selectable 120 Ω termination
* Dedicated RC input connector
* External I²C and SPI expansion connectors
* Two ESC connectors with current sensing and telemetry inputs
* USB-C interface with ESD protection
* Dedicated 5 V and 9 V switching regulators
* Separate 3.3 V regulators for MCU and sensor domains
* Up to 6S battery input

## Project status

The current files should be considered a pre-production engineering revision, not a flight-qualified product.

## Design overview

LEVIA H7 was designed as a general-purpose H7 flight controller rather than as a clone of an existing commercial board.

The architecture follows common flight-controller conventions where useful for firmware compatibility, including standard STM32 peripheral assignments, SDMMC, USB, motor timers and familiar ESC/VTX interfaces.

The following areas were developed independently for LEVIA H7:

* power architecture;
* component placement;
* PCB outline and mechanical design;
* power-distribution network;
* six-layer stackup implementation;
* signal routing;
* grounding strategy;
* design rules and manufacturing preparation.

Publicly available flight-controller schematics, product documentation and firmware hardware definitions were consulted as engineering references.

## Design references

LEVIA H7 is an original KiCad hardware design.

The MatekH743 ArduPilot hardware definition and publicly available flight-controller documentation were used as references for peripheral allocation, firmware compatibility and common interface conventions.

The power architecture, schematic implementation, PCB placement, mechanical design and routing were developed independently.

## Power architecture

LEVIA H7 uses separate power domains for flight-control electronics and external video equipment.

* 5V_SYS supplies the onboard 3.3 V regulators and external low-voltage peripherals.
* 3V3_MCU supplies the STM32H743 and digital logic.
* 3V3_SENS provides a separate supply for onboard sensors.
* 9V is intended for digital video transmitters.
* USB VBUS can power the system through diode OR-ing for configuration and debugging.

The input power architecture supports batteries up to 6S and includes transient-voltage suppression.

## Sensors

Inertial sensing

LEVIA H7 includes two independent ICM-42688-P IMUs connected to separate SPI buses.

The dual-IMU architecture is intended to support sensor redundancy, comparison and firmware-level failover strategies.

## Environmental sensing

The board includes:

* DPS368 barometric pressure sensor;
* IST8310 three-axis magnetometer.

Additional environmental sensing may be considered in future revisions.

## Interfaces

Motor and ESC connections

LEVIA H7 provides two ESC connectors:

* motors 1–4 with current sensing and ESC telemetry;
* motors 5–8 with an independent current input and telemetry UART.

[!CAUTION]
ESC connector pinouts are not universally standardized. Verify VBAT, GND and signal ordering before connecting an ESC.

## Video

The board supports both:

* analog video with onboard OSD;
* digital VTX systems through a dedicated 9 V connector and UART interfaces.

## Expansion

External interfaces include:

* I²C;
* SPI with two chip-select signals;
* CAN;
* UART-based RC input;
* buzzer;
* LED output;
* auxiliary ADC inputs.

The expansion connectors provide 5 V power, while their digital logic operates at 3.3 V.

## PCB

The PCB uses a six-layer stackup with dedicated ground-reference layers.

The layout was developed and documented progressively, with particular attention to:

* uninterrupted signal return paths;
* switching-regulator current loops;
* IMU power integrity;
* separation of analog and switching nodes;
* USB differential routing;
* SDMMC routing;
* motor and telemetry signal grouping.

## Repository contents
```bash
LEVIA-H7/
├── LEVIA_H7.kicad_pro       KiCad project
├── LEVIA_H7.kicad_sch       Top-level schematic
├── LEVIA_H7.kicad_pcb       PCB layout
├── LEVIA_H7.kicad_dru       Custom design rules
├── *.kicad_sch              Hierarchical schematic sheets
├── LEVIA_H7.pdf             Exported schematic
├── LEVIA_H7.step            3D board model
├── bom/                     Bill of materials
├── jlcpcb/                  JLCPCB manufacturing files
├── nextpcb/                 NextPCB manufacturing files
├── plots/                   PCB images and renders
└── LICENSE.txt              CERN-OHL-S-2.0 license
```

## Viewing the design

The project can be opened locally with KiCad 10.

The schematic and PCB can also be inspected directly in a browser through KiCanvas:

KiCanvas: https://kicanvas.org/?repo=https%3A%2F%2Fgithub.com%2Fpiecol%2FLEVIA-H7

No KiCad installation is required for browser-based inspection.

## Manufacturing

Manufacturing exports are included for convenience, but they should not be treated as production-validated files.

Before ordering:

1. review the schematic and PCB independently;
2. verify connector orientation and pin numbering;
3. confirm all selected component variants and footprints;
4. review assembly substitutions;
5. run the latest ERC and DRC;
6. verify the fabrication stackup and controlled-impedance requirements;
7. inspect Gerber and drill files with an independent viewer.

Please use GitHub Issues for review notes, potential errors and proposed improvements.

## License

LEVIA H7 hardware design files are released under the:

CERN Open Hardware Licence Version 2 — Strongly Reciprocal

See LICENSE.txt for the complete license text.

Any redistribution or modified version must comply with the conditions of CERN-OHL-S-2.0.

## Disclaimer

This project is provided without warranty.

LEVIA H7 is experimental hardware intended for engineering, educational and research use.

UAV systems can cause property damage, injury or loss of the aircraft. Anyone manufacturing, modifying or operating this design is responsible for independently validating its safety and regulatory compliance.

⸻

Designed by Pierluigi Colangeli, PhD

Hardware design · Embedded systems · Open hardware
