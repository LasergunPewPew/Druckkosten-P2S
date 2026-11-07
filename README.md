# Druckkosten P2S

Ein Kostenrechner für 3D-Drucke mit dem Bambu Lab P2S und AMS. Er läuft als einzelne Webseite auf GitHub Pages, kostenlos und ohne Server. Alle Eingaben und gespeicherten Kalkulationen bleiben in deinem Browser (localStorage).

## Funktionen

- **Kalkulation:** Material, Strom, Maschine (Abschreibung + Verschleiß), Fehldruck-Risiko, Arbeitszeit, Extras
- **Verkaufspreis:** Marge und Umsatzsteuer (19 %, 7 % oder Kleinunternehmer nach §19 UStG), Kosten pro Stück
- **3MF-Import:** Eine geslicte Datei aus Bambu Studio ablegen; Druckzeit, Gramm und Farben pro Platte werden ausgelesen
- **MakerWorld-Lesezeichen:** Ein Klick auf einer MakerWorld-Modellseite übernimmt alle Druckprofile mit Platten, Zeiten und Filamenten
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

## MakerWorld-Lesezeichen einrichten

1. Den Rechner auf GitHub Pages öffnen und den Bereich **MakerWorld-Lesezeichen** aufklappen. Die Adresse ist dort schon eingetragen.
2. Den blauen Knopf **Druckkosten** in die Lesezeichenleiste ziehen (Safari: Lesezeichenleiste mit Cmd + Shift + B einblenden).
3. Auf MakerWorld ein Modell öffnen und das Lesezeichen anklicken. Der Rechner öffnet sich in einem neuen Tab mit allen Druckprofilen des Modells.
4. Profil und Platten wählen und **In die Kalkulation übernehmen** klicken.

Warum ein Lesezeichen und kein Link-Feld? MakerWorld hat keine offizielle öffentliche Schnittstelle und blockiert Abfragen von fremden Webseiten (CORS, Cloudflare). Das Lesezeichen liest die Seite, die du gerade offen hast, direkt in deinem Browser. Baut MakerWorld die Seite um, kann es aufhören zu funktionieren; der 3MF-Import geht dann weiterhin.

**Hinweis:** Die Werte auf MakerWorld kommen vom Ersteller des Profils und sind oft für einen anderen Drucker geslict (z. B. X1 Carbon). Für genaue Werte das Modell in Bambu Studio für den P2S slicen und die 3MF importieren.

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

Die Grammzahl aus Bambu Studio und MakerWorld enthält bereits Flush und Prime Tower.

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
