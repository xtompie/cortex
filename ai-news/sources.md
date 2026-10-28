# AI news — gdzie szukać

Adresy sprawdzone 2026-10-28 przez curl/gh: odpowiedź 200 i świeże wpisy, chyba że przy pozycji stoi inaczej.
Ocena: high, medium albo low, plus jedno zdanie, dlaczego warto.

## Claude Code i Anthropic

- [Claude Code CHANGELOG](https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md) — high — pełna lista zmian per wersja, także drobne zmiany UI i zachowania.
- [Claude Code changelog w docs](https://code.claude.com/docs/en/changelog) — high — ten sam changelog w czytelnej formie.
- [Claude Code releases (Atom)](https://github.com/anthropics/claude-code/releases.atom) — high — feed RSS nowych wersji.
- [Claude release notes](https://docs.claude.com/en/release-notes/overview) — high — zmiany w API, modelach i aplikacjach Claude.
- [Anthropic News](https://www.anthropic.com/news) — high — premiery modeli i produktów. Brak RSS, sprawdzać stronę.
- [Anthropic Engineering](https://www.anthropic.com/engineering) — high — artykuły techniczne o agentach, kontekście i ewaluacji.
- [Claude blog](https://claude.com/blog) — medium — poradniki i nowe funkcje produktów Claude.

## Inne laboratoria i produkty

- [OpenAI News (RSS)](https://openai.com/news/rss.xml) — high — premiery OpenAI. Aktywny, ostatni wpis 2026-10-28.
- [OpenAI API changelog](https://platform.openai.com/docs/changelog) — high — zmiany w API i modelach.
- [Google AI blog (RSS)](https://blog.google/technology/ai/rss/) — high — Gemini i produkty AI Google.
- [Gemini API changelog](https://ai.google.dev/gemini-api/docs/changelog) — high — nowe modele i funkcje Gemini API.
- [Mistral News](https://mistral.ai/news) — medium — premiery Mistral. Brak RSS.
- [Meta AI blog](https://ai.meta.com/blog/) — medium — Llama i badania Meta. Brak RSS.
- [Qwen blog (RSS)](https://qwenlm.github.io/blog/index.xml) — medium — premiery modeli Qwen.
- [DeepSeek API news](https://api-docs.deepseek.com/news/) — medium — premiery modeli DeepSeek.
- [Cursor changelog](https://cursor.com/changelog) — medium — zmiany w Cursorze. Dobry punkt odniesienia dla Claude Code.
- [GitHub Changelog (RSS)](https://github.blog/changelog/feed/) — medium — Copilot i funkcje AI na GitHubie. Dużo szumu niezwiązanego z AI.

## Feedy wydań kluczowych repo (GitHub `releases.atom`)

Każde repo na GitHubie ma feed `https://github.com/<owner>/<repo>/releases.atom`. Sprawdzone:
- [openai/codex](https://github.com/openai/codex/releases.atom) — high — Codex CLI.
- [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli/releases.atom) — high — Gemini CLI.
- [sst/opencode](https://github.com/sst/opencode/releases.atom) — medium — otwarty agent kodujący.
- [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent/releases.atom) — medium — Hermes Agent, około 258k gwiazdek.
- [github/spec-kit](https://github.com/github/spec-kit/releases.atom) — medium — Spec Kit (spec-driven development).
- [Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec/releases.atom) — medium — OpenSpec.
- [n8n-io/n8n](https://github.com/n8n-io/n8n/releases.atom) — medium — n8n. Wydania są bardzo częste, czytać tylko wersje minor i major.
- [obsidianmd/obsidian-releases](https://github.com/obsidianmd/obsidian-releases/releases.atom) — low — wersje Obsidiana.
- [modelcontextprotocol/modelcontextprotocol](https://github.com/modelcontextprotocol/modelcontextprotocol/releases.atom) — medium — wersje specyfikacji MCP.
- [ollama/ollama](https://github.com/ollama/ollama/releases.atom) — medium — lokalne modele i nowe architektury w Ollama.

Nowe ważne narzędzie → dopisz tu jego feed.

## Popularne i nowe repo

- [GitHub Trending (tydzień)](https://github.com/trending?since=weekly) — high — co zyskuje gwiazdki teraz. Wariant per język: `/trending/python?since=weekly`.
- [GitHub Topics, np. llm](https://github.com/topics/llm?o=desc&s=updated) — medium — repo w temacie. Też topics `ai-agents`, `mcp`, `claude-code`, `llm-wiki`.
- `gh search repos` — high — nowe repo z wieloma gwiazdkami od daty. Gotowe komendy (podmień datę na `discovered`):
  ```bash
  D=2026-10-01
  for q in agent llm claude mcp skill; do
    gh search repos "$q" --created ">$D" --stars ">300" --sort stars --limit 10 \
      --json fullName,stargazersCount,description
  done
  # starsze repo, które nadal rosną, w temacie:
  gh search repos "topic:llm" --updated ">$D" --sort stars --limit 20 --json fullName,stargazersCount
  ```
  Uwaga: wyniki są zaszumione. Trafiają się repo spoza AI, spam i repo z podbitymi gwiazdkami. Oceniaj po opisie i README.
- [Trendshift](https://trendshift.io/) — medium — ranking repo rosnących w czasie, z historią.
- [OSS Insight — AI](https://ossinsight.io/collections/artificial-intelligence) — medium — rankingi repo AI według wzrostu gwiazdek.
- [skills.sh](https://skills.sh) — medium — popularne skille do agentów, z liczbą instalacji. Liczby bywają podbite.

## Hacker News

- [HN Algolia API](https://hn.algolia.com/api/v1/search?tags=story&query=AI&numericFilters=points%3E200) — high — wyszukiwanie z filtrem punktów i daty. Działa stabilnie. Komenda od daty:
  ```bash
  TS=$(date -j -f %Y-%m-%d 2026-10-01 +%s)   # macOS; Linux: date -d 2026-10-01 +%s
  for q in AI LLM Claude agent; do
    curl -s "https://hn.algolia.com/api/v1/search?tags=story&query=$q&hitsPerPage=20&numericFilters=points%3E150,created_at_i%3E$TS" \
      | python3 -c "import json,sys;[print(h['points'],h['title'],h.get('url')) for h in json.load(sys.stdin)['hits']]"
  done
  ```
- [hnrss — front page powyżej 300 punktów](https://hnrss.org/frontpage?points=300) — medium — RSS najmocniejszych tematów dnia. Nie tylko AI.
- hnrss z wyszukiwaniem, np. `https://hnrss.org/newest?q=Claude&points=50` — low — 2026-10-28 wariant z `points` zwracał 502, a bez `points` działał. Niestabilne, dlatego podstawą jest Algolia.

## Blogi i newslettery

- [Simon Willison (Atom)](https://simonwillison.net/atom/everything/) — high — codzienne, rzetelne notatki o LLM, narzędziach i nowych modelach. Najlepsze pojedyncze źródło.
- [Latent Space (RSS)](https://www.latent.space/feed) — high — podcast i newsletter o AI engineering. Aktywny.
- [Interconnects — Nathan Lambert (RSS)](https://www.interconnects.ai/feed) — high — modele otwarte, trening, RL. Głęboka analiza.
- [Import AI — Jack Clark (RSS)](https://importai.substack.com/feed) — medium — tygodniowy przegląd badań.
- [One Useful Thing — Ethan Mollick (RSS)](https://www.oneusefulthing.org/feed) — medium — praktyczne użycie AI. Pisze rzadziej.
- [Karpathy blog (Atom)](https://karpathy.bearblog.dev/feed/) — medium — rzadko, ale wpływowo (np. LLM Wiki). Ostatni wpis 2026-04-30.
- [TLDR AI (RSS)](https://tldr.tech/api/rss/ai) — medium — codzienny skrót newsów. Szeroki, płytki.
- [AINews — smol.ai (RSS)](https://news.smol.ai/rss.xml) — low — kiedyś najlepsze podsumowanie dnia. Ostatni wpis 2026-09-09, sprawdzić, czy jeszcze działa.
- [Pragmatic Engineer (RSS)](https://newsletter.pragmaticengineer.com/feed) — medium — jak firmy naprawdę używają AI w inżynierii.
- [Hamel Husain (RSS)](https://hamel.dev/index.xml) — medium — ewaluacje i praktyka LLM.

## Społeczności

- [r/ClaudeAI — top tygodnia (RSS)](https://www.reddit.com/r/ClaudeAI/top/.rss?t=week) — medium — zgłoszenia nowych funkcji, problemów i trików z Claude Code.
- [r/LocalLLaMA — top tygodnia (RSS)](https://www.reddit.com/r/LocalLLaMA/top/.rss?t=week) — high — najszybsze info o otwartych modelach. Reddit przy częstych wywołaniach zwraca 429, odpytuj rzadko.
- [Lobsters — tag ai (RSS)](https://lobste.rs/t/ai.rss) — low — mniej szumu niż HN, mało wpisów.
- [Product Hunt — AI (Atom)](https://www.producthunt.com/feed?category=artificial-intelligence) — low — nowe produkty AI. Dużo marketingu.

## Modele: rankingi i trendy

- [OpenRouter Rankings](https://openrouter.ai/rankings) — high — które modele ludzie naprawdę używają, według tokenów.
- [Artificial Analysis](https://artificialanalysis.ai/) — high — porównanie modeli: jakość, cena, szybkość.
- [LMArena](https://lmarena.ai/leaderboard) — medium — ranking z głosowań ludzi. Curl dostaje 403, otwierać w przeglądarce.
- [Hugging Face — trending modele (API)](https://huggingface.co/api/models?sort=trendingScore&limit=20) — high — nowe otwarte modele, które zyskują teraz.
- [Hugging Face Papers](https://huggingface.co/papers) — medium — codzienne popularne prace naukowe.

## Jak robić Discover w tym temacie

Weź `D` = `discovered` z `ai-news/index.md`. Idź po kolei. Zbieraj kandydatów, nie czytaj wszystkiego.

1. **Claude Code**: CHANGELOG od wersji z daty `D`. Wypisz nowe funkcje, zmiany zachowania i zmiany UI. Pomiń poprawki błędów, chyba że zmieniają codzienną pracę.
2. **Premiery laboratoriów**: Anthropic News, Claude release notes, OpenAI RSS, Google AI RSS i changelogi API. Tylko wpisy po `D`: nowe modele, nowe produkty, duże funkcje.
3. **Feedy wydań repo**: tylko wydania minor i major po `D`, z sekcji „Feedy wydań kluczowych repo”.
4. **Nowe repo**: komendy `gh search repos` z `--created ">D"` i `--stars ">300"`, plus GitHub Trending (tydzień). Odrzuć spam, repo spoza AI i podbite gwiazdki.
5. **Hacker News**: Algolia z `points>150` i `created_at_i>D`, zapytania AI, LLM, Claude i agent. Zostaw tematy, które pojawiają się też gdzie indziej.
6. **Modele**: OpenRouter Rankings, Artificial Analysis i Hugging Face trending. Sprawdź, czy w czołówce jest coś nowego od `D`.
7. **Blogi**: Simon Willison, Latent Space i Interconnects, wpisy po `D`. Służą do potwierdzenia ważności i kontekstu, nie jako osobne kandydatury.
8. **Społeczności**: r/LocalLLaMA i r/ClaudeAI, top tygodnia. Na końcu, bo dużo szumu.

Progi:
- Kandydat wchodzi na listę, gdy spełnia jedno z dwóch:
  - jest oficjalną premierą albo wydaniem ważnego narzędzia;
  - pojawia się w co najmniej dwóch źródłach.
- Repo z jednego źródła wchodzi tylko przy szybkim wzroście, np. ponad 1000 gwiazdek od `D`.
- Zwróć co najwyżej 15 kandydatów, od najważniejszego.

Po Discover: ustaw `discovered`, a nowe, dobre feedy dopisz do tego pliku.
