---
name: event-debrief
description: "Write the V1 debrief for a B2B event: a pre-filled, fully sourced draft for the debrief call, filed a set number of business days after the event runs, plus the weekday sweep that decides which events are due. Use when a scheduled debrief run fires, when someone asks to debrief, write up, recap or close out an event (\"write the V1 for the Chicago dinner\", \"what's due for debrief this week\"), or asks why an event was or wasn't picked up. Do not write a debrief from memory: the figures and the skip rules both live in files."
---

# Event debrief (V1)

A V1 is a **draft for a debrief call**, not a finished document. Its job is to put every number that already exists in front of the people on the call, each with its source, and to name exactly what is still missing and who holds it. It is not a verdict and it does not close the loop on its own.

Two rules override everything else in this skill:

1. **Every figure carries its source file, row count and the date it was read.**
2. **Anything not sourced is written as an open question, never as an estimate.** A count with no source is not evidence.

A third rule is just as binding: **do not invent meeting counts, sentiment, attendee reactions, or anything said in the room.** If nobody wrote it down, the V1 says nobody wrote it down.

## Setup (once per team)

Fill in `config.md` before the first run. It holds:

- **Where events live**: the events database or tracker (Notion, Airtable, a sheet) and the property names for date, format, region, debrief status, debrief link and folder.
- **The house outline**: the debrief template doc. See `templates/debrief-outline.md` for a starting point. **If a human has edited the template, follow the edited version.** The template is how the team changes every future V1.
- **Commercial assumptions**: gross margin, payback period, planning win rate, trailing win rate, average ACV, meetings-to-opportunity rate.
- **ICP title rule**: who counts as a buyer.
- **Naming convention** for event IDs and files.

Read `config.md` and the house outline every time. Never substitute remembered figures, because assumptions change.

## Two modes

### Mode A: the weekday sweep (scheduled)

Runs every weekday, unattended. Finds every due event, writes a V1 for each, files it and links it. Nobody is watching, so make reasonable calls and **record them in the document** rather than stopping to ask.

### Mode B: one named event (on demand)

Someone names an event. Skip the due-date test: if a human asks for it, it is due. Still run the skip checks, but **report** rather than obey: "This event already has a debrief at <link>. Want me to write a second one, or read that one?" A human can override a skip; the sweep cannot.

Everything from *Gather* onward is identical in both modes.

## Finding what is due (Mode A)

**Due** = today is on or after **3 business days** after the event date. Business days are Mon–Fri, public holidays excluded.

Count forward from the day after the event, not from the event date itself:

> Event on Tue 27 Oct. Day 1 = Wed 28, day 2 = Thu 29, day 3 = Fri 30. Due **Friday 30 Oct**, not Wednesday.
> Event on Sun 25 Oct. Day 1 = Mon 26, day 2 = Tue 27, day 3 = Wed 28. Due **Wednesday 28 Oct**.

Weekend event dates are normal for field and partner events. Holidays push the due date later, never earlier.

An event with **no date set can never be due.** Mention it in the run summary if it looks like a completed event rather than a future one. That is a data gap, not a skip.

### Skip conditions

Skip the event if **any** of these is true:

| Check | Cost |
|---|---|
| Debrief status is `Done` or `N/A` | free (comes with the sweep query) |
| Debrief link is populated | free (comes with the sweep query) |
| The event page body already contains a debrief section | one fetch |
| A file named `<EVENT-ID>_DEBRIEF…` already exists in the event folder | one search |

**Run them in that order and stop at the first hit.** On a typical day the whole sweep is one query and nothing else.

The page-body check exists because **some teams debrief directly in the event page instead of in a separate doc.** Never create a document alongside a page that already carries the debrief. That duplicate is the one most likely to waste a human's afternoon.

**If nothing is due: stop. Write nothing, message nobody.** A quiet day is the expected outcome, not a failure.

## Gather

Fetch the **full event record, both properties and body.**

**The pre-event debrief flags logged on the page are the backbone of the V1.** They were written down at the time so they wouldn't have to be reconstructed from memory. Read them first, carry each one into the document, and for every one state plainly whether the data **confirms it, corrects it, or cannot settle it.** "Cannot settle it" is a real and frequent answer, and more useful than a guess.

Then read every linked artifact you can open: leads CSV, target list, contract, content, outreach, email copy, and anything sitting in the event folder that nothing links to. Note what you couldn't open and why. A broken link is itself a finding.

**If a prior instance of the same event or series exists, read its debrief and carry its theories forward.** Every prior theory needs a verdict. A theory that quietly disappears comes back next quarter.

## Compute, don't describe

Read the leads or attendee file properly and **compute from it**. Describing the file is not the job; the numbers are. Give the row count and the date read for each.

- attended vs registered vs no-show
- ICP prospects under the title rule in `config.md`
- exclusions **with counts** (vendor/sponsor-side, out-of-ICP function, excluded industries)
- match rate, cost per ICP prospect, cost per decision-maker

**Say when a classification is title-only** because the file has no revenue field. A title-only read does not clear a revenue bar and must not be presented as if it had.

### The bar

```
required pipeline   = all-in cost × pipe-to-spend multiple
pipe-to-spend       = 1 ÷ (gross margin × payback years × win rate)
required opps       = required pipeline ÷ ACV
meetings needed     = required opps ÷ meetings-to-opportunity rate
```

**Name the win rate every time you quote the multiple**, and show what the trailing rate would require next to the planning rate. Example: at 50% margin and an 18-month payback, a 30% planning win rate gives a 4.4× multiple, while a 15% trailing rate needs **8.9×**. The gap is entirely the assumption, and someone on the call will ask. Give the **T+90 date** and say the verdict stays open until then.

## Write

Follow the house outline section by section, in order, even where a section's honest content is "nothing sourced; open question." An empty section that names what is missing is doing its job.

Three sections carry most of the value and are the easiest to write badly:

**The finding that reframes the debrief.** One finding, in bold, with the number behind it. Not a summary. Look for a **gap between two measurements that should agree**: people who tried to attend vs people who got in, entitlements paid for vs entitlements used, who was in the room vs who there's a record of talking to. *Example: 44 registrants clicked "join" on a partner webinar but only 33 arrived. That's a technical failure, not an interest failure, and it was invisible in our own export.* Name the people or accounts in the gap when the list is short enough.

**Who the buyers actually were.** Apply the title rule and show the count with its method. Then the harder half: **title alone is the wrong follow-up filter.** Show the people a title rule misses: long attendance, senior, engaged, wrong job title. One past webinar settled on `(ICP title) OR (≥55 min in session AND work email)`. Propose the equivalent rule for *this* format, and flag that **the definition of a qualified lead is a decision for the call to make.**

**What to change next, cheapest first.** One variable per line, each phrased as a decision someone can take. Name the single change to make if only one changes. Finish with a **HOLD CONSTANT** line so the next event is still a clean read.

Under every open theory, leave a literal **"Your take:"** line for the call.

## File it

1. Create the doc in that event's folder, named `<EVENT-ID>_DEBRIEF_<ShortName>`. **Reuse the ShortName the event's other files already use**; don't coin a new one.
2. **Put the event ID on the first line inside the document**, so search still finds it after someone renames the file.
3. Paste the doc link into the event's debrief-link property.

The type token is `DEBRIEF`, never "Recap", "Post-Event" or "Retro". No dates, no "final", no "v2": version history does that job.

## Leave the outcome numbers to the humans

`Meetings Held`, `Qualified Leads`, `Opps Created`, `Pipeline T+90` and `Verdict` **stay empty.** Leave the debrief status alone too. **The loop closes when those five numbers are filled, not when a document exists.**

For each of the five, the V1 says **what it needs, who holds it, and what has to be decided first.** For `Qualified Leads` in particular, the definition itself is a call decision, so the V1 proposes a rule and flags it as unsettled rather than filling a number against an undefined bar.

Filling these from the leads file would be the single most damaging thing this program could do. They feed `Prior Performance` in the next cycle, which prices the next sponsorship.

## Output discipline

**The document and the link are the entire output. Do not notify anyone.** No Slack, no email, no push. People find the V1 on the event page, where they're already looking.

On an unattended sweep, end with a short run log: which events were due, which were skipped and on which condition, and which got a V1. On a quiet day that log is one line.
