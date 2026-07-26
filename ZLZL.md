## RE:PRINT Studio v9

## 📖 Inhaltsverzeichnis

1.  [Einführung](https://gemini.google.com/#-einf%C3%BChrung "null")
    
2.  [Disclaimer / Rechtlicher Hinweis](https://gemini.google.com/#-disclaimer--rechtlicher-hinweis "null")
    
3.  [Systemübersicht](https://gemini.google.com/#-system%C3%BCbersicht "null")
    
4.  [Architektur](https://gemini.google.com/#-architektur "null")
    
    *   [Client-Side Core](https://gemini.google.com/#client-side-core "null")
        
    *   [Cloudflare Workers Integration](https://gemini.google.com/#cloudflare-workers-integration "null")
        
    *   [Service Worker & Offline-Strategie](https://gemini.google.com/#service-worker--offline-strategie "null")
        
    *   [API-Abruf & Cache-Fallback-Sequenz](https://gemini.google.com/#api-abruf--cache-fallback-sequenz "null")
        
5.  [Etikettendesign & Rendering-Engine](https://gemini.google.com/#-etikettendesign--rendering-engine "null")
    
    *   [Gittergeometrie-Berechnung](https://gemini.google.com/#gittergeometrie-berechnung "null")
        
    *   [Dynamische Skalierung](https://gemini.google.com/#dynamische-skalierung "null")
        
    *   [Interaktive Bogenvorschau](https://gemini.google.com/#interaktive-bogenvorschau "null")
        
6.  [Datenfluss & Workflow-Diagramme](https://gemini.google.com/#-datenfluss--workflow-diagramme "null")
    
7.  [Hauptmerkmale](https://gemini.google.com/#-hauptmerkmale "null")
    
8.  [Technische Spezifikationen](https://gemini.google.com/#-technische-spezifikationen "null")
    
9.  [Druckanweisungen](https://gemini.google.com/#-druckanweisungen "null")
    
10.  [Schnellstart](https://gemini.google.com/#-schnellstart "null")
     
11.  [Projektstruktur](https://gemini.google.com/#-projektstruktur "null")
     
12.  [Datenbankverwaltung](https://gemini.google.com/#-datenbankverwaltung "null")
     
13.  [Richtlinien für Mitwirkende](https://gemini.google.com/#-richtlinien-f%C3%BCr-mitwirkende "null")
     
14.  [Lizenz](https://gemini.google.com/#-lizenz "null")
     

## 🚀 Einführung

**RE:PRINT Studio v9** ist eine ressourcenschonende, clientseitige Progressive Web Application (PWA), die für ASZ-Standorte in Oberösterreich entwickelt wurde. Sie bietet dynamische Etikettenformatierung, Live-Berechnungen für die Druckvorschau und das Rendern von anpassbaren Vorlagenbögen für Standard-HERMA A4-Vorlagen.

Die Anwendung wird vollständig im Browser ausgeführt und nutzt moderne Webtechnologien, um eine nahtlose Benutzererfahrung auf Desktop- und Mobilgeräten zu bieten, mit robusten Offline-Funktionen.

## ⚠️ Disclaimer / Rechtlicher Hinweis

> **Wichtiger Hinweis / Disclaimer:**
> 
> **Diese Software ist ein unabhängiges Community-Projekt und ist nicht offiziell mit der LAVU OÖ (O.Ö. Landes-Abfallverwertungsunternehmen GmbH) oder den Bezirksabfallverbänden (BAV OÖ) verbunden.**
> 
> **Dies ist keine offizielle Anwendung oder Software von LAVU OÖ oder BAV OÖ. Alle Marken, Logos und Bezeichnungen gehören ihren jeweiligen Eigentümern.**
> 
> **Hinweis:**
> 
> **Diese Anwendung ist ein unabhängiges Open-Source-Projekt und wird nicht offiziell von LAVU OÖ oder BAV OÖ unterstützt, gesponsert oder ist mit diesen verbunden.**

## 🏗 Systemübersicht

RE:PRINT Studio v9 basiert auf einer **Serverless-Architektur**, die Folgendes kombiniert:

*   **Reines clientseitiges Rendering** mit HTML5, CSS3 und Vanilla JavaScript (ES6+)
    
*   **Cloudflare Workers** für API-Endpunkte, die dynamische JSON-Daten bereitstellen
    
*   **Service Workers** für progressive Verbesserung und Offline-Unterstützung
    
*   **localStorage** für die clientseitige Persistenz von Benutzereinstellungen und zwischengespeicherten Daten
    

### Systemkontext-Diagramm

```
flowchart TB
    subgraph Client ["Browser-Client (PWA)"]
        UI["🎨 UI-Engine<br/>(index.html)"]
        SW["⚙️ Service Worker<br/>(sw.js)"]
        LS["💾 localStorage<br/>Cache & Einstellungen"]
    end

    subgraph Cloudflare ["Cloudflare Workers Edge Network"]
        SA["📦 Sortiment API<br/>/sortiment-api"]
        LA["📍 Standorte API<br/>/locations-api"]
    end

    subgraph External ["Externe Assets & Registry"]
        TEMPLATES["📄 HERMA Vorlagen<br/>(herma_templates.json)"]
        GITHUB["🌐 GitHub Pages<br/>Statische Assets"]
    end

    UI -->|fetch| SA
    UI -->|fetch| LA
    UI -->|fetch| TEMPLATES
    SW -->|Cache-Strategie| GITHUB
    UI -->|Read/Write| LS
    SW -->|Network-First Cache| SA
    SW -->|Network-First Cache| LA

```

## 🏛 Architektur

### Client-Side Core

Der Kern der Anwendung ist in einer einzigen `index.html`\-Datei enthalten, die Folgendes umfasst:

1.  **Vorlagen-Registry-Engine** – Lädt und analysiert `herma_templates.json`
    
2.  **Dynamisches Dropdown-System** – Gruppiert nach numerischen Bereichen und alphabetischen Buchstaben
    
3.  **Interaktiver Gitter-Renderer** – Rendert A4-Bögen mit Klick-zum-Umschalten-Funktionalität
    
4.  **i18n-Laufzeitumgebung** – Zweisprachige Unterstützung mit nahtlosem Wechsel
    
5.  **CRUD-Datenbankmanager** – Datenverwaltung im Browser mit JSON-Export
    

### Cloudflare Workers Integration

Die Anwendung kommuniziert mit zwei primären Cloudflare Worker-Endpunkten:

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

**Worker Implementierungs-Snippet:**

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

#### 2\. Standorte API (`locations-api.lavu-ooe.workers.dev`)

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

**Worker Implementierungs-Snippet:**

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

#### Fetch-Strategie für JSON-Endpunkte

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

#### Offline-Fallback für Navigation

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

### API-Abruf & Cache-Fallback-Sequenz

```
sequenceDiagram
    autonumber
    actor User as 👤 Benutzer
    participant UI as 🖥️ Client UI (index.html)
    participant SW as ⚙️ Service Worker
    participant Cache as 💾 Cache / localStorage
    participant API as ☁️ Cloudflare Worker API

    User->>UI: Wählt Standort / Sortimentsartikel
    UI->>SW: fetch(API Endpunkt)
    
    alt Netzwerk Online
        SW->>API: HTTP GET /locations-api oder /sortiment-api
        API-->>SW: 200 OK (JSON Payload)
        SW->>Cache: Cache-Eintrag aktualisieren
        SW-->>UI: Frische JSON-Antwort zurückgeben
    else Netzwerk Offline / Fetch Fehler
        SW->>Cache: Übereinstimmende zwischengespeicherte Anfrage
        alt Cache Treffer
            Cache-->>SW: Zwischengespeichertes JSON zurückgeben
            SW-->>UI: Zwischengespeichertes JSON zurückgeben (Offline-Modus)
        else Cache Fehlschlag
            SW-->>UI: 503 Service Unavailable (Fallback Payload)
        end
    end
    
    UI->>User: Interaktives Gitter & Etikettenvorschau rendern

```

## 🎨 Etikettendesign & Rendering-Engine

Die zentrale Rendering-Engine wandelt HERMA-Vorlagendefinitionen in interaktive A4-Bögen mit präzisen geometrischen Berechnungen um.

### Gittergeometrie-Berechnung

Der Etiketten-Renderer berechnet dynamische Layout-Geometrie basierend auf in `herma_templates.json` deklarierten Vorlagenparametern.

#### Mathematische Grundlage

Wobei:

|

| **Variable** | **Beschreibung** | | | Anzahl der Spalten (`cols`) | | | Anzahl der Reihen (`rows`) | | | Etikettenbreite in Millimetern | | | Etikettenhöhe in Millimetern | | | Horizontale und vertikale Abstände in Millimetern |

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

#### Gitter-Rendering-Funktion

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

Um zu verhindern, dass das CSS-Layout in Vorschaubereichen zerbricht, werden Skalierungsvektoren als dynamische Inline-Eigenschaften berechnet:

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

## 📊 Datenfluss & Workflow-Diagramme

### Kompletter Anwendungs-Workflow

\`\`\`xml

\`\`\`

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
    J --> K["🖱️ Klick auf Etikettenpositionen"]
    K --> L["🔄 Etikettenstatus umschalten"]
    L --> M["✏️ Anzahl & Startposition aktualisieren"]
    M --> N["🎨 Bogen-Layout neu rendern"]
    
    I -- Jetzt drucken --> O["🖨️ Browser-Druckdialog öffnen"]
    O --> P["📄 Gedruckten A4-Bogen ausgeben"]
    
    I -- Optionen --> Q["⚙️ Einstellungs-Modal öffnen"]
    Q --> R{"📂 Tab auswählen"}
    R -- Service Worker --> S["🌐 API-Endpunkte verwalten"]
    S --> T["✏️ Sortiments-Endpunkt aktualisieren"]
    S --> U["✏️ Standort-Endpunkt aktualisieren"]
    
    R -- Datenbank --> V["🗄️ CRUD-Operationen"]
    V --> W["➕ Elemente hinzufügen / bearbeiten / löschen"]
    W --> X["💾 In localStorage speichern"]
    X --> E
    V --> Y["📥 Datenbank als JSON exportieren"]

```

### Etikettendesign-Workflow

```
flowchart LR
    subgraph Input ["1. Dateneingabe"]
        A1["📄 HERMA SKU auswählen"] --> A2["⚙️ Geometrie-Spezifikationen laden"]
        B1["📍 Standort auswählen"] --> B2["🏷️ Kopfzeilen-Etikett abrufen"]
        C1["📦 Produkt auswählen"] --> C2["🔢 ArtNr & Beschreibung abrufen"]
        D1["✍️ Suffix eingeben"] --> D2["🏷️ Optionales Badge"]
        E1["🔢 Anzahl & Startposition"]
    end

    subgraph Rendering ["2. Rendering-Engine"]
        A2 --> F["📐 Dynamisches Gitter berechnen"]
        B2 --> F
        C2 --> F
        D2 --> F
        E1 --> F
        F --> G1["✨ Aktive Zellen rendern"]
        F --> G2["⚪ Leere Zellen rendern"]
        G1 --> H["🖼️ Composite Vorschau-Bogen"]
        G2 --> H
    end

    subgraph Interaction ["3. Interaktive Bearbeitung"]
        H --> I["🖥️ Interaktive modale Ansicht"]
        I --> J["🖱️ Zelle klicken"]
        J --> K["🔄 Offsets neu berechnen"]
        K --> H
    end

    subgraph Output ["4. Druckausgabe"]
        H --> L["🖨️ Druckauftrag ausführen"]
        L --> M["📄 A4 Vektorgrafiken rendern"]
        M --> N["🏷️ Physischer Bogen gedruckt"]
    end

```

### Anwendungsstatus-Lebenszyklus

```
stateDiagram-v2
    [*] --> Uninitialisiert

    state Uninitialisiert {
        [*] --> RegisterServiceWorker
        RegisterServiceWorker --> CheckCache
    }

    Uninitialisiert --> Bereit : Ressourcen & Daten geladen

    state Bereit {
        [*] --> Standby
        Standby --> LocationSelected : ASZ-Standort auswählen
        LocationSelected --> ItemSelected : Produktartikel auswählen
        ItemSelected --> GridCalculated : Geometrie berechnen
        GridCalculated --> LivePreview : CSS-Gitter rendern
    }

    Bereit --> ModalEditing : Auf Bogenvorschau klicken
    
    state ModalEditing {
        [*] --> ModalOpen
        ModalOpen --> ToggleCell : Gitterzelle klicken
        ToggleCell --> RecalculateOffset : Start/Anzahl aktualisieren
        RecalculateOffset --> ModalOpen : Bogen neu zeichnen
        ModalOpen --> ModalClosed : Modal schließen
    }

    ModalEditing --> Bereit : Zurück zur Haupt-UI
    Bereit --> Printing : Auf "Jetzt drucken" klicken
    Printing --> Bereit : Druckansicht schließen

```

## 🌟 Hauptmerkmale

### 1\. Dynamische HERMA Bogen-Engine

*   **Interaktive Klick-zum-Umschalten** Bogenpositionierung auf Standard-A4-Gittern
    
*   **Echtzeit-Vorschau** mit automatischer Neuberechnung
    
*   Unterstützung für **rechteckige und runde** Etikettenvorlagen
    

### 2\. Serverless & Offline-First

*   Verwendet **Cloudflare Workers** für API-Endpunkte
    
*   Fällt auf **zwischengespeicherten Browser-Status** (`localStorage`) zurück
    
*   **Service Worker** bietet Offline-Fähigkeit mit Network-First-Strategie
    

### 3\. Zweisprachige Unterstützung (i18n)

*   Natives Umschalten zur Laufzeit zwischen **Deutsch (`de`)** und **Englisch (`en`)**
    
*   Dauerhafte Spracheinstellung wird in `localStorage` gespeichert
    

### 4\. Geräteübergreifende reaktionsschnelle UI

*   **Für Mobilgeräte optimierte Layout**\-Umschaltung für Vorlagen und Standortauswahlen
    
*   **Adaptive Breakpoints** bei 768px und 520px
    
*   Für Touch optimierte interaktive Elemente
    

### 5\. PWA-fähig

*   **Offline-Unterstützung** mit Service Worker
    
*   **Manifest-gesteuerte Installationsaufforderungen** auf kompatiblen Browsern
    
*   **Standalone-Anzeige**\-Konfiguration für ein app-ähnliches Erlebnis
    

### 6\. Datenbankverwaltung

*   **CRUD-Operationen im Browser** für die Produktdatenbank
    
*   **JSON-Export**\-Funktionalität
    
*   **Auto-Sync** zwischen localStorage und UI
    

## 🔧 Technische Spezifikationen

### Speicher- & Persistenzschema

| **Speicherschlüssel** | **Typ** | **Beschreibung** | | `lavu_lang` | `string` | Ausgewähltes i18n-Gebietsschema (`de` | `en`) | | `lavu_location` | `string` | Aktuell ausgewählte Site-Code-ID (z.B. `"106"`) | | `lavu_locations_url` | `string` | Remote-Worker-Endpunkt für Standorte | | `lavu_locations_cache` | `string` (JSON) | Zwischengespeicherte Standortlisten-Nutzdaten | | `lavu_studio_defaults_v8` | `string` (JSON) | Letztes bekanntes SKU-Format, Anzahl und Positions-Offset | | `lavu_studio_sortiment_v8` | `string` (JSON) | Lokal bearbeiteter Datenbank-Arbeitsbereich | | `lavu_preview_zoom` | `string` | Zoomstufe für modale Vorschau |

### Media Query Breakpoint Matrix

| **Ansichtsfenster-Breite** | **Visuelle Anpassungen** | | **\> 768px** | Vollständiges Dual-Pane-Vorschau-Desktop-Layout mit interaktivem Bogen-Modal | | **<= 768px** | Verbirgt die Live-Vorschau im Seitenbereich (`.ps-wrapper`). Wechselt zum einspaltigen Fluss | | **<= 520px** | Versteckt Desktop-Header-Standort-Badges (`.hdr-r`). Aktiviert das Steuerelement zur mobilen Standortauswahl (`.mobile-location-wrapper`) |

### Leistungsmetriken

```
console.time('renderGrid');
r2('mdl', data);
console.timeEnd('renderGrid');

```

## 🖨 Druckanweisungen

Befolgen Sie für optimale Druckergebnisse diese Einstellungen im Druckdialog Ihres Browsers:

1.  **Skalierung:** Stellen Sie **100% / Tatsächliche Größe** ein
    
2.  **Ränder:** Auf **Keine** oder **0mm** setzen
    
3.  **Papiergröße:** Auswahl von **A4 Hochformat** erzwingen
    
4.  **Hintergrundgrafiken:** Aktivieren Sie diese, wenn Sie die Gitterlinien sehen möchten
    

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
    
2.  **Über einen beliebigen statischen Site-Server hosten**
    
    ```
    python3 -m http.server 8080
    # ODER
    npx http-server .
    # ODER
    php -S localhost:8080
    
    ```
    
3.  **In Ihrem Browser öffnen**
    
    ```
    http://localhost:8080
    
    ```
    

### Erstmalige Nutzung

1.  **Standort auswählen** – Wählen Sie Ihre ASZ-Filiale aus dem dynamisch geladenen Dropdown-Menü
    
2.  **Einen Artikel auswählen** – Suchen Sie entweder nach **Art.-Nr.** (numerisch gruppiert) oder nach **Bezeichnung** (alphabetisch gruppiert)
    
3.  **Drucklayout anpassen** – Klicken Sie auf das Vorschaubild, um den interaktiven Bogen zu öffnen
    
4.  **Drucken** – Klicken Sie auf "Jetzt drucken", um Ihren A4-Bogen zu erstellen
    

## 📁 Projektstruktur

```
.
├── 📄 index.html                  # Haupt-SPA-UI-Container & CSS-Layout-Engine
├── 📄 herma_templates.json        # A4-Gitter-Registry-Definitionen
├── 📄 manifest.json               # Web-App-Manifest für PWA-Installation
├── 📄 site.webmanifest            # Sekundäre App-Manifest-Definition
├── 📄 sw.js                       # Service Worker für Offline-Unterstützung
├── 📄 README.md                   # Anwendungsdokumentation
├── 📄 LICENSE                     # MIT-Lizenz
├── 🖼️ favicon.svg                 # Skalierbares Vektorgrafik-Symbol
├── 🖼️ favicon-96x96.png           # Statisches Raster-Asset-Symbol
├── 🖼️ logo.png                    # Anwendungslogo
├── 🖼️ apple-touch-icon.png        # Apple iOS-Symbol
├── 🖼️ web-app-manifest-192x192.png # PWA-Symbol (192px)
├── 🖼️ web-app-manifest-512x512.png # PWA-Symbol (512px)
└── 📄 tree.md                     # Dateistruktur-Dokumentation

```

## 🗄 Datenbankverwaltung

### CRUD-Operationen im Browser

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

### Standardeinstellungen speichern

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

### Entwicklungs-Setup

1.  **Forken Sie das Repository**
    
2.  **Erstellen Sie einen Feature-Branch**
    
    ```
    git checkout -b feature/your-feature-name
    
    ```
    
3.  **Nehmen Sie Ihre Änderungen vor**
    
4.  **Lokal testen** – Stellen Sie sicher, dass die Anwendung fehlerfrei ausgeführt wird
    
5.  **Mit konventionellen Commit-Nachrichten committen**
    
    ```
    git commit -m "feat: Add support for new HERMA template SKU"
    git commit -m "fix: Resolve mobile layout issues on Safari"
    git commit -m "docs: Update README with new Cloudflare API endpoints"
    
    ```
    
6.  **Pushen und einen Pull Request erstellen**
    

### Test-Richtlinien

*   **Browserübergreifendes Testen**: Chrome, Firefox, Safari, Edge
    
*   **Mobiles Testen**: iOS Safari, Android Chrome
    
*   **Offline-Testen**: Deaktivieren Sie das Netzwerk und überprüfen Sie die zwischengespeicherte Funktionalität
    
*   **Druck-Testen**: Überprüfen Sie die A4-Ausgabe mit verschiedenen Druckerkonfigurationen
    

### Code-Standards

*   **ES6+** JavaScript mit `const` und `let`
    
*   **CSS-Variablen** für Theming
    
*   **Semantische HTML5**\-Elemente
    
*   **Progressive Enhancement** Prinzipien
    

## 📄 Lizenz

Dieses Projekt ist Open Source und unter der **MIT-Lizenz** lizenziert.

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