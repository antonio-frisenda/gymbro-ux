# Colori

## Palette principale

| Nome | Hex | Uso |
|---|---|---|
| `primary` | `#e11d48` | CTA, accenti, elementi attivi, fase lavoro timer |
| `primary-light` | `#fb7185` | Hover su primary, testo su sfondo scuro |
| `primary-dark` | `#be123c` | Pressed state su primary |
| `bg` | `#0f172a` | Sfondo principale (dark mode) |
| `bg-secondary` | `#1e293b` | Card, sidebar, superfici elevate |
| `border` | `#334155` | Bordi, separatori |
| `text` | `#f1f5f9` | Testo primario |
| `text-muted` | `#94a3b8` | Testo secondario, placeholder, label |
| `success` | `#22c55e` | Operazioni riuscite, stato attivo, fase riposo timer |
| `warning` | `#f59e0b` | Avvisi, ultimi 5 secondi del timer |
| `error` | `#ef4444` | Errori, eliminazioni |
| `info` | `#3b82f6` | Informazioni, link |

## Variabili CSS (gymbro-fe / web)

```css
:root {
  --primary: #e11d48;
  --bg: #ffffff;           /* light mode */
  --bg-secondary: #f8fafc; /* light mode */
  --sidebar-bg: #0f172a;
  --sidebar-text: #94a3b8;
  --sidebar-active: #e11d48;
  --text: #0f172a;         /* light mode */
  --text-muted: #64748b;
  --border: #e2e8f0;
  --card-bg: #ffffff;
}

.dark {
  --bg: #0f172a;
  --bg-secondary: #1e293b;
  --text: #f1f5f9;
  --text-muted: #94a3b8;
  --border: #334155;
  --card-bg: #1e293b;
}
```

## Costanti Flutter (gymbro-screen / gymbro-remote)

```dart
// lib/theme.dart — da usare in entrambe le app Flutter
const kBg          = Color(0xFF0f172a);
const kSurface     = Color(0xFF1e293b);
const kBorder      = Color(0xFF334155);
const kPrimary     = Color(0xFFe11d48);
const kPrimaryLight = Color(0xFFfb7185);
const kPrimaryDark = Color(0xFFbe123c);
const kText        = Color(0xFFf1f5f9);
const kTextMuted   = Color(0xFF94a3b8);
const kSuccess     = Color(0xFF22c55e);
const kWarning     = Color(0xFFf59e0b);
const kError       = Color(0xFFef4444);
const kInfo        = Color(0xFF3b82f6);
```

## Colori contestuali timer

| Stato | Colore | Hex |
|---|---|---|
| Fase lavoro / attivo | `primary` | `#e11d48` |
| Fase riposo | `success` | `#22c55e` |
| Ultimi 5 secondi | `warning` | `#f59e0b` (con pulsazione) |
| Finito | `text-muted` | `#94a3b8` |
| In pausa | `info` | `#3b82f6` |

## Colori brand per workspace

Ogni workspace può avere un `theme_color` (vedi `Settings.brand.primary_color` in `lib/types.ts`). Se impostato, sovrascrive `--primary` solo nelle pagine del workspace. Le app TV e mobile leggono il `theme_color` dal profilo del workspace (servito da `screen-service` o `user-service`) e lo applicano dinamicamente.
