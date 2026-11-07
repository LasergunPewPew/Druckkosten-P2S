# Druckkosten P2S

Ein Kostenrechner für 3D-Drucke mit dem Bambu Lab P2S und AMS. Er läuft als einzelne Webseite auf GitHub Pages, kostenlos und ohne Server. Alle Eingaben und gespeicherten Kalkulationen bleiben in deinem Browser (localStorage).

## Funktionen

- **Kalkulation:** Material, Strom, Maschine (Abschreibung + Verschleiß), Fehldruck-Risiko, Arbeitszeit, Extras
- **Verkaufspreis:** Marge und Umsatzsteuer (19 %, 7 % oder Kleinunternehmer nach §19 UStG), Kosten pro Stück
- **3MF-Import:** Eine geslicte Datei aus Bambu Studio ablegen; Druckzeit, Gramm und Farben pro Platte werden ausgelesen
- **Handy-Ansicht:** Auf dem Smartphone steht das Ergebnis immer unten im Bild; 3MF-Dateien lassen sich aus „Dateien“ bzw. iCloud Drive auswählen
- **Filament-Bibliothek** mit deinen €/kg-Preisen
- **Gespeicherte Kalkulationen** mit CSV-Export (über die Zwischenablage, z. B. für Excel oder Numbers)

## Auf GitHub veröffentlichen (einmalig, ca. 5 Minuten)

1. Bei [github.com](https://github.com) anmelden (oder kostenlos registrieren).
2. Oben rechts **+ › New repository** wählen. Name: `druckkosten`, Sichtbarkeit **Public**, dann **Create repository**.
3. Auf der neuen Seite **uploading an existing file** anklicken, `index.html` und `README.md` hineinziehen und **Commit changes** klicken.
4. Im Repository **Settings › Pages** öffnen. Unter *Build and deployment* bei **Source** „Deploy from a branch“ wählen, Branch **main** und Ordner **/ (root)**, dann **Save**.
5. Nach 1–2 Minuten ist der Rechner erreichbar unter
   `https://DEIN-GITHUB-NAME.github.io/druckkosten/`

Updates: Neue `index.html` über **Add file › Upload files** hochladen. Deine Daten bleiben erhalten, weil sie im Browser gespeichert sind.

## 3MF-Datei vorbereiten

1. Modell in Bambu Studio öffnen (bei der Frage nach dem Drucker auf den P2S umstellen).
2. **Slice plate** klicken.
3. **Datei › Exportieren › Geslicte Plattendatei exportieren** (*Export plate sliced file*). Die Datei endet auf `.gcode.3mf`.
4. Datei im Rechner ablegen bzw. auswählen.

Eine normale Projektdatei (*Projekt speichern*) enthält keine Druckzeiten und wird deshalb nicht erkannt.

## So wird gerechnet

```
Material     = Σ (Gramm × €/kg ÷ 1000) × (1 + Schwund %)
Strom        = Stunden × Watt ÷ 1000 × €/kWh
Maschine     = Stunden × (Anschaffung ÷ Lebensdauer in h + Verschleiß €/h)
Fehldruck    = (Material + Strom + Maschine) × Fehldruck %
Arbeit       = Minuten ÷ 60 × Stundensatz
Selbstkosten = Material + Strom + Maschine + Fehldruck + Arbeit + Extras + Versand
Pro Stück    = Selbstkosten ÷ Stückzahl
Preis        = pro Stück × (1 + Marge %) × (1 + USt %)
```

Die Grammzahl aus Bambu Studio enthält bereits Flush und Prime Tower.

### Startwerte (Beispiele, bitte anpassen)

| Variable | Startwert | Hinweis |
|---|---|---|
| Strompreis | 0,35 €/kWh | Wert aus deiner Stromrechnung |
| Ø Leistung | 150 W | Einmal mit einer Messsteckdose messen; PLA grob 100–200 W |
| Anschaffung | 1.000 € | Dein Kaufpreis für Drucker + AMS |
| Lebensdauer | 5.000 h | Community-üblich 3.000–5.000 Druckstunden |
| Verschleiß | 0,05 €/h | Düsen, Platten, PTFE-Schlauch, Fett |
| Schwund | 3 % | Spulenreste, Tests |
| Fehldruck | 10 % | Am Anfang höher, später 3–5 % |
| Stundensatz | 20 €/h | Nur relevant, wenn du Arbeitszeit einträgst |
| Marge | 30 % | |

## Datenschutz

Es gibt keinen Server und kein Tracking. Die 3MF-Datei wird nur in deinem Browser gelesen. Geladen werden lediglich Schriften von Google Fonts und die ZIP-Bibliothek JSZip von cdnjs.
