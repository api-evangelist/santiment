# Santiment GraphQL API

Santiment exposes its full platform through a single GraphQL endpoint at `https://api.santiment.net/graphql`. The API provides programmatic access to on-chain metrics, social sentiment data, developer activity, price history, and blockchain analytics for more than 2,800 crypto assets across 14 blockchain networks. The schema defines 179 query fields spanning asset discovery (`allProjects`, `project`, `projectBySlug`), timeseries metrics (`getMetric`, `historyPrice`, `ohlc`), social analytics (`getTrendingWords`, `wordsSocialVolume`, `socialDominanceTrendingWords`), blockchain address intelligence (`blockchainAddress`, `historicalBalance`, `topHolders`), NFT trades, and platform-level resources such as dashboards, watchlists, chart configurations, and user alerts.

Authentication uses an API key passed as a Bearer token in the `Authorization` header. Rate limits are enforced per minute, per hour, and per month; the allowed call volume and depth of historical data depend on the subscriber's plan. Unauthenticated requests receive a limited free tier. The schema also exposes 136 mutation fields for managing user-owned resources (watchlists, alerts/triggers, dashboards, chart configurations, comments, and account settings) and custom SQL queries against Santiment's ClickHouse warehouse.

The schema is large — 346 custom types (240 objects, 50 enums, 39 input objects, 16 scalars, and 1 union) — reflecting the breadth of Santiment's analytics surface. Key object families include `Project`, `Metric`, `ChartConfiguration`, `Dashboard`, `Insight`, `UserTrigger`, `Watchlist`, `BlockchainAddress`, `NftTrade`, `Comment`, and paginated variants of most list types. The interactive GraphiQL explorer at `https://api.santiment.net/graphiql` allows browsing and executing queries without a separate client.

**Endpoint:** https://api.santiment.net/graphql

**Documentation:** https://academy.santiment.net/for-developers/

**References:**

- Documentation: https://academy.santiment.net/for-developers/
- GettingStarted: https://academy.santiment.net/sanapi/common-queries/
- Reference: https://api.santiment.net/graphiql
- Authentication: https://academy.santiment.net/products-and-plans/create-an-api-key/
- RateLimits: https://academy.santiment.net/sanapi/rate-limits/
