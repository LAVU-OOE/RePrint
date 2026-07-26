[**📖 Home (README)**](../README.md) &nbsp; ┃ &nbsp; [**🇦🇹 LIESMICH**](./LIESMICH.md) &nbsp; ┃ &nbsp; [**ℹ️ INFORMATION**](./INFORMATION.md) &nbsp; ┃ &nbsp; **🪧 AUSKUNFT** &nbsp; ┃ &nbsp; [**🔧 MECHANICS**](./MECHANICS.md) &nbsp; ┃ &nbsp; [**⚖️ MIT License**](../LICENSE)
---

## 📦 Externe Datenquellen (JSON)

Die App bezieht ihre dynamischen Daten aus zwei zentralen JSON-Dateien, die in diesem Repository verwaltet werden:

1. **`sortiment.json`** – Enthält das Produktsortiment mit Produktnummer, Beschreibung und optionalem Verpackungszusatz.

2. **`locations.json`** – Enthält die Liste der Recyclinghöfe mit Name, Standortcode, Postleitzahl und Region.

Diese Dateien werden über die GitHub-URLs geladen und können unabhängig von der App aktualisiert werden.

## 🚀 Erste Schritte & Nutzung

1. **App öffnen:** Rufen Sie die Seite über den bereitgestellten Link auf oder installieren Sie sie als PWA.

2. **Standort auswählen:** Wählen Sie den gewünschten Recyclinghof aus der dynamisch geladenen Liste in der Kopfzeile aus.

3. **Artikel auswählen:** Suchen Sie den gewünschten Artikel entweder anhand der **Artikelnummer** (numerisch gruppiert) oder der **Beschreibung** (alphabetisch gruppiert).

4. **Drucklayout anpassen (optional):**

* Klicken Sie auf die Vorschau, um das interaktive A4-Druckblatt zu öffnen.

* Klicken Sie auf eine beliebige Stelle auf dem Blatt, um Etiketten hinzuzufügen oder zu entfernen.

5. **Drucken:** Klicken Sie auf die Schaltfläche **Jetzt drucken**, um das A4-Blatt mit Ihren Etiketten zu drucken.

## ⚙️ Datenbankanpassung (CRUD)

Sie können über die Schaltfläche **Optionen** auf den integrierten Datenbankmanager zugreifen:

* **Produktbereich auswählen:** Zeigt die aktuelle Produktliste an.

* **Datenbank verwalten:** Hier können Sie:

* Neue Artikel hinzufügen.

* Vorhandene Artikel bearbeiten oder löschen.

* Die gesamte Datenbank als JSON-Datei exportieren.

* **Standardeinstellungen speichern:** Speichert die aktuellen Einstellungen (Position, Format, Menge, Startposition) als Browser-Standard.

## 🔧 Technische Details & Entwicklung

* **Sprache:** Reines HTML, CSS und JavaScript (ES6+).

* **Speicherung:** Verwendet `localStorage` für benutzerspezifische Einstellungen, den Sortimentscache und den Standortcache.

* **Netzwerk:** Nutzt die `fetch`-API mit einer „No-Store“-Cache-Strategie für JSON-Daten, um stets die aktuellsten Daten zu priorisieren.

* **Service Worker:** Die `sw.js` implementiert eine **Netzwerk-First-Strategie** für JSON-Datenbanken und eine **Cache-First-Strategie** für statische Assets, was eine robuste Offline-Nutzung ermöglicht.

* **Ordnerstruktur:** Die Hauptanwendung befindet sich im Ordner `/`, alle Assets (Icons, Bilder) im Ordner `/assets/`. Eine `index.html`-Datei im Stammverzeichnis leitet zur Anwendung weiter.

## 🤝 Mitwirken

Beiträge sind willkommen! Bitte beachten Sie Folgendes:

1. Forken Sie das Repository.

2. Erstellen Sie einen neuen Branch für Ihr Feature (`git checkout -b feature/new-feature`).

3. Übernehmen Sie Ihre Änderungen („git commit -m 'feat: Neue Funktion hinzugefügt‘“).
4. Pushen Sie den Zweig („git push origin feature/new-feature“).
5. Erstellen Sie eine Pull-Anfrage.

**Wichtige Hinweise für Änderungen an den JSON-Datenbanken:**

* Stellen Sie sicher, dass die JSON-Struktur gültig ist.
* Testen Sie die Änderungen lokal, bevor Sie sie in den Hauptzweig einbinden.

## 📄 Lizenz

Dieses Projekt ist Open Source und steht unter der MIT-Lizenz.

## 📦 Externe Datenquellen (JSON)

Die App bezieht ihre dynamischen Daten aus zwei zentralen JSON-Dateien, die in diesem Repository gepflegt werden:

1. **`sortiment.json`** – Enthält das Artikel-Sortiment mit Artikelnummer, Bezeichnung und optionalem Gebinde-Suffix.
2. **`locations.json`** – Enthält die Liste der ASZ-Standorte mit Name, Standortcode, Postleitzahl und Region.

Diese Dateien werden über die GitHub-Raw-URLs geladen und können unabhängig von der App selbst aktualisiert werden.

## 🚀 Erste Schritte & Nutzung

1. **App öffnen:** Rufen Sie die Seite über den bereitgestellten Link auf oder installieren Sie sie als PWA.
2. **Standort wählen:** Wählen Sie im Header den gewünschten ASZ-Standort aus der dynamisch geladenen Liste.
3. **Artikel auswählen:** Suche den gewünschten Artikel entweder über die **Art.Nr.** (numerisch gruppiert) oder die **Bezeichnung** (alphabetisch gruppiert).
4. **Drucklayout anpassen (optional):** 
* Klicken Sie auf das Vorschaubild, um den interaktiven A4-Druckbogen zu öffnen. 
* Klicken Sie auf beliebige Positionen im Bogen, um Etiketten hinzuzufügen oder zu entfernen.
5. **Drucken:** Klicken Sie auf den Haupt-Button **"Jetzt Drucken"**, um den A4-Bogen mit Ihren Etiketten zu drucken.

## ⚙️ Anpassung der Datenbank (CRUD)

Über den **"Optionen"**-Button kannst du auf den integrierten Datenbank-Manager zugreifen:

* **Sortiment wählen:** Zeigt die aktuelle Artikelliste an.
* **Datenbank verwalten:** Hier kannst du: 
* Neue Artikel hinzufügen. 
* Bestehende Artikel bearbeiten oder löschen. 
* Die gesamte Datenbank als JSON-Datei exportieren.
* **Standard sichern:** Speichert die aktuellen Einstellungen (Standort, Format, Anzahl, Startposition) als Standard im Browser.

## 🔧 Technische Details & Entwicklung

* **Sprache:** Reines HTML, CSS und JavaScript (ES6+).
* **Speicherung:** Verwendet `localStorage` für benutzerspezifische Einstellungen, den Sortiments-Cache und den Standort-Cache.
* **Netzwerk:** Nutzt die `fetch`-API mit „no-store“-Cache-Strategie für die JSON-Daten, um immer aktuelle Daten zu priorisieren.
* **Service Worker:** Der `sw.js` implementiert

Eine **Network-First-Strategie** für die JSON-Datenbanken und eine **Cache-First-Strategie** für statische Assets, was eine robuste Offline-Nutzung ermöglicht.
* **Ordnerstruktur:** Die Hauptanwendung befindet sich im `/`-Ordner, alle Assets (Icons, Bilder) im `/assets/`-Ordner. Eine `index.html` im Root leitet auf die App weiter.

## 🤝 Beitrag leisten

Beiträge sind willkommen! Bitte beachte die folgenden Punkte:

1. Forken Sie das Repository.
2. Erstelle einen neuen Branch für dein Feature (`git checkout -b feature/neues-feature`).
3. Übernehmen Sie Ihre Änderungen (`git commit -m 'feat: Neues Feature hinzugefügt'`).
4. Pushe den Branch („git push origin feature/neues-feature“).
5. Stellen Sie einen Pull Request ein.

**Wichtige Hinweise für Änderungen an den JSON-Datenbanken:**

* Stellen Sie sicher, dass die JSON-Struktur gültig ist.
* Testen Sie die Änderungen lokal, bevor Sie sie in der Hauptbranch zusammenführen.

## 📄 Lizenz

Dieses Projekt ist Open Source und steht unter der [MIT-Lizenz](LICENSE).