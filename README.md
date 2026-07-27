## 🚀 Introduction

**RE:PRINT Studio v9** is a lightweight, client-side Progressive Web Application (PWA) designed for ASZ branch locations in Upper Austria. It provides dynamic label formatting, live print preview calculations, and customizable template sheet rendering for standard HERMA A4 templates.

The application operates entirely in the browser, leveraging modern web technologies to deliver a seamless experience across desktop and mobile devices, with robust offline capabilities.

## ⚠️ Disclaimer / Rechtlicher Hinweis

> **Important Notice / Disclaimer:**
> 
> **This software is an independent community project and is not officially affiliated with LAVU OÖ (Upper Austrian State Waste Management Company) or the district waste management associations (BAV OÖ).**
> 
> **This is not an official application or software of LAVU OÖ or BAV OÖ. All trademarks, logos, and designations belong to their respective owners.**
> 
> **Notice:**
> 
> **This application is an independent open-source project and is not officially affiliated with, endorsed by, or sponsored by LAVU OÖ or BAV OÖ.**

<hr>

## 🔧 Technical Details & Development

* **Language:** Pure HTML, CSS, and JavaScript (ES6+).
* **Storage:** Uses `localStorage` for user-specific settings, the assortment cache, and the location cache.
* **Network:** Uses the `fetch` API with a "no-store" cache strategy for JSON data to always prioritize the most up-to-date data.
* **Service Worker:** The `sw.js` implements a **network-first strategy** for JSON databases and a **cache-first strategy** for static assets, enabling robust offline use.
* **Folder Structure:** The main application is located in the `/` folder, and all assets (icons, images) are in the `/assets/` folder. An `index.html` file in the root directory redirects to the app.

<hr>

## 📦 External Data Sources (JSON) / Externe Datenquellen (JSON)

[en] The app retrieves its dynamic data from two central JSON files maintained in this repository:
[de] Die App bezieht ihre dynamischen Daten aus zwei zentralen JSON-Dateien, die in diesem Repository gepflegt werden:

1. [en] `sortiment.json` – Contains the product assortment with product number, description, and optional packaging suffix.
   [de] `sortiment.json` – Enthält das Artikel-Sortiment mit Artikelnnummer, Bezeichnung und optionalem Gebinde-Suffix.
2. [en] `locations.json` – Contains the list of recycling center locations with name, location code, postal code, and region.
   [de] `locations.json` – Enthält die Liste der ASZ-Standorte mit Name, Standortcode, Postleitzahl und Region.

[en] These files are loaded via the GitHub raw URLs and can be updated independently of the app itself.
[de] Diese Dateien werden über die GitHub-Raw-URLs geladen und können unabhängig von der App selbst aktualisiert werden.

---

## 🚀 Getting Started & Usage / Erste Schritte & Nutzung

[en] 1. Open the App: Access the page via the provided link or install it as a PWA.
[de] 1. App öffnen: Rufe die Seite über den bereitgestellten Link auf oder installiere sie als PWA.

[en] 2. Select a Location: Select the desired recycling center location from the dynamically loaded list in the header.
[de] 2. Standort wählen: Wähle im Header den gewünschten ASZ-Standort aus der dynamisch geladenen Liste.

[en] 3. Select Item: Search for the desired item either by **Item No.** (numerically grouped) or **Description** (alphabetically grouped).
[de] 3. Artikel auswählen: Suche den gewünschten Artikel entweder über die **Art.Nr.** (numerisch gruppiert) oder die **Bezeichnung** (alphabetisch gruppiert).

[en] 4. Adjust Print Layout (Optional): Click on the preview image to open the interactive A4 print sheet. Click on any position on the sheet to add or remove labels.
[de] 4. Drucklayout anpassen (optional): Klicke auf das Vorschaubild, um den interaktiven A4-Druckbogen zu öffnen. Klicke auf beliebige Positionen im Bogen, um Etiketten hinzuzufügen oder zu entfernen.

[en] 5. Print: Click the main **"Print Now"** button to print the A4 sheet with your labels.
[de] 5. Drucken: Klicke auf den Haupt-Button **"Jetzt Drucken"**, um den A4-Bogen mit deinen Etiketten zu drucken.

---

## ⚙️ Database Customization (CRUD) / Anpassung der Datenbank (CRUD)

[en] You can access the integrated database manager via the **"Options"** button:
[de] Über den **"Optionen"**-Button kannst du auf den integrierten Datenbank-Manager zugreifen:

[en] * Select Product Range: Displays the current product list.
[de] * Sortiment wählen: Zeigt die aktuelle Artikelliste an.

[en] * Manage Database: Here you can add new items, edit or delete existing items, and export the entire database as a JSON file.
[de] * Datenbank verwalten: Hier kannst du neue Artikel hinzufügen, bestehende Artikel bearbeiten oder löschen, und die gesamte Datenbank als JSON-Datei exportieren.

[en] * Save Defaults: Saves the current settings (location, format, quantity, starting position) as the browser default.
[de] * Standard sichern: Speichert die aktuellen Einstellungen (Standort, Format, Anzahl, Startposition) als Standard im Browser.

---

## 🤝 Contribute / Beitrag leisten

[en] Contributions are welcome! Please note the following points:
[de] Beiträge sind willkommen! Bitte beachte die folgenden Punkte:

[en] 1. Fork the repository.
[de] 1. Forke das Repository.

[en] 2. Create a new branch for your feature (`git checkout -b feature/new-feature`).
[de] 2. Erstelle einen neuen Branch für dein Feature (`git checkout -b feature/neues-feature`).

[en] 3. Commit your changes (`git commit -m 'feat: New feature added'`).
[de] 3. Committe deine Änderungen (`git commit -m 'feat: Neues Feature hinzugefügt'`).

[en] 4. Push the branch (`git push origin feature/new-feature`).
[de] 4. Pushe den Branch (`git push origin feature/neues-feature`).

[en] 5. Create a pull request.
[de] 5. Erstelle einen Pull Request.

[en] Important notes for changes to the JSON databases: Ensure the JSON structure is valid. Test the changes locally before merging them into the main branch.
[de] Wichtige Hinweise für Änderungen an den JSON-Datenbanken: Stelle sicher, dass die JSON-Struktur gültig ist. Teste die Änderungen lokal, bevor du sie in den Hauptbranch mergst.

---

## 📄 License / Lizenz

[en] This project is open source and is licensed under the MIT License.
[de] Dieses Projekt ist Open Source und steht unter der MIT-Lizenz.


