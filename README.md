# Veltrix-Team-A-Project-
Data dictionary Markdown

## Data Dictionary

### Table: core.customers

Stores customer profiles, property requirements and stated budgets.

| Column | Description | Rules / Notes |
|---|---|---|
| customer_id | Unique identifier for each customer record. | Primary key; unique and not null. |
| email_sha256 | SHA-256 hash of the customer's email address. | Used to identify potential duplicates. |
| phone_sha256 | SHA-256 hash of the customer's phone number. | Used to identify potential duplicates. |
| primary_intent | Customer's main property requirement. | Observed values: Buy and Rent. |
| stated_budget_gbp | Stated property purchase budget in pounds sterling. | May be null. Suspected budget typos require review. |
| stated_rent_budget_pcm_gbp | Stated rental budget in pounds sterling per calendar month. | May be null. |
| preferred_currency | Customer's preferred currency. | Separate from the budget fields, which are labelled GBP. |
| created_at | Date and time the customer record was created. | Used when selecting the earliest-created record for proposed duplicate merges. |
