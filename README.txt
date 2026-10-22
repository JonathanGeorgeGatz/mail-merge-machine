THE MAIL MERGE MACHINE — free giveaway from "Build It With AI", Episode 17
A Google Sheets + Apps Script tool: one letter, personalized for every customer on your list,
previewed first, drafted into your own Gmail by default — and a merge log that accounts for
every single row.

WHAT IT DOES
- Reads three tabs: Contacts (your list — any columns you like), Letter (a Subject row and a
  Body row, with {{Column Name}} fields filled from each contact), Settings.
- Writes a Preview tab with every finished letter BEFORE anything moves, and a Merge Log where
  every row lands somewhere: DRAFTED / SENT / HELD / SKIPPED / REFUSED, with the reason.
- Drafts by default: it creates Gmail drafts and sends nothing. Send mode is a separate,
  conscious choice — it only engages when the Settings cell "I reviewed the Preview" says yes,
  and it does the quota arithmetic up front (your budget AND Google's own remaining daily
  allowance, whichever is smaller), holding the overflow for tomorrow instead of dying mid-list.
- Refuses what it can't trust, out loud: blank or mistyped addresses, duplicates (the kept row
  is named), empty required fields. Honors your Opt Out column — those rows are skipped, counted
  and listed.
- Audits itself on every run: rows in = letters + opted out + refused; no letter leaves with an
  unfilled {{field}}; no two letters share an address; sends never pass the quota. On failure it
  prints DO NOT TRUST THIS MERGE and says why.

SETUP (about five minutes)
1. Make a Google Sheet with three tabs named exactly: Contacts, Letter, Settings.
2. Contacts: your list, headers in row 1 (the sample business's columns are in contacts.csv —
   import it to try the tool). Letter: cell A2 "Subject" with your subject in B2, cell A3 "Body"
   with your letter in B3, using {{Column Name}} wherever a contact's own value belongs.
3. Settings tab, two columns:
     Mode                     | drafts
     Daily send budget        | 100
     Opt-out column           | Opt Out
     Also require (columns)   |
     I reviewed the Preview   |
4. Extensions > Apps Script, paste mailmerge.gs, save, run buildMerge (authorize when asked —
   it needs Sheets and Gmail because drafts land in YOUR Gmail).
5. Read the Preview tab, then look in Gmail > Drafts. Nothing has been sent.
6. To actually send: set Mode to "send", type yes next to "I reviewed the Preview", run again.

FILES
- mailmerge.gs ......... the tool (pure engine + Sheets/Gmail wrapper), as shipped and tested
- engine_v1.gs ......... the FIRST build from the episode, defects and all (send-only, it died
                         on letter 23 of the sample list)
- engine_v2.gs ......... the second build the independent checker caught
- checker.py ........... the independent Python checker (same rules, zero shared code)
- contacts.csv, letter.csv ... the fictional sample business (Brightwell Heating & Air)
- PROMPTS.txt .......... the exact three prompts, word for word

HONEST LIMITS
- Quotas are real and they are Google's, not ours: on Google's own quota page, a script on a
  free Gmail account may reach about 100 recipients a day, and a Google Workspace account about
  1,500. The tool reads your remaining allowance before sending and holds what doesn't fit.
- This is for YOUR customers — people who know you, with an Opt Out column you honor. It is not
  a cold-email cannon, and deliverability of bulk mail is its own subject this tool does not
  solve.
- Sending happens from your own Gmail account, under your own name. The tool never sees a
  password and talks to no server: sheet in, drafts out.
- The sample business is fictional; every address ends in example.com. Any resemblance is
  coincidence.

Found a bug? Ask the AI to fix it — and make it prove the fix the way the episode does: on the
numbers, with a second opinion, not with reassurance.
