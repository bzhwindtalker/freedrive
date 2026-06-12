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

## Community Builds

Freedrive files have been shared with 15+ builders since Season 2. Active community replication builds in 2026 include:

| Builder | Location | Status | Notes |
| :--- | :--- | :--- | :--- |
| **tkfoil** | Germany | ✅ Running | Full replica, 2.3kW+, 30+ starts/session, FD LR6 prop |
| **Mikey** | — | 🔄 In progress | Housing adapted for Flysky 74100 VESC |
| Corsica builder | France | ✅ Running | RS50 tabless cells, custom blades |

See the [foil.zone development thread](https://foil.zone/t/light-assist-season-3/24787) for detailed build logs and ongoing discussions.

---

## Latest verified updates (June 2026)

From the build thread on foil.zone:

### 5085 Motor Testing — Weight Reduction Path
- **Post #208** — **5085 motor** ordered (same as @foilstate's proven design), targeting **~400g weight savings** over the 6384 reference setup.
- **Post #211–#220** — 5085 pod hacked and first water test completed with carbon prop + cotter pins. Despite unbalanced prop and improvised blade mounting, the motor performed well for flat-water starts. Confirmed sufficient for wave/DW assist with small board at 66kg/1600cm² foil.
- **Post #256** — **Titanium blades** received and ready for testing — expected to eliminate blade failure risk.

### Community Replication Builds
- **tkfoil** (Posts #188–#259) — Full replica build from scratch: Craft Cloud aluminum prints, custom spot-welded 12S1P battery with casting epoxy, external antenna setup. After VESC tuning (phase current 125A+, ERPM limit 35k), achieved **2.3kW+ output** and **30+ successful starts** with FD LR6 prop on DW board setup.
- **Mikey** (Posts #183–#187) — Housing adapted to Flysky 74100 VESC + Foil Drive motor components.

### Previous Highlights (Feb 2026)
- **Post #149** — Good results with **EVA foam seals** and move to **titanium screws** after M8 stainless fastener failures.
- **Post #150** — New build assembled in Corsica with **RS50 tabless cells (5.15Ah)**.
- **Post #152** — Clarification that the project needs **no CNC**: parts are printable at home or via services.

Links:
- https://foil.zone/t/light-assist-season-3/24787/208 (5085 motor)
- https://foil.zone/t/light-assist-season-3/24787/220 (5085 first test)
- https://foil.zone/t/light-assist-season-3/24787/256 (titanium blades)
- https://foil.zone/t/light-assist-season-3/24787/249 (community build success)
- https://foil.zone/t/light-assist-season-3/24787/149 (EVA seals)
- https://foil.zone/t/light-assist-season-3/24787/150 (Corsica build)
- https://foil.zone/t/light-assist-season-3/24787/152 (no CNC)

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
