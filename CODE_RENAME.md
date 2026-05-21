# Code-Umbenennung: MoveMatch → GoVity

Die App-Code-Basis hat noch alte Namen drin (MoveMatch, movematch). Das müssen wir umbenennen, **bevor du den ersten Build für den Store machst**, weil:

- **Bundle-ID** ist nach Submit dauerhaft.
- **App-Name auf dem Homescreen** sollte direkt richtig sein.

## STUFE 1 — Pflicht (vor dem ersten Submit)

### 1.1 Android — `android/app/build.gradle.kts`

Pfad:
```
movematch_frontend/android/app/build.gradle.kts
```

Finde den Block `defaultConfig { ... }`. Setze:

```kotlin
defaultConfig {
    applicationId = "com.govity.app"
    minSdk = 23
    targetSdk = 34
    versionCode = 1
    versionName = "1.0.0"
}
```

(Falls `build.gradle` ohne `.kts`: `applicationId "com.govity.app"` ohne `=`.)

### 1.2 Android — `android/app/src/main/AndroidManifest.xml`

Finde das `<application>`-Tag, ändere `android:label`:

**Alt:**
```xml
<application
    android:label="movematch_frontend"
```

**Neu:**
```xml
<application
    android:label="GoVity"
```

### 1.3 iOS — `ios/Runner/Info.plist`

Finde:
```xml
<key>CFBundleDisplayName</key>
<string>Movematch Frontend</string>
```

Ändere zu:
```xml
<key>CFBundleDisplayName</key>
<string>GoVity</string>
```

### 1.4 Pubspec — `pubspec.yaml`

```yaml
name: govity
description: "Spontane Moves in deiner Nähe — Go for Activity"
version: 1.0.0+1
```

Das `+1` ist `versionCode` für Android. Bei jedem neuen Build später hochzählen:
- Bug-Fixes: `1.0.1+2`, `1.0.2+3` ...
- Features: `1.1.0+10`, `1.2.0+11` ...

### 1.5 Flutter Code — App-Name in der UI

Suche nach „MoveMatch" in `lib/` und ersetze mit „GoVity":

**PowerShell-Befehl** (zeigt alle Stellen):
```powershell
cd C:\Users\mauri\Desktop\movematch-backend\movematch_frontend\lib
findstr /s /n /i "MoveMatch" *.dart
```

Typische Stellen:
- `lib/main.dart` — `MaterialApp(title: 'MoveMatch'...)` → `'GoVity'`
- AppBar-Titel auf Login/Register/Home-Screens
- Splash-Screen-Texte

**Suchen + Ersetzen in IntelliJ:**
- `Strg+Shift+R` (Replace in Files)
- Search: `MoveMatch`
- Replace: `GoVity`
- Scope: nur `lib/` Ordner
- **Match Case: AN**

Dann nochmal mit:
- Search: `movematch` (klein)
- Replace: `govity`
- Match Case: AN
- Vorsicht: nicht Variablennamen wie `_movematchToken` ersetzen — die kannst du erstmal lassen.

## STUFE 2 — Empfohlen (vor öffentlicher Verfügbarkeit)

### 2.1 Backend — `application.properties` / Mail-Templates

Im Spring Boot Backend, suche nach Strings „MoveMatch" in:
- E-Mail-HTML-Templates (Verifizierungs-Mail, Reset-Mail)
- Subject-Lines: `subject = "MoveMatch — bestätige deine E-Mail"` → `"GoVity — bestätige deine E-Mail"`
- Logger-Meldungen mit App-Namen

**PowerShell-Suche im Backend:**
```powershell
cd C:\Users\mauri\Desktop\movematch-backend\movematch-backend\src
findstr /s /n /i "movematch" *.java *.html *.properties *.yml
```

### 2.2 Splash-Screen / Native Icons

Wenn du `flutter_launcher_icons` nutzt: in `pubspec.yaml`:
```yaml
flutter_launcher_icons:
  android: true
  ios: true
  image_path: "assets/icon/govity_icon_1024.png"
  adaptive_icon_background: "#7C3AED"
  adaptive_icon_foreground: "assets/icon/govity_icon_foreground.png"
```

## STUFE 3 — Optional (jederzeit später)

### 3.1 Repo-Namen umbenennen (optional)

Du kannst die GitHub-Repos später umbenennen:
- `movematch-backend` → `govity-backend`
- `movematch_frontend` → `govity_frontend`

**Wie:** Auf github.com → Repo → Settings → Repository Name → Save

GitHub legt automatisch eine Weiterleitung von der alten URL an. Lokale `git remote` musst du dann updaten:
```powershell
cd C:\Users\mauri\Desktop\movematch-backend\movematch-backend
git remote set-url origin https://github.com/mauricetrogant-dot/govity-backend.git
```

### 3.2 Lokale Ordner-Pfade umbenennen

Pfad `C:\Users\mauri\Desktop\movematch-backend\` umzubenennen ist **riskant** — viele Tools (IntelliJ, Gradle-Cache, Flutter-Cache) speichern absolute Pfade.

**Empfehlung:** lass den Ordnernamen lokal so wie er ist. Es schadet niemandem.

## Nach allen Änderungen

```powershell
# Frontend
cd C:\Users\mauri\Desktop\movematch-backend\movematch_frontend
flutter clean
flutter pub get
flutter build apk --release --dart-define=API_URL=https://web-production-99b22.up.railway.app

# Backend (falls Backend-Texte angepasst): pushen + Railway redeployt automatisch
cd C:\Users\mauri\Desktop\movematch-backend\movematch-backend
git add .
git commit -m "Rename app: MoveMatch -> GoVity"
git push
```

Beim ersten Build mit neuer `applicationId` wird Android das als **andere App** behandeln — die alte muss erst deinstalliert werden, sonst Signature-Konflikt.

## Bundle-ID-Hinweis: `com.govity.app`

Ich habe `com.govity.app` empfohlen weil:
- `govity.io` ist als Bundle-ID schon belegt (von Trusted Family 2 Software)
- `com.govity.app` ist klassische Apple/Google-Konvention
- Falls du später Web-API/Web-App machst, kannst du `com.govity.web` etc. ergänzen

Falls du später eine eigene Domain `govityapp.de` oder `govityapp.de` registrierst, passt die Bundle-ID gut zusammen.

## Zusammenfassung der Pflicht-Änderungen

| Datei | Änderung |
|---|---|
| `android/app/build.gradle.kts` | `applicationId = "com.govity.app"` |
| `android/app/src/main/AndroidManifest.xml` | `android:label="GoVity"` |
| `ios/Runner/Info.plist` | `CFBundleDisplayName: GoVity` |
| `pubspec.yaml` | `name: govity`, `description: "Spontane Moves in deiner Nähe — Go for Activity"` |
| Alle `.dart` Dateien in `lib/` | „MoveMatch" → „GoVity", „movematch" → „govity" |
| Backend Mail-Templates | „MoveMatch" → „GoVity" |
