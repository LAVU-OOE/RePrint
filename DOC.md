<div contenteditable="false" translate="no" class="ProseMirror" aria-label="Canvas-Editor" aria-busy="false" data-disable-editing="false">
<h1>RE:PRINT Studio v9</h1><h2>📖 Table of Contents</h2><ol><li><p><a href="#-introduction" title="null">Introduction</a></p></li><li><p><a href="#-disclaimer--rechtlicher-hinweis" title="null">Disclaimer / Rechtlicher Hinweis</a></p></li><li><p><a href="#-system-overview" title="null">System Overview</a></p></li><li><p><a href="#-architecture" title="null">Architecture</a></p><ul><li><p><a href="#client-side-core" title="null">Client-Side Core</a></p></li><li><p><a href="#cloudflare-workers-integration" title="null">Cloudflare Workers Integration</a></p></li><li><p><a href="#service-worker--offline-strategy" title="null">Service Worker &amp; Offline Strategy</a></p></li><li><p><a href="#api-fetch--cache-fallback-sequence" title="null">API Fetch &amp; Cache Fallback Sequence</a></p></li></ul></li><li><p><a href="#-label-design--rendering-engine" title="null">Label Design &amp; Rendering Engine</a></p><ul><li><p><a href="#grid-geometry-calculation" title="null">Grid Geometry Calculation</a></p></li><li><p><a href="#dynamic-scaling" title="null">Dynamic Scaling</a></p></li><li><p><a href="#interactive-sheet-preview" title="null">Interactive Sheet Preview</a></p></li></ul></li><li><p><a href="#-data-flow--workflow-diagrams" title="null">Data Flow &amp; Workflow Diagrams</a></p></li><li><p><a href="#-key-features" title="null">Key Features</a></p></li><li><p><a href="#-technical-specifications" title="null">Technical Specifications</a></p></li><li><p><a href="#-printing-instructions" title="null">Printing Instructions</a></p></li><li><p><a href="#-quick-start" title="null">Quick Start</a></p></li><li><p><a href="#-project-structure" title="null">Project Structure</a></p></li><li><p><a href="#-database-management" title="null">Database Management</a></p></li><li><p><a href="#-contribution-guidelines" title="null">Contribution Guidelines</a></p></li><li><p><a href="#-license" title="null">License</a></p></li></ol><h2>🚀 Introduction</h2><p><strong>RE:PRINT Studio v9</strong> is a lightweight, client-side Progressive Web Application (PWA) designed for ASZ branch locations in Upper Austria. It provides dynamic label formatting, live print preview calculations, and customizable template sheet rendering for standard HERMA A4 templates.</p><p>The application operates entirely in the browser, leveraging modern web technologies to deliver a seamless experience across desktop and mobile devices, with robust offline capabilities.</p><h2>⚠️ Disclaimer / Rechtlicher Hinweis</h2><blockquote><p><strong>Important Notice / Disclaimer:</strong></p><p><strong>This software is an independent community project and is not officially affiliated with LAVU OÖ (Upper Austrian State Waste Management Company) or the district waste management associations (BAV OÖ).</strong></p><p><strong>This is not an official application or software of LAVU OÖ or BAV OÖ. All trademarks, logos, and designations belong to their respective owners.</strong></p><p><strong>Notice:</strong></p><p><strong>This application is an independent open-source project and is not officially affiliated with, endorsed by, or sponsored by LAVU OÖ or BAV OÖ.</strong></p></blockquote><h2>🏗 System Overview</h2><p>RE:PRINT Studio v9 is built on a <strong>serverless architecture</strong> that combines:</p><ul><li><p><strong>Pure client-side rendering</strong> using HTML5, CSS3, and vanilla JavaScript (ES6+)</p></li><li><p><strong>Cloudflare Workers</strong> for API endpoints serving dynamic JSON data</p></li><li><p><strong>Service Workers</strong> for progressive enhancement and offline support</p></li><li><p><strong>localStorage</strong> for client-side persistence of user preferences and cached data</p></li></ul><h3>System Context Diagram</h3><pre><code>flowchart TB
    subgraph Client ["Browser Client (PWA)"]
        UI["🎨 UI Engine&lt;br/&gt;(index.html)"]
        SW["⚙️ Service Worker&lt;br/&gt;(sw.js)"]
        LS["💾 localStorage&lt;br/&gt;Cache &amp; Settings"]
    end

```
subgraph Cloudflare ["Cloudflare Workers Edge Network"]
    SA["📦 Sortiment API&lt;br/&gt;/sortiment-api"]
    LA["📍 Locations API&lt;br/&gt;/locations-api"]
end

subgraph External ["External Assets &amp; Registry"]
    TEMPLATES["📄 HERMA Templates&lt;br/&gt;(herma_templates.json)"]
    GITHUB["🌐 GitHub Pages&lt;br/&gt;Static Assets"]
end
```

| UI --> | fetch | SA |
| --- | --- | --- |
| UI --> | fetch | LA |
| UI --> | fetch | TEMPLATES |
| SW --> | Cache Strategy | GITHUB |
| UI --> | Read/Write | LS |
| SW --> | Network-First Cache | SA |
| SW --> | Network-First Cache | LA |

<br class="ProseMirror-trailingBreak"></code></pre><h2>🏛 Architecture</h2><h3>Client-Side Core</h3><p>The application's core is contained within a single <code>index.html</code> file, which includes:</p><ol><li><p><strong>Template Registry Engine</strong> – Loads and parses <code>herma_templates.json</code></p></li><li><p><strong>Dynamic Dropdown System</strong> – Grouped by numeric ranges and alphabetical letters</p></li><li><p><strong>Interactive Grid Renderer</strong> – Renders A4 sheets with click-to-toggle functionality</p></li><li><p><strong>i18n Runtime</strong> – Bilingual support with seamless switching</p></li><li><p><strong>CRUD Database Manager</strong> – In-browser data management with JSON export</p></li></ol><h3>Cloudflare Workers Integration</h3><p>The application interfaces with two primary Cloudflare Worker endpoints:</p><h4>1. Sortiment API (<code>sortiment-api.lavu-ooe.workers.dev</code>)</h4><p>Returns the product catalog in JSON format:</p><pre><code>[
{
"artNr": "4040",
"bez": "Elektro-Kleingeräte",
"geb": "QR-Box"  
}
]

<br class="ProseMirror-trailingBreak"></code></pre><p><strong>Worker Implementation Snippet:</strong></p><pre><code>export default {
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

<br class="ProseMirror-trailingBreak"></code></pre><h4>2. Locations API (<code>locations-api.lavu-ooe.workers.dev</code>)</h4><p>Returns the list of ASZ branch locations:</p><pre><code>[
{
"siteCode": "106",
"name": "ASZ Asten",
"zipCode": "4481",
"region": "Linz-Land &amp; Linz Stadt"
}
]

<br class="ProseMirror-trailingBreak"></code></pre><p><strong>Worker Implementation Snippet:</strong></p><pre><code>export default {
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

<br class="ProseMirror-trailingBreak"></code></pre><h3>Service Worker &amp; Offline Strategy</h3><p>The Service Worker implements a <strong>Network-First</strong> strategy for dynamic JSON data and a <strong>Cache-First</strong> strategy for static assets.</p><h4>Registration &amp; Installation</h4><pre><code>const CACHE_NAME = 'lavu-studio-v10';
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

self.addEventListener('install', event =&gt; {
event.waitUntil(
caches.open(CACHE_NAME)
.then(cache =&gt; cache.addAll([...STATIC_ASSETS, ...DYNAMIC_JSON_URLS]))
.then(() =&gt; self.skipWaiting())
);
});

<br class="ProseMirror-trailingBreak"></code></pre><h4>Fetch Strategy for JSON Endpoints</h4><pre><code>if (DYNAMIC_JSON_URLS.some(jsonUrl =&gt; url.href === jsonUrl)) {
event.respondWith(
fetch(request, { cache: 'no-store' })
.then(response =&gt; {
const clonedResponse = response.clone();
caches.open(CACHE_NAME)
.then(cache =&gt; cache.put(request, clonedResponse));
return response;
})
.catch(() =&gt; {
return caches.match(request)
.then(cachedResponse =&gt; {
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

<br class="ProseMirror-trailingBreak"></code></pre><h4>Offline Fallback for Navigation</h4><pre><code>if (request.mode === 'navigate') {
event.respondWith(
fetch(request)
.then(response =&gt; {
const clonedResponse = response.clone();
caches.open(CACHE_NAME)
.then(cache =&gt; cache.put(request, clonedResponse));
return response;
})
.catch(() =&gt; {
return caches.match('/index.html')
.then(cachedResponse =&gt; {
if (cachedResponse) {
console.log('[SW] Serving offline fallback page');
return cachedResponse;
}
return new Response(
'&lt;html&gt;&lt;body&gt;&lt;h1&gt;Offline&lt;/h1&gt;&lt;p&gt;Bitte verbinden Sie sich mit dem Internet, um die App zu nutzen.&lt;/p&gt;&lt;/body&gt;&lt;/html&gt;',
{ headers: { 'Content-Type': 'text/html' } }
);
});
})
);
return;
}

<br class="ProseMirror-trailingBreak"></code></pre><h3>API Fetch &amp; Cache Fallback Sequence</h3><pre><code>sequenceDiagram
autonumber
actor User as 👤 User
participant UI as 🖥️ Client UI (index.html)
participant SW as ⚙️ Service Worker
participant Cache as 💾 Cache / localStorage
participant API as ☁️ Cloudflare Worker API

```
User-&gt;&gt;UI: Selects Location / Sortiment Item
UI-&gt;&gt;SW: fetch(API Endpoint)

alt Network Online
    SW-&gt;&gt;API: HTTP GET /locations-api or /sortiment-api
    API--&gt;&gt;SW: 200 OK (JSON Payload)
    SW-&gt;&gt;Cache: Update Cache Entry
    SW--&gt;&gt;UI: Return fresh JSON Response
else Network Offline / Fetch Error
    SW-&gt;&gt;Cache: Match Cached Request
    alt Cache Hit
        Cache--&gt;&gt;SW: Return Cached JSON
        SW--&gt;&gt;UI: Return Cached JSON (Offline Mode)
    else Cache Miss
        SW--&gt;&gt;UI: 503 Service Unavailable (Fallback Payload)
    end
end

UI-&gt;&gt;User: Render Interactive Grid &amp; Label Preview
```

|
🎨 Label Design & Rendering Engine
The core rendering engine transforms HERMA template definitions into interactive A4 sheets with precise geometric calculations.

Grid Geometry Calculation
The label renderer computes dynamic layout geometry based on template parameters declared in herma_templates.json.

Mathematical Foundation
W
total
​
=(C⋅W
mm
​
)+((C−1)⋅G
x
​
)
H
total
​
=(R⋅H
mm
​
)+((R−1)⋅G
y
​
)
Where:

|

| Variable | Description |
| --- | --- | --- | --- |
| C | Number of Columns (cols) |  |  |
| R | Number of Rows (rows) |  |  |
| W 
mm
​
| Label Width in Millimeters |  |  |
| H 
mm
​
| Label Height in Millimeters |  |  |
| G 
x
​
,G 
y
​
| Horizontal and Vertical Gaps in Millimeters |

Template Structure (herma_templates.json)
{ |  |
| "engine": "HERMA Label Engine", |  |  |  |
| "page_format": { |  |  |  |

```
"size": "A4",
"width_mm": 210.0,
"height_mm": 297.0,
"orientation": "portrait"
```

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

<br class="ProseMirror-trailingBreak"></code></pre><h4>Grid Rendering Function</h4><pre><code>function r2(containerId, data) {
const container = document.getElementById(containerId);
const t = templateRegistry[currentFormatKey];

const totalGridWidth = t.cols * t.width_mm + (t.cols - 1) * t.gap_x_mm;
const totalGridHeight = t.rows * t.height_mm + (t.rows - 1) * t.gap_y_mm;

const rightMargin = 210 - totalGridWidth - t.left_margin_mm;
const bottomMargin = 297 - totalGridHeight - t.top_margin_mm;

container.style.padding = `    ${t.top_margin_mm}mm  ${Math.max(0, rightMargin)}mm  ${Math.max(0, bottomMargin)}mm  ${t.left_margin_mm}mm`;

container.style.gridTemplateColumns = `repeat(${t.cols}, ${t.width_mm}mm)`;
container.style.gridTemplateRows = `repeat(${t.rows}, ${t.height_mm}mm)`;

for (let i = 1; i &lt;= maxLabels; i++) {
const label = document.createElement('div');
label.className = 'lb';
if (i &gt;= start &amp;&amp; i &lt; start + count) {
label.innerHTML = `        &lt;div class="lbt"&gt;${data.topText || '&amp;nbsp;'}&lt;/div&gt; &lt;div class="lbm"&gt; &lt;div class="lba"&gt;${data.artNr || '&amp;nbsp;'}&lt;/div&gt; ${data.suffix ?`&lt;div class="lbs"&gt;${data.suffix}&lt;/div&gt;`: ''} &lt;/div&gt; &lt;div class="lbb"&gt;${data.bezeichnung || '&amp;nbsp;'}&lt;/div&gt; &lt;div class="lbf"&gt;https://lavu-ooe.github.io/&lt;/div&gt;`;
} else {
label.className += ' e';
}
container.appendChild(label);
}
}

<br class="ProseMirror-trailingBreak"></code></pre><h3>Dynamic Scaling</h3><p>To prevent CSS layout breakage inside preview cards, scale vectors are calculated as dynamic inline properties:</p><pre><code>const baseWidth = 70;  
const baseHeight = 41;  
const scaleX = t.width_mm / baseWidth;
const scaleY = t.height_mm / baseHeight;
const scale = Math.min(scaleX, scaleY, 1);
container.style.setProperty('--label-scale', scale);

<br class="ProseMirror-trailingBreak"></code></pre><h3>Interactive Sheet Preview</h3><p>The modal preview allows users to click on individual label positions to toggle their state:</p><pre><code>function toggleLabel(clickedIndex) {
const t = templateRegistry[currentFormatKey];
const maxLabels = t.cols * t.rows;

| let count = parseInt(document.getElementById('i2').value) |  | 0; |
| --- | --- | --- |
| let start = parseInt(document.getElementById('i3').value) |  | 1; |
| let end = start + count - 1; |  |  |

if (count === 0) {
start = clickedIndex;
count = 1;
} else if (clickedIndex &lt; start) {
count = end - clickedIndex + 1;
start = clickedIndex;
} else if (clickedIndex &gt; end) {
count = clickedIndex - start + 1;
} else {
start = clickedIndex;
count = 1;
}

document.getElementById('i2').value = count;
document.getElementById('i3').value = start;
u1();
}

<br class="ProseMirror-trailingBreak"></code></pre><h2>📊 Data Flow &amp; Workflow Diagrams</h2><h3>Complete Application Workflow</h3><p>`xml</p><p>`</p><pre><code>flowchart TD
A["🚀 User Opens App"] --&gt; B{"🔍 Check localStorage"}
B -- Cache Exists --&gt; C["📦 Load Cached Data"]
B -- No Cache --&gt; D["☁️ Fetch from Cloudflare Workers"]
C --&gt; E["📋 Populate Dropdowns"]
D --&gt; E

```
E --&gt; F["📍 User Selects Location"]
F --&gt; G["🏷️ User Selects Product"]
G --&gt; H["👁️ Render Live Preview"]

H --&gt; I{"⚡ User Action"}
I -- Click Preview --&gt; J["🖼️ Open Interactive Sheet Modal"]
J --&gt; K["🖱️ Click Label Positions"]
K --&gt; L["🔄 Toggle Label State"]
L --&gt; M["✏️ Update Count &amp; Start Position"]
M --&gt; N["🎨 Re-render Sheet Layout"]

I -- Print Now --&gt; O["🖨️ Open Browser Print Dialog"]
O --&gt; P["📄 Output Printed A4 Sheet"]

I -- Options --&gt; Q["⚙️ Open Settings Modal"]
Q --&gt; R{"📂 Select Tab"}
R -- Service Worker --&gt; S["🌐 Manage API Endpoints"]
S --&gt; T["✏️ Update Sortiment Endpoint"]
S --&gt; U["✏️ Update Locations Endpoint"]

R -- Database --&gt; V["🗄️ CRUD Operations"]
V --&gt; W["➕ Add / Edit / Delete Items"]
W --&gt; X["💾 Save to localStorage"]
X --&gt; E
V --&gt; Y["📥 Export Database JSON"]
```

<br class="ProseMirror-trailingBreak"></code></pre><h3>Label Design Workflow</h3><pre><code>flowchart LR
subgraph Input ["1. Data Input"]
A1["📄 Select HERMA SKU"] --&gt; A2["⚙️ Load Geometry Specs"]
B1["📍 Select Location"] --&gt; B2["🏷️ Get Header Label"]
C1["📦 Select Product"] --&gt; C2["🔢 Get ArtNr &amp; Description"]
D1["✍️ Enter Suffix"] --&gt; D2["🏷️ Optional Badge"]
E1["🔢 Count &amp; Start Position"]
end

```
subgraph Rendering ["2. Rendering Engine"]
    A2 --&gt; F["📐 Compute Dynamic Grid"]
    B2 --&gt; F
    C2 --&gt; F
    D2 --&gt; F
    E1 --&gt; F
    F --&gt; G1["✨ Render Active Cells"]
    F --&gt; G2["⚪ Render Empty Cells"]
    G1 --&gt; H["🖼️ Composite Preview Sheet"]
    G2 --&gt; H
end

subgraph Interaction ["3. Interactive Editing"]
    H --&gt; I["🖥️ Interactive Modal View"]
    I --&gt; J["🖱️ Click Cell"]
    J --&gt; K["🔄 Re-calculate Offsets"]
    K --&gt; H
end

subgraph Output ["4. Print Output"]
    H --&gt; L["🖨️ Execute Print Job"]
    L --&gt; M["📄 Render A4 Vector Graphics"]
    M --&gt; N["🏷️ Physical Sheet Printed"]
end
```

<br class="ProseMirror-trailingBreak"></code></pre><h3>Application State Lifecycle</h3><pre><code>stateDiagram-v2
[*] --&gt; Uninitialized

```
state Uninitialized {
    [*] --&gt; RegisterServiceWorker
    RegisterServiceWorker --&gt; CheckCache
}

Uninitialized --&gt; Ready : Resources &amp; Data Loaded

state Ready {
    [*] --&gt; Standby
    Standby --&gt; LocationSelected : Select ASZ Branch
    LocationSelected --&gt; ItemSelected : Select Product Item
    ItemSelected --&gt; GridCalculated : Compute Geometry
    GridCalculated --&gt; LivePreview : Render CSS Grid
}

Ready --&gt; ModalEditing : Click Sheet Preview

state ModalEditing {
    [*] --&gt; ModalOpen
    ModalOpen --&gt; ToggleCell : Click Grid Cell
    ToggleCell --&gt; RecalculateOffset : Update Start/Count
    RecalculateOffset --&gt; ModalOpen : Redraw Sheet
    ModalOpen --&gt; ModalClosed : Close Modal
}

ModalEditing --&gt; Ready : Return to Main UI
Ready --&gt; Printing : Click "Print Now"
Printing --&gt; Ready : Close Print View
```

|
🌟 Key Features

1. Dynamic HERMA Sheet Engine
   Interactive click-to-toggle sheet positioning on standard A4 grids

Real-time preview with automatic recalculation

Support for rectangular and round label templates

2. Serverless & Offline First
   Uses Cloudflare Workers for API endpoints

Falls back to cached browser state (localStorage)

Service Worker provides offline capability with network-first strategy

3. Bilingual Support (i18n)
   Native runtime switching between German (de) and English (en)

Persistent language preference stored in localStorage

4. Cross-Device Responsive UI
   Mobile-optimized layout switching for templates and location selectors

Adaptive breakpoints at 768px and 520px

Touch-optimized interactive elements

5. PWA Capable
   Offline support with service worker

Manifest-driven install prompts on compatible browsers

Standalone display configuration for app-like experience

6. Database Management
   In-browser CRUD operations for product database

JSON export functionality

Auto-sync between localStorage and UI

🔧 Technical Specifications
Storage & Persistence Schema

| Storage Key | Type | Description |
| --- | --- | --- | --- |
| lavu_lang | string | Selected i18n locale (de | en) |
| lavu_location | string | Currently selected Site Code ID (e.g. "106") |  |
| lavu_locations_url | string | Remote Worker endpoint for locations |  |
| lavu_locations_cache | string (JSON) | Cached locations list payload |  |
| lavu_studio_defaults_v8 | string (JSON) | Last known SKU format, count, and position offset |  |
| lavu_studio_sortiment_v8 | string (JSON) | Locally edited database workspace |  |
| lavu_preview_zoom | string | Zoom level for modal preview |

Media Query Breakpoint Matrix
|
| > 768px | Full dual-pane preview desktop layout with interactive sheet modal |  |  |
| <= 768px | Hides side panel live preview (.ps-wrapper). Switches to single-column flow |  |  |
| <= 520px | Hides desktop header location badges (.hdr-r). Activates mobile location select control (.mobile-location-wrapper) |

Performance Metrics
console.time('renderGrid'); |  |
| r2('mdl', data); |  |  |  |
| console.timeEnd('renderGrid'); |  |  |  |

<br class="ProseMirror-trailingBreak"></code></pre><h2>🖨 Printing Instructions</h2><p>For optimal print results, follow these settings in your browser's print dialog:</p><ol><li><p><strong>Scale:</strong> Set to <strong>100% / Actual Size</strong></p></li><li><p><strong>Margins:</strong> Set to <strong>None</strong> or <strong>0mm</strong></p></li><li><p><strong>Paper Size:</strong> Force selection to <strong>A4 Portrait</strong></p></li><li><p><strong>Background Graphics:</strong> Enable if you want to see the grid lines</p></li></ol><h3>Print Preview Code</h3><pre><code>document.getElementById('btn-print-now').addEventListener('click', function () {
if (window.innerWidth &lt;= 768) {
o1();
} else {
window.print();
}
});

<br class="ProseMirror-trailingBreak"></code></pre><h3>Print-Specific CSS</h3><pre><code>@media print {
@page {
size: A4 portrait;
margin: 0 !important;
}

# hpc .pc {

```
display: grid !important;
gap: 0 !important;
padding: 5mm 2mm !important;
width: 210mm !important;
height: 297mm !important;
box-shadow: none !important;
transform: none !important;
```

}

# hpc .lb {

```
display: flex !important;
flex-direction: column !important;
border: 0.5px solid #ccc !important;
padding: 2.5mm 3.5mm !important;
break-inside: avoid !important;
```

}
}

<br class="ProseMirror-trailingBreak"></code></pre><h2>🚀 Quick Start</h2><h3>Installation &amp; Setup</h3><ol><li><p><strong>Clone or download the repository</strong></p><pre><code>git clone https://github.com/LAVU-OOE/RePrint.git
cd RePrint

<br class="ProseMirror-trailingBreak"></code></pre></li><li><p><strong>Host via any static site server</strong></p><pre><code>python3 -m http.server 8080

# OR

npx http-server .

# OR

php -S localhost:8080

<br class="ProseMirror-trailingBreak"></code></pre></li><li><p><strong>Open in your browser</strong></p><pre><code>http://localhost:8080

<br class="ProseMirror-trailingBreak"></code></pre></li></ol><h3>First-Time Usage</h3><ol><li><p><strong>Select a Location</strong> – Choose your ASZ branch from the dynamically loaded dropdown</p></li><li><p><strong>Select an Item</strong> – Search by either <strong>Item No.</strong> (numerically grouped) or <strong>Description</strong> (alphabetically grouped)</p></li><li><p><strong>Adjust Print Layout</strong> – Click the preview image to open the interactive sheet</p></li><li><p><strong>Print</strong> – Click "Print Now" to generate your A4 sheet</p></li></ol><h2>📁 Project Structure</h2><pre><code>.
├── 📄 index.html # Main SPA UI container &amp; CSS layout engine
├── 📄 herma_templates.json # A4 Grid registry definitions
├── 📄 manifest.json # Web App Manifest for PWA installation
├── 📄 site.webmanifest # Secondary app manifest definition
├── 📄 sw.js # Service Worker for offline support
├── 📄 README.md # Application documentation
├── 📄 LICENSE # MIT License
├── 🖼️ favicon.svg # Scalable Vector Graphics icon
├── 🖼️ favicon-96x96.png # Static icon raster asset
├── 🖼️ logo.png # Application logo
├── 🖼️ apple-touch-icon.png # Apple iOS icon
├── 🖼️ web-app-manifest-192x192.png # PWA icon (192px)
├── 🖼️ web-app-manifest-512x512.png # PWA icon (512px)
└── 📄 tree.md # File structure documentation

<br class="ProseMirror-trailingBreak"></code></pre><h2>🗄 Database Management</h2><h3>In-Browser CRUD Operations</h3><p>The application includes a built-in database manager accessible via the <strong>"Options"</strong> button:</p><pre><code>function s3() {
const c1 = document.getElementById('c1').value.trim();
const c2 = document.getElementById('c2').value.trim();
const c3 = document.getElementById('c3').value.trim();

if (!c1 || !c3) {
alert(t.alertFillForm);
return;
}

if (a2.some(item =&gt; item.artNr === c1)) {
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

<br class="ProseMirror-trailingBreak"></code></pre><h3>Export Database as JSON</h3><pre><code>function e2() {
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

<br class="ProseMirror-trailingBreak"></code></pre><h3>Saving Defaults</h3><pre><code>function s7() {
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

<br class="ProseMirror-trailingBreak"></code></pre><h2>🤝 Contribution Guidelines</h2><h3>Development Setup</h3><ol><li><p><strong>Fork the repository</strong></p></li><li><p><strong>Create a feature branch</strong></p><pre><code>git checkout -b feature/your-feature-name

<br class="ProseMirror-trailingBreak"></code></pre></li><li><p><strong>Make your changes</strong></p></li><li><p><strong>Test locally</strong> – Ensure the application runs without errors</p></li><li><p><strong>Commit with conventional commit messages</strong></p><pre><code>git commit -m "feat: Add support for new HERMA template SKU"
git commit -m "fix: Resolve mobile layout issues on Safari"
git commit -m "docs: Update README with new Cloudflare API endpoints"

<br class="ProseMirror-trailingBreak"></code></pre></li><li><p><strong>Push and create a pull request</strong></p></li></ol><h3>Testing Guidelines</h3><ul><li><p><strong>Cross-browser testing</strong>: Chrome, Firefox, Safari, Edge</p></li><li><p><strong>Mobile testing</strong>: iOS Safari, Android Chrome</p></li><li><p><strong>Offline testing</strong>: Disable network and verify cached functionality</p></li><li><p><strong>Print testing</strong>: Verify A4 output with different printer configurations</p></li></ul><h3>Code Standards</h3><ul><li><p><strong>ES6+</strong> JavaScript with <code>const</code> and <code>let</code></p></li><li><p><strong>CSS variables</strong> for theming</p></li><li><p><strong>Semantic HTML5</strong> elements</p></li><li><p><strong>Progressive enhancement</strong> principles</p></li></ul><h2>📄 License</h2><p>This project is open source and is licensed under the <strong>MIT License</strong>.</p><pre><code>MIT License

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

<br class="ProseMirror-trailingBreak"></code></pre><p><em>Independent open-source project</em></p></div>


