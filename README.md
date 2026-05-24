# Gymbro UX — Design System

Sistema di design unificato per tutte le applicazioni Gymbro.

## Applicazioni coperte
| App | Piattaforma | Stack |
|---|---|---|
| `gymbro-fe` | Web (desktop/mobile) | Next.js 15 + Tailwind CSS |
| `gymbro-screen` | Android TV / desktop | Flutter |
| `gymbro-remote` | iOS / Android | Flutter |

## Contenuto
- [`colors.md`](./colors.md) — Palette colori, variabili CSS, costanti Flutter
- [`typography.md`](./typography.md) — Font, scale tipografica, regole d'uso
- [`spacing.md`](./spacing.md) — Griglia, spaziatura, breakpoint
- [`components.md`](./components.md) — Pattern componenti condivisi
- [`motion.md`](./motion.md) — Animazioni, transizioni, durate
- [`platforms/web.md`](./platforms/web.md) — Note specifiche web
- [`platforms/tv.md`](./platforms/tv.md) — Note specifiche Android TV / gymbro-screen
- [`platforms/mobile.md`](./platforms/mobile.md) — Note specifiche mobile / gymbro-remote

## Principi di design

1. **Comodità prima di tutto** — ogni interazione deve richiedere il minor numero possibile di tap/click. Un istruttore deve poter avviare un timer con 1-2 tap, senza navigare nei menu.
2. **Dark-first** — tutte le app vivono in un ambiente scarsamente illuminato (palestra). Il tema dark è quello predefinito e quello su cui si ottimizza tutto.
3. **Leggibilità a distanza** — specialmente su TV, font grandi, contrasto alto, zero informazioni inutili a schermo.
4. **Feedback immediato** — ogni azione riceve una risposta visiva (e opzionalmente tattile/sonora) entro 100ms.
5. **Consistenza cross-platform** — lo stesso colore, lo stesso font, lo stesso pattern di interazione su tutte e tre le app.
