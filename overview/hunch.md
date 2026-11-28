See the instruction you were about to type before you type it, written by a
copy of the agent's own session.

## What you get

- After each finished turn, up to three suggestions: the first as grey text
  inside the empty composer (the default), as numbered cards above the
  composer, or both.
- Press Tab or → in the empty composer, or swipe right on a touch screen, to
  put the first suggestion in the draft. Click a card to do the same with its
  text, or set clicks to send at once. Nothing is sent without your action.
- Silence when there is nothing to suggest: the model is told to return none
  while the agent says work is running, when the task is finished and you
  asked for nothing more, or when the only reply would be an acknowledgment.
- `bb hunch` to show, generate, and debug suggestions, and to see which route
  a thread's request takes.

## How it works

When a visible top-level thread goes idle, Hunch forks the thread's own Claude
Code or Codex session, so the model sees everything the agent saw, tool output
included, and asks it for your next message. A Claude Code fork runs with
no tools, a Codex fork runs in a read-only sandbox, and neither writes a
session file. Threads on other providers, and
sessions on another machine than the bb server, send the first request and the
newest user and assistant messages (no tool output) to the suggestion model
instead. Hunch keeps the suggestions until the thread moves on, across reloads
and restarts, and writes nothing to the thread or the agent's context.

## Requirements

BB 0.45 or newer. Claude Code forks need the `claude` CLI and Codex forks the
`codex` CLI, signed in on the machine that runs the bb server. They use your
existing Claude or ChatGPT subscription and need no API key.

- Claude Code forks run on Haiku 5.5 at low effort. Codex forks run on the
  session's own model at low effort.
- Other threads use the model picked in bb's provider/model picker: Claude
  Code's Sonnet 5.5 at low reasoning by default. Claude Code and Codex models
  run as a CLI call; other providers run as a hidden worker thread.
- An Anthropic- or OpenAI-compatible HTTP API, with your own key, can replace
  every route.

Each fork resends the whole session, so its cost grows with it. Measured on
one Mac: $0.0063 per Claude Code fork of a 60k-token session and $0.076 of a
150k-token session, as reported by the CLI.

The plugin ID is `hunch`. For installation, see the
[project README](https://github.com/Jonathanm10/bb-plugin-hunch#readme).

Hunch is a fork of [Next Prompt](https://github.com/CrazyCoder/bb-plugin-next-prompt)
by Serge Baranov.
