# Spaziatura e Layout

## Unità base: 4px

Tutta la spaziatura è multiplo di 4px.

| Token | px | Tailwind | Flutter |
|---|---|---|---|
| `xs` | 4 | `p-1` / `gap-1` | `4.0` |
| `sm` | 8 | `p-2` / `gap-2` | `8.0` |
| `md` | 16 | `p-4` / `gap-4` | `16.0` |
| `lg` | 24 | `p-6` / `gap-6` | `24.0` |
| `xl` | 32 | `p-8` / `gap-8` | `32.0` |
| `2xl` | 48 | `p-12` / `gap-12` | `48.0` |
| `3xl` | 64 | `p-16` / `gap-16` | `64.0` |

## Border radius

| Token | px | Tailwind | Flutter |
|---|---|---|---|
| `sm` | 4 | `rounded` | `BorderRadius.circular(4)` |
| `md` | 8 | `rounded-lg` | `BorderRadius.circular(8)` |
| `lg` | 12 | `rounded-xl` | `BorderRadius.circular(12)` |
| `xl` | 16 | `rounded-2xl` | `BorderRadius.circular(16)` |
| `full` | 9999 | `rounded-full` | `BorderRadius.circular(999)` |

## Breakpoint web

| Nome | Width | Uso |
|---|---|---|
| `sm` | 640px | Mobile landscape |
| `md` | 768px | Tablet |
| `lg` | 1024px | Desktop small |
| `xl` | 1280px | Desktop |
| `2xl` | 1536px | Desktop large / TV web |

## Layout TV (gymbro-screen)

- **Safe area**: 48px su tutti i lati (overscan TV standard)
- **Timer overlay**: posizionabile dall'utente tramite drag sul telecomando (coordinate 0.0–1.0 relative alla viewport, salvate su DB)
- **Dimensioni timer supportate**: Small (font 64px), Medium (font 96px), Large (font 140px), Fullscreen (font adattivo)

## Layout Mobile (gymbro-remote)

- Margin orizzontale: 16px
- Bottom safe area: rispettare sempre `MediaQuery.of(context).padding.bottom`
- Altezza barra di controllo rapido (bottom sheet fisso): 120px + safe area
