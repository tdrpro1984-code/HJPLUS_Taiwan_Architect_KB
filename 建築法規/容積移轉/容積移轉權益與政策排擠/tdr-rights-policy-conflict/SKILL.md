---
name: tdr-rights-policy-conflict
description: "This skill should be used when evaluating Transfer of Development Rights (TDR / 容積移轉) entitlements in Taiwan, assessing receiving site (接受基地) eligibility and FAR caps under the Urban Planning TDR Implementation Regulations (都市計畫容積移轉實施辦法), calculating TDR volume adjusted by announced land values, identifying stacking conflicts between TDR and bonus FAR programs (危老重建 / 都市更新 / 綠建築), and analyzing how government FAR incentive policies crowd out the cultural heritage TDR market."
user-invocable: true
license: CC-BY-SA-4.0
compatibility: claude-code,opencode,agent-skills
metadata:
  audience: architects
  region: taiwan
---

# TDR Rights & Policy Conflict (Taiwan)

## Overview

This skill applies to projects involving Transfer of Development Rights (TDR / 容積移轉) under Taiwan's regulatory framework. Invoke this skill when:

1. A client holds cultural heritage property (古蹟, 歷史建築, etc.) with unused development rights and seeks to monetize them via TDR.
2. A developer's receiving site is being evaluated for TDR acceptance capacity and FAR ceiling checks.
3. Calculating the combined FAR from TDR plus multiple bonus incentive programs (危老 / 都更 / 綠建築 / 智慧建築).
4. Advising on systemic policy barriers — specifically, how free government bonus FAR crowds out the cultural heritage TDR market.

---

## Section 1: Legal Framework

| Regulation | Key Articles | Scope |
|---|---|---|
| 都市計畫容積移轉實施辦法 | Art. 3–9 | Core TDR rules: sending/receiving sites, calculation, caps |
| 文化資產保存法 | Art. 35 | Cultural heritage properties as TDR sending sites |
| 都市更新條例 | Art. 65–66 | Urban renewal bonus FAR |
| 危險及老舊建築物加速重建條例 | Art. 6 | Dangerous/old building reconstruction bonus FAR |
| 建築技術規則建築設計施工編 | Art. 162–163 | Green building FAR incentives |

---

## Section 2: Sending Site (送出基地) Categories

| Category (Chinese) | Category (English) | Statutory Basis |
|---|---|---|
| 古蹟 | Monuments | 文化資產保存法 Art. 35 |
| 歷史建築 | Historic Buildings | 文化資產保存法 Art. 35 |
| 聚落建築群 | Groups of Historic Buildings | 文化資產保存法 Art. 35 |
| 紀念建築 | Commemorative Buildings | 文化資產保存法 Art. 35 |
| 考古遺址 | Archaeological Sites | 文化資產保存法 Art. 35 |
| 都市計畫表明應保留之公共設施保留地 | Urban-Plan Public Facility Reserves | 都市計畫容積移轉實施辦法 Art. 3 |
| 農業區、保護區土地（依都市計畫劃定者）| Agricultural / Protected Zone Land | 都市計畫容積移轉實施辦法 Art. 3 |

### Maximum Transferable Volume
For cultural heritage sending sites, the transferable volume is the unused FAR that cannot be developed due to preservation requirements:

```
Transferable Volume (m²) = Site Area × (Permitted FAR − Built FAR)
```

---

## Section 3: Receiving Site (接受基地) Eligibility & Constraints

### 3.1 Location Constraint: Same Master Plan (主要計畫), Not Merely Same City

The legally precise boundary for TDR is the **Urban Planning Master Plan (都市計畫主要計畫)**, not simply the same city or county. This distinction has major practical consequences across Taiwan:

| Municipality Type | Master Plan Structure | TDR Intra-Plan Transfer |
|---|---|---|
| **Taipei City** | Single city-wide master plan covering all districts | Intra-city transfer is always within the same master plan — the **norm** |
| **All other counties/cities** (e.g., New Taipei, Taichung, Tainan, Kaohsiung, etc.) | Multiple independent master plans, each covering individual townships/towns/cities (鄉鎮市) | Intra-plan transfer is limited to a single township area — the **exception**; cross-district transfer is the **norm** |

> **Key Insight:** Outside Taipei City, a sending site and a receiving site located in the same county but in different townships almost certainly fall under **different master plans**, making cross-district TDR approval procedures mandatory. Architects must not assume intra-city proximity equals same-plan eligibility.

### 3.2 Cross-District TDR Transfer (跨都市計畫主要計畫移轉)

When the sending and receiving sites are in different master plan areas — which is the common case outside Taipei City — the transfer requires an explicit **cross-district approval**. Most counties use a **three-tier review system (三審制)**:

| Review Tier | Authority | Stage |
|---|---|---|
| **Tier 1** | Township / Town / City Government (鄉鎮市公所) | Local-level review and preliminary approval |
| **Tier 2** | County / City Government (縣市政府) | Administrative review; urban planning conformance check |
| **Tier 3** | Ministry of the Interior (內政部) | Final national-level approval |

**Practical Implications:**
- The three-tier review can take **months to over a year** to complete.
- Each tier may request supplementary documentation or impose conditions.
- Until Tier 3 approval is received, the TDR transaction **cannot be registered or built upon**.
- For time-sensitive development projects, this procedural delay is a significant risk factor that architects must disclose to clients upfront.

### 3.3 FAR Cap for Receiving Sites

| Sending Site Type | Maximum Receivable TDR (% of Base FAR) |
|---|---|
| General sending sites | ≤ **40%** of base FAR |
| Cultural heritage sending sites (文化資產) | ≤ **50%** of base FAR (varies by municipality) |

> **Note:** Individual municipalities may set stricter or more generous caps via local ordinances (自治法規). Always verify with the local urban planning authority (都市發展局 / 建設局) before advising clients.

### 3.4 Receiving Site Disqualification Conditions
- Sites already at maximum allowable FAR after stacking all bonus incentives.
- Sites in areas where the municipal government has suspended TDR acceptance.
- Sites where the combined FAR (base + TDR + bonuses) would exceed the zone's absolute FAR ceiling.
- Sending and receiving sites are in **different master plan areas** and cross-district approval has not been obtained (or is still pending three-tier review).

---

## Section 4: TDR Volume Calculation (公告現值換算)

### Standard Formula (都市計畫容積移轉實施辦法 Art. 7)

```
Transferred Volume at Receiving Site (m²)
  = Sending Site Unused Volume (m²)
  × (Receiving Site Announced Land Value per m²)
  ÷ (Sending Site Announced Land Value per m²)
```

**Key Notes:**
- Use the **公告土地現值** (officially announced land value) effective at the time of application — do NOT use transaction prices.
- If the receiving site's land value is higher, the transferred building area shrinks (value is preserved, not area).
- Convert the transferred volume (m²) to a FAR ratio by dividing by the receiving site's area for cap checking.

### TypeScript Calculation Interface

```typescript
interface TDRInput {
  sendingSiteArea_m2: number;         // Sending site total area (m²)
  sendingPermittedFAR: number;        // Permitted FAR ratio (e.g. 2.0)
  sendingBuiltFAR: number;            // Already developed FAR ratio
  sendingLandValue_NTD_m2: number;    // 公告土地現值 at sending site (NTD/m²)
  receivingLandValue_NTD_m2: number;  // 公告土地現值 at receiving site (NTD/m²)
  receivingSiteArea_m2: number;       // Receiving site total area (m²)
  receivingBaseFAR: number;           // Base FAR ratio at receiving site
  isCulturalHeritage: boolean;        // true → 50% cap; false → 40% cap
}

function calculateTDR(input: TDRInput): {
  unusedVolume_m2: number;
  transferredVolume_m2: number;
  transferredFAR_ratio: number;
  capFAR_ratio: number;
  acceptedFAR_ratio: number;        // min(transferred, cap)
} {
  const unusedVolume = input.sendingSiteArea_m2
    * (input.sendingPermittedFAR - input.sendingBuiltFAR);

  const transferredVolume = unusedVolume
    * (input.receivingLandValue_NTD_m2 / input.sendingLandValue_NTD_m2);

  const transferredRatio = transferredVolume / input.receivingSiteArea_m2;

  const capMultiplier = input.isCulturalHeritage ? 0.50 : 0.40;
  const capRatio = input.receivingBaseFAR * capMultiplier;

  return {
    unusedVolume_m2: unusedVolume,
    transferredVolume_m2: transferredVolume,
    transferredFAR_ratio: transferredRatio,
    capFAR_ratio: capRatio,
    acceptedFAR_ratio: Math.min(transferredRatio, capRatio),
  };
}
```

---

## Section 5: Bonus FAR Stacking & Cumulative Ceiling

Multiple FAR enhancement programs may apply simultaneously to the same receiving site, creating complex stacking problems.

### Common Bonus FAR Sources in Taiwan

| Program | Typical Bonus Range | Statutory Basis | Cost to Developer |
|---|---|---|---|
| 都市更新容積獎勵 | 10–50% of base FAR | 都市更新條例 Art. 65 | Free (complying with scheme) |
| 危老重建容積獎勵 | 10–40% of base FAR | 危老重建條例 Art. 6 | Free (meeting criteria) |
| 綠建築容積獎勵 | Up to 10% of base FAR | 建築技術規則 Art. 162 | Low cost (certification) |
| 智慧建築容積獎勵 | Up to 10% of base FAR | 建築技術規則 | Low cost (certification) |
| 無障礙設施獎勵 | Varies | Local ordinances | Marginal |
| 容積移轉 (TDR) | ≤ 40–50% of base FAR | 都市計畫容積移轉實施辦法 | **Market price (paid)** |

### Stacking Calculation Model

```
Total Allowable FAR = Base FAR
                    + Σ Bonus FAR (各項獎勵，各受其自身上限約束)
                    + TDR FAR   (受 40% 或 50% of Base FAR 上限約束)

Absolute Zone Ceiling = Base FAR × Municipal Zone Multiplier
                        (typically 1.5× to 2.0×; varies by zone and municipality)

Actual TDR Headroom = MIN(
    TDR Cap (40/50% of Base FAR),
    Absolute Ceiling − Base FAR − Σ Bonus FAR already committed
)
```

> **Critical Issue:** When dangerous-building (危老) + urban renewal (都更) bonuses already consume 40–80% of bonus headroom, the remaining space for TDR absorption may be **zero or negligible**, even though the receiving site owner theoretically holds TDR acceptance rights.

---

## Section 6: Policy Conflict — Government FAR Crowding Out Cultural Heritage TDR

### The Crowding-Out Mechanism

Cultural heritage TDR is a **market-based instrument**: heritage property owners monetize unused development rights by selling them to developers who need more FAR. This market requires that:

1. Developers demand additional FAR (receiving sites have headroom).
2. Purchased TDR is price-competitive against alternative FAR sources.

### How Free Government Bonus Programs Displace TDR Demand

| Government Program | Effect on Heritage TDR Market |
|---|---|
| 危老重建容積獎勵 | Provides 10–40% free bonus FAR; reduces developer incentive to purchase heritage TDR |
| 都市更新容積獎勵 | Provides 10–50% free bonus FAR; directly competes with paid TDR |
| Cumulative FAR bonus stacking | When free bonuses already fill available headroom, paid heritage TDR cannot be absorbed regardless of price |
| TDR cap (40%) shared with free bonuses | Free bonuses consume the same cap space as TDR, directly limiting the quantity of heritage TDR that can be accepted |

### Systemic Policy Contradiction

```
文化資產保存法 → Mandates preservation obligations on heritage property owners
                → Intended remedy: TDR market allows owners to monetize unused FAR

危老重建條例 + 都市更新條例 → Supplies large quantities of free/subsidized bonus FAR
                              → Reduces developer demand for paid TDR
                              → Collapses heritage TDR market prices
                              → Heritage owners cannot monetize; preservation incentive weakens
```

### Red Flags — Checklist for Architect Due Diligence

**Cross-District & Master Plan Checks:**
- [ ] Are the sending and receiving sites within the **same Urban Planning Master Plan (主要計畫)**?
  - If in Taipei City: same master plan guaranteed.
  - If outside Taipei City: confirm both sites' township/city and look up whether they share the same master plan boundary.
- [ ] If cross-district: Has the three-tier review (鄉鎮市 → 縣市 → 內政部) been initiated, and what is the realistic timeline?
- [ ] Does the project schedule account for a potential 1-year+ procedural delay from cross-district three-tier review?

**FAR & Market Checks:**
- [ ] Has the target receiving site already committed to 危老 or 都更 programs with significant bonus FAR?
- [ ] After all bonus FAR is applied, does the receiving site still have headroom within the TDR cap (40/50%)?
- [ ] Does the combined total (base + bonuses + TDR) remain below the zone's absolute FAR ceiling?
- [ ] What is the current market price for heritage TDR in this urban planning area? Is it economically viable?
- [ ] Has the heritage property owner explored alternative mechanisms (修復補助, 免徵稅賦) as supplements or substitutes for TDR monetization?
- [ ] Is the client relying on a potential government TDR Bank purchase? If so, advise that no enabling legislation has been enacted and this remains a policy proposal only.

---

## Section 7: Heritage TDR Bank Proposal & Legal Obstacles (古蹟容積銀行)

### 7.1 The TDR Bank Concept

To address systemic TDR market failure, some government agencies have proposed establishing a **Heritage TDR Bank (古蹟容積銀行 / 容積移轉銀行)**. The proposed mechanism:

| Policy Objective | Mechanism |
|---|---|
| **Price stabilization (平準市場售價)** | Government purchases TDR credits from heritage owners at fair prices, preventing price collapse driven by low private demand |
| **Market liquidity (促進交易)** | Government acts as buyer of last resort; heritage owners can monetize TDR even when private developer demand is absent |
| **Controlled release (適時釋出)** | Government releases banked TDR credits to private developers at appropriate market conditions, smoothing supply-demand imbalances |

### 7.2 Legal Obstacle 1: Public-Owned Cultural Heritage Cannot Generate TDR

Current law (文化資產保存法 Art. 35 + 都市計畫容積移轉實施辦法) does not provide a TDR mechanism for **publicly-owned cultural heritage (公有文化資產)**. Only privately-owned heritage sites are eligible TDR sending sites.

| Issue | Description |
|---|---|
| **公有古蹟** excluded | Government-owned monuments, historic buildings, etc. cannot transfer development rights under existing law |
| TDR Bank portfolio constraint | A government TDR Bank cannot build inventory from its own heritage assets; it must purchase exclusively from private owners |
| Asymmetric burden | Government enforces preservation obligations on private owners but does not apply equivalent TDR mechanisms to its own publicly-held heritage |

### 7.3 Legal Obstacle 2: TDR Entitlements as Claim Rights (請求權), Not Property Rights (物權)

Under Taiwan's civil law framework, TDR entitlements are classified as **請求權 (obligatory rights / claim rights)**, not **物權 (rights in rem / real property rights)**. This classification creates fundamental legal problems for a government TDR Bank:

| Legal Category | Nature | Implication for TDR Bank |
|---|---|---|
| **物權** (Real Rights) | Ownership, mortgage, servitude — can be registered in the Land Registry (地政事務所); enforceable against the world | TDR entitlements are **NOT** classified here |
| **請求權** (Claim Rights) | A contractual right to request specific performance; enforceable only against the counterparty | TDR entitlements are currently classified here |

**Specific consequences for a government-operated TDR Bank:**

1. **No registration mechanism**: After purchasing TDR credits, the government receives only a contractual claim. There is no land registry entry or equivalent public record proving government ownership of the TDR.
2. **No collateral or security**: Since TDR is not a 物權, the government cannot pledge or encumber it. Its legal protection depends entirely on the underlying contract.
3. **Secondary transfer ambiguity**: When the government later resells banked TDR to a private developer, the legal basis for this secondary transfer — particularly whether the government can validly assign a claim right it purchased — is legally uncertain.
4. **Public asset accounting**: Government-held TDR credits may not be properly recordable under 國有財產法 as public assets (公有財產), creating fiscal accounting gaps.

```
Private Heritage Owner
   ↓ sells TDR (claim right)
Government TDR Bank
   │ holds TDR as: contractual claim only
   │ cannot register in: Land Registry (地政事務所)
   │ cannot list as:    Registered public property (公有財產)
   ↓ resells TDR to developer ← secondary transfer legality unclear
Private Developer (Receiving Site)
```

### 7.4 Legislative Reforms Required

For a Heritage TDR Bank to be legally viable, the following statutory amendments would be necessary:

| Reform Area | Current Legal Gap | Direction of Amendment |
|---|---|---|
| 公有文化資產 TDR eligibility | Excluded from sending site mechanism | Amend 文化資產保存法 Art. 35 or 都市計畫容積移轉實施辦法 to include publicly-owned heritage |
| TDR credit registration | No land registry mechanism | Establish a dedicated TDR credit registry (容積移轉憑證制度) — analogous to securities or intangible asset registration |
| Legal nature of TDR | Classified as 請求權 only | Consider elevating TDR to a statutory real right (法定物權), or create a special-purpose public law holding mechanism |
| Government asset holding | Unclear under 國有財產法 | Amend public finance law to explicitly authorize and account for government-held TDR credits |

> **Status as of current date:** The Heritage TDR Bank remains a **policy proposal under deliberation**. None of the required legislative amendments have been enacted. Architects must advise clients not to rely on government TDR Bank purchases as a near-term financial planning assumption.

### 7.5 Contract Risks: Floating Receiving Site & Chain-of-Title Collapse (一物數賣與合約鏈崩)

Beyond the structural legal issues above, current TDR market practice introduces severe **contractual risks** that architects advising either sellers or buyers must understand.

#### 7.5.1 The Floating Receiving Site Clause (任一可接受基地)

Most TDR sale contracts in Taiwan are drafted with language such as:

> 「買方得將本容積移轉權益移轉至任一其可接受之基地」
> *"The buyer may transfer the TDR entitlement to any eligible receiving site."*

This clause leaves the **receiving site unspecified**, creating the following risks:

| Risk Type | Description |
|---|---|
| **一物數賣 (Double/Multiple Selling)** | Without a registry, the seller can contractually sell the same TDR credits to multiple buyers simultaneously. No public record exists to detect or prevent duplication. |
| **No buyer-site binding** | The contract does not establish a legal link between the buyer and a specific receiving site. The buyer holds only a contractual right, not a site-specific entitlement. |
| **Verification impossibility** | A receiving site developer cannot independently verify whether the TDR they are purchasing has already been sold or committed to another party. |

#### 7.5.2 Chain-of-Title Collapse (數手轉譲的合約鏈崩風險)

TDR credits are frequently traded through intermediaries before reaching the final developer. A common chain:

```
[1] Heritage Owner (送出基地所有人)
    ↓  Contract A: sells TDR rights
[2] Broker / Intermediary A
    ↓  Contract B: resells TDR rights
[3] Broker / Intermediary B
    ↓  Contract C: resells TDR rights
[4] Developer (Receiving Site / 接受基地開發商)
```

**Cascading failure:** If **any single contract** in the chain becomes void or is disputed:
- All downstream contracts lose their legal foundation.
- [1] Heritage owner may not receive full payment.
- [4] Developer holds no valid TDR entitlement and cannot apply it to the building permit.
- Intermediate parties lose both payment and rights with no recourse path.

Because TDR entitlements are **請求權** (claim rights), not property rights:
- There is no title registry to establish priority between competing claims.
- The principle of good faith purchase (善意取得) that protects buyers of real property does **not** apply.
- A downstream buyer cannot be protected even if they paid in good faith.

#### 7.5.3 Protective Measures for Architects' Clients

**For TDR Sellers (Heritage Owners):**
- [ ] Ensure the contract names a **specific receiving site** and a specific developer (not a floating clause).
- [ ] Require payment escrowed or released only upon verified receipt of TDR application confirmation from the urban planning authority.
- [ ] Avoid splitting TDR entitlements across multiple partial sales without rigorous tracking.
- [ ] Retain legal counsel experienced in TDR transactions before signing.

**For TDR Buyers (Developers):**
- [ ] Establish a **direct contractual relationship with the original heritage owner**, not only with an intermediary broker.
- [ ] Conduct due diligence to confirm the TDR has not been sold or committed to another party (difficult but necessary).
- [ ] Minimize the number of intermediary tiers in the contract chain.
- [ ] Structure payment to be conditional on successful TDR application acceptance by the authority.
- [ ] Consider requiring the seller's cooperation in a **joint application** to the urban planning authority as a condition of final payment release.

> **Root cause:** All of these contract risks ultimately stem from TDR entitlements being classified as **請求權** with no registration mechanism. The creation of a TDR credit registry (容積移轉憑證制度) would resolve the double-selling and chain-of-title problems by providing an authoritative public record analogous to land registry entries.

#### 7.5.4 The Price Trust Mechanism & Construction Management Company Limitation (價金信託與建築經理公司單片付款問題)

##### Typical Trust Structure

To mitigate payment risk in TDR transactions, it is standard practice to require the purchase price to be held in a **price trust (價金信託)**. The typical structure:

```
[Buyer (Developer)]
    ↓ deposits purchase price
[Bank (Trustee / 受託人)]
    ↓ delegates management to affiliated entity
[Construction Management Company (建築經理公司)]
    ↓ releases funds to seller upon contractually specified trigger conditions
[Heritage Owner / Seller]
```

The construction management company (建築經理公司) — typically a subsidiary of the trustee bank — is responsible for administering the payment release process.

##### The Core Problem: Domain Knowledge Gap

Construction management companies are primarily experienced in **construction project fund management** (e.g., pre-sale housing escrow, construction drawdowns). They have **no specialized expertise** in cultural heritage law or TDR regulatory requirements. As a result:

| Condition That Should Be Verified | Construction Company Capability |
|---|---|
| Is the sending site validly designated as cultural heritage under 文化資產保存法? | ❌ Cannot verify designation status independently |
| Is the claimed TDR volume accurately calculated (unused FAR, 公告現値 ratio)? | ❌ Cannot perform or audit the calculation |
| Has the TDR already been sold to another party (double-selling)? | ❌ No access to any registry to detect duplication |
| Has the urban planning authority formally accepted the TDR application? | ✔ Can verify only if a formal acceptance document is provided |
| Does the receiving site have adequate FAR headroom? | ❌ Cannot assess independently |

##### Payment-on-Instruction: Formalistic Rather Than Substantive Protection

In practice, the construction management company acts purely as a **payment-on-instruction conduit (依照指示付款)**:
- It releases funds when contractually specified trigger documents are submitted by the instructing party.
- It does **not** independently assess whether the underlying TDR conditions have been genuinely fulfilled.
- It does **not** have the expertise to detect fraudulent or erroneous representations about heritage status or TDR volumes.

This means the price trust, while providing **procedural formality**, does **not** provide substantive protection against:
- TDR credits that are misrepresented or do not exist
- Double-sold TDR credits
- TDR volumes inflated beyond what the sending site can legally transfer

##### Recommendations for Structuring TDR Payment Trusts

- [ ] **Tie release triggers to objective authority documents**: The primary payment release condition should be a formal acceptance letter (收件文件 or 受理通知) from the competent urban planning authority, not merely contractual representations from the seller.
- [ ] **Engage an independent TDR technical reviewer**: Prior to fund release, commission an architect or urban planner with TDR expertise to certify that the TDR volume, sending site designation, and receiving site eligibility are verified.
- [ ] **Do not rely on the construction management company for substantive TDR verification**: Treat the company as a payment conduit only; all substantive TDR condition verification must be done separately by qualified professionals.
- [ ] **Include a TDR specialist role in the trust deed**: Specify in the trust agreement that fund release requires written sign-off from a designated TDR professional reviewer, in addition to the standard trigger documents.

> **Systemic gap:** The construction management company model was designed for construction fund management, not for complex regulatory entitlement transactions. The use of this model for TDR transactions reflects the absence of a proper TDR credit registry and specialized TDR transaction infrastructure in Taiwan's current legal framework.

---

## MCP Tool Integration Examples

```python
# Search core TDR regulations
taiwan-building-code_search_building_code(query="容積移轉", limit=10)

# Search cultural heritage TDR provision
taiwan-building-code_search_building_code(query="文化資產保存法第三十五條 容積移轉", limit=5)

# Search official interpretations on TDR calculation
taiwan-building-code_search_building_interpretations(query="容積移轉計算公告現值")

# Search bonus FAR stacking ceiling rules
taiwan-building-code_search_building_code(query="容積獎勵上限 累計", limit=8)

# Search urban renewal bonus FAR
taiwan-building-code_search_building_code(query="都市更新容積獎勵", limit=5)

# Search dangerous/old building reconstruction bonus
taiwan-building-code_search_building_code(query="危老重建容積獎勵", limit=5)

# Search receiving site constraints
taiwan-building-code_search_building_interpretations(query="接受基地容積移轉上限")

# Search cross-district TDR transfer approval procedure
taiwan-building-code_search_building_interpretations(query="容積移轉跨都市計畫主要計畫")

# Search Ministry of Interior TDR cross-district review
taiwan-building-code_search_building_code(query="都市計畫容積移轉 內政部審查", limit=5)

# Search public heritage TDR eligibility (TDR Bank legal basis)
taiwan-building-code_search_building_code(query="公有文化資產 容積移轉", limit=5)

# Search TDR legal nature interpretations
taiwan-building-code_search_building_interpretations(query="容積移轉權益 物權 請求權")
```
