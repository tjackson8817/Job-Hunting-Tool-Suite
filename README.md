# Job Hunting Tool Suite — Overview Guide

Four standalone tools that cover a full job search, each solving a distinct stage, designed to work together but each fully independent — any one can be used on its own. A fifth tool, LinkedIn Article Share Builder, sits outside that job-search funnel entirely — it's for staying visible on LinkedIn whether or not you're actively job hunting, and is covered separately near the end of this guide. This guide covers **what each tool does and how they fit together**. For **how to actually use each one** — every field, every toggle, every output option — see that tool's own User Guide or Sale Fish combined guide, linked at the bottom.

---

## The Four Job-Search Tools At a Glance

| Tool | Solves | Core Input |
|---|---|---|
| **Target Company Prompt Builder** | Researches and ranks companies — builds a formatted tracker with a computed Suggested Priority Rank | A company, industry, or NAICS code you already know |
| **Job Posting Finder** | Checks who's actively hiring, right now, with real postings and real URLs | A shortlist of companies and/or job titles |
| **Resume & Cover Letter Tailoring** | Tailors your actual application to a specific posting — gap analysis, bullet rewrites, cover letter or Qualifications Match Letter | A real job posting's text, plus your resume |
| **Outreach Message Builder** | Drafts the messages you send to actually reach someone | Company, contact, and connection-type data from your tracker |

---

## How They Fit Together

There's a natural order to the first two tools, and more flexibility in the last two:

**1. Target Company Prompt Builder → 2. Job Posting Finder** is a fixed sequence. The second tool needs your Suggested Priority Rank to know which companies are worth checking — that data doesn't exist until the first tool has already run. Research and rank first, then check real hiring activity for your top few.

**3. Outreach Message Builder and 4. Resume & Cover Letter Tailoring** don't have one correct order — it depends on your situation:

- **Networking first:** use the Outreach Message Builder to open a warm conversation with a contact before a specific posting is even in play, then tailor your resume once an actual opening exists.
- **Posting first:** find a real opening via the Job Posting Finder, tailor your application immediately with the Resume & Cover Letter Tailoring tool, then use the Outreach Message Builder to follow up with a contact after applying.

Both are legitimate strategies. The tools don't force either order — they're built to be used independently, in whatever sequence matches how you're actually approaching a given company.

---

## What's Consistent Across All Four Tools

A few design decisions were made once and carried through every tool, worth knowing about as a set rather than rediscovering per tool:

- **No install, no account, no server.** Every tool is a single self-contained HTML file. Open it in a browser, or host it via GitHub Pages — nothing is sent anywhere until you copy the generated prompt yourself.
- **Each tool generates a prompt — it doesn't do the work itself.** The web page assembles text; Claude (in a separate chat) does the actual research, writing, or drafting once you paste it in.
- **Every tool has an honesty guardrail suited to what it produces**, not a generic one copy-pasted across all four:
  - Target Company Prompt Builder — won't fabricate company data or figures; marks estimates as estimates.
  - Job Posting Finder — won't fabricate postings; reports fewer results rather than padding the list.
  - Resume & Cover Letter Tailoring — won't fabricate resume content or a recruiter's identity; a named gap is a correct answer, an invented qualification is not.
  - Outreach Message Builder — won't fabricate a relationship or shared history that doesn't exist.
- **"Your background" is a shared, reusable field** — paste it once per tool, and it sharpens Suggested Job Title Keywords, Warm Introduction Path, cover letters, and outreach messages consistently, rather than each tool asking for a differently-shaped version of the same information.
- **Claude Settings requirements vary by tool, and each guide states them plainly up front** rather than assuming — see the quick-reference table below.

---

## Quick Reference: Claude Settings Needed

| Tool | Web Search | Code Execution & File Creation |
|---|---|---|
| Target Company Prompt Builder | Required — the entire tool depends on live research | Required for the `.xlsx` tracker output |
| Job Posting Finder | Required — the entire tool depends on live search for real postings | Only if you choose the Excel output format |
| Resume & Cover Letter Tailoring | Only if recruiter identification is turned on (default: on) | Only if you choose the Word document output format |
| Outreach Message Builder | Not required — drafts from research you already provide | Only if you choose the Word document output format |

If a tool ever responds with an explanation of a missing capability instead of your actual output, this table is usually why — check the relevant toggle and re-run.

---

## Where to Find the Details

| Tool | Standalone Guide | Sale Fish Combined Guide (cover page + "About This Tool" + full guide) |
|---|---|---|
| Target Company Prompt Builder | `Prompt_Builder_User_Guide.md` / `.docx` | `Sale_Fish_Prompt_Builder_Combined_Guide.docx` |
| Job Posting Finder | `Job_Posting_Finder_User_Guide.md` / `.docx` | `Sale_Fish_Job_Posting_Finder_Combined_Guide.docx` |
| Resume & Cover Letter Tailoring | `Resume_Cover_Letter_Tailoring_User_Guide.md` / `.docx` | `Sale_Fish_Resume_Cover_Letter_Tailoring_Combined_Guide.docx` |
| Outreach Message Builder | `Outreach_Message_Builder_User_Guide.md` / `.docx` | `Sale_Fish_Outreach_Message_Builder_Combined_Guide.docx` |
| LinkedIn Article Share Builder | `LinkedIn_Article_Share_User_Guide.md` / `.docx` | `Sale_Fish_LinkedIn_Article_Share_Combined_Guide.docx` |

Each tool's own guide is the authoritative source for its specific fields, toggles, and output formats — this overview intentionally stays at the "what and why" level so it doesn't drift out of sync as individual tools evolve.

---

## A Fifth Tool, Outside the Funnel: LinkedIn Article Share Builder

Everything above is a linear (or semi-linear) job-search funnel. This fifth tool isn't part of that funnel at all — it's for staying visible on LinkedIn consistently, whether or not you're actively job hunting. It finds real, recent, on-brand articles worth sharing, presents the top 3 with reasoning for each, and drafts the actual post (personal hook, summary, hashtags) plus optional matching artwork for whichever one you pick.

It shares the same design discipline as the other four — an honesty guardrail suited to what it produces (only real, verifiable articles with real URLs; no padding the list if genuinely on-brand options are thin that day), and it reuses the "set once, reuse every time" pattern for your name and tagline rather than asking you to retype your brand identity for every post.

One thing worth knowing if you ever consider automating it: running it manually through a Claude chat is free, same as every other tool in this suite. A fully automated "generate one every morning without me" version is possible but requires the Anthropic API directly and small ongoing costs — a genuinely different (and separate) consideration from the free, manual tool described here.
