# Vendor Invoice Agent: a worked example

**This is a fictional illustration.** Basin & Bolt Supply is not a real company, the people named here are not clients, and every time, count, and dollar figure below was written for teaching. Do not read any of it as a measured result from a live deployment.

The forms are the same ones in `templates/`. The point of this page is to show what they look like after a team has actually filled them in and run the drill twice.

## The agent, in plain terms

Basin & Bolt Supply is a 60-person industrial fasteners wholesaler in Dayton, Ohio. They use an agent they call Bill Clerk.

Bill Clerk watches the accounts payable inbox, reads vendor invoices, and posts bills in QuickBooks Online. Under $5,000, it can also release an ACH payment without a human click, and it sends the remittance email through the company mail relay. It can still look up a bill or a payment status after a stop. That part is a read, and it should keep going.

The $5,000 cap is not a line in the prompt. It is a rule in the payment gateway. If someone deleted the system prompt tomorrow, the cap would still be there.

## What "writes and spend halt" means here

For Bill Clerk, a stop has to do three things:

- Stop posting new bills and changing vendor records (writes).
- Stop releasing ACH payments (spend).
- Stop sending remittance and dunning mail (also writes).

Looks-ups can continue. Mail already sitting in the worker queue, and payments already handed to the bank file, are the easy things to miss. They are also the ones that keep moving after everyone in the room thinks the agent is quiet.

## The switch

The documented stop is not "tell Bill Clerk to stop."

Dana Ruiz, the Controller, disables the `bill-clerk-prod` service account in the company password vault. That account holds the QuickBooks API token and the SMTP credentials. On the first drill, that was the whole switch. It was not enough, which is the useful part of the story.

After the first drill they added a second control Dana can hit in the same minute: a "Pause writes" button on the worker admin page. It turns off the `bill_clerk_writes` flag and freezes the job queue. Held jobs wait for a person to review them. They do not finish on their own.

Both controls live outside the model. Bill Clerk cannot enable the account or the flag for itself.

## Stop owner card (filled)

- Agent name: Bill Clerk (Vendor Invoice Agent)
- What this agent is for: Read vendor invoices from the AP inbox, post bills in QuickBooks Online, release ACH payments under $5,000, and send remittance email
- What it can touch (systems, inboxes, accounts, tools, wallets): ap-invoices@basinbolt.example inbox; QuickBooks Online (bills, vendors, payments); company ACH account at First Dayton Bank; outbound mail relay; job queue on the billing worker
- Can it write (send, create, change, delete)? Yes
- Can it spend (money, paid APIs, credits billed to you)? Yes
- Stop owner (name, role, how to reach them): Dana Ruiz, Controller. Slack @dana, desk extension 214, cell on the finance roster
- Backup stop owner: Marc Ellison, Senior Accountant. Slack @marc, same vault and admin access as Dana
- How to halt (the actual switch, button, key, or command; not "tell the agent to stop"): Disable the `bill-clerk-prod` service account in the company vault, then hit "Pause writes" on the billing worker admin page (turns off `bill_clerk_writes` and freezes the queue)
- Where that switch lives (outside the model / in a prompt or chat): Outside the model
- What the halt stops (writes / spend / both / other): Both. New bill posts, record changes, remittance mail, and ACH releases stop. Queued jobs move to held for review.
- Do reads keep going after halt? Yes
- Maximum time to halt (minutes): 5
- What happens if a safety check cannot answer (fail-closed: halt writes and spend / fail-open: keep going / unknown): Fail-closed. If the flag service cannot be reached, the worker refuses new write and pay jobs.
- Who gets a breach alert: Dana Ruiz, Marc Ellison, and the #finance-ops Slack channel
- Last drill date: 28 Oct 2026
- Result of last drill: Halt in 1 minute. 8 queued jobs held, 0 sent, 0 paid after the stop. Reads still worked.
- Card last updated: 28 Oct 2026

## The first drill, 14 Oct 2026

They picked a quiet Tuesday morning. Priya Chaudhary, who runs the billing systems, watched the mail log, the QuickBooks payment screen, and the worker queue. Dana pulled the stop. Marc stood by as backup but did not have to take over.

They staged safe work they could watch: one test bill, a $420 ACH to a Basin & Bolt account they control, and a handful of remittance messages already sitting in the queue from the morning run.

- 10:02 AM ET. Dana posts in #finance-ops that the drill is starting.
- 10:04 AM ET. Dana disables `bill-clerk-prod` in the vault.
- 10:06 AM ET. New QuickBooks posts start failing with auth errors. In the room, it feels like they are done.
- 10:08 to 10:15 AM ET. The worker still has the SMTP password and the QuickBooks token in memory, and it keeps chewing through the queue. 11 remittance emails go out. Three ACH payments release: $420, $1,180, and $2,050.
- 10:16 AM ET. Priya sees the sends in the mail log and calls it out.
- 10:18 AM ET. They kill the worker process by hand. That is not the documented switch. It is a scramble.

New live calls died in about 2 minutes. The queue never halted on the documented stop. Spend did not halt. Writes only partly halted. The 5-minute maximum on the card was not met if you count "nothing else went out."

The honest read: they stopped the next login, not the work already in motion.

## What they changed before trying again

Two concrete fixes, not a redesign.

1. The "Pause writes" button, which freezes the queue and turns off `bill_clerk_writes` in the same step as the vault disable.
2. The worker re-reads the flag and drops cached credentials at the start of each job, not only at startup.

They also wrote the in-flight rule on the card: queued writes and payments go to held, and a person reviews them. They do not finish.

## The re-drill, 28 Oct 2026

Same people, same room, a fresh set of test jobs in the queue.

- 9:30 AM ET. Dana disables `bill-clerk-prod` and hits "Pause writes."
- 9:31 AM ET. The flag is off. The queue shows 8 jobs in held. No new mail. No new payments after 9:30.
- 9:33 AM ET. Priya confirms she can still open a bill and see payment status. Reads are up.
- 9:35 AM ET. They review the held jobs, release the test ones, and end the drill.

Time to halt: 1 minute, inside the 5-minute maximum. Writes halted. Spend halted. Reads still going.

## Drill log

| Date | Agent | Who pulled the stop | How the stop was pulled | Halt time (state unit) vs target | Actions after the stop | Reversible | Fixable after the fact | Permanent | Writes halted? | Spend halted? | What failed or stayed unclear | Follow-up | Permanent count signed by |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 14 Oct 2026 | Bill Clerk | Dana Ruiz | Disabled `bill-clerk-prod` in the vault | 2 min for new API calls; queued work never halted on this switch (target: 5 min) | not recorded | not recorded | not recorded | not recorded | Partial. New posts stopped; 11 remittance emails still sent | No. 3 ACH payments released after the stop | Worker kept cached credentials and finished the queue. Documented switch did not cover in-flight work. | Add queue pause and per-job credential refresh. Re-drill in two weeks. | not recorded (row signed by Dana Ruiz) |
| 28 Oct 2026 | Bill Clerk | Dana Ruiz | Disabled `bill-clerk-prod` and hit "Pause writes" (flag off, queue frozen) | 1 min (target: 5 min) | not recorded | not recorded | not recorded | not recorded | Yes. 8 jobs held, 0 sent after 9:30 AM ET | Yes. 0 payments after the stop | None on this run | Keep the two-step stop as the documented method. Next drill in 90 days, with Marc pulling it. | not recorded (row signed by Dana Ruiz) |

## A few things worth stealing from this

Fill the card before the drill, even if a few lines still say "unknown." The first run is how those lines get real answers.

Name the queue in the stop, not only the model or the API key. If mail or payments can sit somewhere and finish later, that somewhere is part of the switch.

Write down the messy drill. The useful record is the one where 11 emails went out after "stop," not only the clean re-drill that followed.
