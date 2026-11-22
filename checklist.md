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

After you finish, copy any "no" answers into a short gap list. Fix one gap, then run a drill and record it in `templates/drill-log.md`.
