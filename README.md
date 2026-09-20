# hackerone-program-scout

Hermes skill that ranks **public HackerOne bounty programs** and drafts in-scope report outlines.

Research only. It does not test targets, write exploits, or generate payloads.

## One-line install

On the machine that runs Hermes:

```bash
hermes skills install https://raw.githubusercontent.com/motikolorado/hackerone-program-scout/main/SKILL.md
```

That installs `SKILL.md` only. To also get templates:

```bash
git clone --depth 1 https://github.com/motikolorado/hackerone-program-scout.git "${HERMES_HOME:-$HOME/.hermes}/skills/hackerone-program-scout"
```

On the Fly Hermes box (`HERMES_HOME=/opt/data`):

```bash
runuser -u hermes -- git clone --depth 1 https://github.com/motikolorado/hackerone-program-scout.git /opt/data/skills/hackerone-program-scout
```

## Use

New session, then:

> Load hackerone-program-scout and shortlist 8 public paid HackerOne programs with small scopes.

## What it does

- Reads the public HackerOne directory and program policies
- Ranks paid programs by scope size, bounty table, and recent public activity
- Writes a program brief and a report outline

## What it does not do

- Scan, exploit, or browse in-scope apps as an attacker
- Store or require a HackerOne API token
