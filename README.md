# Ubo PCBs

Open hardware design files for the printed circuit boards used in the [Ubo Pod](https://getubo.com)
and its accessories — the main Raspberry Pi HAT, the side connector board, PCIe/M.2 adapters, a
flex cable, and an NFC board. Sources are a mix of **Eagle CAD** and **KiCad**; newer designs are
KiCad. Everything here is licensed under [GPL-3.0](LICENSE).

## Boards

Each board lives in its own directory under [`boards/`](boards/) with its own README.

| Board | Rev | Tool | Status | Connects to |
|---|---|---|---|---|
| [**ubo-top-hat**](boards/ubo-top-hat/) | v1.6 | Eagle | Production | Raspberry Pi 40-pin header |
| [**ubo-sideboard**](boards/ubo-sideboard/) | v1.5.2 | KiCad | Current | Pi 4/5 side ports + top HAT |
| ↳ [v1.4](boards/ubo-sideboard/v1.4-eagle/) | v1.4 | Eagle | Superseded by v1.5.2 | — |
| [**ubo-hab-v2**](boards/ubo-hab-v2/) | v4 | KiCad | Current | Raspberry Pi 5 PCIe + power |
| [**ubo-pcie-adapter**](boards/ubo-pcie-adapter/) | v3 | KiCad | Superseded by HAB v2 | Raspberry Pi 5 PCIe |
| [**m2-mkey-to-aekey**](boards/m2-mkey-to-aekey/) | — | KiCad | Built and tested | M.2 M-key slot |
| [**pcie-fpc-s-shaped**](boards/pcie-fpc-s-shaped/) | v2 | KiCad | Prototype, revision in progress | PCIe adapter FPC connectors |
| [**ubo-nfc-hat**](boards/ubo-nfc-hat/) | 1.0 | KiCad | Experimental | I²C via 1×8 headers |

**What each one is:**

- **ubo-top-hat** — the main Ubo board. LCD, keypad, RGB LED ring, WM8960 audio with speakers and
  microphones, IR transmit/receive, temperature and light sensors, EEPROM, fan, power button, and
  an experimental SDR section.
- **ubo-sideboard** — brings the Pi's mini HDMI, USB-C power, and audio jack around to the back of
  the enclosure, and adds a microSD extender, STEMMA Qt connectors, a power button, and a fan header.
- **ubo-hab-v2** — "hardware added on the bottom." PCIe to M.2 M-key, with optional USB-C PD and
  PoE+ power input modules and 12V/5V/3.3V breakouts.
- **ubo-pcie-adapter** — the first HAB revision; a simpler PCIe to M.2 M-key adapter.
- **m2-mkey-to-aekey** — adapts an M.2 M-key slot to A/E-key, so a Google Coral accelerator can go
  where an NVMe drive would.
- **pcie-fpc-s-shaped** — a 2-layer S-shaped FPC cable matching the connector positions on the
  PCIe adapter.
- **ubo-nfc-hat** — NTAG I²C plus NFC tag with a chain of addressable RGB LEDs.

## Repository layout

One directory per board. Within a board directory:

```
boards/<board>/
  README.md          documentation for this board
  <design files>     KiCad project or Eagle .sch/.brd at the top level,
                     or in a <rev>-<tool>/ subdirectory when a board has
                     more than one revision (see ubo-sideboard)
  images/            renders, layout screenshots, photos
  docs/              exported schematic and assembly PDFs
  datasheets/        datasheets for the components used on this board
  mechanical/        board outline DXF, STEP and other 3D models
```

Not every board has every subdirectory — they exist where there is something to put in them.

## Opening the files

- **KiCad projects** (`.kicad_pro`) — KiCad 8 or 9. Open the `.kicad_pro`, not the individual
  schematic or board files, so the project's library tables load.
- **Eagle designs** (`.sch` / `.brd`) — authored in Eagle CAD 9.6.2. KiCad can also import them
  via *File → Import → Non-KiCad Project*.

## Known limitations

These are real gaps in the repository as it stands. They are documented rather than hidden:

- **The sideboard v1.5.2 KiCad project will not open cleanly on another machine.** Its
  `fp-lib-table` and `sym-lib-table` point at absolute paths under
  `/Users/martin/Documents/KiCAD/9.0/` and at a separate `melonHD` repository, *and* they name
  libraries (`Uno_side_v1.5.2_newFPC.pretty`, `Uno_side_v1.5.2_newFPC-eagle-import.kicad_sym`)
  that do not match the files actually in the folder.
- **HAB v1 and v2 reference a `libs/` directory that was never committed**
  (`${KIPRJMOD}/libs/Mini360_step_down_converter/…`, `${KIPRJMOD}/libs/Wurth_687316124422/…`).
  The 3D models for those parts will be missing when the boards are opened.
- **Several projects reference 3D models by absolute path** under
  `/Users/martin/Documents/KiCAD/9.0/3dmodels/`, plus one inherited from the upstream m1geo
  design under `/home/paulr/`. Where a model file is included in the repo it sits in the board's
  own directory and resolves correctly.
- **There are no fabrication outputs in this repository** — no gerbers, drill files, BOMs, or
  pick-and-place data. Generate them from the source projects.
- **`boards/ubo-top-hat/mechanical/PCB_top_3D_v9.zip` is 23 MB**, which is most of why the git
  history is large. It is a candidate for Git LFS; history has deliberately not been rewritten.

## Moved paths

The repository was reorganized from a per-tool layout into the per-board layout above. If you
have an old link, here is where it went:

| Old path | New path |
|---|---|
| `eagle/top_pcb/` | `boards/ubo-top-hat/eagle/` |
| `images/`, `datasheets/` | `boards/ubo-top-hat/images/`, `boards/ubo-top-hat/datasheets/` |
| `schematics/Ubo_v1.6.1_schematic_full_SKU.pdf` | `boards/ubo-top-hat/docs/` |
| `top_pcb_dimensions.dxf`, `PCB_top_3D v9.zip` | `boards/ubo-top-hat/mechanical/` |
| `eagle/side_pcb/` | `boards/ubo-sideboard/v1.4-eagle/` |
| `schematics/Ubo_side_v1.4_schematic.pdf` | `boards/ubo-sideboard/v1.4-eagle/` |
| `KiCad/ubo_sideboard_v1.5.2/` | `boards/ubo-sideboard/v1.5.2-kicad/` |
| `KiCad/nvme_bm_to_e/` | `boards/m2-mkey-to-aekey/` |
| `KiCad/s-shaped-2layer-PCIe-FPC/` | `boards/pcie-fpc-s-shaped/` |
| `KiCad/ubo-pcie-adapter/` | `boards/ubo-pcie-adapter/` |
| `KiCad/ubo-hab-v2/` | `boards/ubo-hab-v2/` |
| `KiCad/ubo-nfc-hat/` | `boards/ubo-nfc-hat/` |

The Ubo Top HAT documentation that used to be this file now lives at
[`boards/ubo-top-hat/README.md`](boards/ubo-top-hat/README.md).
