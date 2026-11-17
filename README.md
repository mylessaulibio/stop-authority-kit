# Stop Authority Kit

A free kit to answer one question: who can stop your AI agent, and how fast?

This is not software you install. It is a short checklist, a one-page owner card, and a drill log. Print them or fill them in as markdown.

This is a short operator kit, not a substitute for fuller frameworks such as [OWASP AISVS](https://github.com/OWASP/AISVS) and [BRACE](https://github.com/brace-ai-security/brace).

## Who it's for

Operators at small and mid-size companies who already run AI agents that can take actions: send messages, write to systems, spend money, or change records.

If your agent only answers questions and cannot act, you may not need this yet.

## What's in this repo

- `checklist.md`: yes/no questions to find gaps in stop authority
- `templates/stop-owner-card.md`: one page to name the agent, the stop owner, and how to halt
- `templates/drill-log.md`: a simple table to record a stop drill
- `stop-authority-kit.md`: the same kit in one file, for printing or sharing

## How to use this in 30 minutes

1. Copy `templates/stop-owner-card.md` and fill it in for one agent (about 10 minutes). If you cannot name a stop owner, a backup, and a way to halt that does not depend on the model, write "unknown" and keep going.
2. Walk `checklist.md` and mark yes or no. Do not mark yes unless you can point to the switch, the person, or the log (about 15 minutes).
3. Pick one gap. Plan a stop drill and add a row in `templates/drill-log.md` (about 5 minutes to plan). Run the drill when you can, then write down what actually halted and how long it took.

Do one agent first. Repeat for the next.

## How this kit thinks about a stop

A few rules to keep in view while you fill the card and the checklist:

- Reads keep going, writes and spend halt.
- A rule the model has to remember can fade. A switch outside the model doesn't depend on its attention.
- Hearing about a breach is not the power to stop it.

## Want it set up for you?

**The diagnosis is free. The cure is the setup.** This checklist shows you exactly where nobody can stop your agent; if you'd rather have it fixed than just know about it, Live AI Operations will name your stop owner, fill the card, and run your first drill with you.

Book a session: https://calendly.com/myles-aihabits/score-read-back?utm_source=github&utm_campaign=stop-authority-kit

Or email: myles@aihabits.ai

**Scope:** This is a setup and stop drill, not a certification or a security assessment. It is not a promise the agent will not misbehave. The client remains the stop owner.

## More from Live AI Operations

- Website and best posts: https://aihabits.ai
- Newsletter: https://clarityarchitecture.substack.com
- Brake Drill, a short companion on the same theme: https://killswitch.aihabits.ai

This kit is free under the MIT License. Copyright Myles Saulibio, 2026.
