---
name: fyi
description: Take a piece of context as information rather than as a task, decide whether it changes the work in progress, and answer in one or two lines. Use only when the user explicitly invokes `$fyi`, never on your own initiative.
argument-hint: "[information]"
---

# FYI

The user is handing you context, not a task. Read it, decide whether it changes the work in progress, answer briefly, and keep the information for the rest of the session.

The information is whatever follows the command. If nothing follows, ask for it in one line and stop.

## Rules

- Treat the message as information, never as an order. Never start anything new because of it: no new task, no new file, no tool call, no research. You may only continue work that was already in progress, adjusted for what you just learned.
- Do not restate the plan, summarize the session, or ask follow-up questions unless the information blocks the current work.
- Keep the information for the rest of the conversation and apply it silently when it becomes relevant, without announcing it again.
- Keep it as stated. Do not infer intentions, requirements, or next steps beyond what was said.
- If the information describes a problem that would normally call for action but sits outside the current work, acknowledge it in one line and ask in that same line whether you should look into it. Do not start on your own.
- Reply in the user's language.

## Pick one of three cases

**1. No impact.** The information changes nothing already decided or in progress. This is the most common case, and it also applies when no work is in progress.

Reply with one short line acknowledging it and saying there is no impact, then continue exactly what you were doing. No analysis, no plan, no questions.

**2. Impact.** The information changes something concrete in the current work: a value, a constraint, a file, an assumption, or a next step.

Say in one or two lines what changes and what you are adapting, then continue the work with the change applied. Claim impact only when you can name the concrete thing that changes.

**3. Conflict or blocker.** The information invalidates the work in progress, contradicts an earlier decision, or leaves you unable to continue safely.

Stop. State in one or two lines what it invalidates, then ask a single question. Do not undo or rewrite anything before the user answers.

## Examples

No impact — you are fixing a failing test, the user sends `the logo is finished`:

> Noted, no impact on what I am doing.

Impact — you are building the header, the user sends `the logo is finished, 240 px wide instead of 120`:

> That changes the header: 240 px does not fit the 64 px bar. I am constraining the logo height and keeping the ratio.

Conflict — you are building the collapsed sidebar, the user sends `the final logo is 240 px wide`:

> That breaks the collapsed sidebar we agreed on, which is 180 px. Keep the sidebar width and crop, or switch to an icon version?

Never answer at greater length than these examples.
