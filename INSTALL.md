# Setup: instructions for the coding agent

You are setting up the Event Playbook for the user. Follow these steps in order. Ask one question at a time, accept rough answers, and do not ask the user to clean them up. Do not send, post or publish anything during setup.

## 1. Check the folder

- Confirm you are inside the playbook folder (README.md, AGENTS.md and templates/ exist). If it was cloned into a subfolder, cd into it and run every later step from there. All paths below are relative to that folder.
- Create `config/` and `data/` if missing. Confirm `.gitignore` excludes `data/` and `config/`. Lead lists and personal data never get committed.

## 2. Check which tools you can reach

List the tools, MCP servers and CLIs available to you, and map them to these jobs:

| Job | Examples | Fallback if none |
|---|---|---|
| Find and enrich people | Clay MCP or Clay CLI, Apollo, AI Ark, People Data Labs | User uploads a CSV |
| Find work emails | Clay Work Email, Apollo, Prospeo, FindyMail | Skip email, LinkedIn only |
| LinkedIn (attendee lists, invites, DMs) | Crispy, HeyReach, Unipile, Expandi | User exports and sends by hand |
| Email sending | Instantly, Smartlead, lemlist | Export a CSV for the user to upload |
| Scrape web pages (exhibitor, partner and speaker lists) | Web fetch, Firecrawl, Clay | User pastes the list or uploads a CSV |
| Post and keyword tracking | Jungler, Clay signals, Trigify | User checks the event hashtag weekly |
| CRM dedupe | HubSpot, Salesforce, Attio, Pipedrive | User uploads a list of customers and open deals |

Tell the user what you found in one short table, and which jobs will fall back to manual. If a tool needs connecting, tell them how (for Claude Code: the MCP connector settings or `claude mcp add`). Never ask for API keys in chat. Keys go in environment variables or the tool's own config, never in this repo.

## 3. Ask the setup questions

Ask these one at a time. Short answers are fine.

1. What do you sell, in one or two sentences?
2. Who buys it? Titles, company type, company size, regions.
3. Who is never a fit? (Competitors, vendors who will pitch you, regions you do not serve, company types.)
4. Any regions where you only want LinkedIn, not cold email? (For example, some teams keep Germany on LinkedIn only.)
5. Which events do your buyers go to? Name one to start with.
6. What will you invite people to? A side event, dinner, coffee at the venue, a session, or a follow-up after the event.
7. Who approves messages before they are sent, and where? (In this chat, Slack, or the sending tool's review step.)
8. What language and tone do you write in? Paste one or two messages you sent that got good replies, if you have them.

If an answer leaves a gap (for example a size range with a hole in it, or no regions), ask one short follow-up.

## 4. Write the config

- Copy `templates/icp.md` to `config/icp.md` and fill it in from the answers. Keep the tier structure (A, B, hold, reject).
- Copy `templates/messages.md` to `config/messages.md`. Fill in voice and examples from question 8. Rewrite the example messages around what the user sells (question 1); never keep the template's topic. Keep the rules section as is unless the user changes it.
- Write `config/tools.md`: which tool does which job from step 2, a backup tool per job if there is one, any limits the user mentions (daily LinkedIn invites, email volume), and who approves messages and where (question 7).
- Create `data/<event-slug>/brief.md` from `templates/event-brief.md` for the event from question 5, with the invite from question 6. Event slug: lowercase, hyphens, with the year, for example `hannover-messe-2027`.
- Show the user the filled `config/icp.md` and ask for corrections before moving on.

## 5. Dry run

Use the event from question 5 (ask for the URL if you only have the name). The brief from step 4 counts as phase 0. Run phase 1 of the playbook only (build the list), on at most 25 companies or people, and show the result. If the event has not published a list yet, say so and stop. Do not enrich at scale or spend credits beyond a small sample without the user's OK.

## 6. Finish

Tell the user:
- Setup is done, and which jobs are manual.
- How to run it: "Run the event playbook for <event>". In Claude Code, `/event-playbook` works once the agent is started inside this folder.
- Where their files are: `config/` for settings, `data/<event-slug>/` for lists. Both stay out of git.
