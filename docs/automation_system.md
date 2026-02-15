# Mushroom Farm Automation System

Comprehensive automation design for the fruiting room climate control using the Innotech Omni BEMS controller.

## System Overview

### Controller Selection

**Innotech Omni C20 BEMS Controller**

| Specification | Value |
|---------------|-------|
| Model | OMC20 |
| Programmable Points | 20 UI/O |
| Expandable to | 70 UI/O (with U10 modules) |
| Communication | Dual Ethernet, BACnet, Modbus |
| Programming | Focus Logic Software |
| Power | 24VAC/DC |
| Estimated Cost | ~$3,000-4,000 AUD |

### Why Omni C20?

- 20 programmable points covers all requirements with spare capacity
- Australian company (Mass Electronics, Brisbane)
- Used by other mushroom farms (Sno-Valley Mushrooms, Open Support NZ)
- Software-based PID controllers (no external PID hardware needed)
- Real-time monitoring via web interface
- Runs independently once programmed (PC not required)

### Future Expansion Strategy

Starting with the C20 provides a cost-effective path with multiple expansion options:

**Option 1: Add Remote Expansion Modules (REM)**

The Omni U10 REM adds 10 programmable points per module:

| Spec | Detail |
|------|--------|
| Model | OMU10 |
| Points per module | 10 programmable UI/O |
| Max modules per C20 | 5 (adds 50 points → 70 total) |
| Power | 8W max per module |
| Mounting | DIN rail |
| Programming | Via Focus software (same as controller) |
| Estimated cost | ~$800-1,500 AUD per module |

**Note:** A feature licence may be required on the C20 to enable REM support - confirm with Innotech when purchasing.

**Option 2: Add Second C20 Controller**

For a completely separate room (e.g., second fruiting room):

- Connect via BACnet IP (Ethernet) or BACnet MS/TP (RS-485)
- Each controller runs independently but can share data
- Full redundancy - if one fails, the other keeps running
- ~$3,500 AUD for additional C20

**Expansion Scenarios**

| Scenario | Solution | Additional Cost |
|----------|----------|-----------------|
| Add 4-6 sensors to existing room | 1x U10 REM | ~$1,000-1,500 |
| Add incubation room monitoring | 1x U10 REM | ~$1,000-1,500 |
| Add second fruiting room | 2nd C20 controller | ~$3,500 |
| Full second room + sensors | 2nd C20 + U10 | ~$4,500-5,000 |

**Why C20 over C40?**

| Factor | C20 | C40 |
|--------|-----|-----|
| Base cost | ~$3,500 | ~$5,500 |
| Current needs (16 points) | Yes | Yes |
| Spare capacity | 4 points | 24 points |
| Expandable to | 70 points (with REMs) | 90 points (with REMs) |
| Savings | - | -$2,000 initial |

The C20 meets current requirements with room to grow. The $2,000 saved can fund a U10 REM later if needed, providing better value than buying unused capacity upfront.


### Room Specifications

| Room | Dimensions | Volume | Insulation |
|------|------------|--------|------------|
| **Fruiting Room** | 2.95m × 3.15m × 1.95m | 18.12 m³ | 150mm |
| **Pre-Conditioning Room** | 1.0m × 1.0m × 2.0m | 2.0 m³ | 100mm |

**Room Layout:** Pre-con room sits between the exterior brick wall and the fruiting room (shared wall). The coolroom condensing unit (Kirby BA9) mounts outside the brick wall; the evaporator mounts inside the pre-con room on the brick wall. Supply duct passes through the shared wall to the fruiting room.

### Fan Placement Strategy

Fans are positioned to keep them out of the high-humidity, spore-laden fruiting room environment.

| Fan | Location | Action | Environment | Why |
|-----|----------|--------|-------------|-----|
| **Supply** | In-duct (150mm supply duct, shared wall) | Pushing | Cool, dry (15°C) | Out of fruiting room, compact design |
| **Exhaust** | Outside fruiting room (in exhaust duct) | Pulling | Ambient | Avoids 90% RH + spores |

**Supply Fan (in-duct, pushing):**
- 150mm in-duct EC fan sits in the supply duct between pre-con room and fruiting room
- Lives in cool, dry air from coolroom evaporator
- Pushes conditioned air through 150mm insulated duct into fruiting room
- Moved to in-duct position because pre-con room is now a compact 2 m³ plenum

**Exhaust Fan (outside fruiting room, pulling):**
- Mounted in exhaust duct after it exits fruiting room wall
- Pulls humid, CO2-rich air out of fruiting room
- Fan stays in ambient environment, not 90% RH
- Spores pass through but don't accumulate on motor (exhaust direction)

```
[OUTSIDE]          [PRE-CON ROOM]              [FRUITING ROOM]
                   1.0m × 1.0m × 2.0m
                   ┌──────────────────┐        ┌──────────────────────────┐
  Condensing       │                  │        │                          │
  unit      ○──────┤  EVAPORATOR      │ 150mm  │  Fog nozzles (ceiling)   │
  (Kirby BA9)copper│  (brick wall)    │ insul. │                          │
             pipe  │  blows ═══►      ├─duct──►│  Racks + bags            │
                   │                  │in-duct │                          │
  Fresh air ═══►   │    ═══► ═══►     │EC fan  │                       ┌──────────┐
  (G4/F7 filter)   │                  │(push)  │                       │ EXHAUST  │
                   └──────────────────┘        │                  ───►│   FAN    │──► Out
                                               │  Air exits high      │  (pull)  │
                   BRICK WALL    SHARED WALL    │  (opposite wall)     └──────────┘
                                               └──────────────────────────┘
```

**Duct Lengths (adjacent rooms):**

| Duct | Length | Type | Notes |
|------|--------|------|-------|
| Supply | 0.5-1m | 150mm insulated flex | Through shared wall |
| Exhaust | 1-2m | 150mm standard | To external wall + fan |

### Demand-Based Ventilation

**Key insight:** Fans don't run at full speed continuously. CO2-based demand ventilation operates as follows:

| Operating Mode | Fan Speed | Airflow | Time % |
|----------------|-----------|---------|--------|
| **Baseline** | 12% | ~25-30 m³/hr | 60-70% |
| **Moderate CO2** | 30-50% | ~50-80 m³/hr | 20-25% |
| **High CO2 spike** | 70-100% | 100-150 m³/hr | 5-15% |

**Weighted average airflow: ~40-55 m³/hr** (not 150 m³/hr continuously)

This approach provides:
- 73-80% energy savings vs continuous ventilation
- Near-silent operation at baseline (fans barely audible)
- Longer fan life (most hours at low speed)
- ~$1,200/year savings in electricity

### Training Requirement

Innotech requires 2-day training before purchase. This covers:
- Focus Logic programming software
- I/O configuration
- PID loop tuning
- Monitoring and troubleshooting

Contact for training and purchase:
- **Innotech**: +61 7 3421 9100, sales@innotech.com
- **Cortrols (Melbourne)**: 03 9890 8544, info@cortrols.com.au

---

## I/O Configuration

### Input Summary

| Point | Type | Description | Signal | Range |
|-------|------|-------------|--------|-------|
| UI01 | AI | CO2 sensor - fruiting room | 4-20mA | 0-2000 ppm |
| UI02 | AI | Temperature - fruiting room | 4-20mA | 0-50°C |
| UI03 | AI | Humidity - fruiting room | 4-20mA | 0-100% RH |
| UI04 | AI | Temperature - pre-con room | 4-20mA | 0-50°C |
| UI05 | AI | Duct temperature (supply) | 4-20mA | 0-50°C |
| UI06 | DI | Door switch - fruiting room | Dry contact | NC |
| UI07 | DI | Door switch - pre-con room | Dry contact | NC |
| UI08 | DI | Humidifier low water alarm | Dry contact | NO |
| UI09 | DI | Coolroom alarm (high/low pressure, sensor fault) | Dry contact | NO |
| | | **Total Inputs: 9** | | |

### Output Summary

| Point | Type | Description | Signal | Load |
|-------|------|-------------|--------|------|
| UO01 | AO | Exhaust fan speed | 0-10V | EC fan |
| UO02 | AO | Supply fan speed | 0-10V | EC fan |
| UO03 | AO | Fresh air damper position | 0-10V | Belimo actuator |
| UO04 | AO | LED lights dimming | 0-10V | Dimmable driver |
| UO05 | DO | Humidifier control | 12VDC → RL12 relay → 240V | Mistify M-100 fog pump |
| UO06 | DO | Coolroom system enable/disable | 12VDC → RL12 relay → 240V | Coolroom controller power |
| UO07 | DO | Lights on/off | 12VDC → RL12 relay → 240V | Main switch |
| UO08 | DO | Alarm output | 12VDC → RL12 relay → 24V | Beacon/buzzer |

**Note:** The Omni C20 digital outputs are 12VDC (max 45mA). They cannot switch 240V directly. Each DO output drives an [Innotech Omni RL12](https://innotech.com/Products/ProductDetails.aspx?prodid=420) relay module (15.4mA coil, 3A @ 230VAC switching capacity) mounted on DIN rail in the controller enclosure. UO06 switches the coolroom controller's 240V power feed — de-energising UO06 cuts power to the coolroom controller, cleanly shutting down the entire refrigeration system.
| | | **Total Outputs: 8** | | |

### Point Utilization

```
Used:     17 points (9 inputs + 8 outputs)
Available: 20 points
Spare:     3 points (15% reserve for future)
```

---

## Control Logic

### 1. CO2-Based Ventilation

Primary control loop for fresh air exchange.

```
SENSOR: CO2 (4-20mA) → Universal Curve (4mA=0ppm, 20mA=2000ppm)
                              ↓
                        Linear Scale
                              ↓
         ┌────────────────────┴────────────────────┐
         ↓                                         ↓
   Exhaust Fan                              Duty Reducer
   (0-10V output)                                 ↓
                                           Supply Fan
                                           (0-10V output)
```

#### Setpoints

| CO2 Level | Exhaust Fan | Supply Fan | Notes |
|-----------|-------------|------------|-------|
| < 500 ppm | 12% | 10% | Minimum (fans need airflow) |
| 500-800 ppm | 12-40% | 10-30% | Normal operation |
| 800-1200 ppm | 40-70% | 30-50% | Elevated - ramp up |
| 1200-1500 ppm | 70-90% | 50-65% | High - aggressive venting |
| > 1500 ppm | 100% | 70% | Emergency - max exhaust |

#### Negative Pressure Ratio

Supply fan always runs slower than exhaust to maintain negative pressure:

| Exhaust % | Supply % | Ratio |
|-----------|----------|-------|
| 12% | 10% | 0.83 |
| 50% | 38% | 0.76 |
| 75% | 52% | 0.69 |
| 100% | 65% | 0.65 |

### 2. Temperature Control

**Dual-controller architecture:** The coolroom's dedicated controller (Carel IR33 or Dixell XR06CX) manages the compressor directly with proper refrigeration safety logic. The Omni C20 supervises, monitors, and can enable/disable the coolroom system.

```
COOLROOM CONTROLLER (independent):
  Own temp probe → Compressor on/off (with min on/off times, anti-short-cycle)
                → Defrost cycles
                → High/low pressure safety cutouts
                → Evaporator fan delay

OMNI C20 (supervisor):
  SENSOR: Temperature UI04 (pre-con room) → MONITOR + ALARM
  SENSOR: Temperature UI02 (fruiting room) → MONITOR + ALARM
  OUTPUT: UO06 (relay) → Coolroom controller power (enable/disable)
  INPUT:  UI09 → Coolroom alarm relay (fault detection)
```

**Why two controllers:** The Omni C20 is a building automation controller, not a refrigeration controller. It does not manage compressor minimum on/off times, defrost scheduling, or pressure safety — the coolroom controller handles all of this natively. This prevents compressor damage from improper cycling and provides an independent safety layer.

#### Coolroom Controller Settings (set by refrigeration technician)

| Parameter | Value |
|-----------|-------|
| Setpoint | 15°C |
| Differential | 2°C (compressor ON at 17°C, OFF at 15°C) |
| Minimum off time | 5 minutes |
| Minimum on time | 3 minutes |
| Defrost interval | 6-8 hours |
| Defrost type | Electric or hot gas |
| Fan delay after stop | 2-3 minutes |
| High pressure cutout | Auto-reset |
| Low pressure cutout | Manual-reset (requires investigation) |

#### Omni C20 Monitoring Setpoints

| Parameter | Oyster | Lion's Mane |
|-----------|--------|-------------|
| Target fruiting room temp | 20°C | 18°C |
| Pre-con room target | 15°C | 15°C |
| Deadband | ±1°C | ±1°C |
| Emergency high (fruiting) | > 26°C | > 24°C |
| Emergency low (fruiting) | < 15°C | < 14°C |
| Emergency low (pre-con) | < 10°C | < 10°C |

#### Omni C20 Logic

```
DEFAULT STATE:
  - UO06 = ENABLED (coolroom controller manages itself)
  - Coolroom runs independently

IF pre-con temp (UI04) > 20°C for > 10 minutes:
  - ALARM (coolroom not keeping up or has faulted)
  - Check UI09 (coolroom alarm input)

IF pre-con temp (UI04) < 10°C:
  - DISABLE coolroom via UO06 (freeze protection)
  - ALARM

IF fruiting room temp (UI02) > Emergency High:
  - ALARM
  - Max ventilation (fans to 100%)

IF coolroom alarm (UI09) triggered:
  - ALARM beacon ON (UO08)
  - Log event

IF pre-con door (UI07) OPEN > 5 minutes:
  - DISABLE coolroom via UO06 (prevent compressor running with door open)
  - ALARM
```

**Key advantage:** If the Omni C20 crashes or loses power, the coolroom controller keeps running independently — refrigeration continues without building automation. This eliminates a single point of failure for temperature control.

### 3. Humidity Control

PID control loop for humidity.

```
SENSOR: Humidity (4-20mA) → PID Controller → Humidifier (Relay)
                                   ↓
                            Exhaust Fan (adjustment)
```

#### Setpoints

| Parameter | Value |
|-----------|-------|
| Target RH | 90% |
| Deadband | ±3% |
| Humidifier ON | < 87% |
| Humidifier OFF | > 93% |
| Emergency high | > 98% |
| Emergency low | < 75% |

#### Logic

```
IF RH < 87%:
  - Humidifier ON
  - Reduce exhaust fan slightly (retain moisture)

IF RH > 93%:
  - Humidifier OFF

IF RH > 98%:
  - Humidifier OFF
  - Increase exhaust (remove excess moisture)
  - ALARM (check for water leak)

IF RH < 75%:
  - ALARM (humidifier fault?)
  - Check humidifier water level
```

### 4. Lighting Control

Schedule-based with optional dimming.

```
SCHEDULE → Light Relay (on/off)
              ↓
         Light Dimmer (0-10V) for intensity
```

#### Schedule

| Time | Lights | Intensity | Notes |
|------|--------|-----------|-------|
| 06:00 | ON | 50% | Dawn ramp |
| 07:00 | ON | 100% | Full light |
| 18:00 | ON | 50% | Dusk ramp |
| 19:00 | OFF | 0% | Night |

Total photoperiod: 12-13 hours (typical for fruiting)

### 5. Door Interlock

Safety logic to pause systems when door opens.

```
SENSOR: Door Switch (NC) → Logic Block
                              ↓
         ┌────────────────────┼────────────────────┐
         ↓                    ↓                    ↓
   Exhaust Fan 5%     Humidifier OFF    Supply Fan 5%
   (not OFF - backflow             (not OFF - backflow
    prevention)                     prevention)
```

#### Logic

```
IF Door Switch OPEN:
  - Exhaust fan → 5% (NOT OFF - prevents backflow)
  - Supply fan → 5% (NOT OFF - prevents backflow)
  - Humidifier → OFF
  - Lights → unchanged (for visibility)
  - Coolroom → unchanged (prevent temp spike; disable if door open > 5 min)
  - Start 30-second timer
  - Backdraft dampers provide additional protection

IF Door CLOSED:
  - Resume normal operation (fans return to CO2-based control)

IF Door OPEN > 5 minutes:
  - ALARM (door left open)
```

### 6. Alarm Conditions

| Condition | Priority | Action |
|-----------|----------|--------|
| CO2 > 2000 ppm | HIGH | Max ventilation, alarm beacon |
| Temp > 26°C | HIGH | Max cooling, alarm |
| Temp < 14°C | HIGH | Heating, alarm |
| RH > 98% | MEDIUM | Stop humidifier, increase exhaust |
| RH < 75% | MEDIUM | Check humidifier, alarm |
| Door open > 5 min | LOW | Alarm only |
| Humidifier low water | LOW | Alarm, stop humidifier |
| Sensor fault | HIGH | Alarm, safe mode |

### 7. Backflow Prevention

Preventing humid, spore-laden air from flowing back into the pre-conditioning room.

#### The Problem

When fans stop or slow down, natural convection can push hot humid air from the fruiting room back into the pre-conditioning room:

```
FANS RUNNING (Normal):
[Pre-con Room]  →→→  [Fruiting Room]  →→→  [Outside]
   Cold/Dry         Slight Negative         Exhaust
   Positive         Pressure

FANS OFF (Problem):
[Pre-con Room]  ←←←  [Fruiting Room]      [Outside]
   Gets humid!       Hot/Humid/Spores      No exhaust
                     can backflow
```

**Consequences of backflow:**
- Condensation on coolroom evaporator coils
- Spore buildup in pre-con room (oyster spores are aggressive)
- Coolroom efficiency drops
- Mold risk in ductwork

#### Solution: Continuous Operation + Backdraft Dampers

**Two-layer protection:**

1. **Fans never fully stop** - Minimum 10-12% speed maintains airflow and pressure
2. **Backdraft dampers** - Physical barriers that close when airflow stops

```
                   SUPPLY PATH
[Pre-con Room] → [Backdraft Damper] → [In-duct EC Fan] → [Fruiting Room]
     Coolroom       Spring-loaded        min 12%
     evaporator     closes when          always on
     creates        fan stops
     cold dry air

                   EXHAUST PATH
[Fruiting Room] → [Exhaust EC Fan] → [Backdraft Damper] → [Outside]
   humid air          min 12%          Spring-loaded
   + CO2              always on        prevents outdoor
   + spores                            air entering
```

#### Fan Minimum Speed Configuration

In the Omni Focus software Linear Scale block:

```
CO2 Input:     500 ppm (minimum) → 2000 ppm (maximum)
Fan Output:    12% (minimum)     → 100% (maximum)
                ↑
         NEVER goes to 0%
```

**Why 12% minimum?**
- EC fans need minimum airflow to cool motor
- Maintains slight negative pressure at all times
- Power consumption at 12% is negligible (~5-10W per fan)
- Barely audible at night

#### Door Interlock Exception

When door opens, fans can reduce to 5% (not 0%) to prevent backflow while minimizing humidity loss:

```
IF Door OPEN:
  - Exhaust fan → 5% (not OFF)
  - Supply fan → 5% (not OFF)
  - Backdraft dampers provide additional protection
```

---

## Equipment Specifications

### Sensors

#### CO2 Sensor

| Specification | Requirement |
|---------------|-------------|
| Type | NDIR (non-dispersive infrared) |
| Range | 0-2000 ppm (minimum) |
| Output | 4-20mA or 0-10V |
| Accuracy | ±50 ppm or ±3% |
| Response time | < 60 seconds |
| Power | 24VDC |
| Environment | High humidity rated (IP65+) |

**Recommended Products (Australia):**

| Product | Supplier | Output | Price (est) |
|---------|----------|--------|-------------|
| CDT-2N40 | Regulator Automation | 0-10V | ~$300-400 |
| Vaisala GMP251 | ESIS Australia | 4-20mA | ~$600-800 |
| Sensaphone CO2 | Sensaphone AU | 4-20mA | ~$400-500 |

**Australian Suppliers:**
- [Regulator Automation](https://regulatorautomation.com.au/) - CDT-2N40 CO2 sensor
- [ESIS Australia](https://www.esis.com.au/) - Vaisala products

#### Temperature & Humidity Sensor

| Specification | Requirement |
|---------------|-------------|
| Humidity range | 0-100% RH |
| Humidity accuracy | ±2% RH |
| Temperature range | -10 to 60°C |
| Temperature accuracy | ±0.3°C |
| Output | 4-20mA (2 channels) |
| Power | 24VDC |
| Mounting | Wall or duct |

**Recommended Products (Australia):**

| Product | Supplier | Outputs | Price (est) |
|---------|----------|---------|-------------|
| BAPI BA/H200 | Control Store AU | 2× 4-20mA | ~$250-350 |
| Vaisala HMD60 | ESIS Australia | 2× 4-20mA | ~$400-600 |
| Vaisala HMT120 | ESIS Australia | 2× 4-20mA | ~$600 |

**Australian Suppliers:**
- [ESIS Australia](https://www.esis.com.au/) - Vaisala HMD/HMT series
- [Control Store Australia](https://www.controlstore.com.au/) - BAPI sensors

#### Door Switch

| Specification | Requirement |
|---------------|-------------|
| Type | Magnetic reed switch |
| Contact | NC (normally closed) |
| Voltage rating | 24VDC |
| Gap distance | 15-25mm |
| Mounting | Surface mount |

**Recommended Products (Australia):**

| Product | Supplier | Price (est) |
|---------|----------|-------------|
| Magnetic Reed Switch NO/NC | Wiltronics | ~$10-20 |

**Australian Supplier:**
- [Wiltronics](https://www.wiltronics.com.au/) - Door reed switches

### Actuators

#### EC Inline Fans

| Specification | Requirement |
|---------------|-------------|
| Size | 150mm (6") |
| Type | EC motor (electronically commutated) |
| Control | 0-10V speed input |
| Airflow | 400-600 m³/hr (adjustable) |
| Power | 240V |
| Noise | < 40 dB(A) at 50% speed |

**Recommended Products (Australia):**

| Product | Supplier | Airflow | Price (est) |
|---------|----------|---------|-------------|
| Jetline Eco 150mm EC | Sherriff Electrical | 530 m³/hr | ~$300-400 |
| Sigilventus EC 150mm | Happy Hydroponics | 520 m³/hr | ~$250-350 |
| Fantech PowerLine EC | Fantech Australia | Various | ~$350-500 |
| Airvent EC 150mm | Airvent | 350 m³/hr | ~$200-300 |

**Australian Suppliers:**
- [Sherriff Electrical](https://shop.sherriff.com.au/) - Jetline EC fans
- [Happy Hydroponics](https://happyhydroponics.com.au/) - Sigilventus fans
- [Fantech Australia](https://www.fantech.com.au/) - PowerLine EC series
- [Airvent](https://airvent.com.au/) - EC inline fans

#### Damper Actuator

| Specification | Requirement |
|---------------|-------------|
| Torque | 2-5 Nm (for 150mm damper) |
| Control | 0-10V proportional |
| Voltage | 24VAC/DC |
| Rotation | 90° |
| Failsafe | Spring return (optional) |

**Recommended Products (Australia):**

| Product | Supplier | Torque | Price (est) |
|---------|----------|--------|-------------|
| Belimo LM24A-SR | Controls Traders | 5 Nm | ~$200-300 |
| Belimo TF24-SR | Control Store | 2 Nm | ~$150-200 |
| Siemens GDB... | Control Store | Various | ~$150-250 |

**Australian Suppliers:**
- [Controls Traders](https://www.controlstraders.com/) - Belimo actuators
- [Control Store Australia](https://www.controlstore.com.au/) - Belimo, Siemens

#### Humidification System (High-Pressure Fogging)

**Why High-Pressure Fogging over Ultrasonic?**

| Factor | Ultrasonic | High-Pressure Fog |
|--------|------------|-------------------|
| Droplet size | 1-5 microns | 5-15 microns |
| Wets surfaces? | Slightly | No (evaporates mid-air) |
| Mineral dust | Bad (white film on everything) | Minimal |
| Water quality needs | RO/distilled required | Filtered + UV |
| Maintenance | High (weekly tank cleaning) | Low (monthly nozzle check) |
| Bacteria risk | High (atomizes biofilm) | Low (UV sterilization) |
| Lifespan | 1-2 years | 10+ years |

High-pressure fog creates 5-15 micron droplets that evaporate before hitting surfaces - no wet walls, no contamination vectors.

| Specification | Requirement |
|---------------|-------------|
| Type | High-pressure fog (40-70 bar / 600-1000 PSI) |
| Droplet size | 5-15 microns |
| Flow rate | 0.5-1 L/min |
| Nozzles | 4-6 anti-drip stainless steel |
| Control | On/off (relay to pump) |
| Power | 240V |
| Water treatment | 5μm filter + UV sterilization |

**Recommended System: Mistify M-100**

| Specification | Value |
|---------------|-------|
| Model | M-100 |
| Price | $1,875 AUD |
| Nozzles included | 20 (use 4-6 for 9m² room) |
| Pressure | 40-70 bar |
| Flow rate | 1 L/min |
| Power | 180W |
| Control | Phone app + relay trigger |
| Noise | 55 dB |

**Alternative Options (Australia):**

| System | Supplier | Price | Notes |
|--------|----------|-------|-------|
| Mistify M-050 | Mistify | $1,495 | 14 nozzles, 0.5 L/min - minimum viable |
| Mistify M-100 | Mistify | $1,875 | 20 nozzles, recommended |
| MistKing Advanced | Aquatic Supplies AU | ~$700 | Mid-pressure (125 PSI), smaller droplets |
| Custom build | Various | ~$1,500 | DIY with AR pump + Irribiz nozzles |

**Australian Suppliers:**
- [Mistify](https://mistify.com.au/) - Complete high-pressure fog systems
- [Mistafog](https://mistafog.com.au/) - Custom commercial systems, mushroom farm experience
- [CoolMist Systems](https://www.coolmist.com.au/) - Greenhouse fog systems
- [Aquatic Supplies Australia](https://www.aquaticsupplies.com.au/) - MistKing systems

**Water Treatment (Required):**

| Component | Supplier | Price (est) |
|-----------|----------|-------------|
| 5μm Sediment Filter | Clarence Water Filters | ~$50 |
| UV Sterilizer (12LPM, 240V) | Shield Water Filter | ~$250 |
| Float valve + tank fittings | Bunnings/plumbing | ~$50 |

**Australian Water Treatment Suppliers:**
- [Clarence Water Filters](https://www.clarencewaterfilters.com.au/) - Filters and UV
- [Shield Water Filter](https://shieldwaterfilter.com.au/) - UV sterilizers
- [Water Filtration Solutions](https://waterfiltrationsolutions.com.au/) - Complete systems

**Installation Notes:**
- Mount nozzles on ceiling pointing down or at 45° angle toward walls
- Space nozzles 1-1.5m apart for even coverage
- Install UV sterilizer inline before pump inlet
- Use 5μm filter before UV (sediment blocks UV rays)
- Anti-drip nozzles prevent dripping when pump stops
- Connect pump power to Omni C20 output UO05 via RL12 relay (12VDC output drives RL12 coil, RL12 switches 240V to pump)

**Integration with Omni C20:**
```
Humidity Sensor (UI03) → PID Controller → Relay Output (UO05) → Fog Pump Power
                                ↓
                         Setpoint: 90% RH
                         Deadband: ±3%
                         On < 87%, Off > 93%
```

#### LED Grow Lights

| Specification | Requirement |
|---------------|-------------|
| Type | Full spectrum LED |
| Dimming | 0-10V input |
| Coverage | 9 m² room |
| Power | 150-300W total |
| Spectrum | 380-780nm (ePAR) |

**Recommended Products (Australia):**

| Product | Supplier | Power | Price (est) |
|---------|----------|-------|-------------|
| LUMii Switch Blade 150W | Hydro Experts | 150W | ~$200-300 |
| Mars Hydro SP Series | Mars Hydro AU | 150W | ~$200-250 |
| HLG 300L | Quick Bloom Lights | 300W | ~$500-700 |

**Note:** Not all LED grow lights have 0-10V dimming. Check specifications or use relay for on/off only.

**Australian Suppliers:**
- [Quick Bloom Lights](https://www.quickbloomlights.com.au/) - HLG lights
- [Mars Hydro AU](https://marshydroau.com/) - Mars Hydro lights
- [Hydro Experts](https://www.hydroexperts.com.au/) - Various brands

#### Backdraft Dampers

| Specification | Requirement |
|---------------|-------------|
| Size | 150mm (6") |
| Type | Spring-loaded butterfly |
| Material | Galvanized steel body, aluminum flaps |
| Mounting | Inline duct insertion |
| Orientation | Horizontal or vertical |

**Recommended Products (Australia):**

| Product | Supplier | Type | Price (est) |
|---------|----------|------|-------------|
| Fantech RSK150 | Rexel, CNW | Spring-loaded | ~$40-60 |
| Fantech SJK150 | Isupply Electrical | Gravity (low resistance) | ~$50-70 |
| AC Infinity 150mm | Quick Bloom Lights | Spring-loaded | ~$30-50 |
| Pacific Air 150mm | Pacific Air | Spring-loaded | ~$40-50 |

**Australian Suppliers:**
- [Rexel Australia](https://www.rexel.com.au/) - Fantech RSK150
- [CNW Electrical](https://shop.cnw.com.au/) - Fantech dampers
- [Quick Bloom Lights](https://www.quickbloomlights.com.au/) - AC Infinity dampers
- [Pacific Air](https://www.pacificair.com.au/) - Backdraft dampers
- [Hydro Experts](https://www.hydroexperts.com.au/) - Inline dampers

**Installation Notes:**
- Install with arrow pointing in direction of airflow
- Supply duct: arrow pointing toward fruiting room
- Exhaust duct: arrow pointing toward outside
- Ensure airtight seal with foil tape or mastic
- Position after fan (exhaust) or before fan (supply) for best effect

#### Coolroom Refrigeration System

Dedicated coolroom split system for temperature control in the pre-conditioning room. The condensing unit mounts outside the brick wall; the evaporator mounts inside the pre-con room. A standalone coolroom controller (Carel/Dixell) manages the refrigeration cycle independently.

| Specification | Requirement |
|---------------|-------------|
| Type | Split coolroom system (condensing unit + evaporator) |
| Capacity | 0.5-1.0 kW cooling at 15°C room / 35°C ambient |
| Max ambient rating | 45°C minimum (critical for Darwin) |
| Refrigerant | R134a |
| Designed for | 24/7 continuous operation |
| Control | Standalone coolroom controller + Omni enable/disable |
| Compressor type | Hermetic reciprocating (fixed speed) |

**Recommended System: Kirby BA9MHYB1 Condensing Unit + Matched Evaporator**

| Specification | Value |
|---------------|-------|
| Model | Kirby BA9MHYB1 (condensing unit) |
| Compressor | 1/4 HP hermetic reciprocating |
| Refrigerant | R134a |
| Max ambient | 45°C |
| Cooling capacity | ~700-1,000W at 15°C room / 35°C ambient |
| Power draw | 410W |
| Current | 2.6A (standard 10A circuit) |
| Outdoor noise | 38.5 dB LpA (quieter than a household fridge) |
| Condensing unit dimensions | 330W × 470D × 276H mm |
| Condensing unit weight | 18 kg |
| Connections | 3/8" suction, 1/4" liquid |
| Matched evaporator | Kirby KMA021 or KMT021 (selected by refrigeration tech) |
| Coolroom controller | Carel IR33 or Dixell XR06CX (~$80-150 AUD) |
| Price (condensing unit) | ~$940 AUD |
| Price (evaporator) | ~$400-600 AUD |
| Installation (by licensed tech) | ~$800-1,500 AUD |
| **Total installed** | **~$2,400-3,400 AUD** |

**Why Coolroom Refrigeration (Not Residential Split AC)?**
- Designed for 24/7 continuous operation (residential ACs are not)
- 15°C is trivially easy for a unit designed for 0-4°C
- Low temperature differential (TD) evaporator strips less humidity from air
- Built-in defrost cycles and compressor protection
- 10-15+ year lifespan at this light duty cycle
- Residential split ACs struggle below 16°C and risk evaporator icing
- 38.5 dB outdoor noise is quieter than a residential split (46-48 dB)

**Why Kirby?**
- Australian-made (Heatcraft Australia, part of Lennox International)
- Every refrigeration tech in Australia knows Kirby
- Parts stocked at Actrol Darwin (108 Reichardt Road, Winnellie)
- 45°C ambient rated — designed for Australian tropics
- Proven reliability — thousands running in Darwin right now

**Alternative Option: Zanotti MSP121T Split System**

| Specification | Value |
|---------------|-------|
| Type | Pre-packaged split coolroom system |
| Compressor | L'Unite Hermetique, 5/8 HP |
| Capacity | ~1,230W at 32°C ambient / +5°C room |
| Max ambient | 45°C |
| Pre-charged piping | 2.5m quick-connect (included) |
| Price (installed) | ~$3,100-4,500 AUD |
| Distributor | Bromic Refrigeration (Australia) |

The Zanotti is a higher-quality pre-packaged system but less common in Darwin. Parts come from Bromic (Melbourne/Sydney), not local Actrol stock.

**Noise Reference:**
- 38.5 dB = quiet whisper / rural background
- 46-48 dB = quiet library / light rain (residential split AC)
- 55-65 dB = normal conversation / standard coolroom unit

**Installation Notes:**
- Condensing unit mounts outside the brick wall on anti-vibration pads
- Evaporator mounts inside pre-con room on the brick wall (interior side)
- Copper piping runs through the brick wall (~300-500mm, very short)
- Core-drill brick wall for copper pipe penetrations (~15-20mm each)
- Seal penetrations to prevent insect/humidity ingress
- Condensate drain from evaporator to floor drain
- Coolroom controller mounts inside pre-con room or in controller enclosure
- Installation requires licensed refrigeration technician (ARCtick RHL for R134a)

**Darwin Refrigeration Technicians:**
- [CTM Refrigeration](https://www.ctmdarwin.com.au/) - Coolroom specialists since 1980
- [SJS Refrigeration](https://www.sjsrefrigeration.com) - 15 years commercial experience
- [Pro Cool NT](https://www.procoolnt.com.au/) - Commercial refrigeration
- [Baldwin Group NT](https://www.baldwingroupnt.com.au/) - Full refrigeration services

**Parts Supply:**
- [Actrol Darwin](https://www.actrol.com.au/) - 108 Reichardt Road, Winnellie NT — (08) 8935 2110
- Stocks Kirby condensing units, evaporators, Carel/Dixell controllers, copper, R134a

**Integration with Omni C20:**
```
COOLROOM CONTROLLER (independent):
  Own temp probe (pre-con room) → Compressor on/off
                                → Defrost management
                                → Safety cutouts (high/low pressure)
  Setpoint: 15°C, Differential: 2°C

OMNI C20 (supervisor):
  UI04 (pre-con temp) → Monitor + Alarm
  UI09 (coolroom alarm relay) → Fault detection → Alarm beacon (UO08)
  UO06 (relay) → Coolroom controller power feed (enable/disable)

  Default: UO06 ENABLED (coolroom runs independently)
  Disable if: pre-con temp < 10°C, pre-con door open > 5 min, emergency
```

#### Fog Pump Location (Under House, Outside Pre-Con Room)

The Mistify fog pump, 100L tank, and UV sterilizer are located outside the pre-conditioning room (under the house), due to the reduced pre-con room size (2.0 m³ pure air plenum). A high-pressure water line runs from the pump to fog nozzles in the fruiting room.

**Why outside the pre-con room?**

| Factor | Rationale |
|--------|-----------|
| Room size | 2.0 m³ pre-con room is a compact plenum — no space for tank + pump |
| Pump heat (180W) | No longer adding heat load to pre-con room |
| Maintenance access | Easier access to pump, tank, filters outside the sealed room |
| Plumbing | Water line routes directly to fruiting room nozzles |
| Protection | Under the house — sheltered from weather |

**Fog System Layout:**

```
  UNDER THE HOUSE (sheltered area)

  Mains water in
       │
  [Isolation Valve]
       │
  [Float Valve] ──► [100L Tank]
                          │
                     [5μm Filter]
                          │
                     [UV Sterilizer]
                          │
                     [Fog Pump] (wall-mounted, 180W)
                          │
                     HP line ──────────────────► Through wall to fruiting room nozzles
                                                 (4-6 anti-drip stainless nozzles)
```

**Noise Considerations:**

| Factor | Impact |
|--------|--------|
| Pump noise rating | 55 dB |
| Operation | Intermittent (only when RH < 87%) |
| Duty cycle | ~10-20% typical |
| Location | Under house, not in sealed room |
| Distance to upstairs | Significant attenuation through floor structure |
| **Result** | Inaudible upstairs during normal operation |

**Installation Notes:**
- Wall-mount pump above tank for gravity drain-back
- Vibration pads under pump recommended (~$20)
- HP line runs through wall to fruiting room nozzles
- Keep pump and tank accessible for maintenance
- Connect pump power to Omni relay output (UO05) via RL12 relay
- Run 240V power cable from controller enclosure to pump location

#### Ducting Materials

**Critical:** Galvanized steel corrodes within 2 years in high-humidity exhaust applications. Use corrosion-resistant materials.

| Duct | Type | Material | Why |
|------|------|----------|-----|
| **Supply** | Insulated flexible (R0.6-R1.0) | Foil + glass wool insulation | Prevents condensation, easy routing |
| **Exhaust** | Semi-rigid aluminium | 0.89mm aluminium | Corrosion resistant, smooth interior, cleanable |

**Duct Type Comparison:**

| Type | Airflow | Humidity Resistance | Cleanability | Price (150mm) |
|------|---------|---------------------|--------------|---------------|
| Semi-rigid aluminium | Good (smooth) | Excellent | Good | ~$48/3m |
| Insulated flexible | Moderate | Good | Poor (ribbed) | ~$59-89/6m |
| Galvanized spiral | Excellent | **Poor (corrodes)** | Excellent | ~$50-80/3m |
| PVC rigid | Good | Excellent | Good | ~$30-50/3m |

**Supply Duct - Insulated Flexible (R0.6 minimum):**

| Specification | Value |
|---------------|-------|
| Diameter | 150mm internal |
| Insulation | R0.6 to R1.0 |
| Temperature range | -10°C to +80°C |
| Length needed | 0.5-1m (through shared wall) |

Why insulated: Cold air (15°C) passing through warmer environment causes condensation on uninsulated duct. R0.6 is sufficient for short runs.

**Exhaust Duct - Semi-Rigid Aluminium:**

| Specification | Value |
|---------------|-------|
| Diameter | 150mm |
| Material thickness | 0.89mm aluminium |
| Temperature range | -70°C to +220°C |
| Standards | AS1668.1, AS1530.3 (4-Zero fire rated) |
| Length needed | 1-2m (to external wall) |

Why aluminium:
- Won't corrode in 85-95% RH exhaust air
- Smooth interior minimizes spore buildup
- Easy to wipe clean during maintenance
- Self-supporting with minimal sag

**Australian Suppliers:**

| Product | Supplier | Price | Notes |
|---------|----------|-------|-------|
| Insulated duct R0.6 (6m) | Pure Ventilation | $59 | Cut to length |
| Insulated duct R1.0 (6m) | Universal Fans | $69 | Higher R-value |
| Semi-rigid aluminium (3m) | Mitre 10 (Deflecto) | $48 | AS1668.1 compliant |
| Semi-rigid aluminium (3m) | Bunnings | ~$45 | In-store |

**Installation Notes:**
- Pull insulated flex tight to minimize turbulence
- Secure with metal clamps (not cable ties)
- Seal joints with aluminium tape (not duct tape)
- Slope exhaust duct slightly toward exit (drainage)
- Support semi-rigid duct every 1m to prevent sag

#### Fresh Air Intake Filtration

Prevents contamination from outside air entering the pre-conditioning room.

| Specification | Requirement |
|---------------|-------------|
| Filter stages | 3-stage (mesh + G4 + F7) |
| Insect mesh | Stainless steel, removable |
| Pre-filter | G4 pleated panel (>10um) |
| Fine filter | F7 pocket/bag (>1um, 80-90% mold spores) |
| Housing | Galvanized or plastic, accessible for changes |

**Filter Path:**
```
Outside Air -> [Insect Mesh] -> [G4 Pre-filter] -> [F7 Fine Filter] -> Pre-con Room
                  Clean            Replace            Replace
                  monthly          3-6 months         6-12 months
```

**Why F7 not HEPA?**
- HEPA creates excessive pressure drop for EC fans
- F7 captures 80-90% of mold spores (sufficient for mushroom cultivation)
- Lower cost, easier to source replacements

**Australian Suppliers:**
- [Camfil Australia](https://www.camfil.com/en-au/) - Commercial air filters
- [FilterFab](https://www.filterfab.com.au/) - Filter housings and media
- [Air Filter Factory](https://www.airfilterfactory.com.au/) - G4/F7 filters

#### Water Supply System

Auto-fill reservoir for the high-pressure fog system.

**Water Path:**
```
Mains -> [Isolation Valve] -> [Float Valve] -> [100L Tank] -> [5um Filter] -> [UV] -> Fog Pump
               |                    |               |
          Manual shutoff       Auto-fill      Food-grade
                               maintains      polyethylene
                               level
```

| Component | Specification |
|-----------|---------------|
| Tank | 100L food-grade polyethylene |
| Float valve | 1/2" brass, adjustable |
| Isolation valve | 1/2" ball valve |
| Overflow | 25mm fitting to floor drain |
| Level indicator | Visual sight tube or clear tank |

**Why a tank (not direct from mains)?**
- Buffers pressure fluctuations
- UV sterilizer needs consistent flow rate
- Visual confirmation of water level
- Easy to add treatment chemicals if needed

**Australian Suppliers:**
- [Bunnings](https://www.bunnings.com.au/) - Tanks, valves, fittings
- [Irrigation Warehouse](https://www.irrigationwarehouse.com.au/) - Float valves
- [Reece Plumbing](https://www.reece.com.au/) - Commercial fittings

#### Emergency Manual Overrides

Backup controls if the Omni controller fails.

| Override | Type | Function |
|----------|------|----------|
| Fan override | 3-position switch (OFF/AUTO/ON) | Force ventilation |
| Fog override | 3-position switch (OFF/AUTO/ON) | Emergency humidity |
| Coolroom override | 3-position switch (OFF/AUTO/ON) | Prevent overheating |
| Main isolator | Emergency stop (red mushroom) | Kill all systems |

**Wiring Concept:**
```
Omni Relay ----+
               |----[3-pos Switch]---- Load (Fan/Pump/AC)
Manual 240V ---+    OFF/AUTO/ON
```

**Location:** Mount override panel near door entry, outside high-humidity zone, at eye level.

#### Electrical Safety

Requirements for high-humidity environment (AS/NZS 3000 compliance).

| Requirement | Specification |
|-------------|---------------|
| RCD protection | 30mA on all circuits |
| Outlets/switches | IP65 minimum (dust-tight, water jet resistant) |
| Controller enclosure | IP65 with ventilation, mounted high |
| Junction boxes | IP65, sealed cable glands |
| Cable glands | IP68 rated |
| GPO height | Minimum 1.2m from floor |
| Labeling | All circuits clearly labeled |

**Australian Standards:**
- AS/NZS 3000 (Wiring Rules) - RCD protection required in wet areas
- AS/NZS 3012 - Electrical installations on construction sites

**Australian Suppliers:**
- [Clipsal](https://www.clipsal.com/) - IP65 outlets and switches
- [NHP](https://www.nhp.com.au/) - Industrial enclosures
- [RS Components](https://au.rs-online.com/) - IP68 cable glands

#### Spore Management

Oyster mushroom spores are respiratory irritants and colonize damp surfaces aggressively.

| Area | Management Strategy |
|------|---------------------|
| Exhaust duct | Smooth galvanized or PVC (easy to wipe clean) |
| Exhaust termination | Point downward, away from intake (min 3m separation) |
| Wall/ceiling surfaces | Wipe monthly with diluted bleach or H2O2 |
| Between batches | Full sanitization (fog with H2O2 or Virkon) |
| Personal protection | P2/N95 mask during heavy harvests |
| Work clothes | Dedicated clothing, wash separately |

**Sanitization Products:**
- Hydrogen peroxide 3-6% (food-safe)
- Virkon S (broad spectrum disinfectant)
- Sodium hypochlorite (bleach) diluted 1:10

#### Workflow Considerations

Optimized for stainless steel racks on castors.

| Consideration | Recommendation |
|---------------|----------------|
| Floor surface | Sealed, smooth concrete (no catching wheels) |
| Door threshold | Flush or ramped entry (no lip) |
| Turning space | Minimum 1.5m clear for rack rotation |
| Rack spacing | 300-400mm between racks for airflow |
| Parking positions | Mark floor with tape for consistent placement |
| Wheel locks | Engage during fruiting cycle |
| Cleaning access | Racks fully removable for room sanitization |

**Rack Specifications:**

| Spec | Requirement |
|------|-------------|
| Material | 304 stainless steel |
| Shelves | 4-5 tiers, ventilated/mesh |
| Load capacity | 150kg+ total |
| Castors | 100mm, 2 locking |
| Width | To fit door with 50mm clearance each side |

**Australian Suppliers:**
- [Mantova](https://www.mantova.com.au/) - Commercial kitchen racks
- [StoreSafe](https://www.storesafe.com.au/) - Industrial shelving
- [Vogue Australia](https://www.vogueaustralia.com.au/) - Stainless steel racks

---

## Wiring Diagram

### Controller Connections

```
                    ┌─────────────────────────────────────────┐
                    │         INNOTECH OMNI C20               │
                    │                                         │
   SENSORS          │  INPUTS                    OUTPUTS      │        ACTUATORS
                    │                                         │
┌─────────────┐     │                                         │     ┌─────────────┐
│ CO2 Sensor  │────►│ UI01 (4-20mA)     UO01 (0-10V) │────►│ Exhaust Fan │
│ 4-20mA      │     │                                         │     │ EC 0-10V    │
└─────────────┘     │                                         │     └─────────────┘
                    │                                         │
┌─────────────┐     │                                         │     ┌─────────────┐
│ Temp/RH     │────►│ UI02 (4-20mA)     UO02 (0-10V) │────►│ Supply Fan  │
│ Sensor      │────►│ UI03 (4-20mA)                           │     │ EC 0-10V    │
└─────────────┘     │                                         │     │ (in-duct)   │
                    │                                         │     └─────────────┘
                    │                                         │
┌─────────────┐     │                                         │     ┌─────────────┐
│ Pre-con     │────►│ UI04 (4-20mA)     UO03 (0-10V) │────►│ Damper      │
│ Temp        │     │                                         │     │ Actuator    │
└─────────────┘     │                                         │     └─────────────┘
                    │                                         │
┌─────────────┐     │                                         │     ┌─────────────┐
│ Duct Temp   │────►│ UI05 (4-20mA)     UO04 (0-10V) │────►│ LED Dimmer  │
└─────────────┘     │                                         │     └─────────────┘
                    │                                         │
┌─────────────┐     │                                         │     ┌─────────────────────┐
│ Door Switch │────►│ UI06 (DI)         UO05 (12V) │──►[RL12]──►│ Fog Pump (240V)  │
│ NC Contact  │     │                                         │     └─────────────────────┘
└─────────────┘     │                                         │
                    │                                         │     ┌─────────────────────┐
┌─────────────┐     │                                         │     │ Coolroom Controller  │
│ Pre-con     │────►│ UI07 (DI)         UO06 (12V) │──►[RL12]──►│ Power (240V)     │
│ Door Switch │     │                                         │     │ (enable/disable)     │
└─────────────┘     │                                         │     └─────────────────────┘
                    │                                         │
┌─────────────┐     │                                         │     ┌─────────────────────┐
│ Humidifier  │────►│ UI08 (DI)         UO07 (12V) │──►[RL12]──►│ Lights (240V)    │
│ Low Water   │     │                                         │     └─────────────────────┘
└─────────────┘     │                                         │
                    │                                         │     ┌─────────────────────┐
┌─────────────┐     │                                         │     │ Alarm Beacon         │
│ Coolroom    │────►│ UI09 (DI)         UO08 (12V) │──►[RL12]──►│ (24V)            │
│ Alarm Relay │     │                                         │     └─────────────────────┘
└─────────────┘     │                                         │
                    │                                         │
                    │  [RL12] = Innotech Omni RL12 relay      │
                    │          (DIN rail, 3A @ 230VAC)         │
                    │                                         │
                    │  ETHERNET ◄────────────────────────────►│ PC/Monitoring
                    │                                         │
                    │  POWER: 24VAC/DC                        │
                    └─────────────────────────────────────────┘

COOLROOM CONTROLLER (Carel IR33 / Dixell XR06CX) — independent system:
  ┌───────────────────────────────────────────────────┐
  │  Power: 240V via Omni UO06 relay (enable/disable) │
  │  Temp probe: NTC in pre-con room                   │
  │  Output 1: Compressor contactor (240V)             │
  │  Output 2: Evaporator fan                          │
  │  Output 3: Defrost heater (if electric defrost)    │
  │  Alarm relay: → Omni UI09 (fault notification)     │
  │  Inputs: High pressure switch, Low pressure switch │
  └───────────────────────────────────────────────────┘
```

### Power Distribution

```
┌─────────────────────────────────────────────────────────────────┐
│                    MAIN DISTRIBUTION BOARD                       │
│                                                                  │
│  240V 10A ──► Exhaust Fan (EC)                                  │
│  240V 10A ──► Supply Fan (EC)                                   │
│  240V 10A ──► Coolroom Controller → Compressor + Evap Fan        │
│  240V 10A ──► Humidifier                                        │
│  240V 10A ──► LED Lights                                        │
│  240V 10A ──► 24V Power Supply (for controller & sensors)       │
│                    │                                             │
│                    ▼                                             │
│              ┌──────────┐                                        │
│              │ 24VDC PSU│                                        │
│              │ 5A       │                                        │
│              └────┬─────┘                                        │
│                   │                                              │
│                   ├──► Omni C20 Controller                       │
│                   ├──► CO2 Sensor                                │
│                   ├──► Temp/RH Sensors                           │
│                   ├──► Damper Actuator                           │
│                   └──► Door Switches                             │
└─────────────────────────────────────────────────────────────────┘
```

---

## Bill of Materials

### Controller & Infrastructure

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| Innotech Omni C20 | 1 | $3,500 | $3,500 |
| Focus Software License | 1 | Incl. training | - |
| Training (2 days) | 1 | Incl. with purchase | - |
| 24V Power Supply 5A | 1 | $80 | $80 |
| DIN Rail Enclosure | 1 | $150 | $150 |
| **Subtotal** | | | **$3,730** |

### Sensors

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| CO2 Sensor (NDIR, 4-20mA) | 1 | $400 | $400 |
| Temp/RH Sensor (BAPI) | 2 | $300 | $600 |
| Duct Temp Sensor | 1 | $100 | $100 |
| Door Switch (NC) | 2 | $20 | $40 |
| **Subtotal** | | | **$1,140** |

### Actuators

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| EC Fan 150mm (Exhaust) | 1 | $350 | $350 |
| EC Fan 150mm (Supply) | 1 | $350 | $350 |
| Backdraft Damper 150mm | 2 | $50 | $100 |
| Damper 150mm + Actuator | 1 | $300 | $300 |
| LED Grow Light (dimmable) | 1 | $300 | $300 |
| **Subtotal** | | | **$1,400** |

### Humidification System

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| Mistify M-100 Fog System | 1 | $1,875 | $1,875 |
| 5μm Sediment Filter | 1 | $50 | $50 |
| UV Sterilizer (12LPM, 240V) | 1 | $250 | $250 |
| Float valve + tank fittings | 1 | $50 | $50 |
| **Subtotal** | | | **$2,225** |

### Wiring & Accessories

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| Shielded cable (4-20mA) | 50m | $3/m | $150 |
| Control cable (0-10V) | 30m | $2/m | $60 |
| Innotech Omni RL12 relay (DIN rail, 250VAC/3A) | 4 | $40 | $160 |
| Cable glands, terminals | 1 lot | $100 | $100 |
| **Subtotal** | | | **$470** |

### Ducting

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| Insulated flex duct R0.6 150mm (6m) | 1 | $59 | $59 |
| Semi-rigid aluminium 150mm (3m) | 1 | $48 | $48 |
| Metal clamps 150mm | 4 | $5 | $20 |
| Aluminium tape | 1 | $15 | $15 |
| Wall flanges/grilles | 2 | $20 | $40 |
| **Subtotal** | | | **$182** |

### Infrastructure & Safety

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| Intake filter housing + G4/F7 | 1 | $200 | $200 |
| Water tank 100L + float valve | 1 | $100 | $100 |
| Overflow fitting + drain line | 1 | $30 | $30 |
| Manual override panel (3x switches) | 1 | $150 | $150 |
| IP65 controller enclosure | 1 | $180 | $180 |
| IP65 outlets (x4) | 4 | $40 | $160 |
| IP68 cable glands (pack) | 1 | $50 | $50 |
| **Subtotal** | | | **$870** |

### Coolroom Refrigeration System

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| Kirby BA9MHYB1 condensing unit (1/4 HP, R134a) | 1 | $940 | $940 |
| Kirby matched evaporator (KMA021 or KMT021) | 1 | $500 | $500 |
| Coolroom controller (Carel IR33 or Dixell XR06CX) | 1 | $120 | $120 |
| NTC temperature probe (for coolroom controller) | 1 | $30 | $30 |
| Copper piping, fittings, refrigerant (R134a) | 1 lot | $250 | $250 |
| Installation by licensed refrigeration tech | 1 | $1,200 | $1,200 |
| Anti-vibration pads (condensing unit) | 1 | $40 | $40 |
| **Subtotal** | | | **$3,080** |

### Fog Pump Installation (Under House)

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| Vibration isolation pads | 1 | $20 | $20 |
| Wall mounting bracket | 1 | $30 | $30 |
| HP line extension (pump to fruiting room nozzles) | 1 lot | $80 | $80 |
| 240V power run (controller enclosure to pump) | 1 | $50 | $50 |
| **Subtotal** | | | **$180** |

*Note: Fog pump relocated outside pre-con room due to compact 2 m³ plenum design. Water line runs from pump location under the house to fruiting room nozzles.*

### Backup Sensors & Spares

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| Temp/RH Sensor (spare) | 1 | $300 | $300 |
| CO2 Sensor (spare) | 1 | $400 | $400 |
| Door Switch (spare) | 2 | $20 | $40 |
| UV Lamp (spare) | 1 | $80 | $80 |
| Fog nozzles (spare pack) | 1 | $50 | $50 |
| Sediment filter cartridges (3-pack) | 1 | $30 | $30 |
| **Subtotal** | | | **$900** |

### Total Estimated Cost

| Category | Cost (AUD) |
|----------|------------|
| Controller & Infrastructure | $3,730 |
| Sensors | $1,140 |
| Actuators (fans, dampers, lights) | $1,400 |
| Humidification System | $2,225 |
| Wiring & Accessories | $470 |
| Ducting | $182 |
| Infrastructure & Safety | $870 |
| Coolroom Refrigeration System | $3,080 |
| Fog Pump Installation | $180 |
| Backup Sensors & Spares | $900 |
| **TOTAL** | **$14,177** |
| Contingency (15%) | $2,127 |
| **GRAND TOTAL** | **$16,304** |

---

## Implementation Steps

### Phase 1: Planning & Procurement (2-4 weeks)

1. Contact Innotech for training schedule and controller purchase
2. Order all sensors and actuators from Australian suppliers
3. Design final wiring layout
4. Prepare mounting locations in fruiting room

### Phase 2: Training (2 days)

1. Complete Innotech Focus software training
2. Obtain software license
3. Practice with example configurations

### Phase 3: Installation (1-2 weeks)

1. Install DIN rail enclosure and controller
2. Run cables to sensor locations
3. Mount sensors (CO2, Temp/RH)
4. Install EC fans with 0-10V control cables
5. Install damper and actuator
6. Install door switches
7. Connect humidifier relay
8. Connect AC unit relay

### Phase 4: Programming (1 week)

1. Configure I/O points in Focus software
2. Build control logic (CO2 → fans, etc.)
3. Set up PID loops for temperature and humidity
4. Create lighting schedule
5. Program door interlock logic
6. Configure alarms

### Phase 5: Commissioning (1 week)

1. Upload configuration to controller
2. Verify all sensors read correctly
3. Test each output individually
4. Tune PID loops (temperature, humidity)
5. Test door interlock
6. Test alarm conditions
7. Monitor for 48-72 hours under load

### Phase 6: Documentation & Handover

1. Document final configuration
2. Back up Focus project file
3. Create operator guide
4. Establish maintenance schedule

---

## Maintenance Schedule

| Task | Frequency |
|------|-----------|
| Check sensor readings vs portable meter | Weekly |
| Check fog nozzles for clogs | Weekly |
| Check water tank level and float valve | Weekly |
| Check fog pump operation | Weekly |
| Clean insect mesh on intake | Monthly |
| Clean CO2 sensor | Monthly |
| Check door switch operation | Monthly |
| Backup controller configuration | Monthly |
| Wipe walls/ceiling (spore management) | Monthly |
| Inspect exhaust duct interior (spores) | Monthly |
| Clean coolroom evaporator coils | Monthly |
| Replace G4 pre-filter | 3-6 months |
| Check fan bearings/clean | 6 months |
| Coolroom professional service (condenser clean, refrigerant check) | 6-12 months |
| Replace F7 fine filter | 6-12 months |
| Replace UV lamp | 12 months |
| Calibrate CO2 sensor | Annually |
| Full room sanitization | Between batches |
| Replace humidity sensor element | 2-3 years |

---

## Troubleshooting

| Symptom | Possible Cause | Solution |
|---------|---------------|----------|
| CO2 reading stuck at 0 | Sensor fault, wiring | Check 4-20mA loop, power |
| Fans not responding | 0-10V cable, EC board | Check voltage at fan, wiring |
| Humidity won't reach setpoint | Humidifier fault, airflow too high | Check water level, reduce exhaust |
| Temperature swings | Coolroom controller differential too wide, defrost cycle | Adjust coolroom controller differential, check defrost settings |
| Door interlock not working | Switch gap, wiring | Adjust magnet distance, check NC contact |

---

## References

- [Innotech Omni BEMS Platform](https://innotech.com/Products/Digital/Omni-BEMS-Platform.aspx)
- [Sno-Valley Mushrooms FungusBot](https://www.snovalleymushrooms.com/general-6) - Omni controller for mushroom farms
- [Open Support NZ](https://www.youtube.com/watch?v=-zPPu4fNCPM) - Video walkthrough of Omni in mushroom farm
- [ESIS Australia - Vaisala Sensors](https://www.esis.com.au/)
- [Fantech Australia - EC Fans](https://www.fantech.com.au/)
- [Control Store Australia - Actuators](https://www.controlstore.com.au/)
