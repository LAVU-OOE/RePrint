
## 📦 External Data Sources (JSON)

The app retrieves its dynamic data from two central JSON files maintained in this repository:

1. **`sortiment.json`** – Contains the product assortment with product number, description, and optional packaging suffix.
2. **`locations.json`** – Contains the list of recycling center locations with name, location code, postal code, and region.

These files are loaded via the GitHub raw URLs and can be updated independently of the app itself.

## 🚀 Getting Started & Usage

1. **Open the App:** Access the page via the provided link or install it as a PWA.
2. **Select a Location:** Select the desired recycling center location from the dynamically loaded list in the header.
3. **Select Item:** Search for the desired item either by **Item No.** (numerically grouped) or **Description** (alphabetically grouped).
4. **Adjust Print Layout (Optional):**
    * Click on the preview image to open the interactive A4 print sheet.
    * Click on any position on the sheet to add or remove labels.
5. **Print:** Click the main **"Print Now"** button to print the A4 sheet with your labels.

## ⚙️ Database Customization (CRUD)

You can access the integrated database manager via the **"Options"** button:

* **Select Product Range:** Displays the current product list.
* **Manage Database:** Here you can:

* Add new items.
* Edit or delete existing items.
* Export the entire database as a JSON file.
* **Save Defaults:** Saves the current settings (location, format, quantity, starting position) as the browser default.

## 🔧 Technical Details & Development

* **Language:** Pure HTML, CSS, and JavaScript (ES6+).
* **Storage:** Uses `localStorage` for user-specific settings, the assortment cache, and the location cache.
* **Network:** Uses the `fetch` API with a "no-store" cache strategy for JSON data to always prioritize the most up-to-date data.
* **Service Worker:** The `sw.js` implements a **network-first strategy** for JSON databases and a **cache-first strategy** for static assets, enabling robust offline use.
* **Folder Structure:** The main application is located in the `/` folder, and all assets (icons, images) are in the `/assets/` folder. An `index.html` file in the root directory redirects to the app.

## 🤝 Contribute

Contributions are welcome! Please note the following points:

1. Fork the repository.
2. Create a new branch for your feature (`git checkout -b feature/new-feature`).
3. Commit your changes (`git commit -m 'feat: New feature added'`).
4. Push the branch (`git push origin feature/new-feature`).
5. Create a pull request.

**Important notes for changes to the JSON databases:**

* Ensure the JSON structure is valid.
* Test the changes locally before merging them into the main branch.

## 📄 License

This project is open source and is licensed under the MIT License.

## 📦 Externe Datenquellen (JSON)

Die App bezieht ihre dynamischen Daten aus zwei zentralen JSON-Dateien, die in diesem Repository gepflegt werden:

1.  **`sortiment.json`** – Enthält das Artikel-Sortiment mit Artikelnnummer, Bezeichnung und optionalem Gebinde-Suffix.
2.  **`locations.json`** – Enthält die Liste der ASZ-Standorte mit Name, Standortcode, Postleitzahl und Region.

Diese Dateien werden über die GitHub-Raw-URLs geladen und können unabhängig von der App selbst aktualisiert werden.

## 🚀 Erste Schritte & Nutzung

1.  **App öffnen:** Rufe die Seite über den bereitgestellten Link auf oder installiere sie als PWA.
2.  **Standort wählen:** Wähle im Header den gewünschten ASZ-Standort aus der dynamisch geladenen Liste.
3.  **Artikel auswählen:** Suche den gewünschten Artikel entweder über die **Art.Nr.** (numerisch gruppiert) oder die **Bezeichnung** (alphabetisch gruppiert).
4.  **Drucklayout anpassen (optional):**
    *   Klicke auf das Vorschaubild, um den interaktiven A4-Druckbogen zu öffnen.
    *   Klicke auf beliebige Positionen im Bogen, um Etiketten hinzuzufügen oder zu entfernen.
5.  **Drucken:** Klicke auf den Haupt-Button **"Jetzt Drucken"**, um den A4-Bogen mit deinen Etiketten zu drucken.

## ⚙️ Anpassung der Datenbank (CRUD)

Über den **"Optionen"**-Button kannst du auf den integrierten Datenbank-Manager zugreifen:

*   **Sortiment wählen:** Zeigt die aktuelle Artikelliste an.
*   **Datenbank verwalten:** Hier kannst du:
    *   Neue Artikel hinzufügen.
    *   Bestehende Artikel bearbeiten oder löschen.
    *   Die gesamte Datenbank als JSON-Datei exportieren.
*   **Standard sichern:** Speichert die aktuellen Einstellungen (Standort, Format, Anzahl, Startposition) als Standard im Browser.

## 🔧 Technische Details & Entwicklung

*   **Sprache:** Reines HTML, CSS und JavaScript (ES6+).
*   **Speicherung:** Verwendet `localStorage` für benutzerspezifische Einstellungen, den Sortiments-Cache und den Standort-Cache.
*   **Netzwerk:** Nutzt die `fetch`-API mit "no-store"-Cache-Strategie für die JSON-Daten, um immer aktuelle Daten zu priorisieren.
*   **Service Worker:** Der `sw.js` implementiert eine **Network-First-Strategie** für die JSON-Datenbanken und eine **Cache-First-Strategie** für statische Assets, was eine robuste Offline-Nutzung ermöglicht.
*   **Ordnerstruktur:** Die Hauptanwendung befindet sich im `/`-Ordner, alle Assets (Icons, Bilder) im `/assets/`-Ordner. Eine `index.html` im Root leitet auf die App weiter.

## 🤝 Beitrag leisten

Beiträge sind willkommen! Bitte beachte die folgenden Punkte:

1.  Forke das Repository.
2.  Erstelle einen neuen Branch für dein Feature (`git checkout -b feature/neues-feature`).
3.  Committe deine Änderungen (`git commit -m 'feat: Neues Feature hinzugefügt'`).
4.  Pushe den Branch (`git push origin feature/neues-feature`).
5.  Erstelle einen Pull Request.

**Wichtige Hinweise für Änderungen an den JSON-Datenbanken:**

*   Stelle sicher, dass die JSON-Struktur gültig ist.
*   Teste die Änderungen lokal, bevor du sie in den Hauptbranch mergst.

## 📄 Lizenz

Dieses Projekt ist Open Source und steht unter der [MIT-Lizenz](LICENSE).