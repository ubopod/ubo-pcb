# Ubo NFC Hat

An NFC tag board with an addressable RGB LED ring, designed to attach to the Ubo Pod over I²C.
See the [repository index](../../README.md) for the other boards.

| | |
|---|---|
| **Revision** | 1.0 (schematic title block dated 2024-09-15) |
| **Tool** | KiCad — `UboNFC.kicad_pro` |
| **Stack-up** | 2 layers (F.Cu / B.Cu) |
| **Interface** | I²C + 1-wire LED data, via a pair of 1×8 headers |

## Attribution

This design is derived from **"Badge Tag NFC" by HXR.DK**, which is still named in the KiCad
schematic title block. The Ubo adaptation keeps the upstream NFC front-end and adds the LED
chain and the pass-through header arrangement described below.

> **TODO:** confirm the upstream project URL and its license, and record both here.

## Design

| Part | Function |
|---|---|
| **NXP NT3H2x11** (NTAG I²C plus) | NFC Forum Type 2 tag with an I²C interface, password protection, and energy harvesting. Readable by a phone over NFC *and* by the host over I²C. |
| **12 × SK6812SIDE-A** | Side-firing addressable RGB LEDs, daisy-chained from `LED_IN` through to `LED_OUT`. |
| **3 × SD103AW** | Schottky diodes on the LED data / signal lines. |
| **R1–R3, C1** | Pull-ups and decoupling. |

Named nets of interest: `COIL` and `VOUT` are the NFC antenna coil and the energy-harvesting
output; `FieldDetect` signals the host when an NFC field is present; `PushButton` brings a
button input out to the headers.

## Pinout

Two 1×8 horizontal headers. **J1** is the input side and **J2** carries the same signals back out
plus `LED_OUT`, so the LED chain and the I²C bus can be continued to a downstream board.

| Pin | J1 (in) | J2 (out) |
|---:|---|---|
| 1 | +5V | LED_OUT |
| 2 | +3V3 | PushButton |
| 3 | SDA | GND |
| 4 | SCL | GND |
| 5 | LED_IN | SCL |
| 6 | GND | SDA |
| 7 | FieldDetect | +3V3 |
| 8 | PushButton | +5V |

Note that J2 is **not** a straight-through mirror of J1 — the pin order differs. Check the
orientation of any cable you build against this table.

## Status

Experimental. There are no board renders, photos, or fabrication outputs in the repo yet, and
the design has not been documented as built or tested.

> **TODO:** confirm which Ubo board or connector J1 is intended to mate with, and whether the
> `FieldDetect` and `PushButton` lines are wired to specific host GPIOs.
