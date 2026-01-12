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
- Airflow needed: 375kg × 0.3 m³/hr/kg = **~110 m³/hr** (65 CFM)

Cross-check with air changes per hour:
- Minimum (6 ACH): 18.12 m³ × 6 = 109 m³/hr
- Maximum (10 ACH): 18.12 m³ × 10 = 181 m³/hr

**Target airflow: 100-180 m³/hr (~60-105 CFM)**

### Pre-Conditioning Room Design

The pre-conditioning room provides cold, dry air to the fruiting room. The fruiting room then adds humidity (up to 95%) and exhausts CO2.

#### Sizing Guidelines

Pre-conditioning space is sized based on airflow, not as a simple ratio of room volume.

| Approach | Size Calculation | Result |
|----------|------------------|--------|
| Mixing box (minimum) | 2-3× airflow per minute | 6-9 m³ |
| Working room (25-30% of fruiting) | 18.12 × 0.25-0.30 | 4.5-5.4 m³ |
| With equipment clearance (30-40%) | 18.12 × 0.30-0.40 | 5.4-7.2 m³ |

**Recommendation: ~5-6 m³** (e.g., 1.5m × 1.5m × 2.2m)

#### System Layout

```
[Outside Air 35°C]
       ↓
[G3/F5 Pre-filter] ─── Removes dust, prevents spore backflow
       ↓
[PRE-CONDITIONING ROOM]
  ├── AC Unit (2.5-3.5kW inverter split)
  ├── Cools air to 18-20°C
  └── Dehumidifies (AC naturally removes moisture)
       ↓
[150mm Insulated Duct]
       ↓
[FRUITING ROOM 18.12 m³]
  ├── Humidifier → Adds moisture to 85-95% RH
  ├── Circulation fans → Even air distribution
  ├── CO2 sensor → Triggers exhaust at >1000ppm
  └── Exhaust fan → Removes CO2 and excess moisture
       ↓
[Exhaust to Outside]
```

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
| AC unit | 2.5-3.5kW inverter split | Cool from 35°C → 18-20°C |
| Pre-filter | G3 class | Remove dust from intake |
| Supply fan | 180 m³/hr, variable speed | Deliver air to fruiting room |
| Supply duct | 150mm insulated flex | Prevent condensation |
| Damper | Manual or motorized | Control airflow rate |

#### Fruiting Room

| Component | Specification | Purpose |
|-----------|---------------|---------|
| Humidifier | Ultrasonic or high-pressure fog | Maintain 85-95% RH |
| Exhaust fan | 160 m³/hr (90% of supply) | Remove CO2, maintain slight negative pressure |
| CO2 sensor | 0-5000ppm range | Trigger ventilation |
| Circulation fans | Low velocity | Even air distribution |

### AC Sizing for Darwin Climate

Cooling load calculation:

```
Cooling load = 1.08 × CFM × ΔT (°F)
             = 1.08 × 105 CFM × 27°F (35°C to 20°C)
             = ~3,000 BTU/hr

With safety factor (1.5-2×):
             = 5,000-6,000 BTU/hr (1.5-1.8kW)
```

**Recommendation: 2.5kW (8,500 BTU) minimum** for Darwin's extreme heat days.

### Spore Protection

**Critical for oyster mushrooms:** Oyster mushrooms produce massive spore loads that:
- Clog evaporator fins
- Seize fan motors
- Require respirators for personnel

**Solutions:**
- Keep AC unit in separate pre-conditioning room (not in fruiting room)
- Install G3 filter before heat exchanger
- Use positive pressure in pre-con room to prevent spore backflow
- Clean/replace filters regularly

### Duct Sizing

Air duct diameter based on maintaining 4-5 m/s airspeed:

```
Duct area = Airflow ÷ Air velocity
          = 180 m³/hr ÷ 4 m/s
          = 0.0125 m²
          = 125mm diameter (use 150mm for lower resistance)
```

**Recommendation: 150mm insulated flexible duct**

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
