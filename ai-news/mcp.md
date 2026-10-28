---
title: Model Context Protocol (MCP) — stan 2026
updated: 2026-10-28
tags: [mcp, protocol, agents, tools]
sources:
  - "[MCP Blog — The 2026-07-28 Specification](https://blog.modelcontextprotocol.io/posts/2026-07-28/) — 2026-07-28 — high"
  - "[Claude blog — MCP 2026-07-28 spec: stateless core, coming to Claude](https://claude.com/blog/bringing-mcp-2026-07-28-to-claude) — 2026 — high"
  - "[AAIF — MCP 2026-07-28: From Local Tool to Distributed Protocol](https://aaif.io/blog/mcp-2026-07-28-whats-changing-and-how-to-migrate) — 2026 — high"
  - "[Cloudflare — The next generation of MCP](https://blog.cloudflare.com/mcp-v2/) — 2026 — high"
  - "[Google Developers Blog — MCP Stateless updates](https://developers.googleblog.com/scaling-ai-agent-infrastructure-with-the-mcp-stateless-updates/) — 2026 — high"
  - "[Medium — MCP Isn't Dying. It's Being Squeezed From Three Sides](https://medium.com/@visrow/mcp-isnt-dying-it-s-being-squeezed-from-three-sides-in-2026-7017c17eb697) — 2026-10 — low"
  - "[modelcontextprotocol/servers — GitHub](https://github.com/modelcontextprotocol/servers) — 2026-10-28 — high"
---

# Model Context Protocol (MCP) — stan 2026

> MCP to standard, przez który agenci łączą się z narzędziami i danymi. Największa zmiana roku to specyfikacja **2026-07-28**. Protokół przeszedł z trybu stanowego i dwukierunkowego na bezstanowy model żądanie–odpowiedź. Zniknął handshake `initialize`. Serwery MCP mogą teraz działać na serverless i edge. Starsze wersje protokołu mają 12 miesięcy do wycofania.

## Specyfikacja 2026-07-28

- Release candidate zamrożono 2026-05-21. Wersja finalna wyszła 2026-07-28.
- **Bezstanowy rdzeń.** Nie ma `initialize`. Możliwości serwera klient odkrywa na żądanie przez RPC `server/discover`.
- Multi Round-Trip Requests, routing po nagłówkach, cache'owalne wyniki list.
- **Formalny framework rozszerzeń.** MCP Apps i Tasks są teraz wersjonowanymi rozszerzeniami.
- **Wycofane:** sampling i roots.
- **Autoryzacja** zaostrzona i zgodna z OAuth 2.1 i OpenID Connect.
- Nowe SDK pierwszego rzędu: TypeScript, Python, Go, C#. Ruby SDK osiągnął 1.0.0.
- Wsparcie ogłosiły Claude, Google i Cloudflare. U Cloudflare serwer MCP mieści się w jednym Workerze.

## Ekosystem

- Anthropic podaje ponad 400 mln pobrań SDK miesięcznie, 4 razy więcej niż rok wcześniej. Inne źródło podaje 97 mln. Liczby się różnią.
- Według jednej analizy oficjalny rejestr miał 9 652 wpisy w kwietniu 2026.
- Bezpieczeństwo: niezależne skany znajdują podatności w dużej części publicznych serwerów. NSA i CISA wydały formalne wytyczne.
- Dyskusja z października 2026: MCP nie umiera, ale konkurują z nim Code Mode, Skills, UTCP i WebMCP. To źródło niskiej wiarygodności, ale dobrze pokazuje kierunek: przy prostych zadaniach skille i kod zastępują serwery MCP.

## Jak stosować

- Piszesz własny serwer MCP? Celuj w specyfikację 2026-07-28 i bezstanowy rdzeń. Wtedy zadziała na serverless.
- Masz stare serwery na `initialize`? Masz czas do około lipca 2027.
- Zanim podłączysz publiczny serwer MCP, sprawdź autora i uprawnienia. Wiele serwerów ma luki.
- Gdy wystarczy instrukcja i skrypt, skill bywa prostszy niż serwer MCP.

## Zobacz też
- [n8n — automatyzacja workflow z AI](n8n.md) — n8n jako klient i serwer MCP
- [Agenci kodujący — krajobraz (październik 2026)](coding-agents.md) — klienci MCP
