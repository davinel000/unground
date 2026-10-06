# 2026 low-voltage retrofit

## Goal

Rebuild each UNGROUND projector as a simple, repeatable and serviceable 12 V unit for long exhibition operation.

The retrofit should eliminate the remaining 230 V motor load from inside the projector. The existing cooling fans are already 12 V DC, so they can stay if they pass service checks. Mains voltage should ideally stop at the external certified power adapter.

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
   |---------------- existing 12 V fan
   |
   +-- original switch -- [optional PWM] -- 12 V geared motor
```

No microcontroller is required for the baseline version.

## Power supply

Working planning value: **12 V / 8 A (96 W) external adapter per projector**.

Reasoning:

- nominal COB label: about 50 W -> about 4.2 A at 12 V if it actually draws the full nominal power;
- existing fan: **12 V, 0.22 A = 2.64 W**;
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

A panel-mount XT30/XT60-class connector is one practical direction, with the final size chosen after measuring actual current.

For the main 12 V feed and COB branch, start with flexible stranded wire around **0.75–1.0 mm²**, then verify against actual current, cable length and connector rating. Fan and motor branches can use smaller wire once their measured currents are known.

Place the fuse close to the projector power inlet.

## COB LED

Current state:

- nominal 12 V ~50 W COB;
- has already operated reliably directly from the existing 12 V adapter;
- mechanically attached to the heatsink with bolts and thermal paste;
- solder pads are the weak service point: wires can detach;
- current LED assembly is not designed for fast service / hot swap.

### Ordered replacements / spares

On **2026-10-07**, six COB modules were ordered from AliExpress:

https://de.aliexpress.com/item/1005007557573698.html

Listing family: **DC12V / 32V 50W COB LED with integrated Smart-IC driver**.

The order is intended to provide replacements and spares for UNGROUND. On arrival, confirm the exact selected variant before standardising all projectors:

- **12 V / 50 W** version;
- chosen colour temperature / light colour;
- footprint and mounting-hole geometry;
- brightness compared with the current proven COBs;
- thermal behaviour on the existing heatsink;
- contact-pad geometry and solderability;
- actual current draw at 12 V.

Retrofit rule:

**The main harness must never mechanically pull on the COB electrical contacts.**

### Preferred connection for the ordered COBs

Keep the existing bolted thermal mounting:

```text
COB
  |
thermal paste
  |
existing heatsink
```

For power:

```text
COB + / - pads
  |
short flexible silicone-wire tails
  |
mechanical cable clamp / strain relief fixed to heatsink or nearby structure
  |
2-pin service connector
  |
projector harness
```

The strain-relief clamp should be close enough to the COB that the solder joint never flexes when the harness is moved.

A future 3D-printed part can be very small: it only needs to clamp the two short wires to a fixed part of the heatsink / projector. It should not carry the COB-to-heatsink clamping force.

**Do not use crocodile clips for permanent exhibition operation.** They remain useful only for bench testing.

## Cooling

Existing fan specification identified during the October 2026 service:

- format: **6010**
- dimensions: **60 × 60 × 10 mm**
- supply: **12 V DC**
- current: **0.22 A**
- power: **about 2.64 W**
- impeller: about 11 blades

This is a standard size and electrical class. A current commercial equivalent is the TITAN TFD-6010HH12B (60 × 60 × 10 mm, 12 V, 0.22 A, double ball bearing).

The existing fans therefore **do not need a voltage conversion**. Keep them if they run smoothly and move enough air.

Before final installation:

- check bearing noise / vibration;
- note airflow direction;
- verify connector and polarity;
- clean dust;
- run together with the COB for a long thermal test.

For spares, prefer a 60 × 60 × 10 mm 12 V fan with ball / high-lifetime bearing and airflow comparable to the original rather than choosing only by current draw.

The fan should run at full speed whenever the COB is powered.

## Motor

See [motor-profile.md](motor-profile.md).

Four generic **12 V DC / 3 RPM / ~4 mm shaft gearmotors** were ordered from Amazon.de on 2026-10-06:

https://www.amazon.de/Gleichstrommotor-Langsamer-Elektromotor-Wellendurchmesser-Mikromotor/dp/B07ZP52PGK

On arrival verify:

- shaft length against the legacy approx. 19–20 mm shaft;
- body depth and available rear clearance;
- mounting / adapter fit;
- fit of the existing aluminium pinion;
- rotation direction;
- noise and long-run behaviour.

The motor shaft / aluminium pinion already appear to have screw-locking features, which may make adaptation easier than a pure press-fit connection.

If the motor fits mechanically, motor control can remain extremely simple:

```text
12 V -> existing projector switch -> motor
```

## First-unit prototype sequence

1. Photograph the untouched internal wiring and mechanics.
2. Measure the remaining motor geometry with calipers.
3. Measure one complete projector's COB current at steady state.
4. Check rear clearance for the ordered 12 V DC motor.
5. Fit one ordered motor and reuse / adapt the existing aluminium pinion.
6. Service and retain one existing 12 V fan.
7. Fit one of the newly ordered COBs to the existing heatsink.
8. Add short silicone-wire tails + strain relief + a 2-pin service connector.
9. Build a fused 12 V distribution harness.
10. Run a long burn-in test before duplicating the retrofit across the remaining projectors.
11. Standardise connectors, polarity and cable labels on all units.
12. Keep the remaining ordered COBs as matched spares / replacements.

## Open measurements

Still to record:

- real COB current / total projector current;
- exact motor shaft vertical offset;
- exact available motor depth inside the projector;
- existing aluminium pinion bore / screw-lock profile;
- fan connector / pinout and airflow direction;
- preferred panel connector and fuse value after current measurement;
- exact ordered COB colour variant and mounting geometry after delivery.
