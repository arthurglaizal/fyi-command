Install **FYI** in Codex.

Goal: FYI lets me hand Codex a piece of context without it being treated as a task. Codex decides whether the information changes the work in progress, answers in one or two lines, and keeps the information for the rest of the session.

**Important:** do not trust any folder, file path, or format taken from memory, from older tutorials, or from this prompt. Codex changes its formats and locations over time. Work out what is current **now**, at the moment you run this.

## 1. Ask me first, then wait

Ask me where to install FYI:

* **Personal / global (recommended)**: available in all my Codex sessions, in every project. FYI is a way of working, not project content.
* **Project only**: stored inside this repository, versioned, shared with my team.

Wait for my answer before creating, moving, or writing anything.

## 2. Find out what Codex supports today

Before resolving any path:

* Read Codex's current official documentation about reusable, user-invocable instruction files (skills, custom prompts, or whatever the product calls them today). Start from the official Codex documentation site and follow any redirect you hit — the documentation has moved before.
* From that documentation, identify the format the product currently documents as the recommended one for this kind of reusable instruction, which files and metadata it requires, and the location matching the scope I chose.
* Then look at my machine: the installed Codex version, which of the documented folders already exist, and whether an older format is already in use here.
* If the documentation and my local environment disagree, tell me and ask which one to follow.

Do not assume the answer is the same as last year, or the same as what this repository already contains.

## 3. Show me the resolved path before writing

Print:

* the format you selected and why it is the current recommended one;
* the exact absolute path you are about to create, and every file you will put in it;
* the exact name I will type to invoke FYI.

If the target is outside this workspace, tell me clearly that the default sandbox may block writing there and that it will require my approval, and let me approve it.

## 4. Check for an existing installation

Before writing, check whether FYI is already installed at the resolved location **or** in any other location the current documentation still recognises, including an older format.

Treat these as existing installations:

* a real folder or file;
* a symlink pointing to a valid target, for example a local clone of the FYI repository;
* a **broken** symlink whose target no longer exists — report it as broken and ask me what to do.

If something already exists, never overwrite it silently. Show me the differences between what is there and what you would write, then ask me to confirm.

## 5. Create the files

Create only what the current format actually requires: the instruction file itself, plus any companion metadata file or folder structure the product requires today. Check the documentation for which fields are required and which are optional, instead of copying an old example.

The name I type to invoke FYI must be **`fyi`**. Put that name wherever the current format expects it — folder name, file name, or a metadata field. Check the documentation instead of guessing.

Do not create any legacy or deprecated format by default. If a legacy format is still supported and I explicitly ask for it, you may add it afterwards, clearly presented as optional and secondary.

The behaviour below must be preserved **exactly**. Copy this text as the instruction content. You may only adapt the wrapping — add, rename, or drop metadata fields so the file matches what the current format requires — never the rules themselves:

````md
---
name: fyi
description: Take a piece of context as information rather than as a task, decide whether it changes the work in progress, and answer in one or two lines. Use when the user explicitly invokes `$fyi` or hands over context prefixed with "for your information".
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
````

If the current format supports an optional companion file for how the skill is presented and invoked, and the documentation still describes those fields, use this content and adapt the field names to what is documented today. FYI must never be triggered implicitly — only when I invoke it myself:

```yaml
interface:
  display_name: "FYI"
  short_description: "Give context without giving a task."
  default_prompt: "Use $fyi to take this as context, not as a task."
policy:
  allow_implicit_invocation: false
```

If the field that disables implicit invocation no longer exists or has been renamed, tell me instead of silently dropping the intent.

## 6. Validate

After writing:

* confirm every file exists at the paths you announced;
* confirm they are valid for the current format, for example that required metadata is present and the YAML parses;
* if Codex offers a way to list installed skills or prompts, use it and show me the result.

## 7. Tell me

Keep it short:

* what was created, where, and whether the install is personal/global or project-scoped;
* how to invoke FYI, and how to use it: type the command followed by the information;
* whether a restart or a new conversation is needed before it is detected;
* anything you could not confirm in the official documentation.

## Constraints

* Do not modify any other file in this project.
* Do not rename or delete existing skills or prompts.
* Do not add dependencies.
* Do not change project configuration.
* Keep the installed files simple and readable.
