---
title: Workflow generowania SVG przez LLM
updated: 2026-10-28
tags: [svg, llm, workflow, prompting]
sources:
  - "[Chat2SVG: Vector Graphics Generation with LLMs and Image Diffusion Models (CVPR 2025)](https://arxiv.org/abs/2411.16602) — 2024-11-25 — high"
  - "[Reason-SVG: Enhancing Structured Reasoning for Vector Graphics Generation with RL](https://arxiv.org/abs/2505.24499) — 2025 — high"
  - "[SVGThinker: Instruction-Aligned and Reasoning-Driven Text-to-SVG Generation](https://arxiv.org/abs/2509.24299) — 2025 — high"
  - "[CTRL-S: Reliable Reasoning in SVG-LLMs via Multi-Task Multi-Reward RL](https://arxiv.org/abs/2603.16189) — 2026-03 — high"
  - "[IntroSVG: Rendering Feedback for Text-to-SVG via Introspective Generator–Critic](https://arxiv.org/abs/2603.09312) — 2026-03 — medium"
  - "Claude built-in skill artifact-diagramming (wbudowany skill Claude Code, Anthropic) — unknown — high"
  - "[Generating SVG Graphics with AI — Botmonster](https://botmonster.com/web-dev/generating-svg-graphics-with-ai/) — unknown — low"
  - "[pbakaus/impeccable — reference/new-work.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/new-work.md) — unknown — high"
---

# Workflow generowania SVG przez LLM

> LLM robi dobre SVG, gdy najpierw planuje obraz słowami, a dopiero potem pisze kod. Plan to: obiekty, ich części, układ na siatce i współrzędne. Kod buduje z prostych kształtów (`rect`, `circle`, `ellipse`, `line`, `polygon`), a krzywe Béziera dodaje na końcu i tylko tam, gdzie trzeba. Potem renderuje obraz do PNG, ogląda go i poprawia w pętli.

## Dlaczego nie od razu ścieżki

- Pisanie `path d="..."` od razu to zgadywanie liczb bez podglądu. Model myli się w krzywych, proporcjach i nakładaniu kształtów.
- Chat2SVG (CVPR 2025) opiera się na tej obserwacji. LLM najpierw tworzy szablon z prostych kształtów. Autorzy piszą, że taki szablon daje regularne kształty, bo każdy element odpowiada jednej części semantycznej obiektu.
- Botmonster radzi w diagramach zabronić złożonych ścieżek i pozwolić tylko na `rect`, `circle`, `line`, `text` i `g`.
- Wytyczne Anthropic do diagramów mówią to samo: długie dane ścieżek dekoracyjnych to znak, że rysunek wymaga prawdziwego narzędzia graficznego. Wtedy należy uprościć rysunek.

## Etapy (co mówią badania)

Kilka niezależnych prac z lat 2024–2026 dochodzi do tego samego schematu: „najpierw rozumowanie, potem kod”.

1. **Chat2SVG**: rozwinięcie promptu na trzech poziomach. Poziom sceny to obiekty, poziom obiektu to części (np. części ciała lwa), poziom układu to pozycje, rozmiary i kolory. Potem kod z prostych kształtów. Potem „visual rectification”, czyli pętla: render, ocena, poprawka.
2. **Reason-SVG**: „Drawing-with-Thought” ma sześć kroków. Szkic koncepcji, plan płótna, rozkład na kształty, obliczenie współrzędnych, styl i kolor, złożenie całości.
3. **CTRL-S (2026)**: plan kroków rysowania przed kodem. Każdy krok planu odpowiada jednej grupie `<g>` w kodzie.
4. **SVGThinker**: uczy model jawnego rozumowania przed kodem. Autorzy piszą, że to zmniejsza błędy i halucynacje.
5. **IntroSVG (2026)**: generator pisze szkic SVG, krytyk ocenia render i podaje sugestie, a generator pisze wersję końcową.

Te prace trenują własne modele. Sam schemat działa też jako prompt dla ogólnego modelu, np. Claude'a: plan, prymitywy, render, poprawka.

## Proces krok po kroku

1. **Brief**: co przedstawia obraz, gdzie trafi (ikona 24×24, ilustracja hero, diagram), styl (linia lub wypełnienie, grubość obrysu, paleta).
2. **Plan sceny**: lista obiektów, a każdy obiekt rozbity na części.
3. **Siatka i układ**: ustal `viewBox` (np. `0 0 24 24` dla ikony, `0 0 800 450` dla ilustracji). Rozpisz pozycje i rozmiary każdej części w liczbach całkowitych lub na siatce co 4 albo 8 jednostek.
4. **Kod z prymitywów**: każda część to `rect`, `circle`, `ellipse`, `line`, `polyline` lub `polygon`, w nazwanej grupie `<g id="...">`.
5. **Render i ocena**: wyrenderuj do PNG (patrz [Narzędzia SVG — render, optymalizacja, modele i benchmarki](svg-tools.md)) i obejrzyj. Sprawdź proporcje, nakładanie, czytelność w docelowym rozmiarze. Nie pomijaj tego kroku. `impeccable` ostrzega, że modele systematycznie uważają swoje odtworzenie obrazu w HTML, CSS albo SVG za udane, choć takie nie jest. Oceniaj render, nie kod.
6. **Poprawki**: jedna poprawka na jeden konkretny problem. Botmonster: większość diagramów potrzebuje od jednej do trzech iteracji.
7. **Detale**: dopiero teraz zamień wybrane prymitywy na `path` z krzywymi. Tylko tam, gdzie kształt tego wymaga.
8. **Wykończenie**: dostępność, `currentColor`, optymalizacja SVGO (patrz [Techniki SVG na web — viewBox, prymitywy, dostępność, animacja](svg-techniques.md)).

## Jak stosować

Prompt do skopiowania:

```text
Narysuj SVG: <opis>. Przeznaczenie: <ikona 24x24 / ilustracja 800x450 / diagram>.
Styl: <np. linia 2px, zaokrąglone końce, currentColor, bez gradientów>.

Pracuj etapami i pokaż każdy:
1. Plan: wypisz obiekty i ich części.
2. Układ: viewBox i tabela części — x, y, szerokość, wysokość lub promień, w liczbach całkowitych na siatce co 4.
3. Kod: najpierw tylko rect, circle, ellipse, line, polyline, polygon. Każda część w osobnym <g id="nazwa">.
   Używaj path tylko tam, gdzie kształtu nie da się złożyć z prymitywów.
4. Sprawdzenie: wyrenderuj do PNG, obejrzyj i wypisz konkretne błędy (proporcje, nakładanie, puste miejsca).
   Popraw po jednym błędzie naraz.
5. Na końcu: role="img" i aria-label (albo aria-hidden="true", jeśli grafika jest dekoracyjna).
```

Checklista oceny renderu:
- Czy obiekt da się rozpoznać w docelowym rozmiarze (np. 24 px)?
- Czy części stykają się tam, gdzie powinny? Brak szpar i przypadkowych nakładań?
- Czy grubości obrysu są równe w całym zestawie?
- Czy grafika jest czytelna na jasnym i ciemnym tle?

## Zobacz też
- [Techniki SVG na web — viewBox, prymitywy, dostępność, animacja](svg-techniques.md) — viewBox, prymitywy kontra ścieżki, dostępność, animacja
- [Narzędzia SVG — render, optymalizacja, modele i benchmarki](svg-tools.md) — render do PNG, SVGO, modele i benchmarki SVG
