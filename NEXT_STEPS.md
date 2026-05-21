# GoVity — Nächste Schritte

## ✅ Erledigt
- Name finalisiert: **GoVity** (sprich: „Go-Vity")
- Tagline: **„Go for Activity"**
- Bundle-ID festgelegt: `com.govity.app`
- Legal-Pages (HTML) erstellt
- Marketing-Texte erstellt (inkl. TikTok/Instagram-Vorlagen + Mail-Templates)
- Code-Rename-Anleitung erstellt

## 🎯 Heute (~30 Min)

### 1. Domain-Verfügbarkeit prüfen + reservieren (10 Min)

Geh auf **`inwx.de`** oder **`netcup.de`** und prüfe in dieser Reihenfolge:

| Domain | Wenn frei | Was sie kostet |
|---|---|---|
| `govityapp.de` | ✅ NEHMEN | ~5€/Jahr |
| `govityapp.de` | ✅ NEHMEN (zusätzlich) | ~10€/Jahr |
| `govity.app` | ⚠️ Optional | ~25€/Jahr |

**Mindestens `govityapp.de` reservieren.** Das ist deine wichtigste Domain, weil DACH-Markt = `.de` ist Standard.

Falls `govityapp.de` schon weg ist (sehr unwahrscheinlich): probier `govityapp.de`. Falls auch das weg ist: schick mir einen Screenshot, dann gucken wir Plan B.

### 2. App-Icon-Update (15 Min)

**Frage an dich:** Möchtest du das M behalten oder zu G ändern?

**Optionen:**
- **A) M behalten**: stilistisch von „Move" (jeder Move ist eine Aktivität in GoVity)
- **B) Zu G wechseln**: passt besser zum Namen GoVity, klares Branding
- **C) Beides ausprobieren**: ChatGPT generiert beide Varianten, du wählst

**Mein Vorschlag: Option B (G im Pin)** — passt visuell perfekt zum Namen GoVity.

Hier die ChatGPT-Prompts für beide Varianten:

#### Prompt für Variante B (G — empfohlen)

```
Create a 1024x1024 mobile app icon, square format, no transparency, no rounded corners (the operating system applies them automatically).

Background: solid diagonal gradient from bright purple #7C3AED in the top-left corner to deep dark purple #4C1D95 in the bottom-right corner (135 degree angle). The gradient must reach all four edges with no padding.

Centered foreground: a single white location pin shape (the classic Google Maps pin silhouette — round top with a triangular point at the bottom). The pin fills approximately 75% of the icon height, perfectly centered both horizontally and vertically. The pin is solid white, no outline, no inner shadow.

Inside the pin, centered in the round upper portion: a bold uppercase letter G in deep dark purple #4C1D95. The G must be a clean, classic, geometric design — like in modern brand logos (think Material Design, geometric weight, similar to the G in "Google" or "Grab"). The G takes up about 60% of the pin's interior space.

Style: completely flat design. No drop shadows, no glow effects, no bevel, no 3D, no texture, no noise. Sharp clean edges everywhere.

No text, no letters, no words anywhere outside the pin shape.

The result must work as a recognizable mobile app icon when scaled down to 60x60 pixels on a phone home screen.
```

Speichere das Resultat als `govity_icon_1024.png`.

### 3. Impressum-Daten eintragen (5 Min)

Öffne `impressum.html` in einem Editor und ersetze:
- `[DEIN_VOLLER_NAME]`
- `[STRASSE_HAUSNUMMER]`
- `[PLZ_STADT]`
- `[DEINE_EMAIL]`

## 📋 Diese Woche

### 4. GitHub-Repo `govity-legal` anlegen + GitHub Pages aktivieren (10 Min)

```powershell
cd Pfad\zum\Ordner\govity-legal
git init
git add .
git commit -m "Initial legal pages"
git branch -M main
# Auf github.com → New Repository: "govity-legal", Public ✓
git remote add origin https://github.com/mauricetrogant-dot/govity-legal.git
git push -u origin main
```

Dann auf github.com:
- Settings → Pages → Source: "Deploy from a branch", Branch: `main`, Save

Nach ~1-2 Min ist `https://mauricetrogant-dot.github.io/govity-legal/` live.

### 5. Google Play Developer Account anlegen (10 Min + 1-3 Tage Wartezeit)

`https://play.google.com/console/signup`

**Wichtig bei der Anmeldung:**
- Account-Typ: **Personal/Privatperson**
- **Developer name (Anzeigenamen): „GoVity"** ← so steht es im Store
- $25 einmalig (Kreditkarte oder PayPal)
- Identitätsnachweis (Personalausweis-Scan)
- Verifikation dauert 1-3 Werktage

Während der Wartezeit machen wir Code-Anpassung, Icon-Integration, Screenshots.

### 6. Code umbennen (siehe `CODE_RENAME.md`)

- Bundle-ID: `com.govity.app`
- App-Name: „GoVity"
- Pubspec, AndroidManifest, Info.plist
- Alle Dart-Dateien: „MoveMatch" → „GoVity", „movematch" → „govity"
- Backend Mail-Templates anpassen

### 7. App-Icon ins Flutter-Projekt einbinden

Wir nutzen `flutter_launcher_icons` Plugin. Detail-Anleitung gibt's wenn dein Code-Rename fertig ist.

### 8. Screenshots für den Store erstellen

Google Play braucht:
- **Telefon-Screenshots:** 2-8 Stück, 1080x1920 oder 1440x2560 Pixel
- **Tablet-Screenshots (optional):** auch sinnvoll
- **Feature-Grafik:** 1024x500 Pixel — ein Werbe-Banner

Wir machen das wenn du die App umbenannt hast und in der App „GoVity" steht.

### 9. AAB statt APK bauen + signieren

Für den Store-Upload brauchst du einen **AAB** (Android App Bundle), nicht APK. Plus einen **Signing-Key**, den du sicher aufbewahren musst (Verlust = du kannst nie mehr Updates pushen).

### 10. Internal Testing Track

Vor dem öffentlichen Release: deine App in den **Internal Testing Track** hochladen. Dort kannst du:
- Bis zu 100 Tester einladen (per E-Mail)
- Bugs finden vor dem öffentlichen Release
- Keine Review-Wartezeit (sofort live für Tester)

## 📋 Wochen 2-3

### 11. Produktions-Submit Google Play

Wenn das Internal Testing 1-2 Wochen lief und Bugs gefixt sind:
- Production Release mit allen Texten + Screenshots
- Google Review-Zeit: typisch 2-7 Tage

### 12. Marketing-Start

Vorlagen für Mail an Fachschaften und Content Creator findest du in `MARKETING_TEXTS.md`.

## 📋 Wochen 4+

### 13. Apple App Store (parallel oder später)

Erfordert:
- $99/Jahr Apple Developer Account
- Mac (oder Codemagic-CI für Cloud-Builds)
- iOS-Build, TestFlight, App Store Connect Submit

Reihenfolge-Empfehlung: **erst Android stabil laufen lassen** (1-2 Monate), **dann Apple machen**.

## 💡 Realitäts-Erinnerung

Diese Roadmap ist ambitioniert aber machbar. Realistische Zeitachsen:

| Phase | Zeitrahmen |
|---|---|
| Heute → GitHub-Pages live + Google Play Account | 1 Woche |
| Code-Rename + Icon + Screenshots | 1 Woche |
| Internal Testing | 1-2 Wochen |
| Erste Production-Version Android | 4 Wochen ab heute |
| Erste 100 Nutzer (Studenten + Marketing) | 6-8 Wochen ab heute |
| Erste 1.000 Nutzer | realistisch 4-6 Monate |

**Erinnerung:** App-Store-Launch ist nicht das Ende, sondern der Anfang. Marketing wird danach mehr Zeit kosten als das Coden vorher.

## ⚡ Eine wichtige Sache zuletzt

Wir haben jetzt **viel Zeit in die Namensfindung** gesteckt. Das war notwendig, weil markenrechtliche Probleme später teurer wären. Aber **jetzt ist es Zeit, vom Suchen ins Tun zu wechseln**.

Mein Vorschlag für den Energie-Fokus der nächsten Tage:

1. **Heute:** Domain reservieren + Logo-Prompt durchziehen
2. **Morgen:** GitHub Pages + Google Play Account + Impressum
3. **Diese Woche:** Code-Rename + erste APK mit GoVity-Branding
4. **Nächste Woche:** Erste Tester einladen

Wenn du in 2 Wochen einen Lauf hast wo Freunde GoVity tatsächlich nutzen, ist das ein **echter Erfolg** — egal wie groß die App später wird.

Go for it. 🚀
