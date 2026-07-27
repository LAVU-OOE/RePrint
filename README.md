<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>GitHub Markdown Style</title>
    <style>
        /* ────────────────────────────────────────────────
           GitHub Markdown CSS – Mirror
           ──────────────────────────────────────────────── */

        /* ── Reset & Base ── */
        *,
        *::before,
        *::after {
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
                "Helvetica Neue", Arial, "Noto Sans", sans-serif, "Apple Color Emoji",
                "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
            font-size: 16px;
            line-height: 1.6;
            color: #24292f;
            background-color: #ffffff;
            margin: 0;
            padding: 2rem 1rem;
            display: flex;
            justify-content: center;
        }

        .markdown-body {
            max-width: 880px;
            width: 100%;
            padding: 0 1rem;
        }

        /* ── Headings ── */
        .markdown-body h1,
        .markdown-body h2,
        .markdown-body h3,
        .markdown-body h4,
        .markdown-body h5,
        .markdown-body h6 {
            margin-top: 24px;
            margin-bottom: 16px;
            font-weight: 600;
            line-height: 1.25;
            letter-spacing: 0;
            scroll-margin-top: 1rem;
        }

        .markdown-body h1 {
            font-size: 2em;
            padding-bottom: 0.3em;
            border-bottom: 1px solid #d0d7de;
        }

        .markdown-body h2 {
            font-size: 1.5em;
            padding-bottom: 0.3em;
            border-bottom: 1px solid #d0d7de;
        }

        .markdown-body h3 {
            font-size: 1.25em;
        }

        .markdown-body h4 {
            font-size: 1em;
        }

        .markdown-body h5 {
            font-size: 0.875em;
        }

        .markdown-body h6 {
            font-size: 0.85em;
            color: #57606a;
        }

        /* ── Paragraphs ── */
        .markdown-body p {
            margin-top: 0;
            margin-bottom: 16px;
        }

        /* ── Links ── */
        .markdown-body a {
            color: #0969da;
            text-decoration: none;
        }

        .markdown-body a:hover {
            text-decoration: underline;
        }

        /* ── Strong / Bold ── */
        .markdown-body strong {
            font-weight: 600;
        }

        /* ── Emphasis / Italic ── */
        .markdown-body em {
            font-style: italic;
        }

        /* ── Inline Code ── */
        .markdown-body code:not(pre code) {
            padding: 0.2em 0.4em;
            margin: 0;
            font-size: 85%;
            font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, Courier,
                monospace;
            background-color: rgba(175, 184, 193, 0.2);
            border-radius: 6px;
            color: #1f2328;
        }

        /* ── Code Blocks (fenced) ── */
        .markdown-body pre {
            background-color: #f6f8fa;
            border-radius: 6px;
            padding: 16px;
            overflow: auto;
            font-size: 85%;
            line-height: 1.45;
            margin-top: 0;
            margin-bottom: 16px;
            word-wrap: normal;
        }

        .markdown-body pre code {
            background-color: transparent;
            padding: 0;
            margin: 0;
            font-size: 100%;
            font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, Courier,
                monospace;
            color: #1f2328;
            word-break: normal;
            white-space: pre;
        }

        /* ── Blockquotes ── */
        .markdown-body blockquote {
            margin: 0 0 16px 0;
            padding: 0 1em;
            color: #57606a;
            border-left: 0.25em solid #d0d7de;
        }

        .markdown-body blockquote > :first-child {
            margin-top: 0;
        }

        .markdown-body blockquote > :last-child {
            margin-bottom: 0;
        }

        /* ── Lists (unordered & ordered) ── */
        .markdown-body ul,
        .markdown-body ol {
            margin-top: 0;
            margin-bottom: 16px;
            padding-left: 2em;
        }

        .markdown-body ul {
            list-style-type: disc;
        }

        .markdown-body ul ul {
            list-style-type: circle;
        }

        .markdown-body ul ul ul {
            list-style-type: square;
        }

        .markdown-body ol {
            list-style-type: decimal;
        }

        .markdown-body ol ol {
            list-style-type: lower-alpha;
        }

        .markdown-body ol ol ol {
            list-style-type: lower-roman;
        }

        .markdown-body li {
            margin-top: 0.25em;
        }

        .markdown-body li > p {
            margin-top: 0;
            margin-bottom: 0;
        }

        .markdown-body li + li {
            margin-top: 0.25em;
        }

        /* ── Task Lists (if used) ── */
        .markdown-body .task-list-item {
            list-style-type: none;
        }

        .markdown-body .task-list-item input[type="checkbox"] {
            margin-right: 0.4em;
            margin-top: 0.1em;
        }

        /* ── Horizontal Rules ── */
        .markdown-body hr {
            height: 0.25em;
            padding: 0;
            margin: 24px 0;
            background-color: #d0d7de;
            border: 0;
            opacity: 1;
        }

        /* ── Tables ── */
        .markdown-body table {
            display: block;
            width: 100%;
            overflow: auto;
            border-spacing: 0;
            border-collapse: collapse;
            margin-top: 0;
            margin-bottom: 16px;
        }

        .markdown-body table th {
            font-weight: 600;
            padding: 6px 13px;
            border: 1px solid #d0d7de;
            background-color: #f6f8fa;
        }

        .markdown-body table td {
            padding: 6px 13px;
            border: 1px solid #d0d7de;
        }

        .markdown-body table tr {
            background-color: #ffffff;
            border-top: 1px solid #d0d7de;
        }

        .markdown-body table tr:nth-child(2n) {
            background-color: #f6f8fa;
        }

        /* ── Images ── */
        .markdown-body img {
            max-width: 100%;
            height: auto;
            border-style: none;
            background-color: #ffffff;
        }

        /* ── Details / Summary ── */
        .markdown-body details {
            display: block;
            margin-top: 0;
            margin-bottom: 16px;
        }

        .markdown-body summary {
            display: list-item;
            cursor: pointer;
            font-weight: 600;
        }

        /* ── Footnotes ── */
        .markdown-body .footnote-ref {
            color: #0969da;
            text-decoration: none;
        }

        .markdown-body .footnote-ref:hover {
            text-decoration: underline;
        }

        .markdown-body .footnotes {
            border-top: 1px solid #d0d7de;
            padding-top: 16px;
            margin-top: 24px;
        }

        /* ── Helper: keep code blocks from overflowing ── */
        .markdown-body pre code {
            white-space: pre-wrap;
            word-wrap: break-word;
        }

        /* ── Responsive tweaks ── */
        @media (max-width: 768px) {
            body {
                padding: 1rem 0.5rem;
            }

            .markdown-body {
                padding: 0 0.5rem;
            }

            .markdown-body table {
                display: block;
                overflow-x: auto;
                white-space: nowrap;
            }
        }

        @media (prefers-color-scheme: dark) {
            body {
                background-color: #0d1117;
                color: #c9d1d9;
            }

            .markdown-body h1,
            .markdown-body h2 {
                border-bottom-color: #21262d;
            }

            .markdown-body a {
                color: #58a6ff;
            }

            .markdown-body code:not(pre code) {
                background-color: rgba(110, 118, 129, 0.4);
                color: #c9d1d9;
            }

            .markdown-body pre {
                background-color: #161b22;
            }

            .markdown-body pre code {
                color: #c9d1d9;
            }

            .markdown-body blockquote {
                color: #8b949e;
                border-left-color: #21262d;
            }

            .markdown-body hr {
                background-color: #21262d;
            }

            .markdown-body table th {
                border-color: #21262d;
                background-color: #161b22;
            }

            .markdown-body table td {
                border-color: #21262d;
            }

            .markdown-body table tr {
                background-color: #0d1117;
                border-top-color: #21262d;
            }

            .markdown-body table tr:nth-child(2n) {
                background-color: #161b22;
            }

            .markdown-body img {
                background-color: #0d1117;
            }

            .markdown-body .footnotes {
                border-top-color: #21262d;
            }

            .markdown-body .footnote-ref {
                color: #58a6ff;
            }
        }
    </style>
</head>
<body>
    <div class="markdown-body">

        <!-- ─── YOUR HTML CONTENT GOES HERE ─── -->
        <h2 id="🚀-introduction">🚀 Introduction</h2>
        <p><strong>RE:PRINT Studio v9</strong> is a lightweight, client-side Progressive Web Application (PWA) designed for ASZ branch locations in Upper Austria. It provides dynamic label formatting, live print preview calculations, and customizable template sheet rendering for standard HERMA A4 templates.</p>
        <p>The application operates entirely in the browser, leveraging modern web technologies to deliver a seamless experience across desktop and mobile devices, with robust offline capabilities.</p>

        <h2 id="⚠️-disclaimer--rechtlicher-hinweis">⚠️ Disclaimer / Rechtlicher Hinweis</h2>
        <blockquote>
            <p><strong>Important Notice / Disclaimer:</strong></p>
            <p><strong>This software is an independent community project and is not officially affiliated with LAVU OÖ (Upper Austrian State Waste Management Company) or the district waste management associations (BAV OÖ).</strong></p>
            <p><strong>This is not an official application or software of LAVU OÖ or BAV OÖ. All trademarks, logos, and designations belong to their respective owners.</strong></p>
            <p><strong>Notice:</strong></p>
            <p><strong>This application is an independent open-source project and is not officially affiliated with, endorsed by, or sponsored by LAVU OÖ or BAV OÖ.</strong></p>
        </blockquote>
        <hr>

        <h2 id="🔧-technical-details--development">🔧 Technical Details &amp; Development</h2>
        <ul>
            <li><strong>Language:</strong> Pure HTML, CSS, and JavaScript (ES6+).</li>
            <li><strong>Storage:</strong> Uses <code>localStorage</code> for user-specific settings, the assortment cache, and the location cache.</li>
            <li><strong>Network:</strong> Uses the <code>fetch</code> API with a &quot;no-store&quot; cache strategy for JSON data to always prioritize the most up-to-date data.</li>
            <li><strong>Service Worker:</strong> The <code>sw.js</code> implements a <strong>network-first strategy</strong> for JSON databases and a <strong>cache-first strategy</strong> for static assets, enabling robust offline use.</li>
            <li><strong>Folder Structure:</strong> The main application is located in the <code>/</code> folder, and all assets (icons, images) are in the <code>/assets/</code> folder. An <code>index.html</code> file in the root directory redirects to the app.</li>
        </ul>
        <hr>

        <h2 id="📦-external-data-sources-json--externe-datenquellen-json">📦 External Data Sources (JSON) / Externe Datenquellen (JSON)</h2>
        <p>[en] The app retrieves its dynamic data from two central JSON files maintained in this repository:
        [de] Die App bezieht ihre dynamischen Daten aus zwei zentralen JSON-Dateien, die in diesem Repository gepflegt werden:</p>
        <ol>
            <li>[en] <code>sortiment.json</code> – Contains the product assortment with product number, description, and optional packaging suffix.
            [de] <code>sortiment.json</code> – Enthält das Artikel-Sortiment mit Artikelnnummer, Bezeichnung und optionalem Gebinde-Suffix.</li>
            <li>[en] <code>locations.json</code> – Contains the list of recycling center locations with name, location code, postal code, and region.
            [de] <code>locations.json</code> – Enthält die Liste der ASZ-Standorte mit Name, Standortcode, Postleitzahl und Region.</li>
        </ol>
        <p>[en] These files are loaded via the GitHub raw URLs and can be updated independently of the app itself.
        [de] Diese Dateien werden über die GitHub-Raw-URLs geladen und können unabhängig von der App selbst aktualisiert werden.</p>
        <hr>

        <h2 id="🚀-getting-started--usage--erste-schritte--nutzung">🚀 Getting Started &amp; Usage / Erste Schritte &amp; Nutzung</h2>
        <p>[en] 1. Open the App: Access the page via the provided link or install it as a PWA.
        [de] 1. App öffnen: Rufe die Seite über den bereitgestellten Link auf oder installiere sie als PWA.</p>
        <p>[en] 2. Select a Location: Select the desired recycling center location from the dynamically loaded list in the header.
        [de] 2. Standort wählen: Wähle im Header den gewünschten ASZ-Standort aus der dynamisch geladenen Liste.</p>
        <p>[en] 3. Select Item: Search for the desired item either by <strong>Item No.</strong> (numerically grouped) or <strong>Description</strong> (alphabetically grouped).
        [de] 3. Artikel auswählen: Suche den gewünschten Artikel entweder über die <strong>Art.Nr.</strong> (numerisch gruppiert) oder die <strong>Bezeichnung</strong> (alphabetisch gruppiert).</p>
        <p>[en] 4. Adjust Print Layout (Optional): Click on the preview image to open the interactive A4 print sheet. Click on any position on the sheet to add or remove labels.
        [de] 4. Drucklayout anpassen (optional): Klicke auf das Vorschaubild, um den interaktiven A4-Druckbogen zu öffnen. Klicke auf beliebige Positionen im Bogen, um Etiketten hinzuzufügen oder zu entfernen.</p>
        <p>[en] 5. Print: Click the main <strong>&quot;Print Now&quot;</strong> button to print the A4 sheet with your labels.
        [de] 5. Drucken: Klicke auf den Haupt-Button <strong>&quot;Jetzt Drucken&quot;</strong>, um den A4-Bogen mit deinen Etiketten zu drucken.</p>
        <hr>

        <h2 id="⚙️-database-customization-crud--anpassung-der-datenbank-crud">⚙️ Database Customization (CRUD) / Anpassung der Datenbank (CRUD)</h2>
        <p>[en] You can access the integrated database manager via the <strong>&quot;Options&quot;</strong> button:
        [de] Über den <strong>&quot;Optionen&quot;</strong>-Button kannst du auf den integrierten Datenbank-Manager zugreifen:</p>
        <p>[en] * Select Product Range: Displays the current product list.
        [de] * Sortiment wählen: Zeigt die aktuelle Artikelliste an.</p>
        <p>[en] * Manage Database: Here you can add new items, edit or delete existing items, and export the entire database as a JSON file.
        [de] * Datenbank verwalten: Hier kannst du neue Artikel hinzufügen, bestehende Artikel bearbeiten oder löschen, und die gesamte Datenbank als JSON-Datei exportieren.</p>
        <p>[en] * Save Defaults: Saves the current settings (location, format, quantity, starting position) as the browser default.
        [de] * Standard sichern: Speichert die aktuellen Einstellungen (Standort, Format, Anzahl, Startposition) als Standard im Browser.</p>
        <hr>

        <h2 id="🤝-contribute--beitrag-leisten">🤝 Contribute / Beitrag leisten</h2>
        <p>[en] Contributions are welcome! Please note the following points:
        [de] Beiträge sind willkommen! Bitte beachte die folgenden Punkte:</p>
        <p>[en] 1. Fork the repository.
        [de] 1. Forke das Repository.</p>
        <p>[en] 2. Create a new branch for your feature (<code>git checkout -b feature/new-feature</code>).
        [de] 2. Erstelle einen neuen Branch für dein Feature (<code>git checkout -b feature/neues-feature</code>).</p>
        <p>[en] 3. Commit your changes (<code>git commit -m 'feat: New feature added'</code>).
        [de] 3. Committe deine Änderungen (<code>git commit -m 'feat: Neues Feature hinzugefügt'</code>).</p>
        <p>[en] 4. Push the branch (<code>git push origin feature/new-feature</code>).
        [de] 4. Pushe den Branch (<code>git push origin feature/neues-feature</code>).</p>
        <p>[en] 5. Create a pull request.
        [de] 5. Erstelle einen Pull Request.</p>
        <p>[en] Important notes for changes to the JSON databases: Ensure the JSON structure is valid. Test the changes locally before merging them into the main branch.
        [de] Wichtige Hinweise für Änderungen an den JSON-Datenbanken: Stelle sicher, dass die JSON-Struktur gültig ist. Teste die Änderungen lokal, bevor du sie in den Hauptbranch mergst.</p>
        <hr>

        <h2 id="📄-license--lizenz">📄 License / Lizenz</h2>
        <p>[en] This project is open source and is licensed under the MIT License.
        [de] Dieses Projekt ist Open Source und steht unter der MIT-Lizenz.</p>

    </div>
</body>
</html>