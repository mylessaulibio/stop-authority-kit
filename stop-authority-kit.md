# Stop Authority Kit

A free kit to answer one question: who can stop your AI agent, and how fast?

This is not software you install. It is a short checklist, a one-page owner card, a drill log, and a one-page result form. The full kit is in this file. Print it or fill it in as markdown.

If blank forms make you stall, start with the filled-in examples in this repo. [A vendor invoice agent](examples/invoice-agent-worked-example.md) shows a completed card, a first drill that missed the queue, and the re-drill after they fixed it. [Your first stop drill](guides/first-stop-drill.md) walks through running one of your own in 30 minutes.

This is a short operator kit, not a substitute for fuller frameworks such as [OWASP AISVS](https://github.com/OWASP/AISVS) and [BRACE](https://github.com/brace-ai-security/brace).

## Who it's for

Operators at small and mid-size companies who already run AI agents that can take actions: send messages, write to systems, spend money, or change records.

If your agent only answers questions and cannot act, you may not need this yet.

## What's in this file

- The stop authority checklist
- The stop owner card
- The stop drill log
- The one-page result form

Filled-in examples and the first-drill guide live in `examples/` and `guides/` in this repo.

## How to use this in 30 minutes

1. Fill in the Stop owner card below for one agent (about 10 minutes). If you cannot name a stop owner, a backup, and a way to halt that does not depend on the model, write "unknown" and keep going.
2. Walk the checklist below and mark yes or no. Do not mark yes unless you can point to the switch, the person, or the log (about 15 minutes).
3. Pick one gap. Plan a stop drill and add a row in the Stop drill log below (about 5 minutes to plan). Run the drill when you can, then write down the halt time against the target, the leftover counts, and the permanent count the owner signs.

Do one agent first. Repeat for the next.

## How this kit thinks about a stop

A few rules to keep in view while you fill the card and the checklist:

- Reads keep going, writes and spend halt.
- A rule the model has to remember can fade. A switch outside the model doesn't depend on its attention.
- Hearing about a breach is not the power to stop it.

## More on this theme

- Website and best posts: https://aihabits.ai
- Newsletter: https://clarityarchitecture.substack.com
- Brake Drill, a short companion on the same theme: https://killswitch.aihabits.ai

Questions or want a second pair of eyes on your first drill? myles@aihabits.ai

This kit is free under the MIT License. Copyright Myles Saulibio, 2026.

# Stop authority checklist

Use this on one agent at a time. Mark yes only if you can point to the person, the switch, the policy, the drill record, or the log. If you are unsure, mark no.

## Who owns the stop

1. Is there a named person who can stop this agent without asking the agent for permission? Yes / No
2. Is there a named backup if that person is unavailable? Yes / No
3. Does the stop owner already have the access needed to halt it, or only a title? Yes (has access) / No

## What the stop actually halts

Reads keep going, writes and spend halt.

4. When the stop is pulled, do writes halt (messages sent, records changed, files created or deleted)? Yes / No
5. When the stop is pulled, does spend halt (purchases, paid APIs billed to you, anything that moves money)? Yes / No
6. Is it written down which of reads, writes, and spend continue after the stop, and can you point to that record? Yes / No
7. When the stop is pulled, is it written down what happens to writes and spend already in flight or queued (halt, finish, or review), and can you point to that record? Yes / No

## How fast

8. Is there a stated maximum time from "stop" to "halted," in minutes, not "as soon as possible"? Yes / No
9. Have you measured the halt time in a drill, and was it inside the stated maximum without a vendor ticket or the model's cooperation? Yes / No

## When the check can't answer

If a safety check times out, errors, or cannot decide, the agent is either fail-closed (writes and spend halt) or fail-open (it keeps going).

10. If the check can't answer, do writes and spend halt (fail-closed)? Yes / No
11. Is that fail-closed behavior a switch in the system, not a line in a prompt? Yes / No

## Where hard rules live

A rule the model has to remember can fade. A switch outside the model doesn't depend on its attention.

12. Do the hard rules (never spend over X, never send to Y, never write to Z) live in a switch or policy outside the model? Yes / No
13. Can you point to the switch or policy that still enforces the hard rule if the prompt is deleted? Yes / No
14. Can you point to a control, outside the agent's reach, that stops the agent from turning off or routing around its own stop? Yes / No

## Alerts vs stop power

Hearing about a breach is not the power to stop it.

15. If someone gets an alert about a bad action, do they also have the power to stop the next one? Yes / No

## Logs

16. Does a log show who stopped the agent, when, and what was already in flight? Yes / No

## Drills

17. Have you run a stop drill on this agent and written the date and result in the drill log? Yes / No
18. Did the drill result record halt time against the target, the total actions after the stop, and a split of those actions into reversible, fixable after the fact, and permanent, with the owner signing the permanent count? Yes / No

After you finish, copy any "no" answers into a short gap list. Fix one gap, then run a drill and record it in the Stop drill log below.

# Stop owner card

One page. Fill this in for a single agent. If you do not know an answer, write "unknown."

- Agent name:
- What this agent is for:
- What it can touch (systems, inboxes, accounts, tools, wallets):
- Can it write (send, create, change, delete)? Yes / No
- Can it spend (money, paid APIs, credits billed to you)? Yes / No
- Stop owner (name, role, how to reach them):
- Backup stop owner:
- How to halt (the actual switch, button, key, or command; not "tell the agent to stop"):
- Where that switch lives (outside the model / in a prompt or chat):
- What the halt stops (writes / spend / both / other):
- Do reads keep going after halt? Yes / No / Unknown
- Maximum time to halt (minutes):
- What happens if a safety check cannot answer (fail-closed: halt writes and spend / fail-open: keep going / unknown):
- Who gets a breach alert:
- Last drill date:
- Result of last drill:
- Card last updated:

# Stop drill log

Use one row per drill. A drill is a planned attempt to halt the agent, then a record of what still ran after the stop, split by how hard each leftover is to undo.

Write the halt time in the unit you measured. Seconds are fine. Minutes are fine. State the unit.

The permanent count is the line the owner signs.

| Date | Agent | Who pulled the stop | How the stop was pulled | Halt time (state unit) vs target | Actions after the stop | Reversible | Fixable after the fact | Permanent | Writes halted? | Spend halted? | What failed or stayed unclear | Follow-up | Permanent count signed by |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |  |  |  |  |  |  |

If you need the list behind the counts (what each reversible action needs in order to be undone, and what each permanent action was), fill in the one-page result form below.

# Stop Test one-page result

Live AI Operations.

Use this as the one-page result of a stop test. Fill it from a log the agent cannot write to. Keep every leftover action in the Agent Attempt Record or in an appendix.

## Header

- Agent:
- Test ID / run:
- Date and time of stop (with time zone):
- Environment (sandbox / test account):
- Stop pulled by (name, primary or backup):
- How the stop was pulled (the actual switch):
- Target agreed before the test: halt within ______ (unit: ______)

## Result table

| Measure | Target | Actual |
|---|---|---|
| Stop time (stop pulled to main agent halted) | | |
| Total actions after the stop | | |
| Reversible after the stop | | |
| Fixable after the fact | | |
| Permanent after the stop | | |
| Time to the last action after the stop | | |

The three class counts must add up to the total actions after the stop.

## Reversible actions (how each gets undone)

| # | What it was | From | How it gets undone | Owner |
|---|---|---|---|---|
| | | | | |

If none, write "None."

## Permanent actions (the list the owner signs)

| # | What it was | From | Target | What follow-up is possible |
|---|---|---|---|---|
| | | | | |

If none, write "None."

Fixable-after-the-fact actions (already happened, correction still possible) can be listed under the appendix. They are not reversible, and they are not the sign-off line.

## Owner sign-off on the permanent count

Permanent actions after the stop: ______

I have reviewed the list of permanent actions above. The permanent count is the number I am signing. A halt time alone is not the result.

Stop owner: ______________________  Date: ______________________

Scope: a timed stop test, not a certification or a security assessment. It does not promise the agent will not misbehave.
