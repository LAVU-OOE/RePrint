<!DOCTYPE html>
<html lang="de" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RE:PRINT Studio v9 | Interaktive Spezifikation</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=JetBrains+Mono:wght@400;500&display=swap');
        
        :root {
            --bg-main: #fdfcfb;
            --bg-card: #ffffff;
            --text-main: #2d2a26;
            --accent-warm: #d4a373;
            --accent-cool: #a5a58d;
            --border-soft: #e9e5e2;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-main);
            color: var(--text-main);
        }

        .mono { font-family: 'JetBrains Mono', monospace; }

        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
            border-radius: 12px;
        }

        .glass-panel {
            background: rgba(255, 255, 255, 0.8);
            border: 1px solid var(--border-soft);
            box-shadow: 0 4px 20px -2px rgba(45, 42, 38, 0.05);
            transition: all 0.3s ease;
        }

        .geometry-preview {
            aspect-ratio: 210/297;
            background-color: white;
            box-shadow: 0 0 15px rgba(0,0,0,0.1);
            position: relative;
            margin: auto;
        }

        .label-cell {
            border: 1px dashed #d1d5db;
            background: rgba(212, 163, 115, 0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 8px;
            color: #d4a373;
        }

        .nav-link {
            position: relative;
            transition: color 0.3s;
        }

        .nav-link::after {
            content: '';
            position: absolute;
            bottom: -4px;
            left: 0;
            width: 0;
            height: 2px;
            background-color: var(--accent-warm);
            transition: width 0.3s;
        }

        .nav-link:hover::after { width: 100%; }

        .bg-sandal { background-color: #f7f3f0; }
        .text-sandal-dark { color: #8b735b; }
    </style>
</head>
<body class="antialiased">

    <nav class="fixed top-0 w-full z-50 bg-white/80 backdrop-blur-md border-b border-stone-200">
        <div class="max-w-7xl mx-auto px-6 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="w-8 h-8 bg-stone-800 rounded flex items-center justify-center text-white font-bold">R</div>
                <span class="font-bold text-lg tracking-tight">RE:PRINT <span class="text-stone-400">v9</span></span>
            </div>
            <div class="hidden md:flex space-x-8 text-sm font-medium text-stone-600">
                <a href="#overview" class="nav-link">Übersicht</a>
                <a href="#architecture" class="nav-link">Architektur</a>
                <a href="#engine" class="nav-link">Geometrie-Labor</a>
                <a href="#performance" class="nav-link">Performance</a>
            </div>
        </div>
    </nav>

    <main class="pt-24 pb-12 px-6 max-w-7xl mx-auto">

        <!-- Hero Section -->
        <section id="overview" class="mb-20">
            <div class="max-w-3xl mb-12">
                <span class="bg-sandal text-sandal-dark px-3 py-1 rounded-full text-xs font-bold uppercase tracking-widest mb-4 inline-block">Technische Dokumentation</span>
                <h1 class="text-4xl md:text-5xl font-bold text-stone-900 mb-6 leading-tight">
                    Die Zukunft des <span class="text-stone-400">clientseitigen</span> Etikettendrucks.
                </h1>
                <p class="text-lg text-stone-600 leading-relaxed">
                    RE:PRINT Studio v9 ist eine ressourcenschonende PWA, entwickelt für die ASZ-Standorte in Oberösterreich. 
                    Sie kombiniert Serverless-Präzision mit Offline-Fähigkeit, um Druckprozesse unabhängig von Netzwerkschwankungen zu machen.
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
                <div class="glass-panel p-6 rounded-2xl">
                    <div class="text-stone-400 mb-2">⚡ Latenz</div>
                    <div class="text-2xl font-bold">0ms</div>
                    <p class="text-xs text-stone-500 mt-2">Clientseitiges Rendering ohne API-Wartezeit.</p>
                </div>
                <div class="glass-panel p-6 rounded-2xl border-l-4 border-l-amber-200">
                    <div class="text-stone-400 mb-2">🌐 Status</div>
                    <div class="text-2xl font-bold">Offline First</div>
                    <p class="text-xs text-stone-500 mt-2">Dank Service Worker voll einsatzbereit ohne Internet.</p>
                </div>
                <div class="glass-panel p-6 rounded-2xl">
                    <div class="text-stone-400 mb-2">📐 Präzision</div>
                    <div class="text-2xl font-bold">±0.2mm</div>
                    <p class="text-xs text-stone-500 mt-2">Millimetergenaue HERMA-Rasterberechnung.</p>
                </div>
                <div class="glass-panel p-6 rounded-2xl">
                    <div class="text-stone-400 mb-2">🛠 Tech Stack</div>
                    <div class="text-2xl font-bold">Vanilla JS</div>
                    <p class="text-xs text-stone-500 mt-2">Keine schweren Frameworks, maximale Speed.</p>
                </div>
            </div>
        </section>

        <!-- Architektur & Datenfluss -->
        <section id="architecture" class="mb-24 py-12 border-t border-stone-100">
            <div class="mb-12">
                <h2 class="text-3xl font-bold mb-4">Serverless Architektur & Datenfluss</h2>
                <p class="text-stone-600">Erkunden Sie, wie Daten von Cloudflare Edge-Netzwerken über den Service Worker bis in das Browser-Interface fließen.</p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                <div class="space-y-6">
                    <div class="flex gap-4 p-4 rounded-xl hover:bg-stone-50 transition cursor-pointer group border border-transparent hover:border-stone-200">
                        <div class="w-12 h-12 bg-stone-100 rounded-lg flex items-center justify-center text-xl shrink-0 group-hover:bg-amber-100 transition">📦</div>
                        <div>
                            <h4 class="font-bold text-lg mb-1">Cloudflare Workers</h4>
                            <p class="text-sm text-stone-500">Zwei Edge-APIs liefern Sortiment- und Standortdaten als hochperformantes JSON direkt aus dem KV-Speicher.</p>
                        </div>
                    </div>
                    <div class="flex gap-4 p-4 rounded-xl hover:bg-stone-50 transition cursor-pointer group border border-transparent hover:border-stone-200">
                        <div class="w-12 h-12 bg-stone-100 rounded-lg flex items-center justify-center text-xl shrink-0 group-hover:bg-amber-100 transition">⚙️</div>
                        <div>
                            <h4 class="font-bold text-lg mb-1">Service Worker Cache</h4>
                            <p class="text-sm text-stone-500">Implementiert die "Network-First"-Strategie für API-Daten und "Cache-First" für das PWA-App-Shell-Modell.</p>
                        </div>
                    </div>
                    <div class="flex gap-4 p-4 rounded-xl hover:bg-stone-50 transition cursor-pointer group border border-transparent hover:border-stone-200">
                        <div class="w-12 h-12 bg-stone-100 rounded-lg flex items-center justify-center text-xl shrink-0 group-hover:bg-amber-100 transition">💾</div>
                        <div>
                            <h4 class="font-bold text-lg mb-1">localStorage Persistenz</h4>
                            <p class="text-sm text-stone-500">Speichert Standorte, Spracheinstellungen und Datenbank-Overrides direkt beim Benutzer im Browser.</p>
                        </div>
                    </div>
                </div>

                <div class="glass-panel p-8 rounded-3xl">
                    <div class="chart-container">
                        <canvas id="radarChart"></canvas>
                    </div>
                    <div class="mt-6 text-center text-xs text-stone-400 uppercase tracking-widest font-semibold">System-Kapazitäten Score</div>
                </div>
            </div>
        </section>

        <!-- Geometrie Labor -->
        <section id="engine" class="mb-24 py-12 bg-stone-50 rounded-[3rem] px-8 border border-stone-200">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-16">
                <div>
                    <h2 class="text-3xl font-bold mb-6">Das Geometrie-Labor</h2>
                    <p class="text-stone-600 mb-8">
                        Die Engine wandelt HERMA-Parameter in Echtzeit in CSS-Layouts um. Testen Sie die Formeln aus Sektion 5.1 live: 
                        Ändern Sie Spalten und Maße, um zu sehen, wie sich die Ränder ($M_{left}$, $M_{top}$) automatisch kalibrieren.
                    </p>
                    
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-stone-200 space-y-4">
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs font-bold text-stone-400 uppercase mb-1">Spalten (C)</label>
                                <input type="number" id="input-cols" value="3" class="w-full bg-stone-50 border border-stone-200 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-amber-200 transition">
                            </div>
                            <div>
                                <label class="block text-xs font-bold text-stone-400 uppercase mb-1">Zeilen (R)</label>
                                <input type="number" id="input-rows" value="7" class="w-full bg-stone-50 border border-stone-200 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-amber-200 transition">
                            </div>
                            <div>
                                <label class="block text-xs font-bold text-stone-400 uppercase mb-1">Breite mm (W)</label>
                                <input type="number" id="input-w" value="70" class="w-full bg-stone-50 border border-stone-200 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-amber-200 transition">
                            </div>
                            <div>
                                <label class="block text-xs font-bold text-stone-400 uppercase mb-1">Höhe mm (H)</label>
                                <input type="number" id="input-h" value="41" class="w-full bg-stone-50 border border-stone-200 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-amber-200 transition">
                            </div>
                        </div>
                        <div class="pt-4 border-t border-stone-100">
                            <div class="flex justify-between text-sm mb-2">
                                <span class="text-stone-500">Berechneter Rand links ($M_{left}$):</span>
                                <span id="out-mleft" class="font-mono font-bold text-amber-600">0 mm</span>
                            </div>
                            <div class="flex justify-between text-sm">
                                <span class="text-stone-500">Berechneter Rand oben ($M_{top}$):</span>
                                <span id="out-mtop" class="font-mono font-bold text-amber-600">0 mm</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="flex flex-col items-center">
                    <div class="text-xs font-bold text-stone-400 uppercase mb-4 tracking-widest">A4 Bogen Vorschau (Interaktiv)</div>
                    <div id="grid-simulator" class="geometry-preview w-64 md:w-80"></div>
                </div>
            </div>
        </section>

        <!-- Performance & Distribution -->
        <section id="performance" class="mb-24">
            <div class="mb-12 text-center">
                <h2 class="text-3xl font-bold mb-4">Performance & Vorlagen-Analyse</h2>
                <p class="text-stone-600">Statistische Auswertung der unterstützten Etikettenformate und Systemeffizienz.</p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <div class="glass-panel p-8 rounded-3xl">
                    <h4 class="font-bold mb-6 flex items-center gap-2">
                        <span class="w-2 h-6 bg-stone-800 rounded-full"></span>
                        Etiketten-Dichte nach SKUs
                    </h4>
                    <div class="chart-container">
                        <canvas id="barChart"></canvas>
                    </div>
                </div>
                <div class="glass-panel p-8 rounded-3xl">
                    <h4 class="font-bold mb-6 flex items-center gap-2">
                        <span class="w-2 h-6 bg-amber-400 rounded-full"></span>
                        Geometrie-Verteilung (mm)
                    </h4>
                    <div id="plotlyScatter" class="w-full h-[350px]"></div>
                </div>
            </div>
        </section>

        <!-- Operational Checklist -->
        <section class="mb-20">
            <div class="bg-stone-900 text-white rounded-[2rem] p-12 overflow-hidden relative">
                <div class="relative z-10 grid grid-cols-1 md:grid-cols-2 gap-12">
                    <div>
                        <h2 class="text-3xl font-bold mb-6">Druckanleitung & Konfiguration</h2>
                        <p class="text-stone-400 mb-8">Wichtige Parameter für den fehlerfreien Druck auf HERMA-Bögen. Stellen Sie sicher, dass Ihr Browser die Skalierung nicht manipuliert.</p>
                        <div class="space-y-4">
                            <div class="flex items-center gap-4 bg-stone-800/50 p-4 rounded-xl border border-stone-700">
                                <div class="w-8 h-8 flex items-center justify-center rounded-full bg-amber-400 text-black font-bold">1</div>
                                <span>Skalierung: <strong>Tatsächliche Größe / 100%</strong></span>
                            </div>
                            <div class="flex items-center gap-4 bg-stone-800/50 p-4 rounded-xl border border-stone-700">
                                <div class="w-8 h-8 flex items-center justify-center rounded-full bg-amber-400 text-black font-bold">2</div>
                                <span>Ränder: <strong>Keine (0mm)</strong></span>
                            </div>
                            <div class="flex items-center gap-4 bg-stone-800/50 p-4 rounded-xl border border-stone-700">
                                <div class="w-8 h-8 flex items-center justify-center rounded-full bg-amber-400 text-black font-bold">3</div>
                                <span>Format: <strong>DIN A4 (Hochformat)</strong></span>
                            </div>
                        </div>
                    </div>
                    <div class="flex flex-col justify-center">
                        <div class="p-6 bg-stone-800 rounded-2xl border border-stone-700">
                            <h4 class="font-mono text-amber-200 mb-4 tracking-tighter uppercase text-sm">@media print snippet</h4>
                            <pre class="text-xs text-stone-300 mono overflow-x-auto">
@page {
  size: A4 portrait;
  margin: 0 !important;
}

.a4-print-sheet {
  width: 210mm;
  height: 297mm;
}
                            </pre>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-stone-50 border-t border-stone-200 py-12">
        <div class="max-w-7xl mx-auto px-6 text-center text-stone-500 text-sm">
            <p class="font-bold text-stone-800 mb-2">RE:PRINT Studio v9 | Technical Assessment</p>
            <p>&copy; 2026 LAVU OÖ Community Project. Dokumentiert für ASZ Oberösterreich.</p>
        </div>
    </footer>

    <script>
        // 1. Chart Global Configuration
        const chartColors = {
            primary: '#d4a373',
            secondary: '#a5a58d',
            tertiary: '#4b4b4b',
            bg: 'rgba(212, 163, 115, 0.2)'
        };

        // Hilfsfunktion für Tooltip-Label-Umbruch (16-Zeichen-Logik)
        function wrapText(str) {
            const words = str.split(' ');
            const lines = [];
            let currentLine = '';
            words.forEach(w => {
                if ((currentLine + w).length > 16) {
                    lines.push(currentLine.trim());
                    currentLine = w + ' ';
                } else {
                    currentLine += w + ' ';
                }
            });
            lines.push(currentLine.trim());
            return lines;
        }

        // 2. Radar Chart: System Kapazitäten
        const ctxRadar = document.getElementById('radarChart').getContext('2d');
        new Chart(ctxRadar, {
            type: 'radar',
            data: {
                labels: [
                    wrapText('Offline Stabilität'),
                    wrapText('Rendering Speed'),
                    wrapText('API Sicherheit'),
                    wrapText('i18n Support'),
                    wrapText('Daten-Integrität')
                ],
                datasets: [{
                    label: 'Score',
                    data: [100, 100, 95, 90, 95],
                    backgroundColor: chartColors.bg,
                    borderColor: chartColors.primary,
                    pointBackgroundColor: chartColors.primary,
                    borderWidth: 2
                }]
            },
            options: {
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: {
                    r: {
                        beginAtZero: true,
                        max: 100,
                        ticks: { display: false },
                        grid: { color: '#e9e5e2' },
                        pointLabels: { color: '#8b735b', font: { size: 10, weight: '600' } }
                    }
                }
            }
        });

        // 3. Bar Chart: SKU Effizienz
        const ctxBar = document.getElementById('barChart').getContext('2d');
        new Chart(ctxBar, {
            type: 'bar',
            data: {
                labels: ['SKU 4425', 'SKU 4473', 'SKU 4272', 'SKU 4453'],
                datasets: [{
                    label: 'Etiketten pro Bogen',
                    data: [64, 21, 10, 14],
                    backgroundColor: [chartColors.primary, chartColors.secondary, '#4b4b4b', '#e2e2e2'],
                    borderRadius: 6
                }]
            },
            options: {
                indexAxis: 'y',
                maintainAspectRatio: false,
                responsive: true,
                plugins: { legend: { display: false } },
                scales: {
                    x: { grid: { display: false }, ticks: { color: '#8b735b' } },
                    y: { grid: { display: false }, ticks: { color: '#8b735b' } }
                }
            }
        });

        // 4. Plotly: Geometrie Scatter
        const plotlyData = [{
            x: [70, 105, 70, 38, 52, 210, 48],
            y: [37, 148, 41, 21, 21, 297, 25],
            mode: 'markers+text',
            type: 'scatter',
            text: ['4473', '4272', '4453', '4425', '4410', 'A4 Full', '4412'],
            textposition: 'top center',
            marker: { size: 12, color: '#d4a373', opacity: 0.7 }
        }];
        const plotlyLayout = {
            paper_bgcolor: 'rgba(0,0,0,0)',
            plot_bgcolor: 'rgba(0,0,0,0)',
            xaxis: { title: 'Breite (mm)', gridcolor: '#f3f4f6' },
            yaxis: { title: 'Höhe (mm)', gridcolor: '#f3f4f6' },
            margin: { t: 10, b: 40, l: 40, r: 10 },
            font: { family: 'Inter', size: 10, color: '#8b735b' }
        };
        Plotly.newPlot('plotlyScatter', plotlyData, plotlyLayout, {responsive: true, displayModeBar: false});

        // 5. Interaktiver Simulator Logic
        const simContainer = document.getElementById('grid-simulator');
        const inputs = ['input-cols', 'input-rows', 'input-w', 'input-h'].map(id => document.getElementById(id));
        
        function updateSimulator() {
            const C = parseInt(inputs[0].value) || 1;
            const R = parseInt(inputs[1].value) || 1;
            const W = parseFloat(inputs[2].value) || 0;
            const H = parseFloat(inputs[3].value) || 0;

            const totalW = C * W;
            const totalH = R * H;
            
            const M_left = (210 - totalW) / 2;
            const M_top = (297 - totalH) / 2;

            document.getElementById('out-mleft').textContent = `${M_left.toFixed(1)} mm`;
            document.getElementById('out-mtop').textContent = `${M_top.toFixed(1)} mm`;

            // Render Preview
            simContainer.innerHTML = '';
            simContainer.style.display = 'grid';
            simContainer.style.paddingLeft = `${(M_left / 210) * 100}%`;
            simContainer.style.paddingTop = `${(M_top / 297) * 100}%`;
            simContainer.style.gridTemplateColumns = `repeat(${C}, 1fr)`;
            simContainer.style.gridTemplateRows = `repeat(${R}, 1fr)`;

            for(let i=0; i < (C * R); i++) {
                const cell = document.createElement('div');
                cell.className = 'label-cell';
                cell.textContent = `${i+1}`;
                simContainer.appendChild(cell);
            }
        }

        inputs.forEach(input => input.addEventListener('input', updateSimulator));
        window.addEventListener('load', updateSimulator);

    </script>
</body>
</html>