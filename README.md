# ⚡ Prüfapp

Eine mobile-first Progressive Web App (PWA) zur Durchführung und Dokumentation von **DGUV V3 Prüfungen** elektrischer Betriebsmittel. Läuft vollständig im Browser – kein Server, keine Installation, keine Abhängigkeiten.

🌐 **[→ App öffnen](https://johannesiwc.github.io/Pruefapp/)**

---

## 📱 Installation als App

### Android (Chrome)
1. App-Link oben in Chrome öffnen
2. Banner **„Als App installieren"** antippen — oder: Drei-Punkte-Menü → *App installieren*
3. Die App erscheint auf dem Homescreen und läuft im Vollbild ohne Browser-Leiste

### iOS (Safari)
1. App-Link in Safari öffnen
2. Teilen-Symbol → *Zum Home-Bildschirm*

---

## ✨ Features

### Firmenverwaltung
- Firmen anlegen, auswählen und verwalten
- Die aktive Firma wird automatisch in das Prüfprotokoll übernommen
- Abgleich zwischen gewählter Firma und geladener Datenbank mit Warnung bei Abweichung

### Gerätedatenbank
- Automatisches Speichern aller geprüften Geräte (Nummer, Name, Schutzklasse, Spannung)
- Beim nächsten Prüfen einer bekannten Gerätenummer werden Daten automatisch vorausgefüllt
- Datenbankname wird automatisch gesetzt und mit der Firma abgeglichen
- Datenbank anzeigen, bearbeiten, importieren, exportieren und löschen
- Schutz vor versehentlichem Überschreiben durch Bestätigungsdialoge

### Prüfworkflow
- Geführter Schritt-für-Schritt Ablauf durch alle Prüfpunkte
- Schritte: Gerätenummer → Gerätename → Schutzklasse → Sichtprüfung → Spannung → R_SL → I_EA → ISO-Widerstand → Bemerkungen
- Gerätename wird in jedem Schritt angezeigt zur laufenden Kontrolle
- Bekannte Geräte überspringen Eingabeschritte automatisch

### Protokoll
- Konfigurierbare Anzahl Geräte pro Protokoll (Standard: 28, einstellbar 1–100)
- Kollabierbare Listenansicht zum Bearbeiten aller Einträge
- CSV-Export mit korrekter Formatierung für Excel
- Import bestehender CSV-Protokolle zur Weiterbearbeitung
- Originaler Dateiname bleibt beim erneuten Speichern erhalten

### Datensicherheit & Komfort
- **Absturzsicherung**: Protokoll wird nach jedem Gerät automatisch gesichert und bei erneutem Öffnen wiederhergestellt
- Autovervollständigung für Firma, Ort, Prüfer und Gerätename
- Bestätigungsdialoge vor dem Löschen oder Überschreiben von Daten

### Einstellungen
- 🌙 Dunkles und ☀️ helles Theme
- 🇩🇪 Deutsch und 🇬🇧 Englisch
- Maximale Gerätezahl pro Protokoll
- Datenbankname manuell vergeben

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

Alle Daten werden lokal im `localStorage` des Browsers gespeichert:

| Schlüssel | Inhalt |
|---|---|
| `geraeteDB` | Gerätedatenbank |
| `dbLoadedName` | Anzeigename der geladenen Datenbank |
| `dbFirmaName` | Firmenname der Datenbank (für Abgleich) |
| `protokoll_autosave` | Absturzsicherung des laufenden Protokolls |
| `firmaList` | Gespeicherte Firmen |
| `activeFirma` | Aktuell ausgewählte Firma |
| `maxDevices` | Maximale Gerätezahl pro Protokoll |
| `theme` | Farbthema (`light` / `dark`) |
| `lang` | Sprache (`de` / `en`) |
| `ac_firma` / `ac_ort` / `ac_pruefer` / `ac_gName` | Autovervollständigung |

> ⚠️ **Wichtig:** Bei einem Browser-Reset gehen alle gespeicherten Daten verloren. Regelmäßige Datenbankbackups über **Datenbank → Exportieren** werden dringend empfohlen.

---

## 🔄 Prüfablauf

```
Start → Firma wählen
         └── Prüfung starten
              └── Stammdaten (Firma, Ort, Prüfer)
                   └── Gerätenummer
                        ├── [Bekannt] ──────────────────────────→ Sichtprüfung
                        └── [Unbekannt] → Gerätename → Schutzklasse → Sichtprüfung
                                                              └── Spannung
                                                                   ├── [SK I]    → R_SL → I_EA → ISO → Bemerkungen
                                                                   └── [SK II/III]       → ISO → Bemerkungen
                                                                                               └── Speichern → nächstes Gerät / CSV exportieren
```

---

## 🛠 Technologie

- Reines HTML5 / CSS3 / Vanilla JavaScript – keine Frameworks, keine Build-Tools
- PWA mit inline Service Worker und Web App Manifest
- Schriften: [DM Sans](https://fonts.google.com/specimen/DM+Sans) & [DM Mono](https://fonts.google.com/specimen/DM+Mono)
- Datenspeicherung: `localStorage`
- Hosting: GitHub Pages

---

## 🐛 Bugs & Feedback

Fehler oder Verbesserungsvorschläge gerne als [Discussion](https://github.com/JohannesIWC/Pruefapp/discussions/categories/bugs) melden.

---

## 📄 Lizenz

Dieses Projekt steht zur freien privaten und betrieblichen Nutzung zur Verfügung.
