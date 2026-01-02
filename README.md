# A/B Test Feasibility & Sample Size Reality Checker

This project helps product teams decide **whether an A/B test is worth running at all**.

Instead of focusing only on statistical formulas, it incorporates **real-world constraints**—such as traffic volume, fixed timelines, and data loss—to answer a more practical question:

> *Can this experiment realistically reach statistical power before we need to make a decision?*

---

## Why this project exists

In practice, many A/B tests are launched even though they are **statistically impossible** to conclude within the available time or traffic.

This leads to:
- Inconclusive results
- Misleading “wins”
- Wasted engineering and product effort

This tool is designed as a **pre-experiment screening step** to help teams avoid running experiments that are unlikely to produce reliable outcomes.

---

## What the tool does

Given a set of **experiment assumptions and constraints**, the notebook:

1. Calculates the **required sample size per variant** using a two-sample test of proportions
2. Translates the sample size into **expected calendar days**, accounting for:
   - Daily traffic
   - Allocation splits
   - Data loss
   - Ramp-up or excluded days
3. Produces a clear **feasibility verdict**:
   -  Feasible
   -  Risky
   -  Not feasible
4. Provides **actionable recommendations** when an experiment is not viable
5. Includes a **sensitivity analysis** showing trade-offs between effect size and runtime

---

## What this project is *not*

- It does **not** analyze historical experiment data  
- It does **not** require a dataset  
- It does **not** replace a full experimentation platform  

This is an **upstream decision tool**, used *before* an experiment is launched.

---

## Key inputs

The notebook works entirely from planning assumptions that are typically known upfront:

- Baseline conversion rate
- Minimum Detectable Effect (absolute lift)
- Significance level (α)
- Statistical power (1 − β)
- Daily eligible traffic
- Allocation split (control / treatment)
- Maximum allowed experiment duration
- Ramp-up or novelty exclusion period
- Expected data loss / tracking gaps

These inputs reflect how experiments are planned in real product teams.

---

## Outputs

For each scenario, the tool outputs:

- Required sample size **per variant**
- Days needed to collect sufficient data
- Total calendar days (including ramp-up)
- A **feasibility verdict**
- Practical next-step recommendations if the test is not feasible

---

## Sensitivity analysis

Rather than relying on a single Minimum Detectable Effect (MDE), the notebook explores a **range of effect sizes** and shows:

- How required sample size changes
- How long each scenario would take to run
- Which MDEs are feasible within the same time constraint

This helps teams make **explicit trade-offs** between ambition and realism.

---

## Example scenarios

The notebook includes two illustrative cases:

### Scenario A: Low-traffic product
- Limited daily traffic
- Short decision window
- Small MDE

Result: **Not feasible**  
Correct decision: do not run the experiment.

---

### Scenario B: Healthy-traffic product
- High daily traffic
- Same statistical assumptions
- Same time constraint

Result:  **Feasible**  
Correct decision: experiment is likely to reach power.

---

## Methodology notes

- Sample size is calculated using a **normal approximation** for a two-sample test of proportions.
- This approach is standard for **experiment planning** when sample sizes are moderate to large.
- The focus is on **decision usefulness**, not perfect theoretical optimality.

---

## Limitations

- Assumes independent observations
- Does not account for clustering or variance reduction techniques (e.g. CUPED)
- Does not implement sequential testing
- Designed for planning, not final inference

These are intentional trade-offs for clarity and usability.

---

## How to run

The easiest way to run this project is via Google Colab.

1. Open the notebook
2. Run all cells top-to-bottom
3. Adjust the input parameters to match your product context

No setup or data is required.

---

## Why this matters for product analytics

Good experimentation is not just about running tests—it’s about **knowing when not to run them**.

This project demonstrates:
- Statistical literacy
- Product judgment
- Real-world experimentation thinking

It can be used as a **pre-launch checklist** for product, growth, and experimentation teams.

---
