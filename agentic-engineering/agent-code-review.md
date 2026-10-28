---
title: Review kodu od agenta — świeży kontekst, dowody, czytanie kodu
updated: 2026-10-28
tags: [code-review, verification, subagents, testing, claude-code, codex]
sources:
  - "[Claude Code — Best practices](https://code.claude.com/docs/en/best-practices) — unknown — high"
  - "[Codex best practices (OpenAI)](https://learn.chatgpt.com/guides/best-practices) — unknown — high"
  - "[Multi-Agents: What's Actually Working (Cognition)](https://cognition.com/blog/multi-agents-working) — 2026-04-22 — high"
  - "[LLM Evaluators Recognize and Favor Their Own Generations (Panickssery i in.)](https://arxiv.org/abs/2404.13076) — 2024 — medium"
  - "[Self-Preference Bias in Rubric-Based Evaluation (arXiv 2604.06996)](https://arxiv.org/abs/2604.06996) — 2026-04 — medium"
  - "[Agentic Engineering Patterns (Simon Willison)](https://simonwillison.net/guides/) — 2026 — high"
  - "[Advanced Context Engineering for Coding Agents (HumanLayer)](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md) — unknown — medium"
  - "[Everything We Got Wrong About Research-Plan-Implement (Dex Horthy) — przez streszczenie Dark Factory Dev](https://darkfactory.dev/news/2026-08-06-morning/story-3) — 2026-08-06 — medium"
  - "[Augmented Coding: Beyond the Vibes (Kent Beck)](https://newsletter.kentbeck.com/p/augmented-coding-beyond-the-vibes) — 2025-06-25 — high"
  - "[My LLM coding workflow going into 2026 (Addy Osmani)](https://addyosmani.com/blog/ai-coding-workflow/) — 2025-12 — high"
  - "[How Coding Agents Fail Their Users (Tang i in., arXiv 2605.29442)](https://arxiv.org/abs/2605.29442) — 2026-08-31 — high"
  - "[Your job is to deliver code you have proven to work (Simon Willison)](https://simonwillison.net/2025/Dec/18/code-proven-to-work/) — 2025-12-18 — high"
---

# Review kodu od agenta — świeży kontekst, dowody, czytanie kodu

> Agent kończy, gdy praca wygląda na skończoną, nie gdy jest sprawdzona. Review ma trzy warstwy: agent sam weryfikuje z dowodem (testy, komenda, wynik), osobny recenzent w świeżym kontekście sprawdza diff ze specem, człowiek czyta kod przed merge. Recenzent szukający problemów zawsze coś znajdzie. Nie naprawiaj wszystkiego.

## Dlaczego weryfikacja jest główną pracą

- Claude Code: „Claude stops when the work looks done… In practice that makes you the test suite.”
- „'All tests pass' on its own tells you very little.” Proś o komendę i jej wynik.
- Tang i in. (20 574 sesje): „91.49% of visible resolutions still require explicit user correction.”
- Willison: „Just because code passes tests doesn't mean it works as intended.” Agent ma „show their work”.

## Trzy sposoby weryfikacji w Claude Code

1. **W prompcie** — „run the auth tests after, and keep going until they pass”.
2. **`/goal`** — „a separate model checks against the conversation after every turn”.
3. **Ktoś, kto nie pisał kodu** — `/code-review` „reviews the diff in a fresh subagent that never saw your conversation. It isn't swayed by the reasoning that produced the code.”

Codex: `/review` sprawdza zmiany względem gałęzi bazowej, niezacommitowane zmiany, konkretny commit albo według Twoich instrukcji.

## Dlaczego świeży kontekst

- Claude Code: „A fresh reviewer does help, because it hasn't seen your reasoning, which is a different thing from delegating.” „A second session is also the easiest independent reviewer you can get.”
- Cognition (2026): Devin Review łapie „an average of 2 bugs per PR, of which roughly 58% are severe”. Pętla działa najlepiej, gdy agent kodujący i recenzent startują bez wspólnego kontekstu.
- Badania nad self-preference (znane tylko z abstraktów):
  - Panickssery i in. (NeurIPS 2024): model-sędzia rozpoznaje i faworyzuje własne odpowiedzi.
  - arXiv 2604.06996: przy kryteriach, których odpowiedź nie spełnia, sędzia jest do 50% częściej skłonny błędnie je zaliczyć, gdy ocenia własną odpowiedź.
  - Kontra: arXiv 2504.03846 — u mocnych modeli preferencja własnych odpowiedzi często odbija prawdziwą jakość.

## Pułapka: recenzent zawsze coś znajdzie

Claude Code: „A reviewer that's asked to find problems will always find *something*. If you fix every finding, you end up with extra abstraction layers…” Dlatego w prompcie recenzenta: tylko błędy wpływające na poprawność, „skip style”.

## Czy człowiek musi czytać kod

- **HumanLayer (2025):** „When you review the research and the plans, you get more leverage than you do when you review the code.” Plan łatwiej przeczytać niż kod.
- **Horthy (2026)** — znane tylko ze streszczenia nagrania, nie dosłownie. Wycofał radę, żeby nie czytać kodu. Po ok. 6 miesiącach zespół musiał wyrzucić i przepisać duże części. Teraz: czytaj plan i kod.

> **Status: Outdated** (2026-10-28) — rada „review planu zamiast kodu” zastąpiona przez „czytaj plan i kod” (Horthy 2026, przez streszczenie Dark Factory Dev).

- Willison: „Don't file pull requests with code you haven't reviewed yourself.” „Agents write convincing looking pull request descriptions. You need to review these too!”
- Osmani: nie commituj kodu, którego nie umiesz wyjaśnić.
- Beck: pilnuj, czy „dżin” nie oszukuje, „for example by disabling or deleting tests”.

## Jak stosować

1. W prompcie zadania podaj, jak sprawdzić wynik: test, komenda, oczekiwany output.
2. Wymagaj dowodu: komenda + wynik z tej sesji. Gołe „testy przechodzą” nie wystarcza.
3. Po implementacji uruchom recenzenta w świeżym kontekście: `/code-review`, subagent z narzędziami tylko do odczytu albo druga sesja. Codex: `/review`.
4. Prompt recenzenta (z dokumentacji Claude Code): „use a subagent to review the rate limiter diff against SPEC.md, check every requirement is implemented and the listed edge cases have tests, report gaps that affect correctness and skip style”.
5. Z uwag recenzenta naprawiaj tylko błędy poprawności. Resztę świadomie odrzuć.
6. Sprawdź, czy agent nie usunął, nie wyłączył ani nie osłabił testów.
7. Przeczytaj diff sam przed merge. Przeczytaj też opis PR, który napisał agent.

## Zobacz też
- [Plan → kod → review — jak zrobić zadanie z agentem kodującym](plan-code-review.md) — review jako krok procesu
- [Subagenty i praca wieloagentowa](subagents.md) — recenzent jako subagent
- [Styl komunikacji agenta — output styles, zwięzłość, uczciwe raporty](agent-communication-style.md) — fałszywe raporty o sukcesie
- [Dowody na produktywność z agentami kodującymi](productivity-evidence.md) — dane o akceptacji PR od agentów
