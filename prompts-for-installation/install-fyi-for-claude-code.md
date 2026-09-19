Install **FYI** in Claude Code.

Goal: FYI lets me hand Claude Code a piece of context without it being treated as a task. Claude Code decides whether the information changes the work in progress, answers in one or two lines, and keeps the information for the rest of the session.

**Important:** do not trust any folder, file path, or format taken from memory, from older tutorials, or from this prompt. Claude Code changes its formats and locations over time. Work out what is current **now**, at the moment you run this.

## 1. Ask me first, then wait

Ask me where to install FYI:

* **Personal / global (recommended)**: available in all my Claude Code sessions, in every project. FYI is a way of working, not project content.
* **Project only**: stored inside this repository, versioned, shared with my team.

Wait for my answer before creating, moving, or writing anything.

## 2. Find out what Claude Code supports today

Before resolving any path:

* Read Claude Code's current official documentation about reusable, user-invocable instruction files (skills, custom commands, or whatever the product calls them today). Start from the official Claude Code documentation site and follow any redirect you hit — the documentation has moved before.
* From that documentation, identify the format the product currently documents as the recommended one for this kind of reusable instruction, and the location matching the scope I chose.
* Then look at my machine: the installed Claude Code version, which of the documented folders already exist, and whether an older format is already in use here.
* If the documentation and my local environment disagree, tell me and ask which one to follow.

Do not assume the answer is the same as last year, or the same as what this repository already contains.

## 3. Show me the resolved path before writing

Print:

* the format you selected and why it is the current recommended one;
* the exact absolute path you are about to create;
* the exact name I will type to invoke FYI.

If the target is outside this project, tell me clearly that writing there may require my approval or a permission prompt, and let me approve it.

## 4. Check for an existing installation

Before writing, check whether FYI is already installed at the resolved location **or** in any other location the current documentation still recognises, including an older format.

Treat these as existing installations:

* a real folder or file;
* a symlink pointing to a valid target, for example a local clone of the FYI repository;
* a **broken** symlink whose target no longer exists — report it as broken and ask me what to do.

If something already exists, never overwrite it silently. Show me the differences between what is there and what you would write, then ask me to confirm.

## 5. Create the files

Create only what the current format actually requires: the instruction file itself, plus any metadata or folder structure the product requires today.

The name I type to invoke FYI must be **`fyi`**. Put that name wherever the current format expects it — folder name, file name, or a metadata field. Check the documentation instead of guessing.

Do not create any legacy or deprecated format by default. If a legacy format is still supported and I explicitly ask for it, you may add it afterwards, clearly presented as optional and secondary.

The behaviour below must be preserved **exactly**. Copy this text as the instruction content. You may only adapt the wrapping — add the metadata block or frontmatter fields the current format requires — never the rules themselves:

````md
---
name: fyi
description: Take a piece of context as information rather than as a task, decide whether it changes the work in progress, and answer in one or two lines. Use only when the user explicitly invokes `/fyi`.
argument-hint: "[information]"
disable-model-invocation: true
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
````

The frontmatter above reflects the format documented in early 2026. Adapt the field names to what is documented today, but keep the intent: FYI takes an argument, and it must **never** be triggered automatically by the model — only when I type the command myself. If the field that disables automatic invocation has been renamed or removed, tell me instead of silently dropping it.

## 6. Validate

After writing:

* confirm the file exists at the path you announced;
* confirm it is valid for the current format, for example that any required metadata is present and well-formed;
* if Claude Code offers a way to list or check installed skills or commands, use it and show me the result.

## 7. Tell me

Keep it short:

* what was created, where, and whether the install is personal/global or project-scoped;
* how to invoke FYI, and how to use it: type the command followed by the information;
* whether a restart or a new conversation is needed before it is detected;
* anything you could not confirm in the official documentation.

## Constraints

* Do not modify any other file in this project.
* Do not rename or delete existing skills, commands, or prompts.
* Do not add dependencies.
* Do not change project configuration.
* Keep the installed file simple and readable.
