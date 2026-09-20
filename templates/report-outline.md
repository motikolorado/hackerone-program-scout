# HackerOne report outline

Use only after the human has a real, in-scope finding. Agent fills structure. Human fills evidence.

## Title
{asset} — {vuln class} — {one-line impact}

## Program
- Handle:
- Policy URL:
- Asset (exact in-scope string):
- Confirmed in scope on (date):

## Summary
3–5 sentences. What is wrong, where, who is affected. No exploit recipe.

## Severity (suggested)
- CVSS / H1 rating:
- Why that rating (impact only):

## Steps to reproduce
Write as numbered checks the triage team can follow on an account they control.
Do not include payloads, exploit code, or bypass chains.
1.
2.
3.

## Impact
- Confidentiality / integrity / availability:
- Data or function at risk:
- Who can trigger it:

## Evidence (human attaches)
- [ ] Screenshot or video
- [ ] Request/response redacted
- [ ] Account used (test account only)
- [ ] Timestamp

## Mitigation (high level)
One paragraph. No exploit-improvement notes.

## Out of scope check
- [ ] Asset is listed in-scope
- [ ] Not in excluded vuln classes
- [ ] No other users' data accessed
- [ ] Testing stopped at proof, not damage
