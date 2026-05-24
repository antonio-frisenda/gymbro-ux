# Platform: Web (gymbro-fe)

## Stack
- Next.js 15 (App Router)
- Tailwind CSS v4
- Font: Geist Sans / Geist Mono (next/font/google)

## Tema
- Supporta dark/light mode via classe `.dark` su `<html>`
- Default: dipende dalla preferenza di sistema (`prefers-color-scheme`)
- Toggle manuale salvato in localStorage

## Layout
- Sidebar fissa a sinistra (240px) con sfondo `#0f172a`
- Content area: `flex-1`, sfondo `var(--bg)`
- Header: 64px, sfondo `var(--bg)`, bordo bottom `var(--border)`

## Responsive
- Mobile (< 768px): sidebar collassata, bottom nav
- Tablet (768–1024px): sidebar a icone
- Desktop (> 1024px): sidebar completa

## Link al codice
- Variabili colore: `gymbro-fe/app/globals.css`
- Tipi dati: `gymbro-fe/lib/types.ts`
- API client: `gymbro-fe/lib/api.ts`
