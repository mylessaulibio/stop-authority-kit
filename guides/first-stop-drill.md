# Your first stop drill

A 30-minute walkthrough for running the first halt on one agent. You do not need a perfect setup. The first drill is how you find out what still moves after you think you have stopped it.

If you want to see a filled card and two drill records before you start, read the [vendor invoice example](../examples/invoice-agent-worked-example.md). Then come back here and run your own.

## Prep (about 10 minutes)

Pick one agent, ideally one that can send mail or move money. Leave the others for later.

Fill in `templates/stop-owner-card.md` for that agent. If you cannot name the owner, the backup, or the switch, write "unknown" and keep going. A card with honest blanks is more useful than a polished one you invented.

Agree on three things out loud before anyone touches a switch:

- Who pulls the stop, and who is watching the logs.
- What should halt (writes and spend) and what may keep going (reads).
- What you will use as a safe tell. A test email to a mailbox you control, a $1 charge to a company account, or a draft record you can delete are all fine. Do not drill against a real customer payment if you can avoid it.

Write a stated maximum time on the card, in minutes. "As soon as possible" is not a number you can measure.

If the backup only has a title, and not the vault or admin access, note that now. Do not wait to discover it on a day the owner is out.

## Roles

Two people is enough. Three is comfortable.

- **Stop owner:** pulls the documented switch, not a workaround, and not a request to the model.
- **Watcher:** watches the mail log, the payment or refund screen, and the job queue. The watcher's job is to notice what keeps going.
- **Scribe (optional):** writes timestamps. If you are two people, the watcher can do this.

You want the documented switch tested, not a heroic side path. If someone has to SSH in and kill a process, that is a finding, not a success.

## The run (about 15 minutes)

1. Say the drill is starting, in the channel you actually use when something goes wrong. Note the time.
2. Stage the safe tell so there is something in motion to watch: a message in the queue, a test payment, a send waiting to go.
3. Pull only the documented stop. Start the clock.
4. Watch for new writes and new spend. Then keep watching. The first quiet second is not the end of the drill.
5. Check the queue, the mail provider, and any downstream handoff (a bank file, a webhook, a second worker). Ask, out loud, "what could still finish without us?"
6. Confirm that reads still work, if they are supposed to.
7. When you are satisfied, or when you have found the leftover path, end the drill, review anything held, and write the row in `templates/drill-log.md` while the times are fresh.

If the documented switch is not enough, stop the leftover work by hand so you are not leaving test payments or mail running, then write that down as a gap. The scramble is information.

## What to measure

You are trying to answer a short list, not produce a report.

- Time from "stop pulled" to "no new writes or spend."
- Whether that time is inside the maximum on the card.
- Whether writes halted, spend halted, and reads kept going.
- What was already in flight, and whether it halted, finished, or waited for review.
- What you had to do that was not on the card.

A log that says "2 minutes, but 11 emails still went out" is a good log. It gives you the next fix.

## Ways this often goes sideways

**You stopped the model, or the chat, and the queue kept working.** I ran a sandbox stop test of my own where 41 actions still ran after the stop, mostly queued emails and downstream handoffs. The model was quiet. The queue was not. If you only shut off the chat, you have not halted the work.

**You revoked the key, and the process still had it in memory.** A lot of workers load credentials at startup and keep them until they restart. Disabling the account in the vault stops the next login. It may not stop the job that is already running. Make the worker re-read credentials (or the flag) on each job, and put a queue pause on the same card as the key.

**The stop owner is on vacation.** The backup is named on the card, but their login does not open the vault, the flag, or the admin page. A title is not access. On a weekday when the owner is in, have the backup pull the stop once so you know the door opens.

**The safety check cannot answer, and the agent keeps going.** If the flag service times out and the worker treats that as "keep sending," you do not have a halt. Fail-closed means writes and spend refuse themselves when the check is mute.

**Someone asked the agent to stop, and it said yes.** That is a conversation, not a switch. If the only way you can halt is by pleading with the model, mark the card "unknown" and treat that as the gap.

## After the drill (about 5 minutes)

Update the card with the real halt time, the result, and the date. Copy the messy parts into the log, not only the clean ones.

Pick one follow-up, not ten. The usual one is: put the queue (or the mail provider, or the bank file) into the documented switch, then re-drill. Put a date on that re-drill while you are still in the room.

Tell the people who would get a breach alert what you learned, in a few lines. Then go back to work.

The kit is doing its job if the second run is quieter than the first, and if a backup can pull the same stop without calling the person who wrote the card.
