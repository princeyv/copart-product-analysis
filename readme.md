# Copart Vehicle Inventory Listing Quality & Auction Clearance Root-Cause Analysis

## 🎯 Project Overview & Core Business Impact
Auction clearance velocity is a critical operational KPI for Copart's digital bidding marketplace. This data product investigates how front-end data completeness and listing risk indicators independently impact vehicle clearance success. 

By cross-analyzing **24,530 unique vehicle lots** from nationwide daily auction pipelines, this project reveals a massive information-gap anomaly that suppresses bidding confidence and directly impacts clearance margins.

### 🚀 Key Findings Summary:
* **Market Baseline:** **72.2%** of vehicle lots clear cleanly nationwide via standard "Pure Sale" workflows.
* **The Core Data Anomaly:** Listings completely missing a structural repair cost estimate (`repairCost = $0`) experience an immediate auction clearance collapse—crashing down to **35.3%**, compared to an **83.1%** clearance rate when an estimate anchor is populated.
* **The Concentration Pocket:** This lack of data visibility is heavily concentrated inside **Clear Title (CT)** fleet and dealer vehicle dispositions, where **62.0%** of all lots are published completely devoid of a repair cost baseline.

---

## 📊 Interactive Product Dashboard (Tableau)
An Executive Scorecard was designed and structured in Tableau to track clearance metrics, expose performance variance across high-volume listing channels, and pinpoint inventory risk pockets.

* **KPI Highlights:** Unified view of national volume baselines and weighted real-time clearance percentages.
* **Data Segment Flows:** Deep-dive breakdown isolating the 48-percentage-point performance drop between listings with verified cost anchors vs. undocumented profiles.
* **Segment Matrix Heatmap:** Cross-tabulation filtering out low-volume statistical noise to isolate the massive volume bottleneck sitting within the Clear Title (`CT`) category.

---

## 🔬 Statistical Validation (Logistic Regression Rigor Check)
To confirm that the clearance collapse on missing-estimate vehicles isn't merely a proxy for vehicle conditions or regional trends, a multi-variable logistic regression was constructed:

$$is\_pure\_sale = \beta_0 + \beta_1(missing\_repair\_cost) + \sum \beta_i(Vehicle\_Type\_Controls) + \sum \beta_j(Damage\_Type\_Controls)$$

### Model Output & Insights:
* **Regression Coefficient ($\beta_1$):** `-1.6724`
* **Odds Ratio ($e^{-1.6724}$):** `0.188`

> 💡 **The Data Proof:** Holding all other factors completely equal (including specific vehicle types and primary vehicle damage descriptions), a listing missing its repair cost estimate has **only 19% of the odds of clearing cleanly** compared to a twin asset with an estimate anchor on file. This proves that the clearance bottleneck is driven by a lack of buyer data visibility rather than low vehicle quality.

---

## 🛠️ Product Recommendations & Lean Experimentation Plan
Using the **Lean "Build → Measure → Learn" Product Methodology**, we propose introducing an automated **Listing Completeness Engine** to the seller console workflow:

1. **Pre-Submission Yard Auditing Flags:** Auto-flag Clear Title (`CT`) listings registered with a $0 repair cost placeholder pre-auction, routing them to local yard operations for priority damage review.
2. **Contextual Buyer Interface Labels:** Update the public bidding portal to explicitly show **"Estimate Pending"** rather than a raw blank space or misleading "$0" string, successfully separating pending administrative evaluations from truly undamaged vehicles.

### 🧪 Controlled A/B Test Framework:
* **The Experiment Group:** Route 50% of undocumented Clear Title listings into the newly styled "Estimate Pending" interface flow.
* **Success Metrics to Measure:** Track lift in **unique active bidders per lot** and macro **auction clearance recovery** as our core success metrics.