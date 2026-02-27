# Freedrive — Open Foil Assist

A lightweight, open-source electric **foil assist** system for riders who want help getting on foil without turning their setup into a full e-foil.

> Built in the open, tested in real water, and continuously improved with community feedback.

![Freedrive full setup](https://foil.zone/uploads/default/optimized/3X/7/6/7600b1d7a83e75178b8368f0d5a1d5efb3863aa3_2_562x750.jpeg)

---

## Why Freedrive

- **Assist, not full propulsion**: designed for starts and recovery, not long-distance motoring.
- **Low-drag architecture**: slim under-board pod concept.
- **Open hardware workflow**: CAD, print files, wiring, and VESC configs are in this repo.
- **Field-proven iterations**: developed through long-term testing and community builds.

---

## Latest verified updates (Feb 2026)

From the build thread on foil.zone:

- **Post #149** — Good results with **EVA foam seals** and move to **titanium screws** after M8 stainless fastener failures.
- **Post #150** — New build assembled in Corsica with **RS50 tabless cells (5.15Ah)** and custom blade work/testing.
- **Post #152** — Clarification that the project needs **no CNC**: parts are printable at home or via services; material guidance shared for each major component.

Links:
- https://foil.zone/t/light-assist-season-3/24787/149
- https://foil.zone/t/light-assist-season-3/24787/150
- https://foil.zone/t/light-assist-season-3/24787/152

![Corsica assembled unit (community build)](https://foil.zone/uploads/default/original/3X/2/c/2c2dc51ec5a8e2bff7fa10fac7b786cc5623d677.jpeg)

---

## System snapshot (V4 family)

| Feature | Specification |
| :--- | :--- |
| **System voltage** | 12S |
| **Battery current** | 50A |
| **Phase current** | 125A–150A |
| **Power** | ~2200W (6384 120KV reference setup) |
| **Weight** | ~2.8kg (controller, pod, battery) |
| **Expected starts** | 10 to 30 (depends heavily on rider/foil/board/conditions) |
| **Standard battery** | 12S1P 21700 |
| **Assist + one battery cost** | ~650€ |

---

## Who this is for (and not for)

### Good fit
- Experienced DIY riders comfortable with electrical + mechanical assembly.
- Downwind / pump / surf riders wanting launch assist.
- Builders ready to tune and iterate.

### Not a good fit
- Anyone expecting plug-and-play consumer product behavior.
- Riders wanting long powered cruising (use an e-foil platform).
- Builders unwilling to manage electrical/waterproofing/safety risk.

---

## Repository map

| Path | Purpose |
| :--- | :--- |
| `ORDER PRINTS/` | Parts intended for print-order workflow (including metal print parts). |
| `MAKE PARTS/` | Additional parts to manufacture/print. |
| `WIRE/` | Harness PDF + wiring references. |
| `PROGRAMM/` | VESC config files and controller programming notes. |
| `CAD/` | Main STEP and source CAD link. |
| `BOM of V4 system.xlsx` | Bill of materials. |
| `TODO.md` | Current task list / open improvements. |
| `NEWS.md` | Short timeline of recent project updates from the forum thread. |

---

## Manufacturing guidance (current community direction)

Based on current thread guidance:

- **No CNC required** for the baseline project.
- **Base**: aluminum printed (service options cited: Craftcloud / Prototi), with home-print exploration possible.
- **Pod**: printable (PPA-CF FDM or PA12 SLS).
- **Battery box**: PETG print + cast-in-place deep-pour epoxy strategy.
- **Blades**: aluminum printed.
- **Hub**: PA12 SLS or PPA-CF.

Always validate thermal behavior, waterproofing quality, and mechanical integrity before riding.

---

## Scope and limitations

Freedrive is designed as a **lightweight launch/assist system**. It is not intended to replace paddling skill, surf positioning, or proper foil selection.

Known constraints:
- 12S1P travel limitations (airline Wh restrictions).
- Range is limited if motoring heavily.
- Performance depends strongly on total system setup and rider skill.
- This remains a DIY/open project with no warranty, no guaranteed support SLA, and evolving documentation.

---

## Safety (read this first)

A powered propeller under a board is inherently dangerous.

- Build and test at your own risk.
- Treat every test as if failure is possible.
- Verify sealing, fasteners, electrical insulation, and remote fail-safe behavior before water use.
- Keep clear procedures for arming/disarming and handling around people.

---

## Media & communication

- **Main development thread**: https://foil.zone/t/light-assist-season-3
- **Instagram**: https://www.instagram.com/adam_mercier_fr/
- **YouTube**: https://www.youtube.com/@bzhwindtalker29

---

## Credits

Project led by **Bzhwindtalker (Adam Mercier)** with major value from community testing and feedback on foil.zone.

If you build one, share your version and results in the thread — especially reliability, sealing, thermal data, and ride feedback.
