# Santiment API Rate Limits

Santiment enforces rate limits at three time horizons — per minute, per hour,
and per month — all measured in UTC. Limits are applied **per account**; all
API keys belonging to the same account share the same quota.

## How API Calls Are Counted

Each GraphQL **query** counts as one API call. A single HTTP request can
contain multiple named queries; each query increments the counter
independently. For example, a batch request containing two `getMetric` calls
counts as 2 API calls.

## Limits by Plan

| Plan | Per Minute | Per Hour | Per Month |
|---|---|---|---|
| Free | 100 | 500 | 1,000 |
| Sanbase Pro | 100 | 1,000 | 5,000 |
| Sanbase Max | 100 | 4,000 | 80,000 |
| Business Pro | 600 | 30,000 | 600,000 |
| Business Max | 1,200 | 60,000 | 1,200,000 |
| Enterprise | Custom | Custom | Custom |

## Response Headers

Every API response includes headers that expose the current rate-limit state:

| Header | Description |
|---|---|
| `x-ratelimit-limit-minute` | Maximum calls allowed per minute |
| `x-ratelimit-limit-hour` | Maximum calls allowed per hour |
| `x-ratelimit-limit-month` | Maximum calls allowed per month |
| `x-ratelimit-remaining-minute` | Calls remaining in the current minute |
| `x-ratelimit-remaining-hour` | Calls remaining in the current hour |
| `x-ratelimit-remaining-month` | Calls remaining in the current month |
| `x-ratelimit-reset` | Seconds until the next rate-limit window resets |

## When a Limit Is Exceeded

- The API returns **HTTP 429** with an error payload describing which limit was
  hit and when it will reset.
- Limits reset at `00:00:00 UTC` at the start of the next minute, hour, or
  month respectively.
- Each account can self-reset its monthly limit once per **90 days** via the
  Account page at `app.santiment.net/account`.
- Persistent limit issues or plans beyond Business Max require contacting
  Santiment support.

## Query Complexity

In addition to call-count rate limits, SanAPI enforces a **complexity** ceiling
per query. Complexity is a function of the number of data points requested
(time range ÷ interval × metric count). Queries that exceed the complexity
budget are rejected before execution. Details are documented on the
[Complexity Page](https://academy.santiment.net/sanapi/complexity/).

## Checking Remaining Limits (Python)

With the `sanpy` SDK you can inspect your remaining quota programmatically:

```python
import san
san.ApiConfig.api_key = "YOUR_API_KEY"

# Returns dict with remaining calls per window
limits = san.rate_limits()
print(limits)
```

## References

- [Rate Limits Documentation](https://academy.santiment.net/sanapi/rate-limits/)
- [Complexity Page](https://academy.santiment.net/sanapi/complexity/)
- [SanAPI Plans](https://academy.santiment.net/products-and-plans/sanapi-plans/)
