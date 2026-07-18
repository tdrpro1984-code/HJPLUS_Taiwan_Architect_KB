---
name: adaptive-reuse-response-plan
description: "This skill should be used when handling the restoration and adaptive reuse of cultural heritage buildings, specifically for creating a response plan to exempt them from standard urban planning, building, and fire codes."
license: CC-BY-SA-4.0
compatibility: claude-code,opencode,agent-skills
metadata:
  audience: architects
  region: taiwan
---

# Heritage Adaptive Reuse Response Plan (Taiwan)

## Overview
This skill provides guidelines on the legal exemptions available for cultural heritage buildings (Monuments, Historic Buildings, etc.) undergoing restoration or adaptive reuse. Under the Cultural Heritage Preservation Act, these buildings can be exempted from certain provisions of the Urban Planning Law, Building Act, and Fire Services Act by submitting an "Adaptive Reuse Response Plan" (因應計畫).

## Execution Steps
1. **Identify Exemptions Needed**: Assess which current building, fire, or land-use codes conflict with the preservation of the heritage building's original structure or historical value.
2. **Formulate the Response Plan**: Develop alternative safety and management strategies (the Response Plan) for the non-compliant items. This includes:
   - Alternative structural safety measures.
   - Fire safety compensatory measures (e.g., dedicated fire suppression systems suitable for historic materials).
   - Accessibility and land-use alternatives.
3. **Submit for Joint Review**: Submit the Response Plan to the competent cultural authority, which will coordinate a joint review with building control, fire safety, and urban planning departments.
4. **Implementation**: Once approved, the Response Plan legally supersedes the standard codes for that specific building.

## Technical Specifications (Exemptible Regulations)

### 1. Urban Planning Law (都市計畫法)
- Exemptions can often be made for land-use zoning restrictions, allowing commercial or educational use in areas normally restricted, provided it serves the purpose of heritage revitalization.

### 2. Building Act (建築法)
- **Clearance/Setbacks**: Exemptions from building line setbacks.
- **Structural Constraints**: Exemptions from modern seismic or structural requirements if they would destroy historic value (alternative structural reinforcement plans required).
- **Facilities**: Exemptions from parking spaces, air defense shelters, and certain accessibility requirements (though reasonable accommodation is expected).
- **Building Permit Process**: The restoration plan approval can serve in lieu of standard building permits in some cases.

### 3. Fire Services Act (消防法)
- Exemptions from standard fire equipment rules.
- Requires a specialized fire safety design tailored to historic buildings (e.g., water mist systems instead of standard sprinklers, early warning systems).

## Case Example: Automatic Sprinkler Alternatives

**Source**: Regulations for Processing Building Management, Land Use, and Fire Safety for Restoration/Adaptive Reuse of Monuments, Historic Buildings, Commemorative Buildings, and Groups of Buildings, Art. 4(2) (the Response Plan must document "building management and fire safety response measures"); Art. 5 (joint review by land-use, building, and fire authorities; approval may exclude partial or full application of current fire regulations).

This regulation is a framework only — it does not prescribe specific substitute technologies for automatic sprinklers. The specific technical alternative must be proposed case-by-case by the architect/fire engineer based on a site risk analysis, then approved through joint review.

| Measure | Description | Practical Notes |
|---------|-------------|------------------|
| Fine water mist system | Suppresses fire with micro-droplets; far less water discharge than standard sprinkler heads, reducing water damage risk to wood structures, murals, and painted decoration | Only ~5 monuments nationwide have installed automatic water mist systems — most owners avoid it over concern for altering the heritage fabric, indicating a high approval bar, not a default choice |
| Early smoke detection / monitoring | High-sensitivity smoke detectors, CCTV linked to fire dispatch or a management center | Tainan Fire Department pilot at Sacrificial Rites Wu Temple (祀典武廟): existing surveillance equipment networked to back-end dispatch, enabling rapid response during unattended hours — a "compensate for missing suppression via faster response" strategy |
| Enhanced fire extinguisher provisioning | Higher extinguisher density; extinguisher types suited to wood structures / paper artifacts | Fire extinguishers remain the dominant fire protection measure actually installed at monuments nationwide — the most common, least invasive baseline measure |
| Fire prevention / self-management plan | Per National Fire Agency's *Guidelines for Strengthening Fire Prevention Self-Management at Monuments and Historic Buildings*: open-flame/electrical management (incense burners, candles, wiring replacement), hot-work control during construction, disaster maps and rescue route diagrams, regular drills | A non-equipment compensatory measure, typically submitted alongside equipment alternatives in the Response Plan to demonstrate overall risk has been reduced to an acceptable level |
| Other extinguishing systems | Fire Safety Equipment Standards §18 permits water mist, foam, or dry powder systems as alternatives to standard automatic sprinklers | Case-by-case suitability for heritage materials — dry powder/foam can cause secondary contamination, so rarely used in artifact-bearing spaces |

**Drafting priorities**:
1. **Risk analysis first**: document why the standard sprinkler system is unsuitable (structural material, occupant density, egress paths)
2. **Propose an equivalent-safety alternative**: the core requirement is not "omit the system" but "achieve an equivalent or acceptable safety level by other means" — this is what review approval hinges on
3. **Pair with self-management commitments**: equipment substitution alone is rarely sufficient; reviewing fire authorities typically expect it combined with the self-management guideline's routine measures

## Requirements & Constraints
- The exemptions are NOT automatic. They are strictly contingent upon the approval of the "Adaptive Reuse Response Plan" (因應計畫) which must prove that alternative measures provide equivalent or acceptable levels of safety.
- Reference: *Regulations for the Processing of Building Management, Land Use, and Fire Safety for the Restoration or Adaptive Reuse of Monuments, Historic Buildings, Commemorative Buildings, and Groups of Buildings* (古蹟歷史建築紀念建築及聚落建築群修復或再利用建築管理土地使用消防安全處理辦法).
- Reference: Fire Safety Equipment Standards for Various Premises §18 (alternative extinguishing systems).
- Reference: National Fire Agency, *Guidelines for Strengthening Fire Prevention Self-Management at Monuments and Historic Buildings* (強化古蹟及歷史建築火災預防自主管理指導綱領).

## MCP Tool Integration Examples
```python
# Query building code exemptions for cultural heritage
taiwan-building-code_search_building_code(query="因應計畫 消防", limit=5)
taiwan-building-code_search_building_interpretations(query="古蹟 再利用")
```
