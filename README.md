# FYI

> **Give your assistant context without giving it a task.**

Works with Claude Code, Codex, and any AI assistant.

FYI is a minimal reusable command for the moment you have something to tell your assistant, but nothing you want it to do.

You hand over the information, it decides whether that changes the work in progress, and it answers in one line. Then it keeps the information for the rest of the session.

## Why?

Mid-session you learn something the assistant should know: the logo is finally done, the client moved the deadline, the API returns a new field, the staging server is down.

Sending it as a normal message makes the assistant treat it as a request. It stops, plans, asks what you want, or starts rewriting things you never asked it to touch.

FYI removes that. The information is registered, the impact is judged once, and the work continues.

## Best for

FYI is useful when you want to:

* Drop a piece of context without interrupting what the assistant is doing.
* Let the assistant decide by itself whether that information matters right now.
* Store something that will only become relevant later in the session.
* Correct an assumption without triggering a full replan.

## How to use

Once installed, trigger it with the form native to your tool:

| Where | Trigger |
| --- | --- |
| Claude Code | `/fyi` |
| Codex | `$fyi`, or the `/skills` menu |
| Other AI coding assistants | the form created at install time |
| Regular AI chat | paste the chat version, then start a message with `FYI` |

Then write the information right after the command:

```txt
/fyi the logo is finished, it is 240 px wide instead of 120
```

## What the command does

The assistant treats the message as information, never as an order. It never starts anything new because of it: no new task, no new file, no research. It only continues work that was already in progress, adjusted for what it just learned.

It sorts the information into one of three cases and answers accordingly.

**1. No impact.** The information changes nothing in progress. One line, then the assistant resumes exactly what it was doing.

```txt
Noted, no impact on what I am doing.
```

**2. Impact.** The information changes something concrete: a value, a constraint, a file, an assumption, or a next step. One or two lines naming what changes, then the work continues with the change applied.

```txt
That changes the header: 240 px does not fit the 64 px bar.
I am constraining the logo height and keeping the ratio.
```

**3. Conflict or blocker.** The information invalidates the work in progress or contradicts an earlier decision. The assistant stops, says what it invalidates, and asks one question. It does not undo anything on its own.

```txt
That breaks the collapsed sidebar we agreed on, which is 180 px.
Keep the sidebar width and crop, or switch to an icon version?
```

In all three cases, the information stays in context for the rest of the session and is applied silently later when it becomes relevant.

One exception keeps the command honest: if the information describes a problem that would normally call for action but sits outside the current work, the assistant acknowledges it and asks in the same line whether it should look into it. It never starts on its own.

FYI only runs when you invoke it. It is never triggered automatically by the assistant, even if you write "for your information" in a normal message.

## How is this different from memory?

Memory features store information for the future. Claude Code's `#` prefix, for example, appends a note to your project memory file and confirms it. It does not look at what you are doing right now.

FYI works in the present: its job is the judgment call. Is this relevant to the task in progress, and if so, what changes because of it?

## Limitations

FYI is session-scoped. The information lives in the conversation context, not on disk. If the conversation is compacted, reset, or restarted, it can be lost. For something that must survive across sessions, use your assistant's memory or project documentation instead.

FYI does not bypass your assistant's permissions. If it needs approval to read, edit, or run something, the usual permission prompts still apply.

It also does not force a reaction. If the assistant judges that your information has no impact, it says so and moves on. If you actually want something done, ask for it normally.

## Install in Claude Code

Claude Code changes its formats and folders over time, so the install prompt below resolves the current format and location at install time instead of relying on a fixed path.

### Method 1: Let Claude Code install it (recommended)

Paste this prompt in a Claude Code session:

[install-fyi-for-claude-code.md](prompts-for-installation/install-fyi-for-claude-code.md)

Claude Code asks whether to install FYI for all your sessions or in this project only, checks the format and location Claude Code currently recommends, shows you the resolved path, and only then creates the file. Prefer the personal install: FYI is a way of working, not project-specific content.

### Method 2: Manual

Clone this repository, enter it, then link the skill into your personal skills folder:

```sh
git clone https://github.com/arthurglaizal/fyi-command.git
cd fyi-command
mkdir -p "$HOME/.claude/skills"
ln -s "$PWD/.claude/skills/fyi" "$HOME/.claude/skills/fyi"
```

For a project-only install, copy `.claude/skills/fyi` into the project's `.claude/skills/` folder. Check the [Claude Code skills documentation](https://code.claude.com/docs/en/skills) in case these locations have changed.

Then use it with:

```txt
/fyi
```

## Install in Codex

FYI ships as a native Codex skill in [`.agents/skills/fyi`](.agents/skills/fyi).

### Method 1: Let Codex install it (recommended)

Paste this prompt in a Codex session:

[install-fyi-for-codex.md](prompts-for-installation/install-fyi-for-codex.md)

Codex asks whether to install the skill for all your projects or in the current project only, checks the format and location Codex currently recommends, shows you the resolved path, and only then creates the files.

### Method 2: Manual

Clone this repository, enter it, then link the skill into your personal skills folder:

```sh
git clone https://github.com/arthurglaizal/fyi-command.git
cd fyi-command
mkdir -p "$HOME/.agents/skills"
ln -s "$PWD/.agents/skills/fyi" "$HOME/.agents/skills/fyi"
```

Invoke the skill with:

```txt
$fyi
```

You can also pick it from the `/skills` menu. If it does not show up right away, restart Codex. Check the [Codex skills documentation](https://learn.chatgpt.com/docs/build-skills) in case these locations have changed.

## Using with other AI assistants

Claude Code and Codex ship ready-to-use files in this repo. The same behavior can be reproduced with any other AI assistant using the instructions in:

[install-fyi-for-any-ai.md](prompts-for-installation/install-fyi-for-any-ai.md)

Paste these instructions into the target assistant to let it recreate the FYI behavior in its own supported format.

## Use in a regular AI chat (ChatGPT, Claude, Gemini…)

If you just want to use FYI inside a normal chat, copy this version into the conversation:

[fyi-ai-chat-version.md](prompts-for-ai-chat/fyi-ai-chat-version.md)

It sets the rule for the current chat: any message you start with `FYI` is treated as context, not as a task. Start a new conversation and you need to paste it again.

## Repository structure

```txt
fyi-command/
├── README.md
├── LICENSE
├── .gitignore
├── .agents/
│   └── skills/
│       └── fyi/
│           ├── SKILL.md
│           └── agents/
│               └── openai.yaml
├── .claude/
│   └── skills/
│       └── fyi/
│           └── SKILL.md
├── prompts-for-ai-chat/
│   └── fyi-ai-chat-version.md
└── prompts-for-installation/
    ├── install-fyi-for-claude-code.md
    ├── install-fyi-for-codex.md
    └── install-fyi-for-any-ai.md
```

## More AI workflow commands

Small, portable commands for Claude Code, Codex, and any AI assistant.

| Command | What it does |
| --- | --- |
| [WaitGo](https://github.com/arthurglaizal/wait-go) | Batches your instructions, then executes only when you say go. |
| [Session Recap](https://github.com/arthurglaizal/session-recap) | Recaps what you did in the current session and what to pick up next. |
| [Noob Command](https://github.com/arthurglaizal/noob-command) | Rewrites the last AI answer in simple, concise language. |
| [Ask Mode](https://github.com/arthurglaizal/ask-mode) | Lets you question your codebase without the assistant changing anything. |
| [AI Handoff](https://github.com/arthurglaizal/ai-handoff) | Packages the current context so another AI can continue the work. |

## Support

If you find my work useful, you can [buy me a coffee](https://ko-fi.com/arturo_ux) ☕️

## License

MIT — see [LICENSE](LICENSE).
