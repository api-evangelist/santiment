# Santiment

Santiment is a crypto market intelligence platform providing on-chain metrics,
social sentiment data, developer activity tracking, and blockchain analytics
signals via a GraphQL API (SanAPI). The platform covers 2,800+ crypto assets
across 14 blockchain networks and exposes more than 1,000 metrics including
daily active addresses, MVRV ratio, social volume, Twitter followers, trending
words, developer commit activity, and labelled address intelligence (75+ million
Ethereum addresses, 65+ million Bitcoin addresses).

## Products

| Product | URL | Description |
|---|---|---|
| **Sanbase** | https://app.santiment.net | Web analytics dashboard |
| **SanAPI** | https://api.santiment.net | GraphQL data API for developers |
| **Sansheets** | https://sheets.santiment.net | Google Sheets plugin |
| **Insights** | https://insights.santiment.net | Research and market reports |
| **SanR** | https://sanr.app | Blockchain-based price prediction |

## API Quick Start

SanAPI uses GraphQL. The interactive explorer is at
`https://api.santiment.net/graphiql`.

### Authentication

Generate an API key from your account settings at
`https://app.santiment.net/account` and pass it as a Bearer token:

```bash
curl -X POST https://api.santiment.net/graphql \
  -H "Authorization: Apikey YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"query": "{ currentUser { id email } }"}'
```

### Python SDK

```bash
pip install sanpy
```

```python
import san
san.ApiConfig.api_key = "YOUR_API_KEY"

# Fetch daily active addresses for Bitcoin over the last 30 days
df = san.get(
    "daily_active_addresses/bitcoin",
    from_date="2026-05-01",
    to_date="2026-06-01",
    interval="1d"
)
print(df)
```

## Data Categories

- **On-Chain**: daily active addresses, MVRV ratio, exchange flows, NVT ratio
- **Social**: social volume, social dominance, Twitter followers, sentiment scores
- **Developer**: commit activity, GitHub contributors, code changes
- **Market**: price, volume, market cap (multiple data sources)
- **Trending**: trending words/stories with bullish/bearish sentiment ratios
- **Address Intelligence**: labeled exchange/whale/DeFi addresses

## Rate Limits

| Plan | Per Minute | Per Hour | Per Month |
|---|---|---|---|
| Free | 100 | 500 | 1,000 |
| Pro | 100 | 1,000 | 5,000 |
| Max | 100 | 4,000 | 80,000 |
| Business Pro | 600 | 30,000 | 600,000 |
| Business Max | 1,200 | 60,000 | 1,200,000 |

See [rate-limits/README.md](rate-limits/README.md) for details.

## Plans and Pricing

See [plans/README.md](plans/README.md) for full plan comparison.

## FinOps

See [finops/README.md](finops/README.md) for cost-optimisation strategies.

## Links

- [Developer Documentation](https://academy.santiment.net/for-developers/)
- [API Reference](https://academy.santiment.net/sanapi/)
- [GraphiQL Explorer](https://api.santiment.net/graphiql)
- [Available Metrics](https://api.santiment.net/available_metrics)
- [Python SDK (sanpy)](https://github.com/santiment/sanpy)
- [Pricing](https://app.santiment.net/pricing)
- [Terms of Service](https://santiment.net/terms/)
- [Privacy Policy](https://santiment.net/privacy/)
