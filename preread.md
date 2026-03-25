# Pre-Read: Shiny for Submission
## PHUSE US Connect 2026 · Session AV09 · 10-Minute Talk

**Presenter:** Sam Parmar, Statistical Data Scientist, Pfizer  
**Session:** AV09 — {teal} as a Catalyst for Cross-Industry Collaboration  
**Date:** Wednesday, March 25, 2026, 1:30–3:30 PM

---

## What This Talk Is About

This talk covers updates from the [R Consortium R Submissions Working Group](https://rconsortium.github.io/submissions-wg), focusing on Pilots 2 and 4 — the two pilots most directly relevant to Shiny-based submissions. The goal is to bring the `{teal}` community up to speed on what has been proven possible with the FDA, and what practical constraints still exist.

---

## Background: The R Submissions Working Group

The R Consortium R Submissions Working Group runs a series of public pilots demonstrating that R is viable for FDA regulatory submissions. All submission packages and code are publicly available on [GitHub](https://github.com/RConsortium).

| Pilot | Focus | Status |
|-------|-------|--------|
| 1 | TLFs via `{pkglite}` | ✅ FDA accepted |
| 2 | Shiny app submission | ✅ FDA accepted Dec 2022 |
| 3 | ADaM datasets in R | ✅ FDA accepted Aug 2024 |
| 4 | WebAssembly + Containers | ✅ Submitted 2024–2025 |
| 5 | Dataset-JSON | 🔄 Resubmitted Jan 2026, under FDA review |
| 6 | Expanded ADaMs + AI/automation | 🔄 Kicked off Jan 2026 (not a formal FDA submission) |
| 7 | Simulated realistic CDISC data | 🔄 Kicked off Jan 2026, sub-team forming |

---

## Pilot 2: The First Shiny App to FDA

> **Source:** [`ref-sources/pilot2.md`](https://rconsortium.github.io/submissions-wg/pilot2.html)

**Goal:** Demonstrate a Shiny app can be submitted through the current FDA eCTD e-submission process and reviewed by FDA staff.

**What was submitted:**
- A Shiny app displaying the 4 TLFs from Pilot 1 with basic dataset filtering
- Shiny code packaged as a **R package** using `{pkglite}` and `{golem}`- Submitted via the eCTD portal (~2022 H1); **accepted by FDA December 2022**

**What FDA had to do:**
- Deploy the Shiny app on FDA infrastructure (laptop/server)
- Reproduce analysis results
- Requested removal of p-values from filtered tables (p-hacking risk)

**Team:** Ning Leng, Heng Wang (Roche) · Mike Stakehouse, Eli Miller (Atorus) · Yilong Zhang, Gregery Chen (Merck) · Eric Nantz (Eli Lilly)  
**FDA reviewers:** Paul Schuette · Hye Soo Cho

To our knowledge (per Posit, Feb 2023), this was the first publicly available submission package that includes a Shiny component — and the first Shiny app submitted and accepted through the FDA eCTD gateway.

**Key limitation exposed:** FDA reviewers had to set up an R environment, install all dependencies, and run a Shiny server themselves. This is the friction Pilot 4 was designed to solve.

---

## Pilot 4: Shipping the Execution Environment

> **Source:** [`ref-sources/pilot4.md`](https://rconsortium.github.io/submissions-wg/pilot4.html)

**Goal:** Utilize alternative methods of distributing a self-contained submission bundle of the Pilot 2 Shiny application with container and web-assembly technologies.

Pilot 4 explored two parallel approaches:

### Track 1 — WebAssembly

- R compiled to WebAssembly via `{webR}`; embedded web server via `{httpuv}`
- Pilot 2 Shiny app adapted with small modifications to fit webR constraints
- **Submission milestone:** WebAssembly package reached FDA CDER on **September 20, 2024** — to our knowledge, the first publicly available WebAssembly submission received by FDA CDER
- FDA reviewer experience: extract bundle → run setup code → open app in Microsoft Edge. No R installation required.

> **Source:** [`ref-sources/minutes-2025-12-05.md`](https://rconsortium.github.io/submissions-wg/minutes/2025-12-05/index.html): "The WebAssembly application performed well overall across the environments"

**Repo:** [submissions-pilot4-webR](https://github.com/RConsortium/submissions-pilot4-webR)  
**Lead:** Eric Nantz (Eli Lilly)

### Track 2 — Containers (Docker)

- Full Linux environment bundled with R and all package dependencies
- Submitted Summer 2025; tested across approximately 15 FDA computing environments
- Note: early experimental work by Appsilon used Podman; the canonical RConsortium repo uses Docker

> **Source:** [`ref-sources/minutes-2025-12-05.md`](https://rconsortium.github.io/submissions-wg/minutes/2025-12-05/index.html): "A handful of random issues occurred in the Docker container version which were able to be resolved, and do not seem to be caused by any of the Pilot 4 container instructions / code. The Pilot 4 Container Learning Guide was a great resource to help solve those issues."

**Critical finding (Dec 2025):**

> **Source:** [`ref-sources/minutes-2025-12-05.md`](https://rconsortium.github.io/submissions-wg/minutes/2025-12-05/index.html): "Due to recent security policy updates, the Windows Subsystem for Linux (WSL) utility is no longer permitted for installation on FDA reviewer computers. The WSL utility is a key dependency of running Docker on a Windows host, due to the Docker runtime requiring a Linux-compatible environment."

WSL is a hard dependency of Docker on Windows. Without it, Docker-based submissions cannot be run on a typical FDA reviewer's machine. This finding emerged from the Dec 2025 working group meeting, informed by testing across ~15 FDA environments. Security concerns about malicious packages in open-source ecosystems (e.g., the soopsocks PyPI incident) contributed to the policy tightening.

**The unexpected result:** FDA reviewers preferred WebAssembly over containers — contrary to the team's expectation. WebAssembly only required a browser; no WSL, no IT approval, no firewall issues.

> **Source:** [`ref-sources/pilot4.md`](https://rconsortium.github.io/submissions-wg/pilot4.html): "In light of these factors, the use of containers in future submissions will prove to be difficult as container runtimes such as Docker will be much more difficult to set up on a typical FDA reviewer's working machine."

The formal Pilot 4 summary report was nearing completion as of the Feb 2026 working group meeting.

**Repos:** [submissions-pilot4-container](https://github.com/RConsortium/submissions-pilot4-container) · [submissions-pilot4-container-to-fda](https://github.com/RConsortium/submissions-pilot4-container-to-fda)

---

## FDA eCTD File Format Expansion (Aug 2025)

> **Source:** [`ref-sources/fda-ectd-expanded-formats.md`](https://r-consortium.org/posts/expanded-fda-ectd-file-format-support-for-r-packages/)

The August 2025 revision of the FDA eCTD Technical Conformance Guide (effective 2025-08-20) expanded accepted file formats for R workflows:

- **New M&S types:** `.rds`, `.rdb`, `.rdx`, `.rdata`/`.rda`, `.md`, `.rd`
- **Expanded:** `.zip` and `.html` (for delivering full R packages)

Sponsors can now submit non-public R packages directly as a `.zip` file — reducing friction compared to previous workarounds.

**Important:** `{pkglite}` is **not deprecated**. As the R Consortium clarified in a Dec 2025 correction to this post: it "remains a principled, peer-reviewed approach that continues to serve the community well." The `.zip` option is an addition, not a replacement. `{pkglite}`'s advantages — human-readable, transparent, easy version control, language-agnostic — remain valuable.

---

## What's Still Active

### Pilot 5 — Dataset-JSON

> **Sources:** [`ref-sources/minutes-2025-12-05.md`](https://rconsortium.github.io/submissions-wg/minutes/2025-12-05/index.html), [`ref-sources/minutes-2026-03-06.md`](https://rconsortium.github.io/submissions-wg/minutes/2026-03-06/index.html)

Resubmitted January 2026. As of March 2026, under active FDA review with R version compatibility issues — specifically around the `curl` library when compiling packages from source across R 4.4.3 vs 4.5.x environments.

### Pilot 6 — AI-Assisted Programming

> **Source:** [`ref-sources/minutes-2026-01-09.md`](https://rconsortium.github.io/submissions-wg/minutes/2026-01-09/index.html)

Kicked off January 2026. Uses GitHub Copilot, KG AI, and Conviva to build out expanded ADaMs and displays. **This is NOT a formal FDA submission** — it is an exploratory effort. Meetings on Zoom, Fridays 10 AM ET, open to all.

### Pilot 7 — Realistic Submission Data

> **Source:** [`ref-sources/minutes-2026-01-09.md`](https://rconsortium.github.io/submissions-wg/minutes/2026-01-09/index.html)

Kicked off January 2026. Yilong Zhang (Meta) obtained synthetic EDC data from OpenClinica with no identifying information. Sub-team forming with dedicated meeting cadence.

---

## Implications for {teal}

Pilots 2 and 4 establish that Shiny apps — and by extension `{teal}`-based apps — can be submitted to regulators. Key practical considerations:

- **Packaging:** Use `{pkglite}` or `.zip` to submit proprietary R packages
- **Dependencies:** Prefer CRAN-hosted packages — FDA reviewers favour known, vetted dependencies
- **Documentation:** ADRG must document all dependencies in more detail than a SAS submission requires
- **Infrastructure:** Design for deployment on a reviewer's Windows machine
- **Filtering UX:** Avoid displaying inferred statistics (e.g., p-values) on dynamically filtered subsets — FDA raised this explicitly in Pilot 2 review
- **WebAssembly:** `{golem}` was incompatible with webR — framework choices matter if targeting Pilot 4-style delivery
- **Containers:** Docker is effectively blocked at FDA for now due to the WSL policy; monitor for changes

---

## Open Discussion Questions (Workshop)

1. How do we handle `{teal}` module dependency validation in an FDA submission context?
2. WebAssembly for `{teal}` — what's feasible today given webR constraints?
3. Could Nix/Rix offer a lighter-weight alternative to containers for reproducible environments?

---

## Key Links

| Resource | URL |
|----------|-----|
| R Submissions WG Website | https://rconsortium.github.io/submissions-wg |
| Pilot 2 overview | https://rconsortium.github.io/submissions-wg/pilot2.html |
| Pilot 2 repo | https://github.com/RConsortium/submissions-pilot2 |
| Pilot 4 overview | https://rconsortium.github.io/submissions-wg/pilot4.html |
| Pilot 4 WebAssembly repo | https://github.com/RConsortium/submissions-pilot4-webR |
| Pilot 4 WebAssembly live demo | https://submissions-pilot4-webr.netlify.app/ |
| Pilot 4 Container repo | https://github.com/RConsortium/submissions-pilot4-container |
| FDA eCTD format expansion | https://r-consortium.org/posts/expanded-fda-ectd-file-format-support-for-r-packages/ |
| 2026 WG Update | https://r-consortium.org/posts/submissions-wg-2026/ |
| Appsilon: R in FDA Submissions | https://www.appsilon.com/post/r-in-fda-submissions |
| Eric Nantz NESS 2025 talk | https://rpodcast.github.io/opensub-ness2025/ |
| PharmaSUG 2024 SS-344 | https://www.lexjansen.com/pharmasug/2024/SS/PharmaSUG-2024-SS-344.pdf |
| Join the WG | director@r-consortium.org |

---

*Pre-read for PHUSE US Connect 2026, Session AV09. All facts grounded in raw source materials from `ref-sources/`. For the slides, see [`slides.qmd`](slides.qmd).*
