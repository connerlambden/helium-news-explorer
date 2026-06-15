# Helium Trades — Interactive Explorers

Two zero-dependency single-page apps for the [Helium MCP](https://heliumtrades.com/mcp-page/) / REST API. No signup, no key, no tracking. Each page makes one CORS-open HTTPS GET and renders client-side.

## Live

| Page | What it does |
|------|--------------|
| **[News Bias Explorer](https://connerlambden.github.io/helium-news-explorer/)** | 216 news sources × 37 bias dimensions. Ranked bars, scatter plots, live Pearson correlations, per-source detail cards. |
| **[Ticker Forecast Dashboard](https://connerlambden.github.io/helium-news-explorer/tickers.html)** | Top 10 short-vol + long-vol candidates with ML 37-day forecasts, uncertainty cones, and bullish/bearish narratives. |

## What's here

- `index.html` — News Bias Explorer (live API + `corpus.json` fallback)
- `corpus.json` — bundled bias snapshot (~212 sources) for offline / quota-exhausted loads
- `tickers.html` — Ticker Forecast Dashboard (calls `heliumtrades.com/mcp_top_strategies/`)
- Pure HTML + CSS + vanilla JS. No build step. No frameworks. No analytics.

## Why these exist

The Helium MCP server exposes a handful of free, anonymous, CORS-open JSON endpoints. That makes the data ideal substrate for teaching, journalism methodology, quant research, and quick prototyping — anyone with a browser can poke at it. These two explorers are the lowest-friction way to do that. No Python, no signup, no API key.

## News Bias Explorer (`index.html`)

- Tries the live API on load; falls back to bundled `corpus.json` if the free per-IP quota is exhausted
- Rank sources by any of 37 dimensions in a bar chart
- Scatter-plot any two dimensions against each other with live Pearson r
- Click any source for its full 37-dimension profile
- Shareable view URLs via query params

## Ticker Forecast Dashboard (`tickers.html`)

- One call to `mcp_top_strategies/` returns 10 tickers (5 short-vol + 5 long-vol)
- Each card: ticker badge, current price, forecast %, uncertainty cone (SVG), bull case, bear case
- The forecast and the narrative come from the same underlying model — they always agree on the same view of the world
- Links to the full Helium analysis page for each ticker
- Educational only — not investment advice. Track calibration with the [Brier-grade recipe](https://github.com/connerlambden/helium-mcp-cookbook/blob/main/recipes/02_options_calibration_tracker.py).

## Local dev

```bash
git clone https://github.com/connerlambden/helium-news-explorer
cd helium-news-explorer
python3 -m http.server 8000
open http://localhost:8000               # bias explorer
open http://localhost:8000/tickers.html  # forecast dashboard
```

That's it.

## Related

- [helium-mcp-cookbook](https://github.com/connerlambden/helium-mcp-cookbook) — seven runnable Python recipes for the same REST surface
- [helium-mcp](https://github.com/connerlambden/helium-mcp) — the MCP server itself
- [Fear-coding finding writeup](https://dev.to/connerlambden/fear-coding-in-160-news-sources-correlates-085-with-political-extremism-and-only-008-with-45n2) — the empirical analysis the bias explorer was built around
- [Brier-grade your forecasts](https://dev.to/connerlambden/how-to-brier-grade-your-own-ml-option-pricing-forecasts-in-40-lines-of-python-1eii) — the calibration recipe that justifies trusting (or distrusting) the ticker dashboard's numbers

## API quota note

The Helium REST endpoints enforce a daily per-IP quota for unauthenticated calls. Each explorer makes exactly one GET per page load, so a casual visitor will never hit the limit. If a page shows an HTTP 402 error, your IP has temporarily exhausted its free quota — reload tomorrow or [grab a key](https://heliumtrades.com/mcp-page/).

## License

MIT. Both pages and all assets are educational and may be adapted freely. The Helium data itself remains the property of Helium Trades.
