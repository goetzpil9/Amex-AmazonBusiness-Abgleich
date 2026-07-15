# Amex ↔ Amazon Abgleich

Ordnet **Amazon-Business-Bestellungen** den **American-Express-Belastungen** zu – vollständig **lokal im Browser**, ohne Server und ohne Upload deiner Daten.

Amazon überträgt an die Kreditkarte keinen brauchbaren Verwendungszweck: Auf der Amex-Abrechnung stehen praktisch nur Datum und Betrag, die Referenznummern passen weder zur Bestell- noch zur Rechnungsnummer. Dieses Tool nimmt beide Berichte (Amazon + Amex) und ordnet die Posten automatisch über **Betrag + Datum (mit Toleranz)** einander zu.

---

## Was es kann

- **Automatischer Abgleich** von Amazon-Amex-Buchungen gegen die Amex-Umsätze über Betrag + Datum, mit einstellbarer **Datumstoleranz** (Amazon-Transaktionsdatum und Amex-Buchungsdatum weichen oft um 1–2 Tage ab).
- **Mehrdeutigkeit erkennen:** Liegen mehrere gleich hohe Buchungen im selben Zeitfenster, werden alle betroffenen Posten zur manuellen Prüfung markiert, statt willkürlich zuzuordnen.
- **Erstattungen & Storni:** Rückerstattungen werden als Gutschrift behandelt; Belastung-plus-Storno-Paare, die sich auf der Karte aufheben, werden separat als „netto 0" ausgewiesen.
- **Übersichtliche Prüfansicht** mit Kategorien (Zugeordnet, Mehrdeutig, Nur Amex, Nur Amazon, Storno, aus Datenbank) und **Live-Suche** über die Tabelle.
- **Datenbank / Wiederverwendung:** Der Export ist re-importierbar. Beim nächsten Lauf (auch mit überlappenden Zeiträumen) werden bereits zugeordnete Posten übersprungen – erkannt über die Amazon-*Zahlungsreferenz-ID* und den Amex-*Betreff*, die jeweils eindeutig sind.
- **Ein Export für alles:** Eine CSV, die zugleich Datenbank *und* Buchhaltungs-Export ist – inklusive leerer Spalte **Buchungskonto**, die du selbst befüllst und die beim Wieder-Einlesen erhalten bleibt.
- **PWA:** installierbar, offline nutzbar.

---

## Nutzung

### 1. Amazon-Bericht herunterladen
1. In [Amazon Business](https://www.amazon.de/business) anmelden (Rolle *Administrator* oder *Buchhaltung/Finanzen*).
2. **Berichte → Bestell-Abgleich** öffnen ([Direktlink](https://www.amazon.de/b2b/aba/reports?reportType=transactions_report)).
3. Zeitraum wählen (z. B. letzte 12 Wochen) – der Zeitraum wird im UI gesetzt, nicht über die URL.
4. **Bericht erstellen** → CSV lädt herunter.

### 2. Amex-Bericht herunterladen
1. Bei [American Express](https://global.americanexpress.com/activity/search) anmelden.
2. **Kontobewegungen & Abrechnungen** → **Zeitraum personalisieren** (gleicher Zeitraum wie bei Amazon).
3. **Herunterladen → CSV**, dabei **„Alle weiteren Transaktionsdetails einschließen"** anhaken.
4. Datei heißt meist `activity.csv`.

### 3. Abgleichen
1. Beide CSVs in die App ziehen (optional zuerst die zuletzt gespeicherte Datenbank-CSV).
2. **Abgleichen** klicken.
3. Ergebnis prüfen, ggf. mehrdeutige Posten manuell klären.
4. **Zuordnung speichern (CSV)** – das ist deine Datenbank für's nächste Mal und dein Buchhaltungs-Export.

---

## Datenschutz

Es werden **keine Daten hochgeladen oder gespeichert**. Alle CSVs werden ausschließlich im Browser verarbeitet; nichts verlässt dein Gerät, es gibt keinen Server und kein Tracking. Es werden keine Werbeanzeigen eingeblendet.

---

## Als App installieren (PWA)

Beim Öffnen der gehosteten Seite bietet der Browser „Zur Startseite hinzufügen" bzw. „Installieren" an. Danach lässt sich das Tool wie eine App starten und funktioniert offline.

---

## Selbst hosten / deployen

Statische Seite ohne Build-Schritt. Für GitHub Pages:

1. Diese Dateien in einen Ordner des Repos legen:
   - `index.html` *(die App – ggf. aus dem Release umbenennen)*
   - `manifest.json`
   - `sw.js`
   - `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`
2. In den Repo-Einstellungen **GitHub Pages** aktivieren.
3. Seite aufrufen – fertig.

> Der Service Worker (`sw.js`) läuft nur über HTTPS/einen echten Host, nicht per lokalem Doppelklick. Bei Updates die Versionsnummer in `sw.js` erhöhen (`v1` → `v2` …), damit alte Caches ersetzt werden.

---

## Technik

Reines HTML/CSS/JavaScript in einer Datei, **keine externen Abhängigkeiten**, kein Framework, kein Backend. CSV-Parsing, Matching und Export laufen clientseitig.

---

## Roadmap

- [ ] DATEV-Export (aus der gespeicherten Zuordnungs-CSV)

---

## Unterstützen

Wenn dir das Tool hilft: [☕ Buy me a coffee](https://www.buymeacoffee.com/goetzpil)

---

## Hinweise

Dieses Projekt steht in **keiner Verbindung** zu Amazon oder American Express. „Amazon", „Amazon Business" und „American Express" sind Marken der jeweiligen Inhaber.

Der Abgleich erfolgt heuristisch über Betrag und Datum und **ersetzt keine buchhalterische Prüfung**. Ergebnisse bitte vor der Verbuchung kontrollieren. Keine Gewähr für Richtigkeit oder Vollständigkeit.
