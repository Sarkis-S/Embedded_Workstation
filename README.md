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

Absolutely. This is worth documenting because the **mistakes and revisions are arguably more valuable than the finished little power interface**.

I would add a section to the README called something like **“Perfboard Design & Lessons Learned”**. It could read:

```markdown
## Perfboard Design & Lessons Learned

The Workbench Power Interface started as a simple KiCad schematic and PCB layout, but adapting the design to a real 20 × 80 mm perfboard introduced a number of physical constraints that were not obvious during the initial electrical design.

### Designing for the Physical Perfboard

The available perfboard has:

- 20 × 80 mm physical dimensions
- 6 × 28 holes
- 2.54 mm hole pitch
- Isolated plated pads
- Four small M2 mounting holes

The original PCB layout was electrically correct, but it did not accurately represent the physical perfboard. This required revisiting the layout from a mechanical perspective.

A custom KiCad footprint was created to model the perfboard and provide a realistic placement reference.

### Building the Custom Perfboard Footprint

The footprint was designed around the actual 2.54 mm hole spacing.

Because the board contains an even number of rows and columns, its geometric center falls between holes rather than on a hole. The hole array therefore had to be positioned carefully relative to the 80 × 20 mm board outline.

The first version represented the perfboard holes as graphical circles. They were later changed to through-hole pads to more closely resemble the plated pads of the real perfboard.

This looked much more realistic and was useful for verifying component placement. However, it also introduced an important problem: KiCad treated the perfboard holes as real electrical pads.

When component pads were placed over the perfboard pads, the overlapping electrical geometry interfered with routing and connectivity.

This demonstrated an important distinction:

> A useful mechanical representation does not necessarily need to be an electrical representation.

The perfboard footprint will therefore be revised so that the hole pattern acts only as a visual and mechanical placement reference.

### Grid Alignment

The custom perfboard also demonstrated the importance of working with the physical manufacturing grid.

The perfboard uses standard 2.54 mm (0.1 inch) spacing. Setting the KiCad PCB grid to 2.54 mm allowed component footprints to align naturally with the physical hole pattern.

Several selected components are especially compatible with this spacing:

- 2.54 mm pin headers occupy adjacent perfboard holes.
- 5.08 mm terminal blocks span two perfboard pitches.
- The 10.16 mm resistor footprint spans four perfboard pitches.

Once the component layout was aligned to the 2.54 mm grid, the perfboard footprint was no longer required to determine component positions.

### PCB Routing vs. Perfboard Wiring

Another major change was how the connections were represented.

A conventional PCB can route copper traces freely around the board. The actual perfboard, however, uses isolated pads and must be connected manually using component leads, solder bridges, bus wire, or insulated hookup wire.

The layout was therefore revised to better represent how the board will actually be constructed.

Instead of using convenient diagonal PCB traces, the wiring was organized primarily as straight horizontal and vertical runs.

The KiCad routing is therefore being used as a **physical wiring plan**, rather than as artwork for manufactured copper traces.

### Key Lessons

This project demonstrated that passing electrical checks does not automatically make a design physically buildable.

Some of the lessons learned during the process were:

- Start with the dimensions and constraints of the real substrate.
- Electrical design and mechanical design must be considered together.
- Component lead pitch matters when designing for perfboard.
- A 2.54 mm grid provides a direct relationship between KiCad placement and real perfboard holes.
- Through-hole pads and graphical reference holes serve different purposes in KiCad.
- `Edge.Cuts` represents actual board geometry and should not be used merely as decorative artwork inside another PCB.
- Perfboard wiring must account for real wire paths, solder access, conductor size, and current.
- Empty perfboard space can intentionally remain available for future revisions.
- A clean schematic and DRC are only part of validating a physical design.

The biggest lesson was that the design process did not end when the schematic and PCB layout were complete. Inspecting the real hardware exposed new constraints, which required the digital model to be revised.

That iteration is now part of the workstation design process:

Requirements → Schematic → Layout → Physical Inspection → Revision → Build → Test
```