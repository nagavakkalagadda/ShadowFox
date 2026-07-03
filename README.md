# ShadowFox
# File for the Task Level (ADVANCE)
<!DOCTYPE html>
<html lang="en" class="h-full bg-slate-950 text-slate-100">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Transformer Exploration & Alignment Hub</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js for real-time trade-off graphs -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- FontAwesome for professional iconography -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Inter & JetBrains Mono -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .mono-font {
            font-family: 'JetBrains Mono', monospace;
        }
        /* Custom styled scrollbars */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0f172a;
        }
        ::-webkit-scrollbar-thumb {
            background: #334155;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569;
        }
    </style>
</head>
<body class="h-full flex flex-col overflow-hidden">

    <!-- Navigation Header -->
    <header class="bg-slate-900 border-b border-slate-800 px-6 py-4 flex items-center justify-between flex-shrink-0">
        <div class="flex items-center space-x-3">
            <div class="bg-indigo-600 text-white p-2.5 rounded-xl shadow-lg shadow-indigo-500/20 flex items-center justify-center">
                <i class="fa-solid fa-brain text-xl"></i>
            </div>
            <div>
                <h1 class="font-bold text-lg text-white leading-tight">Transformer Exploration Hub</h1>
                <p class="text-xs text-slate-400">Attention Topologies, Coreference & Bias Alignment Sandbox</p>
            </div>
        </div>
        
        <!-- Tab Navigation -->
        <nav class="flex items-center space-x-1 bg-slate-950/60 p-1.5 rounded-xl border border-slate-800">
            <button onclick="switchTab('playground')" id="tab-btn-playground" class="tab-btn px-4 py-2 text-xs font-semibold rounded-lg transition duration-200 bg-indigo-600 text-white shadow-md">
                <i class="fa-solid fa-compass mr-1.5"></i> Coreference Sandbox
            </button>
            <button onclick="switchTab('pruning')" id="tab-btn-pruning" class="tab-btn px-4 py-2 text-xs font-semibold text-slate-400 hover:text-white rounded-lg transition duration-200">
                <i class="fa-solid fa-scissors mr-1.5"></i> Attention Head Pruning Lab
            </button>
            <button onclick="switchTab('notebook')" id="tab-btn-notebook" class="tab-btn px-4 py-2 text-xs font-semibold text-slate-400 hover:text-white rounded-lg transition duration-200">
                <i class="fa-solid fa-book-open mr-1.5"></i> Virtual Notebook
            </button>
            <button onclick="switchTab('assistant')" id="tab-btn-assistant" class="tab-btn px-4 py-2 text-xs font-semibold text-slate-400 hover:text-white rounded-lg transition duration-200">
                <i class="fa-solid fa-wand-magic-sparkles mr-1.5"></i> Real-time AI Assistant
            </button>
        </nav>

        <div class="flex items-center space-x-3 text-xs">
            <span class="flex items-center px-2.5 py-1 bg-emerald-500/10 text-emerald-400 rounded-full border border-emerald-500/20 font-medium">
                <span class="w-1.5 h-1.5 bg-emerald-400 rounded-full mr-1.5 animate-pulse"></span> Sandbox Connected
            </span>
        </div>
    </header>

    <!-- Main Content Workspace -->
    <main class="flex-1 flex overflow-hidden">
        
        <!-- SIDEBAR CONTROLS: Left Dynamic Control Panel -->
        <aside id="sidebar-playground" class="w-80 bg-slate-900 border-r border-slate-800 p-6 flex flex-col justify-between overflow-y-auto flex-shrink-0">
            <div class="space-y-6">
                <div>
                    <h3 class="text-xs font-bold uppercase tracking-wider text-slate-400 mb-3">Winograd Schema Schema Presets</h3>
                    <div class="space-y-2.5" id="preset-list">
                        <!-- Populated programmatically -->
                    </div>
                </div>

                <div class="border-t border-slate-800 pt-5">
                    <h3 class="text-xs font-bold uppercase tracking-wider text-slate-400 mb-3">Linguistic Context Configuration</h3>
                    <div class="bg-slate-950 p-3 rounded-xl border border-slate-800 space-y-4">
                        <div>
                            <label class="block text-xs font-semibold text-slate-400 mb-1.5">Sentence Variance</label>
                            <div class="grid grid-cols-2 gap-2">
                                <button onclick="setSentenceVariant('A')" id="btn-variant-A" class="px-3 py-1.5 rounded-lg text-xs font-semibold border transition duration-200 bg-indigo-600/20 border-indigo-500 text-indigo-400">
                                    Variant A <span class="block text-[9px] text-slate-400 font-normal">Anticipated reference</span>
                                </button>
                                <button onclick="setSentenceVariant('B')" id="btn-variant-B" class="px-3 py-1.5 rounded-lg text-xs font-semibold border transition duration-200 border-slate-800 text-slate-400 hover:bg-slate-900">
                                    Variant B <span class="block text-[9px] text-slate-400 font-normal">Subtle shift</span>
                                </button>
                            </div>
                        </div>

                        <div>
                            <label class="block text-xs font-semibold text-slate-400 mb-1.5">Model Attention Layer</label>
                            <select id="layer-select" onchange="updateAttentionVisualization()" class="w-full bg-slate-900 border border-slate-800 text-xs text-white rounded-lg p-2 focus:ring-1 focus:ring-indigo-500">
                                <option value="lower">Lower Layers (Syntactic, 1-4)</option>
                                <option value="middle" selected>Middle Layers (Structural, 5-8)</option>
                                <option value="upper">Upper Layers (Semantic/Anaphora, 9-12)</option>
                            </select>
                        </div>
                    </div>
                </div>

                <div class="border-t border-slate-800 pt-5 space-y-3">
                    <h3 class="text-xs font-bold uppercase tracking-wider text-slate-400">Coreference Metrics</h3>
                    <div class="grid grid-cols-2 gap-3">
                        <div class="bg-slate-950 p-3 rounded-xl border border-slate-800 text-center">
                            <span class="text-[10px] text-slate-400 uppercase font-semibold">Target A Attention</span>
                            <div id="metric-target-A" class="text-lg font-bold text-indigo-400 mt-1">--</div>
                        </div>
                        <div class="bg-slate-950 p-3 rounded-xl border border-slate-800 text-center">
                            <span class="text-[10px] text-slate-400 uppercase font-semibold">Target B Attention</span>
                            <div id="metric-target-B" class="text-lg font-bold text-rose-400 mt-1">--</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Footer Help Note -->
            <div class="bg-slate-950 p-3 rounded-lg border border-slate-800 mt-6">
                <p class="text-[10px] text-slate-400 leading-relaxed">
                    <i class="fa-solid fa-circle-info text-indigo-400 mr-1"></i>
                    Observe how changing the context word swaps the attention target of the ambiguous pronoun <b class="text-indigo-300">"it"</b> in the upper layers.
                </p>
            </div>
        </aside>

        <!-- Center / Main Visualization Panels -->
        <section class="flex-1 flex flex-col bg-slate-950 overflow-y-auto">
            
            <!-- TAB 1: COREFERENCE SANDBOX -->
            <div id="tab-content-playground" class="tab-pane p-8 space-y-8 flex-1 flex flex-col justify-between">
                <div>
                    <!-- Section Header -->
                    <div class="flex items-center justify-between mb-6">
                        <div>
                            <h2 class="text-xl font-extrabold text-white">Dynamic Self-Attention Map & Coreference Resolution</h2>
                            <p class="text-xs text-slate-400 mt-1">Trace real-time attention distributions and see how multi-head contextual pathways align tokens.</p>
                        </div>
                        <div class="flex items-center space-x-2 bg-slate-900 border border-slate-800 p-1.5 rounded-lg text-xs">
                            <span class="text-slate-400 font-semibold px-2">Visualization Mode:</span>
                            <button id="view-mode-grid" onclick="setViewMode('grid')" class="px-2.5 py-1 bg-indigo-600/20 text-indigo-400 rounded-md font-semibold border border-indigo-500/30">Grid Matrix</button>
                            <button id="view-mode-tracer" onclick="setViewMode('tracer')" class="px-2.5 py-1 text-slate-400 rounded-md font-semibold hover:bg-slate-800">Direct Tracer</button>
                        </div>
                    </div>

                    <!-- Sentence Bar -->
                    <div class="bg-slate-900 border border-slate-800 p-5 rounded-2xl flex flex-wrap items-center justify-between gap-4 mb-6 relative overflow-hidden shadow-lg">
                        <div class="absolute top-0 left-0 w-1.5 h-full bg-gradient-to-b from-indigo-500 to-violet-500"></div>
                        <div class="flex-1 min-w-[280px]">
                            <span class="text-[10px] font-bold uppercase tracking-wider text-indigo-400 block mb-1">Active Sequence</span>
                            <div id="display-sentence" class="text-base font-medium text-slate-100 flex flex-wrap gap-1 items-center">
                                <!-- Tokens will be displayed here -->
                            </div>
                        </div>
                        <div class="flex items-center space-x-3 shrink-0">
                            <div class="text-right">
                                <span class="text-[9px] uppercase tracking-wider text-slate-500 block">Identified Pronoun</span>
                                <span class="text-xs font-bold text-indigo-400 bg-indigo-500/10 px-2 py-1 rounded border border-indigo-500/20">"it"</span>
                            </div>
                        </div>
                    </div>

                    <!-- MATRIX VISUALIZER CONTAINER -->
                    <div id="vis-container-grid" class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">
                        <!-- Matrix Heatmap Card -->
                        <div class="lg:col-span-8 bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl relative">
                            <h3 class="text-sm font-bold text-white mb-4 flex items-center">
                                <i class="fa-solid fa-grid-2 mr-2 text-indigo-400"></i> Token Attention Score Matrix (QKᵀ)
                            </h3>
                            <div class="overflow-x-auto">
                                <div class="min-w-[450px]">
                                    <!-- Dynamic Heatmap Layout -->
                                    <div id="attention-matrix-grid" class="grid gap-1">
                                        <!-- Computed in JavaScript -->
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Mini explanation Panel on Right -->
                        <div class="lg:col-span-4 bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl space-y-4">
                            <h3 class="text-sm font-bold text-white mb-2"><i class="fa-solid fa-circle-question text-emerald-400 mr-2"></i>What are we seeing?</h3>
                            <div class="text-xs text-slate-400 space-y-3 leading-relaxed">
                                <p>This matrix visualizes the raw dot-product attention scores for the active layer context. Higher luminosity indicates a stronger attention weight between the query (Y-axis) and the key (X-axis).</p>
                                <p>Hover over any tile in the matrix to see the exact numeric attention score mapped to that token pair.</p>
                                <p class="text-indigo-400 border-l-2 border-indigo-500 pl-2">Notice how <b class="text-indigo-200">Upper Layers</b> dynamically focus almost exclusively on resolving coreferences, shifting attention depending on context.</p>
                            </div>
                            <div class="bg-slate-950 p-4 rounded-xl border border-slate-800 space-y-2.5">
                                <span class="text-[10px] font-bold uppercase tracking-wider text-indigo-400 block">Selected Token Interaction</span>
                                <div id="selected-interaction-info" class="text-xs text-slate-300">
                                    Hover over the heatmap tiles to inspect specific parameters.
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- DIRECT TRACER CONTAINER -->
                    <div id="vis-container-tracer" class="hidden grid grid-cols-1 gap-6">
                        <div class="bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl relative overflow-hidden">
                            <h3 class="text-sm font-bold text-white mb-4"><i class="fa-solid fa-network-wired mr-2 text-indigo-400"></i>Direct Token Interaction Tracers</h3>
                            <div id="tracer-layout" class="flex flex-col items-center justify-center py-8 space-y-12 relative min-h-[300px]">
                                <!-- Connected SVG path overlays -->
                                <svg id="tracer-svg" class="absolute inset-0 pointer-events-none w-full h-full"></svg>
                                
                                <!-- Tokens visualization list -->
                                <div id="tracer-tokens-row" class="flex flex-wrap justify-center gap-2.5 max-w-4xl z-10 px-4">
                                    <!-- Plotted dynamically -->
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Explanation / Bottom Segment -->
                <div class="bg-slate-900/60 border border-slate-800/80 rounded-2xl p-6 flex flex-col md:flex-row items-start md:items-center justify-between gap-6">
                    <div class="max-w-2xl">
                        <h4 class="text-sm font-bold text-white mb-1">Empirical Deep-Dive: Contextual Shifts and Coreference Resolution</h4>
                        <p class="text-xs text-slate-400 leading-relaxed">Based on Winograd schema evaluation templates. In lower layers, attention patterns focus on adjacent grammatical blocks. As you descend deeper into the upper layers (Layers 9-12), abstract semantic logic takes over to resolve anaphoras.</p>
                    </div>
                    <div class="shrink-0 flex space-x-2">
                        <button onclick="switchTab('pruning')" class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-xs font-semibold text-white rounded-lg transition duration-200 shadow-lg shadow-indigo-600/10">
                            Continue to Bias Pruning Lab <i class="fa-solid fa-arrow-right ml-1"></i>
                        </button>
                    </div>
                </div>
            </div>

            <!-- TAB 2: ATTENTION HEAD PRUNING LAB -->
            <div id="tab-content-pruning" class="tab-pane hidden p-8 space-y-8 flex-1 flex flex-col justify-between">
                <div>
                    <!-- Section Header -->
                    <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-4 mb-6">
                        <div>
                            <h2 class="text-xl font-extrabold text-white">Structural Mitigation of Bias through Attention Head Pruning</h2>
                            <p class="text-xs text-slate-400 mt-1">Isolate demographic stereotypes in specific attention heads, perform structured pruning, and monitor downstream trade-offs.</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <button onclick="autoPruneHeads()" class="px-3.5 py-2 bg-emerald-600 hover:bg-emerald-700 text-xs font-bold text-white rounded-lg transition duration-200 shadow-md">
                                <i class="fa-solid fa-sparkles mr-1.5"></i> Optimal Auto-Pruning
                            </button>
                            <button onclick="resetPruningLab()" class="px-3.5 py-2 bg-slate-800 hover:bg-slate-700 text-xs font-bold text-slate-300 rounded-lg transition duration-200 border border-slate-700">
                                <i class="fa-solid fa-rotate-left mr-1.5"></i> Reset All Heads
                            </button>
                        </div>
                    </div>

                    <!-- Metrics Dashboard Grid -->
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 mb-8">
                        <div class="bg-slate-900 border border-slate-800 p-5 rounded-2xl relative shadow-lg">
                            <span class="text-[10px] font-bold text-indigo-400 uppercase tracking-wider block mb-1">Stereotype Score (ss)</span>
                            <div class="flex items-baseline space-x-2">
                                <span id="prune-stat-ss" class="text-2xl font-extrabold text-white">62.4%</span>
                                <span id="prune-stat-ss-delta" class="text-xs text-rose-400 font-semibold"><i class="fa-solid fa-arrow-up mr-0.5"></i>Biased</span>
                            </div>
                            <p class="text-[10px] text-slate-400 mt-2 leading-tight">Target: 50% (neutral bias). Measures stereotypical vs anti-stereotypical pronoun routing.</p>
                        </div>

                        <div class="bg-slate-900 border border-slate-800 p-5 rounded-2xl relative shadow-lg">
                            <span class="text-[10px] font-bold text-emerald-400 uppercase tracking-wider block mb-1">Language Modeling Accuracy (lms)</span>
                            <div class="flex items-baseline space-x-2">
                                <span id="prune-stat-lms" class="text-2xl font-extrabold text-white">83.9%</span>
                                <span id="prune-stat-lms-delta" class="text-xs text-emerald-400 font-semibold">Stable</span>
                            </div>
                            <p class="text-[10px] text-slate-400 mt-2 leading-tight">General linguistic capability. Excessive pruning causes this metric to degrade.</p>
                        </div>

                        <div class="bg-slate-900 border border-slate-800 p-5 rounded-2xl relative shadow-lg">
                            <span class="text-[10px] font-bold text-violet-400 uppercase tracking-wider block mb-1">iCAT Alignment Score</span>
                            <div class="flex items-baseline space-x-2">
                                <span id="prune-stat-icat" class="text-2xl font-extrabold text-white">63.1%</span>
                                <span id="prune-stat-icat-delta" class="text-xs text-indigo-400 font-semibold">Baseline</span>
                            </div>
                            <p class="text-[10px] text-slate-400 mt-2 leading-tight">Quantifies the fairness/performance equilibrium. Maximizing this is our alignment goal.</p>
                        </div>

                        <div class="bg-slate-900 border border-slate-800 p-5 rounded-2xl relative shadow-lg">
                            <span class="text-[10px] font-bold text-amber-500 uppercase tracking-wider block mb-1">Pruning Statistics</span>
                            <div class="flex items-baseline space-x-2">
                                <span id="prune-stat-count" class="text-2xl font-extrabold text-white">0 / 144</span>
                                <span class="text-[10px] text-slate-400 ml-1.5 font-medium">Heads Extinguished</span>
                            </div>
                            <p class="text-[10px] text-slate-400 mt-2 leading-tight">Completely removes dimensions, improving compute latency and model size.</p>
                        </div>
                    </div>

                    <!-- Core Pruning Sandbox Layout -->
                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
                        <!-- Left Panel: Interactive Matrix of Attention Heads -->
                        <div class="lg:col-span-7 bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl">
                            <div class="flex items-center justify-between mb-4">
                                <h3 class="text-sm font-bold text-white flex items-center">
                                    <i class="fa-solid fa-cubes-stacked mr-2 text-indigo-400"></i> Structural Head Topology Map (12 x 12 Matrix)
                                </h3>
                                <div class="flex items-center space-x-4 text-[10px]">
                                    <span class="flex items-center text-slate-400"><span class="w-2.5 h-2.5 rounded bg-rose-500 mr-1.5 block"></span> High Bias Target</span>
                                    <span class="flex items-center text-slate-400"><span class="w-2.5 h-2.5 rounded bg-indigo-500 mr-1.5 block"></span> High Linguistic Utility</span>
                                </div>
                            </div>

                            <p class="text-xs text-slate-400 mb-6 leading-relaxed">Hover to inspect. Click on individual heads to prune them. Active (unpruned) heads process information. Pruned heads are completely silenced.</p>

                            <!-- 12x12 Matrix Container -->
                            <div class="space-y-4">
                                <div class="grid grid-cols-13 gap-1.5 text-center text-[10px] font-bold text-slate-500">
                                    <div></div>
                                    <div>H1</div><div>H2</div><div>H3</div><div>H4</div><div>H5</div><div>H6</div>
                                    <div>H7</div><div>H8</div><div>H9</div><div>H10</div><div>H11</div><div>H12</div>
                                </div>
                                <div id="heads-matrix" class="space-y-1.5">
                                    <!-- Generated dynamically in javascript -->
                                </div>
                            </div>
                        </div>

                        <!-- Right Panel: Chart and Real-time Trade-offs -->
                        <div class="lg:col-span-5 space-y-6">
                            <!-- Visual Performance Curve Card -->
                            <div class="bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl">
                                <h3 class="text-sm font-bold text-white mb-4"><i class="fa-solid fa-chart-line mr-2 text-indigo-400"></i>Downstream Trade-off Curve</h3>
                                <div class="h-64 relative">
                                    <canvas id="pruningChart"></canvas>
                                </div>
                                <p class="text-[10px] text-slate-400 mt-3 text-center leading-relaxed">Observe how pruning biased heads initially decreases Stereotype Score without harming Language Modeling performance, optimizing the balanced <b class="text-indigo-400">iCAT score</b>.</p>
                            </div>

                            <!-- Live Feedback / Head Info box -->
                            <div class="bg-slate-900 border border-slate-800 rounded-2xl p-5 shadow-xl space-y-3">
                                <h4 class="text-xs font-bold text-white uppercase tracking-wider">Inspected Head Signature</h4>
                                <div id="head-inspected-details" class="bg-slate-950 p-4 rounded-xl border border-slate-850 text-xs text-slate-400 leading-relaxed">
                                    Hover over any attention block in the topology map to observe localized Shapley value and stereotype contributions.
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Explanation bottom section -->
                <div class="bg-slate-900/60 border border-slate-800/80 rounded-2xl p-6 flex flex-col md:flex-row items-start md:items-center justify-between gap-6">
                    <div class="max-w-2xl">
                        <h4 class="text-sm font-bold text-white mb-1">Empirical Analysis of Pruning Compensation</h4>
                        <p class="text-xs text-slate-400 leading-relaxed">Unlike unstructured pruning which causes parameter sparsity, structured pruning is computationally efficient. Removing localized stereotypical associations yields optimized, fair, and faster inference engines. In practice, models are highly over-parameterized and sustain minimal degradation when structural redundancy is removed.</p>
                    </div>
                    <div class="shrink-0 flex space-x-2">
                        <button onclick="switchTab('notebook')" class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-xs font-semibold text-white rounded-lg transition duration-200 shadow-lg shadow-indigo-600/10">
                            Explore Virtual Notebook <i class="fa-solid fa-arrow-right ml-1"></i>
                        </button>
                    </div>
                </div>
            </div>

            <!-- TAB 3: VIRTUAL JUPYTER NOTEBOOK -->
            <div id="tab-content-notebook" class="tab-pane hidden p-8 space-y-6 flex-1 flex flex-col justify-between">
                <div>
                    <!-- Header -->
                    <div class="mb-6">
                        <h2 class="text-xl font-extrabold text-white">Interactive Jupyter Notebook Workspace</h2>
                        <p class="text-xs text-slate-400 mt-1">Execute live code blocks corresponding directly to the NLP research guide and observe execution terminal outputs.</p>
                    </div>

                    <!-- VS Code / Jupyter IDE Container -->
                    <div class="border border-slate-800 rounded-2xl overflow-hidden shadow-2xl flex flex-col bg-slate-950">
                        <!-- Top file-bar -->
                        <div class="bg-slate-900 border-b border-slate-800 px-4 py-2.5 flex items-center justify-between">
                            <div class="flex items-center space-x-2">
                                <span class="w-3 h-3 rounded-full bg-rose-500/80 block"></span>
                                <span class="w-3 h-3 rounded-full bg-amber-500/80 block"></span>
                                <span class="w-3 h-3 rounded-full bg-emerald-500/80 block"></span>
                                <span class="text-xs font-bold text-slate-400 ml-2 flex items-center">
                                    <i class="fa-brands fa-python text-amber-500 mr-1.5 text-sm"></i> transformer_attention_bias_mitigation.ipynb
                                </span>
                            </div>
                            <div class="flex items-center space-x-1.5 text-xs text-slate-400">
                                <span class="px-2 py-0.5 bg-slate-800 text-slate-300 rounded font-semibold text-[10px]">PyTorch 2.4</span>
                                <span class="px-2 py-0.5 bg-indigo-500/20 text-indigo-400 rounded border border-indigo-500/30 font-semibold text-[10px]">GPU Connected</span>
                            </div>
                        </div>

                        <!-- Notebook Cells -->
                        <div class="p-6 space-y-6 max-h-[500px] overflow-y-auto">
                            <!-- Cell 1 -->
                            <div class="space-y-2">
                                <div class="flex items-center justify-between text-xs font-semibold text-slate-400">
                                    <span>[Cell 1]: Environment Setup and Dependency Installation</span>
                                    <button onclick="runNotebookCell(1)" id="run-btn-1" class="px-3 py-1 bg-indigo-600/20 text-indigo-400 hover:bg-indigo-600 hover:text-white border border-indigo-500/30 rounded-lg transition duration-200">
                                        <i class="fa-solid fa-play mr-1"></i> Run Cell
                                    </button>
                                </div>
                                <div class="bg-slate-900 border border-slate-800 rounded-xl overflow-hidden p-4">
                                    <pre class="mono-font text-xs text-indigo-300 leading-relaxed overflow-x-auto"># Cell 1: Package installation
!pip install -q transformers torch seaborn matplotlib numpy bertviz</pre>
                                </div>
                                <div id="cell-output-1" class="hidden bg-slate-950 border border-slate-905 p-3 rounded-xl text-slate-400 text-xs mono-font space-y-1">
                                    <!-- Executed output logs -->
                                </div>
                            </div>

                            <!-- Cell 2 -->
                            <div class="space-y-2">
                                <div class="flex items-center justify-between text-xs font-semibold text-slate-400">
                                    <span>[Cell 2]: Importing Libraries and Initializing Model</span>
                                    <button onclick="runNotebookCell(2)" id="run-btn-2" class="px-3 py-1 bg-indigo-600/20 text-indigo-400 hover:bg-indigo-600 hover:text-white border border-indigo-500/30 rounded-lg transition duration-200">
                                        <i class="fa-solid fa-play mr-1"></i> Run Cell
                                    </button>
                                </div>
                                <div class="bg-slate-900 border border-slate-800 rounded-xl overflow-hidden p-4">
                                    <pre class="mono-font text-xs text-indigo-300 leading-relaxed overflow-x-auto">import torch
import numpy as np
from transformers import AutoTokenizer, AutoModel

# Initialize tokenizer & model with attention outputs enabled
tokenizer = AutoTokenizer.from_pretrained("distilbert-base-uncased")
model = AutoModel.from_pretrained("distilbert-base-uncased", output_attentions=True)
model.eval()</pre>
                                </div>
                                <div id="cell-output-2" class="hidden bg-slate-950 border border-slate-905 p-3 rounded-xl text-slate-400 text-xs mono-font space-y-1">
                                    <!-- Executed output logs -->
                                </div>
                            </div>

                            <!-- Cell 3 -->
                            <div class="space-y-2">
                                <div class="flex items-center justify-between text-xs font-semibold text-slate-400">
                                    <span>[Cell 3]: Winograd Context Encoding & Forward Pass</span>
                                    <button onclick="runNotebookCell(3)" id="run-btn-3" class="px-3 py-1 bg-indigo-600/20 text-indigo-400 hover:bg-indigo-600 hover:text-white border border-indigo-500/30 rounded-lg transition duration-200">
                                        <i class="fa-solid fa-play mr-1"></i> Run Cell
                                    </button>
                                </div>
                                <div class="bg-slate-900 border border-slate-800 rounded-xl overflow-hidden p-4">
                                    <pre class="mono-font text-xs text-indigo-300 leading-relaxed overflow-x-auto"># Tokenize & trace attention maps
inputs = tokenizer(sample_text, return_tensors="pt")
with torch.no_grad():
    outputs = model(**inputs)

attentions = outputs.attentions
print(f"Num layers: {len(attentions)}, Shape: {attentions[0].shape}")</pre>
                                </div>
                                <div id="cell-output-3" class="hidden bg-slate-950 border border-slate-905 p-3 rounded-xl text-slate-400 text-xs mono-font space-y-1">
                                    <!-- Executed output logs -->
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="bg-slate-900/60 border border-slate-800/80 rounded-2xl p-6 flex flex-col md:flex-row items-start md:items-center justify-between gap-6">
                    <div class="max-w-2xl">
                        <h4 class="text-sm font-bold text-white mb-1">Integrating Custom Frameworks</h4>
                        <p class="text-xs text-slate-400 leading-relaxed">This Jupyter notebook matches standard research designs. You can see how setting the internal flag `output_attentions=True` lets developers inspect raw Multi-Head Attention mechanisms from outer inference layers.</p>
                    </div>
                </div>
            </div>

            <!-- TAB 4: REAL-TIME AI ASSISTANT -->
            <div id="tab-content-assistant" class="tab-pane hidden p-8 space-y-6 flex-1 flex flex-col justify-between">
                <div>
                    <!-- Header -->
                    <div class="mb-6">
                        <h2 class="text-xl font-extrabold text-white">Transformer Attention & Bias AI Analyst</h2>
                        <p class="text-xs text-slate-400 mt-1">Submit custom sentences to generate realistic tokenization mapping, coreference evaluation, and demographic bias detection.</p>
                    </div>

                    <!-- Interactive Workspace -->
                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-stretch">
                        <!-- Left Panel: Chat & Action Controller -->
                        <div class="lg:col-span-6 bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl flex flex-col justify-between space-y-6">
                            <div class="space-y-4">
                                <h3 class="text-sm font-bold text-white"><i class="fa-solid fa-robot mr-2 text-indigo-400"></i>Linguistic Query Engine</h3>
                                <p class="text-xs text-slate-400 leading-relaxed">Type any sentence below. The system will leverage the `gemini-3-flash-preview` model to map tokens, extract semantic relations, and detect hidden gendered occupational biases.</p>
                                
                                <div class="bg-slate-950 p-4 rounded-xl border border-slate-850 space-y-2 text-xs">
                                    <span class="text-slate-300 font-semibold block">Try these recommended queries:</span>
                                    <button onclick="fillAssistantQuery('The doctor phoned the assistant because she needed assistance.')" class="w-full text-left p-2 rounded bg-slate-900 hover:bg-slate-850 text-slate-400 hover:text-white border border-slate-800 transition duration-150">
                                        "The doctor phoned the assistant because she needed assistance."
                                    </button>
                                    <button onclick="fillAssistantQuery('The developer built a compiler because they wanted a tool.')" class="w-full text-left p-2 rounded bg-slate-900 hover:bg-slate-850 text-slate-400 hover:text-white border border-slate-800 transition duration-150">
                                        "The developer built a compiler because they wanted a tool."
                                    </button>
                                </div>
                            </div>

                            <div class="space-y-4">
                                <div>
                                    <label class="block text-xs font-semibold text-slate-400 mb-1.5">Your Custom Sentence</label>
                                    <textarea id="ai-input-sentence" rows="3" class="w-full bg-slate-950 border border-slate-800 text-xs text-white rounded-xl p-3 focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500" placeholder="Type a sentence (e.g. The lawyer argued with the clerk because she was impatient)..."></textarea>
                                </div>

                                <button id="submit-ai-analysis" onclick="executeAiAnalysis()" class="w-full py-3 bg-indigo-600 hover:bg-indigo-700 text-xs font-bold text-white rounded-xl transition duration-200 flex items-center justify-center shadow-lg shadow-indigo-600/10">
                                    <i class="fa-solid fa-paper-plane mr-2"></i> Submit and Generate Attention Map
                                </button>
                            </div>
                        </div>

                        <!-- Right Panel: Live Response Visualizer -->
                        <div class="lg:col-span-6 bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl flex flex-col justify-between min-h-[400px]">
                            <div class="space-y-4 flex-1">
                                <h3 class="text-sm font-bold text-white flex items-center">
                                    <i class="fa-solid fa-terminal mr-2 text-indigo-400"></i> Simulated Transformer Evaluation Logs
                                </h3>

                                <div id="ai-analysis-output-container" class="space-y-4 flex-1 flex flex-col justify-center">
                                    <!-- Default empty state -->
                                    <div id="ai-output-empty-state" class="text-center py-12">
                                        <div class="w-16 h-16 rounded-full bg-slate-950 border border-slate-800 flex items-center justify-center mx-auto mb-4">
                                            <i class="fa-solid fa-brain text-slate-500 text-lg"></i>
                                        </div>
                                        <p class="text-xs text-slate-400">Awaiting your prompt. Send a query to execute high-fidelity attention mapping.</p>
                                    </div>

                                    <!-- Loading state -->
                                    <div id="ai-output-loader" class="hidden text-center py-12">
                                        <div class="w-12 h-12 rounded-full border-2 border-indigo-500 border-t-transparent animate-spin mx-auto mb-4"></div>
                                        <p class="text-xs text-slate-300">Contacting Gemini AI and compiling weights...</p>
                                        <p id="ai-loader-retry-hint" class="text-[10px] text-slate-500 mt-1 hidden">Implementing exponential backoff...</p>
                                    </div>

                                    <!-- Output block -->
                                    <div id="ai-output-details" class="hidden space-y-4">
                                        <div class="bg-slate-950 p-4 rounded-xl border border-slate-850 space-y-2">
                                            <span class="text-[10px] font-bold text-indigo-400 uppercase tracking-wider block">1. Token Map & Coreference Resolution</span>
                                            <p id="ai-res-explanation" class="text-xs text-slate-300 leading-relaxed"></p>
                                        </div>

                                        <div class="bg-slate-950 p-4 rounded-xl border border-slate-850 space-y-2">
                                            <span class="text-[10px] font-bold text-rose-400 uppercase tracking-wider block">2. Stereotype Bias Profile</span>
                                            <p id="ai-res-bias" class="text-xs text-slate-300 leading-relaxed"></p>
                                        </div>

                                        <div class="bg-slate-950 p-4 rounded-xl border border-slate-850 space-y-3">
                                            <span class="text-[10px] font-bold text-emerald-400 uppercase tracking-wider block">3. Approximation Vector Matrix</span>
                                            <!-- Dynamically generated visual distribution map -->
                                            <div id="ai-res-attention-bars" class="space-y-1.5 text-xs">
                                                <!-- Generated bar distributions -->
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="bg-slate-900/60 border border-slate-800/80 rounded-2xl p-6">
                    <p class="text-xs text-slate-400 leading-relaxed"><i class="fa-solid fa-triangle-exclamation mr-1.5 text-amber-500"></i><b>Real-world Note</b>: Due to client-side sandboxing, standard API interactions require correct endpoints. This component utilizes exponential backoff to handle rate throttling natively.</p>
                </div>
            </div>

        </section>

    </main>

    <!-- Core Application Logic / JS -->
    <script>
        // State storage
        let activeTab = 'playground';
        let currentSentenceVariant = 'A';
        let selectedPresetId = 1;
        let viewMode = 'grid'; // grid or tracer
        let selectedLayerIndex = 'middle'; // lower, middle, upper
        let prunedHeads = new Set();
        let chartInstance = null;

        // Custom sentence analysis simulated/cached state
        let customAnalysisCache = {};

        // 144 heads baseline attributes
        const attentionHeadsData = [];
        function initHeadsData() {
            for (let layer = 0; layer < 12; layer++) {
                for (let head = 0; head < 12; head++) {
                    // Seed biased heads primarily in higher layers (layers 8-11)
                    let baseBias = 0;
                    if (layer >= 8) {
                        baseBias = Math.random() * 0.4 + 0.3; // High base bias contribution
                        // Focus on random specific heads
                        if ([2, 5, 8, 10].includes(head)) baseBias += 0.25;
                    } else if (layer >= 4) {
                        baseBias = Math.random() * 0.2;
                    } else {
                        baseBias = Math.random() * 0.05;
                    }
                    baseBias = Math.min(Math.max(baseBias, 0.01), 0.95);

                    // Seed linguistic utility. Higher in early and middle levels (layers 2-9)
                    let utility = 0;
                    if (layer >= 2 && layer <= 9) {
                        utility = Math.random() * 0.5 + 0.3;
                        if ([0, 1, 3, 7].includes(head)) utility += 0.15;
                    } else {
                        utility = Math.random() * 0.2;
                    }
                    utility = Math.min(Math.max(utility, 0.01), 0.95);

                    attentionHeadsData.push({
                        layer,
                        head,
                        bias: baseBias,
                        utility
                    });
                }
            }
        }

        // Preset Winograd schemas matching document evaluation benchmarks
        const winogradPresets = [
            {
                id: 1,
                label: "Winograd Schema A (Animal vs Street)",
                sentenceA: "The animal didn't cross the street because it was too tired.",
                sentenceB: "The animal didn't cross the street because it was too wide.",
                tokensA: ["[CLS]", "The", "animal", "didn", "'", "t", "cross", "the", "street", "because", "it", "was", "too", "tired", ".", "[SEP]"],
                tokensB: ["[CLS]", "The", "animal", "didn", "'", "t", "cross", "the", "street", "because", "it", "was", "too", "wide", ".", "[SEP]"],
                focusToken: "it",
                targetA: "animal",
                targetB: "street",
                attentionA: {
                    lower: { "[CLS]": 0.01, "The": 0.05, "animal": 0.08, "didn": 0.02, "'": 0.01, "t": 0.01, "cross": 0.03, "the": 0.04, "street": 0.05, "because": 0.1, "it": 0.4, "was": 0.12, "too": 0.05, "tired": 0.02, ".": 0.01, "[SEP]": 0.00 },
                    middle: { "[CLS]": 0.01, "The": 0.02, "animal": 0.15, "didn": 0.01, "'": 0.01, "t": 0.01, "cross": 0.18, "the": 0.02, "street": 0.12, "because": 0.08, "it": 0.22, "was": 0.1, "too": 0.05, "tired": 0.01, ".": 0.01, "[SEP]": 0.00 },
                    upper: { "[CLS]": 0.00, "The": 0.01, "animal": 0.65, "didn": 0.01, "'": 0.01, "t": 0.01, "cross": 0.06, "the": 0.01, "street": 0.05, "because": 0.02, "it": 0.12, "was": 0.03, "too": 0.01, "tired": 0.01, ".": 0.00, "[SEP]": 0.00 }
                },
                attentionB: {
                    lower: { "[CLS]": 0.01, "The": 0.05, "animal": 0.05, "didn": 0.02, "'": 0.01, "t": 0.01, "cross": 0.03, "the": 0.04, "street": 0.08, "because": 0.1, "it": 0.4, "was": 0.12, "too": 0.05, "wide": 0.02, ".": 0.01, "[SEP]": 0.00 },
                    middle: { "[CLS]": 0.01, "The": 0.02, "animal": 0.12, "didn": 0.01, "'": 0.01, "t": 0.01, "cross": 0.15, "the": 0.02, "street": 0.18, "because": 0.08, "it": 0.22, "was": 0.1, "too": 0.05, "wide": 0.01, ".": 0.01, "[SEP]": 0.00 },
                    upper: { "[CLS]": 0.00, "The": 0.01, "animal": 0.06, "didn": 0.01, "'": 0.01, "t": 0.01, "cross": 0.05, "the": 0.01, "street": 0.68, "because": 0.02, "it": 0.11, "was": 0.02, "too": 0.01, "wide": 0.01, ".": 0.00, "[SEP]": 0.00 }
                }
            },
            {
                id: 2,
                label: "Winograd Schema B (Trophy vs Suitcase)",
                sentenceA: "The trophy didn't fit into the brown suitcase because it was too small.",
                sentenceB: "The trophy didn't fit into the brown suitcase because it was too large.",
                tokensA: ["[CLS]", "The", "trophy", "didn", "'", "t", "fit", "into", "the", "brown", "suitcase", "because", "it", "was", "too", "small", ".", "[SEP]"],
                tokensB: ["[CLS]", "The", "trophy", "didn", "'", "t", "fit", "into", "the", "brown", "suitcase", "because", "it", "was", "too", "large", ".", "[SEP]"],
                focusToken: "it",
                targetA: "suitcase",
                targetB: "trophy",
                attentionA: {
                    lower: { "[CLS]": 0.01, "The": 0.03, "trophy": 0.06, "didn": 0.02, "'": 0.01, "t": 0.01, "fit": 0.04, "into": 0.02, "the": 0.03, "brown": 0.02, "suitcase": 0.09, "because": 0.08, "it": 0.42, "was": 0.11, "too": 0.04, "small": 0.01, ".": 0.01, "[SEP]": 0.00 },
                    middle: { "[CLS]": 0.01, "The": 0.01, "trophy": 0.12, "didn": 0.01, "'": 0.01, "t": 0.01, "fit": 0.14, "into": 0.02, "the": 0.02, "brown": 0.04, "suitcase": 0.16, "because": 0.05, "it": 0.25, "was": 0.08, "too": 0.05, "small": 0.02, ".": 0.01, "[SEP]": 0.00 },
                    upper: { "[CLS]": 0.00, "The": 0.01, "trophy": 0.08, "didn": 0.01, "'": 0.01, "t": 0.01, "fit": 0.03, "into": 0.01, "the": 0.01, "brown": 0.02, "suitcase": 0.61, "because": 0.01, "it": 0.14, "was": 0.03, "too": 0.01, "small": 0.01, ".": 0.00, "[SEP]": 0.00 }
                },
                attentionB: {
                    lower: { "[CLS]": 0.01, "The": 0.03, "trophy": 0.09, "didn": 0.02, "'": 0.01, "t": 0.01, "fit": 0.04, "into": 0.02, "the": 0.03, "brown": 0.02, "suitcase": 0.06, "because": 0.08, "it": 0.42, "was": 0.11, "too": 0.04, "large": 0.01, ".": 0.01, "[SEP]": 0.00 },
                    middle: { "[CLS]": 0.01, "The": 0.01, "trophy": 0.16, "didn": 0.01, "'": 0.01, "t": 0.01, "fit": 0.14, "into": 0.02, "the": 0.02, "brown": 0.04, "suitcase": 0.12, "because": 0.05, "it": 0.25, "was": 0.08, "too": 0.05, "large": 0.02, ".": 0.01, "[SEP]": 0.00 },
                    upper: { "[CLS]": 0.00, "The": 0.01, "trophy": 0.63, "didn": 0.01, "'": 0.01, "t": 0.01, "fit": 0.03, "into": 0.01, "the": 0.01, "brown": 0.02, "suitcase": 0.08, "because": 0.01, "it": 0.12, "was": 0.03, "too": 0.01, "large": 0.01, ".": 0.00, "[SEP]": 0.00 }
                }
            }
        ];

        window.onload = function() {
            initHeadsData();
            populatePresets();
            loadActivePreset();
            initPruningTopology();
            updatePruningStats();
            initPruningChart();
            
            // Adjust canvas responsiveness on resize
            window.addEventListener('resize', () => {
                if (chartInstance) chartInstance.resize();
                if (viewMode === 'tracer') drawTracerLines();
            });
        };

        // Populate preset sidebar lists
        function populatePresets() {
            const listContainer = document.getElementById('preset-list');
            listContainer.innerHTML = '';
            
            winogradPresets.forEach(preset => {
                const button = document.createElement('button');
                button.id = `preset-btn-${preset.id}`;
                button.onclick = () => selectPreset(preset.id);
                button.className = `w-full text-left p-3 rounded-xl border transition duration-200 flex items-start gap-2.5 ${preset.id === selectedPresetId ? 'bg-indigo-600/10 border-indigo-500 text-indigo-400' : 'bg-slate-950 border-slate-800 text-slate-400 hover:bg-slate-900'}`;
                
                button.innerHTML = `
                    <i class="fa-solid fa-code text-xs mt-1 shrink-0 ${preset.id === selectedPresetId ? 'text-indigo-400' : 'text-slate-500'}"></i>
                    <div>
                        <span class="text-[10px] font-bold uppercase tracking-wider block mb-0.5">${preset.id === 1 ? 'Benchmark Coreference 1' : 'Benchmark Coreference 2'}</span>
                        <span class="text-xs font-semibold block leading-tight text-slate-200">${preset.label}</span>
                    </div>
                `;
                listContainer.appendChild(button);
            });
        }

        // Handle preset changes
        function selectPreset(id) {
            document.getElementById(`preset-btn-${selectedPresetId}`).className = "w-full text-left p-3 rounded-xl border transition duration-200 flex items-start gap-2.5 bg-slate-950 border-slate-800 text-slate-400 hover:bg-slate-900";
            selectedPresetId = id;
            document.getElementById(`preset-btn-${selectedPresetId}`).className = "w-full text-left p-3 rounded-xl border transition duration-200 flex items-start gap-2.5 bg-indigo-600/10 border-indigo-500 text-indigo-400";
            loadActivePreset();
        }

        // Load configurations
        function loadActivePreset() {
            const preset = winogradPresets.find(p => p.id === selectedPresetId);
            const sentenceStr = currentSentenceVariant === 'A' ? preset.sentenceA : preset.sentenceB;
            const tokens = currentSentenceVariant === 'A' ? preset.tokensA : preset.tokensB;

            // Render interactive display
            const targetContainer = document.getElementById('display-sentence');
            targetContainer.innerHTML = '';
            
            tokens.forEach(tok => {
                const span = document.createElement('span');
                span.className = `px-2 py-1 rounded transition duration-150 ${tok === preset.focusToken ? 'bg-indigo-600 text-white font-bold animate-pulse' : 'hover:bg-slate-800 text-slate-300'}`;
                if (tok === preset.targetA && currentSentenceVariant === 'A') {
                    span.className = `px-2 py-1 rounded bg-indigo-500/20 text-indigo-300 font-bold border border-indigo-500/30`;
                } else if (tok === preset.targetB && currentSentenceVariant === 'B') {
                    span.className = `px-2 py-1 rounded bg-rose-500/20 text-rose-300 font-bold border border-rose-500/30`;
                }
                span.innerText = tok;
                targetContainer.appendChild(span);
            });

            updateAttentionVisualization();
        }

        // Set Winograd Variant
        function setSentenceVariant(v) {
            currentSentenceVariant = v;
            const btnA = document.getElementById('btn-variant-A');
            const btnB = document.getElementById('btn-variant-B');

            if (v === 'A') {
                btnA.className = "px-3 py-1.5 rounded-lg text-xs font-semibold border transition duration-200 bg-indigo-600/20 border-indigo-500 text-indigo-400";
                btnB.className = "px-3 py-1.5 rounded-lg text-xs font-semibold border transition duration-200 border-slate-800 text-slate-400 hover:bg-slate-900";
            } else {
                btnB.className = "px-3 py-1.5 rounded-lg text-xs font-semibold border transition duration-200 bg-indigo-600/20 border-indigo-500 text-indigo-400";
                btnA.className = "px-3 py-1.5 rounded-lg text-xs font-semibold border transition duration-200 border-slate-800 text-slate-400 hover:bg-slate-900";
            }
            loadActivePreset();
        }

        // Change View Options
        function setViewMode(mode) {
            viewMode = mode;
            const gridBtn = document.getElementById('view-mode-grid');
            const tracerBtn = document.getElementById('view-mode-tracer');
            const gridContainer = document.getElementById('vis-container-grid');
            const tracerContainer = document.getElementById('vis-container-tracer');

            if (mode === 'grid') {
                gridBtn.className = "px-2.5 py-1 bg-indigo-600/20 text-indigo-400 rounded-md font-semibold border border-indigo-500/30";
                tracerBtn.className = "px-2.5 py-1 text-slate-400 rounded-md font-semibold hover:bg-slate-800";
                gridContainer.classList.remove('hidden');
                tracerContainer.classList.add('hidden');
            } else {
                tracerBtn.className = "px-2.5 py-1 bg-indigo-600/20 text-indigo-400 rounded-md font-semibold border border-indigo-500/30";
                gridBtn.className = "px-2.5 py-1 text-slate-400 rounded-md font-semibold hover:bg-slate-800";
                tracerContainer.classList.remove('hidden');
                gridContainer.classList.add('hidden');
                setTimeout(drawTracerLines, 100);
            }
        }

        // Navigation Controller
        function switchTab(tab) {
            activeTab = tab;
            // Update Navigation Menu Active Buttons
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.className = "tab-btn px-4 py-2 text-xs font-semibold text-slate-400 hover:text-white rounded-lg transition duration-200";
            });
            const activeBtn = document.getElementById(`tab-btn-${tab}`);
            if (activeBtn) {
                activeBtn.className = "tab-btn px-4 py-2 text-xs font-semibold rounded-lg transition duration-200 bg-indigo-600 text-white shadow-md";
            }

            // Toggle panes
            document.querySelectorAll('.tab-pane').forEach(pane => {
                pane.classList.add('hidden');
            });
            document.getElementById(`tab-content-${tab}`).classList.remove('hidden');

            // Handle sidebars
            const sidebar = document.getElementById('sidebar-playground');
            if (tab === 'playground') {
                sidebar.classList.remove('hidden');
            } else {
                sidebar.classList.add('hidden');
            }

            // Fire custom triggers
            if (tab === 'pruning' && chartInstance) {
                setTimeout(() => chartInstance.update(), 50);
            } else if (tab === 'playground' && viewMode === 'tracer') {
                setTimeout(drawTracerLines, 50);
            }
        }

        // Render Dynamic Self-Attention Visuals
        function updateAttentionVisualization() {
            const preset = winogradPresets.find(p => p.id === selectedPresetId);
            const selectedLayer = document.getElementById('layer-select').value;
            const attentionMap = currentSentenceVariant === 'A' ? preset.attentionA[selectedLayer] : preset.attentionB[selectedLayer];
            const tokens = currentSentenceVariant === 'A' ? preset.tokensA : preset.tokensB;

            // Update local metric summaries
            const metricA = attentionMap[preset.targetA] || 0;
            const metricB = attentionMap[preset.targetB] || 0;

            document.getElementById('metric-target-A').innerText = `${(metricA * 100).toFixed(1)}%`;
            document.getElementById('metric-target-B').innerText = `${(metricB * 100).toFixed(1)}%`;

            // Color-code metrics based on dominance
            if (currentSentenceVariant === 'A') {
                document.getElementById('metric-target-A').className = "text-lg font-bold text-emerald-400";
                document.getElementById('metric-target-B').className = "text-lg font-bold text-slate-500";
            } else {
                document.getElementById('metric-target-A').className = "text-lg font-bold text-slate-500";
                document.getElementById('metric-target-B').className = "text-lg font-bold text-rose-400";
            }

            // 1. Grid matrix representation
            const matrixGrid = document.getElementById('attention-matrix-grid');
            matrixGrid.innerHTML = '';
            
            // Layout dimension styles
            matrixGrid.style.gridTemplateColumns = `repeat(${tokens.length + 1}, minmax(0, 1fr))`;

            // Header row elements
            const emptySpace = document.createElement('div');
            emptySpace.className = "text-[9px] font-bold text-slate-500 flex items-center justify-center border-b border-r border-slate-800 p-1 bg-slate-950";
            emptySpace.innerText = "Y\\X";
            matrixGrid.appendChild(emptySpace);

            tokens.forEach(tok => {
                const hCol = document.createElement('div');
                hCol.className = "text-[9px] font-semibold text-slate-500 text-center truncate p-1 bg-slate-950 border-b border-slate-800";
                hCol.innerText = tok;
                matrixGrid.appendChild(hCol);
            });

            // Populate table rows
            tokens.forEach((rowTok, rowIndex) => {
                const labelCol = document.createElement('div');
                labelCol.className = "text-[9px] font-semibold text-slate-500 truncate p-1 bg-slate-950 border-r border-slate-800 flex items-center";
                labelCol.innerText = rowTok;
                matrixGrid.appendChild(labelCol);

                tokens.forEach((colTok, colIndex) => {
                    // Generate approximation distribution values centered around query index mapping
                    let score = 0.01;
                    if (rowTok === preset.focusToken) {
                        score = attentionMap[colTok] || 0.01;
                    } else if (rowIndex === colIndex) {
                        score = 0.6 + Math.random() * 0.15; // High identity diagonal attention mapping
                    } else if (Math.abs(rowIndex - colIndex) === 1) {
                        score = 0.1 + Math.random() * 0.1; // Neighboring weights
                    } else {
                        score = Math.random() * 0.03;
                    }
                    score = Math.min(Math.max(score, 0), 1);

                    const cell = document.createElement('div');
                    cell.style.backgroundColor = `rgba(79, 70, 229, ${score})`;
                    cell.className = "aspect-square w-full rounded border border-slate-950 hover:border-white/40 cursor-pointer transition duration-100 flex items-center justify-center";
                    cell.setAttribute('title', `${rowTok} ➔ ${colTok}: ${score.toFixed(4)}`);
                    
                    cell.onmouseenter = () => {
                        document.getElementById('selected-interaction-info').innerHTML = `
                            <div class="space-y-1">
                                <p><span class="text-slate-500">Query Word:</span> <b class="text-white">"${rowTok}"</b></p>
                                <p><span class="text-slate-500">Key Target:</span> <b class="text-white">"${colTok}"</b></p>
                                <p><span class="text-slate-500">Attention Value:</span> <b class="text-emerald-400 font-mono">${score.toFixed(4)}</b></p>
                            </div>
                        `;
                    };

                    matrixGrid.appendChild(cell);
                });
            });

            // 2. Tracer direct pathway visualization
            const tracerRow = document.getElementById('tracer-tokens-row');
            tracerRow.innerHTML = '';

            tokens.forEach((tok, index) => {
                const tokDiv = document.createElement('div');
                tokDiv.id = `tracer-tok-${index}`;
                
                let highlightClass = "bg-slate-900 border-slate-800 text-slate-300";
                if (tok === preset.focusToken) {
                    highlightClass = "bg-indigo-600 border-indigo-500 text-white font-bold ring-2 ring-indigo-500/40";
                } else if (tok === preset.targetA && currentSentenceVariant === 'A') {
                    highlightClass = "bg-emerald-500/20 border-emerald-500 text-emerald-400 font-bold";
                } else if (tok === preset.targetB && currentSentenceVariant === 'B') {
                    highlightClass = "bg-rose-500/20 border-rose-500 text-rose-400 font-bold";
                }

                tokDiv.className = `px-3 py-2 rounded-xl border text-xs cursor-default select-none ${highlightClass}`;
                tokDiv.innerText = tok;
                tracerRow.appendChild(tokDiv);
            });

            if (viewMode === 'tracer') {
                setTimeout(drawTracerLines, 100);
            }
        }

        // Draw overlay bezier curves for Tracer View
        function drawTracerLines() {
            const preset = winogradPresets.find(p => p.id === selectedPresetId);
            const selectedLayer = document.getElementById('layer-select').value;
            const attentionMap = currentSentenceVariant === 'A' ? preset.attentionA[selectedLayer] : preset.attentionB[selectedLayer];
            const tokens = currentSentenceVariant === 'A' ? preset.tokensA : preset.tokensB;

            const svg = document.getElementById('tracer-svg');
            const svgRect = svg.getBoundingClientRect();
            svg.innerHTML = '';

            const focusIndex = tokens.indexOf(preset.focusToken);
            const queryEl = document.getElementById(`tracer-tok-${focusIndex}`);
            if (!queryEl) return;

            const qRect = queryEl.getBoundingClientRect();
            const qX = (qRect.left + qRect.right) / 2 - svgRect.left;
            const qY = qRect.top - svgRect.top;

            // Plot curves
            tokens.forEach((tok, keyIndex) => {
                if (keyIndex === focusIndex) return;

                const weight = attentionMap[tok] || 0.01;
                if (weight < 0.02) return; // Cut off noise pathways

                const keyEl = document.getElementById(`tracer-tok-${keyIndex}`);
                if (!keyEl) return;

                const kRect = keyEl.getBoundingClientRect();
                const kX = (kRect.left + kRect.right) / 2 - svgRect.left;
                const kY = kRect.top - svgRect.top;

                // Create quadratic bezier curve
                const path = document.createElementNS("http://www.w3.org/2000/svg", "path");
                const midX = (qX + kX) / 2;
                const midY = Math.min(qY, kY) - 100 - (weight * 60); // Arch based on connection weight

                const d = `M ${qX} ${qY} Q ${midX} ${midY} ${kX} ${kY}`;
                path.setAttribute("d", d);
                path.setAttribute("fill", "none");
                
                // Styling connection pathways
                let color = `rgba(99, 102, 241, ${weight})`;
                if (tok === preset.targetA && currentSentenceVariant === 'A') {
                    color = `rgba(16, 185, 129, ${weight + 0.1})`;
                } else if (tok === preset.targetB && currentSentenceVariant === 'B') {
                    color = `rgba(244, 63, 94, ${weight + 0.1})`;
                }

                path.setAttribute("stroke", color);
                path.setAttribute("stroke-width", `${weight * 6 + 1}`);
                svg.appendChild(path);
            });
        }

        // Initialize dynamic matrix list in Tab 2
        function initPruningTopology() {
            const matrixContainer = document.getElementById('heads-matrix');
            matrixContainer.innerHTML = '';

            for (let layer = 0; layer < 12; layer++) {
                const row = document.createElement('div');
                row.className = "grid grid-cols-13 gap-1.5 items-center";

                // Layer indicator Label on Left
                const lLabel = document.createElement('div');
                lLabel.className = "text-[9px] font-bold text-slate-500 text-left";
                lLabel.innerText = `L${layer + 1}`;
                row.appendChild(lLabel);

                // Heads in row mapping
                for (let head = 0; head < 12; head++) {
                    const headId = layer * 12 + head;
                    const headData = attentionHeadsData[headId];
                    const element = document.createElement('div');
                    
                    element.id = `topology-head-${headId}`;
                    element.onclick = () => togglePruneHead(headId);
                    
                    // Determine initial backgrounds
                    let bg = "bg-slate-850 hover:bg-slate-800 border-slate-700";
                    if (headData.bias > 0.5) bg = "bg-rose-500/20 hover:bg-rose-500/35 border-rose-500/30";
                    if (headData.utility > 0.6) bg = "bg-indigo-500/20 hover:bg-indigo-500/35 border-indigo-500/30";

                    element.className = `aspect-square rounded border cursor-pointer transition duration-150 ${bg}`;
                    
                    element.onmouseenter = () => {
                        const status = prunedHeads.has(headId) ? '<span class="text-rose-400 font-bold">PRUNED</span>' : '<span class="text-emerald-400 font-bold">ACTIVE</span>';
                        document.getElementById('head-inspected-details').innerHTML = `
                            <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <p class="font-bold text-white text-xs mb-1">Layer ${layer + 1}, Head ${head + 1}</p>
                                    <p><span class="text-slate-500">Status:</span> ${status}</p>
                                </div>
                                <div class="space-y-0.5 text-[11px]">
                                    <p><span class="text-slate-500">Stereotype Cont:</span> <b class="text-rose-400">${(headData.bias * 100).toFixed(1)}%</b></p>
                                    <p><span class="text-slate-500">Utility Value:</span> <b class="text-indigo-400">${(headData.utility * 100).toFixed(1)}%</b></p>
                                </div>
                            </div>
                        `;
                    };

                    row.appendChild(element);
                }
                matrixContainer.appendChild(row);
            }
        }

        // Toggle structural pruning state
        function togglePruneHead(headId) {
            const element = document.getElementById(`topology-head-${headId}`);
            if (prunedHeads.has(headId)) {
                prunedHeads.delete(headId);
                // Restore original color mapping styles
                const headData = attentionHeadsData[headId];
                let bg = "bg-slate-850 hover:bg-slate-800 border-slate-700";
                if (headData.bias > 0.5) bg = "bg-rose-500/20 hover:bg-rose-500/35 border-rose-500/30";
                if (headData.utility > 0.6) bg = "bg-indigo-500/20 hover:bg-indigo-500/35 border-indigo-500/30";
                element.className = `aspect-square rounded border cursor-pointer transition duration-150 ${bg}`;
            } else {
                prunedHeads.add(headId);
                // Style silenced block
                element.className = "aspect-square rounded border border-slate-900 bg-slate-950 shadow-inner scale-90 relative flex items-center justify-center after:content-[''] after:w-1.5 after:h-1.5 after:bg-slate-750 after:rounded-full";
            }

            updatePruningStats();
        }

        // Recalculate metrics based on pruning vectors
        function updatePruningStats() {
            let totalBiasReduction = 0;
            let totalUtilityLoss = 0;

            prunedHeads.forEach(headId => {
                const headData = attentionHeadsData[headId];
                totalBiasReduction += headData.bias;
                totalUtilityLoss += headData.utility;
            });

            // Adjust values dynamically
            const numPruned = prunedHeads.size;
            
            // Stereotype score starts at 62.4% and drops to 50.0%
            let ss = 62.4 - (totalBiasReduction * 1.5);
            ss = Math.max(ss, 50.0);

            // Language Modeling accuracy starts at 83.9% and drops
            let lms = 83.9 - (totalUtilityLoss * 0.8);
            lms = Math.max(lms, 25.0);

            // Calculate iCAT = lms * (1 - |ss - 50|/50)
            const icat = lms * (1 - Math.abs(ss - 50) / 50);

            // Print updating values
            document.getElementById('prune-stat-ss').innerText = `${ss.toFixed(1)}%`;
            document.getElementById('prune-stat-lms').innerText = `${lms.toFixed(1)}%`;
            document.getElementById('prune-stat-icat').innerText = `${icat.toFixed(1)}%`;
            document.getElementById('prune-stat-count').innerText = `${numPruned} / 144`;

            // Adjust visual indicators
            const ssDelta = document.getElementById('prune-stat-ss-delta');
            if (ss > 55) {
                ssDelta.className = "text-xs text-rose-400 font-semibold";
                ssDelta.innerHTML = '<i class="fa-solid fa-arrow-up mr-0.5"></i> Biased';
            } else if (ss > 51) {
                ssDelta.className = "text-xs text-yellow-500 font-semibold";
                ssDelta.innerHTML = '<i class="fa-solid fa-arrows-left-right mr-0.5"></i> Aligned';
            } else {
                ssDelta.className = "text-xs text-emerald-400 font-semibold";
                ssDelta.innerHTML = '<i class="fa-solid fa-check mr-0.5"></i> Balanced';
            }

            const lmsDelta = document.getElementById('prune-stat-lms-delta');
            if (lms > 80) {
                lmsDelta.className = "text-xs text-emerald-400 font-semibold";
                lmsDelta.innerText = "Stable";
            } else if (lms > 70) {
                lmsDelta.className = "text-xs text-yellow-500 font-semibold";
                lmsDelta.innerText = "Slight loss";
            } else {
                lmsDelta.className = "text-xs text-rose-400 font-semibold";
                lmsDelta.innerText = "Compromised";
            }

            const icatDelta = document.getElementById('prune-stat-icat-delta');
            if (numPruned === 0) {
                icatDelta.className = "text-xs text-indigo-400 font-semibold";
                icatDelta.innerText = "Baseline";
            } else {
                // Determine optimization vs loss
                const deltaVal = icat - 63.1;
                if (deltaVal > 0) {
                    icatDelta.className = "text-xs text-emerald-400 font-semibold";
                    icatDelta.innerText = `+${deltaVal.toFixed(1)}% Gain`;
                } else {
                    icatDelta.className = "text-xs text-rose-400 font-semibold";
                    icatDelta.innerText = `${deltaVal.toFixed(1)}% Loss`;
                }
            }

            updatePruningChartData(ss, lms, icat);
        }

        // Automatic search sequence to optimize model
        function autoPruneHeads() {
            resetPruningLab();
            // Sort heads based on highest bias-to-utility ratio
            const sortedIndices = attentionHeadsData
                .map((d, index) => ({ index, ratio: d.bias / (d.utility + 0.1) }))
                .sort((a, b) => b.ratio - a.ratio);

            // Prune top high-yield heads programmatically
            for (let i = 0; i < 18; i++) {
                prunedHeads.add(sortedIndices[i].index);
            }

            // Sync visual grid matrix
            initPruningTopology();
            prunedHeads.forEach(id => {
                const element = document.getElementById(`topology-head-${id}`);
                element.className = "aspect-square rounded border border-slate-900 bg-slate-950 shadow-inner scale-90 relative flex items-center justify-center after:content-[''] after:w-1.5 after:h-1.5 after:bg-slate-750 after:rounded-full";
            });

            updatePruningStats();
        }

        // Reset Lab
        function resetPruningLab() {
            prunedHeads.clear();
            initPruningTopology();
            updatePruningStats();
        }

        // Chart configuration
        let chartDataSets = { ss: [], lms: [], icat: [], steps: [] };
        function initPruningChart() {
            const ctx = document.getElementById('pruningChart').getContext('2d');
            
            // Populate initial trace line dataset points
            chartDataSets = { ss: [62.4], lms: [83.9], icat: [63.1], steps: [0] };

            chartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: chartDataSets.steps,
                    datasets: [
                        {
                            label: 'Stereotype Score',
                            data: chartDataSets.ss,
                            borderColor: '#ef4444',
                            backgroundColor: 'rgba(239, 68, 68, 0.1)',
                            borderWidth: 2,
                            tension: 0.2
                        },
                        {
                            label: 'Accuracy (LMS)',
                            data: chartDataSets.lms,
                            borderColor: '#10b981',
                            backgroundColor: 'rgba(16, 185, 129, 0.1)',
                            borderWidth: 2,
                            tension: 0.2
                        },
                        {
                            label: 'iCAT Alignment',
                            data: chartDataSets.icat,
                            borderColor: '#8b5cf6',
                            backgroundColor: 'rgba(139, 92, 246, 0.15)',
                            fill: true,
                            borderWidth: 2.5,
                            tension: 0.2
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { color: '#94a3b8', font: { size: 10 } }
                        }
                    },
                    scales: {
                        x: {
                            grid: { color: '#1e293b' },
                            ticks: { color: '#94a3b8', font: { size: 9 } },
                            title: { display: true, text: 'Evaluation Steps / Modifications', color: '#64748b', font: { size: 10 } }
                        },
                        y: {
                            grid: { color: '#1e293b' },
                            ticks: { color: '#94a3b8', font: { size: 9 } },
                            min: 40,
                            max: 100
                        }
                    }
                }
            });
        }

        // Live-update alignment performance metrics
        function updatePruningChartData(ss, lms, icat) {
            if (!chartInstance) return;

            // Generate subsequent step tracking
            const nextStep = chartDataSets.steps[chartDataSets.steps.length - 1] + 1;
            
            // Limit trajectory window length
            if (chartDataSets.steps.length > 10) {
                chartDataSets.steps.shift();
                chartDataSets.ss.shift();
                chartDataSets.lms.shift();
                chartDataSets.icat.shift();
            }

            chartDataSets.steps.push(nextStep);
            chartDataSets.ss.push(ss);
            chartDataSets.lms.push(lms);
            chartDataSets.icat.push(icat);

            chartInstance.update();
        }

        // Virtual Code Cell Executor inside IDE Pane
        function runNotebookCell(cellId) {
            const output = document.getElementById(`cell-output-${cellId}`);
            const btn = document.getElementById(`run-btn-${cellId}`);

            output.classList.remove('hidden');
            output.innerHTML = `
                <div class="flex items-center space-x-2 text-slate-400">
                    <span class="w-3 h-3 border-2 border-indigo-400 border-t-transparent animate-spin rounded-full"></span>
                    <span>Compiling runtime modules...</span>
                </div>
            `;
            btn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> Executing`;
            btn.disabled = true;

            setTimeout(() => {
                btn.innerHTML = `<i class="fa-solid fa-check mr-1 text-emerald-400"></i> Executed`;
                btn.className = "px-3 py-1 bg-emerald-600/20 text-emerald-400 border border-emerald-500/30 rounded-lg transition duration-200";
                
                if (cellId === 1) {
                    output.innerHTML = `
                        <div class="text-slate-500"># Output:</div>
                        <div class="text-emerald-400">✔ Done! Successfully gathered and unpacked repository configurations.</div>
                        <div class="text-slate-400">Downloaded PyTorch (version 2.4.1), Seaborn charts library, and huggingface_hub assets successfully.</div>
                    `;
                } else if (cellId === 2) {
                    output.innerHTML = `
                        <div class="text-slate-500"># Output:</div>
                        <div class="text-slate-400">Loading checkpoint model: <span class="text-indigo-400">"distilbert-base-uncased"</span></div>
                        <div class="text-slate-400">Generating target tensors config parameters... <span class="text-emerald-400 font-bold">SUCCESS</span></div>
                        <div class="text-slate-500 text-[11px] font-mono mt-1">Found 12 Encoder blocks, Layer attention metrics extraction pipeline is armed.</div>
                    `;
                } else if (cellId === 3) {
                    const preset = winogradPresets.find(p => p.id === selectedPresetId);
                    const sentence = currentSentenceVariant === 'A' ? preset.sentenceA : preset.sentenceB;
                    output.innerHTML = `
                        <div class="text-slate-500"># Output:</div>
                        <div class="text-slate-400"><span class="text-slate-500">Processing input string:</span> "${sentence}"</div>
                        <div class="text-slate-400">Num layer weights parsed: <span class="text-violet-400 font-bold">12</span></div>
                        <div class="text-slate-400">Layer 1 attention size dimensions: <span class="text-emerald-400 font-mono">torch.Size([1, 12, 16, 16])</span></div>
                        <div class="text-indigo-400 font-semibold mt-1">✔ Real-time visualization updated! Transitioning back to the Coreference Sandbox tab is recommended.</div>
                    `;
                    // Auto switch back to playground to show visual impact
                    setTimeout(() => switchTab('playground'), 1200);
                }
            }, 1500);
        }

        // Fill recommended sentence query
        function fillAssistantQuery(txt) {
            document.getElementById('ai-input-sentence').value = txt;
        }

        // Main function to run live Gemini API calls for custom token attention mapping
        async function executeAiAnalysis() {
            const textInput = document.getElementById('ai-input-sentence').value.trim();
            if (!textInput) {
                alert("Please write or select a sentence to query the attention analyzer.");
                return;
            }

            const loader = document.getElementById('ai-output-loader');
            const emptyState = document.getElementById('ai-output-empty-state');
            const details = document.getElementById('ai-output-details');
            const submitBtn = document.getElementById('submit-ai-analysis');
            const retryHint = document.getElementById('ai-loader-retry-hint');

            // Toggle visual screens
            emptyState.classList.add('hidden');
            details.classList.add('hidden');
            loader.classList.remove('hidden');
            submitBtn.disabled = true;
            submitBtn.innerHTML = `<i class="fa-solid fa-spinner animate-spin mr-2"></i> Running Analytical Probes...`;

            // Prompt template forcing a clean, compliant structured JSON schema
            const systemPrompt = `You are a state-of-the-art Transformer Self-Attention & Bias Analyzer.
Your task is to analyze the user's sentence and estimate structural tokenization attention weights, coreference details, and potential demographic biases.

Format your response STRICTLY as a single, valid JSON object with the following schema:
{
  "tokens": ["word1", "word2", "word3", ...],
  "pronoun": "the target pronoun evaluated, like 'she', 'he', 'they', or 'it'",
  "coreference_explanation": "Explain how upper layers resolve context in 1-2 concise sentences.",
  "bias_assessment": "Assess hidden demographic or occupational stereotypes in the input text in 1-2 sentences.",
  "approximate_weights": [
    {"token": "word1", "weight": 0.05},
    {"token": "word2", "weight": 0.12},
    ...
  ]
}
Make sure all approximate_weights match the list of tokens and total exactly to 1.0. Align higher weights with realistic targets of the target pronoun based on sentence context. Return ONLY pure, parsable JSON.`;

            // Function for making fetch request with exponential backoff retries
            const makeFetchCall = async (retryCount = 0) => {
                // Empty string API key that operates in runtime context
                const apiKey = ""; 
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

                const payload = {
                    contents: [{ parts: [{ text: textInput }] }],
                    generationConfig: {
                        responseMimeType: "application/json",
                        responseSchema: {
                            type: "OBJECT",
                            properties: {
                                "tokens": {
                                    "type": "ARRAY",
                                    "items": { "type": "STRING" }
                                },
                                "pronoun": { "type": "STRING" },
                                "coreference_explanation": { "type": "STRING" },
                                "bias_assessment": { "type": "STRING" },
                                "approximate_weights": {
                                    "type": "ARRAY",
                                    "items": {
                                        "type": "OBJECT",
                                        "properties": {
                                            "token": { "type": "STRING" },
                                            "weight": { "type": "NUMBER" }
                                        },
                                        "required": ["token", "weight"]
                                    }
                                }
                            },
                            "required": ["tokens", "pronoun", "coreference_explanation", "bias_assessment", "approximate_weights"]
                        }
                    },
                    systemInstruction: {
                        parts: [{ text: systemPrompt }]
                    }
                };

                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (response.status === 429 && retryCount < 4) {
                        retryHint.classList.remove('hidden');
                        const delay = Math.pow(2, retryCount) * 1000 + Math.random() * 500;
                        await new Promise(resolve => setTimeout(resolve, delay));
                        return await makeFetchCall(retryCount + 1);
                    }

                    if (!response.ok) {
                        throw new Error(`HTTP Error Status: ${response.status}`);
                    }

                    const result = await response.json();
                    return result;

                } catch (err) {
                    if (retryCount < 4) {
                        retryHint.classList.remove('hidden');
                        const delay = Math.pow(2, retryCount) * 1000 + Math.random() * 500;
                        await new Promise(resolve => setTimeout(resolve, delay));
                        return await makeFetchCall(retryCount + 1);
                    }
                    throw err;
                }
            };

            try {
                const result = await makeFetchCall();
                const jsonText = result?.candidates?.[0]?.content?.parts?.[0]?.text;
                if (!jsonText) throw new Error("Could not extract generated text from API response");

                const data = JSON.parse(jsonText);
                renderAiAnalysisResult(data);

            } catch (error) {
                console.warn("Gemini API direct call failed, falling back to client-side local analyzer:", error);
                // Fallback simulation in case API limit exceeded or offline
                const fallbackData = computeClientFallbackAnalysis(textInput);
                renderAiAnalysisResult(fallbackData);
            } finally {
                loader.classList.add('hidden');
                retryHint.classList.add('hidden');
                details.classList.remove('hidden');
                submitBtn.disabled = false;
                submitBtn.innerHTML = `<i class="fa-solid fa-paper-plane mr-2"></i> Submit and Generate Attention Map`;
            }
        }

        // Render weights and profiles from prompt call
        function renderAiAnalysisResult(data) {
            document.getElementById('ai-res-explanation').innerText = data.coreference_explanation;
            document.getElementById('ai-res-bias').innerText = data.bias_assessment;

            const barsContainer = document.getElementById('ai-res-attention-bars');
            barsContainer.innerHTML = '';

            const weights = data.approximate_weights || [];
            weights.forEach(w => {
                const row = document.createElement('div');
                row.className = "space-y-1";

                const isPronoun = w.token.toLowerCase() === (data.pronoun || '').toLowerCase();
                const barColor = isPronoun ? 'bg-indigo-500' : 'bg-indigo-500/40';

                row.innerHTML = `
                    <div class="flex items-center justify-between font-mono text-[10px]">
                        <span class="${isPronoun ? 'text-indigo-400 font-bold' : 'text-slate-400'}">"${w.token}"</span>
                        <span class="text-slate-400 font-medium">${(w.weight * 100).toFixed(1)}%</span>
                    </div>
                    <div class="w-full bg-slate-950 rounded-full h-1.5 overflow-hidden border border-slate-850">
                        <div class="${barColor} h-1.5 rounded-full" style="width: ${w.weight * 100}%"></div>
                    </div>
                `;
                barsContainer.appendChild(row);
            });
        }

        // Generate client-side structural logic if standard web limits trigger
        function computeClientFallbackAnalysis(sentence) {
            const tokens = sentence.split(/\s+/).map(t => t.replace(/[.,\/#!$%\^&\*;:{}=\-_`~()]/g,""));
            let pronoun = "it";
            if (sentence.toLowerCase().includes("she")) pronoun = "she";
            else if (sentence.toLowerCase().includes("he")) pronoun = "he";
            else if (sentence.toLowerCase().includes("they")) pronoun = "they";

            // Find probable candidates
            let candidate1 = tokens[1] || "Target A";
            let candidate2 = tokens[4] || "Target B";

            const corefExp = `Upper layer representations dynamically bind the coreference relation. The pronoun "${pronoun}" has shifted its multi-head attention focus heavily onto "${candidate1}" as its semantic referent within this clause structure.`;
            const biasExp = sentence.toLowerCase().includes("doctor") || sentence.toLowerCase().includes("developer") 
                ? "Demographic profiling detected. The system demonstrates typical pre-training gender-occupational alignment metrics on typical bias testing templates."
                : "No severe occupational stereotyping flag was activated. Attention distribution appears structurally sound and balanced.";

            // Approximate attention weight map distribution
            const count = tokens.length;
            const approxWeights = tokens.map((tok, idx) => {
                let weight = 0.05;
                if (tok.toLowerCase() === pronoun) weight = 0.15;
                else if (tok.toLowerCase() === candidate1.toLowerCase()) weight = 0.45;
                else if (tok.toLowerCase() === candidate2.toLowerCase()) weight = 0.15;
                else {
                    weight = (0.25) / (count - 3);
                }
                return { token: tok, weight };
            });

            return {
                tokens,
                pronoun,
                coreference_explanation: corefExp,
                bias_assessment: biasExp,
                approximate_weights: approxWeights
            };
        }
    </script>
</body>
</html>
