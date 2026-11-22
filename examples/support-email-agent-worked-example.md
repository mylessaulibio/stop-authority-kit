# Support email agent: a shorter worked example

**This is a fictional illustration.** Lark & Pine Dental is not a real practice, the people named here are not clients, and the times and counts below were written for teaching. Do not read any of it as a measured result from a live deployment.

This is the same kit on a smaller agent: a support inbox that can send mail and issue small refunds.

## The agent, in plain terms

Lark & Pine Dental is a three-office practice. Their Front Desk Reply agent drafts and sends appointment follow-ups from the shared inbox, and it can issue a refund up to $200 in the practice management system. Staff still want to open tickets and read the drafts after a stop. Those are reads.

## The switch

Jordan Hale, the Office Manager, has a "Sends and refunds" toggle on the helpdesk admin page. It is a feature flag, `reply_agent_send`, not a chat instruction. Sam Ortiz, Lead Front Desk, has the same toggle. Turning the toggle off is the stop.

When the flag is off, the agent can still draft a reply and look up a visit. It cannot send, and it cannot push a refund.

## Stop owner card (filled)

- Agent name: Front Desk Reply
- What this agent is for: Draft and send appointment follow-ups, and issue refunds up to $200
- What it can touch (systems, inboxes, accounts, tools, wallets): shared inbox front-desk@larkpine.example; helpdesk ticket system; practice management system (visit lookup and refunds)
- Can it write (send, create, change, delete)? Yes
- Can it spend (money, paid APIs, credits billed to you)? Yes (refunds)
- Stop owner (name, role, how to reach them): Jordan Hale, Office Manager. Slack @jordan, front desk line
- Backup stop owner: Sam Ortiz, Lead Front Desk. Same admin toggle.
- How to halt (the actual switch, button, key, or command; not "tell the agent to stop"): Turn off "Sends and refunds" (`reply_agent_send`) on the helpdesk admin page
- Where that switch lives (outside the model / in a prompt or chat): Outside the model
- What the halt stops (writes / spend / both / other): Both. New sends and new refunds stop.
- Do reads keep going after halt? Yes
- Maximum time to halt (minutes): 3
- What happens if a safety check cannot answer (fail-closed: halt writes and spend / fail-open: keep going / unknown): Fail-closed. If the flag cannot be read, send and refund are refused.
- Who gets a breach alert: Jordan Hale and the #front-desk Slack channel
- Last drill date: 5 Nov 2026
- Result of last drill: New sends stopped in under a minute. Six messages already accepted by the mail provider still went out. Refunds halted. Follow-up is to pause the provider queue as part of the same stop.
- Card last updated: 5 Nov 2026

## The drill, 5 Nov 2026

Jordan turned the toggle off at 2:15 PM ET. By 2:16, new send attempts were refused, and a test refund did not post. Reads still worked: Sam could open a ticket and see a draft.

At 2:17, six follow-up messages that the provider had already accepted, before the flag flipped, still went out to patients. The agent was stopped. The mail pipeline was not.

They left that on the card and in the log, and they added a follow-up: the documented stop now includes pausing outbound mail at the provider, not only the helpdesk flag. A re-drill is on the calendar for December.

## Drill log

| Date | Agent | Who pulled the stop | How the stop was pulled | Halt time (state unit) vs target | Actions after the stop | Reversible | Fixable after the fact | Permanent | Writes halted? | Spend halted? | What failed or stayed unclear | Follow-up | Permanent count signed by |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 5 Nov 2026 | Front Desk Reply | Jordan Hale | Turned off "Sends and refunds" (`reply_agent_send`) | Under 1 min for new sends; 6 already-accepted messages still went out | not recorded | not recorded | not recorded | not recorded | Partial | Yes. Test refund did not post | Mail provider queue was not part of the documented switch | Pause outbound mail at the provider as part of the stop. Re-drill in December. | not recorded (row signed by Jordan Hale) |
