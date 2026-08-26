# Emiuet Validation Instructions

This repository validates Emiuet subsystems before Rev.B integration.

## Product boundary

- Emiuet is a self-contained MIDI instrument with its own battery, charging,
  power-path, and required rails.
- Do not make Hearth or EUB-BUS a requirement for normal Emiuet operation.
- Hearth may only be an optional comparison or protected bench source.
- A test powered by Hearth cannot pass an Emiuet internal-power gate.

## Working rules

- Keep each board focused on one diagnosable subsystem.
- Define test points and pass criteria before PCB layout.
- Record observations separately from hypotheses.
- Do not integrate a circuit into INT-01 until its single-function gate passes.
- Do not start Rev.B from INT-01 until all required integration gates pass.
- Preserve Emiuet's guitar-oriented musical constraints and pin assignment.
