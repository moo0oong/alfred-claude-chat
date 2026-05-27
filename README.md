# Claude Chat for Alfred

Ask Claude directly from the Alfred bar. Type `cld <question>`, get a markdown-rendered answer in a clean Text View. No API key, no extra cost — uses your Claude Max/Pro plan quota via OAuth.

<p align="center">
  <img src="icon.png" alt="Claude Chat icon" width="200"/>
</p>

## Install

1. Download [`Claude Chat.alfredworkflow`](Claude%20Chat.alfredworkflow)
2. Double-click the file → Alfred imports it
3. Make sure you're signed in to Claude Code:

   ```bash
   claude auth login
   ```

That's it. Trigger with `Alfred Hotkey → cld <question>`.

## Usage

| Command | What it does |
|---|---|
| `cld <question>` | Quick answer from Haiku, shown in Alfred's Text View |
| `cld -d <question>` | Copy question to clipboard + open Claude Desktop (for heavy queries) |
| `cld -d` | Just open Claude Desktop (no clipboard change) |

### Examples

```
cld how do I reverse a list in python
cld git rebase vs merge — when to use which
cld -d refactor this code into a class: [paste code]
```

## Requirements

- **macOS** with Alfred 5 + Powerpack
- **Claude Code CLI** — bundled with [Claude Desktop](https://claude.ai/download), or available standalone at [claude.ai/code](https://claude.ai/code)
- **Claude account** — Max plan recommended (Pro works with smaller quota)

## How it works

```
Keyword (cld) → Run Script (bash, calls claude -p --model haiku) → Text View (Markdown)
```

- Authenticates via OAuth — **no API key, no API credit consumption**
- Each call is an independent session (`--no-session-persistence`)
- System prompt nudges Claude toward concise markdown that fits Alfred's Text View
- For longer tasks, `-d` flag routes the question to Claude Desktop instead

## Customization

Open the workflow in Alfred Preferences and edit the Run Script object.

| To change... | Edit |
|---|---|
| Model (Haiku → Sonnet/Opus) | `--model haiku` |
| Response style | `SYSPROMPT` variable |
| Keep conversation context | Remove `--no-session-persistence` |
| Trigger keyword (`cld` → other) | Keyword object's `keyword` field |

## Limitations

- Answers display only after completion (no streaming)
- Alfred blocks until response arrives — use `cld -d` for long questions
- Alfred Text View doesn't render GFM tables, strikethrough, LaTeX, or Mermaid

## License

MIT — see [LICENSE](LICENSE).
