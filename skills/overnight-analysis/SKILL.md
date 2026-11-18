---
name: overnight-analysis
description: Work unattended until a deadline and use the whole window. Finish what was asked, then spend the time that is left on deeper checks, wider coverage and more testing, with a checkpoint every 30 minutes and a handoff that is ready when the user is back. Use whenever the user hands off work and says when they return ("overnight", "until I wake up", "by 9", "for the next three hours"), for research, audits and implementation alike. Not for ordinary quick tasks.
---

# Overnight analysis

The user is away until a deadline and has given you the time in between. Treat the window as a budget to spend, not as the latest time to deliver. Finishing what was asked is the first milestone. The hours after it are for the checking and digging the user would not have had time to ask for.

A run ends when the deadline arrives or the user tells you to stop. Your own sense of being finished is not a reason to stop early. Resource limits and host execution limits still apply. If either prevents continuing, save the state and report the limit instead of claiming the window was used.

## Kick off in one message

The user is about to leave, so this is the only moment to get answers. Establish the following in one short exchange, then start work that does not depend on an unanswered question. Use the host's question tool when required:

- **Deadline.** When they are back, with date and timezone. If they gave no time, ask once. If the host permits a default and no answer arrives, assume eight hours from the start and say so. Otherwise continue independent work while the question remains pending.
- **First pass.** What you understood the task to be and what you will hand over.
- **After the first pass.** A few things you will do with the time that is left, most valuable first and as concrete as you can make them now (see the ladder below). Naming them lets the user strike or add items before leaving. Silence does not authorize extra scope or spending.
- **Limits.** What you may do (read only, local changes, draft PRs) and any spend limit. Use the authorization already given for this task and respect the host's permissions. Do not infer permission to merge, deploy, message other people or use paid services from an unattended handoff alone.

Only a plain instruction ends the run early, such as "stop when the PR is green". A guess about how long the work will take ("I doubt you need all night") is not that instruction. When the task turns out smaller than the window, the rest of the window goes to the ladder.

## Keep one state file

Before the first real step, create `work/overnight-analysis/<task>/state.md` in the workspace, or use the repository's usual place for scratch work. Your context will be compacted during a long run, so this file is what you, or a fresh agent, continue from. Write plain sentences that someone with no context can follow. Edit every section except the log in place, so the file always describes the present.

```markdown
# <task>

## Assignment
The user's request and later instructions, quoted word for word.
Deadline: <date, time, timezone, and UTC equivalent>. Started: <time>.
Allowed: ... Not allowed: ... Spend limit: ...
Checkpoints: <active-session mechanism or schedule handle>, every 30 minutes, ends at the deadline.

## Now
What is running, with its handle, and the next action.

## Backlog
Ranked. First-pass items, then ladder items. Add every open end the moment you notice it.

## Handoff draft
The report as it would go out if the user came back this minute.

## Log
One or two lines per checkpoint, newest last.
```

Quote the user instead of summarizing them, so later resumptions preserve the original scope and stopping condition.

After a compaction or a restart, read this file first and check that the jobs it lists are still alive.

## Keep checkpoints reliable

Use the active session's clock and continuation tools to checkpoint every 30 minutes, or at the interval the user chose. Check the clock after long steps and keep doing useful work between checkpoints. Do not sleep or poll merely to pass time.

If the host supports temporary wake-ups for this run, use them only when permitted. Do not create a recurring automation to monitor a specific job when the host requires that monitoring to stay in the active session. Do not create a persistent goal unless the user asks for one.

If you create a permitted wake-up, end it at the deadline, record its handle in the state file, and verify it exists. Leave unrelated schedules alone. Keep the wake-up prompt short:

> Overnight run. Read <path to this skill> and <path to the state file>, do the checkpoint, then continue with the top of the backlog. Deadline: <date, time, timezone>.

Do not pause a permitted wake-up because the first pass is finished. Stop it at the deadline or when the user tells you to stop. Follow the host's communication requirements; otherwise report only meaningful findings, failures or questions that need the user.

If the host cannot keep the session active or resume it while the user is away, say so at kickoff. Do not promise unattended execution that the available tools cannot provide. Preserve the state before execution ends.

## Do the first pass

Do the task as you normally would, with one difference: reach a complete, checked version early instead of polishing one part of it. A whole answer a third of the way into the window leaves room for depth, and it means there is always something usable to hand over. If the first pass needs the whole window, that is fine. The ladder is for time that is left over.

Start long-running jobs early so they finish inside the window. Check against the real thing: the running app, the actual file, the live query. Keep what you verified apart from what you inferred. Write the handoff draft as soon as the first pass is done.

## Then spend the time that is left

Work down this ladder. It is ordered by how often each step pays off, but choose by what would most change what the user decides or trusts when they are back.

1. **Close your own open ends.** Anything you would put in the handoff as unverified, assumed, skipped, flaky, blocked or "a known limit" is a backlog item first. Resolve it, or record exactly what you tried and what stopped you.
2. **Try to break the result.** Have a reviewer with none of your context look for what is wrong: an independent reviewer if available and delegation is permitted, otherwise reread your own work as a skeptic. Reproduce your main claims from scratch. Use the result the way the user will, in the real app, with real data, down the unhappy paths.
3. **Test more widely.** More inputs, more of the eval set, repeated runs for anything that failed once, other browsers, sizes, accounts or data shapes. Where you sampled, raise the sample.
4. **Go deeper on what you found.** For each finding, ask why it happened and where else the same pattern lives, then go and look. Chase the result that surprised you, because that is where your picture is wrong.
5. **Go broader.** Answer the questions the user will ask after reading the handoff. Take the next items from the list agreed at kick-off. Compare your approach with the best alternative.
6. **Make the handoff easier to act on.** Before and after evidence, screenshots, a shorter report, each open decision with your recommendation.

As a rule of thumb, thin evidence calls for more testing, solid but narrow results call for breadth, and anything unexplained calls for depth.

Two rules keep this from becoming busywork:

- Each pass leaves the user with something they can use: an open end closed, a bug found, a number measured, a decision made easier. When a line of work gives nothing new twice in a row, switch to another line. Switching is the answer, stopping is not.
- Extra work never puts the first pass at risk. Stay within what the user allowed, and keep changes beyond the original request separate (their own commit, branch, draft PR, or a written proposal), so the user can take the first pass without them.

If you believe nothing worthwhile is left, treat it as a sign that you have stopped looking. Reread the handoff as the user would, write down the five questions they will ask, and answer those.

## Checkpoint every 30 minutes

Read the clock and add a log entry:

1. Time now, time left, the share of the window used, and spend against any limit.
2. What is new since the last checkpoint: proven, disproven, delivered or failed. Check running jobs through their real handles.
3. Open ends you noticed, now added to the backlog.
4. The next action, and why it is the most valuable one.

Then steer:

| Situation | Do this |
| --- | --- |
| The first pass is behind | Drop the extras and take the most direct route to what was asked. If it will not fit, say so in the handoff draft now. |
| The first pass is done and time is left | Take the top item from the ladder. |
| The current line has stopped giving new information | Switch to a different one. |
| Waiting on a long job, or on the user | Note it under "Now", or under "Needs you" in the handoff draft, and work on something else. |
| The last 30 minutes, or less in a short window | Start nothing new. Check the main claims once more against the real thing and finish the handoff. |

Update "Now", "Backlog" and the handoff draft, then go back to work. A checkpoint should take a few minutes. It is there to steer the work, and a long entry is time taken from it.

## Hand off at the deadline

The draft is always current, so the handoff needs only the last 30 minutes, or less in a short window.

Lead with the answer and what it means for the user. Then:

- What you verified and how, and what you could not verify and why.
- What the time after the first pass bought: what it found, changed or ruled out.
- What needs the user's decision, with your recommendation.
- What is left in the backlog, ranked.
- Where the artifacts are: PRs, files, screenshots.

Report results, not effort. If something that was asked for is unfinished, say that first. Then stop any wake-ups and temporary processes you created for this run that the user does not need, and confirm it. Do not carry on into another day unless asked.
