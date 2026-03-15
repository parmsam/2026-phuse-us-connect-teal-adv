# PHUSE 2026 US Connect — teal Advance Session (AV09)

**Session:** AV09: Data Visualisation & Open Source Technology Advance Session:
*{teal} as a Catalyst for Cross-Industry Collaboration and Innovation in Clinical Insight Generation*

**Talk:** Shiny for Submission Update — 10-minute presentation / workshop
**Focus:** R Consortium R Submissions Working Group — Pilot 2 & Pilot 4 updates

---

## Authorship & Workflow

These slides are authored and owned by me. Claude is used as a drafting assistant — I review and edit every slide before it's finalised. Content accuracy is maintained by grounding all drafts in raw markdown source files (see below) rather than relying on AI-summarised content.

## Presentation

Slides: [`slides.qmd`](slides.qmd) (Quarto RevealJS)

To render:

```bash
quarto render slides.qmd
```

---

## Reference Sources

> Note: fetched content is stored in `ref-sources/` (gitignored except for [`ref-sources/links.md`](ref-sources/links.md)). Sources were fetched as clean raw markdown via [defuddle.md](https://defuddle.md) — no AI summarisation.

`ref-sources/links.md` is a tracked index of every URL fetched, organised by category. Update it whenever a new source is added.

To repopulate `ref-sources/` yourself, you can use `curl` directly:

```bash
curl -s "https://defuddle.md/r-consortium.org/posts/submissions-wg-2026/" > ref-sources/submissions-wg-2026.md
```

Or if you're using Claude Code with the `/defuddle` skill installed (see `.claude/skills/defuddle/`), you can run:

```
/defuddle https://r-consortium.org/posts/submissions-wg-2026/
```

The skill handles filename inference and saves to `ref-sources/` automatically. Note: defuddle does not work with PDFs — fetch those separately.

| Source | URL |
|--------|-----|
| R Submissions WG 2026 Plans | https://r-consortium.org/posts/submissions-wg-2026/ |
| Pilot 4 Overview | https://rconsortium.github.io/submissions-wg/pilot4.html |
| Pilot 2 Overview | https://rconsortium.github.io/submissions-wg/pilot2 |
| FDA eCTD Expanded R File Formats | https://r-consortium.org/posts/expanded-fda-ectd-file-format-support-for-r-packages/ |
| Swissmedic Presentation | https://r-consortium.org/posts/one-more-step-forward-the-r-consortium-submission-working-group-presentation-to-swissmedic-on-regulator-submission-using-r-and-shiny/ |
| Pilot 3 News | https://r-consortium.org/posts/news-from-r-submissions-working-group-pilot-3/ |
| PharmaSUG 2024 SS-344 | https://www.lexjansen.com/pharmasug/2024/SS/PharmaSUG-2024-SS-344.pdf |

---

## Meeting Minutes (Dec 2025 – Mar 2026)

Fetched from https://rconsortium.github.io/submissions-wg/minutes.html — see `ref-sources/links.md` for full index.

Key findings relevant to this presentation:
- **Dec 2025:** WSL no longer permitted on FDA reviewer computers — effectively blocks Docker on Windows for container submissions
- **Jan 2026:** Pilot 5 resubmitted; Pilot 6 confirmed not a formal FDA submission; Pilot 7 sub-team forming
- **Feb 2026:** Pilot 4 summary report nearing completion; Docker/Windows WSL challenges documented
- **Mar 2026:** Pilot 5 still under review with R version compatibility issues (curl, 4.4.3 vs 4.5.x)

## Key Repositories

- **Pilot 2:** https://github.com/RConsortium/submissions-pilot2
- **Pilot 2 (to FDA):** https://github.com/RConsortium/submissions-pilot2-to-fda
- **Pilot 4 (WebAssembly):** https://github.com/RConsortium/submissions-pilot4-webR
- **Pilot 4 (WebAssembly to FDA):** https://github.com/RConsortium/submissions-pilot4-webR-to-fda
- **Pilot 4 (Container):** https://github.com/RConsortium/submissions-pilot4-container
- **Pilot 4 (Container to FDA):** https://github.com/RConsortium/submissions-pilot4-container-to-fda
- **Submissions WG Site:** https://rconsortium.github.io/submissions-wg
