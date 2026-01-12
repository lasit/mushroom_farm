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
| | | **Total Inputs: 8** | | |

### Output Summary

| Point | Type | Description | Signal | Load |
|-------|------|-------------|--------|------|
| UO01 | AO | Exhaust fan speed | 0-10V | EC fan |
| UO02 | AO | Supply fan speed | 0-10V | EC fan |
| UO03 | AO | Fresh air damper position | 0-10V | Belimo actuator |
| UO04 | AO | LED lights dimming | 0-10V | Dimmable driver |
| UO05 | DO | Humidifier control | Relay 240V | Ultrasonic unit |
| UO06 | DO | AC unit control | Relay 240V | Split system |
| UO07 | DO | Lights on/off | Relay 240V | Main switch |
| UO08 | DO | Alarm output | Relay 24V | Beacon/buzzer |
| | | **Total Outputs: 8** | | |

### Point Utilization

```
Used:     16 points (8 inputs + 8 outputs)
Available: 20 points
Spare:     4 points (20% reserve for future)
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

PID control loop for temperature.

```
SENSOR: Temperature (4-20mA) → PID Controller → AC Unit (Relay)
                                     ↓
                              Fresh Air Damper (0-10V)
```

#### Setpoints

| Parameter | Oyster | Lion's Mane |
|-----------|--------|-------------|
| Target temp | 20°C | 18°C |
| Deadband | ±1°C | ±1°C |
| Cooling trigger | > 21°C | > 19°C |
| Heating trigger | < 19°C | < 17°C |
| Emergency high | > 26°C | > 24°C |
| Emergency low | < 15°C | < 14°C |

#### Logic

```
IF Temp > Target + 1°C:
  - AC cooling ON
  - Fresh air damper OPEN (if outside cooler)

IF Temp < Target - 1°C:
  - AC heating ON (if heat pump)
  - Fresh air damper CLOSE

IF Temp > Emergency High:
  - ALARM
  - Max ventilation
  - AC max cooling
```

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
  - AC → unchanged (prevent temp spike)
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
- Condensation on AC evaporator coils
- Spore buildup in pre-con room (oyster spores are aggressive)
- AC efficiency drops
- Mold risk in ductwork

#### Solution: Continuous Operation + Backdraft Dampers

**Two-layer protection:**

1. **Fans never fully stop** - Minimum 10-12% speed maintains airflow and pressure
2. **Backdraft dampers** - Physical barriers that close when airflow stops

```
                   SUPPLY PATH
[Pre-con Room] → [Backdraft Damper] → [Supply EC Fan] → [Fruiting Room]
     AC unit        Spring-loaded        min 12%
     creates        closes when          always on
     cold dry air   fan stops

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

#### Humidifier

| Specification | Requirement |
|---------------|-------------|
| Type | Ultrasonic cool mist |
| Output | 3-6 kg/hr mist |
| Tank/feed | Auto-fill or large tank |
| Control | On/off (relay) or 0-10V |
| Power | 240V |

**Recommended Products (Australia):**

| Product | Supplier | Output | Price (est) |
|---------|----------|--------|-------------|
| Industrial Ultrasonic 6kg/hr | Hydro Experts | 6 kg/hr | ~$400-600 |
| Mars Hydro 6L Smart | Mars Hydro AU | 0.5 kg/hr | ~$100-150 |

**Note:** For 0-10V control, you may need to use a relay with PWM timer, or contact industrial humidifier suppliers (Condair, Carel) for modulating units.

**Australian Suppliers:**
- [Hydro Experts](https://www.hydroexperts.com.au/) - Industrial humidifiers
- [Mars Hydro AU](https://marshydroau.com/) - Grow room humidifiers

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
└─────────────┘     │                                         │     └─────────────┘
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
┌─────────────┐     │                                         │     ┌─────────────┐
│ Door Switch │────►│ UI06 (DI)         UO05 (Relay) │────►│ Humidifier  │
│ NC Contact  │     │                                         │     │ 240V        │
└─────────────┘     │                                         │     └─────────────┘
                    │                                         │
┌─────────────┐     │                                         │     ┌─────────────┐
│ Pre-con     │────►│ UI07 (DI)         UO06 (Relay) │────►│ AC Unit     │
│ Door Switch │     │                                         │     │ 240V        │
└─────────────┘     │                                         │     └─────────────┘
                    │                                         │
┌─────────────┐     │                                         │     ┌─────────────┐
│ Humidifier  │────►│ UI08 (DI)         UO07 (Relay) │────►│ Lights      │
│ Low Water   │     │                                         │     │ 240V        │
└─────────────┘     │                                         │     └─────────────┘
                    │                                         │
                    │                   UO08 (Relay) │────►│ Alarm       │
                    │                                         │     │ Beacon      │
                    │                                         │     └─────────────┘
                    │                                         │
                    │  ETHERNET ◄────────────────────────────►│ PC/Monitoring
                    │                                         │
                    │  POWER: 24VAC/DC                        │
                    └─────────────────────────────────────────┘
```

### Power Distribution

```
┌─────────────────────────────────────────────────────────────────┐
│                    MAIN DISTRIBUTION BOARD                       │
│                                                                  │
│  240V 10A ──► Exhaust Fan (EC)                                  │
│  240V 10A ──► Supply Fan (EC)                                   │
│  240V 10A ──► AC Unit                                           │
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
| Humidifier (Industrial) | 1 | $500 | $500 |
| LED Grow Light (dimmable) | 1 | $300 | $300 |
| **Subtotal** | | | **$1,900** |

### Wiring & Accessories

| Item | Qty | Unit Price (AUD) | Total (AUD) |
|------|-----|------------------|-------------|
| Shielded cable (4-20mA) | 50m | $3/m | $150 |
| Control cable (0-10V) | 30m | $2/m | $60 |
| Relay module (240V, 4ch) | 1 | $80 | $80 |
| Cable glands, terminals | 1 lot | $100 | $100 |
| **Subtotal** | | | **$390** |

### Total Estimated Cost

| Category | Cost (AUD) |
|----------|------------|
| Controller & Infrastructure | $3,730 |
| Sensors | $1,140 |
| Actuators (incl. backdraft dampers) | $1,900 |
| Wiring & Accessories | $390 |
| **TOTAL** | **$7,160** |
| Contingency (15%) | $1,074 |
| **GRAND TOTAL** | **$8,234** |

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
| Clean CO2 sensor | Monthly |
| Clean humidifier | Weekly |
| Check door switch operation | Monthly |
| Backup controller configuration | Monthly |
| Calibrate CO2 sensor | Annually |
| Replace humidity sensor element | 2-3 years |
| Check fan bearings/clean | 6 months |

---

## Troubleshooting

| Symptom | Possible Cause | Solution |
|---------|---------------|----------|
| CO2 reading stuck at 0 | Sensor fault, wiring | Check 4-20mA loop, power |
| Fans not responding | 0-10V cable, EC board | Check voltage at fan, wiring |
| Humidity won't reach setpoint | Humidifier fault, airflow too high | Check water level, reduce exhaust |
| Temperature swings | PID tuning, AC cycling | Adjust PID parameters |
| Door interlock not working | Switch gap, wiring | Adjust magnet distance, check NC contact |

---

## References

- [Innotech Omni BEMS Platform](https://innotech.com/Products/Digital/Omni-BEMS-Platform.aspx)
- [Sno-Valley Mushrooms FungusBot](https://www.snovalleymushrooms.com/general-6) - Omni controller for mushroom farms
- [Open Support NZ](https://www.youtube.com/watch?v=-zPPu4fNCPM) - Video walkthrough of Omni in mushroom farm
- [ESIS Australia - Vaisala Sensors](https://www.esis.com.au/)
- [Fantech Australia - EC Fans](https://www.fantech.com.au/)
- [Control Store Australia - Actuators](https://www.controlstore.com.au/)
