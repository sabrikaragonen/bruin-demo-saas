# SaaS Demo Dataset

This dataset simulates a B2B SaaS company with 20 customers across different tiers (Enterprise, Growth, Starter). All data is linked via `company_id`.

## Data Sources

| File | Source | Description |
|------|--------|-------------|
| `companies.csv` | Internal | Customer master data with company info |
| `hubspot_crm_deals.csv` | HubSpot | Sales deals and renewal pipeline |
| `stripe_billing_history.csv` | Stripe | Raw payment transaction events |
| `intercom_support_data.csv` | Intercom | Raw support ticket events |
| `segment_usage_data.csv` | Segment | Raw product usage events |

---

## Sample Questions

### Churn & Risk Analysis
- "Which customers are at risk of churning?"
- "Show me customers with high ARR but low product usage"
- "Who has failed payments in the last 90 days?"
- "Which accounts have angry tickets and billing issues?"
- "List customers who haven't logged in for 30+ days"
- "Which enterprise customers have zero recent usage?"
- "Find customers with multiple failed payment attempts"

### Revenue & Renewals
- "What's our total ARR?"
- "What's the total ARR by account owner?"
- "Which customers have renewals in the next 30 days?"
- "Show me the top 10 customers by ARR"
- "What's the ARR breakdown by plan tier?"
- "Which region generates the most revenue?"
- "What's the average deal size by industry?"
- "Calculate total revenue collected last month"
- "What's our payment success rate by payment method?"

### Customer Health
- "Who are our happiest customers?"
- "Which customers have the most open support tickets?"
- "Show me customers with high usage and positive sentiment"
- "List all customers with failed payments"
- "Which accounts are marked as 'At Risk' in the CRM?"
- "What's the average ticket resolution time?"
- "Which ticket categories have the most volume?"

### Usage & Engagement
- "Which customers have the most logins in the last 7 days?"
- "What features are most commonly used?"
- "How many unique users logged in per company this month?"
- "Which customers have the most diverse feature usage?"
- "Show me login activity trends by company"
- "Which companies have no activity in the last 30 days?"

### Support Analysis
- "How many open tickets do we have by company?"
- "What's the distribution of ticket sentiment?"
- "Which companies submit the most tickets?"
- "What are the most common ticket categories?"
- "Show me tickets created this week"
- "Which channel (chat vs email) has higher volume?"

### Account Management
- "List all accounts owned by sarah@bruin.com"
- "Which industries have the most customers?"
- "Show me all Enterprise tier customers"
- "How many customers do we have in each region?"
- "Which customers have been with us the longest?"

### Cross-Source Analysis
- "Find customers paying for Enterprise but with very few logins"
- "Which high-ARR customers have billing issues AND support tickets?"
- "Show me the correlation between usage frequency and customer sentiment"
- "List customers with renewals soon AND negative signals (angry tickets, failed payments, low usage)"
- "Which account owners have the healthiest book of business?"
- "Find customers with billing issues who also have angry support tickets"

---

## Schema Reference

### companies.csv
| Column | Type | Description |
|--------|------|-------------|
| company_id | string | Unique identifier |
| company_name | string | Company name |
| industry | string | Industry vertical |
| employee_count | int | Company size |
| region | string | Geographic region |
| customer_since | date | First contract date |
| tier | string | Enterprise/Growth/Starter |

### hubspot_crm_deals.csv
| Column | Type | Description |
|--------|------|-------------|
| company_id | string | Unique identifier |
| deal_name | string | Deal name |
| deal_stage | string | Closed Won/At Risk |
| renewal_date | date | Contract renewal date |
| contract_start_date | date | Contract start date |
| arr_value | int | Annual Recurring Revenue ($) |
| plan_tier | string | Enterprise/Growth/Starter |
| owner_email | string | Account owner |

### stripe_billing_history.csv
Raw payment transaction events. Aggregate metrics (MRR, failed payment counts, etc.) should be computed from this data.

| Column | Type | Description |
|--------|------|-------------|
| payment_id | string | Unique payment identifier |
| company_id | string | Company identifier |
| payment_date | date | When payment was attempted |
| amount | int | Payment amount ($) |
| status | string | succeeded/failed |
| payment_method | string | credit_card/invoice/wire_transfer |
| invoice_id | string | Associated invoice |

### intercom_support_data.csv
Raw support ticket events. Aggregate metrics (open ticket counts, sentiment distribution, etc.) should be computed from this data.

| Column | Type | Description |
|--------|------|-------------|
| ticket_id | string | Unique ticket identifier |
| company_id | string | Company identifier |
| user_id | string | User who created ticket |
| created_at | datetime | Ticket creation time |
| resolved_at | datetime | Ticket resolution time (null if open) |
| status | string | open/resolved |
| channel | string | chat/email |
| category | string | billing/bug/feature_request/account/integration/onboarding |
| sentiment | string | Happy/Neutral/Angry |

### segment_usage_data.csv
Raw event-level usage data. Aggregate metrics (logins per period, active users, etc.) should be computed from this data.

| Column | Type | Description |
|--------|------|-------------|
| event_id | string | Unique event identifier |
| company_id | string | Company identifier |
| user_id | string | User identifier |
| event_type | string | login/feature_use |
| event_timestamp | datetime | When the event occurred |
| feature_used | string | Feature accessed (dashboard/reports/integrations/workflows/api_console) |
