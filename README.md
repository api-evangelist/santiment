# Santiment

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
