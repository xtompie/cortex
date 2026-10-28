---
title: Modele z otwartymi wagami i modele lokalne (stan na 2026-10-28)
updated: 2026-10-28
tags: [open-weight, local-llm, ollama, qwen, deepseek, kimi, glm, meta, mistral]
sources:
  - "[Announcing Artificial Analysis Intelligence Index v5](https://artificialanalysis.ai/articles/artificial-analysis-intelligence-index-v5) — 2026-10-27 — high"
  - "[PyTorch — Muse Spark Is Now an Open-Weights Model](https://pytorch.org/blog/muse-spark-open/) — 2026-10-15 — high"
  - "[MarkTechPost — Meta Releases Muse Spark Open](https://www.marktechpost.com/2026/10/15/meta-muse-spark-open-816b-open-weight-model/) — 2026-10-15 — medium"
  - "[TechCrunch — Meta launches an open-weight model that runs on Macs](https://techcrunch.com/2026/10/15/meta-launches-an-open-weight-model-that-runs-on-macs/) — 2026-10-15 — medium"
  - "[LLM Gateway — LLMs Released in 2026](https://llmgateway.io/timeline/2026) — 2026-10-23 — medium"
  - "[Taskade — 10 Best Open-Source LLMs October 2026](https://www.taskade.com/blog/open-source-llms) — 2026-10 — low"
  - "[morphllm — The Best Open Source LLMs (October 2026)](https://www.morphllm.com/best-open-source-llm) — 2026-10 — low"
  - "[kingy.ai — Best Open-Weight AI Models 2026](https://kingy.ai/news/best-open-weight-ai-models-in-2026-glm-5-2-vs-deepseek-v4-vs-kimi-k2-6-vs-qwen-vs-mistral/) — 2026 — low"
  - "[Wikipedia — Qwen](https://en.wikipedia.org/wiki/Qwen) — 2026-10 — medium"
  - "[PromptQuorum — Best Local AI & LLMs 2026 by VRAM](https://www.promptquorum.com/local-llms) — 2026-10 — low"
  - "[BenchLM — Best Ollama Models (October 2026)](https://benchlm.ai/best/ollama-models) — 2026-10 — low"
  - "[InsiderLLM — Best Local LLMs for Mac in 2026](https://insiderllm.com/guides/best-local-llms-mac-2026/) — 2026 — low"
---

# Modele z otwartymi wagami i modele lokalne (stan na 2026-10-28)

> Najmocniejsze otwarte modele to Kimi K3, GLM-5.3, DeepSeek V4/V4.1, Qwen3.8 i Meta Muse Spark Open. To duże modele MoE z kontekstem 1M, do uruchomienia u dostawcy albo na kilku GPU. Luka do zamkniętej czołówki urosła: według AA v5 wynosi 12 punktów, a w v4.3 było to 3. Lokalnie, na jednej karcie 24 GB albo na Macu z 32 GB, najczęściej polecany jest Qwen 27B (3.8 albo 3.6) przez Ollamę.

## Czołówka otwartych modeli

| Model | Firma | Rozmiar (całość / aktywne) | Licencja | Uwagi |
|---|---|---|---|---|
| Kimi K3 (07-16) / K3.1 Pro (10-23) | Moonshot AI | K3: 2.8T / 104B | zmodyfikowana MIT (K2.6) | K3.1 Pro: 46 w AA v5, najlepszy otwarty, ale wag jeszcze nie wydano |
| GLM-5.3 (08-14) | Z.AI (Zhipu) | baza 753B GLM-5.2 | nowa licencja; GLM-5.3-Flash (320B / 18B) zostaje na MIT | AA v5: 32 (max), wspólne pierwsze miejsce wśród wydanych wag |
| DeepSeek V4 / V4.1 Flash | DeepSeek | V4-Pro 1.6T / 49B, V4 Flash 284B / 13B | MIT | V4.1 Flash 1017 (10-17): AA v5 32 (max), wspólne pierwsze miejsce wśród wydanych wag |
| Qwen3.8 (sierpień) | Alibaba | największy około 2.4T | duże: umowa o podziale przychodów powyżej US$50M rocznie; Qwen3.8 27B: Apache 2.0 | 27B to typowy wybór na jedną kartę |
| Muse Spark Open (10-15) | Meta | 816B / 42B, 1M kontekstu, multimodalny | Muse Model License | według Meta najmocniejszy otwarty model z USA; ta sama baza co zamknięty Muse Spark 1.3 |
| Mistral Large 4 (10-06) | Mistral | około 1T / 52B | wagi zapowiedziane na koniec października | na razie podgląd API |
| Nemotron 3.5 Super VL | NVIDIA | 120B / 12B, 1M kontekstu | — | wizja |

> **Status: Disputed** — liczby z AA zależą od wersji indeksu. W v4.3 GLM-5.3 miał 45, a Muse Spark Open 39. W v5 te same modele mają około 32, bo v5 to trudniejsze, prywatne testy. Porównuj tylko w obrębie jednej wersji.

Ważna uwaga z AA v5: zamknięty Claude Haiku 5.5 (max) ma 36 punktów, czyli więcej niż każdy model z publicznie wydanymi wagami.

## Lokalnie — co uruchomić

| Sprzęt | Model | Uwagi |
|---|---|---|
| 1 GPU 24 GB / Mac 32 GB | `qwen3.8:27b` (Ollama) | około 18 GB, 256K kontekstu, tekst i obraz; najczęściej polecany ogólnie |
| 1 GPU 24 GB, kodowanie | `qwen3.6:27b` | około 16 GB Q4_K_M; 77.2 SWE-bench Verified według BenchLM |
| Mac 32–48 GB | Qwen 3.6-35B-A3B (MLX 4-bit albo Ollama) | Ollama ma natywny runner MLX na Apple Silicon od wersji 0.19 (2026-03-31) |
| Kodowanie, MoE | `qwen3-coder:30b` | 30B / 3.3B aktywnych, około 19 GB, 256K |
| GPU 16 GB | `gpt-oss:20b` | rozumowanie na poziomie o3-mini |
| GPU 12 GB | Gemma 4 12B | około 8 GB, 256K, wizja i wywołania narzędzi |
| 2× Mac Studio M5 Ultra 512 GB | Muse Spark Open (MLX) | albo około 300 GB w 2-bitowym GGUF od Unsloth |

Najnowsza wersja Ollamy: 0.40.10 (2026-10-23).

## Ostatnie zmiany

- 2026-10-23 — Kimi K3.1 Pro: najlepszy otwarty w AA v5 (46), ale wagi jeszcze niewydane.
- 2026-10-21 — Qwen3.6 27B (Alibaba) według LLM Gateway.
- 2026-10-17 — DeepSeek V4.1 Flash 1017 (MIT).
- 2026-10-15 — Meta Muse Spark Open: 816B, otwarte wagi, uruchamia się na Macach (premiera razem z Apple).
- 2026-10-06 — Mistral Large 4 w podglądzie API, wagi zapowiedziane.
- 2026-08-14 — GLM-5.3 i Qwen3.8 27B.
- 2026-07-16 — Kimi K3.

## Jak stosować

- **Najwyższa jakość z otwartych wag:** Kimi K3 (wagi dostępne). K3.1 Pro, gdy Moonshot wyda wagi.
- **Agent albo kodowanie na własnym serwerze:** GLM-5.3 albo DeepSeek V4.1 Flash. Oba są wysoko w AA v5. DeepSeek ma licencję MIT.
- **Najlepsza cena:** DeepSeek, według kilku agregatorów.
- **Jedna karta albo laptop:** Qwen3.8 27B przez Ollamę (`ollama pull qwen3.8:27b`).
- **Licencja ma znaczenie:** sprawdź ją przed produkcją. MIT (DeepSeek, GLM-5.3-Flash) i Apache 2.0 (Qwen3.8 27B) są proste. Duże Qwen i Muse Spark Open mają własne licencje z warunkami.
- Otwarty model jest wyraźnie słabszy od zamkniętej czołówki. Wybieraj go dla prywatności, kosztu albo kontroli, a nie dla jakości.

## Zobacz też
- [Krajobraz modeli LLM (stan na 2026-10-28)](models-landscape.md) — cała czołówka, rankingi i trendy
