---
name: heritage-investigation
description: "This skill should be used when initiating a cultural heritage restoration project to conduct historical research, surveying, and damage investigation according to the Regulations for the Restoration and Adaptive Reuse of Historic Monuments."
user-invocable: true
---

# Heritage Investigation and Research

This skill outlines the procedures for conducting an investigation and research phase for cultural heritage buildings in Taiwan. According to the Cultural Heritage Preservation Act, this is a mandatory step before any restoration design can begin.

## 1. Required Competencies and Qualifications

According to the Regulations for the Restoration and Adaptive Reuse of Historic Monuments, the principal investigator must meet specific qualifications (e.g., architects, relevant scholars with heritage preservation experience).

## 2. Key Components of the Investigation Report

An investigation and research report typically includes:

| Component | Description |
|-----------|-------------|
| Historical Research | Tracing the building's origin, alterations, and historical significance. |
| Environmental & Urban Planning Survey | Review the site's urban planning (major and detailed plans), zoning regulations, Floor Area Ratio (FAR), and Building Coverage Ratio (BCR). If located in a Preservation Zone, strict adherence to the higher-level preservation plan is required. |
| Surveying Technology (測量技術) | Mandatory on-site surveying. Most heritage buildings lack original permit drawings. On-site surveying is no longer limited to traditional laser rangefinders; modern techniques such as **360-degree cameras**, **3D Laser Point Cloud Scanning (雷射點雲掃描)**, and **UAV/Drone Aerial Scanning** are highly recommended to create accurate as-built drawings (plans, elevations, sections). |
| On-site Condition Narrative | The narrative of physical conditions and damages must strictly follow a logical "Top-to-Bottom, Large-to-Small" sequence: **Roof -> Structure -> Ceiling -> Walls -> Floors -> Stairs -> Doors & Windows -> Decorative Details**. Findings must be cross-referenced with possible historical construction methods. |
| Damage Assessment & Structural Data | Due to the irreplaceable nature of heritage, prioritize **Non-Destructive Testing (NDT)**. |
| Restoration Recommendations | Preliminary guidelines for the subsequent restoration design phase. |

## 3. Taiwan Building Code / MCP Integration

While primarily governed by the Cultural Heritage Preservation Act, related searches can be done if needed:

```python
# Search for official interpretations regarding heritage building preservation
taiwan-building-code_search_building_interpretations(query="文化資產保存")
```