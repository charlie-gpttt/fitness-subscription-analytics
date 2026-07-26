This README summarizes the key business insights from the `report.twb` Tableau workbook, built on the `Fitness_Subscriptions_Dataset` (customers + transactions, Jan 2024 – Jan 2026, 9,300 customers / ~65,000 transactions).

---

## 1. Customer Cohort Analysis — When do customers typically cancel?

**Most customers churn within their first 2–3 months.**

Looking at retention by "months since first purchase" across all cohorts:

| Months since first purchase | % of cohort still active |
|---|---|
| 0 (signup month) | 100% |
| 1 | 85% |
| 2 | 78% |
| **3** | **50%** |
| 6 | 44% |
| 12 | 36% |
| 24 | 30% |

There's a sharp cliff between month 2 and month 3, where retention drops from 78% to 50%. This is confirmed by looking at customer tenure directly: the single most common tenure length (mode) is **2 months**, and the median tenure is **3 months**.

After that initial drop-off, the customers who remain are much more loyal — the decline slows dramatically and roughly 30–35% of any cohort is still transacting a year or more later.

**Takeaway:** the biggest churn risk window is months 2–3 after acquisition. Retention efforts (onboarding, engagement nudges, check-ins) are likely to have the highest ROI if concentrated in that window, rather than spread evenly across the customer lifecycle.

---

## 2. Revenue Forecast — Next 12 months & seasonality

**Forecasted revenue for the next 12 months (Feb 2026 – Jan 2027): ≈ $3,175,000**, growing from about $214K/month in Feb 2026 to $324K/month by Dec 2026, following the same trend the business has shown since 2024.

**Yes — the forecast shows clear seasonality.** Two years of data (2024 and 2025) both show the same pattern:

- **November–December: a strong seasonal spike** (roughly +$22K to +$25K above trend)
- **January: a sharp seasonal dip** (roughly –$23K below trend) — revenue fell -13% in Jan 2025 and -30% in Jan 2026 versus the prior month, both immediately after a Nov/Dec peak

This means the forecast isn't a straight upward line — it's an upward trend *with* a recurring end-of-year peak followed by a January drop. The forecast projects this pattern to repeat: a peak around $324K in Dec 2026, followed by a dip to roughly $284K in Jan 2027.

**Takeaway:** the January dip is a real, recurring pattern (2 years in a row), not noise — it should be planned for in budgeting and staffing rather than treated as a one-off anomaly. Understanding *why* (e.g., New Year promotions ending, holiday-gifted memberships lapsing) would help the business get ahead of it.

---

## 3. CAC vs. LTV — How long to recover acquisition cost?

Comparing cumulative revenue (LTV) per cohort against that cohort's total customer acquisition cost (CAC):

| Cohort | Customers | Total CAC | Avg. CAC/customer | Months to break even |
|---|---|---|---|---|
| **2024** | 2,816 | $501,537 | ~$178 | **~4 months** |
| **2025** | 3,119* | $563,056 | ~$181 | **~5 months** |

*\*Restricted to customers acquired early enough in 2025 to have at least 6 full months of observed data, so the comparison is apples-to-apples with the 2024 cohort rather than mixing mature and very-recent customers.*

Both cohorts recover their acquisition cost quickly — **within about 4 to 5 months** — which is healthy relative to a subscription business with monthly recurring billing. The 2025 cohort took slightly longer to break even than 2024, even though average CAC per customer barely changed (~$178 → ~$181). This points to the extra month coming from revenue pacing/mix in the 2025 cohort rather than rising acquisition costs.

**Takeaway:** CAC recovery is fast and consistent year over year, which supports continuing to invest in acquisition. Worth monitoring whether the slight slowdown in payback (4 → 5 months) continues into 2026 cohorts, since it could signal early softening in early-cohort spend or a shift in acquisition channel mix.

---

## Notes on methodology

- Cohort = calendar month/year of a customer's first transaction (`FIXED [Customer_ID] : MIN([Transaction_Date])` in Tableau).
- Revenue forecast uses exponential smoothing with trend + additive seasonality (12-month period), matching Tableau's native forecasting model (`model-type='auto-season'` in the workbook).
- CAC vs. LTV total CAC uses `{ FIXED YEAR([Cohort Month]) : SUM([CAC]) }` so it correctly recalculates when filtering the "CAC vs LTV" sheet by cohort year.
- All figures are point estimates from historical data through January 2026; the most recent 1–2 months of any cohort are naturally less mature and were excluded where they would bias the comparison (see CAC vs LTV caveat above).
