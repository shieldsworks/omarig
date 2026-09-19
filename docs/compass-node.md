# The compass node: parts

The first omarig node. It measures which way the boat is pointing and how fast
it is turning, and it is what [omahelm](https://github.com/shieldsworks/omahelm)
needs for a heading-up chart, what
[omalookout](https://github.com/shieldsworks/omalookout) needs for bearings from
the bow, and what [omatiller](https://github.com/shieldsworks/omatiller) needs
before it can steer anything.

Nothing here is bought yet. Prices are what the shops listed on 2026-09-19, in
US dollars, before shipping and tax.

## Stage 1: the bench

Enough to sit at a table, spin the sensor, and see a heading. No soldering:
both boards have the same solderless I²C connector, and the cable joins them.

| Part | What it is | Price |
|---|---|---|
| [Adafruit ICM-20948 9-DoF IMU, #4554](https://www.adafruit.com/product/4554) | The sensor: gyro, accelerometer, magnetometer. pypilot's recommended chip, so its calibration work is worth reading against ours. STEMMA QT. In stock. | $19.95 |
| [Adafruit ESP32-S3 Feather, 8 MB flash, #5323](https://www.adafruit.com/product/5323) | The computer: runs our Rust firmware, talks Wi-Fi, USB-C for power and programming, battery connector for later. STEMMA QT. In stock. | $17.50 |
| [STEMMA QT cable, 100 mm, #4210](https://www.adafruit.com/product/4210) × 2 | Joins the two. A spare, because it's a dollar. | $1.90 |

**About $39**, plus a USB-C cable you probably have.

### Alternatives worth knowing

- [SparkFun ICM-20948, Qwiic](https://www.sparkfun.com/products/15335), $21.95 —
  the same chip, same connector, slightly dearer.
- **OpenMarine's ICM-20948 module, €10** — pypilot's own, the cheapest of the
  three, but shipping from Europe.
- [Adafruit BNO085, #4754](https://www.adafruit.com/product/4754), $29.50 — the
  same nine sensors, but it fuses them on its own chip and hands over a
  finished orientation. Not the plan, because the fusion is the interesting
  part and we want it in our own Rust. Worth $30 later as a second opinion:
  when our heading and its heading disagree, one of them is wrong, and it's
  useful to know which. [cypilot](https://github.com/jft7/cypilot) switched to
  this chip for exactly that reason.
- The smaller [QT Py ESP32-S3, #5426](https://www.adafruit.com/product/5426) is
  $12.50 and fits a smaller box, but has no battery connector and only six were
  in stock.

## Stage 2: aboard

Only after the bench work says the heading is good. Prices are rougher here,
and the enclosure isn't chosen yet.

| Part | What it is | Price |
|---|---|---|
| [Pololu D24V10F5](https://www.pololu.com/product/2831) | 5 V from the boat's 12 V: 5.1–36 V in, 1 A out, so it copes with a battery sagging under the windlass. | $12.95 |
| Waterproof enclosure, about 120 × 80 × 55 mm | IP65 or better, with a flat floor to bolt the boards to. | ~$20, not chosen |
| Cable gland, M12 | Where the wire enters the box. | ~$3 |
| Inline fuse holder and a 1 A fuse | At the battery end of the run, not at the box. | ~$8 |
| Tinned marine wire, 18 AWG, two-core | The run from the panel. Length depends on where the box goes. | ~$1/ft |
| 316 stainless screws, and a backing plate or big washers | It has to stay put and keep its orientation. | ~$10 |

**About $55**, plus wire.

## Where it goes

- **Low, near the centerline**, where the boat's motion is least.
- **At least 750 mm from the ram's motor.** Raymarine's own handbook keeps
  their pilots that far from a steering compass, and their compass is inside
  the pilot; ours has no excuse to be closer.
- **Away from steel, engine, batteries, speakers and any cable carrying real
  current.** A wire that only carries current sometimes is worse than one that
  always does, because the error comes and goes.
- **Bolted, in a fixed orientation**, and noted which way it faces. Every
  heading afterwards is relative to how it was mounted. This is why it doesn't
  go on a clip or a ball mount.

## What this doesn't cover

- **The wired link to omatiller.** When there's a pilot to talk to, the
  steering path wants a wire rather than Wi-Fi, which means a transceiver at
  each end. Nothing to buy until omatiller's controller exists.
- **A board of our own.** These are dev boards: they work, but a node that
  lives on a boat eventually wants a single conformally coated board with the
  connectors it actually needs. That is omarig's real job, and it comes after
  the firmware proves what the node has to do.
- **The other omarig nodes** — pressure, temperature, bilge float. Separate
  boxes, later.
