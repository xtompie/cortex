---
title: Prompty do sterowania estetyką designu
updated: 2026-10-28
tags: [prompting, frontend, design, claude, skills, design-md]
sources:
  - "[Prompting for frontend aesthetics (Claude Cookbook, Prithvi Rajasekaran)](https://platform.claude.com/cookbook/coding-prompting-for-frontend-aesthetics) — 2025-10-21 — high"
  - "[Improving frontend design through Skills (claude.com)](https://claude.com/resources/articles/improving-frontend-design-through-skills) — 2025-11-12 — high"
  - "[anthropics/skills — frontend-design SKILL.md](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md) — 2026-09-03 — high"
  - "[anthropics/skills — canvas-design SKILL.md](https://github.com/anthropics/skills/blob/main/skills/canvas-design/SKILL.md) — unknown — high"
  - "Claude built-in skill artifact-design — unknown — high"
  - "[rohitg00/awesome-claude-design](https://github.com/rohitg00/awesome-claude-design) — 2026-10-28 — medium"
---

# Prompty do sterowania estetyką designu

> Model ma wiedzę o typografii i kolorze, ale bez kierunku wybiera bezpieczny środek. Działają cztery dźwignie: (1) temat, odbiorca i zadanie strony w briefie, (2) osobne polecenia dla każdego wymiaru (typografia, kolor, ruch, tło), (3) konkretna inspiracja albo ograniczenie motywu, (4) wymuszenie planu i jego przeglądu przed kodem. Wytyczne trzymaj w Skillu albo w pliku design systemu, nie w globalnym system prompcie.

## Hierarchia ważności

Artifact-design ustala kolejność: najpierw słowa użytkownika, potem istniejący design system projektu (CLAUDE.md, plik tokenów, style komponentów), dopiero potem wybory modelu. Wytyczne „anty-slop” wypełniają luki i nigdy nie nadpisują briefu. Jeśli brief prosi o kremowe tło z terakotą — model ma to zrobić.

## Dźwignie

**1. Zakotwicz w temacie.** Podaj jeden konkretny temat, odbiorcę i główne zadanie strony. Przykład ze skilla: zabawka dla dziewczynek 8–11 lat wygląda zupełnie inaczej niż dashboard dla analityków finansowych. Artifact-design dodaje: umieść co najmniej jeden detal, który ma tylko ten temat (prawdziwe jednostki, konwencje dokumentów, terminy branżowe), jako treść, nie ozdobę.

**2. Steruj każdym wymiarem osobno.** Cookbook zaleca kierować uwagę modelu osobno na typografię, kolor, ruch i tło. Każdy wymiar można też zadać izolowanym promptem (cookbook ma osobny `<use_interesting_fonts>`).

**3. Inspiracja bez nadmiernej precyzji.** Cookbook: „Draw from IDE themes and cultural aesthetics for inspiration.” Wskaż źródło (motyw IDE, epokę, ruch artystyczny, materiał), ale nie dyktuj każdego hexa.

**4. Ograniczenie motywu.** Cookbook pokazuje izolowany prompt motywu, np. Solarpunk:

```
<always_use_solarpunk_theme>
Always design with Solarpunk aesthetic:
- Warm, optimistic color palettes (greens, golds, earth tones)
- Organic shapes mixed with technical elements
- Nature-inspired patterns and textures
- Bright, hopeful atmosphere
- Retro-futuristic typography
</always_use_solarpunk_theme>
```

**5. Najpierw filozofia, potem forma (grafika statyczna).** Skill `canvas-design` każe najpierw napisać manifest „ruchu artystycznego” (nazwa w 1–2 słowach, np. „Brutalist Joy”, i 4–6 akapitów o przestrzeni, kolorze, skali, kompozycji, hierarchii), a dopiero potem go wyrazić: 90% wizualnie, 10% tekstu.

**6. Plan i przegląd przed kodem.** Patrz proces w [Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md): tokeny (4–6 kolorów, kroje, layout + ASCII wireframe), przegląd „czy to domyślny wybór?”, dopiero kod, potem zrzuty ekranu.

**7. Pamięć prób.** Skill zauważa, że człowiek pamięta, co już robił, i szuka nowego. Model nie. Notuj wybrane kierunki (np. w pliku projektu), żeby kolejne projekty nie zbiegały do tego samego.

## Gdzie trzymać wytyczne

- **Skill** — ładuje się tylko przy zadaniu frontendowym; tak robi Anthropic (`frontend-design`, około 400 tokenów).
- **CLAUDE.md / AGENTS.md projektu** — cookbook pozwala dopisać prompt estetyczny do system promptu albo CLAUDE.md. Sens ma tylko w repo, które jest głównie frontendem.
- **DESIGN.md** — plik opisujący design system marki (paleta, typografia, komponenty), który Claude Design i agenci czytają jako kontekst. `awesome-claude-design` zbiera takie pliki pogrupowane w 9 „rodzin estetycznych” (editorial minimalism, terminal-core, warm editorial, data-dense pro, cinematic dark, playful color, glass / soft-futurism, neon brutalist, cult / indie). Uwaga: „warm editorial” to dokładnie klaster 1 z [Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md) — dobry jako świadomy wybór, zły jako domyślny.

## Jak stosować

Szablon briefu do wklejenia (uzupełnij nawiasy):

```
Zaprojektuj [stronę/ekran] dla [konkretny temat].
Odbiorca: [kto]. Główne zadanie strony: [jedno zadanie].
Inspiracja: [motyw IDE / epoka / ruch artystyczny / materiał ze świata tematu].
Ograniczenia: [istniejący design system, kolory marki — albo "brak, wybierz sam"].

Zanim napiszesz kod:
1. Plan: 4–6 nazwanych kolorów hex, kroje i ich role (max 2 rodziny),
   koncepcja layoutu w 1 zdaniu + ASCII wireframe, wyrównanie, 2–3 zasady.
2. Przejrzyj plan: co wygląda jak domyślny wybór dla dowolnej podobnej strony
   (krem+terakota, czerń+kwasowy akcent, identyczne karty, Inter/Space Grotesk,
   eyebrow ALL CAPS, fade-in każdej sekcji)? Zmień to i napisz, co zmieniłeś.
3. Jeden element ma być zapamiętywalny. Reszta spokojna.
Potem koduj według planu. Responsywnie do mobile, widoczny focus,
prefers-reduced-motion. Na końcu zrzut ekranu desktop + mobile i jedna
runda poprawek.
```

Wariant „kilka kierunków”: poproś o 3 plany w różnych rodzinach estetycznych (tylko tokeny + wireframe ASCII), wybierz jeden i dopiero go buduj.

## Zobacz też
- [Wytyczne Anthropic do designu frontendu z Claude](anthropic-frontend-design.md) — źródło zasad i pełny proces
- [Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md) — checklista tików do wyłapania po zbudowaniu
- [Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru](art-direction.md) — idea z tematu, tryby strony i strategia koloru ze skilli `taste-skill` i `impeccable`
