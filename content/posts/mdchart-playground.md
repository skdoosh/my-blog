---
title: "mdchart: Markdown Charts, End-to-End"
date: 2026-03-09T12:00:00+05:30
draft: false
tags: ["hugo", "mdchart", "charts", "fastapi", "matplotlib"]
description: "A showcase of mdchart: DSL parser, chart rendering engine, API deployment, and live Hugo playground"
---

I built **mdchart** to turn a tiny chart DSL into real matplotlib charts, with a clean API and a blog-embedded playground.

Instead of pasting static images, I can now describe a chart in a few lines and render it on demand.

{{< mdchart-playground />}}

## What this project includes

- A DSL parser for fenced chart blocks (`type`, `x`, `y`, `data`)
- A rendering engine that generates PNG charts with matplotlib
- A FastAPI backend (`/v1/render-dsl`, `/v1/render-markdown`)
- A Hugo shortcode playground that calls the live API from this post

## Why this matters

- Markdown stays source-of-truth for chart intent
- Charts are reproducible from text, not manually exported files
- The same engine powers CLI, API, and website experience

## Architecture snapshot

1. DSL text is validated and parsed into a typed chart spec.
2. Renderer converts spec into PNG bytes.
3. API returns chart metadata and base64 image payload.
4. Hugo shortcode UI renders the returned image instantly.

## Current deployment

- Backend: Render free tier (`https://mdchart.onrender.com`)
- Blog: Hugo + PaperMod, with a reusable `mdchart-playground` shortcode

## What’s next

- Add more chart types (scatter, area, stacked bar)
- Add style/theme options in DSL
- Persist/share chart snippets via short links
