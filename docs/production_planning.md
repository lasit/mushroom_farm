# Mushroom Production Planning

Production planning documentation for calculating bag quantities, cycle timing, and financials.

## Growing Cycle Overview

The production cycle starts when grain spawn is added to a pasteurized substrate bag and ends when the bag is disposed of after harvesting.

```
[Inoculation] → [Incubation] → [Fruiting Room] → [Harvest Flush 1] → [Harvest Flush 2] → [Dispose]
```

### Cycle Stages

| Stage | Oyster | Lion's Mane | Description |
|-------|--------|-------------|-------------|
| Incubation | 2-3 weeks | 3-4 weeks | Bag colonizes in dark, warm conditions |
| Fruiting | 2-3 weeks | 3-4 weeks | Bag in fruiting room, 2 flushes harvested |
| **Total Cycle** | ~5 weeks | ~7 weeks | From inoculation to disposal |

### Flush Distribution

- **First flush**: ~60-70% of total yield
- **Second flush**: ~30-40% of total yield
- Third flush possible but often not worth the space/time

## Key Variables

### Biological Efficiency (BE)

Yield as a percentage of dry substrate weight.

| Variety | Conservative | Good | Excellent |
|---------|-------------|------|-----------|
| Oyster | 100% | 125% | 150%+ |
| Pink Oyster | 100% | 125% | 150%+ |
| Lion's Mane | 75% | 90% | 100%+ |

**Example**: 1kg dry substrate × 100% BE = 1kg fresh mushrooms

### Substrate Composition

For a typical 5kg hydrated bag:

| Component | Percentage | Weight |
|-----------|------------|--------|
| Water | 70-75% | 3.5-3.75kg |
| Dry substrate | 25-30% | 1.25-1.5kg |

**Dry substrate per bag** = Bag weight × Dry substrate %

Using 25% dry content: 5kg × 0.25 = **1.25kg dry substrate**

## Production Calculations

### Yield Per Bag

```
Yield per bag = Dry substrate weight × Biological Efficiency
```

**Example (Oyster)**:
- Dry substrate: 1.25kg
- BE: 100%
- Yield: 1.25kg × 1.0 = **1.25kg fresh mushrooms**

### Bags Needed Per Week

```
Bags per week = Target weekly output ÷ Yield per bag
```

**Example**: 20kg/week ÷ 1.25kg/bag = **16 bags/week**

### Total Bags in Rotation

```
Bags in rotation = Bags per week × Total cycle length (weeks)
```

**Example**: 16 bags/week × 5 weeks = **80 bags in rotation**

This is the total number of bags in your system at any time (incubation + fruiting combined).

### Bags in Fruiting Room

Not all bags are in the fruiting room at once. The proportion depends on cycle timing:

```
Bags in fruiting = Bags in rotation × (Fruiting weeks ÷ Total cycle weeks)
```

**Example (equal incubation/fruiting)**:
- 80 bags in rotation
- 2.5 weeks fruiting ÷ 5 weeks total = 50%
- Bags in fruiting: 80 × 0.5 = **40 bags**

**Example (longer fruiting)**:
- 80 bags in rotation
- 3 weeks fruiting ÷ 5 weeks total = 60%
- Bags in fruiting: 80 × 0.6 = **48 bags**

## Financial Calculations

### Cost Per Bag

| Cost Item | Oyster | Lion's Mane | Notes |
|-----------|--------|-------------|-------|
| Substrate | $2.50 | $3.00 | Straw/sawdust/supplements |
| Spawn | $1.50 | $2.00 | Grain spawn allocation |
| Bag & filter | $0.80 | $0.80 | Autoclavable grow bag |
| Labor | $1.00 | $1.50 | Time value |
| Utilities | $0.50 | $1.00 | Power, water, cooling |
| **Total** | **$6.30** | **$8.30** | Per bag |

Note: Lion's Mane has higher utility costs in Darwin due to cooling requirements (prefers 18-22°C).

### Cost Per Kilogram

```
Cost per kg = Total cost per bag ÷ Yield per bag
```

**Oyster**: $6.30 ÷ 1.25kg = **$5.04/kg**
**Lion's Mane**: $8.30 ÷ 1.0kg = **$8.30/kg**

This is your breakeven price.

### Revenue and Profit

```
Weekly revenue = Target kg × Sale price per kg
Weekly costs = Bags per week × Cost per bag
Weekly profit = Revenue - Costs
Profit margin = Profit ÷ Revenue
```

**Example (Oyster, 20kg/week @ $25/kg)**:
- Revenue: 20 × $25 = $500/week
- Costs: 16 bags × $6.30 = $100.80/week
- Profit: $500 - $100.80 = **$399.20/week**
- Margin: 399.20 ÷ 500 = **79.8%**

### Profit Per Bag

```
Profit per bag = (Sale price × Yield per bag) - Cost per bag
```

**Oyster**: ($25 × 1.25) - $6.30 = **$24.95/bag**

## Space Planning

### Fruiting Room Capacity

For a 3m × 3m room (9 sqm) with 4-tier shelving:

| Parameter | Value |
|-----------|-------|
| Floor space | 9 sqm |
| Bags per sqm (4-tier) | 10-12 bags |
| **Max capacity** | 90-108 bags |

### Space Check

```
Space utilization = Bags in fruiting ÷ Room capacity
```

If utilization exceeds 100%, you need to either:
- Reduce production targets
- Add more shelving tiers
- Expand room size
- Stagger production (not all varieties at full capacity)

## Combined Operation Example

Running both Oyster (20kg/week) and Lion's Mane (10kg/week):

| Metric | Oyster | Lion's Mane | Total |
|--------|--------|-------------|-------|
| Target kg/week | 20 | 10 | 30 |
| Bags/week | 16 | 10 | 26 |
| Bags in rotation | 80 | 70 | 150 |
| Bags in fruiting | 40 | 35 | 75 |
| Weekly profit | $399 | $267 | $666 |
| Monthly profit | $1,729 | $1,156 | $2,885 |

Space check: 75 bags in fruiting ÷ 108 capacity = **69% utilization** ✓

## Climate Control & Pre-Conditioning Room

### Fruiting Room Specifications

| Parameter | Value |
|-----------|-------|
| Dimensions | 2.95m × 3.15m × 1.95m |
| Volume | 18.12 m³ |
| Floor area | 9.29 m² |

### Environmental Requirements

| Parameter | Oyster | Lion's Mane |
|-----------|--------|-------------|
| Temperature | 18-24°C | 18-22°C |
| Humidity | 85-95% | 85-95% |
| CO2 (max) | <1000 ppm | <800 ppm |
| Air velocity | 0.1-0.3 m/s | 0.1-0.3 m/s |

### Airflow Calculation

Airflow is calculated based on **substrate load**, not room volume.

| Method | Airflow Required |
|--------|------------------|
| Single-zone (all blocks fruit together) | 250-300 m³/hr per ton of substrate |
| Mixed-age blocks | 180-220 m³/hr per ton of substrate |

**For this operation:**
- ~75 bags in fruiting at 5kg/bag = 375kg substrate
- Peak airflow needed: 375kg × 0.3 m³/hr/kg = **~110 m³/hr** (65 CFM)

Cross-check with air changes per hour:
- Minimum (6 ACH): 18.12 m³ × 6 = 109 m³/hr
- Maximum (10 ACH): 18.12 m³ × 10 = 181 m³/hr

**Design capacity: 150 m³/hr** (sized for peak demand with headroom)

### Demand-Based Ventilation (Actual Operation)

**Key insight:** Fans don't run at full speed continuously. CO2-based demand ventilation means:
- Fans run at **12% minimum** most of the time (backflow prevention)
- Only ramp up when CO2 exceeds setpoint (~1000 ppm)
- Peak ventilation is brief, not continuous

#### Actual Operating Profile

| Operating Mode | Fan Speed | Airflow | Time % | Trigger |
|----------------|-----------|---------|--------|---------|
| **Baseline** | 12% | ~25-30 m³/hr | 60-70% | Constant (backflow prevention) |
| **Moderate CO2** | 30-50% | ~50-80 m³/hr | 20-25% | CO2 800-1000 ppm |
| **High CO2 spike** | 70-100% | 100-150 m³/hr | 5-15% | CO2 >1000 ppm |

**Weighted average airflow: ~40-55 m³/hr** (not 150 m³/hr continuously)

#### Why This Works

Mushroom CO2 production varies throughout the day and growth cycle:
- **Pin formation:** Low respiration, minimal CO2
- **Active growth:** Moderate respiration, periodic flushing needed
- **Mature fruiting bodies:** Higher respiration, more frequent ventilation
- **Post-harvest:** CO2 drops quickly, fans return to minimum

The controller monitors CO2 continuously and responds proportionally, using only the ventilation actually needed.

### Pre-Conditioning Room Design

The pre-conditioning room provides cold, dry air to the fruiting room. The fruiting room then adds humidity (up to 95%) and exhausts CO2.

#### Sizing Guidelines

Pre-conditioning space is sized based on airflow. With demand-based ventilation, typical airflow is much lower than design maximum.

| Scenario | Airflow | Sizing Approach | Result |
|----------|---------|-----------------|--------|
| **Old assumption** (continuous) | 150 m³/hr | 2-3× per minute | 5-7.5 m³ |
| **Demand-based typical** | 40-55 m³/hr | 2-3× per minute | 1.3-2.8 m³ |
| **With equipment space** | - | AC + filter + clearance | +2 m³ |

#### Pre-Conditioning Room Specification

**Actual dimensions: 1.0m × 1.0m × 2.0m = 2.0 m³**

| Parameter | Value |
|-----------|-------|
| Width | 1.0m |
| Depth | 1.0m |
| Height | 2.0m |
| Volume | 2.0 m³ |
| Floor area | 1.0 m² |
| Insulation | 100mm panels (minimum) |
| Layout | Adjacent to fruiting room (shared wall), exterior brick wall on opposite side |
| Cooling | Kirby BA9 coolroom condensing unit (split system — evaporator inside, condenser outside) |

This room functions as a pure air conditioning plenum. The smaller volume is possible because the dedicated coolroom unit (low temperature differential evaporator) conditions air more effectively than a residential split AC, requiring less mixing volume.

**Equipment inside pre-con room:**
- Coolroom evaporator (wall-mounted on brick wall side)
- G4/F7 intake filter
- Temperature probe (coolroom controller)
- Temperature probe (Omni C20 monitoring)

**Equipment relocated outside pre-con room:**
- Coolroom condensing unit — mounted outside on brick wall (short copper pipe run through wall)
- Fog pump + 100L tank + UV sterilizer — relocated under the house (water line runs to fruiting room nozzles)
- Supply fan — now an in-duct EC fan in the 150mm supply duct (shared wall)

**Why 2 m³ works with a coolroom unit:**
- Low-TD evaporator (5.5°C vs 19°C for residential AC) requires less mixing volume
- Air is conditioned effectively in a single pass across the evaporator
- No bulky equipment inside the room — it's a pure air plenum
- 100mm insulation reduces heat gain (critical for 15°C target with 30°C+ ambient)
- At baseline ventilation (25-30 m³/hr), air dwell time is ~4 minutes — adequate for mixing

#### Energy Savings from Demand-Based Ventilation

| Component | Continuous (old) | Demand-Based | Savings |
|-----------|-----------------|--------------|---------|
| Fan energy | ~25W continuous | ~5W typical | 80% |
| AC load (ventilation) | 1.5kW average | 0.4kW average | 73% |
| Daily fan cost | ~$0.15 | ~$0.03 | $0.12/day |
| Daily AC cost (vent) | ~$4.30 | ~$1.15 | $3.15/day |
| **Annual savings** | - | - | **~$1,200/year** |

#### System Layout

```
[Outside Air 30-35°C]
       ↓
[G4/F7 Filter] ─── Removes dust, mold spores
       ↓
┌─────────────────────────────────────┐
│  PRE-CONDITIONING ROOM (2.0 m³)     │
│  1.0m × 1.0m × 2.0m                 │
│                                     │
│  ┌──────────────┐                   │
│  │  EVAPORATOR  │ ← Kirby BA9      │
│  │  (brick wall)│   coolroom unit   │
│  │  blows ═══►  │   (condenser     │
│  └──────┬───────┘    outside wall)  │
│         │ copper pipe through wall  │
│         │                           │
│    Cold air mixes ═══►              │
│              ═══► ═══►              │
│                       ↓             │
│         [150mm insulated duct] ─────┼──► To fruiting room
│         [In-duct EC supply fan]     │    (shared wall)
└─────────────────────────────────────┘

                         [HP Fog Line] ─── From fog pump (under house)
                              ↓
┌─────────────────────────────────────┐
│     FRUITING ROOM (18.12 m³)        │
│     2.95m × 3.15m × 1.95m           │
│                                     │
│  Fog nozzles → 85-95% RH            │
│  CO2 sensor → Triggers fan ramp-up  │
│  Circulation → Even distribution    │
│                                     │
│  [Exhaust EC Fan] ─── 12% baseline  │
│         ↓              +10% offset  │
└─────────┼───────────────────────────┘
          ↓
   [150mm Standard Duct]
          ↓
   [Backdraft Damper]
          ↓
   [Exhaust to Outside]
```

**Airflow path through pre-con room:**
The evaporator mounts on the brick wall (interior side), blowing cold air across the full width of the room. The supply duct is on the opposite wall (shared with fruiting room). This forces air to travel the full room width before exiting, ensuring proper mixing and preventing cold discharge air from entering the fruiting room unmixed.

### Fresh Air vs Recirculation

Mixing fresh air with recirculated room air reduces cooling load.

| Growth Phase | Fresh Air % | Recirculated % |
|--------------|-------------|----------------|
| First flush | 60-80% | 20-40% |
| Second flush | 40-50% | 50-60% |

Recirculated air is already at target temperature and humidity, reducing energy costs.

### Equipment Specifications

#### Pre-Conditioning Room

| Component | Specification | Purpose |
|-----------|---------------|---------|
| Coolroom evaporator | Kirby matched evaporator (inside pre-con room, on brick wall) | Cool air from 30-35°C → 15°C |
| Coolroom condensing unit | Kirby BA9MHYB1, 1/4 HP, R134a, 45°C ambient rated (outside brick wall) | Reject heat to outside |
| Coolroom controller | Carel IR33 or Dixell XR06CX (manages compressor, defrost, safety) | Refrigeration management |
| Pre-filter | G4 + F7 (3-stage with insect mesh) | Remove dust, mold spores from intake |
| Supply fan | 150mm in-duct EC fan, 0-10V control | Deliver air to fruiting room |
| Supply duct | 150mm insulated flex | Prevent condensation |
| Damper | Motorized (Belimo, 0-10V) | Control fresh air rate |

#### Fruiting Room

| Component | Specification | Purpose |
|-----------|---------------|---------|
| Humidifier | Ultrasonic or high-pressure fog | Maintain 85-95% RH |
| Exhaust fan | 160 m³/hr (90% of supply) | Remove CO2, maintain slight negative pressure |
| CO2 sensor | 0-5000ppm range | Trigger ventilation |
| Circulation fans | Low velocity | Even air distribution |

### Coolroom Sizing for Darwin Climate

**Unit: Kirby BA9MHYB1 condensing unit + matched evaporator**

| Specification | Value |
|---------------|-------|
| Compressor | 1/4 HP hermetic reciprocating |
| Refrigerant | R134a |
| Max ambient | 45°C (designed for Australian tropics) |
| Cooling capacity | ~700-1,000W at 15°C room / 35°C ambient |
| Power draw | 410W |
| Current | 2.6A (standard 10A plug) |
| Outdoor noise | 38.5 dB (quieter than a fridge) |
| Condensing unit dimensions | 330W × 470D × 276H mm |

Heat load calculation for 2 m³ pre-con room (100mm insulation):

```
Transmission (walls/ceiling): ~50-80W
Air infiltration:             ~30-50W
Product load (warm bags):     ~100-200W (intermittent)
Equipment (fan motors):       ~20-50W
Total steady-state:           ~100-200W
Peak load:                    ~400W
```

The Kirby BA9 delivers 700-1,000W at these conditions — comfortably oversized, meaning the compressor cycles lightly (20-40% duty cycle) and runs gently. This extends compressor life significantly.

**Why a coolroom unit instead of a residential split AC:**
- Designed for 24/7 continuous operation (residential ACs are not)
- 15°C is trivially easy (designed for 0-4°C)
- Low temperature differential (TD) evaporator strips less humidity from the air
- Built-in defrost cycles and compressor protection
- 10-15+ year lifespan at this light duty cycle
- Residential split ACs struggle below 16°C and risk evaporator icing in Darwin's heat

### Spore Protection

**Critical for oyster mushrooms:** Oyster mushrooms produce massive spore loads that:
- Clog evaporator fins
- Seize fan motors
- Require respirators for personnel

**Solutions:**
- Keep coolroom evaporator in separate pre-conditioning room (not in fruiting room)
- Install G4/F7 filters on fresh air intake
- Use positive pressure in pre-con room to prevent spore backflow
- Clean/replace filters regularly
- Condensing unit is outside the building — never exposed to spores

### Room Pressure: Negative for Fruiting

The fruiting room should maintain **slight negative pressure** to contain spores.

| Pressure Type | How It Works | Best For |
|---------------|--------------|----------|
| **Positive** | Intake > Exhaust, air pushes OUT through gaps | Labs, inoculation rooms (keeps contaminants OUT) |
| **Negative** | Exhaust > Intake, air is PULLED IN through gaps | Fruiting rooms (keeps spores CONTAINED) |

#### Why Negative Pressure for Fruiting?

Oyster mushrooms produce massive spore loads. Negative pressure ensures:
- Spores stay contained in the fruiting room
- Any air leaks draw filtered air IN (not spore-laden air OUT)
- Pre-conditioning room and rest of building stay spore-free
- No respirator needed outside the fruiting room

#### Pressure Zones

```
[OUTSIDE]           [PRE-CON ROOM]         [FRUITING ROOM]
 Ambient      →     Slight Positive    →    Slight Negative
                    (keeps spores out)      (contains spores)
```

### Intake vs Exhaust Fan Sizing

To achieve slight negative pressure with demand-based ventilation:

| Component | Design Capacity | Baseline (12%) | Moderate (50%) | Peak (100%) |
|-----------|----------------|----------------|----------------|-------------|
| Intake fan | 150 m³/hr | ~18 m³/hr | ~75 m³/hr | 150 m³/hr |
| Exhaust fan | 165 m³/hr | ~20 m³/hr | ~82 m³/hr | 165 m³/hr |

**EC Fan Speed Relationship:**

| Exhaust Speed | Intake Speed | Notes |
|---------------|--------------|-------|
| 12% (minimum) | 10% | Baseline backflow prevention |
| 50% | 45% | Moderate CO2 response |
| 100% | 90% | Peak ventilation burst |

The exhaust runs 10-15% faster at all speed levels, maintaining consistent negative pressure throughout the operating range.

**Practical setup:** Use same size EC fans, set exhaust to run 10-15% faster via controller offset.

### Duct Sizing

Air duct diameter based on maintaining 4-5 m/s airspeed at design capacity.

#### Formula

```
Duct Area = Airflow (m³/s) ÷ Velocity (m/s)
Diameter = √(4 × Area ÷ π)
```

#### Calculation Comparison

| Flow Scenario | Airflow | 100mm Velocity | 150mm Velocity |
|---------------|---------|----------------|----------------|
| **Peak (burst)** | 150 m³/hr | 5.3 m/s | 2.4 m/s |
| **Moderate** | 80 m³/hr | 2.8 m/s | 1.3 m/s |
| **Baseline (12%)** | 30 m³/hr | 1.1 m/s | 0.5 m/s |

#### Duct Size Options

| Size | Pros | Cons |
|------|------|------|
| **100mm** | Cheaper, easier to install | Noisier at peak, higher pressure drop |
| **125mm** | Good compromise | Non-standard, harder to source fittings |
| **150mm** | Quiet at all speeds, low pressure drop, future capacity | Larger, more expensive |

#### Recommendation: Keep 150mm Ducts

With demand-based ventilation, fans run at low speed most of the time. **150mm ducts provide:**

1. **Near-silent operation** - 0.5 m/s at baseline vs 1.1 m/s with 100mm
2. **Lower fan energy** - Less pressure drop = EC fans work less hard
3. **Peak capacity** - Still handles burst ventilation at comfortable 2.4 m/s
4. **Noise matters** - You're living upstairs; quiet operation is worth the cost

| Duct | Size | Type | Reasoning |
|------|------|------|-----------|
| **Intake** | 150mm | Insulated flex | Prevents condensation, quiet operation |
| **Exhaust** | 150mm | Standard flex | Same size, fan speed controls pressure |

Using same duct size simplifies construction. Control pressure with fan speed, not duct size.

#### Why Insulate Intake Duct?

Cold air (18-20°C) passing through duct in hot Darwin ambient (35°C+) causes condensation on duct exterior. Insulated duct prevents dripping.

Exhaust duct doesn't need insulation - hot humid air won't condense going outside.

### Complete Ventilation Layout

```
[OUTSIDE]                [PRE-CON ROOM 2.0 m³]        [FRUITING ROOM 18.12 m³]

  Condensing unit         ┌──────────────────┐        ┌──────────────────────────┐
  (Kirby BA9)             │                  │        │                          │
  outside brick    ○──────┤  EVAPORATOR      │        │  Cold dry air enters     │
  wall             copper │  blows ═══►      │ 150mm  │  high on wall            │
                   pipe   │                  │ insul. │         ↓                │
  Fresh air ═══►          │    ═══► ═══►   ──┼─duct──►│  Fog nozzles add RH      │
  (filtered)       G4/F7  │                  │ in-duct│         ↓                │
                   filter │                  │  EC    │  Air flows across shelves │
                          └──────────────────┘  fan   │         ↓                │
                                                      │  CO2/moisture accumulates │
                   BRICK WALL      SHARED WALL        │         ↓                │
                                                      │  Exhaust removes stale   │
                                                      └──────────┼───────────────┘
                                                                 │
                                                           150mm standard duct
                                                                 │
                                                           Exhaust EC fan (pulling)
                                                                 │
                                                     [TO OUTSIDE - spore-laden air]
```

### Fan Placement

**Key principle:** Keep fans OUT of the high-humidity, spore-laden fruiting room.

| Fan | Location | Action | Environment |
|-----|----------|--------|-------------|
| **Supply** | In-duct (150mm duct between pre-con and fruiting room) | Pushing | Cool, dry (15°C) |
| **Exhaust** | Outside fruiting room (in exhaust duct) | Pulling | Ambient |

**Why this matters:**
- Fruiting room is 85-95% RH with heavy spore load
- Fans in this environment fail quickly (moisture in bearings, spores clog motor)
- Placing fans outside the fruiting room extends lifespan significantly
- Supply fan moved to in-duct position because the pre-con room is now a compact 2 m³ plenum

**Air entry/exit points (inside fruiting room):**

| Point | Position | Reasoning |
|-------|----------|-----------|
| Supply inlet | High on wall | Cold air falls, distribute from top |
| Exhaust outlet | High on opposite wall | CO2 doesn't accumulate at floor level |
| Distance apart | 2.95-3.15m (room dimensions) | Cross-flow pattern |

**Room arrangement:**
- Pre-con room sits between the exterior brick wall and the fruiting room
- Evaporator on brick wall side, supply duct on shared wall side
- Condensing unit outside the brick wall (short copper pipe run)
- Supply duct: through shared wall (in-duct fan in this duct)
- Exhaust duct: 1-2m to external wall where exhaust fan is mounted

### Ventilation Control Options

#### Option A: Demand-Based EC Fans (Recommended)

**This is the approach for this project.**

- Both fans EC type with 0-10V speed control
- Controller modulates speed based on CO2 levels
- Baseline: 12% speed (backflow prevention only)
- Ramps up proportionally as CO2 rises
- 100% only during CO2 spikes

| Benefit | Impact |
|---------|--------|
| Energy savings | 73-80% reduction vs continuous |
| Noise reduction | Near-silent at baseline |
| Precise control | Proportional response to actual need |
| Longer fan life | Most hours at low speed |

#### Option B: Fixed Speed with Dampers

- Fixed speed fans
- Damper on intake restricts flow
- Exhaust runs unrestricted
- Simpler but wastes energy, can't respond to CO2

#### Option C: Passive Intake

- No intake fan - just filtered opening
- Exhaust fan creates negative pressure
- Air pulled through passive intake
- Can't pre-condition air, temperature swings

### Duct Resistance Adjustments

Add to fan CFM requirements:
- +5% per metre of ducting
- +30% for each 90° bend
- +15% for each 45° bend
- +25% if using carbon filter

**Example:** 150 m³/hr + 3m duct (+15%) + one 90° bend (+30%) = 150 × 1.45 = **218 m³/hr fan capacity needed**

## Scaling Considerations

### To increase output:

1. **Increase bags per week** - More pasteurization batches
2. **Improve BE** - Better substrate recipes, environmental control
3. **Reduce cycle time** - Optimize incubation conditions
4. **Add third flush** - Diminishing returns but possible

### Constraints to watch:

- **Fruiting room space** - Physical limit on bags
- **Pasteurization capacity** - How many bags can you prep per batch?
- **Labor time** - Solo operation limits
- **Spawn production** - Do you have enough grain spawn ready?

## Files

- `mushroom_calculator.xlsx` - Interactive spreadsheet with all formulas
  - **Oyster** sheet - Full calculator for oyster varieties
  - **Lions Mane** sheet - Full calculator for lion's mane
  - **Summary** sheet - Combined view and space check
  - **Scenario Planner** sheet - What-if analysis at different production levels
