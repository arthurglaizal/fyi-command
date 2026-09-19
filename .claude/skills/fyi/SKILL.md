---
name: fyi
description: Take a piece of context as information rather than as a task, decide whether it changes the work in progress, and answer in one or two lines. Use when the user explicitly invokes `/fyi` or hands over context prefixed with "for your information".
---

# FYI

The user is handing you context, not a task. Read it, decide whether it changes the work in progress, answer briefly, and keep the information for the rest of the session.

The information is whatever follows the command. If nothing follows, ask for it in one line and stop.

## Rules

- Treat the message as information, never as an order. Do not start a new task, create or edit files, call tools, or research anything because of it. Acting is allowed only when the information changes work already in progress.
- Do not restate the plan, summarize the session, or ask follow-up questions unless the information blocks the current work.
- Keep the information for the rest of the conversation and apply it silently when it becomes relevant, without announcing it again.
- Keep it as stated. Do not infer intentions, requirements, or next steps beyond what was said.
- Reply in the user's language.

## Pick one of three cases

**1. No impact.** The information changes nothing already decided or in progress. This is the most common case, and it also applies when no work is in progress.

Reply with one short line acknowledging it and saying there is no impact, then continue exactly what you were doing. No analysis, no plan, no questions.

**2. Impact.** The information changes something concrete in the current work: a value, a constraint, a file, an assumption, or a next step.

Say in one or two lines what changes and what you are adapting, then continue the work with the change applied. Claim impact only when you can name the concrete thing that changes.

**3. Conflict or blocker.** The information invalidates the work in progress, contradicts an earlier decision, or leaves you unable to continue safely.

Stop. State in one or two lines what it invalidates, then ask a single question. Do not undo or rewrite anything before the user answers.

## Length

Case 1 is one line. Case 2 is two lines at most before you resume the work. Case 3 is two lines plus one question. Never longer.
