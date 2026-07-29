RE:PRINT Studio v9 — Editorial Assessment & Technical Reference Manual📋 Technical Writing Evaluation & Editorial FeedbackProficiency Level: OutstandingYour technical documentation for RE:PRINT Studio v9 is extraordinarily comprehensive, well-structured, and clear. It seamlessly bridges high-level architecture overview with granular implementation details.Growth Areas & Specific RecommendationsMathematical Formula Formatting:Observation: In Section 5, mathematical calculations for total grid width and margins were written as plain text variable assignments (e.g., W_total = (Cols * W_mm) + ...).Actionable Step: Standardize all mathematical expressions using formal LaTeX notation ($...$ for inline and $$...$$ for block displays). This improves readability and provides a professional mathematical foundation.Code Snippet Completeness & Consistency:Observation: In the Service Worker section and JSON template blocks, a few unclosed JSON trailing fragments and code blocks were present at the end of the raw draft.Actionable Step: Ensure all code examples are fully closed, syntactically valid, and formatted with appropriate syntax highlighting tags (javascript, json, css, bash).Diagram Cross-Referencing:Observation: The document features excellent Mermaid flowcharts and sequence diagrams, but could benefit from explicit textual references in the preceding sections.Actionable Step: Add brief contextual introductions before each diagram explaining what the viewer should observe (e.g., "The sequence diagram below details the offline-fallback mechanism during network degradation...").RE:PRINT Studio v9 — Technische DokumentationOfficial engineering specification and operational guide for RE:PRINT Studio v9.📖 InhaltsverzeichnisEinführungHaftungsausschluss / Rechtlicher HinweisSystemübersichtArchitekturClient-Seitiger KernCloudflare Workers IntegrationService Worker & Offline-StrategieAPI Fetch & Cache Fallback SequenzEtikettendesign & Rendering EngineBerechnung der RastergeometrieDynamische SkalierungInteraktive BogenvorschauDatenfluss & Workflow-DiagrammeHauptfunktionenTechnische SpezifikationenDruckanleitungSchnellstartProjektstrukturDatenbankverwaltungRichtlinien für MitwirkendeLizenz1. 🚀 EinführungRE:PRINT Studio v9 ist eine ressourcenschonende, clientseitige Progressive Web Application (PWA), die für ASZ-Standorte (Altstoffsammelzentren) in Oberösterreich entwickelt wurde. Sie bietet dynamische Etikettenformatierung, Live-Berechnungen der Druckvorschau und anpassbares Rendern von Vorlagenbögen für Standard-HERMA-A4-Etiketten.Die Anwendung läuft vollständig im Browser und nutzt moderne Webtechnologien, um ein nahtloses Erlebnis über Desktop- und Mobilgeräte hinweg zu bieten, mit robusten Offline-Funktionen.2. ⚠️ Haftungsausschluss / Rechtlicher HinweisWichtiger Hinweis / Haftungsausschluss:Diese Software ist ein unabhängiges Community-Projekt und steht in keiner offiziellen Verbindung zur LAVU OÖ (OÖ. Landes-Abfallverwertungsunternehmen GmbH) oder den Bezirksabfallverbänden (BAV OÖ).Dies ist keine offizielle Anwendung oder Software der LAVU OÖ oder des BAV OÖ. Alle Marken, Logos und Bezeichnungen gehören ihren jeweiligen Eigentümern.Dieses Open-Source-Projekt wird von der LAVU OÖ oder dem BAV OÖ weder offiziell unterstützt noch gesponsert oder in irgendeiner Weise damit in Verbindung gebracht.3. 🏗 SystemübersichtRE:PRINT Studio v9 basiert auf einer Serverless-Architektur, die Folgendes kombiniert:Reines clientseitiges Rendering mit HTML5, CSS3 und Vanilla JavaScript (ES6+).Cloudflare Workers für API-Endpunkte, die dynamische JSON-Daten bereitstellen.Service Workers für progressive Verbesserung und Offline-Unterstützung.localStorage für die clientseitige Persistenz von Benutzereinstellungen und zwischengespeicherten Daten.Systemkontextdiagrammflowchart TB
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
4. 🏛 Architektur4.1 Client-Seitiger KernDer Kern der Anwendung ist in einer einzigen index.html-Datei enthalten, die Folgendes umfasst:Vorlagen-Registry-Engine – Lädt und analysiert herma_templates.json.Dynamisches Dropdown-System – Gruppiert nach Zahlenbereichen und alphabetischen Buchstaben.Interaktiver Raster-Renderer – Rendert A4-Bögen mit Klick-zum-Umschalten-Funktionalität.i18n Runtime – Zweisprachige Unterstützung mit nahtlosem Umschalten.CRUD-Datenbankmanager – In-Browser-Datenverwaltung mit JSON-Export.4.2 Cloudflare Workers IntegrationDie Anwendung kommuniziert mit zwei primären Cloudflare-Worker-Endpunkten:1. Sortiment API (sortiment-api.lavu-ooe.workers.dev)Gibt den Produktkatalog im JSON-Format zurück:[
  {
    "artNr": "4040",
    "bez": "Elektro-Kleingeräte",
    "geb": "QR-Box"  
  }
]
Worker-Implementierungs-Snippet:export default {
  async fetch(request, env) {
    const CORS_HEADERS = {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, OPTIONS',
      'Content-Type': 'application/json; charset=utf-8'
    };
    if (request.method === 'OPTIONS') {
      return new Response(null, { headers: CORS_HEADERS });
    }
    try {
      const data = await env.SORTIMENT_KV.get('sortiment', 'json');
      return new Response(JSON.stringify(data), { headers: CORS_HEADERS });
    } catch (error) {
      return new Response(
        JSON.stringify({ error: 'Fehler beim Abrufen der Sortimentsdaten' }),
        { status: 500, headers: CORS_HEADERS }
      );
    }
  }
};
2. Locations API (locations-api.lavu-ooe.workers.dev)Gibt die Liste der ASZ-Standorte zurück:[
  {
    "siteCode": "106",
    "name": "ASZ Asten",
    "zipCode": "4481",
    "region": "Linz-Land & Linz Stadt"
  }
]
Worker-Implementierungs-Snippet:export default {
  async fetch(request, env) {
    const CORS_HEADERS = {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, OPTIONS',
      'Content-Type': 'application/json; charset=utf-8'
    };
    if (request.method === 'OPTIONS') {
      return new Response(null, { headers: CORS_HEADERS });
    }
    try {
      const locations = await env.LOCATIONS_KV.get('locations', 'json');
      return new Response(JSON.stringify(locations), { headers: CORS_HEADERS });
    } catch (error) {
      return new Response(
        JSON.stringify({ error: 'Fehler beim Abrufen der Standortdaten' }),
        { status: 500, headers: CORS_HEADERS }
      );
    }
  }
};
4.3 Service Worker & Offline-StrategieDer Service Worker (sw.js) implementiert eine Network-First-Strategie für dynamische JSON-Daten und eine Cache-First-Strategie für statische Assets.const CACHE_NAME = 'lavu-studio-v10';
const STATIC_ASSETS = [
  './',
  './index.html',
  './manifest.json',
  './favicon.svg',
  './logo.png',
  './web-app-manifest-192x192.png',
  './web-app-manifest-512x512.png'
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

self.addEventListener('activate', event => {
  event.waitUntil(
    caches.keys().then(keys => {
      return Promise.all(
        keys.filter(key => key !== CACHE_NAME).map(key => caches.delete(key))
      );
    }).then(() => self.clients.claim())
  );
});
4.4 API Fetch & Cache Fallback SequenzDas folgende Sequenzdiagramm illustriert den Ablauf von Netzwerkanfragen mit automatischem Fallback auf den lokalen Speicher:sequenceDiagram
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
5. 🎨 Etikettendesign & Rendering EngineDie Kern-Rendering-Engine wandelt HERMA-Vorlagendefinitionen mit präzisen geometrischen Berechnungen in interaktive A4-Bögen um.5.1 Berechnung der RastergeometrieDer Etiketten-Renderer berechnet dynamische Layout-Geometrien basierend auf den Vorlagenparametern aus herma_templates.json.Gegeben seien Spalten $C$, Zeilen $R$, Etikettenbreite $W_{\text{mm}}$, Etikettenhöhe $H_{\text{mm}}$, Abstände $G_x$ und $G_y$, sowie Ränder $M_{\text{left}}$ und $M_{\text{top}}$:$$\text{Gesamtbreite } (W_{\text{total}}) = (C \cdot W_{\text{mm}}) + ((C - 1) \cdot G_x)$$$$\text{Gesamthöhe } (H_{\text{total}}) = (R \cdot H_{\text{mm}}) + ((R - 1) \cdot G_y)$$$$\text{Rechter Rand } (M_{\text{right}}) = 210\text{mm} - W_{\text{total}} - M_{\text{left}}$$$$\text{Unterer Rand } (M_{\text{bottom}}) = 297\text{mm} - H_{\text{total}} - M_{\text{top}}$$Die Position eines Etiketts an der Spalte $i \in [0, C-1]$ und Zeile $j \in [0, R-1]$ wird durch folgende Koordinaten bestimmt:$$X(i) = M_{\text{left}} + i \cdot (W_{\text{mm}} + G_x)$$$$Y(j) = M_{\text{top}} + j \cdot (H_{\text{mm}} + G_y)$$Vorlagenstruktur (herma_templates.json){
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
Raster-Rendering-Funktionfunction renderGrid(containerId, data) {
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
  
  container.innerHTML = '';
  const maxLabels = t.cols * t.rows;
  
  for (let i = 1; i <= maxLabels; i++) {
    const label = document.createElement('div');
    label.className = 'lb';
    if (i >= startPos && i < startPos + count) {
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
      label.className += ' empty'; 
    }
    container.appendChild(label);
  }
}
5.2 Dynamische SkalierungUm CSS-Layoutbrüche in Vorschaukarten zu vermeiden, werden Skalierungsfaktoren berechnet:$$\text{scale}_x = \frac{W_{\text{mm}}}{W_{\text{base}}}, \quad \text{scale}_y = \frac{H_{\text{mm}}}{H_{\text{base}}}$$$$\text{scale} = \min(\text{scale}_x, \text{scale}_y, 1.0)$$const baseWidth = 70;   
const baseHeight = 41;  
const scaleX = t.width_mm / baseWidth;
const scaleY = t.height_mm / baseHeight;
const scale = Math.min(scaleX, scaleY, 1);
container.style.setProperty('--label-scale', scale);
5.3 Interaktive BogenvorschauDie modale Vorschau ermöglicht es Benutzern, auf einzelne Etikettenpositionen zu klicken, um deren Druckstatus umzuschalten.6. 📊 Datenfluss & Workflow-DiagrammeVollständiger Anwendungs-Workflowflowchart TD
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
    R -- Datenbank --> V["🗄️ CRUD-Operationen"]
    V --> W["➕ Elemente hinzufügen / bearbeiten / löschen"]
    W --> X["💾 In localStorage speichern"]
    X --> E
7. 🌟 HauptfunktionenDynamische HERMA-Bogen-Engine:Interaktive Klick-zum-Umschalten-Bogenpositionierung auf Standard-A4-Rastern.Echtzeit-Vorschau mit automatischer Neuberechnung.Unterstützung für rechteckige und runde Etikettenvorlagen.Serverless & Offline First:Cloudflare Workers für performante Edge-APIs.Lokaler Browser-Cache (localStorage & ServiceWorker) sorgt für vollkommene Offline-Lauffähigkeit.Zweisprachige Unterstützung (i18n):Nahtloser Wechsel zwischen Deutsch (de) und Englisch (en).Responsive & Mobile UI:Optimierte Ansichten für Tablets, Smartphones und Desktop-Terminals.8. 🔧 Technische SpezifikationenSpeicher- & PersistenzschemaSpeicherschlüsselTypBeschreibunglavu_langstringAusgewählte i18n-Sprache (de | en)lavu_locationstringAktuell ausgewählte Site-Code-ID (z. B. "106")lavu_locations_urlstringRemote-Worker-Endpunkt für Standortelavu_locations_cachestring (JSON)Zwischengespeicherte Standortlistelavu_studio_defaults_v8string (JSON)Standard-Format, Anzahl und Startpositionlavu_studio_sortiment_v8string (JSON)Lokal bearbeiteter Sortimentsspeicher9. 🖨 DruckanleitungSkalierung: Auf 100% / Tatsächliche Größe einstellen (nicht "An Seite anpassen").Ränder: Auf Keine oder 0mm einstellen.Papiergröße: DIN A4 (Portrait).Hintergrundgrafiken: Aktivieren.@media print {
  @page {
    size: A4 portrait;
    margin: 0 !important;
  }
  
  body {
    background: white !important;
  }

  .a4-print-sheet {
    width: 210mm !important;
    height: 297mm !important;
    box-shadow: none !important;
  }
}
10. 🚀 Schnellstart# Repository klonen
git clone https://github.com/LAVU-OOE/RePrint.git
cd RePrint

# Lokalen Webserver starten
python3 -m http.server 8080

# Im Browser aufrufen
# http://localhost:8080
11. 📁 Projektstrukturreprint-studio/
├── index.html                  # Haupt-PWA-Container & Layout Engine
├── herma_templates.json        # HERMA A4-Geometriedefinitionen
├── manifest.json               # Web App Manifest
├── sw.js                       # Service Worker
├── favicon.svg                 # Vektor-App-Icon
├── logo.png                    # Branding Logo
└── workers/
    ├── sortiment-api/          # Cloudflare Worker Sortiment-Endpunkt
    └── locations-api/          # Cloudflare Worker Standorte-Endpunkt
12. 🗄 DatenbankverwaltungÜber das Optionsmenü können Sortimentsdaten lokal hinzugefügt, bearbeitet, gelöscht und als JSON exportiert werden.function exportDatabaseJSON(dataArray) {
  const jsonData = JSON.stringify(dataArray, null, 2);
  const blob = new Blob([jsonData], { type: "application/json" });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = "sortiment_export.json";
  a.click();
  URL.revokeObjectURL(url);
}
13. 🤝 Richtlinien für MitwirkendePWA / Standard JS: Keine schweren Frameworks (React, Vue) verwenden; Vanilla JS ES6+ beibehalten.Geometrie-Präzision: Neue HERMA-SKUs mit einem digitalen Messschieber verifizieren ($W_{\text{mm}}, H_{\text{mm}}, G_x, G_y$).Browser-Kompatibilität: Über Chrome, Edge, Firefox und iOS Safari testen.14. 📄 LizenzDieses Projekt steht unter der MIT-Lizenz.MIT License

Copyright (c) 2026 LAVU OÖ Community Project

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
