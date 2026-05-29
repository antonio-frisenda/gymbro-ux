# Componenti

Pattern di componenti riutilizzati su più piattaforme.

---

## Button

### Varianti
| Variante | Uso | Colore bg | Colore testo |
|---|---|---|---|
| `primary` | Azione principale, CTA | `#e11d48` | `#f1f5f9` |
| `secondary` | Azione secondaria | `#1e293b` | `#f1f5f9` |
| `ghost` | Azione terziaria, link | transparent | `#e11d48` |
| `danger` | Eliminazione, stop | `#ef4444` | `#f1f5f9` |
| `success` | Conferma, riprendi | `#22c55e` | `#0f172a` |

### Sizing
| Size | Height | Padding H | Font |
|---|---|---|---|
| `sm` | 32px | 12px | 14px |
| `md` | 40px | 16px | 15px |
| `lg` | 48px | 24px | 16px |
| `xl` | 56px | 32px | 18px |

**Regola UX**: i bottoni di azione timer (start/pausa/stop) devono essere almeno `lg` su mobile e `xl` su TV.

### Flutter
```dart
ElevatedButton(
  style: ElevatedButton.styleFrom(
    backgroundColor: kPrimary,
    foregroundColor: kText,
    minimumSize: const Size(double.infinity, 56),
    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
  ),
  onPressed: () {},
  child: Text('AVVIA', style: GoogleFonts.inter(fontSize: 18, fontWeight: FontWeight.w700)),
)
```

---

## Card

```dart
// Flutter
Container(
  padding: const EdgeInsets.all(16),
  decoration: BoxDecoration(
    color: kSurface,
    borderRadius: BorderRadius.circular(12),
    border: Border.all(color: kBorder, width: 1),
  ),
  child: ...,
)
```

```css
/* Web */
.card {
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 16px;
}
```

---

## Badge / Chip (Modo timer)

Badge colorato per identificare la modalità timer. Uppercase, font-weight 600.

| Modo | Colore |
|---|---|
| TABATA | `#e11d48` (primary) |
| EMOM | `#3b82f6` (info) |
| AMRAP | `#f59e0b` (warning) |
| SIMPLE | `#22c55e` (success) |
| STOPWATCH | `#94a3b8` (muted) |
| COUNTDOWN | `#8b5cf6` (viola) |

---

## Status Dot (Connessione)

Dot da 10px + label.

```dart
Row(children: [
  Container(width: 10, height: 10, decoration: BoxDecoration(
    color: isConnected ? kSuccess : kTextMuted,
    shape: BoxShape.circle,
  )),
  const SizedBox(width: 6),
  Text(label, style: GoogleFonts.inter(fontSize: 13, color: kTextMuted)),
])
```

---

## Timer Display

Il componente più importante del sistema. Regole:

1. Il numero deve occupare almeno il 60% dell'altezza dello spazio disponibile.
2. Colore contestuale (vedi `colors.md` — Colori contestuali timer).
3. Usare `fontFeatures: [FontFeature.tabularFigures()]` per evitare il "ballo" dei digit.
4. Pulsazione CSS/Flutter negli ultimi 5 secondi: opacità 1.0↔0.6 ogni 500ms.
5. Il modo e la fase (es. "TABATA • LAVORO") sono sempre visibili sotto il numero.
6. Il contatore dei round (es. "Round 3 / 8") è visibile per TABATA ed EMOM.

---

## Preset Tile

Card cliccabile per avviare rapidamente un WOD salvato.

Struttura:
- Sinistra: `[badge modo] [nome preset]`
- Destra: `[▶ Avvia]` button
- On tap sul corpo: apre la configurazione per modificare
- On tap su "Avvia": `configure` + `start` immediato (1 tap = timer avviato)

---

## Screen Selector

Lista degli schermi disponibili nel workspace, mostrata nel remote prima di inviare comandi.

- Ogni riga: `[● status] [nome schermo] [gruppo]`
- Status: verde = online, grigio = offline
- Selezione multipla: checkbox per broadcast a più schermi
- Gruppi collassabili (es. "Sala Pesi [2 schermi]")

---

## Timer Position Picker (mobile → TV)

Componente drag-and-drop nel remote per posizionare il timer overlay sulla TV.

- Mostra un rettangolo 16:9 in miniatura (aspect ratio TV)
- Dentro c'è un widget draggable che rappresenta il timer
- Al termine del drag: invia `{ type: "set_timer_position", x: 0.35, y: 0.7 }` al server
- Separato: size picker con 4 opzioni (Small / Medium / Large / Fullscreen)
- L'anteprima si aggiorna in real-time mentre si trascina

---

## Gymbro Logo & Background

### Modalità sfondo (configurabile per schermo)
| Modalità | Descrizione |
|---|---|
| `gymbro_logo` | Logo Gymbro animato su sfondo `#0f172a` (default) |
| `custom_logo` | Logo della palestra (PNG/SVG, max 512KB, S3/MinIO) |
| `solid_color` | Colore a tinta unita — color picker libero |
| `phrases` | Frasi motivazionali a rotazione: predefinite dal sistema + custom dell'admin |
| `video` | Video/audio da playlist, timer in overlay |

Il timer viene mostrato sopra qualsiasi modalità di sfondo. In modalità `video`, il timer è un overlay posizionabile. Nelle altre modalità il timer occupa il centro dello schermo (o la posizione configurata).

### Frasi motivazionali predefinite (IT)
```
"Non mollare."
"Ogni rep conta."
"La fatica di oggi è la forza di domani."
"Spingi oltre i tuoi limiti."
"Il corpo ottiene ciò che la mente crede."
"Sii più forte di ieri."
"Il dolore è temporaneo. La gloria è eterna."
"Forza. Disciplina. Risultati."
```
L'admin può aggiungere frasi custom dalla sezione Impostazioni del remote.
