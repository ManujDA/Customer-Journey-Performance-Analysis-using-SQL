# 📊 Customer Journey Performance Analysis (SQL | BigQuery)

## Overview  
This project analyses **end-to-end customer journeys** using the same event-level dataset provided for this analysis (`Funnel_analysis_raw events`).  
The goal is to understand how users progress through a digital service, where they drop off, and how effectively the journey converts into completed outcomes.

The work focuses on **measurement accuracy, data quality, and evidence-based insight**, reflecting how performance data is used in real digital and service teams to support decision-making.

---

## Dataset  

All analysis in this project is based on a **single source dataset** containing anonymised event-level interactions.

**Source fields used:**
- `user_pseudo_id` – anonymised user identifier  
- `event_name` – interaction or journey step  
- `event_timestamp` – time of the event  
- `category` – service or product category  
- `country` – user location  
- `device_type` – device used (Desktop, Mobile, Tablet)  

No external datasets or synthetic data were introduced.  
All metrics, charts, and conclusions shown below are derived directly from this dataset.

---

## Objectives  

- Reconstruct customer journeys across key service stages  
- Measure progression, conversion, and drop-off at each step  
- Identify friction points in the journey  
- Compare performance by device and geography  
- Translate findings into actionable recommendations  

---

## Methodology  

### 1. Data Quality & Event Deduplication  
Raw event data contains repeated interactions that can inflate counts.  
To ensure accurate measurement, events were deduplicated so that **each user contributes only one instance per event per journey stage**.

This was achieved using SQL window functions (`ROW_NUMBER()`), retaining the earliest occurrence of each event per user.

**Why this matters:**
- Prevents over-counting engagement  
- Produces realistic funnel conversion rates  
- Reflects true user progression through the service  

---

### 2. Journey & Funnel Definition  
Based on the dataset, six key events were selected to represent meaningful stages in the customer journey:

1. `page_view`  
2. `view_item`  
3. `add_to_cart`  
4. `add_shipping_info`  
5. `add_payment_info`  
6. `purchase`  

These stages represent increasing user commitment and readiness to complete the service.

---

### 3. Funnel & Conversion Calculations  
Using the deduplicated dataset:

- Unique users were counted at each stage  
- Conversion was calculated step-to-step and relative to `page_view`  
- Drop-off volumes were derived by comparing consecutive stages  

All calculations were performed using SQL aggregations to ensure transparency and reproducibility.

---

## Visual Analysis & How the Conclusions Were Reached  

### Conversion Rate by Device  
The chart below shows **purchase conversion relative to page views**, segmented by device type.

![Conversion Rate by Device](conversion_rate_by_device.png)

**How this was calculated:**
- Count of users who reached `purchase` per device  
- Divided by count of users who reached `page_view` on the same device  
- Calculated from the same deduplicated dataset  

**What this shows:**
- Mobile users convert slightly better than desktop  
- Tablet users show consistently lower conversion  
- Device-level differences highlight where usability or optimisation issues may exist  

---

### Overall Conversion by Journey Stage  
This chart shows how users progress through the full journey from entry to completion.

![Overall Conversion by Stage](overall_conversion_by_stage.png)

**How this was calculated:**
- Unique users counted at each funnel stage  
- Each stage expressed as a proportion of `page_view` users  
- Ordered using observed journey progression  

**What this shows:**
- A sharp drop between `view_item` and `add_to_cart`  
- Continued decline through checkout stages  
- Later-stage friction has a disproportionate impact on overall outcomes  

---

## Key Insights  

- Strong early engagement does not translate proportionally into completed outcomes  
- Checkout-related stages contribute most to overall conversion loss  
- Device performance varies, suggesting inconsistent user experience  
- Improving later stages would deliver the highest impact on completion rates  

---

## How This Supports Digital & Service Decision-Making  

This analysis demonstrates how event-level data can be used to:

- Measure whether a digital service behaves as intended  
- Identify where users disengage or encounter friction  
- Prioritise improvements with the greatest potential impact  
- Support discussions with product teams and service designers  

The same methodology could be applied to:
- Evaluating new digital features  
- Monitoring performance over time  
- Comparing alternative service journeys  

---

## Recommendations / Next Steps  

If applied in a live environment, next steps would include:

- Automated monitoring of drop-offs at key journey stages  
- Deeper segmentation by device, country, or category  
- Tracking time-to-completion as a core KPI  
- Using rolling averages for regular performance reporting  
- Feeding insights into continuous service improvement cycles  

---

## Tools & Skills Demonstrated  

- SQL (CTEs, window functions, ranking, aggregation)  
- BigQuery-style analytical querying  
- Funnel and journey analysis  
- Data quality validation  
- Performance visualisation  
- Translating data into actionable insights  

---

## Why This Matters  

Understanding how users move through digital services — and where they struggle — is critical for improving efficiency, reducing avoidable contact, and supporting scalable digital transformation.

This project demonstrates a **structured, evidence-led approach** to learning from customer journeys using a single, consistent dataset.
