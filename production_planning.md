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
