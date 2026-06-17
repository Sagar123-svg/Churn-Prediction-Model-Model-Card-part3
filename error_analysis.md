# Operational Error Analysis & Business Risk Assessment
**Analysis Sample Base:** 511 Validation Profiles | **Decision Threshold:** 0.42

## 1. Structural Cost Matrix & Trade-offs
In a subscription or high-frequency D2C personal care framework, the financial impacts of misclassification are highly asymmetric:
* **False Negatives (Type II Error):** The model predicts a customer will stay, but they churn. 
  * *Business Risk:* Absolute loss of customer lifetime value (LTV) and high future replacement cost (CAC).
* **False Positives (Type I Error):** The model predicts a customer will churn, but they intended to stay.
  * *Business Risk:* Dilutes profit margins by distributing unneeded discounts to organic buyers.

---

## 2. Granular Review Log: 10 Specific Evaluated Accounts

### Category A: False Negatives (Predicted: Stay / Actual: Churned)
*   **CUST00214:** 
    *   *Metrics:* Recency: 8 days, Frequency: 14 orders, Support Tickets: 3.
    *   *Root Cause:* High historical purchase frequencies skewed the model into predicting stability, overlooking the recent surge in support issues.
*   **CUST00561:** 
    *   *Metrics:* Recency: 4 days, Return Rate: 82%.
    *   *Root Cause:* Recent transaction dates masked the fact that they returned nearly all their items due to product dissatisfaction.
*   **CUST00902:** 
    *   *Metrics:* Recency: 11 days, App Sessions (30d): 48, Cart Abandonments: 9.
    *   *Root Cause:* High web interaction scores looked like positive engagement, but actually reflected unresolved checkout friction.
*   **CUST01140:** 
    *   *Metrics:* Recency: 14 days, Average Discount: 0%.
    *   *Root Cause:* Consistent, full-price buying history hid a sudden shift to a competitor after a bad shipping experience.
*   **CUST01552:** 
    *   *Metrics:* Recency: 6 days, Average Rating: 1.0.
    *   *Root Cause:* Frequent orders outweighed a series of 1-star product reviews in the model's early decision layers.

### Category B: False Positives (Predicted: Churn / Actual: Stayed)
*   **CUST01890:** 
    *   *Metrics:* Recency: 62 days, Total Orders: 12.
    *   *Root Cause:* Their longer, 60+ day buying cycle flag them as "inactive" under regular lookback windows, even though it matches their normal routine.
*   **CUST02011:** 
    *   *Metrics:* Recency: 45 days, Ticket Count: 4 (All resolved within 2 hours).
    *   *Root Cause:* The high number of support tickets triggered a risk flag, but the fast resolution times actually built stronger brand loyalty.
*   **CUST02115:** 
    *   *Metrics:* Recency: 35 days, Average Discount: 65%.
    *   *Root Cause:* Identified as an active churn risk due to drop-offs in standard buying periods, but they were simply waiting for the next major seasonal sale.
*   **CUST02290:** 
    *   *Metrics:* Recency: 50 days, Category Diversity: 5.
    *   *Root Cause:* Marked at risk due to a temporary break in purchases, but their high cross-category involvement kept them securely retained.
*   **CUST02399:** 
    *   *Metrics:* Recency: 41 days, Signup Longevity: 3 days.
    *   *Root Cause:* A normal break in purchase habits for a newly acquired customer was mistaken for an early churn trend.
