# SaaS Pipeline

## How to Query Data

**Use Bruin MCP tools to query data.** Do NOT write Python scripts or functions to fetch data. Bruin MCP provides direct database access - use it.

## CRITICAL: Dataset Prefix Required

**Dataset:** `saas`
**Project:** `bruin-demo-data`

**ALWAYS prefix table names with `saas.` in ALL queries.**

```sql
-- CORRECT
SELECT * FROM saas.companies;

-- WRONG (will fail)
SELECT * FROM companies;
```

## Available Tables

- `saas.companies` - Company/account master data
- `saas.hubspot_crm_deals` - Sales deals and renewals from HubSpot
- `saas.stripe_billing_history` - Payment transactions from Stripe
- `saas.segment_usage_data` - Product usage events from Segment
- `saas.intercom_support_data` - Support tickets from Intercom

Table schemas are defined in `assets/*.asset.yml` files.

## Key Relationships

- `company_id` links all tables (B2B account-level data, not user-level)
