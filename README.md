# Helium News Bias Explorer

An interactive single-page explorer for the [Helium MCP](https://heliumtrades.com/mcp-page/) server's structured news-bias corpus — **216 sources scored on 37 dimensions**, fetched live from the public REST endpoint on every page load.

**Live**: [connerlambden.github.io/helium-news-explorer](https://connerlambden.github.io/helium-news-explorer/)

## What it does

- Pulls the full bias corpus on load via one CORS-open HTTPS GET
- Ranks sources by any of 37 dimensions in a bar chart
- Scatter-plots any two dimensions against each other with a live Pearson correlation
- Click any source to see its full 37-dimension profile in a popup card
- Share view URLs (state is encoded in query params)

No build step. No dependencies. Single `index.html` file. ~10 KB minified.

## Why it exists

The Helium MCP server exposes structured bias scores on a free anonymous GET, which makes it ideal teaching substrate for media-literacy classes, journalism methodology courses, and researchers studying news-ecosystem patterns. This explorer is a zero-friction way to play with the corpus — no Python, no signup, no API key, no tracking.

## Local dev

```bash
git clone https://github.com/connerlambden/helium-news-explorer
cd helium-news-explorer
python3 -m http.server 8000
open http://localhost:8000
```

That's it. The page makes one cross-origin GET to `heliumtrades.com/mcp_all_source_biases/` and renders client-side.

## Related

- [helium-mcp-cookbook](https://github.com/connerlambden/helium-mcp-cookbook) — seven runnable Python recipes for the same REST surface
- [helium-mcp](https://github.com/connerlambden/helium-mcp) — the MCP server itself
- [Fear-coding finding writeup](https://dev.to/connerlambden/fear-coding-in-160-news-sources-correlates-085-with-political-extremism-and-only-008-with-45n2) — the empirical analysis that motivated this explorer

## License

MIT. Recipes and source are educational and may be adapted freely.
