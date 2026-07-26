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