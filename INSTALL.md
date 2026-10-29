# Installing Cortex: instructions for an AI agent

You are an AI coding agent (Claude Code, Codex, Cursor, OpenCode or similar). The user asked you to install Cortex. Follow these steps. Ask one question at a time and wait for the answer. Talk in the user's language.

## 1. Location

Ask where to put Cortex. Suggest `~/cortex`. If the path already exists, stop and ask.

## 2. Clone

```bash
git clone https://github.com/xtompie/cortex.git <path>
```

## 3. Example topics

The repo ships with example topics written in Polish: `design/`, `ai-news/`, `agentic-engineering/`.

Ask: keep them, or start with an empty Cortex?

- **Start empty.** Delete every topic folder (each top-level folder that contains `index.md`). Replace root `index.md` with exactly:

  ```markdown
  # Cortex
  ```

  Remove `language` too: `AGENTS.md` sets it on the first topic, from the language the user speaks.
- **Keep.** Change nothing. Tell the user the wiki language is Polish (`language: pl` in root `index.md`), so new pages will also be in Polish.

## 4. Make it the user's own repo

The clone still points at `xtompie/cortex`. Ask which option they want:

- **Local only.** Run `git remote remove origin`.
- **Own GitHub repo.** Run `git remote remove origin`. Then ask for a name and visibility (private is the safe default) and run `gh repo create <name> --private --source . --push`.

If they started empty, offer a fresh history: `rm -rf .git && git init && git add . && git commit -m "Start Cortex"`. Do this only after a clear yes.

Never push without asking.

## 5. Explain how to use it

Tell the user, briefly:

- Open an agent session in the Cortex folder, or in any other project say: "use my Cortex at `<path>`".
- Then talk naturally. "How do I …?" asks the wiki. "Add `<url or file>`" adds a source. "Research X" fills a gap. "What's new in X?" finds news. "Check the wiki" cleans up.
- The full rules are in `AGENTS.md`. The user never has to read it.

## 6. First topic

Ask what they want to learn about first. Then follow `AGENTS.md`: "New topic", then "Research".
