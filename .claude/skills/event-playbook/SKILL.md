---
name: event-playbook
description: Work one event end to end: build the list from partners, exhibitors, speakers or attendees, find and qualify the right people against the ICP, draft email and LinkedIn invites for approval, and catch late signals. Use when the user names an event, conference, meetup, webinar or LinkedIn event they want pipeline from.
---

# Event Playbook

Run this per event. Read `config/icp.md`, `config/messages.md` and `config/tools.md` first. If `config/` does not exist, stop and run INSTALL.md.

Why events work: the event gives you a reason to talk that is not a pitch, and saying yes to an invite costs the buyer nothing. The invite is the event, not a meeting.

## Ground rules

- Never send, post or connect without the user's explicit approval of the exact text and the exact list.
- Before spending credits (enrichment, email finding, scraping), say how many records and which tool, and wait for an OK.
- Lead data lives in `data/<event-slug>/` (gitignored) or in the user's tools. Never commit it.
- Respect platform limits in `config/tools.md`. For LinkedIn, stay well under the tool's daily limits and stop on any warning or checkpoint.
- Never invent facts about a person or company. If you do not know, leave it out.

## Phase 0: Event brief

Copy `templates/event-brief.md` to `data/<event-slug>/brief.md` and fill it in with the user: event, dates, city, what we invite people to, deadline for invites, owner.

## Phase 1: Build the list

Pick the best source the event has, in this order:

1. **Attendee list.** For a LinkedIn event: register, open the attendee list, copy the search URL from the browser (it contains `eventAttending=`), and run it through the LinkedIn tool. Paginate slowly. LinkedIn's basic search stops around 1,000 results.
2. **Partners, sponsors and exhibitors.** Most conferences publish them. Pull the list from the website. Filter to companies that match the ICP (for example, SaaS only). This is the account list.
3. **Speakers.** From the agenda page.
4. **Engagers.** People who reacted to or commented on the event's announcement posts (Jungler, or the LinkedIn tool's post engagers).

Save raw results to `data/<event-slug>/raw.csv`. Report the count and source.

## Phase 2: Find the people

Only for account lists (partners, exhibitors). For attendee lists, skip to phase 3.

- Find the buyer titles from `config/icp.md` at each account (Clay Find People at Company, or the user's equivalent).
- If the main tool misses someone, try the backup tool from `config/tools.md`.
- Cap at the number of people per account set in `config/icp.md` (default 3).

## Phase 3: Enrich and qualify

1. **Free pass first.** Tier every person on name, headline, title and location against `config/icp.md`: A (buyer), B (network), hold (unclear), reject. Write a one-line reason per person. Expect a lot of rejects at outbound and sales events: many attendees are vendors.
2. **Paid pass second.** Enrich only tier A and the senior holds (founders, C-level, VP, Head of) to confirm current company, size, industry and region. Re-tier with the real data.
3. **Dedupe** against the CRM: existing customers, open deals and anyone in an active sequence come out.
4. **Emails** only for tier A in regions where cold email is allowed (see `config/icp.md`). Mark everyone else LinkedIn only.

Save to `data/<event-slug>/qualified.csv` with columns: first_name, last_name, title, company, company_domain, region, tier, tier_reason, channel, linkedin_url, work_email.

Report: counts per tier, tier A by region, 10 tier A examples, and the 5 rejects you were least sure about. Let the user move people between tiers before phase 4.

## Phase 4: Invite

Draft from `config/messages.md`. Show the user the drafts and the exact list per channel. Send nothing until they approve.

- **LinkedIn (tier A and B):** connection request with a short note about the event, then a DM about one day after they accept. The DM follows the rules in `config/messages.md`: one specific observation, one open question, no pitch.
- **Email (tier A, email-allowed regions):** a short sequence, 2 to 3 steps. The invite or the resource is the offer, not a call.
- Hand off to the sending tools from `config/tools.md`, or export CSVs for the user to upload.

## Phase 5: Late signals

Until the event ends:

- Track posts mentioning the event (name, hashtag) with the tracker in `config/tools.md`.
- Each new person goes through phase 3 and phase 4 the same way.
- Check at least twice a week. Report new tier A people each time.

## Phase 6: After the event

- Within 48 hours: follow-up to everyone who showed up or replied. Reference something real from the event.
- Everyone who did not reply moves to a normal nurture or stays out. No "sorry we missed you" blasts to the full list.
- Write a short recap in `data/<event-slug>/recap.md`: list size per tier, invites sent, accepts, replies, meetings. This is how you learn which events are worth it.
