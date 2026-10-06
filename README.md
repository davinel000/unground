# UNGROUND

**UNGROUND** is a kinetic typographic light installation by Slava Romanov. It uses rotating fragments of the German word **ORDNUNG** ("order") to reflect the anxious search for stable meaning inside an overwhelming news cycle.

Three modified gobo projectors cast continuously moving capsules containing 3D-printed letters. The letters repeatedly approach readable combinations without settling into a stable word. The installation was first presented at **Lichtrouten 2025** in the abandoned Forum am Sternplatz in Lüdenscheid, Germany.

Artwork page: https://www.slavaromanov.art/2025/unground

## Repository purpose

This repository is the technical and production record for UNGROUND:

- current hardware configuration and measurements;
- service and repair notes;
- the 2026 low-voltage retrofit;
- motor, cooling and power-component research;
- installation / burn-in procedures;
- spare-parts and maintenance planning.

The broader production BOM for the Aalen exhibition is kept here:
https://docs.google.com/spreadsheets/d/1ByDcBuZ3S7MSAMFwdORGYyI9jrdRuSqN4YNLZB1TsBk/edit?gid=1342182857#gid=1342182857

## Current hardware baseline

Each projection unit currently contains:

- a modified gobo projector body;
- a 12 V nominal ~50 W COB LED that has already run reliably from its existing 12 V adapter in exhibition use;
- a heatsink and active cooling;
- a rotating letter capsule / gobo carrier;
- an original slow synchronous motor (230 V AC, 3 RPM, 1.2 W) in some units;
- original mains-powered cooling fans in the legacy configuration.

The known weak point of the LED assembly is the direct solder connection to the COB pads. The retrofit should add proper strain relief and a serviceable connector close to the LED while keeping mechanical load away from the COB pads.

## 2026 retrofit direction

The current goal is to eliminate mains voltage from the internal serviceable parts of each projector and standardise the units around a common **12 V DC architecture**:

```text
external 12 V PSU
       |
     fuse
       |
  distribution
   |    |     |
  COB  FAN  MOTOR
             |
           switch
        [optional PWM]
```

The preferred first version intentionally avoids a microcontroller. The installation only needs stable continuous rotation, light and cooling. A controller should be added only if a later artistic version requires synchronisation, speed choreography, sensing or remote control.

See:

- [2026 retrofit plan](docs/retrofit-2026.md)
- [motor profile and replacement research](docs/motor-profile.md)

## Documentation status

This repository starts from measurements taken during the October 2026 service / preparation cycle. Values marked **approx.** should be rechecked with calipers before bulk ordering or CAD work.
