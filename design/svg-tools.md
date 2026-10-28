---
title: Narzędzia SVG — render, optymalizacja, modele i benchmarki
updated: 2026-10-28
tags: [svg, tools, svgo, benchmark]
sources:
  - "[rsvg-convert(1) — Arch manual pages](https://man.archlinux.org/man/extra/librsvg/rsvg-convert.1.en) — unknown — high"
  - "[Convert SVG to PNG From the Command Line — techearl.com](https://techearl.com/convert-svg-to-png-command-line) — unknown — low"
  - "[svgo 4.1.0 — jsDocs.io](https://www.jsdocs.io/package/svgo) — unknown — high"
  - "[Experimental SVGO optimization — withastro/roadmap #1317](https://github.com/withastro/roadmap/discussions/1317) — 2026-03 — medium"
  - "[A Deep Dive into SVGO Configuration — allsvgicons.com](https://allsvgicons.com/blog/svgo-configuration-maximum-compression/) — unknown — low"
  - "[StarVector — joanrod/star-vector](https://github.com/joanrod/star-vector) — unknown — high"
  - "[OmniSVG: A Unified Scalable Vector Graphics Generation Model (NeurIPS 2025)](https://arxiv.org/abs/2504.06263) — 2025-04 — high"
  - "[SVGenius: Benchmarking LLMs in SVG Understanding, Editing and Generation](https://arxiv.org/abs/2506.03139) — 2025-06 — high"
  - "[SVGEval: Vision-Grounded Perceptual-Quality Benchmarking in Text-to-SVG](https://arxiv.org/abs/2608.01977) — 2026-08 — medium"
  - "[simonw/pelican-bicycle](https://github.com/simonw/pelican-bicycle) — unknown — high"
  - "[Gemini 3.1 Pro — Simon Willison](https://simonwillison.net/2026/Feb/19/gemini-31-pro/) — 2026-02-19 — high"
---

# Narzędzia SVG — render, optymalizacja, modele i benchmarki

> Do pętli „render i sprawdź” wystarczy `rsvg-convert` albo `resvg`, które zamieniają SVG na PNG do obejrzenia. Dla SVG mocno korzystających ze specyfikacji renderuj w headless Chrome. Gotowe SVG przepuść przez SVGO v4 z `multipass` i rozsądnym `floatPrecision`. Wyspecjalizowane modele (StarVector, OmniSVG) robią głównie wektoryzację obrazów. Do ilustracji z opisu wystarcza ogólny LLM z dobrym procesem, patrz [Workflow generowania SVG przez LLM](svg-workflow-llm.md).

## Render SVG do PNG (pętla sprawdzania)

- **rsvg-convert** (librsvg, GNOME): `rsvg-convert -w 512 in.svg -o out.png`. Instalacja na macOS: `brew install librsvg`.
  - Podanie `-w` i `-h` naraz rozciąga obraz. Proporcje zachowa `--keep-aspect-ratio` (man page).
  - `-b white` daje białe tło. Domyślnie tło jest przezroczyste, co utrudnia ocenę ciemnych obrysów.
  - Nie obsługuje SVG zależnych od JS ani części funkcji SVG 2.0 (techearl).
- **resvg** (Rust): `resvg -w 1024 icon.svg icon.png`. Plik wyjściowy to argument pozycyjny, bez `-o`. Ma też wersję dla Node i WebAssembly.
- **Headless Chrome / Playwright**: jedyny renderer, który pokazuje to samo co przeglądarka, gdy SVG mocno korzysta ze specyfikacji (techearl). Przydatny, gdy SVG ma CSS, animację lub jest osadzony w stronie.
- ImageMagick bez librsvg używa słabego własnego renderera. Lepiej go unikać.

## Optymalizacja: SVGO

- SVGO v4: `removeViewBox` nie należy już do `preset-default` (jsDocs svgo 4.1.0, Astro #1317). Stare porady o wyłączaniu go dotyczą v3. W v4 to nadmiarowe, ale nieszkodliwe.
- Ważne opcje: `multipass: true`, globalne `floatPrecision`. W CLI precyzję ustawia `svgo -p <n>`.
- Zbyt niska precyzja widocznie zniekształca kształty. `cleanupIds` może zepsuć odwołania z animacji, `<use>` i CSS/JS (allsvgicons). Wyłącz go, gdy grafika ma `aria-labelledby` lub animację po id.
- Praktyczna rada (allsvgicons, low): `floatPrecision` 2 dla ikon, 3 dla szczegółowych ilustracji.

```js
// svgo.config.mjs
export default {
  multipass: true,
  floatPrecision: 2,
  plugins: [
    { name: 'preset-default', params: { overrides: { cleanupIds: false } } },
  ],
};
```

## Modele wyspecjalizowane w SVG

- **StarVector**: model „obraz lub tekst do kodu SVG”. Ma benchmark SVG-Bench z 10 zbiorami danych i 3 zadaniami: Image-to-SVG, Text-to-SVG, Diagram-to-SVG. Według OmniSVG radzi sobie z ikonami, ale nie z ilustracjami i złożonymi postaciami.
- **OmniSVG** (NeurIPS 2025): zbiór MMSVG-2M, czyli dwa miliony opisanych grafik (ikony, ilustracje, anime). Benchmark MMSVG-Bench. Krytykuje Chat2SVG za kosztowną optymalizację po wygenerowaniu kodu.
- Badawcze podejścia z rozumowaniem (Reason-SVG, SVGThinker, CTRL-S) opisuje [Workflow generowania SVG przez LLM](svg-workflow-llm.md).

## Benchmarki — jak ocenić model do SVG

- **SVGenius**: testuje rozumienie, edycję i generowanie SVG przez LLM.
- **SVGEval** (2026-08): krytykuje metryki, które oceniają tylko wynik rastrowy. Według autorów takie metryki słabo wykrywają błędy geometrii i układu typowe dla SVG.
- **Pelican benchmark** Simona Willisona: prompt „Generate an SVG of a pelican riding a bicycle” na każdym nowym modelu. Sam autor nazywa go „deeply unscientific”. Daje szybki, porównywalny obraz możliwości SVG nowych modeli. Przykład: Gemini 3.1 Pro myślał 323,9 sekundy przed narysowaniem pelikana (wpis z 2026-02-19).

## Jak stosować

Minimalny zestaw do pracy z LLM nad SVG:
1. `brew install librsvg` i `npm i -D svgo`.
2. Pętla: model pisze `out.svg` → `rsvg-convert -w 512 -b white out.svg -o out.png` → model ogląda `out.png` → poprawka.
3. Dla SVG z CSS lub animacją: zrzut ekranu w Playwright zamiast rsvg-convert.
4. Na koniec: `npx svgo --multipass -p 2 out.svg`. Potem render jeszcze raz, żeby sprawdzić, czy optymalizacja niczego nie zniekształciła.

## Zobacz też
- [Workflow generowania SVG przez LLM](svg-workflow-llm.md) — proces generowania krok po kroku
- [Techniki SVG na web — viewBox, prymitywy, dostępność, animacja](svg-techniques.md) — viewBox, dostępność, animacja
