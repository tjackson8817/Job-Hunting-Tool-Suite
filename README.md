# Beacon — OT Career Target-List Builder

Builds an expanded target-company list for OT cybersecurity consulting/
advisory job searches and networking — from a seed company/website and/or
NAICS codes, using free public data (SEC EDGAR) plus AI-assisted research
(via the Anthropic API with web search enabled) for company discovery and
qualitative enrichment. Exports to `.xlsx`.

## What it does

1. **NAICS expansion** — given a seed company/website/NAICS codes/keywords,
   identifies primary NAICS codes and suggests secondary/tertiary related
   codes (competitors, suppliers, manufacturers served, adjacent service
   providers).
2. **Public-company discovery via SEC EDGAR** — for each relevant NAICS
   code (mapped to SIC), pulls real, verifiable public companies from SEC's
   free EDGAR system.
3. **AI-assisted discovery** — fills remaining slots with private and
   public companies found via Claude's web search, to reach your target
   count.
4. **Enrichment** — for every company, generates the qualitative columns
   (industry fit, OT/ICS relevance, cybersecurity relevance, growth
   signals, outreach strategy, target executive **titles**, LinkedIn search
   keywords) via AI research, and pulls verified SIC/HQ from SEC EDGAR for
   any company matched to a public filer.
5. **Dashboard + `.xlsx` export** — browse any generated list and export it
   to Excel, matching (and extending) the structure of the original
   workbook this tool is based on.

## What this deliberately does NOT do

- **No LinkedIn scraping.** "Target executive" fields are role titles and
  search keywords to use yourself — never scraped named individuals or
  contact URLs. This is a Terms-of-Service line, not a judgment about the
  (completely legitimate) goal of executive networking during a job search.
- **No fabricated precision.** Revenue/employee data is only shown as
  verified when it traces to an SEC filing. Otherwise it's an AI estimate,
  clearly labeled — the same convention your original workbook already used
  for revenue bands and growth signals.
- **No Data Axle integration** — this version uses free sources only. If
  you get Data Axle (or similar) API access later, that can be added as an
  additional, more authoritative data source.

## Setup

1. Push this repo to GitHub (public, for free Pages).
2. Settings → Secrets and variables → Actions → New repository secret:
   `ANTHROPIC_API_KEY` (same key used for other tools like Fenceline).
3. Settings → Actions → General → Workflow permissions → **Read and write**.
4. Settings → Pages → Deploy from branch → `main` → `/(root)`.

## Building a list

1. Repo → **Actions** → **Build Target Company List** → **Run workflow**
2. Fill in what you have — you don't need all fields:
   - **List name** (required) — e.g. "Tom Jackson - OT Cyber Search"
   - **Seed company / website** — your current or most recent employer
   - **Seed NAICS codes** — comma-separated, if you already know them
     (leave blank to let the tool infer them, or to use the default
     OT-cyber-consulting code set if no seed company is given either)
   - **Industry keywords** — free text
   - **Geography** — e.g. "Texas, United States"
   - **Max companies** — keep this modest (default 25); see cost note below
3. Run it. This takes longer than Fenceline or Sightline — expect several
   minutes, since it makes multiple web-search-enabled API calls.
4. Refresh your Pages URL — the new list appears in the dropdown.

## Cost note

This tool costs meaningfully more per run than Fenceline or Sightline,
because each company enrichment call uses Claude's web search tool (which
can perform several searches per call), not just a single text-generation
call. Keep `max_companies` modest (20-30) while you get a feel for actual
cost, especially since you mentioned budget is a real consideration right
now. Each run is manually triggered — nothing runs on a schedule, so cost
only accrues when you actually build a list.

**Quick/free mode**: check the `skip_ai_enrichment` box when running the
workflow to get a free, fast, SEC-EDGAR-only preview — real public
companies with verified HQ/SIC, but no AI research, no private companies,
and every qualitative column left blank ("run full enrichment to populate
this"). Useful for sanity-checking your NAICS codes before spending on a
full run.

## The formatted .xlsx

Each run produces both a `.json` (for the dashboard) and a matching `.xlsx`
in `data/reports/`, generated server-side with openpyxl — bold header row,
green/amber/gray fills for High/Medium/Low relevance and confidence,
frozen header row, and sensible column widths. The dashboard's "Download
formatted .xlsx" button links straight to that file.

There's also a "Quick export" button that builds an `.xlsx` in your browser
instead — unstyled, but it respects any rows you've removed in the
dashboard first (see below). The pre-formatted file is fixed at build time
and doesn't reflect removals.

## Removing companies before export

Every row in the dashboard has a Remove button. This only affects what you
see and what the "Quick export" button includes — it doesn't change the
underlying data file or the pre-formatted `.xlsx`, so you can experiment
freely.

## Adding new columns

The schema is intentionally simple to extend — three coordinated edits, no
rearchitecture:
1. Add the field to the `SYSTEM_ENRICHMENT` schema in
   `scripts/build_target_list.py`, with a one-line instruction on how the
   model should determine it.
2. Add a column to the table in `index.html` (`renderList`) and to the
   `COMPANY_COLUMNS` list in `build_target_list.py` (for the formatted
   `.xlsx`) and the `exportXLSX` mapping (for the quick export).
3. Re-run a list to see it populated.

`currently_hiring_signal` / `currently_hiring_detail` are already built in
as a working example of this pattern — note the schema's comment that
hiring status is a fast-changing fact, better treated as a snapshot than a
stable attribute like HQ location.

## Known limitations

- **SEC EDGAR's SIC-code company search is confirmed non-functional as
  implemented, across 40+ different SIC codes spanning every industry
  tested** — this is no longer a hypothesis. The pipeline does not depend
  on it: AI discovery (via Claude's web search) is the real mechanism.
  "Skip AI enrichment" (quick/free mode) will return nothing until this is
  separately fixed, since that mode relies on EDGAR alone by design — for
  now, don't rely on quick mode.
- **Enrichment now degrades gracefully.** Earlier versions could complete
  a whole run with zero output even when discovery found real, good
  companies, because a failed enrichment batch silently dropped those
  companies. Now: batches are smaller (3 companies instead of 5) with a
  much larger token budget, and if a batch still fails, or the model drops
  a company from its response, that company is kept in the list with a
  clear "enrichment failed, re-run to try again" note rather than
  disappearing. Real research already done is never thrown away.
- The NAICS→SIC crosswalk table in `scripts/build_target_list.py` covers
  only the codes most relevant to OT cyber consulting out of the box;
  other codes fall back to asking Claude for the mapping, which is not as
  authoritative as an official Census/BLS crosswalk file.
- SEC EDGAR only covers public companies. Most of a target list like this
  is realistically going to be private companies, which is where the AI
  research step (not a verified database) has to carry more weight — treat
  those rows as a strong starting point, not verified fact.
- The sample list included (`sample-ot-cyber-consulting-advisory-firms.json`)
  is built from real companies and real facts already present in your
  original workbook, reformatted into this schema — it's not a live pipeline
  run, just a working example so the dashboard shows something immediately.

## Copyright and license

© 2026 Tom Jackson. All rights reserved.

Beacon is part of the Job Hunting Tool Suite. You're welcome to use it
for your own personal job search, and to fork this repo to run your own
copy. Selling it, repackaging it as a paid product or service, or
republishing it as your own work isn't permitted without written
permission. See [LICENSE](LICENSE) for the full terms.
