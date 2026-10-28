---
title: Spec-driven development (SDD)
updated: 2026-10-28
tags: [sdd, spec, planning, agents, workflow]
sources:
  - "[Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl (Birgitta Böckeler, martinfowler.com)](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) — 2025-10-15 — high"
  - "[Thoughtworks Technology Radar — Spec-driven development](https://www.thoughtworks.com/radar/techniques/spec-driven-development) — 2025-11-05 — high"
  - "[Thoughtworks Technology Radar — GitHub Spec Kit](https://www.thoughtworks.com/radar/languages-and-frameworks/github-spec-kit) — 2026-04-15 — high"
  - "[Spec-Driven Development as Prescribed and as Practiced (Agarwal, Singhal, Macvean, Vasilescu, Breaux, arXiv 2608.25202)](https://arxiv.org/abs/2608.25202) — 2026-10-15 — high"
  - "[Spec-Driven Test Generation (Tufano et al., Google, arXiv 2608.17177)](https://arxiv.org/abs/2608.17177) — 2026-08-17 — high"
---

# Spec-driven development (SDD)

> SDD to praca, w której przed kodem powstaje spec: opis, co ma działać i jak to sprawdzić. Spec jest źródłem prawdy dla człowieka i dla agenta. Badanie z 2026 roku mówi, że agenci działają wtedy pewniej, ale planowanie i review kosztują więcej. Krytycy ostrzegają przed lawiną plików markdown i przed ciężkim procesem przy małych zadaniach.

## Trzy poziomy SDD (Böckeler)

- **Spec-first** — spec powstaje przed kodem i służy do jednego zadania. Potem można go wyrzucić.
- **Spec-anchored** — spec zostaje po zadaniu. Służy do dalszego rozwoju i utrzymania funkcji.
- **Spec-as-source** — spec jest głównym źródłem na stałe. „The human never touches the code.”

Jak Böckeler ocenia narzędzia (październik 2025):
- Kiro „seems to be mostly spec-first”.
- Spec Kit traktuje spec jako „a living artifact for the lifetime of a change request”. Spec żyje tyle co zmiana, nie tyle co funkcja.
- Tessl jako jedyny „explicitly aspires to a spec-anchored approach”.

Szczegóły narzędzi: [Narzędzia SDD — Spec Kit, OpenSpec, Kiro, BMAD, Tessl](sdd-tools.md).

## Krytyka

Böckeler:
- „I'd rather review code than all these markdown files”.
- Kiro przy małym bugu było „like using a sledgehammer to crack a nut”.
- Agenci i tak ignorowali instrukcje ze speca, np. tworzyli zduplikowane klasy.
- Spec-anchored i spec-as-source „might end up with the downsides of both MDD and LLMs”.
- Termin jest „already semantically diffused”. Każdy rozumie go trochę inaczej.

Thoughtworks Technology Radar:
- Technika SDD weszła na pierścień **Assess** w listopadzie 2025 (Vol 33).
- „The workflows remain elaborate and opinionated”.
- „Some generate lengthy spec files that are hard to review”.
- „Handcrafting detailed rules for AI ultimately doesn't scale”.
- Vol 34 (kwiecień 2026) widzi „two broad camps”: minimum struktury kontra „defined workflows and detailed specifications”.

## Dowody empiryczne

**Agarwal i in., „Spec-Driven Development as Prescribed and as Practiced” (2026).**
- Dane: wywiady z 21 praktykami, analiza Reddita i 470 795 plików spec z 73 030 repozytoriów (zbiór SpecMine).
- Ludzie używają SDD głównie przy nowych funkcjach.
- Agenci działają pewniej. Planowanie i review kosztują więcej.
- Specy często zawierają szczegóły implementacji. Przez to szybko się starzeją.

**Tufano i in., Google (2026).** Badali generowanie testów ze speca, nie samo SDD. Testy ze speca znalazły o 9,8 pp więcej bugów (p=0,0352) i dały +2,5 pp pokrycia gałęzi.

## Kiedy SDD, a kiedy nie

- **Mały bug, jasna zmiana** — bez pełnego SDD. Wystarczy krótki plan w czacie. Narzędzia mają tryby lekkie: Quick Spec w Kiro, rozszerzenie bug w Spec Kit, „right-sized process” w BMAD.
- **Funkcja w istniejącym repo** — lekki spec zmiany (OpenSpec, Spec Kit). Radar pisze, że zespoły Thoughtworks używają Spec Kit „mostly in brownfield environments”.
- **Duża nowa funkcja z wieloma decyzjami** — pełny cykl: wymagania, design, zadania, implementacja, sprawdzenie zgodności ze specem.

## Jak stosować

1. Pisz w specu intencję i kryteria akceptacji, nie implementację. Szczegóły implementacji przyspieszają starzenie speca (Agarwal i in.).
2. Wymagania pisz sprawdzalnie. Dobre wzory: EARS „WHEN [warunek] THE SYSTEM SHALL [zachowanie]” (Kiro) albo SHALL + scenariusze WHEN/THEN (OpenSpec).
3. Przejrzyj spec, zanim agent zacznie kod. Spec jest tańszy w poprawce niż kod.
4. Trzymaj spec krótki. Jeśli nie chcesz go czytać, agent i tak go nie wykona dobrze. To wniosek Cortexu z krytyki Böckeler i Radaru.
5. Z kryteriów akceptacji wyprowadź testy. Testy ze speca znajdują więcej bugów (Tufano i in.).
6. Po implementacji sprawdź kod ze specem w osobnym kroku: `/speckit.converge`, `/opsx:verify` albo review w świeżym kontekście ([Review kodu od agenta — świeży kontekst, dowody, czytanie kodu](agent-code-review.md)).

## Zobacz też
- [Narzędzia SDD — Spec Kit, OpenSpec, Kiro, BMAD, Tessl](sdd-tools.md) — Spec Kit, OpenSpec, Kiro, BMAD, Tessl i jak wybrać
- [Plan → kod → review — jak zrobić zadanie z agentem kodującym](plan-code-review.md) — SDD to cięższa wersja kroku „plan”
- [Context engineering dla agentów kodujących](context-engineering.md) — spec jako trwały kontekst między sesjami
