# Legacy mains / halogen power stages (October 2026 inspection)

## Source photographs

The October 2026 internal projector photographs show:

1. **DMS ET-D15S** halogen electronic transformer.
2. A small PCB with AC-IN connector, four discrete rectifier diodes, an electrolytic capacitor, and an opposite-side connector.

## Transformer — confirmed directly from label

- Manufacturer/marking: DMS
- Model: **ET-D15S**
- Primary: **220–240 V AC**, 50/60 Hz, 0.46 A
- Secondary: **11.5 V AC**, not 12 V DC
- Output load rating: **35–105 W**
- Marking: **FOR USE WITH 12V HALOGEN LIGHTS ONLY**
- Ambient / case temperatures on label: Ta 50°C, Tc 80°C.

This is an electronic halogen transformer, not a regulated 12 V DC power supply. Its 35 W minimum load is especially problematic if used only for the existing 12 V, 0.22 A (2.64 W) fan.

## Small PCB — inferred function

Visible components are:

- connector labelled **AC-IN**;
- four discrete diodes consistent with a full bridge rectifier;
- one electrolytic smoothing capacitor;
- DC-side connector (the exact output marking is partly obscured).

The board is therefore **probably a rectifier/filter used to feed the 12 V DC fan**, but the wire routing needs to be traced before calling this definitive.

The photo does not show an obvious 12 V voltage regulator. Output voltage, ripple, permissible current and diode rating have NOT been established.

For comparison, 11.5 V RMS sine AC rectified with a bridge plus smoothing capacitor would produce a no-load peak of roughly 15 V DC after diode losses. This numerical estimate does not establish the actual output of an electronic halogen transformer, which may produce high-frequency waveforms, need a minimum load and behave differently with a bridge/capacitor.

**Do not connect a nominal 12 V / 50 W COB to this unknown PCB.** It is not documented or verified as a regulated 12 V high-current PSU.

## Retrofit decision

With the existing 12 V DC fans retained and the 12 V 3 RPM DC motor replacements on order, the simplest reliable architecture is:

```text
230 V mains
    |
external certified regulated 12 V DC power adapter
    |
current-rated, keyed connector + appropriately rated inlet fuse
    |
12 V DC distribution
    +---- existing 12 V integrated-driver COB
    +---- existing 12 V fan (0.22 A)
    +---- original motor switch ---- new 12 V / 3 RPM geared motor
```

The DMS ET-D15S and the bridge/capacitor board are **both candidates for complete removal from the modified unit** after confirming no other parts depend on them. Removing the two boards also recovers interior volume.

Do not reuse the electronic transformer's primary mains wiring inside the redesigned 12 V projector. Any remaining mains components/circuits should be identified and isolated/removed by a suitably qualified person. Disconnect the projector from mains before opening or working on it, and respect residual charge in capacitors.

## Checks before complete removal

- Trace both wires at the rectifier board's AC-IN connector to their source.
- Confirm the DC-side connector leads only to the fan (or identify other loads).
- Trace the transformer secondary wires and identify every consumer.
- Trace old motor switch and any remaining 230 V wiring separately.
- Document original wiring before disassembly.
- Verify polarity before reconnecting the existing 12 V fan to the new external supply.
- Test the assembled projector with thermal and current measurements.

## Source of findings

Primary evidence: Slava's October 2026 photographs of the actual projector; no exact full board schematic was available.
