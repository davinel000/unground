# 2026 low-voltage retrofit

## Goal

Rebuild each UNGROUND projector as a simple, repeatable and serviceable 12 V unit for long exhibition operation.

The retrofit should remove the remaining 230 V motor and fan loads from inside the projector. Mains voltage should ideally stop at the external certified power adapter.

## Proposed architecture

```text
230 V AC
   |
external certified 12 V PSU
   |
panel connector rated >= 10 A
   |
local fuse
   |
12 V distribution
   |---------------- COB LED
   |---------------- 12 V fan
   |
   +-- original switch -- [optional PWM] -- 12 V geared motor
```

No microcontroller is required for the baseline version.

## Power supply

Working planning value: **12 V / 8 A (96 W) external adapter per projector**.

Reasoning:

- nominal COB label: about 50 W -> about 4.2 A at 12 V if it actually draws the full nominal power;
- fan: expected to be a small fraction of an amp;
- slow geared motor: expected to be a small fraction of an amp in normal operation, with a higher startup / stall current;
- an 8 A supply leaves useful thermal and transient headroom.

The actual COB current should still be measured on one finished projector before locking the final PSU model. The existing 12 V COB + adapter combination has already been proven in exhibition use, so the retrofit should preserve that successful operating condition where practical.

## Input connector and main wiring

Avoid a generic low-current 5.5 mm barrel jack for the final 8 A design unless its exact rating is known to be sufficient.

Preferred characteristics:

- panel-mounted, keyed / polarity-safe connector;
- continuous current rating of at least **10 A**;
- mechanical retention;
- easy replacement during installation.

A panel-mount XT60-family connector is one practical option.

For the main 12 V feed and COB branch, start with flexible stranded wire around **0.75–1.0 mm²**, then verify against actual current, cable length and connector rating. Fan and motor branches can use smaller wire once their measured currents are known.

Place the fuse close to the projector power inlet.

## COB LED

Current state:

- nominal 12 V ~50 W COB;
- has already operated reliably directly from the existing 12 V adapter;
- mechanically attached to the heatsink with bolts and thermal paste;
- solder pads are the weak service point: wires can detach.

Retrofit rule:

**The main harness must never mechanically pull on the COB solder pads.**

Preferred assembly:

```text
COB pads
  |
short flexible silicone-wire tails
  |
mechanical strain relief fixed to the LED/heatsink structure
  |
service connector
  |
projector harness
```

A future 3D-printed frame can hold strain relief or spring contacts, but the LED-to-heatsink clamping force should continue to be carried by metal fasteners, not by a heat-softening printed part.

## Cooling

The legacy 230 V fans should be replaced with 12 V brushless fans.

Before ordering:

- measure fan frame dimensions;
- measure mounting-hole spacing;
- note airflow direction;
- record current / power from the label;
- check available thickness and connector route.

The fan should normally run at full speed whenever the COB is powered. Do not add speed control unless noise proves to be a real installation problem.

## Motor

See [motor-profile.md](motor-profile.md).

Current preferred prototype: generic **12 V DC, 3 RPM, 40 mm display-stand gearmotor with 50 mm mounting centres and ~4 mm shaft**.

If it fits mechanically, motor control can remain extremely simple:

```text
12 V -> existing projector switch -> motor
```

## First-unit prototype sequence

1. Photograph the untouched internal wiring and mechanics.
2. Measure the old motor and fan with calipers.
3. Measure one complete projector's COB current at steady state.
4. Check rear clearance for the deeper 12 V DC motor candidate.
5. Fit one 12 V motor and reuse / adapt the existing aluminium pinion.
6. Replace one fan with a matched 12 V fan.
7. Build a fused 12 V distribution harness with strain relief.
8. Run a long burn-in test before duplicating the retrofit across the remaining projectors.
9. Standardise connectors, polarity and cable labels on all units.
10. Prepare at least one pre-wired spare motor/fan/wiring module for exhibition service.

## Open measurements

Still to record:

- exact fan dimensions and current;
- real COB current / total projector current;
- exact motor shaft vertical offset;
- exact available motor depth inside the projector;
- existing aluminium pinion bore profile;
- preferred panel connector and fuse value after current measurement.
