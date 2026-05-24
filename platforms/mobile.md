# Platform: Mobile (gymbro-remote)

## Stack
- Flutter (iOS / Android)
- Orientamento: portrait (primario), landscape supportato
- Font: Inter (google_fonts)

## Tema
- **Dark only** — stesso tema di gymbro-fe in dark mode
- Nessun light mode per ora (palestre con luce forte → il contrasto dark è comunque superiore con font grandi)

## Autenticazione
- Auth0 (stesso tenant del frontend web)
- Login con `flutter_appauth` o `auth0_flutter`
- Token JWT persistito in `flutter_secure_storage`
- Stesso account usabile su web e mobile

## Modello multi-remote (stile Spotify Connect)

### Concetto
Più utenti dello stesso workspace possono controllare lo stesso schermo contemporaneamente, esattamente come Spotify Connect permette a più dispositivi di controllare la stessa coda musicale.

### Flusso
1. L'utente apre l'app ed è già loggato
2. Vede la lista degli **schermi online** nel suo workspace
3. Sceglie uno schermo (o un gruppo, o "Tutti") come target
4. Da quel momento l'app è in "sessione" con quello schermo:
   - Riceve in tempo reale lo stato del timer dallo schermo
   - Può inviare comandi
5. Un altro utente può fare la stessa cosa sullo stesso schermo → entrambi vedono lo stesso stato, entrambi possono inviare comandi
6. **Last command wins**: se due utenti premono "Start" a 50ms di distanza, il server processa il primo e ignora il secondo (il secondo vedrà che il timer è già avviato)

### "Presa di controllo"
Non c'è un meccanismo di locking, ma il telecomando mostra chi ha inviato l'ultimo comando (nome utente + "X ha avviato il timer"). Questo crea accountability senza burocrazia.

## Struttura schermate

```
/ PairingScreen      → lista schermi workspace, selezione target
/ ControlScreen      → controllo timer in tempo reale
/ ConfigureScreen    → configurazione modalità timer
/ PresetsScreen      → gestione preset WOD
/ SettingsScreen     → impostazioni (vibrazione, audio, feedback, screensaver)
```

## Schermata controllo (ControlScreen) — priorità UX

Layout verticale, da top a bottom:

1. **Connection bar** (32px): `[● verde] Sala Pesi – TV 1  [Cambia]`
2. **Timer display card** (flex 1): grande, colorata, mostra stato live
3. **Azione rapida** (80px):
   - IDLE → `[▶ AVVIA ULTIMO]` (full width, red)
   - RUNNING → `[⏸ PAUSA]` (yellow, 60%) + `[■ STOP]` (red, 40%)
   - PAUSED → `[▶ RIPRENDI]` (green, 60%) + `[■ STOP]` (red, 40%)
4. **Preset veloci** (scroll orizzontale, ~100px): cards dei preset con 1-tap avvio
5. **Modalità** (scroll orizzontale, ~80px): chips TABATA / EMOM / AMRAP / SEMPLICE / STOPWATCH / COUNTDOWN
6. **[+ Configura nuovo]** button

## Timer Position Picker

Accessibile da SettingsScreen o da un pulsante nella ControlScreen:

```
┌─────────────────────────────┐  ← miniatura 16:9
│                             │
│     [TIMER]  ← draggable   │
│                             │
└─────────────────────────────┘
Dimensione: [S] [M] [L] [⬜ Full]
```

- Il widget `[TIMER]` è trascinabile liberamente nel rettangolo
- Le coordinate normalizzate (0–1) vengono inviate al server in real-time durante il drag
- La TV aggiorna la posizione mentre si trascina (latency < 100ms su rete locale)

## Feedback

| Evento | Feedback |
|---|---|
| Comando inviato con successo | Vibrazione leggera (50ms) |
| Timer avviato | Vibrazione doppia (100ms + 200ms) |
| Comando fallito / timeout | Vibrazione lunga (400ms) + toast errore |
| Cambio fase timer (live) | Vibrazione breve (30ms) + cambio colore display |
| Timer finito | Vibrazione pattern "finish" (100+100+300ms) |

Tutto configurabile da SettingsScreen, salvato su MongoDB per account utente.

## Impostazioni (SettingsScreen)

- Vibrazione feedback: on/off + intensità
- Audio beep sul telefono: on/off
- Screensaver schermo TV: off / dopo 5 min / dopo 10 min / dopo 30 min
- Auto-avanzamento round: on/off (default: on)
- Avviso 3s prima del cambio fase: on/off (default: on)
- Posizione e dimensione timer overlay (apre il Timer Position Picker)
- Logout

Tutte le impostazioni vengono salvate su MongoDB (screen-service) legate all'account utente + workspace.
