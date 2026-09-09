# Unfold Neo — GitHub Pages build

Statische build van de Unfold Neo-app (versie 20). Werkt zonder buildstap: het is
kant-en-klare HTML/JS die GitHub Pages direct kan serveren.

## Inhoud
- `index.html` — de pagina; mount de app in `#root` en zet `window.NEO_ASSET_BASE`.
- `assets/app.js` — de volledige app (React is meegebundeld).
- `assets/neo/` — de NEO-mascotte-varianten (WebP) + `manifest.json`; deze laden lazy.
- `.nojekyll` — zorgt dat GitHub Pages de bestanden ongemoeid serveert.
- `.github/workflows/deploy.yml` — publiceert automatisch bij push naar `main`.

## Publiceren — makkelijkste manier (Deploy from branch)
1. Maak een nieuwe GitHub-repository (bijv. `unfold-neo`).
2. Zet de **inhoud** van deze map in de **root** van de repo
   (dus `index.html` en `assets/` staan bovenaan, niet in een submap).
3. Push naar `main`.
4. Repo → **Settings → Pages** → *Build and deployment* →
   **Source: Deploy from a branch** → Branch: `main` / **/(root)** → **Save**.
5. Na ~1 minuut staat de site op `https://<gebruiker>.github.io/<repo>/`.

## Publiceren — via Actions (aanbevolen)
Als je de meegeleverde workflow gebruikt: Settings → Pages →
*Source: **GitHub Actions***. De workflow doet de rest bij elke push naar `main`.

## Belangrijk
- De NEO-gezichtsanimaties (knipperen/lachen) en het lazy-loaden van de
  varianten werken alleen via **https** (dus op de gehoste site), niet door
  `index.html` lokaal met `file://` te openen.
- Het lettertype (Space Grotesk) en de foto's komen van internet; een
  internetverbinding is nodig bij eerste gebruik.
