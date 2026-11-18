# Event Playbook for your coding agent

From Revenue Systems Decoded, issue #2: "how we work an event".
Read the play first: https://www.revenuesystemsdecoded.com/p/issue-2-event-playbook

This repo turns that play into something your coding agent can run. Claude Code, Codex, Cursor or any agent that reads files and runs tools.

It does five things around one event:

1. Builds the list: the event's partners, exhibitors, speakers or attendees.
2. Finds the right people at those companies.
3. Enriches and qualifies them against your ICP (tier A, B, hold, reject).
4. Drafts the invite on email and LinkedIn. You approve every message before it goes out.
5. Catches late signals: people who post that they are going.

Nothing is sent without your approval. No lead data is written into this repo.

## Install (one paste)

Open your coding agent in an empty folder and paste this:

```
Clone https://github.com/outbound-catalyst/demo into this folder (git clone <url> .), then read INSTALL.md and follow it step by step. Ask me the setup questions one at a time.
```

Use a new, empty folder, not an existing project. If you cloned into a subfolder instead, restart your agent inside that folder so it picks up the playbook.

No git? Download the repo as a zip, unzip it, open your agent in the folder and paste:

```
Read INSTALL.md and follow it step by step. Ask me the setup questions one at a time.
```

Setup takes about 10 minutes. The agent asks about your ICP, the event and which tools you have, checks what it can connect to, and writes your config.

## Run it

After setup, for each event:

```
Run the event playbook for <event name or URL>.
```

In Claude Code you can also type `/event-playbook`.

## What you need

- A coding agent. Claude Code works best because the playbook ships as a skill.
- One way to find and enrich people. Clay (MCP or CLI) is what we use. Apollo, AI Ark or similar also work.
- Optional: a LinkedIn tool your agent can reach (for attendee lists and invites), an email sender (Instantly, Smartlead, lemlist), and a post tracker (Jungler or Clay keyword signals).

Missing a tool? The playbook falls back to CSV files you upload or export by hand.

## Files

| File | What it is |
|---|---|
| INSTALL.md | Setup instructions the agent follows once |
| .claude/skills/event-playbook/SKILL.md | The playbook itself, run per event |
| AGENTS.md | Same entry point for Codex, Cursor and other agents |
| templates/icp.md | Your ICP and tier rules, filled in during setup |
| templates/messages.md | Message rules and drafts for invites and DMs |
| templates/event-brief.md | One brief per event, filled in per run |

## Questions

Hit reply on the newsletter or find me on LinkedIn: Olivier Tytgat, Outbound Catalyst.
