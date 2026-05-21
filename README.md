# GoVity Legal Pages

Statische HTML-Seiten für Privacy Policy, Impressum und AGB von GoVity.

Live-URL nach GitHub-Pages-Setup:
**https://mauricetrogant-dot.github.io/govity-legal/**

## Setup (einmalig, ~5 Min)

### 1. Daten im Impressum eintragen

Öffne `impressum.html` und ersetze die Platzhalter:
- `[DEIN_VOLLER_NAME]`
- `[STRASSE_HAUSNUMMER]`
- `[PLZ_STADT]`
- `[DEINE_EMAIL]`

### 2. GitHub-Repository anlegen

```bash
cd govity-legal
git init
git add .
git commit -m "Initial legal pages"
git branch -M main

# Repo auf github.com/mauricetrogant-dot/govity-legal anlegen (public!)
git remote add origin https://github.com/mauricetrogant-dot/govity-legal.git
git push -u origin main
```

### 3. GitHub Pages aktivieren

1. Auf github.com → Repository `govity-legal`
2. Settings → Pages
3. Bei **Source**: "Deploy from a branch"
4. Branch: `main`, Folder: `/ (root)`
5. Save

Nach 1-2 Minuten ist die Seite unter
**https://mauricetrogant-dot.github.io/govity-legal/** erreichbar.

### 4. URLs zum Hinterlegen

Diese drei URLs brauchst du für Apple/Google:

- **Privacy Policy URL**: `https://mauricetrogant-dot.github.io/govity-legal/privacy.html`
- **Terms of Service URL**: `https://mauricetrogant-dot.github.io/govity-legal/terms.html`
- **Impressum URL**: `https://mauricetrogant-dot.github.io/govity-legal/impressum.html`

## Später bei eigener Domain

Sobald `govityapp.de` oder `govityapp.de` registriert ist:

1. CNAME-Datei zum Repo hinzufügen mit Inhalt `legal.govityapp.de`
2. DNS bei deinem Domain-Provider: CNAME `legal` → `mauricetrogant-dot.github.io`
3. Settings → Pages → Custom domain: `legal.govityapp.de`

Dann sind die URLs:
- `https://legal.govityapp.de/privacy.html`

## Update-Workflow

Texte ändern → committen → pushen. GitHub Pages deployt automatisch.

```bash
git add privacy.html
git commit -m "Update privacy policy: add new third party"
git push
```

## Wichtig: Sicherheit

Dieses Repo ist **public** und enthält absichtlich nur:
- 4 HTML-Dateien (Legal-Texte)
- Diese README

**Keine** App-Code, **keine** API-Keys, **keine** Passwörter. Daher unproblematisch öffentlich.

Deine **App-Repos** (`movematch-backend`, `movematch_frontend` — wie auch immer du sie umbenennst) bleiben **privat**.
