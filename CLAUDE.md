# PHUSE 2026 US Connect — teal Advance Session (AV09)

## Project Overview

10-minute presentation/workshop on **Shiny for Submission** updates, focused on R Consortium R Submissions Working Group Pilots 2 and 4. Delivered at PHUSE US Connect 2026, Session AV09: {teal} as a Catalyst for Cross-Industry Collaboration.

**Main output:** `slides.qmd` — Quarto RevealJS presentation

## Role of Claude

Claude is a **drafting assistant** only. The presenter authors, reviews, and edits every slide. Do not present drafts as final — flag uncertainty, suggest options, and defer to the presenter's judgement on content and framing.

Context is managed deliberately: all factual content must be grounded in the raw markdown files in `ref-sources/`, not recalled from training data or AI-summarised sources. If a fact isn't in the ref-sources, say so.

## Reference Sources

All reference material lives in `ref-sources/` (gitignored). Sources are fetched as **raw verbatim markdown** using [defuddle.md](https://defuddle.md) — prepend `https://defuddle.md/` to any URL to get clean markdown, then save with `curl`:

```bash
curl -s "https://defuddle.md/example.com/some-page/" > ref-sources/some-page.md
```

Do not use WebFetch to populate ref-sources — it summarizes content through an AI model and loses detail. When adding a new source, also update `ref-sources/links.md` with the URL, filename, and category — this file is gitignored except for `links.md`.

## Key Facts (from sources)

- **Pilot 2 (~2022 H1):** First Shiny app submitted via FDA eCTD portal. Shiny code packaged as proprietary R package via `{pkglite}`. FDA deployed on their own infrastructure.
- **Pilot 4 WebAssembly (Sept 20, 2024):** First publicly available WebAssembly submission received by FDA CDER. Runs in Microsoft Edge, no R installation required. Lead: Eric Nantz (Eli Lilly).
- **Pilot 4 Containers (Summer 2025):** Docker-based (early Appsilon experimental work used Podman; canonical RConsortium repo uses Docker). Tested across ~15 FDA computing environments. Critical finding (Dec 2025): WSL is no longer permitted on FDA reviewer computers due to a security policy update — Docker on Windows requires WSL, effectively blocking Docker-based submissions at FDA. Formal summary report nearing completion as of Feb 2026.
- **FDA preference:** WebAssembly over containers — contrary to the team's expectation.
- **FDA eCTD format expansion (Aug 2025):** Now accepts `.zip`, `.rds`, `.rdb`, `.rdx`, `.rda`, `.md`, `.rd`, `.html`. `{pkglite}` remains valid — `.zip` is an added option, not a replacement (Dec 2025 correction in source).
- **Pilot 5 (ongoing):** Resubmitted Jan 2026. Under FDA review as of Mar 2026 — R version compatibility issues (curl library, 4.4.3 vs 4.5.x).
- **Pilot 6:** Kicked off Jan 2026. Will NOT be submitted to FDA — AI-assisted programming (GitHub Copilot, KG AI, Conviva), Friday meetings 10am ET.
- **Pilot 7:** Kicked off Jan 2026. Simulated realistic CDISC data; OpenClinica synthetic data obtained, sub-team forming.

## Slide Accuracy Rules

- Do not imply `{pkglite}` is deprecated — it is a peer-reviewed approach that remains valid.
- WebAssembly requires some libraries to compile/launch; say "no R installation required" not "no dependencies."
- Pilot 4 formal report is not yet published — note as "nearing completion."
- Pilot 6 won't be submitted to FDA.

## Rendering

```bash
quarto render slides.qmd
```
