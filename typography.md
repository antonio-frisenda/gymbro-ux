# Tipografia

## Font

| Piattaforma | Font principale | Font mono |
|---|---|---|
| Web (`gymbro-fe`) | **Geist Sans** (next/font/google) | Geist Mono |
| Flutter (screen / remote) | **Inter** (google_fonts package) | — |

Geist Sans e Inter sono metricamente quasi identici — questa è una scelta intenzionale per mantenere la stessa sensazione tipografica su tutte le piattaforme.

## Scala tipografica

### Web (Tailwind CSS classes)

| Ruolo | Class | Size | Weight |
|---|---|---|---|
| Display / hero | `text-4xl font-bold` | 36px | 700 |
| H1 | `text-3xl font-bold` | 30px | 700 |
| H2 | `text-2xl font-semibold` | 24px | 600 |
| H3 | `text-xl font-semibold` | 20px | 600 |
| Body | `text-base` | 16px | 400 |
| Small / label | `text-sm` | 14px | 400 |
| Micro / caption | `text-xs` | 12px | 400 |

### Flutter (TextStyle)

```dart
// Usare sempre Google Fonts: GoogleFonts.inter(...)

// Timer display — TV, grande distanza
const timerHuge  = TextStyle(fontSize: 140, fontWeight: FontWeight.w800, letterSpacing: -4);
const timerLarge = TextStyle(fontSize: 96,  fontWeight: FontWeight.w800, letterSpacing: -3);
const timerMedium= TextStyle(fontSize: 64,  fontWeight: FontWeight.w700, letterSpacing: -2);

// UI generale
const display    = TextStyle(fontSize: 32,  fontWeight: FontWeight.w700);
const h1         = TextStyle(fontSize: 28,  fontWeight: FontWeight.w700);
const h2         = TextStyle(fontSize: 22,  fontWeight: FontWeight.w600);
const h3         = TextStyle(fontSize: 18,  fontWeight: FontWeight.w600);
const body       = TextStyle(fontSize: 16,  fontWeight: FontWeight.w400);
const small      = TextStyle(fontSize: 14,  fontWeight: FontWeight.w400);
const micro      = TextStyle(fontSize: 12,  fontWeight: FontWeight.w400);

// Badge / label
const label      = TextStyle(fontSize: 11,  fontWeight: FontWeight.w600, letterSpacing: 0.5);
```

## Regole d'uso

- **Mai usare font-weight < 400** su sfondi dark — il testo diventa poco leggibile.
- **Letter-spacing negativo** solo per i numeri del timer (dimensioni >= 64px) — migliora la leggibilità a distanza.
- **Uppercase con `letterSpacing: 1.5`** per label di modo timer (es. "TABATA", "LAVORO", "RIPOSO").
- **Numeri monospaziati**: per il timer usare `fontFeatures: [FontFeature.tabularFigures()]` in Flutter per evitare il "ballo" dei numeri durante il countdown.

## Timer label format

```
// Formato visualizzazione tempo
< 1 ora  →  "MM:SS"        (es. "04:30")
>= 1 ora →  "H:MM:SS"      (es. "1:04:30")
Millisecondi (ultimi 3s) →  "MM:SS.d"  (es. "00:03.2") — opzionale
```
