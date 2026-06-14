# Santiment FinOps

This document covers cost management, billing options, and strategies for
optimising API spend when using Santiment's SanAPI and Sanbase products.

## Pricing Tiers at a Glance

| Plan | Monthly Price | Monthly API Calls | Best For |
|---|---|---|---|
| Free | $0 | 1,000 | Evaluation and personal experimentation |
| Sanbase Pro | $49 | 5,000 | Individual researchers and traders |
| Sanbase Max | $249 | 80,000 | Active quant developers |
| Business Pro | Contact sales | 600,000 | Small production pipelines |
| Business Max | Contact sales | 1,200,000 | Large production data products |
| Enterprise | Custom | Custom | Institutional / white-label deployments |

Annual subscriptions receive approximately a 10 % discount over monthly billing.

## Discounts and Token Economics

- **SAN token holders** receive a **20 % discount** on Pro and Max plans.
- **Annual crypto payments** (ETH, DAI, USDC, USDT) unlock the annual
  discount without credit card requirements.
- **SAN token burn**: tokens can be burned to pay for subscriptions at **2×
  market value**, effectively halving the cost for committed ecosystem
  participants.

## Cost-Optimisation Strategies

### Batch Queries
A single GraphQL HTTP request can contain multiple named queries. Each query
still counts as one API call, but batching reduces overhead and lets you
stay within per-minute limits while maximising throughput.

### Use `san.get_many()` for Multi-Asset Requests
The Python SDK's `get_many()` method fetches a metric across many assets in
a single API call instead of one call per asset, dramatically reducing monthly
call consumption.

### AsyncBatch
`san.AsyncBatch` executes queries concurrently without accumulating GraphQL
complexity, allowing high-throughput pipelines to stay within complexity
budgets.

### Cache Results Locally
Historical on-chain and social metrics are largely immutable once the day
closes. Cache daily metrics in a local database (SQLite, Postgres, Parquet)
and only fetch incremental updates to avoid redundant API calls.

### Monitor Rate-Limit Headers
Parse `x-ratelimit-remaining-month` from every response and implement
back-off logic before hitting the ceiling. This prevents surprise HTTP 429
errors that interrupt production pipelines.

### S3 Export for Bulk Historical Backfill
For large historical data loads (multi-year backtests), request direct S3
bucket access from Santiment rather than calling the GraphQL API thousands of
times. Data is delivered as Parquet files at 5-minute and daily granularity.
Contact Santiment sales to arrange bucket credentials.

### Choose the Right Interval
The complexity of a query grows with the number of data points returned
(time range ÷ interval). Using `1d` intervals instead of `1h` for metrics that
do not need intraday resolution reduces both complexity consumption and the
volume of data transferred.

### Self-Reset Monthly Limit
Each account can reset its monthly API call counter once per **90 days** via
`app.santiment.net/account`. Use this sparingly as an emergency lever before
month end rather than a routine workaround.

## Billing References

- [Pricing Page](https://app.santiment.net/pricing)
- [SanAPI Plans](https://academy.santiment.net/products-and-plans/sanapi-plans/)
- [Sanbase Plans](https://academy.santiment.net/products-and-plans/sanbase-plans/)
- [Rate Limits](https://academy.santiment.net/sanapi/rate-limits/)
- [Create API Key](https://academy.santiment.net/products-and-plans/create-an-api-key/)
