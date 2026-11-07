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
