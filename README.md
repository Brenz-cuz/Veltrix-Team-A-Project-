# Veltrix-Team-A-Project-
Data dictionary Markdown

## Data Dictionary

### Table: core.customers

# Veltrix Data Dictionary

## Notes

- Schema: core.
- Nullable indicates whether the database permits NULL.
- TIMESTAMP below means timestamp without time zone.
- Identifier columns are not labelled as enforced primary or foreign keys
  because this metadata query does not report those constraints.
- GBP means pounds sterling; PCM means per calendar month.
- No column defaults were reported.
- These are initial entries covering selected fields in each table.

  ----  IDENTIFIES THE DATA DICTIONARIES IN EACH TABLE AND COLUMNS 

SELECT
    table_name,
    column_name,
    data_type,
    is_nullable,
    column_default
FROM information_schema.columns
WHERE table_schema = 'core'
ORDER BY table_name, ordinal_position;

## 1. Customers - core.customers

Customer profiles, property requirements and stated budgets.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| customer_id | TEXT | No | Customer identifier. |
| email_sha256 | TEXT | Yes | SHA-256 hash of the customer's email address. |
| phone_sha256 | TEXT | Yes | SHA-256 hash of the customer's phone number. |
| primary_intent | TEXT | Yes | Main property requirement, including Buy or Rent. |
| stated_budget_gbp | NUMERIC | Yes | Stated purchase budget in GBP. |
| stated_rent_budget_pcm_gbp | NUMERIC | Yes | Stated monthly rental budget in GBP. |
| preferred_currency | TEXT | Yes | Customer's preferred currency. |
| consent_marketing | BOOLEAN | Yes | Recorded marketing consent indicator. |
| created_at | TIMESTAMP | Yes | Customer record creation date and time. |

## 2. Leads - core.leads

Property enquiries and their progress.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| lead_id | TEXT | No | Lead identifier. |
| customer_id | TEXT | Yes | Associated customer identifier. |
| agent_id | TEXT | Yes | Associated agent identifier. |
| campaign_id | TEXT | Yes | Associated marketing campaign identifier. |
| lead_stage | TEXT | Yes | Recorded stage of the lead. |
| created_date | DATE | Yes | Lead creation date. |
| closed_date | DATE | Yes | Lead closure date. |
| converted | BOOLEAN | Yes | Recorded conversion indicator. |

## 3. Agents - core.agents

Agent team, branch and employment details.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| agent_id | TEXT | No | Agent identifier. |
| team | TEXT | Yes | Agent's team. |
| branch | TEXT | Yes | Agent's branch. |
| seniority | TEXT | Yes | Recorded seniority level. |
| hire_date | DATE | Yes | Hire date. |
| propertymark_qualified | BOOLEAN | Yes | Recorded Propertymark qualification indicator. |

## 4. Campaigns - core.campaigns

Marketing campaign details and expenditure.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| campaign_id | TEXT | No | Campaign identifier. |
| campaign_name | TEXT | Yes | Campaign name. |
| channel | TEXT | Yes | Marketing channel. |
| target_segment | TEXT | Yes | Intended customer segment. |
| start_date | DATE | Yes | Campaign start date. |
| end_date | DATE | Yes | Campaign end date. |
| spend_gbp | NUMERIC | Yes | Recorded campaign expenditure in GBP. |

## 5. Campaign Responses - core.campaign_responses

Customer responses to marketing campaigns.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| response_id | TEXT | No | Response identifier. |
| campaign_id | TEXT | Yes | Associated campaign identifier. |
| customer_id | TEXT | Yes | Associated customer identifier. |
| response_type | TEXT | Yes | Recorded response category. |
| response_time | TIMESTAMP | Yes | Recorded response date and time. |

## 6. Interactions - core.interactions

Communications associated with leads and agents.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| interaction_id | TEXT | No | Interaction identifier. |
| lead_id | TEXT | Yes | Associated lead identifier. |
| agent_id | TEXT | Yes | Associated agent identifier. |
| channel | TEXT | Yes | Communication channel. |
| direction | TEXT | Yes | Recorded communication direction. |
| interaction_time | TIMESTAMP | Yes | Interaction date and time. |
| response_time_min | NUMERIC | Yes | Recorded response time in minutes. |

## 7. Locations - core.locations

Geographic areas and market indicators.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| location_id | TEXT | No | Location identifier. |
| area_name | TEXT | Yes | Area name. |
| region | TEXT | Yes | Geographic region. |
| country | TEXT | Yes | Country. |
| avg_price_per_sqm_gbp | NUMERIC | Yes | Average property price per square metre in GBP. |
| avg_gross_yield_pct | NUMERIC | Yes | Recorded average gross yield percentage. |
| latitude | DOUBLE PRECISION | Yes | Latitude coordinate. |
| longitude | DOUBLE PRECISION | Yes | Longitude coordinate. |

## 8. Properties - core.properties

Property characteristics and advertised prices.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| property_id | TEXT | No | Property identifier. |
| location_id | TEXT | Yes | Associated location identifier. |
| property_type | TEXT | Yes | Recorded property category. |
| bedrooms | INTEGER | Yes | Number of bedrooms. |
| size_sqm | NUMERIC | Yes | Property size in square metres. |
| asking_price_gbp | NUMERIC | Yes | Advertised purchase price in GBP. |
| rent_pcm_gbp | NUMERIC | Yes | Advertised monthly rent in GBP. |
| new_build | BOOLEAN | Yes | Recorded new-build indicator. |
| first_marketed_date | DATE | Yes | Date the property was first marketed. |

## 9. Web Sessions - core.web_sessions

Website sessions and activity measures.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| session_id | TEXT | No | Website session identifier. |
| customer_id | TEXT | Yes | Associated customer identifier, where recorded. |
| session_start | TIMESTAMP | Yes | Session start date and time. |
| device | TEXT | Yes | Recorded device category. |
| traffic_source | TEXT | Yes | Recorded traffic source. |
| pages_viewed | INTEGER | Yes | Number of pages viewed during the session. |
| duration_sec | NUMERIC | Yes | Session duration in seconds. |

## 10. Property Views - core.property_views

Website events associated with properties.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| view_id | TEXT | No | Property event identifier. |
| session_id | TEXT | Yes | Associated website session identifier. |
| property_id | TEXT | Yes | Associated property identifier. |
| event_type | TEXT | Yes | Recorded event category. |
| event_time | TIMESTAMP | Yes | Event date and time. |

## 11. Site Visits - core.site_visits

Property visits and recorded outcomes.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| visit_id | TEXT | No | Visit identifier. |
| lead_id | TEXT | Yes | Associated lead identifier. |
| property_id | TEXT | Yes | Associated property identifier. |
| visit_type | TEXT | Yes | Recorded visit category. |
| visit_date | DATE | Yes | Visit date. |
| outcome | TEXT | Yes | Recorded visit outcome. |

## 12. Transactions - core.transactions

Property transactions and agreed financial terms.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| transaction_id | TEXT | No | Transaction identifier. |
| lead_id | TEXT | Yes | Associated lead identifier. |
| customer_id | TEXT | Yes | Associated customer identifier. |
| property_id | TEXT | Yes | Associated property identifier. |
| agreed_price_gbp | NUMERIC | Yes | Agreed purchase price in GBP. |
| agreed_rent_pcm_gbp | NUMERIC | Yes | Agreed monthly rent in GBP. |
| contract_date | DATE | Yes | Contract date. |
| completion_or_move_in_date | DATE | Yes | Completion or move-in date. |
| tenancy_months | INTEGER | Yes | Recorded tenancy duration in months. |
| mortgage_ltv_pct | NUMERIC | Yes | Recorded mortgage loan-to-value percentage. |

## 13. Payments - core.payments

Payment amounts, dates and settlement status.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| payment_id | TEXT | No | Payment identifier. |
| transaction_id | TEXT | Yes | Associated transaction identifier. |
| due_date | DATE | Yes | Payment due date. |
| paid_date | DATE | Yes | Recorded payment date. |
| amount_gbp | NUMERIC | Yes | Recorded payment amount in GBP. |
| payment_currency | TEXT | Yes | Recorded payment currency. |
| status | TEXT | Yes | Recorded payment status. |
| days_late | INTEGER | Yes | Recorded number of days late. |

## 14. Customer Mapping - core.customer_mapping

Supporting table created during duplicate-customer cleaning.
This is additional to the 13 original case study tables.

| Column | Data type | Nullable | Description |
|---|---|---|---|
| duplicate_customer_id | TEXT | No | Customer identifier whose related records are to be re-pointed. |
| surviving_customer_id | TEXT | No | Customer identifier retained as the destination for related records. |



# Veltrix Feature Documentation and Leakage Review

## Purpose and grain

The feature views summarise customer behaviour, requirements and engagement.
Each view contains at most one row per customer_id.

Outcome fields are stored separately in core.customer_outcomes.

Customers without activity may be absent from individual activity views.
When building the final customer table, start from core.customers and
LEFT JOIN each aggregated view by customer_id.

## 1. Website Session Features

Source: core.v_customer_sessions
Underlying table: core.web_sessions

| Feature | Definition | Unit | Missing-value handling |
|---|---|---|---|
| total_sessions | Number of identified website sessions. | Sessions | Use 0 where a customer has no recorded sessions. |
| total_pages_viewed | Sum of pages_viewed across sessions. | Pages | Use 0 for no sessions; retain NULL if activity exists but values are entirely missing. |
| total_duration_sec | Sum of recorded session durations. | Seconds | Use 0 for no sessions; retain NULL if durations are entirely missing. |
| avg_session_duration_sec | Average recorded session duration. | Seconds | Retain NULL when no duration observations exist. |
| first_session_at | Earliest recorded session start. | Timestamp | Retain NULL when no sessions exist. |
| last_session_at | Latest recorded session start. | Timestamp | Retain NULL when no sessions exist. |

Unidentified sessions are excluded from customer-level attribution.

## 2. Property-View Features

Source: core.v_customer_property_view_summary
Underlying tables: core.property_views and core.web_sessions

Only events with event_type = 'View' are included.

| Feature | Definition | Unit | Missing-value handling |
|---|---|---|---|
| total_property_views | Number of property-view events, including repeat views. | Events | Use 0 for customers with no recorded views. |
| distinct_properties_viewed | Number of different properties viewed. | Properties | Use 0 for customers with no recorded views. |
| sessions_with_property_views | Number of sessions containing property-view events. | Sessions | Use 0 for customers with no recorded views. |
| first_property_view_at | Earliest recorded property-view event. | Timestamp | Retain NULL when no views exist. |
| last_property_view_at | Latest recorded property-view event. | Timestamp | Retain NULL when no views exist. |

Save, Share, Virtual tour and Floorplan download events are excluded.

## 3. Viewed-Price Features for Budget Imputation

Source: core.v_customer_viewed_budget_medians
Underlying tables: core.property_views, core.web_sessions and core.properties

Only View events and positive, non-null advertised prices contribute.

| Feature | Definition | Unit | Missing-value handling |
|---|---|---|---|
| median_asking_price_gbp | Median advertised purchase price across property-view events. | GBP | Retain NULL when no qualifying purchase prices exist. |
| median_rent_pcm_gbp | Median advertised monthly rent across property-view events. | GBP per month | Retain NULL when no qualifying rents exist. |
| purchase_price_view_count | Number of view events contributing to the purchase-price median. | Events | Use 0 when no qualifying events exist. |
| rent_price_view_count | Number of view events contributing to the rental median. | Events | Use 0 when no qualifying events exist. |

Repeated views give a property repeated weight in the median.
These are behavioural budget estimates, not confirmed affordability.

No customer budgets have been imputed by this view alone.
If used for imputation, preserve stated budgets and record the estimate's
source and supporting observation count.

## 4. Enquiry and Viewing Features

Source: core.v_customer_enquiry_features
Underlying tables: core.leads, core.interactions and core.site_visits

| Feature | Definition | Unit | Missing-value handling |
|---|---|---|---|
| total_enquiries | Number of associated lead records. | Leads | 0 when no leads exist. |
| avg_response_time_min | Average non-negative recorded interaction response time. | Minutes | Retain NULL when no qualifying observations exist. |
| response_time_observations | Number of interactions contributing to the response-time average. | Interactions | 0 when no qualifying observations exist. |
| total_recorded_visits | Number of associated site-visit records. | Visits | 0 when no visits are recorded. |

Visits include In person, Virtual, Open house and Proxy types.
The observed outcomes are consistent with visits having taken place.
A second-viewing request does not itself count as a second completed visit.

Response time reflects recorded interaction handling and may be influenced
by agent workload, channel and service processes. It is not established
as a measure of customer response speed.

## 5. Outcome Fields — Evaluation Only

Source: core.customer_outcomes

| Field | Definition | Handling |
|---|---|---|
| converted | TRUE if any associated lead is marked converted. | NULL when no non-null lead conversion information exists. |
| avg_days_to_decision | Mean days from lead creation to closure, using valid date pairs. | NULL when no qualifying pairs exist. Closure is a proxy for decision. |
| decision_observations | Number of lead date pairs contributing to the average. | 0 when none qualify. |
| on_time_payments | Number of qualifying payments paid by their due date. | Includes only positive amounts with known paid and due dates. |
| payments_with_known_timing | Number of positive payments with known paid and due dates. | Denominator for the payment rate. |
| on_time_payment_rate | On-time payments divided by payments with known timing. | Proportion from 0 to 1; NULL when the denominator is 0. |

Unpaid payments are excluded from this rate.
The four unresolved negative payment amounts are also excluded.

All fields in this outcome table, including supporting counts, are excluded
from clustering inputs.

## 6. Leakage Review

| Field or feature group | Risk | Required treatment |
|---|---|---|
| customer_id | Identifier may introduce arbitrary distances or categories. | Use only for joins and traceability; exclude from model inputs. |
| converted and decision-time fields | Direct outcome information. | Keep in the outcome table for evaluation. |
| Payment rate and payment counts | Information arising from transactions and settlement. | Exclude from clustering inputs. |
| Total sessions, views, enquiries and visits | Current views include all available activity, potentially after conversion or the intended scoring date. | Restrict source records to the agreed observation cutoff before modelling. |
| Response-time features | Later interactions may occur after the intended scoring point. | Restrict to interactions whose response information was available by the cutoff. |
| First/last activity timestamps | May reveal later activity and differences in customer tenure. | Apply the cutoff; derive recency or tenure where useful instead of using raw timestamps. |
| Viewed-price medians | Later views can reveal preferences that were unknown earlier. | Use only eligible views available by the cutoff. |
| Advertised property prices | Current prices may differ from prices displayed when the customer viewed the property. | Use historical prices if available; otherwise document this limitation. |
| Customer profile and stated budgets | Current values may have been updated after the scoring point. | Use historical snapshots where available; otherwise disclose the limitation. |
| Budget imputation and preprocessing | Fitting on validation/test records can contaminate evaluation. | Fit shared imputation, scaling and encoding rules on training data only when using a train/test split. |

## 7. Timing Rules

For descriptive segmentation:
- Choose a fixed snapshot date.
- Include only information available by that date.
- Describe subsequent outcome comparisons as associations.

For segmentation intended for early lead routing:
- Define an observation period, such as the first agreed number of days
  after lead creation.
- Use only information available during that period.
- Evaluate outcomes occurring after the observation period.
- Account for customers with multiple leads so that later lead activity
  does not enter an earlier lead's feature window.

The observation period must be chosen before interpreting model results.

## 8. Current Review Status

- Outcome fields are stored separately from behavioural features.
- Each activity source is aggregated before joining customer summaries,
  reducing the risk of inflated counts.
- Customer identifiers must be excluded from clustering inputs.
- The existing views do not yet enforce an observation cutoff.
- Historical availability of profile changes and property prices is unverified.
- Timing leakage checks therefore remain outstanding.

  

# Veltrix: Provisional Customer Segment Names

The following names describe the observed characteristics and behaviour of customers in the three candidate clustering solutions: K6, K7 and K8.

Segment numbers are specific to each solution. For example, Segment 1 in K6 does not necessarily represent the same customer group as Segment 1 in K7.

## K6: Six-Segment Solution

| Segment | Provisional name | One-line description |
|---|---|---|
| Segment 1 | Low-digital, direct enquirers | Very little recorded browsing, but around one enquiry and three viewings per customer. |
| Segment 2 | Light-browsing, active enquirers | Occasional online browsing alongside regular enquiries and viewings. |
| Segment 3 | Browsers with limited direct engagement | Mainly buyers exploring properties online with very few enquiries or viewings. |
| Segment 4 | Higher-budget, engaged buyers | Mainly buyers with higher estimated budgets, regular viewings and a comparatively high overseas share. |
| Segment 5 | Lower-budget, highly engaged buyers | Predominantly UK-based buyers with lower estimated budgets and strong enquiry and viewing activity. |
| Segment 6 | Intensive property browsers | Extensive online browsing with very little recorded enquiry or viewing activity. |

## K7: Seven-Segment Solution

| Segment | Provisional name | One-line description |
|---|---|---|
| Segment 1 | Occasional property explorers | Light online browsing, few enquiries and almost no recorded viewings. |
| Segment 2 | Light-browsing, viewing-active customers | Limited online browsing but comparatively strong direct engagement through enquiries and viewings. |
| Segment 3 | Low-digital, direct enquirers | Minimal recorded online activity, but around one enquiry and three viewings per customer. |
| Segment 4 | Regular browsers with limited enquiries | Regular online property exploration with few enquiries and almost no recorded viewings. |
| Segment 5 | Higher-budget, engaged buyers | Mainly buyers with higher estimated budgets, regular viewings and around 21% overseas customers. |
| Segment 6 | Lower-budget, highly engaged buyers | Predominantly UK-based buyers with lower estimated budgets and strong enquiry and viewing activity. |
| Segment 7 | Intensive property browsers | Very high session and property-view activity with little recorded direct engagement. |

## K8: Eight-Segment Solution

| Segment | Provisional name | One-line description |
|---|---|---|
| Segment 1 | Occasional property explorers | Light online browsing, very few enquiries and no recorded viewings. |
| Segment 2 | Light-browsing, viewing-active customers | Limited online browsing alongside comparatively strong enquiry and viewing activity. |
| Segment 3 | Low-digital, direct enquirers | Minimal recorded browsing, but around one enquiry and three viewings per customer. |
| Segment 4 | Regular browsers without viewings | Regular property browsing with very few enquiries and no recorded viewings. |
| Segment 5 | Lower-budget, browsing-led buyers | Predominantly UK-based buyers with lower estimated budgets and more browsing than direct engagement. |
| Segment 6 | Higher-budget, internationally mixed buyers | Mainly buyers with higher estimated budgets, regular viewings and around 22% overseas customers. |
| Segment 7 | Intensive property browsers | Extensive online property exploration with very few enquiries or recorded viewings. |
| Segment 8 | Lower-budget, viewing-intensive buyers | Mainly buyers with lower estimated budgets and the strongest enquiry and viewing activity in K8. |

## Interpretation Notes

- Names are provisional and describe group tendencies rather than every individual.
- Higher and lower budgets are relative to this dataset; budget estimates include imputed values.
- Low recorded online activity does not establish a preferred contact channel.
- High browsing activity does not necessarily indicate readiness to purchase.
- Activity totals cover the available observation period and may reflect differences in customer tenure.
- These are descriptive customer profiles; using them for early lead routing requires features restricted to information available at the routing date.


# Veltrix: Provisional Customer Persona Cards

These 21 cards describe the alternative K6, K7 and K8 solutions. Each solution covers the same **101,598 surviving customers**; do not add their populations together. Segment IDs are specific to each solution. Each card is a compact, standalone persona suitable for a one-page layout; Markdown itself does not enforce printed page breaks.

## How to read the cards

- **Size:** customer count and share within that candidate solution.
- **Value:** separate median estimated purchase and monthly rental budgets, plus recorded conversion among customers with known outcomes. Budgets indicate requirements, not revenue, wealth or profitability. Estimates combine stated budgets and imputed values.
- **Behaviour:** mean recorded activity per customer across the available history. Recorded visits include in-person, virtual, open-house and proxy visits.
- **Channels:** suggested channels to test, not measured preferences. These profiles do not include segment-level channel performance. Check recorded preferences and marketing consent before contact.
- **Interpretation:** group tendencies are not individual facts. Different observation lengths can affect activity totals. Missing outcomes do not mean non-conversion. These snapshot segments are descriptive and have not been cleared for early lead routing.
- **Scope:** no age-based persona labels are assigned because the reviewed profiles do not establish dominant age groups. Conversion is an evaluation outcome, not a clustering input. No segment-level collected-receipts figures are available in the profile source, so none are invented here.

Source: `segment_profiles.csv` and methodology in `Veltrix_Candidate_Segments_Complete.zip`. Payment outcomes are omitted from these cards because the previously reported SQL results are more current and small payment samples require separate interpretation. All recommended approaches are proposals to test.

---

## K6 · Segment 1: Low-digital, direct enquirers

**Size:** 7,387 customers · 7.3% of K6.

### Customer characteristics

- **Purchase intent:** 72.0% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 9.3%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £315,000 |
| Median estimated monthly rent budget — Rent customers | £1,500.00 pcm |
| Recorded conversion rate — known outcomes only | 24.9% |
| Customers with known conversion outcomes | 5,546 / 7,387 (75.1%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 0.3 |
| Property View events | 1.7 |
| Enquiries | 1.05 |
| Recorded viewings / visits | 2.59 |

### Channels to test

Offer telephone follow-up or an appointment after an enquiry; provide a concise email summary if requested. Channel preference has not been verified for this segment.

### Recommended approach

Make direct enquiry handling straightforward and avoid requiring customers to complete an extensive online journey. Confirm intent, budget and preferred contact method before arranging a suitable viewing.

**Measure success:** Enquiry-to-viewing progression and successful contact rate. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Low digital activity describes the recorded data; it does not prove a preference for telephone or branch contact.

---

## K6 · Segment 2: Light-browsing, active enquirers

**Size:** 9,852 customers · 9.7% of K6.

### Customer characteristics

- **Purchase intent:** 72.0% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 6.9%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £345,000 |
| Median estimated monthly rent budget — Rent customers | £1,750.00 pcm |
| Recorded conversion rate — known outcomes only | 27.0% |
| Customers with known conversion outcomes | 8,061 / 9,852 (81.8%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 2.8 |
| Property View events | 7.2 |
| Enquiries | 1.17 |
| Recorded viewings / visits | 2.94 |

### Channels to test

Offer telephone or email viewing coordination, according to the customer’s stated preference. Channel preference has not been verified for this segment.

### Recommended approach

Prioritise relevant shortlists and convenient viewing arrangements. Use their enquiry details to personalise follow-up rather than waiting for more website activity.

**Measure success:** Viewing attendance and subsequent enquiry or offer progression. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K6 · Segment 3: Browsers with limited direct engagement

**Size:** 21,784 customers · 21.4% of K6.

### Customer characteristics

- **Purchase intent:** 74.0% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 9.2%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £370,000 |
| Median estimated monthly rent budget — Rent customers | £1,550.00 pcm |
| Recorded conversion rate — known outcomes only | 0.1% |
| Customers with known conversion outcomes | 2,008 / 21,784 (9.2%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 7.2 |
| Property View events | 36.3 |
| Enquiries | 0.09 |
| Recorded viewings / visits | 0.01 |

### Channels to test

Test consented email shortlists and website enquiry prompts; provide an optional adviser callback. Channel preference has not been verified for this segment.

### Recommended approach

Help customers narrow their search using relevant shortlists and clearer property information. Test a low-pressure invitation to speak to an adviser.

**Measure success:** Browsing-to-enquiry progression and viewing bookings. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Known conversion outcomes cover only a minority of this segment; the observed rate should not be generalised to all members. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K6 · Segment 4: Higher-budget, engaged buyers

**Size:** 17,462 customers · 17.2% of K6.

### Customer characteristics

- **Purchase intent:** 81.5% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 20.0%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £485,000 |
| Median estimated monthly rent budget — Rent customers | £2,150.00 pcm |
| Recorded conversion rate — known outcomes only | 23.8% |
| Customers with known conversion outcomes | 17,462 / 17,462 (100.0%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 12.2 |
| Property View events | 66.0 |
| Enquiries | 1.48 |
| Recorded viewings / visits | 3.79 |

### Channels to test

Offer an adviser-led telephone or video appointment and an emailed shortlist, based on preference; use virtual viewing options where helpful. Channel preference has not been verified for this segment.

### Recommended approach

Provide a tailored shortlist within the customer’s confirmed budget. Ask whether remote coordination is useful; offer it where requested rather than assuming every customer is overseas.

**Measure success:** Relevant viewing bookings, enquiry progression and customer feedback. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Overseas customers are a minority; offer remote support based on individual needs.

---

## K6 · Segment 5: Lower-budget, highly engaged buyers

**Size:** 24,420 customers · 24.0% of K6.

### Customer characteristics

- **Purchase intent:** 83.2% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 3.9%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £210,000 |
| Median estimated monthly rent budget — Rent customers | £1,150.00 pcm |
| Recorded conversion rate — known outcomes only | 29.6% |
| Customers with known conversion outcomes | 24,420 / 24,420 (100.0%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 13.8 |
| Property View events | 82.1 |
| Enquiries | 1.86 |
| Recorded viewings / visits | 4.84 |

### Channels to test

Offer concise email shortlists and telephone viewing coordination, following the customer’s preference. Channel preference has not been verified for this segment.

### Recommended approach

Focus on properties within confirmed affordability and coordinate viewings efficiently. Clarify financing needs without inferring financial circumstances from the cluster label.

**Measure success:** Viewing progression and shortlist relevance. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K6 · Segment 6: Intensive property browsers

**Size:** 20,693 customers · 20.4% of K6.

### Customer characteristics

- **Purchase intent:** 84.1% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 8.5%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £310,000 |
| Median estimated monthly rent budget — Rent customers | £1,350.00 pcm |
| Recorded conversion rate — known outcomes only | 0.9% |
| Customers with known conversion outcomes | 3,293 / 20,693 (15.9%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 37.0 |
| Property View events | 310.2 |
| Enquiries | 0.16 |
| Recorded viewings / visits | 0.06 |

### Channels to test

Test website comparison prompts and consented email shortlists; offer a callback rather than unsolicited intensive contact. Channel preference has not been verified for this segment.

### Recommended approach

Help customers reduce a broad search to a manageable shortlist. Test comparison tools and an optional adviser conversation; do not equate frequent browsing with readiness to transact.

**Measure success:** Browsing-to-enquiry progression and uptake of adviser support. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Known conversion outcomes cover only a minority of this segment; the observed rate should not be generalised to all members. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K7 · Segment 1: Occasional property explorers

**Size:** 8,586 customers · 8.5% of K7.

### Customer characteristics

- **Purchase intent:** 71.1% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 8.6%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £400,000 |
| Median estimated monthly rent budget — Rent customers | £1,900.00 pcm |
| Recorded conversion rate — known outcomes only | 0.0% |
| Customers with known conversion outcomes | 847 / 8,586 (9.9%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 3.8 |
| Property View events | 12.5 |
| Enquiries | 0.10 |
| Recorded viewings / visits | 0.00 |

### Channels to test

Test consented email property alerts and helpful website prompts; offer direct contact when requested. Channel preference has not been verified for this segment.

### Recommended approach

Offer a simple route from browsing to an enquiry. Test concise property recommendations and a clear invitation to book a viewing without assuming purchase readiness.

**Measure success:** New enquiries per contacted customer and alert engagement. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Known conversion outcomes cover only a minority of this segment; the observed rate should not be generalised to all members. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K7 · Segment 2: Light-browsing, viewing-active customers

**Size:** 9,850 customers · 9.7% of K7.

### Customer characteristics

- **Purchase intent:** 71.8% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 6.5%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £330,000 |
| Median estimated monthly rent budget — Rent customers | £1,700.00 pcm |
| Recorded conversion rate — known outcomes only | 30.5% |
| Customers with known conversion outcomes | 9,850 / 9,850 (100.0%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 3.3 |
| Property View events | 10.2 |
| Enquiries | 1.55 |
| Recorded viewings / visits | 4.16 |

### Channels to test

Offer telephone or email viewing coordination, according to the customer’s stated preference. Channel preference has not been verified for this segment.

### Recommended approach

Prioritise relevant shortlists and convenient viewing arrangements. Use their enquiry details to personalise follow-up rather than waiting for more website activity.

**Measure success:** Viewing attendance and subsequent enquiry or offer progression. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K7 · Segment 3: Low-digital, direct enquirers

**Size:** 7,213 customers · 7.1% of K7.

### Customer characteristics

- **Purchase intent:** 72.1% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 9.4%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £315,000 |
| Median estimated monthly rent budget — Rent customers | £1,500.00 pcm |
| Recorded conversion rate — known outcomes only | 24.3% |
| Customers with known conversion outcomes | 5,354 / 7,213 (74.2%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 0.3 |
| Property View events | 1.7 |
| Enquiries | 1.03 |
| Recorded viewings / visits | 2.51 |

### Channels to test

Offer telephone follow-up or an appointment after an enquiry; provide a concise email summary if requested. Channel preference has not been verified for this segment.

### Recommended approach

Make direct enquiry handling straightforward and avoid requiring customers to complete an extensive online journey. Confirm intent, budget and preferred contact method before arranging a suitable viewing.

**Measure success:** Enquiry-to-viewing progression and successful contact rate. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Low digital activity describes the recorded data; it does not prove a preference for telephone or branch contact.

---

## K7 · Segment 4: Regular browsers with limited enquiries

**Size:** 20,347 customers · 20.0% of K7.

### Customer characteristics

- **Purchase intent:** 76.1% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 8.6%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £317,500 |
| Median estimated monthly rent budget — Rent customers | £1,375.00 pcm |
| Recorded conversion rate — known outcomes only | 0.0% |
| Customers with known conversion outcomes | 2,188 / 20,347 (10.8%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 10.2 |
| Property View events | 58.3 |
| Enquiries | 0.11 |
| Recorded viewings / visits | 0.00 |

### Channels to test

Test consented email shortlists and website enquiry prompts; provide an optional adviser callback. Channel preference has not been verified for this segment.

### Recommended approach

Help customers narrow their search using relevant shortlists and clearer property information. Test a low-pressure invitation to speak to an adviser.

**Measure success:** Browsing-to-enquiry progression and viewing bookings. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Known conversion outcomes cover only a minority of this segment; the observed rate should not be generalised to all members. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K7 · Segment 5: Higher-budget, engaged buyers

**Size:** 16,617 customers · 16.4% of K7.

### Customer characteristics

- **Purchase intent:** 82.4% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 20.6%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £490,000 |
| Median estimated monthly rent budget — Rent customers | £2,168.75 pcm |
| Recorded conversion rate — known outcomes only | 22.2% |
| Customers with known conversion outcomes | 16,617 / 16,617 (100.0%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 12.7 |
| Property View events | 69.3 |
| Enquiries | 1.44 |
| Recorded viewings / visits | 3.60 |

### Channels to test

Offer an adviser-led telephone or video appointment and an emailed shortlist, based on preference; use virtual viewing options where helpful. Channel preference has not been verified for this segment.

### Recommended approach

Provide a tailored shortlist within the customer’s confirmed budget. Ask whether remote coordination is useful; offer it where requested rather than assuming every customer is overseas.

**Measure success:** Relevant viewing bookings, enquiry progression and customer feedback. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Overseas customers are a minority; offer remote support based on individual needs.

---

## K7 · Segment 6: Lower-budget, highly engaged buyers

**Size:** 23,476 customers · 23.1% of K7.

### Customer characteristics

- **Purchase intent:** 83.6% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 3.9%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £210,000 |
| Median estimated monthly rent budget — Rent customers | £1,150.00 pcm |
| Recorded conversion rate — known outcomes only | 29.6% |
| Customers with known conversion outcomes | 23,476 / 23,476 (100.0%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 14.3 |
| Property View events | 85.4 |
| Enquiries | 1.86 |
| Recorded viewings / visits | 4.84 |

### Channels to test

Offer concise email shortlists and telephone viewing coordination, following the customer’s preference. Channel preference has not been verified for this segment.

### Recommended approach

Focus on properties within confirmed affordability and coordinate viewings efficiently. Clarify financing needs without inferring financial circumstances from the cluster label.

**Measure success:** Viewing progression and shortlist relevance. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K7 · Segment 7: Intensive property browsers

**Size:** 15,509 customers · 15.3% of K7.

### Customer characteristics

- **Purchase intent:** 85.8% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 9.0%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £335,000 |
| Median estimated monthly rent budget — Rent customers | £1,400.00 pcm |
| Recorded conversion rate — known outcomes only | 1.0% |
| Customers with known conversion outcomes | 2,458 / 15,509 (15.8%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 43.9 |
| Property View events | 379.6 |
| Enquiries | 0.16 |
| Recorded viewings / visits | 0.06 |

### Channels to test

Test website comparison prompts and consented email shortlists; offer a callback rather than unsolicited intensive contact. Channel preference has not been verified for this segment.

### Recommended approach

Help customers reduce a broad search to a manageable shortlist. Test comparison tools and an optional adviser conversation; do not equate frequent browsing with readiness to transact.

**Measure success:** Browsing-to-enquiry progression and uptake of adviser support. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Known conversion outcomes cover only a minority of this segment; the observed rate should not be generalised to all members. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K8 · Segment 1: Occasional property explorers

**Size:** 7,324 customers · 7.2% of K8.

### Customer characteristics

- **Purchase intent:** 70.6% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 7.8%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £380,000 |
| Median estimated monthly rent budget — Rent customers | £1,800.00 pcm |
| Recorded conversion rate — known outcomes only | 0.0% |
| Customers with known conversion outcomes | 792 / 7,324 (10.8%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 3.5 |
| Property View events | 10.6 |
| Enquiries | 0.11 |
| Recorded viewings / visits | 0.00 |

### Channels to test

Test consented email property alerts and helpful website prompts; offer direct contact when requested. Channel preference has not been verified for this segment.

### Recommended approach

Offer a simple route from browsing to an enquiry. Test concise property recommendations and a clear invitation to book a viewing without assuming purchase readiness.

**Measure success:** New enquiries per contacted customer and alert engagement. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Known conversion outcomes cover only a minority of this segment; the observed rate should not be generalised to all members. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K8 · Segment 2: Light-browsing, viewing-active customers

**Size:** 9,402 customers · 9.3% of K8.

### Customer characteristics

- **Purchase intent:** 71.8% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 6.7%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £340,000 |
| Median estimated monthly rent budget — Rent customers | £1,725.00 pcm |
| Recorded conversion rate — known outcomes only | 30.6% |
| Customers with known conversion outcomes | 9,402 / 9,402 (100.0%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 3.3 |
| Property View events | 9.9 |
| Enquiries | 1.52 |
| Recorded viewings / visits | 4.11 |

### Channels to test

Offer telephone or email viewing coordination, according to the customer’s stated preference. Channel preference has not been verified for this segment.

### Recommended approach

Prioritise relevant shortlists and convenient viewing arrangements. Use their enquiry details to personalise follow-up rather than waiting for more website activity.

**Measure success:** Viewing attendance and subsequent enquiry or offer progression. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K8 · Segment 3: Low-digital, direct enquirers

**Size:** 7,152 customers · 7.0% of K8.

### Customer characteristics

- **Purchase intent:** 72.0% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 9.4%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £315,000 |
| Median estimated monthly rent budget — Rent customers | £1,500.00 pcm |
| Recorded conversion rate — known outcomes only | 24.2% |
| Customers with known conversion outcomes | 5,318 / 7,152 (74.4%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 0.3 |
| Property View events | 1.6 |
| Enquiries | 1.02 |
| Recorded viewings / visits | 2.51 |

### Channels to test

Offer telephone follow-up or an appointment after an enquiry; provide a concise email summary if requested. Channel preference has not been verified for this segment.

### Recommended approach

Make direct enquiry handling straightforward and avoid requiring customers to complete an extensive online journey. Confirm intent, budget and preferred contact method before arranging a suitable viewing.

**Measure success:** Enquiry-to-viewing progression and successful contact rate. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Low digital activity describes the recorded data; it does not prove a preference for telephone or branch contact.

---

## K8 · Segment 4: Regular browsers without viewings

**Size:** 19,785 customers · 19.5% of K8.

### Customer characteristics

- **Purchase intent:** 76.1% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 9.8%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £355,000 |
| Median estimated monthly rent budget — Rent customers | £1,450.00 pcm |
| Recorded conversion rate — known outcomes only | 0.0% |
| Customers with known conversion outcomes | 1,169 / 19,785 (5.9%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 9.5 |
| Property View events | 53.0 |
| Enquiries | 0.06 |
| Recorded viewings / visits | 0.00 |

### Channels to test

Test consented email shortlists and website enquiry prompts; provide an optional adviser callback. Channel preference has not been verified for this segment.

### Recommended approach

Help customers narrow their search using relevant shortlists and clearer property information. Test a low-pressure invitation to speak to an adviser.

**Measure success:** Browsing-to-enquiry progression and viewing bookings. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Known conversion outcomes cover only a minority of this segment; the observed rate should not be generalised to all members. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K8 · Segment 5: Lower-budget, browsing-led buyers

**Size:** 15,934 customers · 15.7% of K8.

### Customer characteristics

- **Purchase intent:** 80.3% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 4.0%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £220,000 |
| Median estimated monthly rent budget — Rent customers | £1,200.00 pcm |
| Recorded conversion rate — known outcomes only | 13.0% |
| Customers with known conversion outcomes | 15,907 / 15,934 (99.8%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 15.6 |
| Property View events | 90.2 |
| Enquiries | 1.14 |
| Recorded viewings / visits | 2.28 |

### Channels to test

Test consented email recommendations and website viewing prompts, with optional telephone support. Channel preference has not been verified for this segment.

### Recommended approach

Offer affordable, relevant shortlists and invite customers to clarify their requirements. Encourage a suitable viewing without treating online engagement alone as a commitment.

**Measure success:** Viewing bookings and enquiry progression among engaged browsers. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K8 · Segment 6: Higher-budget, internationally mixed buyers

**Size:** 14,479 customers · 14.3% of K8.

### Customer characteristics

- **Purchase intent:** 82.8% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 22.4%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £520,000 |
| Median estimated monthly rent budget — Rent customers | £2,300.00 pcm |
| Recorded conversion rate — known outcomes only | 22.8% |
| Customers with known conversion outcomes | 14,479 / 14,479 (100.0%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 12.6 |
| Property View events | 68.9 |
| Enquiries | 1.43 |
| Recorded viewings / visits | 3.61 |

### Channels to test

Offer an adviser-led telephone or video appointment and an emailed shortlist, based on preference; use virtual viewing options where helpful. Channel preference has not been verified for this segment.

### Recommended approach

Provide a tailored shortlist within the customer’s confirmed budget. Ask whether remote coordination is useful; offer it where requested rather than assuming every customer is overseas.

**Measure success:** Relevant viewing bookings, enquiry progression and customer feedback. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Overseas customers are a minority; offer remote support based on individual needs.

---

## K8 · Segment 7: Intensive property browsers

**Size:** 15,649 customers · 15.4% of K8.

### Customer characteristics

- **Purchase intent:** 85.1% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 8.4%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £330,000 |
| Median estimated monthly rent budget — Rent customers | £1,350.00 pcm |
| Recorded conversion rate — known outcomes only | 0.8% |
| Customers with known conversion outcomes | 1,850 / 15,649 (11.8%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 43.1 |
| Property View events | 373.6 |
| Enquiries | 0.12 |
| Recorded viewings / visits | 0.03 |

### Channels to test

Test website comparison prompts and consented email shortlists; offer a callback rather than unsolicited intensive contact. Channel preference has not been verified for this segment.

### Recommended approach

Help customers reduce a broad search to a manageable shortlist. Test comparison tools and an optional adviser conversation; do not equate frequent browsing with readiness to transact.

**Measure success:** Browsing-to-enquiry progression and uptake of adviser support. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Known conversion outcomes cover only a minority of this segment; the observed rate should not be generalised to all members. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.

---

## K8 · Segment 8: Lower-budget, viewing-intensive buyers

**Size:** 11,873 customers · 11.7% of K8.

### Customer characteristics

- **Purchase intent:** 86.4% Buy; remaining customers have Rent intent in this candidate dataset.
- **Overseas share:** 4.8%; this does not establish preferred contact channel.

### Value and observed outcomes

| Measure | Profile |
|---|---:|
| Median estimated purchase budget — Buy customers | £210,000 |
| Median estimated monthly rent budget — Rent customers | £1,250.00 pcm |
| Recorded conversion rate — known outcomes only | 45.6% |
| Customers with known conversion outcomes | 11,873 / 11,873 (100.0%) |

### Recorded behaviour

| Average per customer | Value |
|---|---:|
| Website sessions | 12.8 |
| Property View events | 78.9 |
| Enquiries | 2.65 |
| Recorded viewings / visits | 7.41 |

### Channels to test

Offer a named adviser by the customer’s preferred channel, with email viewing summaries and optional telephone follow-up. Channel preference has not been verified for this segment.

### Recommended approach

Coordinate viewings and follow-up carefully, summarise feedback and refine the shortlist. Confirm next steps and affordability without applying pressure or assuming readiness.

**Measure success:** Viewing-to-offer or application progression and follow-up completion. Evaluate any proposed contact strategy through a pilot rather than assuming an effect.

**Interpretation:** Conversion describes customers with recorded outcomes and does not establish future performance. Behaviour totals can reflect time observed and activity after conversion; they do not establish current intent.
