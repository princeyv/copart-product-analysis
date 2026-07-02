# Prince's Summer 2027 Internship Push — Context & Project Plan

*Last updated: June 30, 2026*

---

## 1. Where This Started

Goal: land a Data Science / ML Engineering internship for **Summer 2027**, as a stepping stone toward a full-time US role and eventual H1B sponsorship after graduating from UNT's MS Data Science program (ML Engineering track).

Timing constraint: tech internship applications for Summer 2027 open **July–October 2026** on a rolling basis, meaning early, high-quality applications matter far more than late, generic ones. Portfolio needs to be application-ready by late July 2026.

## 2. The Portfolio Philosophy (from Kedeisha Bryan's video)

Most aspiring analysts fail to stand out because they build repetitive tutorial-style projects. The fix is to build projects that tell a business story and solve a real problem, not just display a chart. Five high-impact project archetypes:

1. **KPI Card Dashboard** — one clear business question, one number, clear stakeholder context
2. **Root Cause Analysis** — investigate a specific anomaly using structured hypothesis testing (the "why," not just the "what")
3. **Domain-Specific Project** — build within an industry you're targeting, to speak that field's language
4. **Consulting-Style Recommendation** — synthesize analysis into a 3–5 slide executive deck non-technical people can act on
5. **Real-World Consulting** — free 30-day analytical support for a nonprofit/small business, to get real data and references

Key takeaway: shift from "tool user who makes charts" to "problem solver who drives decisions."

## 3. Job Posting Analysis (from uploaded LinkedIn/job board PDF)

Analyzed 8 DFW-based internship postings. Ranked by real fit (skills match + degree level match) **and** flagged which postings contain "no future visa sponsorship" language, since that's a hard filter on Prince's long-term H1B path even though it doesn't block CPT-based internship applications themselves.

| Rank | Company / Role | Visa flag | Fit notes |
|---|---|---|---|
| 1 | **Copart — Technology Product Analyst Intern** (Dallas, TX) | None found | Best fit — wants master's students in Data Analytics/Math/Stats, wants SQL + Tableau + KPI/product-analytics skills. Matches existing churn + Tableau projects closely. |
| 2 | Delta Electronics — Market Intelligence Intern (Plano, TX) | "No current or future sponsorship" | Strong technical fit (Excel/PPT/Tableau/Power BI), explicitly pays Master's students more — but visa language is a long-term red flag. |
| 3 | Darling Ingredients — Analytics Intern (Irving, TX) | None found | Generic, low technical bar, easy application, no visa flag — good volume/backup application. |
| 4 | American Heart Association — Data Science Intern, Remote | "Sponsorship, now or in the future" | Skills match is strong (Python/SQL/ML/healthcare) but experience bar is MS/PhD + peer-reviewed publications — mismatched seniority, plus visa dealbreaker. |
| 5 | Koch — Summer 2027 Tax Internship (Plano, TX) | "Not eligible for VISA Sponsorship" | Wrong domain (tax/accounting) and visa dealbreaker. Low priority. |
| 6–8 | Wells Fargo ×3 (Finance / COO Business Risk / COO Global Operations, Irving TX) | "Does not require visa sponsorship now or in the future" (all 3) | Targets undergrad juniors, finance-first majors, and carries the visa dealbreaker on all three. Lowest priority. |

**Decision: start with Copart.**

## 4. Copart — Technology Product Analyst Intern (key posting details, for reference)

- **Location:** Dallas, TX — Headquarters, Full-time internship
- **Team:** Product Management
- **Core responsibilities:** define/monitor KPIs, analyze feature usage and product trends, build dashboards/reports, design beta/pilot tests, apply lean methodology (build → measure → learn), support SDLC discovery phase
- **Required qualifications:** current student or recent grad pursuing a **master's degree** in Data Analytics, Mathematics, Engineering, Statistics, etc.
- **Tools wanted:** SQL, Tableau (or similar reporting tools), Mixpanel/Flurry/Google Analytics, JIRA, Agile/Scrum, Lean methodology
- **Visa language:** none found — only standard E-Verify (confirms current work authorization; doesn't block future sponsorship)

## 5. The Portfolio Project — Full Outline

### Title
**"Copart Salvage Lot Risk & Listing-Quality Root Cause Analysis"**

### Why this project, specifically
It combines two of Bryan's five archetypes at once — **Root Cause Analysis** and **Domain-Specific** — using data from the actual company Prince is applying to, which almost no other applicant will do. It directly mirrors the Copart JD's language: defining KPIs, spotting patterns in feature/data quality, and proposing a testable product fix with a measurement plan.

### Data source
Real, free, legitimately-scraped Copart salvage auction listing data:
- GitHub: `rebrowser/copart-dataset` (public preview sample + free research access)
- Also mirrored on Kaggle: `kaggle.com/datasets/rebrowser/copart-dataset`
- ~2M+ real Copart lots, updated daily. Contains: make, model, year, damage type, repair cost, mileage, title type, drivetrain, state/yard location, sale date, and field-by-field completeness (body style, trim, secondary damage, auto grade — all have uneven fill rates).
- **Important limitation:** `highBid`, `estRetailValue`, and a few other fields are locked behind Copart/Rebrowser's paid tier in the free sample — so this project does **not** attempt a "final sale price" story. It focuses on **listing data-quality** and **repair-cost risk**, both fully supported by the free fields.
- **Licensing note:** free for research / non-commercial use with attribution. Frame the project publicly as "independent analysis of publicly available Copart auction data" — no claim of official affiliation, no monetization.

### The business question (KPI framing)
"Which segments of Copart's inventory carry hidden risk or incomplete information for bidders, and what's driving it?"

### Root-cause chain to build

1. **Find the anomaly** — Measure listing completeness (% of key fields populated: body style, trim, secondary damage, auto grade) broken down by state, yard, and damage type. Expect uneven completeness across segments.
2. **Form hypotheses for why** — Candidates to test:
   - Yard volume (higher-volume yards may cut corners on data entry)
   - Vehicle type (motorcycles/commercial trucks under-documented vs. passenger cars)
   - Seller type (insurance auto-feed vs. manual dealer submission)
   - Seasonal/volume spikes affecting data entry quality
3. **Test the hypotheses** — Group-by comparisons across those dimensions; chi-square or simple statistical comparison to see which hypothesis actually holds.
4. **Second thread: repair-cost risk** — Within peer groups (same make/model/year/damage type), flag lots whose repair cost estimate is a statistical outlier vs. peers (z-score or IQR method). This is a proxy for inconsistent/risky listings, since the true retail value field isn't available.
5. **The recommendation (the part most portfolio projects skip)** — Don't just report the finding, propose a product fix, e.g.:
   - A "listing completeness score" shown to sellers pre-submission
   - Auto-flagging repair-cost estimates that fall outside the normal range for that vehicle profile, for yard manager review
   - Define what to measure post-launch to know if it worked: bid count per lot, listing edit rate, dispute rate — directly echoes the "build → measure → learn" language in Copart's own posting.

### Day-by-day build plan (~1 week, solo)

| Day | Task |
|---|---|
| 1 | Pull dataset (Kaggle or GitHub parquet files), load into pandas, profile null rates and record counts by state/yard/damage type |
| 2–3 | Core analysis: completeness rate breakdowns, outlier detection on repair cost within peer groups, hypothesis testing across segments |
| 4 | Build Tableau dashboard: one KPI card up top (e.g. "National listing completeness: X%, range Y%–Z% by state"), drill-down views underneath |
| 5 | Build 3-slide consulting-style recommendation deck (reuse existing pptxgenjs workflow): business question → root cause finding → recommended feature + measurement plan |
| 6 | Package: GitHub repo with README that tells the story in words first, code second. Post on LinkedIn. Link in Copart application and resume. |

### Deliverables checklist
- [ ] Cleaned analysis notebook (Python/pandas or SQL)
- [ ] Tableau dashboard (KPI card + drill-downs)
- [ ] 3-slide executive recommendation deck
- [ ] GitHub repo with narrative README
- [ ] LinkedIn post
- [ ] Link added to resume/portfolio and Copart application

### Talking points for cover letter / interview
- "I analyzed Copart's own public auction listing data and found [X]% variation in listing completeness across states/yards, which likely affects bidder confidence."
- "I designed a lean-methodology test plan — a completeness score feature — with a clear before/after metric, matching how your Product team evaluates feature changes."
- Positions Prince as already thinking like a Copart product analyst before day one.

## 6. Next Steps (pick up here in a new conversation)

1. Pull the Copart dataset and start exploratory analysis (null rates, completeness by segment)
2. Once the root-cause finding is confirmed, build the Tableau dashboard
3. Build the 3-slide recommendation deck
4. Draft the tailored Copart cover letter, referencing this project as "in progress" or "completed" depending on timing
5. After Copart, circle back to Delta Electronics cover letter (second priority)
