# Animazioni e Motion

## Principi

- **Funzionale, non decorativa**: ogni animazione ha uno scopo (feedback, transizione di stato, attirare l'attenzione).
- **Veloce**: durate brevi. L'utente non aspetta le animazioni.
- **Respect system preferences**: rispettare `prefers-reduced-motion` su web e `AccessibilityFeatures.disableAnimations` su Flutter.

## Durate standard

| Token | ms | Uso |
|---|---|---|
| `instant` | 0–50 | Feedback tap, aggiornamenti dati in tempo reale |
| `fast` | 100–150 | Hover, focus, piccoli cambi di stato |
| `normal` | 200–300 | Transizioni di componenti, apertura menu |
| `slow` | 400–500 | Transizioni di pagina, modal, bottom sheet |

## Easing

```dart
// Flutter
const fastOut = Curves.easeOutCubic;   // elementi che escono
const fastIn  = Curves.easeInCubic;    // elementi che entrano velocemente
const smooth  = Curves.easeInOutCubic; // transizioni bilanciate
```

```css
/* Web */
--ease-out:   cubic-bezier(0.16, 1, 0.3, 1);
--ease-in:    cubic-bezier(0.7, 0, 0.84, 0);
--ease-inout: cubic-bezier(0.87, 0, 0.13, 1);
```

## Timer — animazioni specifiche

### Pulsazione "ultimi 5 secondi"
```dart
// Flutter — AnimationController loop
AnimationController(duration: const Duration(milliseconds: 500), vsync: this)
  ..repeat(reverse: true);
// Opacity: 1.0 ↔ 0.5
// Scale: 1.0 ↔ 1.05 (solo Large/Fullscreen)
```

### Cambio fase (lavoro → riposo)
- Colore del timer: transizione di 300ms da `kPrimary` a `kSuccess`
- Scale: 1.0 → 1.1 → 1.0 (200ms bounce)

### Cambio round
- Flash bianco (opacity 0.3) per 150ms sull'intero overlay

### Timer finito
- "TIME!" appare con scale 0.5 → 1.2 → 1.0 in 400ms
- Colore: `kPrimary` → bianco → `kPrimary`

## Transizioni di pagina (Flutter)

```dart
// Tutte le navigazioni usano FadeTransition
PageRouteBuilder(
  transitionDuration: const Duration(milliseconds: 250),
  pageBuilder: (_, __, ___) => TargetPage(),
  transitionsBuilder: (_, animation, __, child) =>
    FadeTransition(opacity: animation, child: child),
)
```
