# Embedded Workstation

A compact modular workstation for embedded systems development,
electronics prototyping, hardware testing, and PCB development.

## Current Revision

Rev A is the original acrylic workstation assembled as a practical
development platform rather than from a predefined mechanical design.

Current hardware includes:

- Arduino Uno
- ESP32 development platform
- Solderless breadboards
- Logic analyzer
- External bench power supply support
- Removable prototyping modules
- Two-level acrylic construction for equipment and cable management

## Design Goals

- Keep common embedded-development hardware readily accessible
- Provide a clean breadboarding and experimentation area
- Support both MCU-powered logic and externally powered loads
- Allow instrumentation such as a multimeter and logic analyzer to
  connect easily
- Remain modular so individual sections can be upgraded independently

## Development

The original workstation was designed and assembled iteratively.
Future modifications are being documented here as formal hardware
revisions.

Planned development includes:

- Workbench power interface
- Improved external power distribution
- Modular perfboard hardware
- Additional test points and connectors
- Future workstation revisions

### Workbench Power Interface

A custom perfboard-based external power distribution interface designed in KiCad for the workstation. The project includes physical perfboard modeling, component placement, realistic wiring planning, and documented design iterations.

See `hardware/workbench_power_interface/README.md` for the full design and lessons learned.
