# Job Hunting Tool Suite — Overview Guide

Six standalone tools cover a full job search, each solving a distinct stage, designed to work together but each fully independent — any one can be used on its own. Two additional tools sit outside that job-search funnel entirely: **LinkedIn Article Share Builder**, for staying visible on LinkedIn and building an actual thought-leadership position whether or not you're actively job hunting, and **Recruiter Message & Job Posting Sanity Check**, for screening suspicious recruiter outreach or job listings — both covered separately near the end of this guide. This guide covers **what each tool does and how they fit together**. For **how to actually use each one** — every field, every toggle, every output option — see that tool's own User Guide or Sale Fish combined guide, linked at the bottom.

---

## The Six Job-Search Tools At a Glance

| Tool | Solves | Core Input | Output |
|---|---|---|---|
| **Target Company Prompt Builder** (Step 1, Research) | Researches and ranks companies — builds a formatted tracker with a computed Suggested Priority Rank | A company, industry, or NAICS code you already know | Prompt(s) — paste into a new Claude chat to generate the `.xlsx` tracker |
| **Job Posting Finder** (Step 2, Verify) | Checks who's actively hiring, right now, with real postings and real URLs | A shortlist of companies and/or job titles | Prompt text — paste into a new Claude chat to generate the postings list |
| **Resume & Cover Letter Tailoring** (Step 3a, Apply/Connect) | Tailors your actual application to a specific posting — gap analysis, bullet rewrites, cover letter or Qualifications Match Letter | A real job posting's text, plus your resume | Prompt text — paste into a new Claude chat to generate the tailored documents |
| **Outreach Message Builder** (Step 3b, Apply/Connect) | Drafts the messages you send to actually reach someone, tailored per company and per stage of the relationship | Company, contact, and connection-type data from your tracker | Prompt text — paste into a new Claude chat to generate the draft messages |
| **Interview Prep Guide Builder** (Step 4, Interview) | Builds a real, grounded prep guide once an interview lands — three modes for a recruiter screen, a hiring-manager call, or anything else | Your resume, the job description, and (optionally) who you're meeting with | Prompt text — paste into a new Claude chat to generate the prep guide |
| **Salary Negotiator** (Step 5, Negotiate) | Turns a real offer, sourced market data, and your real qualifications into an actual negotiation plan and counter-offer draft | The offer details you have so far, plus your resume | Prompt text — paste into a new Claude chat to generate the negotiation guide |

Note the **Output** column above: none of these six tools produce a finished document by themselves. Each one builds a prompt that you copy into a separate Claude conversation, where the actual research, writing, or file generation happens. That's a deliberate design choice, not a missing feature — see "What's Consistent Across All Six Tools" below.

---

## How They Fit Together

There's a natural, largely fixed order across these six stages, with one deliberate fork in the middle:

**Step 1 → Step 2** is a fixed sequence. Job Posting Finder needs your Suggested Priority Rank to know which companies are worth checking — that data doesn't exist until Target Company Prompt Builder has already run. Research and rank first, then check real hiring activity for your top few.

**Step 3a and Step 3b don't have one correct order** — it depends on your situation:

- **Networking first:** use Outreach Message Builder (3b) to open a warm conversation with a contact before a specific posting is even in play, then tailor your resume with Resume & Cover Letter Tailoring (3a) once an actual opening exists.
- **Posting first:** find a real opening via Job Posting Finder, tailor your application immediately with Resume & Cover Letter Tailoring (3a), then use Outreach Message Builder (3b) to follow up with a contact after applying.

Both are legitimate strategies. Neither tool forces the other's order — they're built to be used independently, in whatever sequence matches how you're actually approaching a given company.

**Step 4 comes after Step 3 actually lands an interview**, whichever path got you there. Interview Prep Guide Builder's Recruiter Screen mode even includes salary-*range* coaching — explicitly framed as "state a range, not a negotiation yet."

**Step 5 comes after Step 4 actually produces a real offer.** Salary Negotiator is the direct sequel to that Recruiter Screen salary-range coaching, for once a real number is on the table and it's time to negotiate for real.

Afterward, the specific things discussed in the interview or the negotiation become real Context Notes for a genuinely grounded follow-up or thank-you message back in Outreach Message Builder (3b) — the funnel loops back on itself rather than ending in one direction.

---

## What's Consistent Across All Six Tools

A few design decisions were made once and carried through every tool, worth knowing about as a set rather than rediscovering per tool:

- **No install, no account, no server.** Every tool is a single self-contained HTML file. Open it in a browser, or host it via GitHub Pages — nothing is sent anywhere until you copy the generated prompt yourself.
- **Each tool generates a prompt — it doesn't do the work itself.** The web page assembles text; Claude (in a separate chat) does the actual research, writing, or drafting once you paste it in.
- **Every tool has an honesty guardrail suited to what it produces**, not a generic one copy-pasted across all six:
  - Target Company Prompt Builder — won't fabricate company data or figures; marks estimates as estimates.
  - Job Posting Finder — won't fabricate postings; reports fewer results rather than padding the list.
  - Resume & Cover Letter Tailoring — won't fabricate resume content or a recruiter's identity; a named gap is a correct answer, an invented qualification is not.
  - Outreach Message Builder — won't fabricate a relationship, shared history, or prior conversation detail that doesn't exist.
  - Interview Prep Guide Builder — won't write your actual behavioral stories for you, and won't invent detail about a named interviewer beyond real search results.
  - Salary Negotiator — the sharpest version in the family: never invents or exaggerates a competing offer. A fabricated one used in a real negotiation is a lie told to a real employer, not just bad draft output.
- **"Your background" is a shared, reusable field** — paste it once per tool, and it sharpens Suggested Job Title Keywords, Warm Introduction Path, cover letters, outreach messages, interview prep, and negotiation differentiators consistently, rather than each tool asking for a differently-shaped version of the same information.
- **Claude Settings requirements vary by tool, and each guide states them plainly up front** rather than assuming — see the quick-reference table below.

---

## Quick Reference: Claude Settings Needed

| Tool | Web Search | Code Execution & File Creation |
|---|---|---|
| Target Company Prompt Builder | Required — the entire tool depends on live research | Required for the `.xlsx` tracker output |
| Job Posting Finder | Required — the entire tool depends on live search for real postings | Only if you choose the Excel output format |
| Resume & Cover Letter Tailoring | Only if recruiter identification is turned on (default: on) | Only if you choose the Word document output format |
| Outreach Message Builder | Not required — drafts from research you already provide | Only if you choose the Word document output format |
| Interview Prep Guide Builder | Required — for company, interviewer, and (Recruiter Screen mode) salary research | Only if you choose the Word document output format |
| Salary Negotiator | Required — for market and company-specific compensation research | Only if you choose the Word document output format |
| LinkedIn Article Share Builder | Required — the entire tool depends on live search for real articles | Only if you generate artwork, or choose the Word document output format |
| Recruiter Message & Job Posting Sanity Check | Not required | Not required — the tool runs entirely in your browser; no Claude chat needed at all |

If a tool ever responds with an explanation of a missing capability instead of your actual output, this table is usually why — check the relevant toggle and re-run.

---

## Where to Find the Details

| Tool | Standalone Guide | Sale Fish Combined Guide (cover page + "About This Tool" + full guide) |
|---|---|---|
| Target Company Prompt Builder | `Prompt_Builder_User_Guide.md` / `.docx` | `Sale_Fish_Prompt_Builder_Combined_Guide.docx` |
| Job Posting Finder | `Job_Posting_Finder_User_Guide.md` / `.docx` | `Sale_Fish_Job_Posting_Finder_Combined_Guide.docx` |
| Resume & Cover Letter Tailoring | `Resume_Cover_Letter_Tailoring_User_Guide.md` / `.docx` | `Sale_Fish_Resume_Cover_Letter_Tailoring_Combined_Guide.docx` |
| Outreach Message Builder | `Outreach_Message_Builder_User_Guide.md` / `.docx` | `Sale_Fish_Outreach_Message_Builder_Combined_Guide.docx` |
| Interview Prep Guide Builder | `Interview_Prep_Guide_Builder_User_Guide.md` / `.docx` | *(none — single guide only)* |
| Salary Negotiator | `Salary_Negotiator_User_Guide.md` / `.docx` / `.doc` | *(none — single guide only)* |
| LinkedIn Article Share Builder | `LinkedIn_Article_Share_User_Guide.md` / `.docx` | `Sale_Fish_LinkedIn_Article_Share_Combined_Guide.docx` |
| Recruiter Message & Job Posting Sanity Check | `Recruiter_Message_Sanity_Check_User_Guide.md` / `.docx` | *(none — single guide only)* |

Each tool's own guide is the authoritative source for its specific fields, toggles, and output formats — this overview intentionally stays at the "what and why" level so it doesn't drift out of sync as individual tools evolve.

---

## A Seventh Tool, Outside the Funnel: LinkedIn Article Share Builder

Everything above is a linear (or semi-linear) job-search funnel. This tool isn't part of that funnel at all — it's for staying visible on LinkedIn and building an actual thought-leadership position, whether or not you're actively job hunting. It finds real, recent, on-brand articles worth sharing, narrows to the top 3, and drafts **two genuinely different posts for each** — an Informational Share (short, factual, safe to post often) and a Position/Stance take (a real point of view, grounded in your background) — plus optional matching artwork for whichever one you pick. That's 6 fully drafted options in one pass, not one draft to approve.

It shares the same design discipline as the other tools — an honesty guardrail suited to what it produces (only real, verifiable articles with real URLs; no padding the list if genuinely on-brand options are thin that day; the Position/Stance variant never invents a personal claim or credential beyond what you actually gave it). Your brand identity (name, tagline, eyebrow, background, ongoing themes) isn't remembered automatically by the page — an earlier version claimed it was "set once, reused every time," which turned out not to be true and was actively confusing. It now works through a genuine **Save/Load brand identity file** instead: download a small file once, reload it each time, rather than retyping or trusting a promise the tool didn't keep.

Like the funnel tools, this one generates a prompt for a separate Claude conversation — it doesn't draft the post itself.

One thing worth knowing if you ever consider automating it: running it manually through a Claude chat is free, same as every other prompt-generating tool in this suite. A fully automated "generate one every morning without me" version is possible but requires the Anthropic API directly and small ongoing costs — a genuinely different (and separate) consideration from the free, manual tool described here.

---

## An Eighth Tool, Also Outside the Funnel: Recruiter Message & Job Posting Sanity Check

Fake recruiter messages and fake job postings have both become common enough to warrant their own tool. This one is different in kind from every other tool in this suite: pick a mode — **Recruiter Message** or **Job Posting** — paste in the suspicious text, optionally note the claimed company and a relevant email, and check off any red flags you've noticed. The tool scores it against a fixed list of known scam patterns for that mode and hands back a verdict (Low / Caution / High) with every flagged phrase highlighted in place.

The two modes check genuinely different things — a message's sender vs. a listing's own legitimacy — so each gets its own full field set, checklist, and pattern library rather than a handful of shared fields with the rest bolted on.

Unlike every other tool in this suite, **this one does not generate a prompt for a separate Claude conversation.** It's a self-contained scanner — the entire check runs in your browser, and the finished result appears immediately. No Claude chat, no copy-paste step, no Claude Settings requirements at all.

It carries the same honesty discipline as the rest of the suite, adapted to what it produces: the score is explicitly labeled "pattern match strength" (message mode) or "listing risk signal strength" (posting mode), not a statistical probability of fraud, since no dataset exists to calculate a true probability honestly. A clean result never implies legitimacy is confirmed, and a flagged one is never treated as proof of a scam — both push the user back toward verifying independently.
