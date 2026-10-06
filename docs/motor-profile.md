# Motor profile and 12 V replacement research

## Legacy motor — measured / reported profile

Original motor type: slow AC synchronous motor used to rotate the internal gobo / capsule carrier.

Electrical:

- supply: **230 V AC**
- speed: **3 RPM**
- power: **1.2 W**

Mechanical measurements taken from the existing unit:

- round body diameter: **approx. 40–41 mm**
- round body thickness: **approx. 15–16 mm**, excluding the output shaft / boss
- overall width including the two mounting ears: **approx. 58.5 mm**
- mounting-hole centre-to-centre distance: **50 mm**
- mounting-hole diameter: **approx. 3 mm**
- output shaft is horizontally centred between the two ears
- output shaft centre is vertically offset toward the upper edge of the body
- shaft centre: **approx. 9–10 mm below the upper edge** of the 40–41 mm body
- output shaft length: **approx. 20 mm**
- output shaft diameter: **approx. 4 mm**

Existing aluminium drive adapter / pinion:

- overall length: **approx. 16 mm**
- gear diameter: **approx. 20 mm**
- toothed section length: **approx. 7 mm**
- lower cylindrical section: **approx. 10 mm**
- existing adapter is a tight fit on the current shaft.

These measurements are the current mechanical envelope for replacement research. Recheck with calipers before ordering four motors.

## Primary replacement candidate — 12 V / 3 RPM display gearmotor

A generic family of 12 V DC geared motors sold for rotating display stands is unusually close to the legacy geometry.

Published / drawing values found for this family:

- supply: **12 V DC**
- no-load speed: **3 RPM**
- front gearbox / mounting body diameter: **40 mm**
- mounting-hole centre distance: **50 mm**
- overall flange width: **60 mm**
- mounting-hole diameter: **about 3.5 mm**
- output shaft: nominal **4 mm flat / about 5 mm round section**
- reversible by swapping polarity
- intended use includes small display stands and slow rotating presentation objects.

This is currently the **first motor to prototype**, because the 40 mm body, 50 mm mounting centres and 3 RPM speed match the important legacy dimensions exceptionally well.

Reference listings / drawings:

- https://fyndiq.se/produkt/high-torque-12v-dc-motor-lag-varvtal-elmotor-vaxellada-3rpm-4mm-axeldiameter-mikromotor-1st-4cc7e385d31e48c5/
- https://www.motormaker.net/product/99/12v-dc-high-torque-motor-for-display-stand-electric-motor-gearbox-3-rpm-4mm-shaft-diameter-small-size-slow-speed-low-noise-reversible-easy-installation
- current eBay search example: https://www.ebay.de/itm/137234499085

### Critical fit check

The main possible mismatch is **depth**. The 12 V DC version adds a conventional DC motor behind the front gearbox and is therefore substantially deeper than the original flat AC synchronous motor. The drawing found for the 40 mm family shows an assembly depth of roughly the mid-30 mm range, while the legacy pancake body was reported at about 15–16 mm.

Before buying a full set:

1. measure available rear clearance inside one projector;
2. measure the exact vertical offset of the legacy shaft;
3. compare the candidate shaft length and profile with the aluminium pinion;
4. buy **one** candidate motor and physically test it in one projector;
5. only then order the remaining units + spare.

If the 4 mm section of the new shaft cannot accept the existing aluminium adapter directly, use a small machined / printed coupling or replace the pinion hub rather than modifying all projector mechanics.

## Secondary candidate — 50TYC 12 V / 3 RPM

A 12 V 3 RPM 50TYC brushless synchronous motor also exists.

Typical published values:

- 12 V DC
- 3 RPM
- body approx. **50 × 20 mm**
- shaft approx. **7 × 16 mm**
- mounting holes approx. **4.5 mm**
- separate small inverter / control module.

Reference:
https://www.harfington.com/de-de/products/p-1000778

It keeps the low-speed synchronous behaviour but is a poorer mechanical match: larger body, much larger shaft and additional electronics. Keep only as a fallback.

## Secondary candidate — 37 mm metal DC gearmotor

37 mm spur gearmotors are widely available at 12 V and can be configured down to roughly 1–3 RPM. They are mechanically robust and easy to control, but generally have:

- a deeper motor/gearbox assembly;
- a different mounting pattern;
- a 6 mm-class shaft on many versions.

Example families:
- https://www.gearmotordc.com/product/round-dc-gear-motor/sg37-b-gear-motor.html
- https://www.masingmotor.com/sale-52092637-rs-385-rs-395-dc-motor-with-37mm-gearbox-dc-12v-gear-motor-high-torque-brushed-gear-motor.html

Use this route only if the near-drop-in 40 mm display motor proves unreliable or does not fit.

## Current decision

Prototype the **40 mm / 50 mm mounting-centre / 12 V / 3 RPM / 4 mm shaft display gearmotor first**.

Do not design a microcontroller around the motor at this stage. With a true 3 RPM gearbox, the preferred baseline is simply:

```text
12 V -> existing motor switch -> motor
```

A small PWM speed controller can be added later if fine tuning is genuinely useful, but the mechanical reduction should provide the target speed by itself.
