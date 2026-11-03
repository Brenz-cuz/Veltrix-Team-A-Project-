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
