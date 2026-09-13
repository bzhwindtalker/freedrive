# Foil Assist Jet System — Research

Research on water jet / impeller propulsion for foil assist system.
Context: Freedrive S4 jet duct concept, comparison with Flite AMP,
and smaller-diameter (40-60mm) impeller options for reduced system thickness.

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
| Max power | 2.66kW | ~1.5-2kW (est) |
| Max thrust | ~25kg | 25kg (confirmed) |
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

### Where Freedrive wins
- Price (10-15x cheaper)
- Continuous throttle control (vs 10s fixed cycle)
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

---

## 7. Links

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
