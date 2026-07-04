# Copart Vehicle Inventory Listing Quality & Auction Clearance Root-Cause Analysis

## 🎯 Project Overview & Core Business Impact
[cite_start]Auction clearance velocity is a critical operational KPI for Copart's digital bidding marketplace[cite: 10, 17]. [cite_start]This data product investigates how front-end data completeness and listing risk indicators independently impact vehicle clearance success[cite: 21]. 

[cite_start]By cross-analyzing **24,530 unique vehicle lots** from nationwide daily auction pipelines, this project reveals a massive information-gap anomaly that suppresses bidding confidence and directly suppresses clearance margins.

### 🚀 Key Findings Summary:
* [cite_start]**Market Baseline:** **72.2%** of vehicle lots clear cleanly nationwide via standard "Pure Sale" workflows.
* [cite_start]**The Core Data Anomaly:** Listings completely missing a structural repair cost estimate (`repairCost = $0`) experience an immediate auction clearance collapse—crashing down to **35.3%**, compared to an **83.1%** clearance rate when an estimate anchor is populated.
* [cite_start]**The Concentration Pocket:** This lack of data visibility is heavily concentrated inside **Clear Title (CT)** fleet and dealer vehicle dispositions, where **62.0%** of all lots are published completely devoid of a repair cost baseline.

---

## 📊 Interactive Product Dashboard (Tableau)
[cite_start]An Executive Scorecard was designed and structured in Tableau to track clearance metrics, expose performance variance across high-volume listing channels, and pinpoint inventory risk pockets.

* [cite_start]**KPI Highlights:** Unified view of national volume baselines and weighted real-time clearance percentages.
* [cite_start]**Data Segment Flows:** Deep-dive breakdown isolating the 48-percentage-point performance drop between listings with verified cost anchors vs. undocumented profiles.
* [cite_start]**Segment Matrix Heatmap:** Cross-tabulation filtering out low-volume statistical noise to isolate the massive volume bottleneck sitting within the Clear Title (`CT`) category.

---

## 🔬 Statistical Validation (Logistic Regression Rigor Check)
[cite_start]To confirm that the clearance collapse on missing-estimate vehicles isn't merely a proxy for vehicle conditions or regional trends, a multi-variable logistic regression was constructed:

$$\text{is\_pure\_sale} = \beta_0 + \beta_1(\text{missing\_repair\_cost}) + \sum \beta_i(\text{Vehicle Type Controls}) + \sum \beta_j(\text{Damage Type Controls})$$

### Model Output & Insights:
* [cite_start]**Regression Coefficient ($\beta_1$):** `-1.6724` 
* **Odds Ratio ($e^{-1.6724}$):** `0.188` 

> 💡 **The Data Proof:** Holding all other factors completely equal (including specific vehicle types and primary vehicle damage descriptions), a listing missing its repair cost estimate has **only 19% of the odds of clearing cleanly** compared to a twin asset with an estimate anchor on file. This proves that the clearance bottleneck is driven by a lack of buyer data visibility rather than low vehicle quality.

---

## 🛠️ Product Recommendations & Lean Experimentation Plan
Using the **Lean "Build → Measure → Learn" Product Methodology**, we propose introducing an automated **Listing Completeness Engine** to the seller console workflow[cite: 22, 66]:

1. **Pre-Submission Yard Auditing Flags:** Auto-flag Clear Title (`CT`) listings registered with a $0 repair cost placeholder pre-auction, routing them to local yard operations for priority damage review[cite: 66].
2. **Contextual Buyer Interface Labels:** Update the public bidding portal to explicitly show **"Estimate Pending"** rather than a raw blank space or misleading "$0" string, successfully separating pending administrative evaluations from truly undamaged vehicles[cite: 64, 66].

### 🧪 Controlled A/B Test Framework:
* [cite_start]**The Experiment Group:** Route 50% of undocumented Clear Title listings into the newly styled "Estimate Pending" interface flow[cite: 66, 440].
* [cite_start]**Success Metrics to Measure:** Track lift in **unique bidder counts per lot** and macro **auction clearance rate recovery** across the target clear title segment[cite: 66, 441].