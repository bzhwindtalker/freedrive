# Foil Assist Jet System — Research

Research on water jet / impeller propulsion for foil assist system.
Context: Freedrive S4 jet duct concept, comparison with Flite AMP,
and smaller-diameter (40-60mm) impeller options for reduced system thickness.

Full build/test log with photos and video references:
[docs/turbine-development.md](docs/turbine-development.md)

---

## 1. Current Setup (Freedrive S4 Jet)

- Motor: 5080, 4-blade prop, ~95mm pitch (too low per @V_S on foil.zone)
- Battery: 12s1p P45B = **199Wh** (NOT 700Wh — corrected)
- Max draw: 41V/65A = **2.66kW**
- ESC: BWESC 220A (80V rated, 16s possible)
- VESC config: [PROGRAMM/vesc_mcconf_freedrive.xml](PROGRAMM/vesc_mcconf_freedrive%20(1).xml)
- Weight: ~1.5-2kg (pod + motor + prop)
- Test results (13 Sept 2026):
  - Small board: starts only with full battery, 41V/65A = battery hammered
  - Big board: easy flying with pumping, transition to full flight not easy
  - Touchdown motor off = high drag, motor on = drag OK
  - Air intake sensitive (confirmed)
  - Pod lost in water (17 Aug 2026)

### Status at 2026-10-27 (thread post [#377](https://foil.zone/t/24787/377))
- Purchase made: **5065 motor, 320 KV, rated 1800 W** + **8 mm stainless steel shaft**.
- Impeller path: scale an RC boat **40 mm two-stage turbine to 50 mm**
  (post [#369](https://foil.zone/t/24787/369)). Builder report: **13.3 kg thrust at 8S / 2.2 kW**.
- Package target: motor under the mast, one water inlet on each side, battery in front,
  about **55 mm** package thickness.
- Turbine CAD is paused while the motor and shaft are sourced (post #377).
- Note: the 1800 W motor rating is below the 2.2-2.7 kW the tests pulled. See [§8](#8-scaling-law-for-the-jet-unit).

---

## 2. Flite AMP Comparison

| Spec | Freedrive S4 | Flite AMP (4'2" S) |
|---|---|---|
| Board | ~25L / 7'2 | 4'2" 27L carbon |
| Board weight (dry) | ~2.5kg | 2.94kg (6.5lbs) |
| Jet unit | 5080 + 4-blade prop + duct | Enclosed impeller, alu anodised |
| Jet weight | ~1.5kg | 2.3kg (incl 2 cells) |
| Battery | 12s1p P45B = **199Wh** | 2x AMPCell = **284Wh** |
| Battery weight | ~1.5kg | 2.0kg |
| Battery voltage | 41V (sag) | 50.4V nominal (58.8-42V) |
| Max power | 2.66kW | ~1.5-2kW (**our estimate; Flite publishes no power figure**) |
| Max thrust | ~25kg | **25kg peak, 2 AMPCells, 10s boost cycle** (verified 2026-10-27) |
| Total system weight | ~6.5-7kg | 7.2kg |
| Control | Maytech RX + BWESC 220A (continuous throttle) | LAUNCHPad + Flite App (10s fixed cycle) |
| Touchdown drag | HIGH (motor off) | LOW (enclosed, no prop to catch) |
| Air intake | Sensitive (open duct) | No (fully enclosed) |
| Price | ~500-800€ | 7,924€ (set) / 3,849€ (jet) |
| AMPCell weight | — | 1.0kg each |
| AMPCell charge time | — | 1 hour |
| AMPCell safety | — | Humidity sensor, PCM thermal, sight glass, fly-safe |

### Flite AMP key specs (from official + reviews)
- 25kg max thrust (2x AMPCells)
- 142Wh per AMPCell, 50.4V nominal
- 1.0kg per AMPCell
- Fully enclosed impeller, anodised aluminium, precision bushes
- 10s thrust cycle: moderate → high → moderate → off
- Board first, jet second design philosophy
- Jet swaps out in seconds
- Price: $3,849 USD (jet), $7,924 USD (4'2" set)

### Verification of the 25 kg figure (online check, 2026-10-27)

Sources checked: Fliteboard US and EU product pages, the AMPJet product page, a dealer
page (Wet Feet Sports), two independent reviews (The Inertia, Foiling Magazine), and one
market comparison (Foilfun). Fliteboard and the two reviews agree on the headline number.

| Claim | Value found | Source |
|---|---|---|
| Max thrust | **25 kg, only with 2 × AMPCells.** One cell gives less. | [fliteboard.com/products/ampjet](https://fliteboard.com/products/ampjet), [eu.fliteboard.com](https://eu.fliteboard.com/pages/flitelab-amp) |
| Thrust, independent | "Flitelab cites **25 kg (55 lbs)** of max thrust" | [The Inertia review](https://www.theinertia.com/gear/flitelab-ampjet-foil-assist-review/) |
| Thrust, independent | "can provide **up to 25 kg of thrust** at the touch of a button" | [Foiling Magazine test](https://www.thefoilingmagazine.com/test-center/flitelab-amp_jet/) |
| Jet cartridge mass | **2.2 kg** with impeller, plus **2 × 1.0 kg** cells = **4.2 kg** system | The Inertia |
| Added mass on board | "adds only 4 kg", 4'2" board + jet + 2 cells = **7.2 kg** | Foiling Magazine |
| Cell capacity | **142 Wh** per AMPCell, **284 Wh** for two | official + Inertia |
| Charge time | **about 50 min** for two cells on the included charger | The Inertia |
| Boost count per session | **about 40 boosts**, session about 2 h | [Foilfun comparison](https://foilfun.com/foil-assist/) |
| Duty cycle | **Boost = about 5 s (±2 s) at max power.** Paddle Assist = low power for 1 min. About **40 Boost / Paddle Assist actions** from 2 × AMPCell_142 | [FLITELab FAQ](https://fliteboard.com/en-ca/pages/flitelab-faq). A rider-reported 10 s cycle: [foilsurfing.net](https://foilsurfing.net/flitelab-amp-board-initial-thoughts/) |
| Price | **$8,254 USD** board package, **$11,813** with the 1010 foil | The Inertia |

**Physics plausibility check (computed, not measured).** 25 kgf = 245 N. Actuator disk
theory gives `P = T · ve / 2`, so:

| Exit velocity | Ideal power | Electrical at 80% motor + ESC |
|---|---|---|
| 8 m/s | 980 W | 1230 W |
| 10 m/s | 1230 W | 1530 W |
| 12 m/s | 1470 W | 1840 W |
| 14 m/s | 1720 W | 2150 W |

So 25 kg needs roughly **1.5-2.1 kW electrical**. That matches the pack size: 284 Wh at
1.8 kW is **9.5 min** of full thrust, or **about 115 boosts of 5 s**. Flite quotes about
40 actions per two cells, so the claim is internally consistent. The duty cycle also puts
a ceiling on peak power: usable energy is about 256 Wh. If the 40 actions are 5 s boosts
and boosts take 40-60 % of the pack, peak boost power is **1.8-2.8 kW**. If boosts take
the whole pack, the ceiling is 4.6 kW. So the true peak is somewhere in **1.5-4.5 kW**.
Flite publishes no wattage, so we keep the range.

**Reconciling ideal theory with our own measurement.** Ideal momentum theory is a lower
bound, not a prediction. For a plain nozzle it gives `ve = sqrt(T / (ρ·A))`:

| Nozzle | Ideal exit velocity | Ideal power |
|---|---|---|
| 50 mm | 11 m/s | 1.4 kW |
| 60 mm | 9 m/s | 1.1 kW |
| 80 mm | 7 m/s | 0.9 kW |

Our **measured** 80 mm unit needed **2.66 kW** for about 25 kg. Real efficiency is
therefore about **35 % of ideal** at this scale. Apply that same loss factor to a 50 mm
unit and 25 kg costs about **4.5 kW**, which agrees with the
[§8 scaling law](#8-scaling-law-for-the-jet-unit). Do not size the 50 mm jet from ideal
theory. Size it from the measured point.

**What the 25 kg figure does not tell you:**
1. No power, no voltage, no current is published. Our 1.5-2 kW row stays an estimate.
2. It is a **peak, short-cycle** number. It is not a continuous rating.
3. Static thrust is not thrust at speed. Foil Drive and Elevate publish thrust at speed;
   Flite does not. Elevate states **50 kg at 5 kW** on their home page, quoted in the
   foil.zone "Fr 2019 motor system" thread
   ([#116](https://foil.zone/t/3762/116)). By our scaling that ratio also points to
   about 2 kW for 25 kg.
4. Impeller diameter is not published. The bracket in the next section puts it at
   **60-75 mm**, from board thickness and energy balance. Treat it as inferred.

**Access note:** The Inertia and Foiling Magazine return **403** to plain `curl`. Their
content above was read through a text proxy. Open both links in a browser to check them.

**Corrections made to the table above:** the earlier row read "25kg (confirmed)" with no
duty qualification. It is now labelled as peak, two cells, 10 s cycle. The
"50.4 V nominal" figure for the AMPCell is **not confirmed by these sources**; it is an
assumption carried from earlier notes. Treat it as unverified.

### Impeller diameter: not published, bracket 60-75 mm (2026-10-27)

Flite does not publish the AMPJet impeller or duct diameter. Sources checked, all of them
give only the phrase "completely enclosed impeller": the US and EU AMPJet product pages,
the Shopify product JSON, the [FLITELab FAQ](https://fliteboard.com/en-ca/pages/flitelab-faq),
the [FLITELab quickstart](https://fliteboard.com/pages/flitelab-quickstart), The Inertia,
Foiling Magazine, The Foiling Collective, and dealer pages (Surfdoctor, eFoil-riders,
Houston Kiteboarding). No teardown or measurement exists online.

Two published anchors let us bracket it.

**Anchor 1, board thickness.** The AMP_Board technical spec is on the product page. The
cartridge sits inside the tail cavity, so the duct has to fit under the deck.

| Board | Length | Width | Thickness |
|---|---|---|---|
| AMP_S 4'2" | 1270 mm | 445 mm | **79 mm** (3.1") |
| AMP_S 4'8" | 1422 mm | 508 mm | **89 mm** (3.5") |
| AMP_M 5'0" | 1524 mm | 457 mm | **91 mm** (3.6") |
| AMP_M 5'8" | 1727 mm | 483 mm | **107 mm** (4.2") |

A cartridge in a 79 mm thick tail leaves room for a duct of roughly **55-70 mm** after the
shell, deck core and intake. The cartridge plan-view width in the official bottom render
measures about 190-320 mm at the tail, so width is not the limit. Thickness is the limit.

**Anchor 2, Flite's other jet.** The Fliteboard eFoil "Flite Jet 2" is specified in their
own [User Guide](https://support.fliteboard.com/hc/en-us/article_attachments/40487401948823):
**jet diameter 88 mm**, input 5000 W, shaft 3600 W, motor 10 500 rpm peak. That is a
different product, but it shows the size class Flite works in.

**Power needed for 25 kg, by duct diameter.** Ideal actuator disk, then our measured
efficiency band (45 % and 35 % of ideal).

| Duct | Ideal power | Electrical at 45 % | Electrical at 35 % |
|---|---|---|---|
| 50 mm | 1.94 kW | 4.31 kW | 5.54 kW |
| 55 mm | 1.76 kW | 3.91 kW | 5.03 kW |
| 60 mm | 1.61 kW | 3.59 kW | 4.61 kW |
| 65 mm | 1.49 kW | 3.31 kW | 4.26 kW |
| 70 mm | 1.38 kW | 3.08 kW | 3.95 kW |
| 75 mm | 1.29 kW | 2.87 kW | 3.69 kW |
| 80 mm | 1.21 kW | 2.69 kW | 3.46 kW |

Cross-check: the duty-cycle ceiling is 1.5-4.5 kW. A 60-75 mm duct needs 2.9-4.6 kW at our
measured efficiency. That fits. A 50 mm duct needs 4.3-5.5 kW, which the 284 Wh pack can
only support at the extreme end.

**Conclusion.** The AMPJet impeller is most likely **60-75 mm**, not a small high-RPM
impeller. Our own 80 mm unit at 2.66 kW for 25 kg sits just above it, which supports the
reading. Confidence is medium. The band is ±15 mm and comes from geometry and energy
balance, not from a measurement.

**What this changes for us.**
1. The AMP does not prove that 25 kg fits in a 50 mm duct. It points the other way.
2. Our 50 mm target at 2.2-2.7 kW still gives **15-18 kg**, see
   [§8](#8-scaling-law-for-the-jet-unit). Open question 9 stands.
3. Flite runs a **5 s boost**, not continuous thrust. A motor rated 1800 W can still deliver
   a 3 kW peak for 5 s if the battery and ESC can source it. That is a way to answer open
   question 7 without a bigger motor: define the S4 duty cycle as boost-only.

### Where Freedrive wins
- Price (10-15x cheaper)
- Continuous throttle control (vs a fixed about 5 s boost cycle)
- Higher sustained power (2.66kW vs ~1.5-2kW)
- Customizable, repairable, open source
- Can use existing boards

### Where Flite wins
- Touchdown drag (enclosed = no drag when off)
- Integration (in-board vs on-mast)
- Safety systems (humidity sensor, thermal, fly-safe)
- Prop/impeller efficiency (optimized)
- No air intake sensitivity

### Links
- Official: https://fliteboard.com/pages/flitelab-amp
- Product: https://fliteboard.com/products/ampjet_board-set
- Jet: https://fliteboard.com/products/ampjet
- Review: https://foilsurfing.net/flitelab-amp-board-initial-thoughts/
- Review (independent): https://www.theinertia.com/gear/flitelab-ampjet-foil-assist-review/
- Test (independent): https://www.thefoilingmagazine.com/test-center/flitelab-amp_jet/
- Market comparison table: https://foilfun.com/foil-assist/
- Dealer spec text: https://wetfeetsports.com/products/flitelab-amp
- AMPCell: https://www.kitepower.com.au/products/flitelab-amp-cell

---

## 3. Smaller Impeller Analysis (40-60mm)

### Physics
Thrust ∝ D² × pitch × RPM² (approx)

At 2.66kW, to maintain ~25kg thrust:
- 80mm (current): 6,500rpm
- 60mm: need **8,667rpm**
- 50mm: need **10,400rpm**
- 40mm: need **13,000rpm**

All achievable with high-KV motor + 12s (41V).

### Thickness comparison
| System | Diameter | Length | Thickness |
|---|---|---|---|
| Freedrive 5080 | 80mm | ~150mm | 80mm |
| 60mm 2-stage | 60mm | ~130mm | 60mm |
| HPW40 (40mm) | 40mm | ~120mm | 40mm |
| Flite AMP | ~150mm | ~200mm | 150mm (in-board) |

60mm = 25% thinner than 5080, 60% thinner than Flite.

### Recommended motor for 60mm
- 5065 800-1000KV → 10,000-12,000rpm at 41V
- 5070 600-800KV → 8,000-10,000rpm at 41V
- Weight: 300-400g
- Power: 2-3kW

**Superseded on 2026-10-27**: a **5065 320 KV (1800 W rated)** was bought instead.
At 12S it already turns 13,100-16,100 rpm, which covers the 50-60mm band without
extra gearing. See [§8](#8-scaling-law-for-the-jet-unit).

---

## 4. Open Source Jet Pump / Impeller Designs

### 4.1 HPW40 — 40mm 2-Stage Water Jet Drive (BEST MATCH)

- **URL**: https://youmagine.com/designs/1d90c387-66b6-4e87-a7b4-b5b339b6804f
- **Also**: https://cults3d.com/en/3d-model/game/hpw40-2-stage-water-jet-pump-wasserstrahlantrieb
- **Author**: HillPrinties
- **Diameter**: 40mm nominal
- **Stages**: 2 (like jet ski)
- **Designed for**: 4074 1400KV motor, 150A ESC, 3-6S LiPo
- **Power**: 2.0-2.5kW
- **Includes**: housing, stator, stator housing, 2 impellers, control nozzle, reverse flap, V8 motor cover
- **3D printable**: PA12/ABS-CF recommended
- **Price**: $20.50 STL (YouMagine) / $179 alu kit (vajjexrc)
- **Weight**: ~500-700g (printed)
- **Components needed** (not included):
  - 4074 1400KV brushless motor
  - 150A ESC
  - 2x 3S LiPo
  - 1-2 25kg waterproof servo
  - 1x shaft seal ring 5x16x5
  - 2x sealed stainless steel ball bearing 5x13x4

### 4.2 54mm Jet Drive

- **URL**: https://www.printables.com/model/179699-water-jet-pump-jet-drive-54mm-pump-jet
- **Author**: Andrew W.
- **Diameter**: 54mm
- **Use**: RC boat, used 2x for electric surfboard
- **Single-stage** design
- Free STL

### 4.3 80mm Water Jet (Mixed-Flow)

- **URL**: https://www.thingiverse.com/thing:5247333
- **Diameter**: 80mm
- **Design**: Mixed-flow (higher static pressure than axial)
- **Status**: Experimental prototype
- **Target**: Kayaks, surfboards

### 4.4 Commercial CNC Impellers (AliExpress)

- 40mm/60mm/70mm/85mm/100mm/120mm range
- 7075 aluminum, 2-3 blades
- 4-5mm shaft
- Price: $20-50
- Some kits include 3674 motor + water cooling jacket
- Not open source, but cheap and proven
- Search: "water jet impeller" on AliExpress

### 4.5 SSS 4074 Motor (for HPW40)

- **40mm diameter x 74mm long**
- KV options: 1400 / 1850 / 2200 / 2500
- 4-pole inner runner
- Water cooling jacket included
- Efficiency >90%
- Weight: ~750g (with jacket)
- **URLs**:
  - https://www.tflhobby.com/products/sss-4074-series-4-poles-inner-runner-brushless-motor-water-cooling-for-rc-boat-electric-surfboard
  - https://www.noahsrcark.co.uk/products/dcf8ed7467/131444000002103471
  - https://www.aliexpress.com/item/32848316583.html

---

## 5. Parametric Turbine / Impeller CAD Tools

### 5.1 TurboDesigner (CLOSEST TO WHAT YOU WANT)

- **URL**: https://github.com/OpenOrion/turbodesigner
- **Install**: `pip install turbodesigner`
- **What**: Parametric turbomachinery design tool
- **Input**: pressure ratio, mass flow, RPM
- **Output**: Mean-line thermodynamic analysis, blade flow analysis, 3D STEP files
- **Currently**: Axial compressor focused, plans for axial turbines + turbopumps
- **Methods**: Free-vortex theory, Johnsen-Bullock deviation, DCA + NACA 65 airfoils
- **CAD**: CadQuery (OpenCASCADE), exports STEP
- **Note**: Designed for air (compressors), needs adaptation for water (lower speed, higher density)

### 5.2 ParaturboCAD

- **URL**: https://github.com/SoheylM/paraturbo-cad
- **What**: Python + CadQuery, parametric centrifugal impeller design
- **Context**: ASME 2024 research paper (gas-bearing turbocompressors)
- **Classes**: IMPELLER(), SGTB(), ROTOR(), HELPER()
- **Use**: Overkill for water jet, but blade geometry code reusable
- **Install**: Python 3.11, Conda, `pip install -r requirements.txt`

### 5.3 RadialTurboMacrosFreeCAD

- **URL**: https://github.com/20jeka08
- **What**: FreeCAD Python macros for parametric radial impeller generation
- **Use**: FreeCAD (free), export STEP/STL
- **Note**: Radial, not axial, but blade geometry adaptable

### 5.4 CFturbo (NOT OPEN SOURCE)

- **URL**: https://cfturbo.com
- **What**: Professional turbomachinery design + CFD
- **Use**: Axial impeller design tutorial available (PDF)
- **Cost**: Commercial, expensive
- **Link**: https://cfturbo.com/fileadmin/content/down/tutorials/CFturbo_Axial_Impeller.pdf

---

## 6. Recommendations

### Option A: Print (fastest, 1-2 weeks)
1. Download HPW40 STL from YouMagine ($20)
2. Scale to 60mm in Fusion360 (50% scale)
3. Print housing in PA12 (CraftCloud, ~€30-50)
4. Get 5065 800-1000KV motor (AliExpress, ~$80-120)
5. Test with existing BWESC + 12s1p
6. If thrust insufficient: go 12s2p (398Wh)

### Option B: CNC (best performance, 2-4 weeks)
1. Use TurboDesigner to generate 60mm axial impeller
2. Export STEP, send to CNC shop or China
3. 7075 aluminum, 3-5 blades
4. Cost: $50-150
5. Test with 5065/5070 high-KV motor

### Option C: Buy (fastest, 1-2 weeks shipping)
1. AliExpress 60mm CNC impeller ($30)
2. 5065 high-KV motor ($100)
3. Test immediately with existing ESC + battery

### Option D (path chosen on 2026-10-13): scale a proven RC turbine
1. Buy the files for a **40 mm RC boat turbine** (post [#369](https://foil.zone/t/24787/369)).
   Builder report: 13.3 kg thrust at 8S / 2.2 kW.
2. Scale to **50 mm** for a package about **55 mm** thick.
3. Put the **motor under the mast**, one **water inlet on each side**, battery in front.
   Side inlets keep the intake below the surface. This should beat the open top duct on
   air ingestion (post #369, unproven).
4. Two stages, per the @BabePilot / Flite AMP logic: stage one pushes water, stage two
   pushes the air-water mix. See [§8](#8-scaling-law-for-the-jet-unit) for the thrust this buys.
5. Motor bought: 5065 320 KV, 1800 W rated, 8 mm stainless shaft (post [#377](https://foil.zone/t/24787/377)).
   Check the 1800 W limit against the 2.2 kW target before the first bench run.

### Battery upgrade path
- Current: 12s1p P45B = 199Wh (hammered at 2.66kW)
- Option 1: 12s2p = 398Wh, ~3kg, 65A → 32A per pack
- Option 2: 16s1p = 266Wh, higher voltage, less current (BWESC handles 80V)
- Option 3: 12s1p P50B = 266Wh, still 1x C at 65A

### Key gaps to solve
1. **Prop pitch**: 95mm too low → need higher pitch for DW speed
2. **Air intake**: Sensitive → redesign intake or add shroud
3. **Touchdown drag**: Motor off = high drag → folding prop or gate
4. **Thermal**: No cooling for 5080 at 65A sustained → monitor temp
5. **Pod retention**: Lost pod in water → need retention mechanism
6. **Battery**: 199Wh too small for 2.66kW → 12s2p or 16s
7. **Motor rating**: 5065 320 KV is rated 1800 W. The 50 mm jet wants 2.2-2.7 kW.
   Solve with a bigger motor, or two 5065 in a twin jet, or a lower thrust target.
8. **Hub reliability**: printed folding hubs crack. See [§7.1](#71-folding-hub-cracking-the-main-reliability-failure).
   A jet unit has no folding hub, which is one reason the jet path is more reliable.
9. **Thrust budget honesty**: a 50 mm jet at 2.5 kW is a 15-18 kg unit. Do not
   design the board and foil around 25 kg. See [§8](#8-scaling-law-for-the-jet-unit).

---

## 7. Field intel from the thread, Aug-Oct 2026

Numbers below come from rider reports in
[Light assist Season 3](https://foil.zone/t/light-assist-season-3/24787). They are
field data, not bench measurements.

### 7.1 Folding hub cracking (the main reliability failure)

| Case | Material | Result | Post |
|:---|:---|:---|:---|
| Adam 5085 hub | PA12 (printed) | Cracked after 5 batteries | [#323](https://foil.zone/t/24787/323) |
| Adam 5085 hub, 2nd | printed, then PLA+ (volkv remix) | 2nd hub also broke; Ti blades lost in water | [#338](https://foil.zone/t/24787/338) |
| @sat_be 6384 hub | CC3D PBT pro + GF | Cracked after some sessions | [#326](https://foil.zone/t/24787/326) |
| @sat_be 6384 hub | PC-ABS | Printed, not tested yet | [#326](https://foil.zone/t/24787/326) |
| @volkv 5085 hub | SUNLU Easy PA, 3 bolts through the base, heat inserts | Two sessions, no crack | [#336](https://foil.zone/t/24787/336) |
| @nekitesurfing 6384 hub | SiraTech Fibreheart PPA-CF | Holding up, prints well on Bambu X1C | [#340](https://foil.zone/t/24787/340) |

@volkv hammer test at 90 °C, one prop tower broken with a hammer (post [#339](https://foil.zone/t/24787/339)):
- PETG: broke, but held better than PETG-CF.
- PETG-CF: shattered on the second blow.
- Easy PA: did not break, only marked and deformed.
- Suspected weak point in printed hubs: layer adhesion in Z. Suggested fixes: print tilted 45°.

Failure mode read from the thread:
- Cracks start at the blade root / tower, not at the layer line (post [#330](https://foil.zone/t/24787/330)).
- Foil Drive puts small chips in the hub face and smooth blade seats. The chips are
  a sand escape path, so grit cannot jam a blade (post [#337](https://foil.zone/t/24787/337)).
- Oxidised printed alu blades gain opening resistance over time, which raises hub load (post [#330](https://foil.zone/t/24787/330)).
- A 5085 hub has less material than a 6384 hub, and Ti blades add a bigger snap-open torque (post [#327](https://foil.zone/t/24787/327)).
- Fix direction in the thread: aluminium or titanium hub and adapter for reliability (post [#327](https://foil.zone/t/24787/327)).
- Hub material question raised again in the spin-off thread: [TPU-GF for motor hub](https://foil.zone/t/tpu-gf-for-motor-hub/27024).

### 7.2 Potting compound attacks thermal pads
@tkfoil opened a controller after one season (post [#361](https://foil.zone/t/24787/361),
follow-ups [#363](https://foil.zone/t/24787/363), [#366](https://foil.zone/t/24787/366)):
- The silicone thermal pad dissolved where it touched Magic Gel potting compound.
- Dissolving reached about 2 mm under the controller. The gel was still fluid only in that zone.
- Cause read as a chemical reaction, not heat.
- Rule: keep potting compound off the thermal pad, or pot the pad area separately.

### 7.3 RF link through water
- 868 MHz (BRemote) keeps range through the water where 2.4 GHz struggles (post [#332](https://foil.zone/t/24787/332)).
- A smaller 868 MHz receiver was announced for 2-3 weeks out (post [#334](https://foil.zone/t/24787/334)).
- Working fix on the Freedrive rig: lengthen the coax by soldering a second section,
  seal the antenna ends, and line the two antennas up. Signal went back to fully usable (post [#338](https://foil.zone/t/24787/338)).
- Best long term idea: embed the antenna inside the TPU pad between board and assist unit (post #338).
- Corrosion around the antenna area needs sealing on both sides (post [#335](https://foil.zone/t/24787/335)).

### 7.4 Remote ergonomics for pop-up
@Jan12 retrofit, no disassembly (post [#344](https://foil.zone/t/24787/344)):
- Low trigger that does not catch on chop.
- Guard that stops fingers pushing the trigger and gives a flat pad to press on during the pop-up.

### 7.5 Power settings that were in use on the 5085 jet
From post [#327](https://foil.zone/t/24787/327):
- Phase current limit 130 A → **150 A**.
- Battery current limit 50 A → **55 A**.
- LVC lowered to **2.5 V per cell under load**.
- erpm raised about **10 %**.
Effect: 1050 cm² foil became underpowered as soon as the battery sagged.
Reading: current limits, not the motor, set the ceiling. 55 A × 50.4 V ≈ 2.77 kW.

### 7.6 Session length data points
- @tkfoil, DW board + 1300 cm² foil + 12S1P P42: 9.69 km in 2 h 11 min, about 30 waves (post [#322](https://foil.zone/t/24787/322)).
- Same session length as a rider on Foil Drive Slim with a DW board (post #322).
- Bigger board raises efficiency a lot, but is harder to launch (post [#323](https://foil.zone/t/24787/323)).

---

## 8. Scaling law for the jet unit

The RC boat turbine to scale: **40 mm, 2.2 kW, 13.3 kg thrust** (post [#369](https://foil.zone/t/24787/369)).
A 1:1 area scale (×(50/40)²) would predict 20.8 kg. That is wrong. It ignores the
power the bigger impeller needs.

Correct approach, same geometry family and the same advance ratio:
- Thrust `T = CT · ρ · n² · D⁴`
- Power `P = CP · ρ · n³ · D⁵`
- Remove `n`: **T ∝ (P · D)^(2/3)**

| D (mm) | P (kW) | Thrust (kg) |
|:---|:---|:---|
| 40 | 2.20 | 13.3 (reported) |
| 40 | 2.66 | 15.1 |
| 50 | 2.20 | 15.4 |
| 50 | 2.66 | 17.5 |
| 55 | 2.66 | 18.7 |
| 60 | 2.66 | 19.8 |
| 80 | 2.66 | 24.0 |

Cross-check: the law gives 24 kg for the 80 mm 5080 unit at 2.66 kW. The measured
figure for that unit is about 25 kg. The law is within 5 % on the one point we can check.

Power needed for a thrust target:

| D (mm) | kW for 20 kg | kW for 25 kg |
|:---|:---|:---|
| 50 | 3.25 | 4.54 |
| 55 | 2.95 | 4.12 |
| 60 | 2.70 | 3.78 |
| 80 | 2.03 | 2.83 |

Consequences for the 50 mm design:
1. A 50 mm jet at the current 2.2-2.7 kW budget gives **15-18 kg**, not 20 kg.
2. 25 kg at 50 mm needs about **4.5 kW**. That is out of the class.
3. 20 kg at 55-60 mm needs **2.7-3.0 kW**. This is the nearest way to reach the
   old 5080 thrust level with a thin unit.
4. The bought **5065 320 KV is rated 1800 W**. Run it at 2.2 kW and it is overloaded.
   Either keep it under 1.8 kW and accept about 13-15 kg at 50 mm, or move to a
   5070/5085 class motor for 2.5 kW plus.

### Speed check for the 5065 320 KV at 12S

| Bus voltage | No-load rpm | 50 mm tip speed | 55 mm tip speed |
|:---|:---|:---|:---|
| 50.4 V (12S full) | 16,100 | 42 m/s | 46 m/s |
| 44.4 V (12S nominal) | 14,200 | 37 m/s | 41 m/s |
| 41.0 V (sag under load) | 13,100 | 34 m/s | 38 m/s |

Tip speed above about 40-45 m/s in water brings cavitation risk. The 55 mm option
sits at the top of that band at full charge. The 50 mm option has margin.

---

## 9. Links

### Freedrive repo
- https://github.com/bzhwindtalker/freedrive
- CAD (Onshape): https://cad.onshape.com/documents/69e061cb4c8645619cdbc4fc/w/9ab742b640d16d4199051770/e/b0ebddbcfe0ccffe19f3a73c
- BOM: [BOM of V4 system.xlsx](BOM%20of%20V4%20system.xlsx)
- VESC config: [PROGRAMM/vesc_mcconf_freedrive.xml](PROGRAMM/vesc_mcconf_freedrive%20(1).xml)
- Wiring: [WIRE/HARNESS%20FREEDRIVE%20V4.pdf](WIRE/HARNESS%20FREEDRIVE%20V4.pdf)

### Forum
- Main thread: https://foil.zone/t/light-assist-season-3/24787
- S4 jet test (13 Sept): https://foil.zone/t/light-assist-season-3/24787/355
- 5080 motor: https://foil.zone/t/light-assist-season-3/24787/348
- V_S prop pitch comment: https://foil.zone/t/light-assist-season-3/24787/353
- Dedicated S4 system concept (17 Sept): https://foil.zone/t/light-assist-season-3/24787/358
- 40 mm RC turbine files + 50 mm scaling (13 Oct): https://foil.zone/t/light-assist-season-3/24787/369
- Two-stage jet vs AMP drag debate: https://foil.zone/t/light-assist-season-3/24787/374
- Turbine CAD progress (18 Oct): https://foil.zone/t/light-assist-season-3/24787/373
- Motor + shaft ordered, 5065 320 KV (27 Oct): https://foil.zone/t/light-assist-season-3/24787/377
- Hub cracking thread, materials data: https://foil.zone/t/light-assist-season-3/24787/330
- TPU-GF hub experiment thread: https://foil.zone/t/tpu-gf-for-motor-hub/27024

### Flite AMP
- Official: https://fliteboard.com/pages/flitelab-amp
- Product: https://fliteboard.com/products/ampjet_board-set
- Jet: https://fliteboard.com/products/ampjet
- AMPCell: https://www.kitepower.com.au/products/flitelab-amp-cell
- Review: https://foilsurfing.net/flitelab-amp-board-initial-thoughts/

### Jet pump designs
- HPW40: https://youmagine.com/designs/1d90c387-66b6-4e87-a7b4-b5b339b6804f
- 54mm: https://www.printables.com/model/179699-water-jet-pump-jet-drive-54mm-pump-jet
- 80mm: https://www.thingiverse.com/thing:5247333
- STLFinder (118 models): https://www.stlfinder.com/3dmodels/water-jet-impeller/

### Turbine CAD tools
- TurboDesigner: https://github.com/OpenOrion/turbodesigner
- ParaturboCAD: https://github.com/SoheylM/paraturbo-cad
- RadialTurboFreeCAD: https://github.com/20jeka08
- CFturbo tutorial: https://cfturbo.com/fileadmin/content/down/tutorials/CFturbo_Axial_Impeller.pdf

### Motors
- SSS 4074: https://www.tflhobby.com/products/sss-4074-series-4-poles-inner-runner-brushless-motor-water-cooling-for-rc-boat-electric-surfboard
- SSS 4074 (Ali): https://www.aliexpress.com/item/32848316583.html
