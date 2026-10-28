---
title: Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru
updated: 2026-10-28
tags: [art-direction, frontend, design, concept, color, typography]
sources:
  - "[leonxlnx/taste-skill — tasteskill v2 SKILL.md](https://github.com/leonxlnx/taste-skill/blob/main/skills/taste-skill/SKILL.md) — unknown — medium"
  - "[pbakaus/impeccable — SKILL.md v4.8.0](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/SKILL.md) — unknown — high"
  - "[pbakaus/impeccable — reference/new-work.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/new-work.md) — unknown — high"
  - "[pbakaus/impeccable — reference/init.md](https://github.com/pbakaus/impeccable/blob/main/.claude/skills/impeccable/reference/init.md) — unknown — high"
---

# Kierunek artystyczny — idea z tematu, tryby strony, strategia koloru

> Strona z modelu wygląda jak średnia wszystkich stron, które model widział. Dwa popularne skille, `taste-skill` i `impeccable`, rozwiązują to tak samo. Najpierw ustalają, czym ta strona jest (tryb, zadanie, odbiorca). Potem budują ideę z rzeczy, które ma tylko ten temat. Dopiero potem wybierają styl. Oba celowo wykluczają domyślny wygląd kategorii i jego przewidywalne przeciwieństwo.

## Tryb strony (impeccable)

Tryb mówi, jak wygląda sukces odwiedzającego. Wybierasz go według ekranu, nie według produktu.

- **Persuade** — odwiedzający decyduje i działa. Landing, marketing, cennik. Pełna odwaga i wyrazisty kierunek.
- **Operate** — odwiedzający wykonuje zadanie. Aplikacja, dashboard, edytor, ustawienia. Czytelność, spójność i znane wzorce są ważniejsze niż ekspresja. Marka żyje w precyzyjnych detalach.
- **Read** — odwiedzający ma coś zrozumieć. Dokumentacja, artykuły, changelog. Struktura pod zrozumienie.
- **Experience** — odwiedzający jest w środku dzieła. Portfolio, galeria. Dzieło prowadzi od pierwszego ekranu, interfejs się chowa.

Landing narzędzia to dalej Persuade. Dokumentacja domu mody to dalej Read. `taste-skill` dzieli prościej: **strona** (czytana i przewijana) albo **ekran aplikacji** (w nim się pracuje). Każdy rodzaj ma własne reguły.

## Idea z tematu (taste-skill)

1. **Inwentarz tematu.** Wypisz 8–12 rzeczy, które ma ten klient i żaden konkurent. Szukaj w nazwie i jej znaczeniu, w adresie i wyglądzie miejsca (płytki, szyldy, kolory, światło), w liczbach z briefu, w ograniczeniu, z którym żyje („jedna partia w miesiącu”), w materiałach, rytuałach i godzinach, w drukach z jego świata (rozkład jazdy, etykieta, bilet).
2. **Argument.** Zanim zaczniesz projektować, rozpisz stronę jako tezy z dowodami, jedna linia na sekcję. Sekcję bez tezy usuń. Tak unikasz standardowej sekwencji hero, logotypy, trzy funkcje, opinia, cennik, CTA.
3. **Zdanie idei.** „Na tej stronie **[coś, co należy do tematu]** staje się **[środkiem, którego wymaga kierunek]**”. Pierwszą lukę wypełniasz z inwentarza. Gdzie szukać: wynik działania produktu, jego kształt, nazwa, miejsce, rytuał, druk z jego świata, przeciwieństwo.
4. **Test konkurenta.** Wstaw do zdania najbliższego konkurenta. Jeśli zdanie dalej działa, idea należy do kategorii, a nie do klienta. „Czysto i nowocześnie” to nie idea.
5. **Jedna żywa rzecz.** Strona ma jedną rzecz, którą odwiedzający może zrobić, zbudowaną z idei i prawdziwych danych. Przykłady: wybierz drewno i zobacz krzesło, ustaw kredyt i przeczytaj prawdziwą ratę. Działa kciukiem na telefonie i ma prosty fallback bez skryptu. Według autorów w ślepych testach każda wygrywająca strona miała taką rzecz.
6. **Słowa przed markupem.** Cała treść jako tekst przed kodem. Nagłówek ma maksymalnie dwie linie na każdej szerokości (około 32 znaki). Mediana hero w badanej galerii to 5 słów i 32 znaki. Pierwszy ekran odpowiada dużą czcionką na pierwsze pytanie odwiedzającego.

Autorzy piszą, że to badanie 247 stron z galerii One Page Love i Awwwards Sites of the Day. Wyniki ślepych testów pochodzą od autorów skilla i nikt ich niezależnie nie sprawdził.

## Kierunek wizualny (impeccable)

1. Nazwij jednym zdaniem unikalny mechanizm produktu. Opisz prawdziwą scenę odbiorcy, jego kulturowy dom i to, co ma udowodnić pierwszy ekran.
2. Nazwij stronę, którą ta kategoria zawsze wypuszcza, i jej przewidywalne przeciwieństwo. Obie to koleina. Żadna nie trafia na listę kandydatów.
3. Ze świata odbiorcy wypisz 7 konkretnych systemów wizualnych, artefaktów, miejsc albo rytuałów, które odbiorca zna na pamięć. Przy każdym dopisz, czemu rezonuje i jak wygląda: tło, główne kolory, głosy typografii, jeden rozpoznawalny znak. Świat odbiorcy obejmuje też jego tradycje graficzne i ekranowe, nie tylko przedmioty.
4. Zamień je w pełne kierunki: świat wizualny połączony z konkretnym pierwszym ekranem.
5. Zawsze zostaw jedną cichą alternatywę: standard kategorii zrobiony porządnie. Wybiera ją tylko człowiek. Model jej nie poleca.

Skille losują kierunek skryptem (`concept-seed` w impeccable, `draw.mjs` w taste-skill), bo model sam wybiera domyślny wygląd kategorii. Bez skryptu ten sam efekt da lista kilku kierunków do wyboru przez człowieka.

## Strategia koloru (impeccable)

Najpierw wybierz strategię, dopiero potem kolory:
- **Restrained** — neutrale podbarwione światem tematu plus jeden akcent. Typowe dla Operate i Read.
- **Committed** — jeden nasycony kolor pokrywa 30–60% powierzchni.
- **Full palette** — 3–4 nazwane role kolorów.
- **Drenched** — powierzchnia sama jest kolorem.

Persuade i Experience mają prawo do odważniejszych strategii. Jasny albo ciemny motyw wybieraj ze sceny użycia: kto, gdzie i przy jakim świetle. Nie wybieraj go według kategorii.

`taste-skill`: jedno tło, jeden tusz, jeden akcent. Akcent jest na akcji i najwyżej na jednej innej rzeczy. Jeśli temat ma własne, jednoznaczne kolory (materiał, farba ulicy, krajobraz), weź proporcje z kierunku, a kolory z tematu.

## Krój pisma

- Operate i Read: systemowe stosy i sprawdzone kroje UI.
- Persuade i Experience: kroje z charakterem, dobrane jak przedmioty ze świata tematu.
- Impeccable wymienia kroje, które znaczą, że „przestałeś szukać”: Fraunces, Playfair Display, Cormorant, Lora, Crimson, Newsreader, Syne, Space Grotesk, Space Mono, IBM Plex, Inter jako display, DM Sans, DM Serif, Outfit, Plus Jakarta Sans, Instrument Sans.
- Impeccable zauważa też skrzywienie modelu: tematy ciepłe, książkowe, rodzinne i dziecięce wychodzą jako kremowe tło, szeryf z kursywą i światło lampy, nawet gdy kierunek tego nie chciał. Taką pierwszą paletę traktuj jako zużytą.

## Jak stosować

Notatka kierunku przed kodem (wypełnij):

```
Tryb: Persuade | Operate | Read | Experience
Mechanizm produktu (1 zdanie):
Odbiorca i jego scena:
Koleina kategorii: [typowa strona] / [jej przeciwieństwo] — obie odpadają
Inwentarz tematu (8–12): ...
Argument: sekcja → teza → dowód (sekcja bez tezy wypada)
Idea: "Na tej stronie [X z tematu] staje się [środek]". Test konkurenta: zdany?
Jedna żywa rzecz:
Strategia koloru: Restrained | Committed | Full palette | Drenched
Krój: [nazwa] — czemu pasuje do świata tematu
```

## Zobacz też
- [Proces projektowania strony z LLM — od pytań do krytyki](design-process.md) — gdzie ta notatka wchodzi w proces (krok 2)
- [Jak uniknąć designu, który wygląda na wygenerowany przez AI](avoiding-ai-slop.md) — czego unikać przy wyborze kierunku
- [Prompty do sterowania estetyką designu](design-prompting.md) — dźwignie sterowania estetyką
- [Katalog popularnych skilli do designu (skills.sh)](design-skills-catalog.md) — skille, z których pochodzą te zasady
