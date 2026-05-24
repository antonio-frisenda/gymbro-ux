# Platform: TV (gymbro-screen)

## Stack
- Flutter (Android TV / desktop)
- Target principale: Android TV (landscape 1920×1080 o 3840×2160)
- Secondary target: desktop connesso alla TV via HDMI

## Principi UX TV

1. **Nessun touch**: tutta la configurazione avviene dal telecomando (gymbro-remote). La TV è un display passivo che riceve comandi.
2. **D-pad**: le uniche interazioni locali (impostazioni startup, config locale) devono essere navigabili con il D-pad del telecomando TV.
3. **Leggibilità a 3+ metri**: font minimo 24px per testo secondario, 48px+ per testo principale.
4. **Safe area**: 48px margin su tutti i lati per l'overscan TV.
5. **Sempre attiva**: l'app non va mai in sleep/screensaver senza autorizzazione esplicita dell'utente.

## Orientamento
- Sempre **landscape** (forza `DeviceOrientation.landscapeLeft/Right` in main.dart)
- `SystemChrome.setEnabledSystemUIMode(SystemUiMode.immersiveSticky)` — no status bar

## Schermata di pairing (primo avvio / disconnesso)
- Fullscreen dark (`#0f172a`)
- Centro: QR code (280×280px) per il Device Authorization Flow Auth0
- Logo Gymbro sopra il QR (o logo del workspace se configurato)
- Sotto il QR: URL corto per login manuale + codice device (es. "Vai su app.gymbro.io/link → inserisci: ABCD-1234")
- In basso a destra: pulsante "Impostazioni" (gear icon) navigabile con D-pad

## Schermata principale (connesso)
- Video / audio in background (fullscreen)
- Timer overlay: posizionabile e ridimensionabile dall'utente tramite drag sul remote
- Top-right: status dot (● verde = remote connesso, ● grigio = nessun remote)
- Top-left: logo (piccolo, 40px height) — nascosto in modalità timer-only
- Nessun altro elemento UI — schermo pulito

## Fallback senza contenuti
Cascata:
1. Logo workspace (se caricato) + sfondo `#0f172a` con gradiente sottile
2. Se no logo workspace: logo Gymbro animato
3. Frasi motivazionali a rotazione (configurabili dall'admin)

## Impostazioni locali (salvate on-device, no DB)
- Avvio automatico all'accensione TV (boot receiver Android — disabilitato se non supportato)
- Porta WebSocket locale (default 4242, solo per debug)
- Mostra/nascondi codice dispositivo nella schermata di pairing

## Timer overlay — posizione e dimensioni
Il server mantiene per ogni schermo:
```json
{
  "timer_position": { "x": 0.5, "y": 0.5 },
  "timer_size": "large",
  "timer_anchor": "center"
}
```
- `x`, `y`: percentuali 0.0–1.0 relative alla viewport (escluso safe area)
- `timer_size`: `"small"` (64px) | `"medium"` (96px) | `"large"` (140px) | `"fullscreen"` (adattivo)
- `timer_anchor`: `"center"` | `"top_left"` | `"bottom_right"` ecc.

## Audio
- Beep timer riproducibili dalla TV (audioplayers package)
- Volume configurabile dall'admin via remote (0–100%)
- Mute automatico durante il countdown finale opzionale (per non sovrapporsi a musica in sala)
- L'audio del video (se presente) è controllabile separatamente via remote

## Connessione al screen-service
- WebSocket persistente a `wss://screen-service.gymbro.io/ws/screen/<screen_id>`
- Token JWT (persistito in secure storage) inviato come header all'handshake
- Auto-reconnect esponenziale: 1s, 2s, 4s, 8s, 16s, 30s (poi ogni 30s)
- In caso di disconnessione: mostra un badge "Riconnessione..." nell'angolo, non interrompe il timer in corso
