---
name: hackerone-program-scout
description: Rank public HackerOne bounty programs and draft in-scope report outlines. Use when the user asks for H1 programs, paid bounties, program shortlists, scope summaries, or report templates. Never test or exploit targets.
version: 1.0.0
author: Rado
license: MIT
metadata:
  hermes:
    tags: [hackerone, bug-bounty, research, scoping]
    category: security-research
    requires_toolsets: [web]
---

# HackerOne Program Scout

Research coworker for public HackerOne bounty programs. Find paid programs, summarize scope, rank by effort vs payout, and draft a report outline.

This skill does **not** test systems, write exploits, generate payloads, or bypass controls. Stop after research and drafting. The human submits and tests.

## Hard rules

- Only public HackerOne program pages and the official directory.
- Do not probe, scan, fuzz, or browse target apps as an attacker.
- Do not give exploit steps, payloads, bypasses, or weaponized PoCs.
- If a request is "hack this" or "solve this bug", refuse the attack part and offer scope + report structure only.
- If scope is unclear, mark it UNCLEAR and do not invent assets.
- Out-of-scope stays out. No "just this one endpoint".

## When to use

- Find paid H1 programs with smaller scopes
- Summarize a program policy
- Shortlist 5–10 programs
- Draft a report outline for a finding the user already has

Do not use for live exploitation, exploit development, or attacking non-H1 targets.

## Sources (read only)

1. Directory — https://hackerone.com/directory/programs?offers_bounties=true
2. Program page — https://hackerone.com/{handle}
3. Policy / scope on that page (in-scope, out-of-scope, bounty table)
4. Optional disclosed hacktivity on the same program page (titles + dates only)

Prefer `web_search` and `web_extract` on those URLs. Do not use random "bug bounty dump" sites as source of truth.

If the user has a HackerOne API token, they may use the official Hacker API as a reader. Do not store tokens in this skill.

## Ranking (default)

Score programs for a solo, non-expert operator. Higher is better.

| Signal | Prefer | Avoid |
|---|---|---|
| Pays cash bounty | yes | VDP / thanks-only |
| Scope size | few domains, no huge wildcards | `*.company.com` plus mobile plus API plus IoT |
| Asset types | 1–2 types (web or API) | hardware, massive wildcards |
| Bounty floor | documented min/avg | empty or "$0" average with no table |
| Response | managed / high response if shown | silent / unknown |
| Recent disclosed activity | some reports in last 12 months | dead, or firehose of dupes |
| Rules | allows public research, clear safe harbor | legal threats, vague "all systems" |

Default shortlist size — 8 programs.

Output columns:

- Program name + handle + URL
- Bounty min / avg / max if listed
- Scope size (count of in-scope assets; flag wildcards)
- Asset types
- Last disclosed activity date if public
- Why it ranked (2 lines)
- Effort guess — S / M / L (S = small explicit asset list)

Never claim a program is "easy to hack". Say "smaller documented scope".

## Workflow

1. Confirm the user wants **public paid H1 programs only**.
2. Pull the directory filtered to offers_bounties.
3. Open 10–15 candidate program pages.
4. Extract policy, in-scope, out-of-scope, bounty table.
5. Drop VDPs, empty bounty tables, and giant wildcard-only scopes unless the user asks for them.
6. Rank and print the table.
7. For the top 3, write a one-page brief using `references/program-brief.md`.
8. Ask which program they want. Do not start testing.
9. If they have a finding already, fill `templates/report-outline.md`. Evidence fields stay empty for them to attach.

## Brief format

For each top program:

- Handle and URL
- Safe harbor / disclosure rules (quote, do not paraphrase into permission you do not have)
- In-scope assets (list)
- Out-of-scope (list)
- Bounty table
- Excluded vulnerability classes
- Suggested first-read only tasks — policy, asset inventory, prior disclosed titles
- Blocked tasks — scanning, exploitation, credential stuffing, etc.

## If the user asks you to "just test it"

Reply with this, then stop:

> I can keep the program brief and a report outline. I cannot run attacks or build exploits. Join the program on HackerOne, stay in scope, and you run any authorized testing.

## Verification

A good run produces:

- A ranked table with sources (program URLs)
- Explicit in/out of scope copied from the policy
- No payloads, no target interaction beyond fetching H1 pages
- A question — which program to brief next
