---
name: assembly-hall-fire-safety
description: "This skill should be used when evaluating fire safety and life safety code compliance for auditoriums, assembly halls, or performance venues (禮堂/集會堂) in Taiwan, including occupancy classification, occupant load calculation, egress design (exits, corridors, stairs), auditorium-specific seating/aisle provisions per Building Technical Regulations §117-128, interior finish material limits, and required fire protection equipment for Class A (甲類) premises per the Fire Safety Equipment Standards."
user-invocable: true
---

# Assembly Hall / Auditorium Fire Safety Compliance

## Overview

This skill provides comprehensive fire safety and life safety code compliance evaluation for auditoriums, assembly halls, and performance venues (禮堂、集會堂、演藝廳) under Taiwan's dual regulatory framework. It should be invoked when:

- Determining regulatory applicability for an assembly hall design (which article thresholds apply)
- Calculating occupant load (收容人員人數) to size exits and fire protection systems
- Designing seating layout, aisles, and egress paths in an auditorium
- Reviewing exit, corridor, and stair provisions against code minimums
- Confirming required fire protection equipment for a Class A (甲類) premises
- Checking interior finish material fire-retardancy requirements

---

## Section 1: Regulatory Framework & Applicability

Assembly halls are governed by two parallel regulatory systems that must both be satisfied.

| System | Source | Classification Provision |
|--------|--------|--------------------------|
| **Building Act** | Building Technical Regulations (Design & Construction) | §69 (Occupancy Group A-1, Assembly & Performance) |
| **Fire Act** | Fire Safety Equipment Standards for Various Premises | §12, Class A (甲類), Item 2 — grouped with bowling alleys, billiard halls, fitness/leisure centers |

### Auditorium-Specific Chapter Trigger

Building Technical Regulations §117-128 (Chapter 5, Section 2) applies to theaters, cinemas, cabarets, performance halls, **and assembly halls with floor area > 200 m²** (§117). Assembly spaces ≤ 200 m² are subject only to general egress provisions (Chapter 3, Section 1) and Class A equipment requirements — not the detailed seating/aisle rules below.

```typescript
interface AssemblyHallApplicability {
  floorArea: number; // m² — audience/assembly area
  usageType: 'theater' | 'cinema' | 'cabaret' | 'performance-hall' | 'assembly-hall';
}

function requiresAuditoriumChapter(input: AssemblyHallApplicability): boolean {
  if (input.usageType !== 'assembly-hall') return true; // theaters/cinemas/etc. always apply
  return input.floorArea > 200; // §117 threshold for assembly halls specifically
}
```

---

## Section 2: Occupant Load Calculation

Per Ministry of Interior Fire Agency interpretation (各類場所收容人員計算方式), applicable to film exhibition venues, cabarets, assembly halls, gymnasiums, and activity centers:

```
Occupant Load = Staff Count + Fixed Seating + Standing Area + Other Area
```

| Component | Formula |
|-----------|---------|
| Staff count | Actual number of working personnel |
| Fixed seating | Number of seats; for continuous-row (bench) seating: `seat frontage width ÷ 0.4 m`, fractional remainder < 1 discarded |
| Standing area | `floor area ÷ 0.2 m²` |
| Other area | `floor area ÷ 0.5 m²` |

```typescript
interface OccupantLoadInput {
  staffCount: number;
  fixedSeatCount?: number;              // discrete seats
  continuousSeatingWidthM?: number;     // m — bench-style seating frontage
  standingAreaM2?: number;
  otherAreaM2?: number;
}

function calcOccupantLoad(input: OccupantLoadInput): number {
  const fixedSeats =
    (input.fixedSeatCount ?? 0) +
    Math.floor((input.continuousSeatingWidthM ?? 0) / 0.4);
  const standing = Math.floor((input.standingAreaM2 ?? 0) / 0.2);
  const other = Math.floor((input.otherAreaM2 ?? 0) / 0.5);
  return input.staffCount + fixedSeats + standing + other;
}
```

Occupant load drives exit width sizing, the fire-safety-manager designation threshold, and fire protection equipment scale — calculate it early in design.

---

## Section 3: General Egress Provisions (Chapter 3, Section 1)

| Parameter | Requirement | Reference |
|-----------|-------------|-----------|
| Exit door width (direct stair to exterior) | ≥ 1.2 m; minimum 2 exits in different directions | §90 |
| Corridor width | ≥ 1.6 m if rooms open on both sides; ≥ 1.2 m otherwise | §92 |
| Travel distance | Occupancy Group A (assembly/performance): ≤ 30 m; reduced to ≤ 20 m for floors ≥ 15F | §93 |
| Stair provision | 3-5F: at least one enclosed stair (安全梯); 6F+: enclosed stair required; ≥ 15F: exterior stair or special enclosed stair (特別安全梯) | §96 |

---

## Section 4: Auditorium-Specific Provisions (§117-128)

```typescript
interface AuditoriumSeatingCheck {
  seatBackToBackSpacingCm: number;   // §123 minimum 85
  tieredFloorStepRiserCm: number;    // §123 maximum 50 per step
  seatsPerVerticalAisleGroup: number; // §124: vertical aisle every 8 seats
  auditoriumFloorAreaM2: number;      // determines aisle width threshold
  continuousSeatWidthCm?: number;     // §124-1 minimum 45
}

function minVerticalAisleWidthCm(floorAreaM2: number): number {
  return floorAreaM2 > 900 ? 95 : 80; // §124
}
```

| Article | Requirement |
|---------|-------------|
| §121 | Frontage road width ≥ 12 m; road frontage length ≥ 1/6 of site perimeter |
| §122 | If the main seating level is at the discharge (avoidance) floor, seating must be set back ≥ 1.5 m from the building line; for area > 200 m², add 2.5 cm setback per additional 10 m² |
| §123 | Seat back-to-back spacing ≥ 85 cm; tiered floor step riser ≤ 50 cm |
| §124 | Vertical aisle required every 8 seats in a row; width ≥ 80 cm (≥ 95 cm if auditorium floor area > 900 m²); horizontal (cross) aisle required at least every 15 rows and at the frontmost row, width ≥ 1 m |
| §124-1 | Continuous (bench) seating: minimum 45 cm per seat; aisles ≥ 1.1 m wide flanking the seating block, connecting to exits |
| §126 | Stage construction requires fire curtain / fire-rated separation from the auditorium |
| §127 | Main seating level should be located at or near the discharge floor, with egress path considered |
| §128 | Projection room (if present): non-combustible construction, fire-separated from the auditorium |

---

## Section 5: Interior Finish Material Requirements

**Source**: Building Technical Regulations §88

For Occupancy Group A (Assembly, including performance use):

| Location | Minimum Fire-Retardancy Class |
|----------|-------------------------------|
| Rooms / assembly seating area | 耐燃三級 (Class 3) or higher |
| Corridors and stairs leading to grade | 耐燃二級 (Class 2) or higher |

**Exemption**: Not required where the space is fire-compartmented at ≤ 100 m² per zone with ≥ 1-hour rated walls/fire doors, is at grade level with floor area ≤ 100 m², or is equipped with both automatic fire extinguishing and smoke exhaust systems.

---

## Section 6: Fire Protection Equipment (Class A / 甲類 Premises)

**Source**: Fire Safety Equipment Standards for Various Premises — assembly halls are Class A (甲類), Item 2

| Equipment | Trigger Threshold | Reference |
|-----------|--------------------|-----------|
| Fire extinguishers | Mandatory for all Class A premises | §15 |
| Indoor fire hydrant | ≤5F: any floor ≥ 300 m²; ≥6F: any floor ≥ 150 m² | §16 |
| Automatic sprinkler | ≤10F: aggregate floor area ≥ 300 m²; ≥11F: any floor ≥ 100 m² | §17 |
| Automatic fire alarm | ≤5F: any floor ≥ 300 m²; 6-10F: any floor ≥ 300 m²; ≥11F: mandatory regardless of area | §19 |
| Emergency broadcast system | Required wherever automatic fire alarm is required; speaker sound pressure: L-class ≥ 92 dB, M-class ≥ 87 dB | §133, §134 |
| Exit signage | Exit signs + directional signs; theaters/cinemas additionally require auditorium aisle guide lights, illuminance ≥ 0.2 lux | §146, §147 |
| Emergency lighting | Mandatory for Class A premises; underground passage ≥ 10 lux, other areas ≥ 2 lux | §200, §202 |
| Smoke exhaust | Triggered at floor area > 500 m² — see `smoke-exhaust-review` skill (cross-reference below) | Building Tech Reg §100①/ Fire Safety §28① |

> Connected water supply piping (連結送水管) and dedicated fire reservoirs (消防專用蓄水池) are triggered by building scale (story count / aggregate floor area) and must be checked case-by-case; not tabulated here as thresholds are project-specific.

---

## Section 7: Cross-Reference — Smoke Exhaust

Assembly halls exceeding 500 m² floor area trigger smoke exhaust obligations under **both** the Building Act (§100①) and Fire Act (§28①) — this is "Entry B: Designated Occupancy" in the `smoke-exhaust-review` skill. For smoke compartment partitioning, exhaust window effective area calculation, and central control room requirements, invoke that skill directly rather than duplicating its logic here.

---

## Section 8: MCP Integration

```typescript
// Occupancy classification and auditorium chapter
taiwan-building-code_search_building_code(query: "使用類組 A-1 集會表演")
taiwan-building-code_search_building_code(query: "建技規 第一百十七條 集會堂")
taiwan-building-code_search_building_code(query: "觀眾席 通道 座位排列")

// Occupant load
taiwan-building-code_search_building_interpretations(query: "收容人員計算方式 集會堂")

// Fire protection equipment
taiwan-building-code_search_building_code(query: "各類場所消防安全設備設置標準 甲類場所")
taiwan-building-code_search_building_code(query: "室內消防栓 自動撒水設備 設置標準")

// Interior finish materials
taiwan-building-code_search_building_code(query: "建技規 第八十八條 內部裝修材料 耐燃")
```

---

## Section 9: References

- Building Technical Regulations (Design & Construction) §69, §88, §90, §92, §93, §96, §117-128
- Fire Safety Equipment Standards for Various Premises §12, §15-§17, §19, §133-§134, §146-§147, §200, §202
- Ministry of Interior Fire Agency interpretation: Occupant Load Calculation Method for Various Premises (各類場所收容人員計算方式)
- Related skill: `smoke-exhaust-review` (排煙窗法規檢討) for smoke exhaust design details
