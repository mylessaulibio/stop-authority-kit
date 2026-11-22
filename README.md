# Stop Authority Kit

A free kit to answer one question: who can stop your AI agent, and how fast?

This is not software you install. It is a short checklist, a one-page owner card, a drill log, and a one-page result form. Print them or fill them in as markdown.

If blank forms make you stall, start with a filled-in example. You will see how the card and the log look once they are filled in, including a first drill that did not go cleanly.

This is a short operator kit, not a substitute for fuller frameworks such as [OWASP AISVS](https://github.com/OWASP/AISVS) and [BRACE](https://github.com/brace-ai-security/brace).

## See it filled in

[A vendor invoice agent at a mid-size wholesaler](examples/invoice-agent-worked-example.md) is a fictional walkthrough with a completed stop owner card, a first drill where queued mail and payments kept going, and the re-drill after they fixed the switch.

There is also a shorter fictional write-up of [a customer-support email agent](examples/support-email-agent-worked-example.md).

When you want to run your own, use [Your first stop drill](guides/first-stop-drill.md). It is a 30-minute walkthrough of prep, roles, what to measure, and the ways a stop often fails in practice.

## Who it's for

Operators at small and mid-size companies who already run AI agents that can take actions: send messages, write to systems, spend money, or change records.

If your agent only answers questions and cannot act, you may not need this yet.

## What's in this repo

- `checklist.md`: yes/no questions to find gaps in stop authority
- `templates/stop-owner-card.md`: one page to name the agent, the stop owner, and how to halt
- `templates/drill-log.md`: a simple table to record a stop drill, including leftover counts and a sign-off on the permanent count
- `templates/one-page-result.md`: the one-page result form (halt time against target, reversible and permanent lists, owner sign-off on the permanent count)
- `examples/invoice-agent-worked-example.md`: a filled card and two drill records for a fictional vendor invoice agent
- `examples/support-email-agent-worked-example.md`: a shorter fictional example for a support inbox agent
- `guides/first-stop-drill.md`: how to run your first drill in 30 minutes
- `stop-authority-kit.md`: the same kit in one file, for printing or sharing

## How to use this in 30 minutes

1. Copy `templates/stop-owner-card.md` and fill it in for one agent (about 10 minutes). If you cannot name a stop owner, a backup, and a way to halt that does not depend on the model, write "unknown" and keep going.
2. Walk `checklist.md` and mark yes or no. Do not mark yes unless you can point to the switch, the person, or the log (about 15 minutes).
3. Pick one gap. Plan a stop drill and add a row in `templates/drill-log.md` (about 5 minutes to plan). Run the drill when you can, then write down the halt time against the target, the leftover counts, and the permanent count the owner signs. Use `templates/one-page-result.md` for the list behind those counts.

Do one agent first. Repeat for the next. The [first-drill guide](guides/first-stop-drill.md) walks through the run itself.

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
