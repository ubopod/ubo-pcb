# Ubo Sideboard

The board that brings the Raspberry Pi's side connectors — mini HDMI, USB-C power, and the
audio jack — around to the back of the Ubo Pod enclosure. See the
[repository index](../../README.md) for the other boards.

Two revisions are kept here:

| Revision | Tool | Status | Files |
|---|---|---|---|
| **v1.5.2** | KiCad | **Current** | [`v1.5.2-kicad/`](v1.5.2-kicad/) — [full documentation](v1.5.2-kicad/README.md) |
| v1.4 | Eagle | Superseded, kept for reference | [`v1.4-eagle/`](v1.4-eagle/) — sources plus [schematic PDF](v1.4-eagle/Ubo_side_v1.4_schematic.pdf) |

Start with **[v1.5.2](v1.5.2-kicad/README.md)** — it carries the feature list, layout, and
schematic images. The v1.4 Eagle design predates the KiCad port and is retained only for history.

> **Heads-up:** the v1.5.2 KiCad project's library tables reference absolute paths on the
> author's machine and name libraries that are not in this folder, so it will not open cleanly
> elsewhere without fixing `fp-lib-table` and `sym-lib-table`. See
> [Known limitations](../../README.md#known-limitations).
