# Freedrive Season 4 — Turbine (Jet Drive) Development

Development log for the ducted jet drive (turbine) propulsion variant of Freedrive.
Context: replace the open propeller with a ducted jet for safety, touchdown drag,
and prop-loss immunity, while keeping the light-assist power class (~2-2.7 kW).

Main thread: https://foil.zone/t/light-assist-season-3/24787
Related analysis: [research.md](../research.md)

---

## 1. Why a turbine

- **Safety**: open prop close calls accumulate with hours. A ducted jet keeps the
  impeller behind a duct lip. This is the main driver (post #351).
- **Touchdown behavior**: open pod causes high drag on touchdown. A ducted unit
  idles much cleaner when the motor spins (post #355).
- **No prop loss**: no folding mechanism, no loose blades to shed.
- **Use case**: downwind starts, surf pop-up, displacement motoring between peaks.
  Same "Flite AMP class" target, open-source and repairable.

Trade-offs accepted for v1:
- Higher static pressure loss in duct → lower efficiency than open prop at flat out.
- Air intake sensitivity (open duct top).
- Touchdown with motor OFF is still a hard brake (funnel effect).

---

## 2. Timeline

| Date | Event | Thread ref |
| :--- | :--- | :--- |
| 2025-09 | Jet concept raised for S3 ("jet pod or EDF style" for safety) | [#131963](https://foil.zone/t/24787/131963) |
| 2026-05 | 5085 motor test path started (weight reduction, see [§4](#4-the-5085-motor-path)) | [#208](https://foil.zone/t/24787/208) |
| 2026-08-17 | V4 prop pod lost in the water. Reliability rework begins. 5085 re-ordered | [#342](https://foil.zone/t/24787/342) |
| 2026-09-05 | S4 jet concept posted ("trying something new for season 4") | [#345](https://foil.zone/t/24787/345) |
| 2026-09-08 | Concept detail: angled intake to save space + reduce cavitation. 5080 motor + 4-blade prop selected | [#348](https://foil.zone/t/24787/348) |
| 2026-09-12 | Bench/early water feedback: sensitive to air intake, balance OK, no scrape/vibration | [#354](https://foil.zone/t/24787/354) |
| 2026-09-13 | **First water test success** (see [§5](#5-first-water-test--13-sept-2026)). Test videos posted | [#355](https://foil.zone/t/24787/355), [#356](https://foil.zone/t/24787/356) |

---

## 3. Test unit (S4 jet v1)

| Item | Spec |
| :--- | :--- |
| Motor | 5080, 4-blade prop supplied, ~95 mm pitch (low pitch per [@V_S](https://foil.zone/t/24787/353)) |
| Intake | Angled duct entry (space saving + cavitation reduction) |
| Battery | 12S1P 21700 P45B, 199 Wh |
| ESC | BWESC 80 V 220 A |
| Max draw seen | 41 V / 65 A ≈ **2.66 kW** |
| Mount | High on the mast, higher than the usual V4 pod |
| Weight | ~1.5–2 kg (pod + motor + prop) |

Concept and build photos (from the thread):

| Concept sketch | Intake detail | Angled 5080 + 4-blade prop | Wiring |
| :--- | :--- | :--- | :--- |
| ![](media/jet-turbine-test/s4-jet-concept-1.jpg) | ![](media/jet-turbine-test/s4-jet-concept-2.jpg) | ![](media/jet-turbine-test/s4-motor-angled.jpg) | ![](media/jet-turbine-test/s4-wiring.jpg) |

---

## 4. The 5085 motor path (context)

The turbine work follows directly from the 5085 motor swap, which cut ~400 g from
the V4 prop setup and gave the cleanest feel of all tested motors.

- **2026-05-12** — 5085 ordered (same motor as @foilstate's proven design).
- **2026-05-13** — V4 pod hacked to fit the 5085. Hub printed (PETG-GF cracked
  after one session → PPA/PA 100% infill hubs).
- **2026-05-16** — First 5085 test with unbalanced carbon prop + cotter pins:
  felt stronger than the maytech 6374, lower drag on pod touchdown, easy
  starts in small chop. (post [#220](https://foil.zone/t/24787/220))
- **2026-06-06** — Titanium blade set received (90 USD, alu + ti set). No post
  processing needed, edges sharper than alu. (post [#256](https://foil.zone/t/24787/256))
- **2026-06-15** — Ti prop test: perfect out of the box. 5085 + ti setup "very
  smooth, gets forgotten when pumping". Previous DW score passed on 15 kt
  tailwind + slow Saône current. Ti bolts + ti blades credited. (post [#261](https://foil.zone/t/24787/261))

5085 / Ti build photos:

| Hacked 5085 pod | First 5085 water test | Ti blade set |
| :--- | :--- | :--- |
| ![](media/5085/5085-pod-hack.jpg) | ![](media/5085/5085-first-test.jpg) | ![](media/ti-blades/ti-blades-1.jpg) |

---

## 5. First water test — 13 Sept 2026

Results from the first dedicated jet test (post [#355](https://foil.zone/t/24787/355)):

- **System works.** Small board started a few times, but only with full battery.
- **Battery hammered**: 41 V / 65 A at full charge on 12S1P. 199 Wh is too small
  for this duty cycle. 12S2P is the fix.
- **Big board**: easy flying with some pumping. Transition to fully flying not easy.
- **Touchdown**: motor off = lot of drag (funnel brake). Motor spinning = drag much less noticeable.
- **Air intake**: confirmed very sensitive (post #354).
- **Balance**: no scraping or vibration felt.

Test screenshots (from the posted videos, [13 septembre 2026](https://www.youtube.com/watch?v=aBwcKk_be1A) and [End of battery](https://www.youtube.com/watch?v=OXS7Xq_WdP4)):

| Start on small board | Foiling with the jet | Flight, big board |
| :--- | :--- | :--- |
| ![](media/jet-turbine-test/yt-jet-start.jpg) | ![](media/jet-turbine-test/yt-jet-foiling.jpg) | ![](media/jet-turbine-test/yt-jet-flight.jpg) |

On-site photos from the test day (post #355):

| Jet test 1 | Jet test 2 |
| :--- | :--- |
| ![](media/jet-turbine-test/jet-test-1.jpg) | ![](media/jet-turbine-test/jet-test-2.jpg) |

---

## 6. Known gaps (carried from research.md, updated by the tests)

1. **Prop pitch**: 95 mm too low for DW speed. Higher pitch impeller next.
2. **Air intake**: sensitive → shroud or redesigned intake.
3. **Touchdown drag**: motor-off funnel brake → gate or folding element study.
4. **Thermal**: 5080 at 65 A sustained, no active cooling → monitor.
5. **Pod retention**: pod lost in water (17 Aug 2026) → retention mechanism.
6. **Battery**: 199 Wh too small for 2.66 kW → 12S2P (398 Wh) or 16S1P.

---

## 7. Links

- S4 jet concept: https://foil.zone/t/light-assist-season-3/24787/345
- Angled intake + motor: https://foil.zone/t/light-assist-season-3/24787/348
- Air intake sensitivity: https://foil.zone/t/light-assist-season-3/24787/354
- First water test: https://foil.zone/t/light-assist-season-3/24787/355
- Test videos: https://foil.zone/t/light-assist-season-3/24787/356
  - [13 septembre 2026](https://www.youtube.com/watch?v=aBwcKk_be1A)
  - [End of battery](https://www.youtube.com/watch?v=OXS7Xq_WdP4)
- 5085 motor: https://foil.zone/t/light-assist-season-3/24787/208
- Ti blades: https://foil.zone/t/light-assist-season-3/24787/256
- Ti prop test: https://foil.zone/t/light-assist-season-3/24787/261
- Jet research (impellers, Flite AMP, CAD tools): [research.md](../research.md)
