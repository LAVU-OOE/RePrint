# RE:PRINT Studio v9

<div id="tldr-summary"></div>

<details>
<summary><b>⚡ TL;DR / (Quick Overview)</b></summary>

> **🇬🇧 English:** Quick summary of what this tool does, how it works, and how to use it instantly.

---

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

---

> **🇦🇹 Deutsch:** Schnelle Zusammenfassung, was dieses Tool macht, wie es funktioniert und wie man es sofort nutzt.
> 

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

---

</details>

---

## RE:PRINT Studio v9

## 📖 Table of Contents

1.  [Introduction](https://gemini.google.com/#-introduction "null")
    
2.  [Disclaimer / Rechtlicher Hinweis](https://gemini.google.com/#-disclaimer--rechtlicher-hinweis "null")
    
3.  [System Overview](https://gemini.google.com/#-system-overview "null")
    
4.  [Architecture](https://gemini.google.com/#-architecture "null")
    
    *   [Client-Side Core](https://gemini.google.com/#client-side-core "null")
        
    *   [Cloudflare Workers Integration](https://gemini.google.com/#cloudflare-workers-integration "null")
        
    *   [Service Worker & Offline Strategy](https://gemini.google.com/#service-worker--offline-strategy "null")
        
    *   [API Fetch & Cache Fallback Sequence](https://gemini.google.com/#api-fetch--cache-fallback-sequence "null")
        
5.  [Label Design & Rendering Engine](https://gemini.google.com/#-label-design--rendering-engine "null")
    
    *   [Grid Geometry Calculation](https://gemini.google.com/#grid-geometry-calculation "null")
        
    *   [Dynamic Scaling](https://gemini.google.com/#dynamic-scaling "null")
        
    *   [Interactive Sheet Preview](https://gemini.google.com/#interactive-sheet-preview "null")
        
6.  [Data Flow & Workflow Diagrams](https://gemini.google.com/#-data-flow--workflow-diagrams "null")
    
7.  [Key Features](https://gemini.google.com/#-key-features "null")
    
8.  [Technical Specifications](https://gemini.google.com/#-technical-specifications "null")
    
9.  [Printing Instructions](https://gemini.google.com/#-printing-instructions "null")
    
10.  [Quick Start](https://gemini.google.com/#-quick-start "null")
     
11.  [Project Structure](https://gemini.google.com/#-project-structure "null")
     
12.  [Database Management](https://gemini.google.com/#-database-management "null")
     
13.  [Contribution Guidelines](https://gemini.google.com/#-contribution-guidelines "null")
     
14.  [License](https://gemini.google.com/#-license "null")
     

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

## 🏗 System Overview

RE:PRINT Studio v9 is built on a **serverless architecture** that combines:

*   **Pure client-side rendering** using HTML5, CSS3, and vanilla JavaScript (ES6+)
    
*   **Cloudflare Workers** for API endpoints serving dynamic JSON data
    
*   **Service Workers** for progressive enhancement and offline support
    
*   **localStorage** for client-side persistence of user preferences and cached data
    

### System Context Diagram

```
flowchart TB
    subgraph Client ["Browser Client (PWA)"]
        UI["🎨 UI Engine<br/>(index.html)"]
        SW["⚙️ Service Worker<br/>(sw.js)"]
        LS["💾 localStorage<br/>Cache & Settings"]
    end

    subgraph Cloudflare ["Cloudflare Workers Edge Network"]
        SA["📦 Sortiment API<br/>/sortiment-api"]
        LA["📍 Locations API<br/>/locations-api"]
    end

    subgraph External ["External Assets & Registry"]
        TEMPLATES["📄 HERMA Templates<br/>(herma_templates.json)"]
        GITHUB["🌐 GitHub Pages<br/>Static Assets"]
    end

    UI -->|fetch| SA
    UI -->|fetch| LA
    UI -->|fetch| TEMPLATES
    SW -->|Cache Strategy| GITHUB
    UI -->|Read/Write| LS
    SW -->|Network-First Cache| SA
    SW -->|Network-First Cache| LA

```

## 🏛 Architecture

### Client-Side Core

The application's core is contained within a single `index.html` file, which includes:

1.  **Template Registry Engine** – Loads and parses `herma_templates.json`
    
2.  **Dynamic Dropdown System** – Grouped by numeric ranges and alphabetical letters
    
3.  **Interactive Grid Renderer** – Renders A4 sheets with click-to-toggle functionality
    
4.  **i18n Runtime** – Bilingual support with seamless switching
    
5.  **CRUD Database Manager** – In-browser data management with JSON export
    

### Cloudflare Workers Integration

The application interfaces with two primary Cloudflare Worker endpoints:

#### 1\. Sortiment API (`sortiment-api.lavu-ooe.workers.dev`)

Returns the product catalog in JSON format:

```
[
  {
    "artNr": "4040",
    "bez": "Elektro-Kleingeräte",
    "geb": "QR-Box"  
  }
]

```

**Worker Implementation Snippet:**

```
export default {
  async fetch(request) {
    const CORS_HEADERS = {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, OPTIONS',
      'Content-Type': 'application/json'
    };
    try {
      const data = await SORTIMENT_KV.get('sortiment', 'json');
      return new Response(JSON.stringify(data), { headers: CORS_HEADERS });
    } catch (error) {
      return new Response(
        JSON.stringify({ error: 'Failed to fetch sortiment data' }),
        { status: 500, headers: CORS_HEADERS }
      );
    }
  }
}

```

#### 2\. Locations API (`locations-api.lavu-ooe.workers.dev`)

Returns the list of ASZ branch locations:

```
[
  {
    "siteCode": "106",
    "name": "ASZ Asten",
    "zipCode": "4481",
    "region": "Linz-Land & Linz Stadt"
  }
]

```

**Worker Implementation Snippet:**

```
export default {
  async fetch(request) {
    const CORS_HEADERS = {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, OPTIONS',
      'Content-Type': 'application/json'
    };
    try {
      const locations = await LOCATIONS_KV.get('locations', 'json');
      return new Response(JSON.stringify(locations), { headers: CORS_HEADERS });
    } catch (error) {
      return new Response(
        JSON.stringify({ error: 'Failed to fetch locations data' }),
        { status: 500, headers: CORS_HEADERS }
      );
    }
  }
}

```

### Service Worker & Offline Strategy

The Service Worker implements a **Network-First** strategy for dynamic JSON data and a **Cache-First** strategy for static assets.

#### Registration & Installation

```
const CACHE_NAME = 'lavu-studio-v10';
const STATIC_ASSETS = [
  '.',
  'index.html',
  'manifest.json',
  'favicon.svg',
  'logo.png',
  'favicon-96x96.png',
  'apple-touch-icon.png',
  'web-app-manifest-192x192.png',
  'web-app-manifest-512x512.png'
];
const DYNAMIC_JSON_URLS = [
  'https://locations-api.lavu-ooe.workers.dev/',
  'https://sortiment-api.lavu-ooe.workers.dev/'
];

self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll([...STATIC_ASSETS, ...DYNAMIC_JSON_URLS]))
      .then(() => self.skipWaiting())
  );
});

```

#### Fetch Strategy for JSON Endpoints

```
if (DYNAMIC_JSON_URLS.some(jsonUrl => url.href === jsonUrl)) {
  event.respondWith(
    fetch(request, { cache: 'no-store' })
      .then(response => {
        const clonedResponse = response.clone();
        caches.open(CACHE_NAME)
          .then(cache => cache.put(request, clonedResponse));
        return response;
      })
      .catch(() => {
        return caches.match(request)
          .then(cachedResponse => {
            if (cachedResponse) {
              console.log('[SW] Serving JSON from cache');
              return cachedResponse;
            }
            return new Response(
              JSON.stringify({ error: 'Offline - Data not available' }),
              { status: 503, headers: { 'Content-Type': 'application/json' } }
            );
          });
      })
  );
  return;
}

```

#### Offline Fallback for Navigation

```
if (request.mode === 'navigate') {
  event.respondWith(
    fetch(request)
      .then(response => {
        const clonedResponse = response.clone();
        caches.open(CACHE_NAME)
          .then(cache => cache.put(request, clonedResponse));
        return response;
      })
      .catch(() => {
        return caches.match('/index.html')
          .then(cachedResponse => {
            if (cachedResponse) {
              console.log('[SW] Serving offline fallback page');
              return cachedResponse;
            }
            return new Response(
              '<html><body><h1>Offline</h1><p>Bitte verbinden Sie sich mit dem Internet, um die App zu nutzen.</p></body></html>',
              { headers: { 'Content-Type': 'text/html' } }
            );
          });
      })
  );
  return;
}

```

### API Fetch & Cache Fallback Sequence

```
sequenceDiagram
    autonumber
    actor User as 👤 User
    participant UI as 🖥️ Client UI (index.html)
    participant SW as ⚙️ Service Worker
    participant Cache as 💾 Cache / localStorage
    participant API as ☁️ Cloudflare Worker API

    User->>UI: Selects Location / Sortiment Item
    UI->>SW: fetch(API Endpoint)
    
    alt Network Online
        SW->>API: HTTP GET /locations-api or /sortiment-api
        API-->>SW: 200 OK (JSON Payload)
        SW->>Cache: Update Cache Entry
        SW-->>UI: Return fresh JSON Response
    else Network Offline / Fetch Error
        SW->>Cache: Match Cached Request
        alt Cache Hit
            Cache-->>SW: Return Cached JSON
            SW-->>UI: Return Cached JSON (Offline Mode)
        else Cache Miss
            SW-->>UI: 503 Service Unavailable (Fallback Payload)
        end
    end
    
    UI->>User: Render Interactive Grid & Label Preview

```

## 🎨 Label Design & Rendering Engine

The core rendering engine transforms HERMA template definitions into interactive A4 sheets with precise geometric calculations.

### Grid Geometry Calculation

The label renderer computes dynamic layout geometry based on template parameters declared in `herma_templates.json`.

#### Mathematical Foundation

Where:

|

| **Variable** | **Description** | | | Number of Columns (`cols`) | | | Number of Rows (`rows`) | | | Label Width in Millimeters | | | Label Height in Millimeters | | | Horizontal and Vertical Gaps in Millimeters |

#### Template Structure (`herma_templates.json`)

```
{
  "engine": "HERMA Label Engine",
  "page_format": {
    "size": "A4",
    "width_mm": 210.0,
    "height_mm": 297.0,
    "orientation": "portrait"
  },
  "templates": [
    {
      "sku": "4473",
      "category": "MEDIUM",
      "cols": 3,
      "rows": 7,
      "width_mm": 70.0,
      "height_mm": 41.0,
      "round": false,
      "top_margin_mm": 10.0,
      "left_margin_mm": 0.0,
      "gap_x_mm": 0.0,
      "gap_y_mm": 0.0
    }
  ]
}

```

#### Grid Rendering Function

```
function r2(containerId, data) {
  const container = document.getElementById(containerId);
  const t = templateRegistry[currentFormatKey];
  
  const totalGridWidth = t.cols * t.width_mm + (t.cols - 1) * t.gap_x_mm;
  const totalGridHeight = t.rows * t.height_mm + (t.rows - 1) * t.gap_y_mm;
  
  const rightMargin = 210 - totalGridWidth - t.left_margin_mm;
  const bottomMargin = 297 - totalGridHeight - t.top_margin_mm;
  
  container.style.padding = `
    ${t.top_margin_mm}mm 
    ${Math.max(0, rightMargin)}mm 
    ${Math.max(0, bottomMargin)}mm 
    ${t.left_margin_mm}mm
  `;
  
  container.style.gridTemplateColumns = `repeat(${t.cols}, ${t.width_mm}mm)`;
  container.style.gridTemplateRows = `repeat(${t.rows}, ${t.height_mm}mm)`;
  
  for (let i = 1; i <= maxLabels; i++) {
    const label = document.createElement('div');
    label.className = 'lb';
    if (i >= start && i < start + count) {
      label.innerHTML = `
        <div class="lbt">${data.topText || '&nbsp;'}</div>
        <div class="lbm">
          <div class="lba">${data.artNr || '&nbsp;'}</div>
          ${data.suffix ? `<div class="lbs">${data.suffix}</div>` : ''}
        </div>
        <div class="lbb">${data.bezeichnung || '&nbsp;'}</div>
        <div class="lbf">https://lavu-ooe.github.io/</div>
      `;
    } else {
      label.className += ' e'; 
    }
    container.appendChild(label);
  }
}

```

### Dynamic Scaling

To prevent CSS layout breakage inside preview cards, scale vectors are calculated as dynamic inline properties:

```
const baseWidth = 70;   
const baseHeight = 41;  
const scaleX = t.width_mm / baseWidth;
const scaleY = t.height_mm / baseHeight;
const scale = Math.min(scaleX, scaleY, 1);
container.style.setProperty('--label-scale', scale);

```

### Interactive Sheet Preview

The modal preview allows users to click on individual label positions to toggle their state:

```
function toggleLabel(clickedIndex) {
  const t = templateRegistry[currentFormatKey];
  const maxLabels = t.cols * t.rows;
  let count = parseInt(document.getElementById('i2').value) || 0;
  let start = parseInt(document.getElementById('i3').value) || 1;
  let end = start + count - 1;
  
  if (count === 0) {
    start = clickedIndex;
    count = 1;
  } else if (clickedIndex < start) {
    count = end - clickedIndex + 1;
    start = clickedIndex;
  } else if (clickedIndex > end) {
    count = clickedIndex - start + 1;
  } else {
    start = clickedIndex;
    count = 1;
  }
  
  document.getElementById('i2').value = count;
  document.getElementById('i3').value = start;
  u1(); 
}

```

## 📊 Data Flow & Workflow Diagrams

### Complete Application Workflow

\`\`\`xml

\`\`\`

```
flowchart TD
    A["🚀 User Opens App"] --> B{"🔍 Check localStorage"}
    B -- Cache Exists --> C["📦 Load Cached Data"]
    B -- No Cache --> D["☁️ Fetch from Cloudflare Workers"]
    C --> E["📋 Populate Dropdowns"]
    D --> E
    
    E --> F["📍 User Selects Location"]
    F --> G["🏷️ User Selects Product"]
    G --> H["👁️ Render Live Preview"]
    
    H --> I{"⚡ User Action"}
    I -- Click Preview --> J["🖼️ Open Interactive Sheet Modal"]
    J --> K["🖱️ Click Label Positions"]
    K --> L["🔄 Toggle Label State"]
    L --> M["✏️ Update Count & Start Position"]
    M --> N["🎨 Re-render Sheet Layout"]
    
    I -- Print Now --> O["🖨️ Open Browser Print Dialog"]
    O --> P["📄 Output Printed A4 Sheet"]
    
    I -- Options --> Q["⚙️ Open Settings Modal"]
    Q --> R{"📂 Select Tab"}
    R -- Service Worker --> S["🌐 Manage API Endpoints"]
    S --> T["✏️ Update Sortiment Endpoint"]
    S --> U["✏️ Update Locations Endpoint"]
    
    R -- Database --> V["🗄️ CRUD Operations"]
    V --> W["➕ Add / Edit / Delete Items"]
    W --> X["💾 Save to localStorage"]
    X --> E
    V --> Y["📥 Export Database JSON"]

```

### Label Design Workflow

```
flowchart LR
    subgraph Input ["1. Data Input"]
        A1["📄 Select HERMA SKU"] --> A2["⚙️ Load Geometry Specs"]
        B1["📍 Select Location"] --> B2["🏷️ Get Header Label"]
        C1["📦 Select Product"] --> C2["🔢 Get ArtNr & Description"]
        D1["✍️ Enter Suffix"] --> D2["🏷️ Optional Badge"]
        E1["🔢 Count & Start Position"]
    end

    subgraph Rendering ["2. Rendering Engine"]
        A2 --> F["📐 Compute Dynamic Grid"]
        B2 --> F
        C2 --> F
        D2 --> F
        E1 --> F
        F --> G1["✨ Render Active Cells"]
        F --> G2["⚪ Render Empty Cells"]
        G1 --> H["🖼️ Composite Preview Sheet"]
        G2 --> H
    end

    subgraph Interaction ["3. Interactive Editing"]
        H --> I["🖥️ Interactive Modal View"]
        I --> J["🖱️ Click Cell"]
        J --> K["🔄 Re-calculate Offsets"]
        K --> H
    end

    subgraph Output ["4. Print Output"]
        H --> L["🖨️ Execute Print Job"]
        L --> M["📄 Render A4 Vector Graphics"]
        M --> N["🏷️ Physical Sheet Printed"]
    end

```

### Application State Lifecycle

```
stateDiagram-v2
    [*] --> Uninitialized

    state Uninitialized {
        [*] --> RegisterServiceWorker
        RegisterServiceWorker --> CheckCache
    }

    Uninitialized --> Ready : Resources & Data Loaded

    state Ready {
        [*] --> Standby
        Standby --> LocationSelected : Select ASZ Branch
        LocationSelected --> ItemSelected : Select Product Item
        ItemSelected --> GridCalculated : Compute Geometry
        GridCalculated --> LivePreview : Render CSS Grid
    }

    Ready --> ModalEditing : Click Sheet Preview
    
    state ModalEditing {
        [*] --> ModalOpen
        ModalOpen --> ToggleCell : Click Grid Cell
        ToggleCell --> RecalculateOffset : Update Start/Count
        RecalculateOffset --> ModalOpen : Redraw Sheet
        ModalOpen --> ModalClosed : Close Modal
    }

    ModalEditing --> Ready : Return to Main UI
    Ready --> Printing : Click "Print Now"
    Printing --> Ready : Close Print View

```

## 🌟 Key Features

### 1\. Dynamic HERMA Sheet Engine

*   **Interactive click-to-toggle** sheet positioning on standard A4 grids
    
*   **Real-time preview** with automatic recalculation
    
*   Support for **rectangular and round** label templates
    

### 2\. Serverless & Offline First

*   Uses **Cloudflare Workers** for API endpoints
    
*   Falls back to **cached browser state** (`localStorage`)
    
*   **Service Worker** provides offline capability with network-first strategy
    

### 3\. Bilingual Support (i18n)

*   Native runtime switching between **German (`de`)** and **English (`en`)**
    
*   Persistent language preference stored in `localStorage`
    

### 4\. Cross-Device Responsive UI

*   **Mobile-optimized layout** switching for templates and location selectors
    
*   **Adaptive breakpoints** at 768px and 520px
    
*   Touch-optimized interactive elements
    

### 5\. PWA Capable

*   **Offline support** with service worker
    
*   **Manifest-driven install prompts** on compatible browsers
    
*   **Standalone display** configuration for app-like experience
    

### 6\. Database Management

*   **In-browser CRUD operations** for product database
    
*   **JSON export** functionality
    
*   **Auto-sync** between localStorage and UI
    

## 🔧 Technical Specifications

### Storage & Persistence Schema

| **Storage Key** | **Type** | **Description** | | `lavu_lang` | `string` | Selected i18n locale (`de` | `en`) | | `lavu_location` | `string` | Currently selected Site Code ID (e.g. `"106"`) | | `lavu_locations_url` | `string` | Remote Worker endpoint for locations | | `lavu_locations_cache` | `string` (JSON) | Cached locations list payload | | `lavu_studio_defaults_v8` | `string` (JSON) | Last known SKU format, count, and position offset | | `lavu_studio_sortiment_v8` | `string` (JSON) | Locally edited database workspace | | `lavu_preview_zoom` | `string` | Zoom level for modal preview |

### Media Query Breakpoint Matrix

| **Viewport Width** | **Visual Adjustments** | | **\> 768px** | Full dual-pane preview desktop layout with interactive sheet modal | | **<= 768px** | Hides side panel live preview (`.ps-wrapper`). Switches to single-column flow | | **<= 520px** | Hides desktop header location badges (`.hdr-r`). Activates mobile location select control (`.mobile-location-wrapper`) |

### Performance Metrics

```
console.time('renderGrid');
r2('mdl', data);
console.timeEnd('renderGrid');

```

## 🖨 Printing Instructions

For optimal print results, follow these settings in your browser's print dialog:

1.  **Scale:** Set to **100% / Actual Size**
    
2.  **Margins:** Set to **None** or **0mm**
    
3.  **Paper Size:** Force selection to **A4 Portrait**
    
4.  **Background Graphics:** Enable if you want to see the grid lines
    

### Print Preview Code

```
document.getElementById('btn-print-now').addEventListener('click', function () {
  if (window.innerWidth <= 768) {
    o1();
  } else {
    window.print();
  }
});

```

### Print-Specific CSS

```
@media print {
  @page {
    size: A4 portrait;
    margin: 0 !important;
  }
  
  #hpc .pc {
    display: grid !important;
    gap: 0 !important;
    padding: 5mm 2mm !important;
    width: 210mm !important;
    height: 297mm !important;
    box-shadow: none !important;
    transform: none !important;
  }
  
  #hpc .lb {
    display: flex !important;
    flex-direction: column !important;
    border: 0.5px solid #ccc !important;
    padding: 2.5mm 3.5mm !important;
    break-inside: avoid !important;
  }
}

```

## 🚀 Quick Start

### Installation & Setup

1.  **Clone or download the repository**
    
    ```
    git clone https://github.com/LAVU-OOE/RePrint.git
    cd RePrint
    
    ```
    
2.  **Host via any static site server**
    
    ```
    python3 -m http.server 8080
    # OR
    npx http-server .
    # OR
    php -S localhost:8080
    
    ```
    
3.  **Open in your browser**
    
    ```
    http://localhost:8080
    
    ```
    

### First-Time Usage

1.  **Select a Location** – Choose your ASZ branch from the dynamically loaded dropdown
    
2.  **Select an Item** – Search by either **Item No.** (numerically grouped) or **Description** (alphabetically grouped)
    
3.  **Adjust Print Layout** – Click the preview image to open the interactive sheet
    
4.  **Print** – Click "Print Now" to generate your A4 sheet
    

## 📁 Project Structure

```
.
├── 📄 index.html                  # Main SPA UI container & CSS layout engine
├── 📄 herma_templates.json        # A4 Grid registry definitions
├── 📄 manifest.json               # Web App Manifest for PWA installation
├── 📄 site.webmanifest            # Secondary app manifest definition
├── 📄 sw.js                       # Service Worker for offline support
├── 📄 README.md                   # Application documentation
├── 📄 LICENSE                     # MIT License
├── 🖼️ favicon.svg                 # Scalable Vector Graphics icon
├── 🖼️ favicon-96x96.png           # Static icon raster asset
├── 🖼️ logo.png                    # Application logo
├── 🖼️ apple-touch-icon.png        # Apple iOS icon
├── 🖼️ web-app-manifest-192x192.png # PWA icon (192px)
├── 🖼️ web-app-manifest-512x512.png # PWA icon (512px)
└── 📄 tree.md                     # File structure documentation

```

## 🗄 Database Management

### In-Browser CRUD Operations

The application includes a built-in database manager accessible via the **"Options"** button:

```
function s3() {
  const c1 = document.getElementById('c1').value.trim(); 
  const c2 = document.getElementById('c2').value.trim(); 
  const c3 = document.getElementById('c3').value.trim(); 
  
  if (!c1 || !c3) {
    alert(t.alertFillForm);
    return;
  }
  
  if (a2.some(item => item.artNr === c1)) {
    alert(t.alertDuplicate);
    return;
  }
  
  a2.push({ artNr: c1, geb: c2 || '-', bez: c3 });
  localStorage.setItem('lavu_studio_sortiment_v8', JSON.stringify(a2));
  i1(); 
  e1(); 
  u1(); 
}

function s4() {
  const index = document.getElementById('e1').value;
  const c1 = document.getElementById('c1').value.trim();
  const c2 = document.getElementById('c2').value.trim();
  const c3 = document.getElementById('c3').value.trim();
  
  a2[index] = { artNr: c1, geb: c2, bez: c3 };
  localStorage.setItem('lavu_studio_sortiment_v8', JSON.stringify(a2));
  i1();
  e1();
  u1();
}

function d1(index) {
  if (confirm(t.confirmDelete)) {
    a2.splice(index, 1);
    localStorage.setItem('lavu_studio_sortiment_v8', JSON.stringify(a2));
    i1();
    u1();
  }
}

```

### Export Database as JSON

```
function e2() {
  const jsonData = JSON.stringify(a2, null, 2);
  const blob = new Blob([jsonData], { type: "application/json" });
  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');
  link.href = url;
  link.download = "sortiment_export.json";
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
  URL.revokeObjectURL(url);
}

```

### Saving Defaults

```
function s7() {
  const data = g1();
  const config = {
    formatKey: currentFormatKey,
    topText: document.getElementById('i1').value,
    count: data.count,
    startPos: data.startPos,
    artNr: data.artNr,
    suffix: data.suffix,
    bezeichnung: data.bezeichnung,
    sortimentIndex: data.sortimentIndex
  };
  localStorage.setItem('lavu_studio_defaults_v8', JSON.stringify(config));
  localStorage.setItem('lavu_location', document.getElementById('i1').value);
}

```

## 🤝 Contribution Guidelines

### Development Setup

1.  **Fork the repository**
    
2.  **Create a feature branch**
    
    ```
    git checkout -b feature/your-feature-name
    
    ```
    
3.  **Make your changes**
    
4.  **Test locally** – Ensure the application runs without errors
    
5.  **Commit with conventional commit messages**
    
    ```
    git commit -m "feat: Add support for new HERMA template SKU"
    git commit -m "fix: Resolve mobile layout issues on Safari"
    git commit -m "docs: Update README with new Cloudflare API endpoints"
    
    ```
    
6.  **Push and create a pull request**
    

### Testing Guidelines

*   **Cross-browser testing**: Chrome, Firefox, Safari, Edge
    
*   **Mobile testing**: iOS Safari, Android Chrome
    
*   **Offline testing**: Disable network and verify cached functionality
    
*   **Print testing**: Verify A4 output with different printer configurations
    

### Code Standards

*   **ES6+** JavaScript with `const` and `let`
    
*   **CSS variables** for theming
    
*   **Semantic HTML5** elements
    
*   **Progressive enhancement** principles
    

## 📄 License

This project is open source and is licensed under the **MIT License**.

```
MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```

*Independent open-source project*

---

<details>
<summary><b>🇦🇹 Click here to switch to German / Auf Deutsch umschalten</b></summary>

<div id="german-version">

---

## RE:PRINT Studio v9

## 📖 Inhaltsverzeichnis

1.  [Einführung](https://gemini.google.com/#-einf%C3%BChrung "null")
    
2.  [Haftungsausschluss / Rechtlicher Hinweis](https://gemini.google.com/#-haftungsausschluss--rechtlicher-hinweis "null")
    
3.  [Systemübersicht](https://gemini.google.com/#-system%C3%BCbersicht "null")
    
4.  [Architektur](https://gemini.google.com/#-architektur "null")
    
    *   [Client-Seitiger Kern](https://gemini.google.com/#client-seitiger-kern "null")
        
    *   [Cloudflare Workers Integration](https://gemini.google.com/#cloudflare-workers-integration "null")
        
    *   [Service Worker & Offline Strategie](https://gemini.google.com/#service-worker--offline-strategie "null")
        
    *   [API Fetch & Cache Fallback Sequenz](https://gemini.google.com/#api-fetch--cache-fallback-sequenz "null")
        
5.  [Etikettendesign & Rendering Engine](https://gemini.google.com/#-etikettendesign--rendering-engine "null")
    
    *   [Berechnung der Rastergeometrie](https://gemini.google.com/#berechnung-der-rastergeometrie "null")
        
    *   [Dynamische Skalierung](https://gemini.google.com/#dynamische-skalierung "null")
        
    *   [Interaktive Bogenvorschau](https://gemini.google.com/#interaktive-bogenvorschau "null")
        
6.  [Datenfluss & Workflow Diagramme](https://gemini.google.com/#-datenfluss--workflow-diagramme "null")
    
7.  [Hauptfunktionen](https://gemini.google.com/#-hauptfunktionen "null")
    
8.  [Technische Spezifikationen](https://gemini.google.com/#-technische-spezifikationen "null")
    
9.  [Druckanleitung](https://gemini.google.com/#-druckanleitung "null")
    
10.  [Schnellstart](https://gemini.google.com/#-schnellstart "null")
     
11.  [Projektstruktur](https://gemini.google.com/#-projektstruktur "null")
     
12.  [Datenbankverwaltung](https://gemini.google.com/#-datenbankverwaltung "null")
     
13.  [Richtlinien für Mitwirkende](https://gemini.google.com/#-richtlinien-f%C3%BCr-mitwirkende "null")
     
14.  [Lizenz](https://gemini.google.com/#-lizenz "null")
     

## 🚀 Einführung

**RE:PRINT Studio v9** ist eine ressourcenschonende, clientseitige Progressive Web Application (PWA), die für ASZ-Standorte (Altstoffsammelzentren) in Oberösterreich entwickelt wurde. Sie bietet dynamische Etikettenformatierung, Live-Berechnungen der Druckvorschau und anpassbares Rendern von Vorlagenbögen für Standard-HERMA-A4-Etiketten.

Die Anwendung läuft vollständig im Browser und nutzt moderne Webtechnologien, um ein nahtloses Erlebnis über Desktop- und Mobilgeräte hinweg zu bieten, mit robusten Offline-Funktionen.

## ⚠️ Haftungsausschluss / Rechtlicher Hinweis

> **Wichtiger Hinweis / Haftungsausschluss:**
> 
> **Diese Software ist ein unabhängiges Community-Projekt und steht in keiner offiziellen Verbindung zur LAVU OÖ (OÖ. Landes-Abfallverwertungsunternehmen GmbH) oder den Bezirksabfallverbänden (BAV OÖ).**
> 
> **Dies ist keine offizielle Anwendung oder Software der LAVU OÖ oder des BAV OÖ. Alle Marken, Logos und Bezeichnungen gehören ihren jeweiligen Eigentümern.**
> 
> **Hinweis:**
> 
> **Diese Anwendung ist ein unabhängiges Open-Source-Projekt und wird von der LAVU OÖ oder dem BAV OÖ weder offiziell unterstützt noch gesponsert oder in irgendeiner Weise damit in Verbindung gebracht.**

## 🏗 Systemübersicht

RE:PRINT Studio v9 basiert auf einer **Serverless-Architektur**, die Folgendes kombiniert:

*   **Reines clientseitiges Rendering** mit HTML5, CSS3 und Vanilla JavaScript (ES6+)
    
*   **Cloudflare Workers** für API-Endpunkte, die dynamische JSON-Daten bereitstellen
    
*   **Service Workers** für progressive Verbesserung und Offline-Unterstützung
    
*   **localStorage** für die clientseitige Persistenz von Benutzereinstellungen und zwischengespeicherten Daten
    

### Systemkontextdiagramm

```
flowchart TB
    subgraph Client ["Browser Client (PWA)"]
        UI["🎨 UI Engine<br/>(index.html)"]
        SW["⚙️ Service Worker<br/>(sw.js)"]
        LS["💾 localStorage<br/>Cache & Einstellungen"]
    end

    subgraph Cloudflare ["Cloudflare Workers Edge Network"]
        SA["📦 Sortiment API<br/>/sortiment-api"]
        LA["📍 Locations API<br/>/locations-api"]
    end

    subgraph External ["Externe Assets & Registry"]
        TEMPLATES["📄 HERMA Templates<br/>(herma_templates.json)"]
        GITHUB["🌐 GitHub Pages<br/>Statische Assets"]
    end

    UI -->|fetch| SA
    UI -->|fetch| LA
    UI -->|fetch| TEMPLATES
    SW -->|Cache-Strategie| GITHUB
    UI -->|Lesen/Schreiben| LS
    SW -->|Network-First Cache| SA
    SW -->|Network-First Cache| LA
```

## 🏛 Architektur

### Client-Seitiger Kern

Der Kern der Anwendung ist in einer einzigen `index.html`\-Datei enthalten, die Folgendes umfasst:

1.  **Vorlagen-Registry-Engine** – Lädt und analysiert `herma_templates.json`
    
2.  **Dynamisches Dropdown-System** – Gruppiert nach Zahlenbereichen und alphabetischen Buchstaben
    
3.  **Interaktiver Raster-Renderer** – Rendert A4-Bögen mit Klick-zum-Umschalten-Funktionalität
    
4.  **i18n Runtime** – Zweisprachige Unterstützung mit nahtlosem Umschalten
    
5.  **CRUD-Datenbankmanager** – In-Browser-Datenverwaltung mit JSON-Export
    

### Cloudflare Workers Integration

Die Anwendung kommuniziert mit zwei primären Cloudflare-Worker-Endpunkten:

#### 1\. Sortiment API (`sortiment-api.lavu-ooe.workers.dev`)

Gibt den Produktkatalog im JSON-Format zurück:

```
[
  {
    "artNr": "4040",
    "bez": "Elektro-Kleingeräte",
    "geb": "QR-Box"  
  }
]
```

**Worker-Implementierungs-Snippet:**

```
export default {
  async fetch(request) {
    const CORS_HEADERS = {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, OPTIONS',
      'Content-Type': 'application/json'
    };
    try {
      const data = await SORTIMENT_KV.get('sortiment', 'json');
      return new Response(JSON.stringify(data), { headers: CORS_HEADERS });
    } catch (error) {
      return new Response(
        JSON.stringify({ error: 'Fehler beim Abrufen der Sortimentsdaten' }),
        { status: 500, headers: CORS_HEADERS }
      );
    }
  }
}
```

#### 2\. Locations API (`locations-api.lavu-ooe.workers.dev`)

Gibt die Liste der ASZ-Standorte zurück:

```
[
  {
    "siteCode": "106",
    "name": "ASZ Asten",
    "zipCode": "4481",
    "region": "Linz-Land & Linz Stadt"
  }
]
```

**Worker-Implementierungs-Snippet:**

```
export default {
  async fetch(request) {
    const CORS_HEADERS = {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, OPTIONS',
      'Content-Type': 'application/json'
    };
    try {
      const locations = await LOCATIONS_KV.get('locations', 'json');
      return new Response(JSON.stringify(locations), { headers: CORS_HEADERS });
    } catch (error) {
      return new Response(
        JSON.stringify({ error: 'Fehler beim Abrufen der Standortdaten' }),
        { status: 500, headers: CORS_HEADERS }
      );
    }
  }
}
```

### Service Worker & Offline-Strategie

Der Service Worker implementiert eine **Network-First**\-Strategie für dynamische JSON-Daten und eine **Cache-First**\-Strategie für statische Assets.

#### Registrierung & Installation

```
const CACHE_NAME = 'lavu-studio-v10';
const STATIC_ASSETS = [
  '.',
  'index.html',
  'manifest.json',
  'favicon.svg',
  'logo.png',
  'favicon-96x96.png',
  'apple-touch-icon.png',
  'web-app-manifest-192x192.png',
  'web-app-manifest-512x512.png'
];
const DYNAMIC_JSON_URLS = [
  'https://locations-api.lavu-ooe.workers.dev/',
  'https://sortiment-api.lavu-ooe.workers.dev/'
];

self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll([...STATIC_ASSETS, ...DYNAMIC_JSON_URLS]))
      .then(() => self.skipWaiting())
  );
});
```

#### Abrufstrategie für JSON-Endpunkte

```
if (DYNAMIC_JSON_URLS.some(jsonUrl => url.href === jsonUrl)) {
  event.respondWith(
    fetch(request, { cache: 'no-store' })
      .then(response => {
        const clonedResponse = response.clone();
        caches.open(CACHE_NAME)
          .then(cache => cache.put(request, clonedResponse));
        return response;
      })
      .catch(() => {
        return caches.match(request)
          .then(cachedResponse => {
            if (cachedResponse) {
              console.log('[SW] JSON wird aus dem Cache bereitgestellt');
              return cachedResponse;
            }
            return new Response(
              JSON.stringify({ error: 'Offline - Daten nicht verfügbar' }),
              { status: 503, headers: { 'Content-Type': 'application/json' } }
            );
          });
      })
  );
  return;
}
```

#### Offline-Fallback für die Navigation

```
if (request.mode === 'navigate') {
  event.respondWith(
    fetch(request)
      .then(response => {
        const clonedResponse = response.clone();
        caches.open(CACHE_NAME)
          .then(cache => cache.put(request, clonedResponse));
        return response;
      })
      .catch(() => {
        return caches.match('/index.html')
          .then(cachedResponse => {
            if (cachedResponse) {
              console.log('[SW] Offline-Fallback-Seite wird bereitgestellt');
              return cachedResponse;
            }
            return new Response(
              '<html><body><h1>Offline</h1><p>Bitte verbinden Sie sich mit dem Internet, um die App zu nutzen.</p></body></html>',
              { headers: { 'Content-Type': 'text/html' } }
            );
          });
      })
  );
  return;
}
```

### API Fetch & Cache Fallback Sequenz

```
sequenceDiagram
    autonumber
    actor User as 👤 Benutzer
    participant UI as 🖥️ Client UI (index.html)
    participant SW as ⚙️ Service Worker
    participant Cache as 💾 Cache / localStorage
    participant API as ☁️ Cloudflare Worker API

    User->>UI: Wählt Standort / Sortimentsartikel
    UI->>SW: fetch(API-Endpunkt)
    
    alt Netzwerk Online
        SW->>API: HTTP GET /locations-api oder /sortiment-api
        API-->>SW: 200 OK (JSON-Nutzdaten)
        SW->>Cache: Cache-Eintrag aktualisieren
        SW-->>UI: Neue JSON-Antwort zurückgeben
    else Netzwerk Offline / Abruffehler
        SW->>Cache: Zwischengespeicherte Anfrage abgleichen
        alt Cache-Treffer
            Cache-->>SW: Zwischengespeichertes JSON zurückgeben
            SW-->>UI: Zwischengespeichertes JSON zurückgeben (Offline-Modus)
        else Cache-Fehlschlag
            SW-->>UI: 503 Service Unavailable (Fallback-Nutzdaten)
        end
    end
    
    UI->>User: Interaktives Raster & Etikettenvorschau rendern
```

## 🎨 Etikettendesign & Rendering Engine

Die Kern-Rendering-Engine wandelt HERMA-Vorlagendefinitionen mit präzisen geometrischen Berechnungen in interaktive A4-Bögen um.

### Berechnung der Rastergeometrie

Der Etiketten-Renderer berechnet dynamische Layout-Geometrien basierend auf den Vorlagenparametern, die in `herma_templates.json` deklariert sind.

#### Mathematische Grundlage

Wobei:

| 
**Variable**

 | 

**Beschreibung**

 |
| --- | --- |
|  | 

Anzahl der Spalten (`cols`)

 |
|  | 

Anzahl der Zeilen (`rows`)

 |
|  | 

Etikettenbreite in Millimetern

 |
|  | 

Etikettenhöhe in Millimetern

 |
|  | 

Horizontale und vertikale Abstände in Millimetern

 |

#### Vorlagenstruktur (`herma_templates.json`)

```
{
  "engine": "HERMA Label Engine",
  "page_format": {
    "size": "A4",
    "width_mm": 210.0,
    "height_mm": 297.0,
    "orientation": "portrait"
  },
  "templates": [
    {
      "sku": "4473",
      "category": "MEDIUM",
      "cols": 3,
      "rows": 7,
      "width_mm": 70.0,
      "height_mm": 41.0,
      "round": false,
      "top_margin_mm": 10.0,
      "left_margin_mm": 0.0,
      "gap_x_mm": 0.0,
      "gap_y_mm": 0.0
    }
  ]
}
```

#### Raster-Rendering-Funktion

```
function r2(containerId, data) {
  const container = document.getElementById(containerId);
  const t = templateRegistry[currentFormatKey];
  
  const totalGridWidth = t.cols * t.width_mm + (t.cols - 1) * t.gap_x_mm;
  const totalGridHeight = t.rows * t.height_mm + (t.rows - 1) * t.gap_y_mm;
  
  const rightMargin = 210 - totalGridWidth - t.left_margin_mm;
  const bottomMargin = 297 - totalGridHeight - t.top_margin_mm;
  
  container.style.padding = `
    ${t.top_margin_mm}mm 
    ${Math.max(0, rightMargin)}mm 
    ${Math.max(0, bottomMargin)}mm 
    ${t.left_margin_mm}mm
  `;
  
  container.style.gridTemplateColumns = `repeat(${t.cols}, ${t.width_mm}mm)`;
  container.style.gridTemplateRows = `repeat(${t.rows}, ${t.height_mm}mm)`;
  
  for (let i = 1; i <= maxLabels; i++) {
    const label = document.createElement('div');
    label.className = 'lb';
    if (i >= start && i < start + count) {
      label.innerHTML = `
        <div class="lbt">${data.topText || '&nbsp;'}</div>
        <div class="lbm">
          <div class="lba">${data.artNr || '&nbsp;'}</div>
          ${data.suffix ? `<div class="lbs">${data.suffix}</div>` : ''}
        </div>
        <div class="lbb">${data.bezeichnung || '&nbsp;'}</div>
        <div class="lbf">https://lavu-ooe.github.io/</div>
      `;
    } else {
      label.className += ' e'; 
    }
    container.appendChild(label);
  }
}
```

### Dynamische Skalierung

Um CSS-Layoutbrüche in Vorschaukarten zu vermeiden, werden Skalierungsvektoren als dynamische Inline-Eigenschaften berechnet:

```
const baseWidth = 70;   
const baseHeight = 41;  
const scaleX = t.width_mm / baseWidth;
const scaleY = t.height_mm / baseHeight;
const scale = Math.min(scaleX, scaleY, 1);
container.style.setProperty('--label-scale', scale);
```

### Interaktive Bogenvorschau

Die modale Vorschau ermöglicht es Benutzern, auf einzelne Etikettenpositionen zu klicken, um deren Status umzuschalten:

```
function toggleLabel(clickedIndex) {
  const t = templateRegistry[currentFormatKey];
  const maxLabels = t.cols * t.rows;
  let count = parseInt(document.getElementById('i2').value) || 0;
  let start = parseInt(document.getElementById('i3').value) || 1;
  let end = start + count - 1;
  
  if (count === 0) {
    start = clickedIndex;
    count = 1;
  } else if (clickedIndex < start) {
    count = end - clickedIndex + 1;
    start = clickedIndex;
  } else if (clickedIndex > end) {
    count = clickedIndex - start + 1;
  } else {
    start = clickedIndex;
    count = 1;
  }
  
  document.getElementById('i2').value = count;
  document.getElementById('i3').value = start;
  u1(); 
}
```

## 📊 Datenfluss & Workflow Diagramme

### Vollständiger Anwendungs-Workflow

```
flowchart TD
    A["🚀 Benutzer öffnet App"] --> B{"🔍 localStorage prüfen"}
    B -- Cache existiert --> C["📦 Zwischengespeicherte Daten laden"]
    B -- Kein Cache --> D["☁️ Von Cloudflare Workers abrufen"]
    C --> E["📋 Dropdowns füllen"]
    D --> E
    
    E --> F["📍 Benutzer wählt Standort"]
    F --> G["🏷️ Benutzer wählt Produkt"]
    G --> H["👁️ Live-Vorschau rendern"]
    
    H --> I{"⚡ Benutzeraktion"}
    I -- Klick auf Vorschau --> J["🖼️ Interaktives Bogen-Modal öffnen"]
    J --> K["🖱️ Etikettenpositionen anklicken"]
    K --> L["🔄 Etikettenstatus umschalten"]
    L --> M["✏️ Anzahl & Startposition aktualisieren"]
    M --> N["🎨 Bogen-Layout neu rendern"]
    
    I -- Jetzt drucken --> O["🖨️ Browser-Druckdialog öffnen"]
    O --> P["📄 Gedruckten A4-Bogen ausgeben"]
    
    I -- Optionen --> Q["⚙️ Einstellungs-Modal öffnen"]
    Q --> R{"📂 Tab auswählen"}
    R -- Service Worker --> S["🌐 API-Endpunkte verwalten"]
    S --> T["✏️ Sortiments-Endpunkt aktualisieren"]
    S --> U["✏️ Standorte-Endpunkt aktualisieren"]
    
    R -- Datenbank --> V["🗄️ CRUD-Operationen"]
    V --> W["➕ Elemente hinzufügen / bearbeiten / löschen"]
    W --> X["💾 In localStorage speichern"]
    X --> E
    V --> Y["📥 Datenbank-JSON exportieren"]
```

### Etikettendesign-Workflow

```
flowchart LR
    subgraph Input ["1. Dateneingabe"]
        A1["📄 HERMA SKU auswählen"] --> A2["⚙️ Geometriespezifikationen laden"]
        B1["📍 Standort auswählen"] --> B2["🏷️ Kopf-Etikett abrufen"]
        C1["📦 Produkt auswählen"] --> C2["🔢 ArtNr & Beschreibung abrufen"]
        D1["✍️ Suffix eingeben"] --> D2["🏷️ Optionales Badge"]
        E1["🔢 Anzahl & Startposition"]
    end

    subgraph Rendering ["2. Rendering Engine"]
        A2 --> F["📐 Dynamisches Raster berechnen"]
        B2 --> F
        C2 --> F
        D2 --> F
        E1 --> F
        F --> G1["✨ Aktive Zellen rendern"]
        F --> G2["⚪ Leere Zellen rendern"]
        G1 --> H["🖼️ Vorschaubogen zusammensetzen"]
        G2 --> H
    end

    subgraph Interaction ["3. Interaktive Bearbeitung"]
        H --> I["🖥️ Interaktive modale Ansicht"]
        I --> J["🖱️ Zelle anklicken"]
        J --> K["🔄 Offsets neu berechnen"]
        K --> H
    end

    subgraph Output ["4. Druckausgabe"]
        H --> L["🖨️ Druckauftrag ausführen"]
        L --> M["📄 A4 Vektorgrafiken rendern"]
        M --> N["🏷️ Physischer Bogen gedruckt"]
    end
```

### Lebenszyklus des Anwendungsstatus

```
stateDiagram-v2
    [*] --> Uninitialized

    state Uninitialized {
        [*] --> RegisterServiceWorker
        RegisterServiceWorker --> CheckCache
    }

    Uninitialized --> Ready : Ressourcen & Daten geladen

    state Ready {
        [*] --> Standby
        Standby --> LocationSelected : ASZ-Filiale auswählen
        LocationSelected --> ItemSelected : Produktartikel auswählen
        ItemSelected --> GridCalculated : Geometrie berechnen
        GridCalculated --> LivePreview : CSS-Raster rendern
    }

    Ready --> ModalEditing : Klick auf Bogenvorschau
    
    state ModalEditing {
        [*] --> ModalOpen
        ModalOpen --> ToggleCell : Rasterzelle anklicken
        ToggleCell --> RecalculateOffset : Start/Anzahl aktualisieren
        RecalculateOffset --> ModalOpen : Bogen neu zeichnen
        ModalOpen --> ModalClosed : Modal schließen
    }

    ModalEditing --> Ready : Zurück zur Haupt-UI
    Ready --> Printing : Klick auf "Jetzt drucken"
    Printing --> Ready : Druckansicht schließen
```

## 🌟 Hauptfunktionen

### 1\. Dynamische HERMA-Bogen-Engine

*   **Interaktive Klick-zum-Umschalten**\-Bogenpositionierung auf Standard-A4-Rastern
    
*   **Echtzeit-Vorschau** mit automatischer Neuberechnung
    
*   Unterstützung für **rechteckige und runde** Etikettenvorlagen
    

### 2\. Serverless & Offline First

*   Nutzt **Cloudflare Workers** für API-Endpunkte
    
*   Fällt auf **zwischengespeicherten Browserstatus** (`localStorage`) zurück
    
*   **Service Worker** bietet Offline-Fähigkeit mit Network-First-Strategie
    

### 3\. Zweisprachige Unterstützung (i18n)

*   Natives Umschalten zur Laufzeit zwischen **Deutsch (`de`)** und **Englisch (`en`)**
    
*   Dauerhafte Speicherung der Spracheinstellung im `localStorage`
    

### 4\. Geräteübergreifende Responsive UI

*   **Für Mobilgeräte optimiertes Layout**, das bei Vorlagen und Standortauswahl umschaltet
    
*   **Adaptive Breakpoints** bei 768px und 520px
    
*   Für Touch optimierte interaktive Elemente
    

### 5\. PWA-Fähig

*   **Offline-Unterstützung** durch Service Worker
    
*   **Manifest-gesteuerte Installationsaufforderungen** in kompatiblen Browsern
    
*   **Standalone-Anzeige**\-Konfiguration für ein App-ähnliches Erlebnis
    

### 6\. Datenbankverwaltung

*   **In-Browser-CRUD-Operationen** für die Produktdatenbank
    
*   **JSON-Export**\-Funktionalität
    
*   **Automatische Synchronisation** zwischen localStorage und UI
    

## 🔧 Technische Spezifikationen

### Speicher- & Persistenzschema

| 
**Speicherschlüssel**

 | 

**Typ**

 | 

**Beschreibung**

 |
| --- | --- | --- |
| 

`lavu_lang`

 | 

`string`

 | 

Ausgewählte i18n-Sprache (`de` | `en`)

 |
| 

`lavu_location`

 | 

`string`

 | 

Aktuell ausgewählte Site-Code-ID (z. B. `"106"`)

 |
| 

`lavu_locations_url`

 | 

`string`

 | 

Remote-Worker-Endpunkt für Standorte

 |
| 

`lavu_locations_cache`

 | 

`string` (JSON)

 | 

Zwischengespeicherte Standortliste

 |
| 

`lavu_studio_defaults_v8`

 | 

`string` (JSON)

 | 

Zuletzt bekanntes SKU-Format, Anzahl und Positions-Offset

 |
| 

`lavu_studio_sortiment_v8`

 | 

`string` (JSON)

 | 

Lokal bearbeiteter Datenbank-Arbeitsbereich

 |
| 

`lavu_preview_zoom`

 | 

`string`

 | 

Zoomstufe für modale Vorschau

 |

### Media Query Breakpoint Matrix

| 
**Viewport-Breite**

 | 

**Visuelle Anpassungen**

 |
| --- | --- |
| 

**\> 768px**

 | 

Volles Dual-Pane-Vorschau-Desktop-Layout mit interaktivem Bogen-Modal

 |
| 

**<= 768px**

 | 

Versteckt die Live-Vorschau im Seitenbereich (`.ps-wrapper`). Wechselt zum einspaltigen Fluss

 |
| 

**<= 520px**

 | 

Versteckt die Desktop-Header-Standort-Badges (`.hdr-r`). Aktiviert die mobile Standortauswahlsteuerung (`.mobile-location-wrapper`)

 |

### Leistungsmetriken

```
console.time('renderGrid');
r2('mdl', data);
console.timeEnd('renderGrid');
```

## 🖨 Druckanleitung

Befolgen Sie für optimale Druckergebnisse diese Einstellungen im Druckdialog Ihres Browsers:

1.  **Skalierung:** Auf **100% / Tatsächliche Größe** einstellen
    
2.  **Ränder:** Auf **Keine** oder **0mm** einstellen
    
3.  **Papiergröße:** Auswahl erzwingen auf **A4 Hochformat**
    
4.  **Hintergrundgrafiken:** Aktivieren, wenn Sie die Rasterlinien sehen möchten
    

### Druckvorschau-Code

```
document.getElementById('btn-print-now').addEventListener('click', function () {
  if (window.innerWidth <= 768) {
    o1();
  } else {
    window.print();
  }
});
```

### Druckspezifisches CSS

```
@media print {
  @page {
    size: A4 portrait;
    margin: 0 !important;
  }
  
  #hpc .pc {
    display: grid !important;
    gap: 0 !important;
    padding: 5mm 2mm !important;
    width: 210mm !important;
    height: 297mm !important;
    box-shadow: none !important;
    transform: none !important;
  }
  
  #hpc .lb {
    display: flex !important;
    flex-direction: column !important;
    border: 0.5px solid #ccc !important;
    padding: 2.5mm 3.5mm !important;
    break-inside: avoid !important;
  }
}
```

## 🚀 Schnellstart

### Installation & Einrichtung

1.  **Repository klonen oder herunterladen**
    
    ```
    git clone https://github.com/LAVU-OOE/RePrint.git
    cd RePrint
    ```
    
2.  **Hosten über einen beliebigen Server für statische Seiten**
    
    ```
    python3 -m http.server 8080
    # ODER
    npx http-server .
    # ODER
    php -S localhost:8080
    ```
    
3.  **Im Browser öffnen**
    
    ```
    http://localhost:8080
    ```
    

### Erstmalige Verwendung

1.  **Einen Standort auswählen** – Wählen Sie Ihre ASZ-Filiale aus dem dynamisch geladenen Dropdown-Menü
    
2.  **Einen Artikel auswählen** – Suchen Sie entweder nach **Artikelnr.** (numerisch gruppiert) oder nach **Beschreibung** (alphabetisch gruppiert)
    
3.  **Drucklayout anpassen** – Klicken Sie auf das Vorschaubild, um den interaktiven Bogen zu öffnen
    
4.  **Drucken** – Klicken Sie auf "Jetzt drucken", um Ihren A4-Bogen zu generieren
    

## 📁 Projektstruktur

```
.
├── 📄 index.html                  # Haupt-SPA-UI-Container & CSS-Layout-Engine
├── 📄 herma_templates.json        # A4-Raster-Registrierungsdefinitionen
├── 📄 manifest.json               # Web App Manifest für PWA-Installation
├── 📄 site.webmanifest            # Sekundäre App-Manifestdefinition
├── 📄 sw.js                       # Service Worker für Offline-Unterstützung
├── 📄 README.md                   # Anwendungsdokumentation
├── 📄 LICENSE                     # MIT-Lizenz
├── 🖼️ favicon.svg                 # Skalierbares Vektorgrafik-Symbol
├── 🖼️ favicon-96x96.png           # Statisches Raster-Symbol-Asset
├── 🖼️ logo.png                    # Anwendungslogo
├── 🖼️ apple-touch-icon.png        # Apple iOS-Symbol
├── 🖼️ web-app-manifest-192x192.png # PWA-Symbol (192px)
├── 🖼️ web-app-manifest-512x512.png # PWA-Symbol (512px)
└── 📄 tree.md                     # Dateistruktur-Dokumentation
```

## 🗄 Datenbankverwaltung

### In-Browser CRUD-Operationen

Die Anwendung enthält einen integrierten Datenbankmanager, der über die Schaltfläche **"Optionen"** zugänglich ist:

```
function s3() {
  const c1 = document.getElementById('c1').value.trim(); 
  const c2 = document.getElementById('c2').value.trim(); 
  const c3 = document.getElementById('c3').value.trim(); 
  
  if (!c1 || !c3) {
    alert(t.alertFillForm);
    return;
  }
  
  if (a2.some(item => item.artNr === c1)) {
    alert(t.alertDuplicate);
    return;
  }
  
  a2.push({ artNr: c1, geb: c2 || '-', bez: c3 });
  localStorage.setItem('lavu_studio_sortiment_v8', JSON.stringify(a2));
  i1(); 
  e1(); 
  u1(); 
}

function s4() {
  const index = document.getElementById('e1').value;
  const c1 = document.getElementById('c1').value.trim();
  const c2 = document.getElementById('c2').value.trim();
  const c3 = document.getElementById('c3').value.trim();
  
  a2[index] = { artNr: c1, geb: c2, bez: c3 };
  localStorage.setItem('lavu_studio_sortiment_v8', JSON.stringify(a2));
  i1();
  e1();
  u1();
}

function d1(index) {
  if (confirm(t.confirmDelete)) {
    a2.splice(index, 1);
    localStorage.setItem('lavu_studio_sortiment_v8', JSON.stringify(a2));
    i1();
    u1();
  }
}
```

### Datenbank als JSON exportieren

```
function e2() {
  const jsonData = JSON.stringify(a2, null, 2);
  const blob = new Blob([jsonData], { type: "application/json" });
  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');
  link.href = url;
  link.download = "sortiment_export.json";
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
  URL.revokeObjectURL(url);
}
```

### Standards speichern

```
function s7() {
  const data = g1();
  const config = {
    formatKey: currentFormatKey,
    topText: document.getElementById('i1').value,
    count: data.count,
    startPos: data.startPos,
    artNr: data.artNr,
    suffix: data.suffix,
    bezeichnung: data.bezeichnung,
    sortimentIndex: data.sortimentIndex
  };
  localStorage.setItem('lavu_studio_defaults_v8', JSON.stringify(config));
  localStorage.setItem('lavu_location', document.getElementById('i1').value);
}
```

## 🤝 Richtlinien für Mitwirkende

### Entwicklungsumgebung

1.  **Repository forken**
    
2.  **Einen Feature-Branch erstellen**
    
    ```
    git checkout -b feature/dein-feature-name
    ```
    
3.  **Deine Änderungen vornehmen**
    
4.  **Lokal testen** – Stelle sicher, dass die Anwendung ohne Fehler läuft
    
5.  **Mit konventionellen Commit-Nachrichten committen**
    
    ```
    git commit -m "feat: Unterstützung für neue HERMA Vorlagen-SKU hinzugefügt"
    git commit -m "fix: Mobile Layout-Probleme in Safari behoben"
    git commit -m "docs: README mit neuen Cloudflare API-Endpunkten aktualisiert"
    ```
    
6.  **Pushen und einen Pull Request erstellen**
    

### Testrichtlinien

*   **Browserübergreifendes Testen**: Chrome, Firefox, Safari, Edge
    
*   **Mobiles Testen**: iOS Safari, Android Chrome
    
*   **Offline-Testen**: Netzwerk deaktivieren und gecachte Funktionalität überprüfen
    
*   **Druck-Testen**: A4-Ausgabe mit verschiedenen Druckerkonfigurationen überprüfen
    

### Code-Standards

*   **ES6+** JavaScript mit `const` und `let`
    
*   **CSS-Variablen** für das Theming
    
*   **Semantische HTML5**\-Elemente
    
*   **Progressive Enhancement**\-Prinzipien
    

## 📄 Lizenz

Dieses Projekt ist Open Source und steht unter der **MIT-Lizenz**.

```
MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

*Unabhängiges Open-Source-Projekt*

---

</div>
</details>

---



---

<details>
<summary><b>🇦🇹 Auf Deutsch anzeigen (Click to view German LIESMICH)</b></summary>

---

## RE:PRINT Studio v9

## 📖 Inhaltsverzeichnis

1.  [Einführung](https://gemini.google.com/#-einf%C3%BChrung "null")
    
2.  [Haftungsausschluss / Rechtlicher Hinweis](https://gemini.google.com/#-haftungsausschluss--rechtlicher-hinweis "null")
    
3.  [Systemübersicht](https://gemini.google.com/#-system%C3%BCbersicht "null")
    
4.  [Architektur](https://gemini.google.com/#-architektur "null")
    
    *   [Client-Seitiger Kern](https://gemini.google.com/#client-seitiger-kern "null")
        
    *   [Cloudflare Workers Integration](https://gemini.google.com/#cloudflare-workers-integration "null")
        
    *   [Service Worker & Offline Strategie](https://gemini.google.com/#service-worker--offline-strategie "null")
        
    *   [API Fetch & Cache Fallback Sequenz](https://gemini.google.com/#api-fetch--cache-fallback-sequenz "null")
        
5.  [Etikettendesign & Rendering Engine](https://gemini.google.com/#-etikettendesign--rendering-engine "null")
    
    *   [Berechnung der Rastergeometrie](https://gemini.google.com/#berechnung-der-rastergeometrie "null")
        
    *   [Dynamische Skalierung](https://gemini.google.com/#dynamische-skalierung "null")
        
    *   [Interaktive Bogenvorschau](https://gemini.google.com/#interaktive-bogenvorschau "null")
        
6.  [Datenfluss & Workflow Diagramme](https://gemini.google.com/#-datenfluss--workflow-diagramme "null")
    
7.  [Hauptfunktionen](https://gemini.google.com/#-hauptfunktionen "null")
    
8.  [Technische Spezifikationen](https://gemini.google.com/#-technische-spezifikationen "null")
    
9.  [Druckanleitung](https://gemini.google.com/#-druckanleitung "null")
    
10.  [Schnellstart](https://gemini.google.com/#-schnellstart "null")
     
11.  [Projektstruktur](https://gemini.google.com/#-projektstruktur "null")
     
12.  [Datenbankverwaltung](https://gemini.google.com/#-datenbankverwaltung "null")
     
13.  [Richtlinien für Mitwirkende](https://gemini.google.com/#-richtlinien-f%C3%BCr-mitwirkende "null")
     
14.  [Lizenz](https://gemini.google.com/#-lizenz "null")
     

## 🚀 Einführung

**RE:PRINT Studio v9** ist eine ressourcenschonende, clientseitige Progressive Web Application (PWA), die für ASZ-Standorte (Altstoffsammelzentren) in Oberösterreich entwickelt wurde. Sie bietet dynamische Etikettenformatierung, Live-Berechnungen der Druckvorschau und anpassbares Rendern von Vorlagenbögen für Standard-HERMA-A4-Etiketten.

Die Anwendung läuft vollständig im Browser und nutzt moderne Webtechnologien, um ein nahtloses Erlebnis über Desktop- und Mobilgeräte hinweg zu bieten, mit robusten Offline-Funktionen.

## ⚠️ Haftungsausschluss / Rechtlicher Hinweis

> **Wichtiger Hinweis / Haftungsausschluss:**
> 
> **Diese Software ist ein unabhängiges Community-Projekt und steht in keiner offiziellen Verbindung zur LAVU OÖ (OÖ. Landes-Abfallverwertungsunternehmen GmbH) oder den Bezirksabfallverbänden (BAV OÖ).**
> 
> **Dies ist keine offizielle Anwendung oder Software der LAVU OÖ oder des BAV OÖ. Alle Marken, Logos und Bezeichnungen gehören ihren jeweiligen Eigentümern.**
> 
> **Hinweis:**
> 
> **Diese Anwendung ist ein unabhängiges Open-Source-Projekt und wird von der LAVU OÖ oder dem BAV OÖ weder offiziell unterstützt noch gesponsert oder in irgendeiner Weise damit in Verbindung gebracht.**

## 🏗 Systemübersicht

RE:PRINT Studio v9 basiert auf einer **Serverless-Architektur**, die Folgendes kombiniert:

*   **Reines clientseitiges Rendering** mit HTML5, CSS3 und Vanilla JavaScript (ES6+)
    
*   **Cloudflare Workers** für API-Endpunkte, die dynamische JSON-Daten bereitstellen
    
*   **Service Workers** für progressive Verbesserung und Offline-Unterstützung
    
*   **localStorage** für die clientseitige Persistenz von Benutzereinstellungen und zwischengespeicherten Daten
    

### Systemkontextdiagramm

```
flowchart TB
    subgraph Client ["Browser Client (PWA)"]
        UI["🎨 UI Engine<br/>(index.html)"]
        SW["⚙️ Service Worker<br/>(sw.js)"]
        LS["💾 localStorage<br/>Cache & Einstellungen"]
    end

    subgraph Cloudflare ["Cloudflare Workers Edge Network"]
        SA["📦 Sortiment API<br/>/sortiment-api"]
        LA["📍 Locations API<br/>/locations-api"]
    end

    subgraph External ["Externe Assets & Registry"]
        TEMPLATES["📄 HERMA Templates<br/>(herma_templates.json)"]
        GITHUB["🌐 GitHub Pages<br/>Statische Assets"]
    end

    UI -->|fetch| SA
    UI -->|fetch| LA
    UI -->|fetch| TEMPLATES
    SW -->|Cache-Strategie| GITHUB
    UI -->|Lesen/Schreiben| LS
    SW -->|Network-First Cache| SA
    SW -->|Network-First Cache| LA
```

## 🏛 Architektur

### Client-Seitiger Kern

Der Kern der Anwendung ist in einer einzigen `index.html`\-Datei enthalten, die Folgendes umfasst:

1.  **Vorlagen-Registry-Engine** – Lädt und analysiert `herma_templates.json`
    
2.  **Dynamisches Dropdown-System** – Gruppiert nach Zahlenbereichen und alphabetischen Buchstaben
    
3.  **Interaktiver Raster-Renderer** – Rendert A4-Bögen mit Klick-zum-Umschalten-Funktionalität
    
4.  **i18n Runtime** – Zweisprachige Unterstützung mit nahtlosem Umschalten
    
5.  **CRUD-Datenbankmanager** – In-Browser-Datenverwaltung mit JSON-Export
    

### Cloudflare Workers Integration

Die Anwendung kommuniziert mit zwei primären Cloudflare-Worker-Endpunkten:

#### 1\. Sortiment API (`sortiment-api.lavu-ooe.workers.dev`)

Gibt den Produktkatalog im JSON-Format zurück:

```
[
  {
    "artNr": "4040",
    "bez": "Elektro-Kleingeräte",
    "geb": "QR-Box"  
  }
]
```

**Worker-Implementierungs-Snippet:**

```
export default {
  async fetch(request) {
    const CORS_HEADERS = {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, OPTIONS',
      'Content-Type': 'application/json'
    };
    try {
      const data = await SORTIMENT_KV.get('sortiment', 'json');
      return new Response(JSON.stringify(data), { headers: CORS_HEADERS });
    } catch (error) {
      return new Response(
        JSON.stringify({ error: 'Fehler beim Abrufen der Sortimentsdaten' }),
        { status: 500, headers: CORS_HEADERS }
      );
    }
  }
}
```

#### 2\. Locations API (`locations-api.lavu-ooe.workers.dev`)

Gibt die Liste der ASZ-Standorte zurück:

```
[
  {
    "siteCode": "106",
    "name": "ASZ Asten",
    "zipCode": "4481",
    "region": "Linz-Land & Linz Stadt"
  }
]
```

**Worker-Implementierungs-Snippet:**

```
export default {
  async fetch(request) {
    const CORS_HEADERS = {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, OPTIONS',
      'Content-Type': 'application/json'
    };
    try {
      const locations = await LOCATIONS_KV.get('locations', 'json');
      return new Response(JSON.stringify(locations), { headers: CORS_HEADERS });
    } catch (error) {
      return new Response(
        JSON.stringify({ error: 'Fehler beim Abrufen der Standortdaten' }),
        { status: 500, headers: CORS_HEADERS }
      );
    }
  }
}
```

### Service Worker & Offline-Strategie

Der Service Worker implementiert eine **Network-First**\-Strategie für dynamische JSON-Daten und eine **Cache-First**\-Strategie für statische Assets.

#### Registrierung & Installation

```
const CACHE_NAME = 'lavu-studio-v10';
const STATIC_ASSETS = [
  '.',
  'index.html',
  'manifest.json',
  'favicon.svg',
  'logo.png',
  'favicon-96x96.png',
  'apple-touch-icon.png',
  'web-app-manifest-192x192.png',
  'web-app-manifest-512x512.png'
];
const DYNAMIC_JSON_URLS = [
  'https://locations-api.lavu-ooe.workers.dev/',
  'https://sortiment-api.lavu-ooe.workers.dev/'
];

self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll([...STATIC_ASSETS, ...DYNAMIC_JSON_URLS]))
      .then(() => self.skipWaiting())
  );
});
```

#### Abrufstrategie für JSON-Endpunkte

```
if (DYNAMIC_JSON_URLS.some(jsonUrl => url.href === jsonUrl)) {
  event.respondWith(
    fetch(request, { cache: 'no-store' })
      .then(response => {
        const clonedResponse = response.clone();
        caches.open(CACHE_NAME)
          .then(cache => cache.put(request, clonedResponse));
        return response;
      })
      .catch(() => {
        return caches.match(request)
          .then(cachedResponse => {
            if (cachedResponse) {
              console.log('[SW] JSON wird aus dem Cache bereitgestellt');
              return cachedResponse;
            }
            return new Response(
              JSON.stringify({ error: 'Offline - Daten nicht verfügbar' }),
              { status: 503, headers: { 'Content-Type': 'application/json' } }
            );
          });
      })
  );
  return;
}
```

#### Offline-Fallback für die Navigation

```
if (request.mode === 'navigate') {
  event.respondWith(
    fetch(request)
      .then(response => {
        const clonedResponse = response.clone();
        caches.open(CACHE_NAME)
          .then(cache => cache.put(request, clonedResponse));
        return response;
      })
      .catch(() => {
        return caches.match('/index.html')
          .then(cachedResponse => {
            if (cachedResponse) {
              console.log('[SW] Offline-Fallback-Seite wird bereitgestellt');
              return cachedResponse;
            }
            return new Response(
              '<html><body><h1>Offline</h1><p>Bitte verbinden Sie sich mit dem Internet, um die App zu nutzen.</p></body></html>',
              { headers: { 'Content-Type': 'text/html' } }
            );
          });
      })
  );
  return;
}
```

### API Fetch & Cache Fallback Sequenz

```
sequenceDiagram
    autonumber
    actor User as 👤 Benutzer
    participant UI as 🖥️ Client UI (index.html)
    participant SW as ⚙️ Service Worker
    participant Cache as 💾 Cache / localStorage
    participant API as ☁️ Cloudflare Worker API

    User->>UI: Wählt Standort / Sortimentsartikel
    UI->>SW: fetch(API-Endpunkt)
    
    alt Netzwerk Online
        SW->>API: HTTP GET /locations-api oder /sortiment-api
        API-->>SW: 200 OK (JSON-Nutzdaten)
        SW->>Cache: Cache-Eintrag aktualisieren
        SW-->>UI: Neue JSON-Antwort zurückgeben
    else Netzwerk Offline / Abruffehler
        SW->>Cache: Zwischengespeicherte Anfrage abgleichen
        alt Cache-Treffer
            Cache-->>SW: Zwischengespeichertes JSON zurückgeben
            SW-->>UI: Zwischengespeichertes JSON zurückgeben (Offline-Modus)
        else Cache-Fehlschlag
            SW-->>UI: 503 Service Unavailable (Fallback-Nutzdaten)
        end
    end
    
    UI->>User: Interaktives Raster & Etikettenvorschau rendern
```

## 🎨 Etikettendesign & Rendering Engine

Die Kern-Rendering-Engine wandelt HERMA-Vorlagendefinitionen mit präzisen geometrischen Berechnungen in interaktive A4-Bögen um.

### Berechnung der Rastergeometrie

Der Etiketten-Renderer berechnet dynamische Layout-Geometrien basierend auf den Vorlagenparametern, die in `herma_templates.json` deklariert sind.

#### Mathematische Grundlage

Wobei:

| 
**Variable**

 | 

**Beschreibung**

 |
| --- | --- |
|  | 

Anzahl der Spalten (`cols`)

 |
|  | 

Anzahl der Zeilen (`rows`)

 |
|  | 

Etikettenbreite in Millimetern

 |
|  | 

Etikettenhöhe in Millimetern

 |
|  | 

Horizontale und vertikale Abstände in Millimetern

 |

#### Vorlagenstruktur (`herma_templates.json`)

```
{
  "engine": "HERMA Label Engine",
  "page_format": {
    "size": "A4",
    "width_mm": 210.0,
    "height_mm": 297.0,
    "orientation": "portrait"
  },
  "templates": [
    {
      "sku": "4473",
      "category": "MEDIUM",
      "cols": 3,
      "rows": 7,
      "width_mm": 70.0,
      "height_mm": 41.0,
      "round": false,
      "top_margin_mm": 10.0,
      "left_margin_mm": 0.0,
      "gap_x_mm": 0.0,
      "gap_y_mm": 0.0
    }
  ]
}
```

#### Raster-Rendering-Funktion

```
function r2(containerId, data) {
  const container = document.getElementById(containerId);
  const t = templateRegistry[currentFormatKey];
  
  const totalGridWidth = t.cols * t.width_mm + (t.cols - 1) * t.gap_x_mm;
  const totalGridHeight = t.rows * t.height_mm + (t.rows - 1) * t.gap_y_mm;
  
  const rightMargin = 210 - totalGridWidth - t.left_margin_mm;
  const bottomMargin = 297 - totalGridHeight - t.top_margin_mm;
  
  container.style.padding = `
    ${t.top_margin_mm}mm 
    ${Math.max(0, rightMargin)}mm 
    ${Math.max(0, bottomMargin)}mm 
    ${t.left_margin_mm}mm
  `;
  
  container.style.gridTemplateColumns = `repeat(${t.cols}, ${t.width_mm}mm)`;
  container.style.gridTemplateRows = `repeat(${t.rows}, ${t.height_mm}mm)`;
  
  for (let i = 1; i <= maxLabels; i++) {
    const label = document.createElement('div');
    label.className = 'lb';
    if (i >= start && i < start + count) {
      label.innerHTML = `
        <div class="lbt">${data.topText || '&nbsp;'}</div>
        <div class="lbm">
          <div class="lba">${data.artNr || '&nbsp;'}</div>
          ${data.suffix ? `<div class="lbs">${data.suffix}</div>` : ''}
        </div>
        <div class="lbb">${data.bezeichnung || '&nbsp;'}</div>
        <div class="lbf">https://lavu-ooe.github.io/</div>
      `;
    } else {
      label.className += ' e'; 
    }
    container.appendChild(label);
  }
}
```

### Dynamische Skalierung

Um CSS-Layoutbrüche in Vorschaukarten zu vermeiden, werden Skalierungsvektoren als dynamische Inline-Eigenschaften berechnet:

```
const baseWidth = 70;   
const baseHeight = 41;  
const scaleX = t.width_mm / baseWidth;
const scaleY = t.height_mm / baseHeight;
const scale = Math.min(scaleX, scaleY, 1);
container.style.setProperty('--label-scale', scale);
```

### Interaktive Bogenvorschau

Die modale Vorschau ermöglicht es Benutzern, auf einzelne Etikettenpositionen zu klicken, um deren Status umzuschalten:

```
function toggleLabel(clickedIndex) {
  const t = templateRegistry[currentFormatKey];
  const maxLabels = t.cols * t.rows;
  let count = parseInt(document.getElementById('i2').value) || 0;
  let start = parseInt(document.getElementById('i3').value) || 1;
  let end = start + count - 1;
  
  if (count === 0) {
    start = clickedIndex;
    count = 1;
  } else if (clickedIndex < start) {
    count = end - clickedIndex + 1;
    start = clickedIndex;
  } else if (clickedIndex > end) {
    count = clickedIndex - start + 1;
  } else {
    start = clickedIndex;
    count = 1;
  }
  
  document.getElementById('i2').value = count;
  document.getElementById('i3').value = start;
  u1(); 
}
```

## 📊 Datenfluss & Workflow Diagramme

### Vollständiger Anwendungs-Workflow

```
flowchart TD
    A["🚀 Benutzer öffnet App"] --> B{"🔍 localStorage prüfen"}
    B -- Cache existiert --> C["📦 Zwischengespeicherte Daten laden"]
    B -- Kein Cache --> D["☁️ Von Cloudflare Workers abrufen"]
    C --> E["📋 Dropdowns füllen"]
    D --> E
    
    E --> F["📍 Benutzer wählt Standort"]
    F --> G["🏷️ Benutzer wählt Produkt"]
    G --> H["👁️ Live-Vorschau rendern"]
    
    H --> I{"⚡ Benutzeraktion"}
    I -- Klick auf Vorschau --> J["🖼️ Interaktives Bogen-Modal öffnen"]
    J --> K["🖱️ Etikettenpositionen anklicken"]
    K --> L["🔄 Etikettenstatus umschalten"]
    L --> M["✏️ Anzahl & Startposition aktualisieren"]
    M --> N["🎨 Bogen-Layout neu rendern"]
    
    I -- Jetzt drucken --> O["🖨️ Browser-Druckdialog öffnen"]
    O --> P["📄 Gedruckten A4-Bogen ausgeben"]
    
    I -- Optionen --> Q["⚙️ Einstellungs-Modal öffnen"]
    Q --> R{"📂 Tab auswählen"}
    R -- Service Worker --> S["🌐 API-Endpunkte verwalten"]
    S --> T["✏️ Sortiments-Endpunkt aktualisieren"]
    S --> U["✏️ Standorte-Endpunkt aktualisieren"]
    
    R -- Datenbank --> V["🗄️ CRUD-Operationen"]
    V --> W["➕ Elemente hinzufügen / bearbeiten / löschen"]
    W --> X["💾 In localStorage speichern"]
    X --> E
    V --> Y["📥 Datenbank-JSON exportieren"]
```

### Etikettendesign-Workflow

```
flowchart LR
    subgraph Input ["1. Dateneingabe"]
        A1["📄 HERMA SKU auswählen"] --> A2["⚙️ Geometriespezifikationen laden"]
        B1["📍 Standort auswählen"] --> B2["🏷️ Kopf-Etikett abrufen"]
        C1["📦 Produkt auswählen"] --> C2["🔢 ArtNr & Beschreibung abrufen"]
        D1["✍️ Suffix eingeben"] --> D2["🏷️ Optionales Badge"]
        E1["🔢 Anzahl & Startposition"]
    end

    subgraph Rendering ["2. Rendering Engine"]
        A2 --> F["📐 Dynamisches Raster berechnen"]
        B2 --> F
        C2 --> F
        D2 --> F
        E1 --> F
        F --> G1["✨ Aktive Zellen rendern"]
        F --> G2["⚪ Leere Zellen rendern"]
        G1 --> H["🖼️ Vorschaubogen zusammensetzen"]
        G2 --> H
    end

    subgraph Interaction ["3. Interaktive Bearbeitung"]
        H --> I["🖥️ Interaktive modale Ansicht"]
        I --> J["🖱️ Zelle anklicken"]
        J --> K["🔄 Offsets neu berechnen"]
        K --> H
    end

    subgraph Output ["4. Druckausgabe"]
        H --> L["🖨️ Druckauftrag ausführen"]
        L --> M["📄 A4 Vektorgrafiken rendern"]
        M --> N["🏷️ Physischer Bogen gedruckt"]
    end
```

### Lebenszyklus des Anwendungsstatus

```
stateDiagram-v2
    [*] --> Uninitialized

    state Uninitialized {
        [*] --> RegisterServiceWorker
        RegisterServiceWorker --> CheckCache
    }

    Uninitialized --> Ready : Ressourcen & Daten geladen

    state Ready {
        [*] --> Standby
        Standby --> LocationSelected : ASZ-Filiale auswählen
        LocationSelected --> ItemSelected : Produktartikel auswählen
        ItemSelected --> GridCalculated : Geometrie berechnen
        GridCalculated --> LivePreview : CSS-Raster rendern
    }

    Ready --> ModalEditing : Klick auf Bogenvorschau
    
    state ModalEditing {
        [*] --> ModalOpen
        ModalOpen --> ToggleCell : Rasterzelle anklicken
        ToggleCell --> RecalculateOffset : Start/Anzahl aktualisieren
        RecalculateOffset --> ModalOpen : Bogen neu zeichnen
        ModalOpen --> ModalClosed : Modal schließen
    }

    ModalEditing --> Ready : Zurück zur Haupt-UI
    Ready --> Printing : Klick auf "Jetzt drucken"
    Printing --> Ready : Druckansicht schließen
```

## 🌟 Hauptfunktionen

### 1\. Dynamische HERMA-Bogen-Engine

*   **Interaktive Klick-zum-Umschalten**\-Bogenpositionierung auf Standard-A4-Rastern
    
*   **Echtzeit-Vorschau** mit automatischer Neuberechnung
    
*   Unterstützung für **rechteckige und runde** Etikettenvorlagen
    

### 2\. Serverless & Offline First

*   Nutzt **Cloudflare Workers** für API-Endpunkte
    
*   Fällt auf **zwischengespeicherten Browserstatus** (`localStorage`) zurück
    
*   **Service Worker** bietet Offline-Fähigkeit mit Network-First-Strategie
    

### 3\. Zweisprachige Unterstützung (i18n)

*   Natives Umschalten zur Laufzeit zwischen **Deutsch (`de`)** und **Englisch (`en`)**
    
*   Dauerhafte Speicherung der Spracheinstellung im `localStorage`
    

### 4\. Geräteübergreifende Responsive UI

*   **Für Mobilgeräte optimiertes Layout**, das bei Vorlagen und Standortauswahl umschaltet
    
*   **Adaptive Breakpoints** bei 768px und 520px
    
*   Für Touch optimierte interaktive Elemente
    

### 5\. PWA-Fähig

*   **Offline-Unterstützung** durch Service Worker
    
*   **Manifest-gesteuerte Installationsaufforderungen** in kompatiblen Browsern
    
*   **Standalone-Anzeige**\-Konfiguration für ein App-ähnliches Erlebnis
    

### 6\. Datenbankverwaltung

*   **In-Browser-CRUD-Operationen** für die Produktdatenbank
    
*   **JSON-Export**\-Funktionalität
    
*   **Automatische Synchronisation** zwischen localStorage und UI
    

## 🔧 Technische Spezifikationen

### Speicher- & Persistenzschema

| 
**Speicherschlüssel**

 | 

**Typ**

 | 

**Beschreibung**

 |
| --- | --- | --- |
| 

`lavu_lang`

 | 

`string`

 | 

Ausgewählte i18n-Sprache (`de` | `en`)

 |
| 

`lavu_location`

 | 

`string`

 | 

Aktuell ausgewählte Site-Code-ID (z. B. `"106"`)

 |
| 

`lavu_locations_url`

 | 

`string`

 | 

Remote-Worker-Endpunkt für Standorte

 |
| 

`lavu_locations_cache`

 | 

`string` (JSON)

 | 

Zwischengespeicherte Standortliste

 |
| 

`lavu_studio_defaults_v8`

 | 

`string` (JSON)

 | 

Zuletzt bekanntes SKU-Format, Anzahl und Positions-Offset

 |
| 

`lavu_studio_sortiment_v8`

 | 

`string` (JSON)

 | 

Lokal bearbeiteter Datenbank-Arbeitsbereich

 |
| 

`lavu_preview_zoom`

 | 

`string`

 | 

Zoomstufe für modale Vorschau

 |

### Media Query Breakpoint Matrix

| 
**Viewport-Breite**

 | 

**Visuelle Anpassungen**

 |
| --- | --- |
| 

**\> 768px**

 | 

Volles Dual-Pane-Vorschau-Desktop-Layout mit interaktivem Bogen-Modal

 |
| 

**<= 768px**

 | 

Versteckt die Live-Vorschau im Seitenbereich (`.ps-wrapper`). Wechselt zum einspaltigen Fluss

 |
| 

**<= 520px**

 | 

Versteckt die Desktop-Header-Standort-Badges (`.hdr-r`). Aktiviert die mobile Standortauswahlsteuerung (`.mobile-location-wrapper`)

 |

### Leistungsmetriken

```
console.time('renderGrid');
r2('mdl', data);
console.timeEnd('renderGrid');
```

## 🖨 Druckanleitung

Befolgen Sie für optimale Druckergebnisse diese Einstellungen im Druckdialog Ihres Browsers:

1.  **Skalierung:** Auf **100% / Tatsächliche Größe** einstellen
    
2.  **Ränder:** Auf **Keine** oder **0mm** einstellen
    
3.  **Papiergröße:** Auswahl erzwingen auf **A4 Hochformat**
    
4.  **Hintergrundgrafiken:** Aktivieren, wenn Sie die Rasterlinien sehen möchten
    

### Druckvorschau-Code

```
document.getElementById('btn-print-now').addEventListener('click', function () {
  if (window.innerWidth <= 768) {
    o1();
  } else {
    window.print();
  }
});
```

### Druckspezifisches CSS

```
@media print {
  @page {
    size: A4 portrait;
    margin: 0 !important;
  }
  
  #hpc .pc {
    display: grid !important;
    gap: 0 !important;
    padding: 5mm 2mm !important;
    width: 210mm !important;
    height: 297mm !important;
    box-shadow: none !important;
    transform: none !important;
  }
  
  #hpc .lb {
    display: flex !important;
    flex-direction: column !important;
    border: 0.5px solid #ccc !important;
    padding: 2.5mm 3.5mm !important;
    break-inside: avoid !important;
  }
}
```

## 🚀 Schnellstart

### Installation & Einrichtung

1.  **Repository klonen oder herunterladen**
    
    ```
    git clone https://github.com/LAVU-OOE/RePrint.git
    cd RePrint
    ```
    
2.  **Hosten über einen beliebigen Server für statische Seiten**
    
    ```
    python3 -m http.server 8080
    # ODER
    npx http-server .
    # ODER
    php -S localhost:8080
    ```
    
3.  **Im Browser öffnen**
    
    ```
    http://localhost:8080
    ```
    

### Erstmalige Verwendung

1.  **Einen Standort auswählen** – Wählen Sie Ihre ASZ-Filiale aus dem dynamisch geladenen Dropdown-Menü
    
2.  **Einen Artikel auswählen** – Suchen Sie entweder nach **Artikelnr.** (numerisch gruppiert) oder nach **Beschreibung** (alphabetisch gruppiert)
    
3.  **Drucklayout anpassen** – Klicken Sie auf das Vorschaubild, um den interaktiven Bogen zu öffnen
    
4.  **Drucken** – Klicken Sie auf "Jetzt drucken", um Ihren A4-Bogen zu generieren
    

## 📁 Projektstruktur

```
.
├── 📄 index.html                  # Haupt-SPA-UI-Container & CSS-Layout-Engine
├── 📄 herma_templates.json        # A4-Raster-Registrierungsdefinitionen
├── 📄 manifest.json               # Web App Manifest für PWA-Installation
├── 📄 site.webmanifest            # Sekundäre App-Manifestdefinition
├── 📄 sw.js                       # Service Worker für Offline-Unterstützung
├── 📄 README.md                   # Anwendungsdokumentation
├── 📄 LICENSE                     # MIT-Lizenz
├── 🖼️ favicon.svg                 # Skalierbares Vektorgrafik-Symbol
├── 🖼️ favicon-96x96.png           # Statisches Raster-Symbol-Asset
├── 🖼️ logo.png                    # Anwendungslogo
├── 🖼️ apple-touch-icon.png        # Apple iOS-Symbol
├── 🖼️ web-app-manifest-192x192.png # PWA-Symbol (192px)
├── 🖼️ web-app-manifest-512x512.png # PWA-Symbol (512px)
└── 📄 tree.md                     # Dateistruktur-Dokumentation
```

## 🗄 Datenbankverwaltung

### In-Browser CRUD-Operationen

Die Anwendung enthält einen integrierten Datenbankmanager, der über die Schaltfläche **"Optionen"** zugänglich ist:

```
function s3() {
  const c1 = document.getElementById('c1').value.trim(); 
  const c2 = document.getElementById('c2').value.trim(); 
  const c3 = document.getElementById('c3').value.trim(); 
  
  if (!c1 || !c3) {
    alert(t.alertFillForm);
    return;
  }
  
  if (a2.some(item => item.artNr === c1)) {
    alert(t.alertDuplicate);
    return;
  }
  
  a2.push({ artNr: c1, geb: c2 || '-', bez: c3 });
  localStorage.setItem('lavu_studio_sortiment_v8', JSON.stringify(a2));
  i1(); 
  e1(); 
  u1(); 
}

function s4() {
  const index = document.getElementById('e1').value;
  const c1 = document.getElementById('c1').value.trim();
  const c2 = document.getElementById('c2').value.trim();
  const c3 = document.getElementById('c3').value.trim();
  
  a2[index] = { artNr: c1, geb: c2, bez: c3 };
  localStorage.setItem('lavu_studio_sortiment_v8', JSON.stringify(a2));
  i1();
  e1();
  u1();
}

function d1(index) {
  if (confirm(t.confirmDelete)) {
    a2.splice(index, 1);
    localStorage.setItem('lavu_studio_sortiment_v8', JSON.stringify(a2));
    i1();
    u1();
  }
}
```

### Datenbank als JSON exportieren

```
function e2() {
  const jsonData = JSON.stringify(a2, null, 2);
  const blob = new Blob([jsonData], { type: "application/json" });
  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');
  link.href = url;
  link.download = "sortiment_export.json";
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
  URL.revokeObjectURL(url);
}
```

### Standards speichern

```
function s7() {
  const data = g1();
  const config = {
    formatKey: currentFormatKey,
    topText: document.getElementById('i1').value,
    count: data.count,
    startPos: data.startPos,
    artNr: data.artNr,
    suffix: data.suffix,
    bezeichnung: data.bezeichnung,
    sortimentIndex: data.sortimentIndex
  };
  localStorage.setItem('lavu_studio_defaults_v8', JSON.stringify(config));
  localStorage.setItem('lavu_location', document.getElementById('i1').value);
}
```

## 🤝 Richtlinien für Mitwirkende

### Entwicklungsumgebung

1.  **Repository forken**
    
2.  **Einen Feature-Branch erstellen**
    
    ```
    git checkout -b feature/dein-feature-name
    ```
    
3.  **Deine Änderungen vornehmen**
    
4.  **Lokal testen** – Stelle sicher, dass die Anwendung ohne Fehler läuft
    
5.  **Mit konventionellen Commit-Nachrichten committen**
    
    ```
    git commit -m "feat: Unterstützung für neue HERMA Vorlagen-SKU hinzugefügt"
    git commit -m "fix: Mobile Layout-Probleme in Safari behoben"
    git commit -m "docs: README mit neuen Cloudflare API-Endpunkten aktualisiert"
    ```
    
6.  **Pushen und einen Pull Request erstellen**
    

### Testrichtlinien

*   **Browserübergreifendes Testen**: Chrome, Firefox, Safari, Edge
    
*   **Mobiles Testen**: iOS Safari, Android Chrome
    
*   **Offline-Testen**: Netzwerk deaktivieren und gecachte Funktionalität überprüfen
    
*   **Druck-Testen**: A4-Ausgabe mit verschiedenen Druckerkonfigurationen überprüfen
    

### Code-Standards

*   **ES6+** JavaScript mit `const` und `let`
    
*   **CSS-Variablen** für das Theming
    
*   **Semantische HTML5**\-Elemente
    
*   **Progressive Enhancement**\-Prinzipien
    

## 📄 Lizenz

Dieses Projekt ist Open Source und steht unter der **MIT-Lizenz**.

```
MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

*Unabhängiges Open-Source-Projekt*

---

</details>