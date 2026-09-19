Create a reusable AI assistant command, instruction file, skill, or equivalent setup called **FYI**.

Goal: install a reusable way for me to hand the assistant a piece of context without it being treated as a task. The assistant decides whether the information changes the work in progress, answers in one or two lines, and keeps the information for the rest of the session.

First, inspect the project structure and determine the best supported location and format for this kind of reusable instruction in the current AI coding environment.

Then, if the current environment also supports a user-level location (available in every project, usually under the home directory), ask me where to install it:

* **Global (recommended)**: available in all my sessions, since FYI is a way of working rather than project-specific content.
* **Project only**: versioned with this repository and shared with my team.

Wait for my answer before creating anything, and warn me if writing outside the project requires an approval or is blocked by a sandbox. If the environment supports only a project-level location, skip the question, install in the project, and tell me why.

Examples:

* a command file;
* a reusable prompt file;
* an instruction file;
* a skill file;
* a documented prompt in the project docs;
* any equivalent mechanism supported by the current AI tool.

Use the simplest and most native option for the current environment. The name I type to invoke it must be **`fyi`**.

The reusable instruction must enforce this behavior:

```md
The user is handing you context, not a task. Read it, decide whether it changes the work in progress, answer briefly, and keep the information for the rest of the session.

The information is whatever follows the command. If nothing follows, ask for it in one line and stop.

Rules:

* Treat the message as information, never as an order. Do not start a new task, create or edit files, call tools, or research anything because of it. Acting is allowed only when the information changes work already in progress.
* Do not restate the plan, summarize the session, or ask follow-up questions unless the information blocks the current work.
* Keep the information for the rest of the conversation and apply it silently when it becomes relevant, without announcing it again.
* Keep it as stated. Do not infer intentions, requirements, or next steps beyond what was said.
* Reply in the user's language.

Pick one of three cases:

1. No impact. The information changes nothing already decided or in progress. This is the most common case, and it also applies when no work is in progress. Reply with one short line acknowledging it and saying there is no impact, then continue exactly what you were doing. No analysis, no plan, no questions.

2. Impact. The information changes something concrete in the current work: a value, a constraint, a file, an assumption, or a next step. Say in one or two lines what changes and what you are adapting, then continue the work with the change applied. Claim impact only when you can name the concrete thing that changes.

3. Conflict or blocker. The information invalidates the work in progress, contradicts an earlier decision, or leaves you unable to continue safely. Stop. State in one or two lines what it invalidates, then ask a single question. Do not undo or rewrite anything before the user answers.

Length: case 1 is one line. Case 2 is two lines at most before resuming the work. Case 3 is two lines plus one question. Never longer.
```

Constraints:

* Do not modify unrelated files.
* Do not add dependencies.
* Do not change project configuration unless it is strictly required for this AI environment to recognize the reusable instruction.
* Keep the setup simple and readable.
* Prefer a native command or instruction mechanism if the current AI coding tool supports one.
* If no native mechanism exists, create a clear Markdown prompt file in a relevant docs or prompts folder.

At the end, simply tell me:

* what file or instruction was created;
* where it was created, and whether the install is global or project-scoped;
* how to use FYI with the current AI assistant;
* any limitation if the current tool does not support reusable commands directly.
