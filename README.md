# RE:PRINT Studio v9

**RE:PRINT Studio v9** is a lightweight, client-side Progressive Web Application (PWA) designed for ASZ branch locations in Upper Austria (LAVU ÖO). It provides dynamic label formatting, live print preview calculations, and customizable template sheet rendering for standard HERMA A4 templates.

---

## 🌟 Key Features

* **Dynamic HERMA Sheet Engine:** Supports interactive click-to-toggle sheet positioning on standard A4 grids.
* **Serverless & Offline First:** Uses Worker APIs for location and assortment registry syncing, falling back to cached local browser state (`localStorage`).
* **Bilingual Support (i18n):** Native runtime switching between German (`de`) and English (`en`).
* **Cross-Device Responsive UI:** Mobile-optimized layout switching for templates and location select inputs on narrow viewports.
* **PWA Capable:** Offline support, manifest-driven install prompts, and standalone display configurations.

---

## 🚀 Quick Start

1. Clone or download the repository.
2. Host via any static site server (GitHub Pages, Cloudflare Pages, Nginx, or Caddy).
3. Open `index.html` in any modern Browser (Chrome, Edge, Safari, Firefox).

```bash
# Example local testing with Python
python3 -m http.server 8080
````

## 🛠 Project Structure

Plaintext

```
├── index.html            # Main SPA UI container & CSS layout engine
├── herma_templates.json  # A4 Grid registry definitions
├── site.webmanifest     # Web App Manifest for PWA installation
├── manifest.json         # Secondary app manifest definition
├── favicon.svg           # Scalable Vector Graphics icon
└── favicon-96x96.png     # Static icon raster asset
```

## 🖨 Printing Instructions

-   **Browser Scale:** Ensure the print scale setting in the print dialog is set to **100% / Actual Size**.
-   **Margins:** Set page margins to **None** or **0mm**.
-   **Paper Size:** Force paper selection to **A4 Portrait**.

````

---

# System Architecture & Technical Specifications

## 1. Grid Rendering Mechanics

The label renderer computes dynamic layout geometry based on template parameters declared in `herma_templates.json`.

$$W_{\text{total}} = (C \cdot W_{\text{mm}}) + ((C - 1) \cdot G_x)$$

$$H_{\text{total}} = (R \cdot H_{\text{mm}}) + ((R - 1) \cdot G_y)$$

Where:
* $C$ = Number of Columns (`cols`)
* $R$ = Number of Rows (`rows`)
* $W_{\text{mm}}$ = Label Width in Millimeters
* $H_{\text{mm}}$ = Label Height in Millimeters
* $G_x, G_y$ = Horizontal and Vertical Gaps in Millimeters

### Viewport Scaling Vector
To prevent CSS layout breakage inside preview cards, scale vectors are calculated dynamic inline properties:

```js
const scaleX = t.width_mm / baseWidth;
const scaleY = t.height_mm / baseHeight;
const scale = Math.min(scaleX, scaleY, 1);
container.style.setProperty('--label-scale', scale);
````

## 2\. Dynamic Data Fetching Workflow

Code-Snippet

```
sequenceDiagram
    autonumber
    participant Client as Browser (PWA)
    participant LS as LocalStorage
    participant Worker as Cloudflare Workers API

    Client->>LS: Read 'lavu_locations_cache'
    alt Cache Present
        LS-->>Client: Return cached Location JSON
        Client->>Client: Render Location Selectors
    end

    Client->>Worker: Fetch GET /locations-api
    alt HTTP 200 OK
        Worker-->>Client: Return Fresh Locations JSON Array
        Client->>LS: Update 'lavu_locations_cache'
        Client->>Client: Re-populate Location Selectors
    else Network Failure
        Worker-->>Client: Error / Timeout
        Client->>Client: Fallback to hardcoded ASZ emergency array
    end
```

## 3\. Storage & Persistence Schema

| Storage Key | Type | Description |
| --- | --- | --- |
| `lavu_lang` | `string` | Selected i18n locale string (`de` \\| `en`). |
| `lavu_location` | `string` | Currently selected Site Code ID (e.g. `"106"`). |
| `lavu_locations_url` | `string` | Remote HTTP Worker Endpoint for location lookup. |
| `lavu_locations_cache` | `string` (JSON) | Cached locations list payload. |
| `lavu_studio_defaults_v8` | `string` (JSON) | Last known selected SKU format, count, and position offset. |
| `lavu_studio_sortiment_v8` | `string` (JSON) | Locally edited database workspace array. |

## 4\. Media Query Breakpoint Matrix

| Viewport Width | Visual Adjustments |
| --- | --- |
| **\\> 768px** | Full dual-pane preview desktop layout with interactive sheet modal. |
| **<= 768px** | Hides side panel live preview (`.ps-wrapper`). Switches to single-column flow. |
| **<= 520px** | Hides desktop header location badges (`.hdr-r`). Activates mobile location select control (`.mobile-location-wrapper`). |