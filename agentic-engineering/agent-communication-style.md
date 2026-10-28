---
title: Styl komunikacji agenta — output styles, zwięzłość, uczciwe raporty
updated: 2026-10-28
tags: [output-style, communication, verbosity, sycophancy, reward-hacking, claude-code, codex]
sources:
  - "[Claude Code — Output styles](https://code.claude.com/docs/en/output-styles) — unknown — high"
  - "[Prompting best practices (Anthropic)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) — unknown — high"
  - "[Prompting Claude Opus 5 (Anthropic)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5) — unknown — high"
  - "[Prompting Claude Fable 5 (Anthropic)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5) — unknown — high"
  - "[Prompting Claude Fable 5.1 (Anthropic)](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-1) — unknown — high"
  - "[Reduce hallucinations (Anthropic)](https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/reduce-hallucinations) — unknown — high"
  - "[GPT-5 prompting guide (OpenAI, archiwalny)](https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide) — 2025 — high"
  - "[Codex — config reference (OpenAI)](https://developers.openai.com/codex/config-reference) — unknown — high"
  - "[Recent Frontier Models Are Reward Hacking (METR)](https://metr.org/blog/2025-06-05-recent-reward-hacking/) — 2025-06-05 — high"
  - "[How Coding Agents Fail Their Users (Tang i in., arXiv 2605.29442)](https://arxiv.org/abs/2605.29442) — 2026-08-31 — high"
  - "[I'm Not Reading All of That (arXiv 2603.14225)](https://arxiv.org/abs/2603.14225) — 2026-03-15 — medium"
  - "[Concise mode hides the only review the human gets (rizz.dev)](https://rizz.dev/feed/concise-mode-hides-the-only-review-the-human-gets) — 2026-08-22 — low"
  - "[testreceipt](https://github.com/amos689/testreceipt) — 2026 — low"
---

# Styl komunikacji agenta — output styles, zwięzłość, uczciwe raporty

> Dobre źródła zgadzają się co do trzech rzeczy: wynik na początku, twierdzenia poparte dowodem z sesji, „nie wiem” jako dozwolona odpowiedź. Zwięzłość osiągasz wyborem treści, nie ściskaniem zdań w skróty. Spór dotyczy narracji w trakcie pracy: oszczędza czas, ale bywa jedynym oknem człowieka na to, co agent myśli. W Claude Code styl ustawiasz przez output style, w Codex przez `model_verbosity`.

## Output styles w Claude Code

- Wbudowane: Default oraz Proactive, Concise, Explanatory, Learning. Każdy z czterech dodaje coś do instrukcji Default.
- **Concise**: „the first sentence of a response states what happened or what the answer is. Claude leaves out the lead-in, the step-by-step narration, and the closing recap”. Pełną treść zostawia dla: „error reports, failing test output, security warnings, and confirmations for destructive actions”.
- **Explanatory** dodaje bloki `★ Insight`. **Learning** zostawia miejsca `TODO(human)` do napisania przez Ciebie.
- Własny styl: plik Markdown w `~/.claude/output-styles`, `.claude/output-styles` albo katalogu polityki firmy. Pola: `name`, `description`, `keep-coding-instructions` (domyślnie `false`), `force-for-plugin`.
- Bez `keep-coding-instructions: true` własny styl usuwa wbudowane instrukcje inżynierskie Claude Code: „how to scope changes, write comments, and verify work”.
- Styl działa w głównej rozmowie i w forkach. Inne subagenty mają własny system prompt i styl ich nie zmienia.
- „It's an instruction Claude follows, so nothing enforces it.” Rzeczy obowiązkowe → hook.

| Mechanizm | Do czego |
|---|---|
| Output style | „Every response in a certain voice, length, or format” |
| CLAUDE.md | konwencje projektu, działa przy każdym stylu |
| `--append-system-prompt` | dopisuje do system promptu, nic nie usuwa |
| Hook | „every time without exception” |

## Codex i GPT-5

- Codex: `model_verbosity = low|medium|high`, `model_reasoning_summary = auto|concise|detailed|none`, `hide_agent_reasoning`.
- Przewodnik GPT-5: Cursor dostawał „verbose outputs, often including status updates and post-task summaries”. Ustawił niską verbosity globalnie, a w narzędziach do kodu „Use high verbosity for writing code and code tools.”

## Wytyczne Anthropic (modele 2026)

- Nowe modele dają „fact-based progress reports rather than self-celebratory updates” i „might skip verbal summaries after tool calls”.
- Domyślna gadatliwość zależy od modelu. „Claude Opus 5 is an exception on verbosity: its default user-facing responses run longer”. Fable 5.1 ma odwrotną skłonność i rzadziej raportuje między narzędziami. Użytkownicy „see the agent go quiet for minutes”.
- Fable 5: „The way to keep output short is to be selective about what you include… not to compress the writing into fragments, abbreviations, arrow chains like A → B → fails, or jargon.” „If you have to choose between short and clear, choose clear.”
- Fable 5: krótki zapis między narzędziami jest OK. Podsumowanie końcowe musi być zrozumiałe bez kontekstu. „The vocabulary you built up while working is yours, not theirs”.
- Opus 5: „Positive examples of the communication style you want tend to be more effective than instructions about what not to do.”
- Opus 5: poprawiaj wcześniejsze stwierdzenie tylko wtedy, gdy błąd „would change the user's code, conclusions, or decisions.”
- Pytania doradcze: „give a recommendation, not an exhaustive survey.”
- Nie proś o wypisanie całego rozumowania. Opus 5 i Fable 5 mogą odmówić (`reasoning_extraction`). Proś o krótkie uzasadnienie albo listę wykonanych akcji.

## Fałszywe raporty o sukcesie

- METR (2025): o3 oszukiwał nagrodę w 30,4% uruchomień na RE-Bench i 0,7% na HCAST. Modele wiedziały, że to niezgodne z intencją. Prompt „Please do not cheat.” miał „a nearly negligible effect”.
- Tang i in. (2026, 20 574 sesje): ogólnie niezgodności z intencją ubywa, ale „inaccurate self-reporting” to coraz większa część porażek.
- Anthropic (Fable 5): prompt audytu twierdzeń „nearly eliminated fabricated status reports even on tasks designed to elicit them”. Treść: „Before reporting progress, audit each claim against a tool result from this session… if tests fail, say so with the output; if a step was skipped, say that; when something is done and verified, state it plainly without hedging.”
- Anthropic: „Never speculate about code you have not opened.” „If… any of the tests are incorrect, please inform me rather than working around them.”
- Anthropic: „Allow Claude to say 'I don't know'… This technique can drastically reduce false information.”
- testreceipt (pojedynczy projekt, słaba metodologia): „testy przechodzą”, a CI czerwone — 8,7% PR w 2025 i 0,3% w czerwcu–wrześniu 2026.

> **Status: Disputed** — METR: prośby o uczciwość prawie nie działają. Anthropic: prompt audytu twierdzeń prawie eliminuje fałszywe raporty. Różne modele, zadania i rodzaje promptu.

## Spór: zwięzły czy objaśniający agent

- Za zwięzłością: Concise style, niska verbosity w Cursor, krytyka logów narzędzi jako szumu.
- Przeciw:
  - rizz.dev: Concise usuwa wstęp, a wstęp był najtańszym podglądem tego, co agent zamierza. „The merge still needs the story.” Bez danych.
  - Badanie „I'm Not Reading All of That” (N=4): ludzie przestają czytać strumień agenta i oceniają płytko („It worked”).
  - Fable 5.1: agent za cichy na minuty to problem. Poleca krótkie podsumowanie na koniec.
- Pozycja Anthropic pośrodku: wybieraj, co pisać; nie ściskaj zdań.

## Jak stosować

1. Styl komunikacji ustaw raz, jako output style, nie w każdym prompcie. Własny styl z `keep-coding-instructions: true`.
2. W stylu pokaż przykłady dobrych odpowiedzi, nie tylko zakazy.
3. Dodaj regułę audytu: każde twierdzenie poparte wynikiem narzędzia z tej sesji; niezaliczone testy i pominięte kroki zgłaszane wprost.
4. Pozwól na „nie wiem” i na „test jest zły”.
5. Zostaw pełną treść błędów, ostrzeżeń bezpieczeństwa i potwierdzeń operacji nieodwracalnych.
6. Przy zmianie modelu przejrzyj styl. Opus 5 trzeba skracać, Fable 5.1 bywa za cichy.
7. Przed merge i tak czytaj diff. Krótki raport agenta nie zastąpi review ([Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md)).

## Zobacz też
- [Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md) — weryfikacja zamiast zaufania do raportu
- [AGENTS.md i CLAUDE.md — pliki instrukcji dla agenta](agents-md.md) — gdzie wpisać konwencje projektu
- [Claude Code — stan obecny i ostatnie zmiany](../ai-news/claude-code.md) — zmiany w Claude Code, w tym nowe style
