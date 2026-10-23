---
name: "ambition"
description: "Push work past \"did what was asked\" toward the outcome it is for. Use when the user says \"be ambitious\", \"go deeper\", \"ambition\", \"depth prompt\", \"range review\", or wants a build or report to be actually good."
---

# Ambition

Source: https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/ (Felix Rieseberg, 13 Oct 2026).

Core problem: an agent finishes the literal task and stops, because nothing in the
request says what the task is *for*. Fix that before building, and prove the result
with something other than your own opinion.

The article names four kinds of ambition: Speed, Altitude, Depth, Range. Speed is already the default, so this skill covers the other three plus the judge.

Pick the levels that fit. Default for a normal build = **Altitude + Depth + Judge**.
**Range** only when the user asks for it (it spawns agents and takes a long time).
Skip all of it for quick one-off edits. Deeper means a better method, not more machinery: do not add frameworks or components the user did not ask for.

## 1. Altitude: aim at the outcome, not the task

Before starting, write down in 1-3 lines:
- **The outcome** this task serves (not "build the sales dashboard" but "close more deals this quarter": what's stuck and what to do next).
- **What done looks like at that level**, e.g. "crash-free" instead of "fix crash #412".
- **What the output must let the user decide or do.** For reports and dashboards: tell them what's wrong, why, and what to do, instead of only showing numbers. Name the **three most urgent decisions** with for/against arguments.

If the outcome is unclear, ask **one** question. Altitude is weak for purely creative work, where the deliverable stands on its own; skip it there.
Tell-tale that altitude is missing: the work still needs a meeting or a chat to decide what the numbers mean.

**Make it durable.** When the work recurs, don't just do it again: design something better that runs without the user re-asking (a scheduled job, a watcher, a dashboard feed). Before replacing the old way, backtest the new one on past data and run both side by side for a cycle. That only works if the Prerequisite below is met.

## 2. Depth: work the way the best practitioner would

A persona ("act as a senior X") changes the vocabulary and nothing else. Change the method instead.
Before building, answer these four in a short block shown to the user:
1. **What would a top professional in this field do here that wasn't asked for?**
2. **What raw material would they start from?** Logs, source data, the real API, actual analytics, primary documents. Not summaries or secondhand conclusions.
3. **Which specific methods and tools would they use?** Name them: Lighthouse traces instead of "make it faster", cohort analysis instead of averages, a database and statistics instead of markdown tables.
4. **What, other than me saying so, would prove the result is right?** A test, benchmark, metric, screenshot diff, or real-data replay.

Then restate the task as a deeper (not bigger) version and work from that.
If the user says "depth prompt", output only the rewritten prompt so they can paste it into a fresh session.

Techniques:
- **Stretch target.** Set a goal that can't be met by tweaking: "load in 200ms" when 5 seconds would do, "zero manual steps" instead of "fewer". Treat it as reasonable. When something looks impossible, tell yourself it is solvable and keep going; try at least one structural rethink before you say it can't be done.
- **Challenge what we believe.** Give the model the raw data and have it adversarially test an assumption: "we think X; try to reproduce that from the raw data."
- **Produce new knowledge.** Once deep in the data, build something that didn't exist (e.g. a simulation of customers built from logs), ask for blind spots and the earliest signal we don't know about yet, and check that it predicts on data it has not seen.

## 3. Outside judge: never grade your own work

You made every decision in the work, so you'll judge it kindly. Before calling non-trivial work done:
- **Mechanical judge first:** run the test, benchmark, linter, build, or page in a browser, whatever answered depth question 4. This is the judge the article asks for; the model reviews below are extras on top of it.
- **Fresh-eyes review** (works from Claude Code): run a separate non-interactive session with a *different* Claude model than the one that built it, e.g. `claude -p --model <another-claude-model> "<goal + depth answers + what to review>. Findings only, no fixes."` It has none of this session's reasoning, so it can't defend it.
- **Different-family review** (a model from another lab, not another Claude): same-family models share training and blind spots and tend to approve each other's output. Claude Code has no route to non-Claude models, so do not pretend. Instead:
  1. Write a self-contained review packet to a file: the goal, the depth answers, the full text or code to review, and the instruction "findings only, no fixes, cite exact lines or quotes, read-only, do not fabricate, flag what you could not verify".
  2. Tell the user the file path and ask them to run it through a non-Claude model (another lab's model, or another agent setup they have) and bring the findings back.
  3. Until that comes back, report the work as "mechanical and fresh-eyes reviewed, not cross-family reviewed". Do not call it fully reviewed.
- Use the cross-family step for written work (articles, sales or fundraising copy, analysis) and anything that matters. Fresh-eyes alone is fine for small code changes.
- Verify each finding yourself before acting on it.
- Report: what the judge found, what you fixed, and what you dismissed and why.

## 4. Range: bring in fields you wouldn't normally use (on request only)
1. **Noun to verb.** Restate the thing by what it does for people. Not "the pricing page" but "getting a busy buyer to trust us with their problem and decide in under a minute."
2. **Assemble the crew.** List 4-6 fields that are best at that verb, including at least one adversarial one (short seller, forensic accountant, regulator, skeptical customer).
3. **Do what they do, don't talk like them.** Each applies its profession's actual procedure (an audit checklist, a red-team pass, an editorial line edit), not its voice. Ask for what a short seller does to research a position, not for a short seller. Role-play only makes the transcript weirder. Run them in sequence as subagents, each seeing the previous one's changes. One level of delegation only, no nested agents.
4. Confirm the crew and the cost with the user before spawning. Finish with the outside judge.

## Prerequisite: can the model see whether it got there?

None of the above works if the agent can't observe the result. Check for and name what's missing:
- **Signal:** where failures show up (logs, crash reports, GSC, analytics, test output).
- **Context:** what maps a failure to a cause (versions to commits, the data to its source).
- **Sandbox and data access:** a computer that can install software, somewhere to reproduce and test a fix (local dev server, browser, staging server), plus the raw data (MCP, API, files).

If one is missing, say so up front. Don't guess around it. This is the same rule as "verify before claiming."
