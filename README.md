# ⚡ Prüfapp

Eine mobile-first Progressive Web App (PWA) zur Durchführung und Dokumentation von **DGUV V3 Prüfungen** elektrischer Betriebsmittel. Läuft vollständig im Browser – kein Server, keine Installation, keine Abhängigkeiten.

---

## 📱 Features

### Prüfworkflow
- Geführter Schritt-für-Schritt Ablauf durch alle Prüfpunkte
- Gerätenummer-Eingabe mit automatischer Erkennung bekannter Geräte
- Erfassung von: Schutzklasse, Sichtprüfung, Nennspannung, R_SL, I_EA, ISO-Widerstand und Bemerkungen
- Anzeige des Gerätenamens in jedem Schritt zur Kontrolle

### Gerätedatenbank
- Automatisches Speichern aller geprüften Geräte (Nummer, Name, Schutzklasse, Spannung)
- Beim nächsten Prüfen derselben Gerätenummer werden Name und Parameter automatisch vorausgefüllt
- Datenbank-Export als JSON-Backup und Import aus Backup-Datei

### Protokoll
- Bis zu 28 Geräte pro Protokoll (konfigurierbar über Einstellungen)
- Listenansicht zum nachträglichen Bearbeiten aller Einträge
- Export als **CSV**-Datei mit korrekter Formatierung für Excel (Semikolon-Trennung, BOM, Komma als Dezimaltrennzeichen)
- Import bestehender CSV-Protokolle zur Weiterbearbeitung – der originale Dateiname bleibt beim erneuten Speichern erhalten

### Datensicherheit
- **Absturzsicherung**: Das aktuelle Protokoll wird nach jedem Gerät automatisch im `localStorage` gesichert
- Bei erneutem Öffnen der App nach einem Absturz wird das unterbrochene Protokoll zur Wiederherstellung angeboten
- Regelmäßige Datenbankbackups per Export-Button empfohlen

### Einstellungen
- Maximale Gerätezahl pro Protokoll frei einstellbar (1–100, Standard: 28)
- Wahl zwischen **Dunklem Theme** (Standard) und **Hellem Theme**
- Einstellungen werden dauerhaft gespeichert

### Autovervollständigung
Folgende Felder merken sich zuvor eingegebene Werte und schlagen passende Einträge vor:
- Firma / Kunde
- Einsatzort
- Name des Prüfers
- Gerätename

### PWA / Offline-Nutzung
- Installierbar als App auf Android und iOS (kein App Store nötig)
- Vollständig offline nutzbar nach einmaligem Laden
- Läuft im Vollbild ohne Browser-Adressleiste

---

## 🚀 Installation als App (Android / iOS)

### Android (Chrome)
1. Seite in Chrome öffnen
2. Unten erscheint automatisch ein Banner **„Als App installieren"** → antippen
3. Alternativ: Drei-Punkte-Menü → *„App installieren"* bzw. *„Zum Startbildschirm hinzufügen"*

### iOS (Safari)
1. Seite in Safari öffnen
2. Teilen-Symbol antippen → *„Zum Home-Bildschirm"*

### Lokale Nutzung ohne Server
Die App kann auch direkt als HTML-Datei lokal betrieben werden:
1. Datei auf das Gerät übertragen (USB, E-Mail, etc.)
2. App **„Simple HTTP Server"** aus dem Play Store installieren
3. Server auf die HTML-Datei zeigen → in Chrome öffnen → installieren

---

## 📂 Dateinamen-Konvention

| Dateityp | Format | Beispiel |
|---|---|---|
| Protokoll CSV | `Werte_Firma_Ort_DD-MM-JJJJ.csv` | `Werte_Mustermann_GmbH_Halle_1_20-03-2026.csv` |
| DB-Backup | `DB_Backup_Firma_DD-MM-JJJJ_HH-MMUhr.json` | `DB_Backup_Mustermann_GmbH_20-03-2026_14-35Uhr.json` |

---

## 🗂 CSV-Spaltenformat

Die exportierte CSV enthält folgende Spalten (Semikolon-getrennt):

| Spalte | Inhalt |
|---|---|
| 1 | Inventar-Nr. |
| 2 | Gerätename |
| 3 | SK I (X oder leer) |
| 4 | SK II/III (X oder leer) |
| 5 | Sichtprüfung (X = OK, O = Defekt) |
| 6 | Prüfung SL (X = bestanden, O = nicht bestanden) |
| 7 | Spannung (230 / 400) |
| 8 | R_SL in Ω |
| 9 | ISO-Widerstand in MΩ |
| 10 | I_EA in mA |
| 11 | Gesamtstatus (X = bestanden, O = nicht bestanden) |
| 12 | Bemerkung |

---

## 💾 Datenspeicherung

Alle Daten werden ausschließlich lokal im `localStorage` des Browsers gespeichert:

| Schlüssel | Inhalt |
|---|---|
| `geraeteDB` | Gerätedatenbank (Nummer → Name, SK, Spannung) |
| `protokoll_autosave` | Aktuelles Protokoll (Absturzsicherung) |
| `maxDevices` | Eingestellte maximale Gerätezahl |
| `theme` | Gewähltes Farbthema (`light` / `dark`) |
| `ac_firma` | Autovervollständigung Firma |
| `ac_ort` | Autovervollständigung Ort |
| `ac_pruefer` | Autovervollständigung Prüfer |
| `ac_gName` | Autovervollständigung Gerätename |

> ⚠️ **Wichtig:** Bei einem Browser-Reset oder dem Löschen der Browser-Daten gehen alle gespeicherten Daten verloren. Regelmäßige Datenbankbackups über den Export-Button werden dringend empfohlen.

---

## 🛠 Technologie

- Reines HTML5 / CSS3 / Vanilla JavaScript – keine Frameworks, keine Build-Tools
- PWA mit Service Worker und Web App Manifest (inline als Blob eingebettet)
- Schriften: [DM Sans](https://fonts.google.com/specimen/DM+Sans) & [DM Mono](https://fonts.google.com/specimen/DM+Mono) via Google Fonts
- Datenspeicherung: `localStorage`

---

## 📋 Prüfablauf

```
Start
 └── Stammdaten (Firma, Ort, Prüfer)
      └── Gerätenummer
           ├── [Bekanntes Gerät] → Sichtprüfung
           └── [Unbekanntes Gerät] → Gerätename → Schutzklasse → Sichtprüfung
                                                        └── Spannung
                                                             ├── [SK I]  → R_SL → I_EA → ISO → Bemerkungen → Speichern
                                                             └── [SK II/III] → ISO → Bemerkungen → Speichern
```

---

## 📄 Lizenz

Dieses Projekt steht zur freien privaten und betrieblichen Nutzung zur Verfügung.
