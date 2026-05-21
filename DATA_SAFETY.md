# Datensicherheits-Formular (Google Play) + Privacy Manifest (Apple)

Diese beiden Formulare musst du beim Submit ausfüllen. Hier sind die ehrlichen Antworten für GoVity.

## Google Play — Datensicherheits-Formular

Im Play Console → App-Inhalt → Datensicherheit:

### Sammelt deine App Daten?
**Ja**

### Sind alle erfassten Daten verschlüsselt?
**Ja** (TLS/HTTPS in der Übertragung, BCrypt für Passwörter)

### Können Nutzer:innen Daten löschen?
**Ja** — Account-Löschung in der App und auf Anfrage per E-Mail

### Erfasste Datentypen — Auswahl

| Kategorie | Typ | Erfasst | Geteilt | Pflicht | Zweck |
|---|---|---|---|---|---|
| **Personenbezogen** | E-Mail-Adresse | ✓ | ✗ | ✓ | Kontoverwaltung, Authentifizierung, Kommunikation |
| **Personenbezogen** | Name (Anzeigename) | ✓ | ✗ | ✓ | Kontoverwaltung, Sicherheit |
| **Personenbezogen** | Andere personenbezogene Daten (Geburtsdatum) | ✓ | ✗ | ✓ | Sicherheit (Mindestalter-Prüfung) |
| **Standort** | Ungefährer Standort | ✓ | ✗ | ✗ | App-Funktionalität (Moves in der Nähe) |
| **Standort** | Genauer Standort | ✓ | ✗ | ✗ | App-Funktionalität (Moves in der Nähe) |
| **App-Aktivität** | App-Interaktionen | ✓ | ✗ | ✗ | Analyse (nur Server-Logs zur Missbrauchsabwehr) |
| **Nachrichten** | Andere In-App-Nachrichten (Move-Chats) | ✓ | ✗ | ✓ | App-Funktionalität (Gruppenchat) |
| **Authentifizierung** | Passwörter | ✓ | ✗ | ✓ | Authentifizierung |

### Daten teilen mit Drittanbietern
**Nein** — Wir geben keine personenbezogenen Daten an Drittanbieter zur Werbung oder zum Verkauf weiter. Die einzigen "Drittanbieter" sind:
- **Railway** (Hosting) — Auftragsverarbeitung
- **Brevo** (E-Mail-Versand) — Auftragsverarbeitung
- **OpenStreetMap / CartoCDN** (Karten) — IP-Adresse beim Karten-Laden

Diese sind alle "Auftragsverarbeiter", nicht "Drittempfänger" im Sinne des Formulars.

---

## Apple — Privacy Manifest (`PrivacyInfo.xcprivacy`)

Apple verlangt seit Frühjahr 2024 eine `PrivacyInfo.xcprivacy`-Datei in iOS-Apps.

Datei: `ios/Runner/PrivacyInfo.xcprivacy`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>NSPrivacyTracking</key>
    <false/>
    <key>NSPrivacyTrackingDomains</key>
    <array/>
    <key>NSPrivacyCollectedDataTypes</key>
    <array>
        <dict>
            <key>NSPrivacyCollectedDataType</key>
            <string>NSPrivacyCollectedDataTypeEmailAddress</string>
            <key>NSPrivacyCollectedDataTypeLinked</key>
            <true/>
            <key>NSPrivacyCollectedDataTypeTracking</key>
            <false/>
            <key>NSPrivacyCollectedDataTypePurposes</key>
            <array>
                <string>NSPrivacyCollectedDataTypePurposeAppFunctionality</string>
            </array>
        </dict>
        <dict>
            <key>NSPrivacyCollectedDataType</key>
            <string>NSPrivacyCollectedDataTypeName</string>
            <key>NSPrivacyCollectedDataTypeLinked</key>
            <true/>
            <key>NSPrivacyCollectedDataTypeTracking</key>
            <false/>
            <key>NSPrivacyCollectedDataTypePurposes</key>
            <array>
                <string>NSPrivacyCollectedDataTypePurposeAppFunctionality</string>
            </array>
        </dict>
        <dict>
            <key>NSPrivacyCollectedDataType</key>
            <string>NSPrivacyCollectedDataTypeCoarseLocation</string>
            <key>NSPrivacyCollectedDataTypeLinked</key>
            <true/>
            <key>NSPrivacyCollectedDataTypeTracking</key>
            <false/>
            <key>NSPrivacyCollectedDataTypePurposes</key>
            <array>
                <string>NSPrivacyCollectedDataTypePurposeAppFunctionality</string>
            </array>
        </dict>
        <dict>
            <key>NSPrivacyCollectedDataType</key>
            <string>NSPrivacyCollectedDataTypePreciseLocation</string>
            <key>NSPrivacyCollectedDataTypeLinked</key>
            <true/>
            <key>NSPrivacyCollectedDataTypeTracking</key>
            <false/>
            <key>NSPrivacyCollectedDataTypePurposes</key>
            <array>
                <string>NSPrivacyCollectedDataTypePurposeAppFunctionality</string>
            </array>
        </dict>
        <dict>
            <key>NSPrivacyCollectedDataType</key>
            <string>NSPrivacyCollectedDataTypeOtherUserContent</string>
            <key>NSPrivacyCollectedDataTypeLinked</key>
            <true/>
            <key>NSPrivacyCollectedDataTypeTracking</key>
            <false/>
            <key>NSPrivacyCollectedDataTypePurposes</key>
            <array>
                <string>NSPrivacyCollectedDataTypePurposeAppFunctionality</string>
            </array>
        </dict>
    </array>
    <key>NSPrivacyAccessedAPITypes</key>
    <array>
        <dict>
            <key>NSPrivacyAccessedAPIType</key>
            <string>NSPrivacyAccessedAPICategoryUserDefaults</string>
            <key>NSPrivacyAccessedAPITypeReasons</key>
            <array>
                <string>CA92.1</string>
            </array>
        </dict>
        <dict>
            <key>NSPrivacyAccessedAPIType</key>
            <string>NSPrivacyAccessedAPICategoryFileTimestamp</string>
            <key>NSPrivacyAccessedAPITypeReasons</key>
            <array>
                <string>C617.1</string>
            </array>
        </dict>
    </array>
</dict>
</plist>
```

**Was diese Datei sagt:**
- Wir tracken nicht (`NSPrivacyTracking: false`)
- Wir sammeln: E-Mail, Name, ungefährer + genauer Standort, User-Inhalte (Chats, Move-Beschreibungen)
- Alle gesammelten Daten sind **mit dem Account verknüpft** (linked)
- Zweck ist immer **App-Funktionalität**, nicht Werbung oder Tracking

Diese Datei legst du in `ios/Runner/PrivacyInfo.xcprivacy` ab.
**Aber:** das brauchen wir erst beim iOS-Submit. Für den Android-Submit ist das nicht relevant.
