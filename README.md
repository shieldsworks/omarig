# Omarig

Open sensor hardware and firmware for [Omahoy](https://github.com/shieldsworks/omahoy).

**Status: planned.** Nothing to install yet. The first node will be a compass,
because the rest of Omahoy has no heading: see
[docs/compass-node.md](docs/compass-node.md) for its parts.

## What it will do

- Put ESP32 sensor nodes around the boat: pressure, temperature, humidity
  (BME280), temperature probes (DS18B20), and a bilge float switch.
- Run Rust firmware (esp-hal) that reports to
  [omakeel](https://github.com/shieldsworks/omakeel) over the boat's Wi-Fi.
- Include enclosures and circuit boards built for salt air.

## License

MIT
