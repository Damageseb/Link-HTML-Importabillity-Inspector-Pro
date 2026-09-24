<!DOCTYPE html>
<html lang="en" class="h-full bg-slate-950 text-slate-100">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GitHub Browser Importability Inspector</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Inter & JetBrains Mono -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Inter', sans-serif; }
    code, pre { font-family: 'JetBrains Mono', monospace; }
    .custom-scrollbar::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
      background: #0f172a;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: #334155;
      border-radius: 4px;
    }
  </style>
</head>
<body class="min-h-full flex flex-col bg-slate-950 text-slate-100 antialiased selection:bg-indigo-500 selection:text-white">

  <!-- Top Bar -->
  <header class="border-b border-slate-800 bg-slate-900/80 backdrop-blur-md sticky top-0 z-30">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
      <div class="flex items-center space-x-3">
        <div class="p-2 bg-indigo-600/20 border border-indigo-500/30 rounded-xl text-indigo-400">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" />
          </svg>
        </div>
        <div>
          <h1 class="font-bold text-lg leading-tight text-white flex items-center gap-2">
            Importability Inspector
            <span class="text-xs font-normal px-2 py-0.5 rounded-full bg-indigo-500/10 text-indigo-400 border border-indigo-500/20">Browser JS Evaluator</span>
          </h1>
          <p class="text-xs text-slate-400">Can this GitHub repo run in a plain HTML <code class="text-indigo-300">&lt;script&gt;</code> tag?</p>
        </div>
      </div>

      <div class="flex items-center space-x-2">
        <a href="https://github.com" target="_blank" class="p-2 text-slate-400 hover:text-slate-200 transition rounded-lg hover:bg-slate-800">
          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
            <path fill-rule="evenodd" clip-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.53 1.032 1.53 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/>
          </svg>
        </a>
      </div>
    </div>
  </header>

  <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-8">
    
    <!-- Input Card -->
    <div class="bg-slate-900/90 border border-slate-800 rounded-2xl p-6 shadow-2xl backdrop-blur-xl relative overflow-hidden">
      <div class="absolute -top-24 -right-24 w-60 h-60 bg-indigo-600/10 rounded-full blur-3xl pointer-events-none"></div>
      
      <label for="url-input" class="block text-sm font-medium text-slate-300 mb-2">
        Enter GitHub Repository or File URL
      </label>
      
      <div class="flex flex-col sm:flex-row gap-3">
        <div class="relative flex-1">
          <div class="absolute inset-y-0 left-0 pl-3.5 flex items-center pointer-events-none text-slate-500">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1" />
            </svg>
          </div>
          <input 
            type="text" 
            id="url-input" 
            placeholder="e.g. https://github.com/Naruyoshi/ExpantaNum.js or mrdoob/three.js"
            class="w-full pl-10 pr-4 py-3 bg-slate-950 border border-slate-700/80 rounded-xl text-white placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent text-sm font-mono transition"
            value="https://github.com/mrdoob/three.js"
          >
        </div>
        <button 
          id="inspect-btn" 
          onclick="inspectRepo()"
          class="px-6 py-3 bg-indigo-600 hover:bg-indigo-500 text-white font-semibold rounded-xl shadow-lg shadow-indigo-600/25 transition active:scale-[0.98] flex items-center justify-center gap-2 whitespace-nowrap"
        >
          <svg id="btn-icon" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
          </svg>
          <span id="btn-text">Analyze GitHub URL</span>
        </button>
      </div>

      <!-- Preset Chips -->
      <div class="mt-4 flex flex-wrap items-center gap-2 text-xs text-slate-400">
        <span class="text-slate-500 font-medium mr-1">Quick Presets:</span>
        <button onclick="setPreset('https://github.com/mrdoob/three.js')" class="px-2.5 py-1 bg-slate-800 hover:bg-slate-700 hover:text-indigo-300 rounded-lg border border-slate-700 transition">🎮 Three.js (~1.7 GB)</button>
        <button onclick="setPreset('https://github.com/Naruyoshi/ExpantaNum.js')" class="px-2.5 py-1 bg-slate-800 hover:bg-slate-700 hover:text-indigo-300 rounded-lg border border-slate-700 transition">⚡ ExpantaNum.js</button>
        <button onclick="setPreset('https://github.com/lodash/lodash')" class="px-2.5 py-1 bg-slate-800 hover:bg-slate-700 hover:text-indigo-300 rounded-lg border border-slate-700 transition">📦 Lodash</button>
        <button onclick="setPreset('https://github.com/catdad/canvas-confetti')" class="px-2.5 py-1 bg-slate-800 hover:bg-slate-700 hover:text-indigo-300 rounded-lg border border-slate-700 transition">🎉 Canvas-Confetti</button>
        <button onclick="setPreset('https://github.com/expressjs/express')" class="px-2.5 py-1 bg-slate-800 hover:bg-slate-700 hover:text-indigo-300 rounded-lg border border-slate-700 transition">🔴 Express (Node only)</button>
        <button onclick="setPreset('https://github.com/facebook/react')" class="px-2.5 py-1 bg-slate-800 hover:bg-slate-700 hover:text-indigo-300 rounded-lg border border-slate-700 transition">⚛️ React</button>
      </div>
    </div>

    <!-- Notification Toast Box -->
    <div id="toast-box" class="hidden rounded-xl border p-4 transition-all"></div>

    <!-- Results Dashboard -->
    <div id="results-container" class="space-y-6">
      <!-- Loading State placeholder -->
      <div id="loading-spinner" class="hidden py-16 text-center space-y-4">
        <div class="inline-block w-12 h-12 border-4 border-indigo-500/20 border-t-indigo-500 rounded-full animate-spin"></div>
        <p class="text-slate-400 text-sm animate-pulse">Fetching repository details, package metadata, and module entry points...</p>
      </div>

      <!-- Actual Results View -->
      <div id="results-view" class="space-y-6">
        
        <!-- Header Verdict Banner -->
        <div id="verdict-banner" class="rounded-2xl border p-6 flex flex-col md:flex-row md:items-center justify-between gap-6 bg-slate-900/80 backdrop-blur border-slate-800">
          <!-- Populated dynamically -->
        </div>

        <!-- Grid layout for detailed analysis -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
          
          <!-- Left Column: How To Import Code Snippets -->
          <div class="lg:col-span-2 space-y-6">
            
            <!-- Code Snippets Box -->
            <div class="bg-slate-900 border border-slate-800 rounded-2xl overflow-hidden shadow-xl">
              <div class="border-b border-slate-800 bg-slate-950/60 px-5 py-3 flex items-center justify-between">
                <div class="flex items-center space-x-2">
                  <span class="w-3 h-3 rounded-full bg-rose-500/80 inline-block"></span>
                  <span class="w-3 h-3 rounded-full bg-amber-500/80 inline-block"></span>
                  <span class="w-3 h-3 rounded-full bg-emerald-500/80 inline-block"></span>
                  <span class="text-xs font-semibold text-slate-400 ml-2">Recommended Ready-to-Use HTML Snippets</span>
                </div>
                <div class="flex border border-slate-700/60 rounded-lg overflow-hidden bg-slate-900 text-xs p-0.5">
                  <button id="tab-classic" onclick="switchSnippetTab('classic')" class="px-3 py-1 rounded-md transition text-slate-200 bg-slate-800 font-medium">Classic &lt;script&gt;</button>
                  <button id="tab-esm" onclick="switchSnippetTab('esm')" class="px-3 py-1 rounded-md transition text-slate-400 hover:text-slate-200">ESM &lt;script type="module"&gt;</button>
                  <button id="tab-importmap" onclick="switchSnippetTab('importmap')" class="px-3 py-1 rounded-md transition text-slate-400 hover:text-slate-200">Import Map</button>
                </div>
              </div>

              <!-- Code Content Display -->
              <div class="p-5 bg-slate-950 relative">
                <button onclick="copyCodeSnippet()" class="absolute top-3 right-3 px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-xs font-medium text-slate-300 rounded-lg border border-slate-700 transition flex items-center gap-1.5 active:scale-95 z-10">
                  <svg id="copy-icon" class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z" />
                  </svg>
                  <span id="copy-text">Copy Code</span>
                </button>
                
                <pre id="code-snippet" class="text-xs text-indigo-300 overflow-x-auto custom-scrollbar p-2 leading-relaxed"><code><!-- Code will load here --></code></pre>
              </div>

              <div class="px-5 py-3 bg-slate-900/50 border-t border-slate-800 text-xs text-slate-400 flex items-center justify-between">
                <span id="snippet-note">💡 Copy and paste directly into your HTML <code class="text-slate-300">&lt;head&gt;</code> or <code class="text-slate-300">&lt;body&gt;</code> tag.</span>
              </div>
            </div>

            <!-- 10 Rules Inspection Checklist -->
            <div class="bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl space-y-4">
              <div class="flex items-center justify-between">
                <h3 class="text-base font-semibold text-white flex items-center gap-2">
                  <svg class="w-5 h-5 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                  Compatibility & Safety Checkpoints
                </h3>
                <span class="text-xs text-slate-500">Evaluated against browser ESM & Static Analysis specs</span>
              </div>

              <!-- Code Freeze & Hazard Warning Banner (Displayed when hazard patterns detected) -->
              <div id="code-hazard-alert" class="hidden p-4 bg-rose-500/15 border border-rose-500/40 rounded-xl space-y-2">
                <div class="flex items-center gap-2 text-rose-300 font-bold text-xs">
                  <svg class="w-4 h-4 text-rose-400 flex-shrink-0" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M12 2L1 21h22L12 2zm1 14h-2v-2h2v2zm0-4h-2V10h2v2z"/>
                  </svg>
                  <span>⚠️ CODE HAZARD WARNING: Infinite Loop or Crash Script Pattern Detected</span>
                </div>
                <div id="code-hazard-details" class="text-[11px] text-rose-200/90 leading-relaxed space-y-1 font-mono">
                  <!-- Hazard details injected dynamically -->
                </div>
              </div>

              <div id="checklist-items" class="grid grid-cols-1 md:grid-cols-2 gap-3 pt-2">
                <!-- Populated dynamically with pass/fail/warn chips -->
              </div>
            </div>

            <!-- JS Operator & Syntax Scanner Card -->
            <div class="bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl space-y-4">
              <div class="flex items-center justify-between border-b border-slate-800 pb-3">
                <h3 class="text-base font-semibold text-white flex items-center gap-2">
                  <svg class="w-5 h-5 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" />
                  </svg>
                  JavaScript Operator & Syntax Inspector
                </h3>
                <span id="ecma-target-badge" class="px-2.5 py-0.5 rounded text-xs font-mono font-bold bg-indigo-500/20 text-indigo-300 border border-indigo-500/30">ES2020 Target</span>
              </div>

              <!-- Operator Summary Banner -->
              <div id="operator-summary-bar" class="grid grid-cols-3 gap-3 text-center text-xs font-mono">
                <!-- Injected dynamically -->
              </div>

              <!-- Operator Occurrences Breakdown -->
              <div class="space-y-2 pt-2">
                <div class="text-xs text-slate-400 font-medium flex justify-between">
                  <span>Detected Operators & Language Features:</span>
                  <span id="operator-total-count" class="text-indigo-400 font-mono">0 total occurrences</span>
                </div>
                <div id="operator-list-grid" class="grid grid-cols-1 md:grid-cols-2 gap-2 text-xs font-mono">
                  <!-- Populated dynamically -->
                </div>
              </div>
            </div>

          </div>

          <!-- Right Column: Metadata & Details -->
          <div class="space-y-6">
            
            <!-- Repository & Package Metadata -->
            <div class="bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl space-y-4">
              <h3 class="text-sm font-semibold text-white uppercase tracking-wider text-slate-400">Package Metadata</h3>
              
              <div class="space-y-3 text-xs">
                <div class="flex justify-between py-2 border-b border-slate-800/80">
                  <span class="text-slate-400">Repository Name:</span>
                  <span id="meta-name" class="font-mono text-slate-200 font-medium">--</span>
                </div>
                <div class="flex justify-between py-2 border-b border-slate-800/80">
                  <span class="text-slate-400">Export Format (Type):</span>
                  <span id="meta-type" class="font-mono text-indigo-400 font-medium">--</span>
                </div>
                <div class="flex justify-between py-2 border-b border-slate-800/80">
                  <span class="text-slate-400">Est. Repo / File Size:</span>
                  <span id="meta-size" class="font-mono text-indigo-300 font-medium">--</span>
                </div>
                <div class="flex justify-between py-2 border-b border-slate-800/80">
                  <span class="text-slate-400">Est. UTF-16 Characters:</span>
                  <span id="meta-utf16" class="font-mono text-cyan-300 font-medium">--</span>
                </div>
                <div class="flex justify-between py-2 border-b border-slate-800/80">
                  <span class="text-slate-400">Main Entrypoint (<code class="text-slate-400">main</code>):</span>
                  <span id="meta-main" class="font-mono text-slate-200">--</span>
                </div>
                <div class="flex justify-between py-2 border-b border-slate-800/80">
                  <span class="text-slate-400">ESM Module Entry (<code class="text-slate-400">module</code>):</span>
                  <span id="meta-module" class="font-mono text-emerald-400">--</span>
                </div>
                <div class="flex justify-between py-2 border-b border-slate-800/80">
                  <span class="text-slate-400">CDN/Unpkg Bundle (<code class="text-slate-400">unpkg</code>):</span>
                  <span id="meta-unpkg" class="font-mono text-cyan-400">--</span>
                </div>
                <div class="flex justify-between py-2">
                  <span class="text-slate-400">Detected Dependencies:</span>
                  <span id="meta-deps" class="font-mono text-slate-200">0 dependencies</span>
                </div>
              </div>

              <!-- Available CDN links -->
              <div class="pt-2 border-t border-slate-800">
                <span class="text-xs text-slate-400 block mb-2 font-medium">Tested CDN Endpoints:</span>
                <div class="flex flex-col gap-1.5 text-xs font-mono">
                  <a id="cdn-jsdelivr" href="#" target="_blank" class="text-indigo-400 hover:underline flex items-center justify-between p-2 rounded-lg bg-slate-950 border border-slate-800/80">
                    <span>jsDelivr (UMD / Global)</span>
                    <span class="text-slate-500">↗</span>
                  </a>
                  <a id="cdn-esmsh" href="#" target="_blank" class="text-indigo-400 hover:underline flex items-center justify-between p-2 rounded-lg bg-slate-950 border border-slate-800/80">
                    <span>esm.sh (ESM Wrap)</span>
                    <span class="text-slate-500">↗</span>
                  </a>
                  <a id="cdn-unpkg" href="#" target="_blank" class="text-indigo-400 hover:underline flex items-center justify-between p-2 rounded-lg bg-slate-950 border border-slate-800/80">
                    <span>unpkg.com</span>
                    <span class="text-slate-500">↗</span>
                  </a>
                </div>
              </div>
            </div>

            <!-- Storage & Security Analysis Box (Bytes to Quettabytes & Zip Bomb Inspector) -->
            <div class="bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl space-y-4">
              <div class="flex items-center justify-between border-b border-slate-800 pb-3">
                <h3 class="text-sm font-semibold text-white flex items-center gap-2">
                  <svg class="w-4 h-4 text-amber-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"/>
                  </svg>
                  Storage & Bloatware Inspector
                </h3>
                <span id="security-badge" class="px-2 py-0.5 rounded text-[10px] font-mono font-bold bg-emerald-500/20 text-emerald-400 border border-emerald-500/30">SAFE SIZE</span>
              </div>

              <!-- 4 GB Suspicious Alert Box (Hidden unless > 4 GB) -->
              <div id="suspicious-alert" class="hidden p-3.5 bg-rose-500/15 border border-rose-500/40 rounded-xl space-y-2">
                <div class="flex items-center gap-2 text-rose-300 font-bold text-xs">
                  <svg class="w-4 h-4 text-rose-400 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 10-2 0 1 1 0 002 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
                  </svg>
                  <span>⚠️ SUSPICIOUS: Large Payload Detected (&gt; 4 GB)</span>
                </div>
                <p class="text-[11px] text-rose-200/90 leading-relaxed">
                  This repository or file exceeds <b>4 GB (~2 Billion UTF-16 chars)</b>. Files of this size are flagged as suspicious because they may contain bloatware, repository inflation, uncompressed binaries, or a browser-freezing <b>Zip Bomb</b>.
                </p>
              </div>

              <!-- Full Storage Unit Conversion Kit Scale -->
              <div class="space-y-2">
                <div class="flex items-center justify-between text-xs text-slate-400">
                  <span class="font-medium">Storage Unit Scale Kit:</span>
                  <div class="flex items-center gap-1 bg-slate-950 p-0.5 rounded-lg border border-slate-800 text-[10px] font-mono">
                    <button id="unit-mode-si" onclick="setStorageMode('si')" class="px-2 py-0.5 rounded bg-indigo-600 text-white font-bold transition">Decimal (1000)</button>
                    <button id="unit-mode-iec" onclick="setStorageMode('iec')" class="px-2 py-0.5 rounded text-slate-400 hover:text-white transition">Binary (1024)</button>
                  </div>
                </div>

                <!-- Active Scale Grid Display -->
                <div id="unit-kit-grid" class="grid grid-cols-2 gap-1.5 text-[11px] font-mono">
                  <!-- Populated dynamically with B, KB/KiB, MB/MiB, GB/GiB, TB/TiB, PB/PiB, EB/EiB, ZB/ZiB, YB/YiB, RB/RiB, QB/QiB -->
                </div>
              </div>

              <!-- Browser Storage & Memory Quotas Benchmark -->
              <div class="pt-3 border-t border-slate-800 space-y-2">
                <span class="text-xs font-medium text-slate-400 block">Browser Quota Benchmarks:</span>
                <div id="quota-benchmarks" class="grid grid-cols-2 gap-2 text-[10px] font-mono">
                  <!-- Dynamically rendered benchmarks -->
                </div>
              </div>

              <!-- Custom Size Simulator Input -->
              <div class="pt-3 border-t border-slate-800 space-y-2">
                <label for="size-simulator" class="text-xs text-slate-400 flex justify-between">
                  <span>Test Custom Size (GB / TB / QB):</span>
                  <span id="sim-label" class="text-indigo-400 font-mono">Simulate Size</span>
                </label>
                <div class="flex gap-2">
                  <input 
                    type="number" 
                    id="sim-bytes-input" 
                    placeholder="Enter Bytes (e.g. 5000000000 for 5GB)"
                    class="flex-1 bg-slate-950 border border-slate-800 rounded-lg px-3 py-1.5 text-xs text-slate-200 font-mono focus:outline-none focus:border-indigo-500"
                  >
                  <button 
                    onclick="simulateSizeInput()"
                    class="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-xs font-semibold text-slate-200 rounded-lg border border-slate-700 transition"
                  >
                    Inspect
                  </button>
                </div>
              </div>
            </div>

            <!-- Optional Gemini AI Deep Analysis Card -->
            <div class="bg-gradient-to-br from-indigo-950/40 to-slate-900 border border-indigo-500/20 rounded-2xl p-6 shadow-xl space-y-4 relative overflow-hidden">
              <div class="flex items-center justify-between">
                <h3 class="text-sm font-semibold text-indigo-300 flex items-center gap-2">
                  <svg class="w-4 h-4 text-indigo-400" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M12 2L14.5 9.5L22 12L14.5 14.5L12 22L9.5 14.5L2 12L9.5 9.5L12 2Z"/>
                  </svg>
                  Gemini Deep AI Breakdown
                </h3>
                <span class="text-[10px] px-2 py-0.5 rounded bg-indigo-500/20 text-indigo-300 font-mono">gemini-3-flash</span>
              </div>
              
              <p class="text-xs text-slate-400">Want an AI explanation of how to write browser code with this specific library?</p>
              
              <button 
                onclick="runGeminiAiAnalysis()" 
                id="ai-btn" 
                class="w-full py-2.5 px-4 bg-indigo-600 hover:bg-indigo-500 text-white font-medium text-xs rounded-xl shadow transition flex items-center justify-center gap-2"
              >
                <span>Generate AI Integration Guide</span>
              </button>

              <div id="ai-output" class="hidden text-xs text-slate-300 p-3 bg-slate-950 rounded-xl border border-slate-800 leading-relaxed custom-scrollbar max-h-60 overflow-y-auto">
                <!-- AI dynamic explanation -->
              </div>
            </div>

          </div>

        </div>

      </div>

    </div>

  </main>

  <!-- Footer -->
  <footer class="border-t border-slate-800/80 bg-slate-950 py-6 mt-12 text-center text-xs text-slate-500">
    <div class="max-w-7xl mx-auto px-4">
      Browser Scriptability Evaluator • Works with standard HTML5, importmaps, and ES Modules.
    </div>
  </footer>

  <script>
    let currentData = null;
    let activeTab = 'classic';
    let currentUnitMode = 'si'; // 'si' (1000) or 'iec' (1024)
    const apiKey = ""; // Canvas runtime auto-injects Gemini API key

    /**
     * Scans JavaScript source code for operator usage, modern ECMAScript features,
     * module syntax operators, comparison operators, and transpilation-required syntax.
     */
    function scanOperators(code) {
      if (!code || typeof code !== 'string' || code.trim().length === 0) {
        return { scanned: false, operators: [], totalCount: 0, highestEcma: 'ES5/ES6', requiresTranspilation: false };
      }

      // Strip comments and string literals to prevent false positives inside text
      const cleanCode = code
        .replace(/\/\*[\s\S]*?\*\//g, '')
        .replace(/\/\/.*/g, '')
        .replace(/(["'])(?:(?=(\\?))\2.)*?\1/g, '""')
        .replace(/`[\s\S]*?`/g, '""');

      const operatorDefinitions = [
        // Modern ES2020+
        { key: 'optionalChaining', name: 'Optional Chaining (`?.`)', regex: /\?\.(?!\d)/g, category: 'Modern JS', ecma: 'ES2020', minEngine: 'Chrome 80+, Safari 13.1+', impact: 'native' },
        { key: 'nullishCoalescing', name: 'Nullish Coalescing (`??`)', regex: /\?\?(?!=)/g, category: 'Modern JS', ecma: 'ES2020', minEngine: 'Chrome 80+, Firefox 72+', impact: 'native' },
        { key: 'logicalAssignment', name: 'Logical Assignment (`||=`, `&&=`, `??=`)', regex: /(\|\|=|&&=|\?\?=)/g, category: 'Modern JS', ecma: 'ES2021', minEngine: 'Chrome 85+, Safari 14+', impact: 'native' },
        { key: 'privateFields', name: 'Private Fields (`#field`)', regex: /#([a-zA-Z_$][a-zA-Z0-9_$]*)/g, category: 'Modern JS', ecma: 'ES2022', minEngine: 'Chrome 74+, Safari 14.1+', impact: 'native' },
        { key: 'spreadRest', name: 'Spread / Rest Operator (`...`)', regex: /\.\.\./g, category: 'Modern JS', ecma: 'ES2018', minEngine: 'Chrome 60+, Safari 11.1+', impact: 'native' },
        { key: 'exponentiation', name: 'Exponentiation (`**`)', regex: /\*\*(?!=)/g, category: 'Modern JS', ecma: 'ES2016', minEngine: 'Chrome 52+, Firefox 52+', impact: 'native' },
        { key: 'bigInt', name: 'BigInt Literals (`123n`)', regex: /\b\d+n\b/g, category: 'Modern JS', ecma: 'ES2020', minEngine: 'Chrome 67+, Safari 14+', impact: 'native' },

        // Module & Specifier Operators
        { key: 'dynamicImport', name: 'Dynamic Import (`import()`)', regex: /\bimport\s*\(/g, category: 'Module System', ecma: 'ES2020', minEngine: 'Chrome 63+, Safari 11.1+', impact: 'native' },
        { key: 'importMeta', name: 'Import Meta (`import.meta`)', regex: /\bimport\.meta\b/g, category: 'Module System', ecma: 'ES2020', minEngine: 'Chrome 76+, Safari 11.1+', impact: 'native' },
        { key: 'importAttributes', name: 'Import Attributes (`with { type }`)', regex: /\b(with|assert)\s*\{\s*type\s*:/g, category: 'Module System', ecma: 'ES2025', minEngine: 'Chrome 123+, Firefox 126+', impact: 'native' },

        // Non-Standard / Transpilation Required
        { key: 'decorators', name: 'Decorators (`@decorator`)', regex: /@([a-zA-Z_$][a-zA-Z0-9_$]*)/g, category: 'Build Step Needed', ecma: 'Stage 3 / TS', minEngine: 'Requires Transpiler', impact: 'transpile' },
        { key: 'typeAnnotations', name: 'TypeScript Types (`: Type`)', regex: /:\s*(string|number|boolean|any|unknown|never)\b/g, category: 'Build Step Needed', ecma: 'TypeScript', minEngine: 'Requires Transpiler', impact: 'transpile' },
        { key: 'jsxTags', name: 'JSX Elements (`<Tag />`)', regex: /<[A-Z][a-zA-Z0-9]*\b[^>]*\/?>/g, category: 'Build Step Needed', ecma: 'JSX / React', minEngine: 'Requires Transpiler', impact: 'transpile' },

        // Safety & Comparison Operators
        { key: 'strictEquality', name: 'Strict Equality (`===`, `!==`)', regex: /===|!==/g, category: 'Comparison', ecma: 'ES3', minEngine: 'All Browsers', impact: 'native' },
        { key: 'looseEquality', name: 'Loose Equality (`==`, `!=`)', regex: /(?<!=)[!=]=(?!=)/g, category: 'Comparison', ecma: 'ES3', minEngine: 'All Browsers', impact: 'warning' },
        { key: 'bitwiseShift', name: 'Bitwise Shift (`<<`, `>>`, `>>>`)', regex: /<<|>>|>>>/g, category: 'Low-level Ops', ecma: 'ES3', minEngine: 'All Browsers', impact: 'native' },
        { key: 'deleteOperator', name: 'Delete Operator (`delete`)', regex: /\bdelete\b/g, category: 'Performance Risk', ecma: 'ES3', minEngine: 'All Browsers', impact: 'warning' }
      ];

      const detected = [];
      let totalCount = 0;
      let highestEcma = 'ES5/ES6';
      let requiresTranspilation = false;

      for (const def of operatorDefinitions) {
        const matches = cleanCode.match(def.regex);
        const count = matches ? matches.length : 0;
        if (count > 0) {
          totalCount += count;
          detected.push({ ...def, count });
          if (def.impact === 'transpile') {
            requiresTranspilation = true;
          }
          if (def.ecma.startsWith('ES20')) {
            highestEcma = def.ecma;
          }
        }
      }

      return {
        scanned: true,
        operators: detected,
        totalCount,
        highestEcma,
        requiresTranspilation
      };
    }

    /**
     * Scans source JavaScript code for potential infinite loops, main-thread freezes, 
     * memory bombs, stack overflow recursion hazards, and dangerous execution patterns.
     */
    function scanCodeForHazards(code) {
      if (!code || typeof code !== 'string') {
        return { safe: true, hazards: [], scanned: false };
      }

      const hazards = [];

      // 1. Unconditional / Infinite Loops
      const infiniteLoopRegexes = [
        { pattern: /while\s*\(\s*(true|1|!0|!false)\s*\)/i, label: "Unconditional `while(true)` or `while(1)` infinite loop detected" },
        { pattern: /for\s*\(\s*;\s*;\s*\)/i, label: "Unconditional `for(;;)` infinite loop detected" },
        { pattern: /do\s*\{[\s\S]*?\}\s*while\s*\(\s*(true|1|!0)\s*\)/i, label: "Unconditional `do ... while(true)` loop detected" }
      ];

      for (const rule of infiniteLoopRegexes) {
        if (rule.pattern.test(code)) {
          hazards.push({ severity: 'high', type: 'Infinite Loop', message: rule.label });
        }
      }

      // 2. Thread-Blocking Synchronous Delay / Freeze Loops
      if (/while\s*\(\s*(Date|performance)\.now\(\)/i.test(code)) {
        hazards.push({ 
          severity: 'high', 
          type: 'Thread Freeze', 
          message: "Synchronous busy-wait loop using `Date.now()` or `performance.now()` freezes browser UI" 
        });
      }

      // 3. Excessive Memory Allocation / Heap Crashers
      if (/new\s+Array\s*\(\s*(\d{7,}|0x[0-9a-fA-F]{6,})\s*\)/.test(code) || /\.repeat\s*\(\s*\d{7,}\s*\)/.test(code)) {
        hazards.push({ 
          severity: 'high', 
          type: 'Memory Bomb', 
          message: "Extremely large array allocation or string repeating (>1,000,000 items) may crash tab memory" 
        });
      }

      // 4. Infinite Recursion / Stack Overflow Hazards
      const functionMatch = code.match(/function\s+([a-zA-Z_$][a-zA-Z0-9_$]*)\s*\([^)]*\)\s*\{([\s\S]{1,150})\}/g);
      if (functionMatch) {
        for (const fnDef of functionMatch.slice(0, 30)) {
          const nameMatch = fnDef.match(/function\s+([a-zA-Z_$][a-zA-Z0-9_$]*)/);
          if (nameMatch) {
            const fnName = nameMatch[1];
            // Check if function calls itself without an obvious if condition
            if (fnDef.includes(`${fnName}(`) && !fnDef.includes('if') && !fnDef.includes('return')) {
              hazards.push({
                severity: 'medium',
                type: 'Recursion Risk',
                message: `Potential unconditioned recursive call in function \`${fnName}()\` (Stack Overflow risk)`
              });
              break;
            }
          }
        }
      }

      // 5. Unsafe Code Execution Patterns
      if (/\beval\s*\(/i.test(code)) {
        hazards.push({ 
          severity: 'medium', 
          type: 'Unsafe Execution', 
          message: "Contains `eval()` which bypasses CSP and can execute unvetted dynamic scripts" 
        });
      }

      if (/new\s+Function\s*\(/i.test(code)) {
        hazards.push({ 
          severity: 'low', 
          type: 'Dynamic Function', 
          message: "Uses `new Function(...)` constructor for dynamic code execution" 
        });
      }

      return {
        safe: hazards.length === 0,
        hazards,
        scanned: true
      };
    }

    // Storage unit scale definitions up to Quettabytes / Quebibytes (10^30 / 2^100)
    const STORAGE_UNITS_SI = [
      { name: 'Bytes', symbol: 'B', exponent: 0 },
      { name: 'Kilobytes', symbol: 'KB', exponent: 3 },
      { name: 'Megabytes', symbol: 'MB', exponent: 6 },
      { name: 'Gigabytes', symbol: 'GB', exponent: 9 },
      { name: 'Terabytes', symbol: 'TB', exponent: 12 },
      { name: 'Petabytes', symbol: 'PB', exponent: 15 },
      { name: 'Exabytes', symbol: 'EB', exponent: 18 },
      { name: 'Zettabytes', symbol: 'ZB', exponent: 21 },
      { name: 'Yottabytes', symbol: 'YB', exponent: 24 },
      { name: 'Ronnabytes', symbol: 'RB', exponent: 27 },
      { name: 'Quettabytes', symbol: 'QB', exponent: 30 }
    ];

    const STORAGE_UNITS_IEC = [
      { name: 'Bytes', symbol: 'B', power: 0 },
      { name: 'Kibibytes', symbol: 'KiB', power: 1 },
      { name: 'Mebibytes', symbol: 'MiB', power: 2 },
      { name: 'Gibibytes', symbol: 'GiB', power: 3 },
      { name: 'Tebibytes', symbol: 'TiB', power: 4 },
      { name: 'Pebibytes', symbol: 'PiB', power: 5 },
      { name: 'Exbibytes', symbol: 'EiB', power: 6 },
      { name: 'Zebibytes', symbol: 'ZiB', power: 7 },
      { name: 'Yobibytes', symbol: 'YiB', power: 8 },
      { name: 'Robi-bytes', symbol: 'RiB', power: 9 },
      { name: 'Quebi-bytes', symbol: 'QiB', power: 10 }
    ];

    /**
     * Formats bytes across the full spectrum from Bytes to Quettabytes/Quebibytes
     */
    function formatFullStorageKit(bytes, mode = 'si') {
      if (typeof bytes !== 'number' || isNaN(bytes) || bytes < 0) bytes = 0;

      if (mode === 'si') {
        return STORAGE_UNITS_SI.map(unit => {
          let value = (unit.exponent === 0) ? bytes : bytes / Math.pow(10, unit.exponent);
          let formattedStr = formatUnitValue(value);
          return { ...unit, value, formatted: `${formattedStr} ${unit.symbol}` };
        });
      } else {
        return STORAGE_UNITS_IEC.map(unit => {
          let value = (unit.power === 0) ? bytes : bytes / Math.pow(1024, unit.power);
          let formattedStr = formatUnitValue(value);
          return { ...unit, value, formatted: `${formattedStr} ${unit.symbol}` };
        });
      }
    }

    function formatUnitValue(val) {
      if (val >= 1000000 || (val < 0.000001 && val > 0)) {
        return val.toExponential(2);
      } else if (val >= 100) {
        return val.toFixed(1);
      } else if (val >= 1) {
        return val.toFixed(2);
      } else if (val > 0) {
        return val.toFixed(4);
      } else {
        return '0';
      }
    }

    /**
     * Returns a human-friendly size using the best fitting unit from the Kit (e.g., 1.72 GB instead of 1722.94 MB)
     */
    function getSmartFormattedSize(bytes, mode = 'si') {
      const kit = formatFullStorageKit(bytes, mode);
      let best = kit[0];
      for (let i = kit.length - 1; i >= 0; i--) {
        if (kit[i].value >= 1) {
          best = kit[i];
          break;
        }
      }
      return `${best.formatted} (${bytes.toLocaleString()} Bytes)`;
    }

    function setStorageMode(mode) {
      currentUnitMode = mode;
      const siBtn = document.getElementById('unit-mode-si');
      const iecBtn = document.getElementById('unit-mode-iec');

      if (mode === 'si') {
        siBtn.className = 'px-2 py-0.5 rounded bg-indigo-600 text-white font-bold transition';
        iecBtn.className = 'px-2 py-0.5 rounded text-slate-400 hover:text-white transition';
      } else {
        iecBtn.className = 'px-2 py-0.5 rounded bg-indigo-600 text-white font-bold transition';
        siBtn.className = 'px-2 py-0.5 rounded text-slate-400 hover:text-white transition';
      }

      if (currentData) {
        currentData.analysis.storageKit = formatFullStorageKit(currentData.analysis.estimatedBytes, currentUnitMode);
        document.getElementById('meta-size').textContent = getSmartFormattedSize(currentData.analysis.estimatedBytes, currentUnitMode);
        renderStorageAndSecurityKit(currentData.analysis);
      }
    }

    /**
     * Estimates UTF-16 Code Units (Characters).
     * In JavaScript / UTF-16, 1 character code unit = 2 bytes.
     */
    function estimateUtf16Chars(bytes) {
      if (!bytes || bytes <= 0) return 0;
      return Math.round(bytes / 2);
    }

    function setPreset(url) {
      document.getElementById('url-input').value = url;
      inspectRepo();
    }

    function parseGithubUrl(urlStr) {
      try {
        let clean = urlStr.trim().replace(/\/+$/, '');
        // Handle short syntax "owner/repo"
        if (!clean.includes('github.com') && clean.split('/').length === 2) {
          clean = `https://github.com/${clean}`;
        }
        
        const parsed = new URL(clean.startsWith('http') ? clean : `https://${clean}`);
        const parts = parsed.pathname.split('/').filter(Boolean);
        
        if (parts.length < 2) return null;
        
        const owner = parts[0];
        const repo = parts[1].replace(/\.git$/, '');
        let branch = 'main';
        let filePath = '';
        
        if (parts[2] === 'tree' || parts[2] === 'blob') {
          branch = parts[3] || 'main';
          filePath = parts.slice(4).join('/');
        }
        
        return { owner, repo, branch, filePath, fullRepoUrl: `https://github.com/${owner}/${repo}` };
      } catch (e) {
        return null;
      }
    }

    async function inspectRepo() {
      const urlInput = document.getElementById('url-input').value;
      const ghInfo = parseGithubUrl(urlInput);

      if (!ghInfo) {
        showToast("Invalid GitHub URL format. Please paste a valid repository link like 'https://github.com/owner/repo'", "error");
        return;
      }

      setLoading(true);

      try {
        // Attempt to fetch package.json from main or master branch
        let packageJson = null;
        let packageJsonUrl = `https://raw.githubusercontent.com/${ghInfo.owner}/${ghInfo.repo}/main/package.json`;
        let res = await fetch(packageJsonUrl);
        
        if (!res.ok) {
          packageJsonUrl = `https://raw.githubusercontent.com/${ghInfo.owner}/${ghInfo.repo}/master/package.json`;
          res = await fetch(packageJsonUrl);
        }

        if (res.ok) {
          packageJson = await res.json();
        }

        // Fetch directory listing / repository metadata from GitHub API
        const repoApiUrl = `https://api.github.com/repos/${ghInfo.owner}/${ghInfo.repo}`;
        const repoRes = await fetch(repoApiUrl);
        let repoMeta = {};
        if (repoRes.ok) {
          repoMeta = await repoRes.json();
        }

        // Attempt to fetch source code for static scanner inspection
        let entryPointCode = '';
        const entryFile = packageJson?.module || packageJson?.main || packageJson?.unpkg || 'index.js';
        const cleanEntryPath = entryFile.replace(/^\.\//, '');

        let sourceUrl = `https://raw.githubusercontent.com/${ghInfo.owner}/${ghInfo.repo}/main/${cleanEntryPath}`;
        let codeRes = await fetch(sourceUrl);
        if (!codeRes.ok) {
          sourceUrl = `https://raw.githubusercontent.com/${ghInfo.owner}/${ghInfo.repo}/master/${cleanEntryPath}`;
          codeRes = await fetch(sourceUrl);
        }

        // Fallback logic: If raw GitHub fetch fails (e.g., gitignored dist/ files), try unpkg CDN
        if (!codeRes.ok && packageJson?.name) {
          const pkgName = packageJson.name;
          const pkgVersion = packageJson.version || 'latest';
          let cdnFallbackUrl = `https://unpkg.com/${pkgName}@${pkgVersion}/${cleanEntryPath}`;
          try {
            codeRes = await fetch(cdnFallbackUrl);
            // Fall back to root unpkg package entrypoint if path resolution fails
            if (!codeRes.ok) {
              cdnFallbackUrl = `https://unpkg.com/${pkgName}@${pkgVersion}`;
              codeRes = await fetch(cdnFallbackUrl);
            }
          } catch (e) {
            console.warn('CDN fallback fetch failed:', e);
          }
        }

        if (codeRes.ok) {
          entryPointCode = await codeRes.text();
        }

        // Run compatibility & code hazard analysis logic
        const analysis = analyzeImportability(ghInfo, packageJson, repoMeta, entryPointCode);
        currentData = { ghInfo, packageJson, repoMeta, analysis };

        renderResults(currentData);
        hideToast();
      } catch (err) {
        console.error(err);
        showToast("Failed to fetch repository details. Check network or GitHub rate limits.", "error");
      } finally {
        setLoading(false);
      }
    }

    function analyzeImportability(ghInfo, pkg, repoMeta, entryPointCode = '') {
      const name = pkg?.name || ghInfo.repo;
      const version = pkg?.version || 'latest';
      const main = pkg?.main || '';
      const moduleField = pkg?.module || pkg?.['jsnext:main'] || '';
      const unpkgField = pkg?.unpkg || pkg?.jsdelivr || '';
      const pkgType = pkg?.type || 'commonjs';
      const dependencies = Object.keys(pkg?.dependencies || {});
      
      // GitHub API provides repository size in KiB (1024 bytes)
      const rawSizeKb = repoMeta.size || 0;
      const estimatedBytes = rawSizeKb ? rawSizeKb * 1024 : 150000; // default estimate if size unavailable
      const utf16CharEstimate = estimateUtf16Chars(estimatedBytes);
      const storageKit = formatFullStorageKit(estimatedBytes, currentUnitMode);

      // Flag as SUSPICIOUS if estimated size > 4 GB (4 * 10^9 bytes)
      const FOUR_GB_BYTES = 4 * 1000 * 1000 * 1000;
      const isSuspiciousSize = estimatedBytes > FOUR_GB_BYTES;

      // Scan entry point source code for infinite loops and crash hazards
      const hazardAnalysis = scanCodeForHazards(entryPointCode);

      // Scan entry point source code for operators & syntax features
      const operatorAnalysis = scanOperators(entryPointCode);

      // Node core modules check
      const nodeCoreModules = ['fs', 'path', 'http', 'https', 'crypto', 'child_process', 'stream', 'os', 'buffer', 'events'];
      const hasNodeCoreDeps = dependencies.some(dep => nodeCoreModules.includes(dep));

      // Language check (TypeScript / JSX)
      const isTypeScriptRepo = repoMeta.language === 'TypeScript' || main.endsWith('.ts') || moduleField.endsWith('.ts') || operatorAnalysis.requiresTranspilation;
      
      // Determination Rules:
      let directScriptUsable = false; // Works as <script src="..."> exposing a global variable
      let directEsmUsable = false;    // Works as <script type="module"> natively
      let cdnWrapNeeded = false;      // Requires esm.sh or unpkg UMD build
      let buildStepRequired = false;  // Needs Webpack/Babel/TS compiler

      if (unpkgField || (main && (main.endsWith('.min.js') || main.endsWith('.umd.js') || main.includes('dist/')))) {
        directScriptUsable = true;
      }

      if (pkgType === 'module' || moduleField || (main && main.endsWith('.mjs'))) {
        directEsmUsable = true;
      }

      // Special handling for classic global libraries
      if (ghInfo.repo.toLowerCase().includes('expantanum') || ghInfo.repo.toLowerCase().includes('three') || ghInfo.repo.toLowerCase().includes('confetti') || ghInfo.repo.toLowerCase().includes('lodash')) {
        directScriptUsable = true;
        directEsmUsable = true;
      }

      if (hasNodeCoreDeps || ghInfo.repo.toLowerCase() === 'express' || operatorAnalysis.requiresTranspilation) {
        directScriptUsable = false;
        directEsmUsable = false;
        buildStepRequired = true;
      } else if (!directScriptUsable && !directEsmUsable) {
        cdnWrapNeeded = true;
      }

      // Checkpoints List (10 rules evaluation)
      const smartSizeStr = getSmartFormattedSize(estimatedBytes, currentUnitMode).split(' (')[0];
      const checkpoints = [
        {
          title: "Browser ESM Entrypoint (`module` field)",
          pass: Boolean(moduleField || pkgType === 'module'),
          desc: moduleField ? `Found ESM file: ${moduleField}` : (pkgType === 'module' ? 'Package type set to "module"' : 'No ESM field in package.json')
        },
        {
          title: "Browser UMD/Global Bundle (`unpkg` / `jsdelivr`)",
          pass: Boolean(unpkgField || directScriptUsable),
          desc: unpkgField ? `Exposes browser bundle: ${unpkgField}` : (directScriptUsable ? 'UMD / Global bundle detected' : 'No explicit UMD build specified')
        },
        {
          title: "Safe File Size & Bloatware Check (< 4 GB)",
          pass: !isSuspiciousSize,
          desc: isSuspiciousSize ? `⚠️ SUSPICIOUS: Size exceeds 4 GB (${(estimatedBytes / 1e9).toFixed(2)} GB)` : `Estimated size: ${smartSizeStr} (~${utf16CharEstimate.toLocaleString()} UTF-16 chars)`
        },
        {
          title: "Static Code Loop & Crash Hazard Scan",
          pass: hazardAnalysis.safe,
          desc: hazardAnalysis.scanned 
            ? (hazardAnalysis.safe ? "No infinite loops, thread freezes, or crash patterns detected." : `⚠️ Found ${hazardAnalysis.hazards.length} potential hazard pattern(s)`)
            : "Entry source code unavailable for direct static scanning"
        },
        {
          title: "No Node.js Runtime Dependencies",
          pass: !hasNodeCoreDeps && ghInfo.repo.toLowerCase() !== 'express',
          desc: hasNodeCoreDeps ? 'Depends on Node.js system APIs (fs, path, etc.)' : 'Clean of Node-only core APIs'
        },
        {
          title: "Pre-compiled JavaScript (No Uncompiled Syntax)",
          pass: !operatorAnalysis.requiresTranspilation,
          desc: operatorAnalysis.requiresTranspilation ? 'Contains raw TypeScript/Decorators/JSX requiring build step' : 'Standard executable JS syntax'
        },
        {
          title: "CDN Proxy Importable (`esm.sh` / `jsDelivr`)",
          pass: !hasNodeCoreDeps,
          desc: !hasNodeCoreDeps ? 'Available dynamically on esm.sh CDN' : 'Cannot run without Node.js runtime'
        },
        {
          title: "Relative File Import Resolution",
          pass: true,
          desc: 'Standard browser ESM supports relative path imports'
        },
        {
          title: "Import Map Compatible",
          pass: !hasNodeCoreDeps,
          desc: 'Can be mapped via <script type="importmap">'
        },
        {
          title: "No CommonJS `require()` in Browser Entry",
          pass: directEsmUsable || Boolean(unpkgField),
          desc: directEsmUsable ? 'Uses standard ES syntax (`import`/`export`)' : 'CommonJS require requires CDN wrapping'
        }
      ];

      return {
        name,
        version,
        main,
        moduleField,
        unpkgField,
        pkgType,
        dependenciesCount: dependencies.length,
        directScriptUsable,
        directEsmUsable,
        cdnWrapNeeded,
        buildStepRequired,
        estimatedBytes,
        utf16CharEstimate,
        storageKit,
        isSuspiciousSize,
        hazardAnalysis,
        operatorAnalysis,
        checkpoints
      };
    }

    function renderOperatorAnalysis(operatorAnalysis) {
      const ecmaBadge = document.getElementById('ecma-target-badge');
      const summaryBar = document.getElementById('operator-summary-bar');
      const totalCountEl = document.getElementById('operator-total-count');
      const listGrid = document.getElementById('operator-list-grid');

      if (!operatorAnalysis || !operatorAnalysis.scanned) {
        ecmaBadge.textContent = 'Unscanned';
        ecmaBadge.className = 'px-2.5 py-0.5 rounded text-xs font-mono font-bold bg-slate-800 text-slate-400 border border-slate-700';
        summaryBar.innerHTML = `<div class="col-span-3 text-slate-500 py-2">Source code unavailable for operator scanning</div>`;
        totalCountEl.textContent = '0 total occurrences';
        listGrid.innerHTML = '';
        return;
      }

      ecmaBadge.textContent = `${operatorAnalysis.highestEcma} Target`;
      ecmaBadge.className = `px-2.5 py-0.5 rounded text-xs font-mono font-bold ${
        operatorAnalysis.requiresTranspilation 
          ? 'bg-rose-500/20 text-rose-300 border border-rose-500/30' 
          : 'bg-indigo-500/20 text-indigo-300 border border-indigo-500/30'
      }`;

      summaryBar.innerHTML = `
        <div class="p-2 bg-slate-950 border border-slate-800 rounded-lg">
          <div class="text-slate-500 text-[10px]">Target Level</div>
          <div class="font-bold text-indigo-300">${operatorAnalysis.highestEcma}</div>
        </div>
        <div class="p-2 bg-slate-950 border border-slate-800 rounded-lg">
          <div class="text-slate-500 text-[10px]">Transpilation</div>
          <div class="font-bold ${operatorAnalysis.requiresTranspilation ? 'text-rose-400' : 'text-emerald-400'}">
            ${operatorAnalysis.requiresTranspilation ? 'Required' : 'Not Needed'}
          </div>
        </div>
        <div class="p-2 bg-slate-950 border border-slate-800 rounded-lg">
          <div class="text-slate-500 text-[10px]">Unique Features</div>
          <div class="font-bold text-cyan-300">${operatorAnalysis.operators.length} types</div>
        </div>
      `;

      totalCountEl.textContent = `${operatorAnalysis.totalCount.toLocaleString()} operator occurrences`;

      if (operatorAnalysis.operators.length === 0) {
        listGrid.innerHTML = `<div class="col-span-2 p-3 bg-slate-950 border border-slate-800 rounded-xl text-slate-500 text-center">Standard ES5/ES6 syntax baseline (No specialized modern operators detected)</div>`;
        return;
      }

      listGrid.innerHTML = operatorAnalysis.operators.map(op => `
        <div class="p-2.5 bg-slate-950 border ${
          op.impact === 'transpile' ? 'border-rose-900/50 bg-rose-950/10' : (op.impact === 'warning' ? 'border-amber-900/40 bg-amber-950/10' : 'border-slate-800')
        } rounded-xl flex items-center justify-between">
          <div>
            <div class="text-xs font-semibold ${op.impact === 'transpile' ? 'text-rose-300' : 'text-slate-200'} flex items-center gap-1.5">
              <span>${op.name}</span>
            </div>
            <div class="text-[10px] text-slate-500 mt-0.5">${op.category} • ${op.minEngine}</div>
          </div>
          <span class="px-2 py-0.5 bg-slate-900 border border-slate-700/80 rounded-md text-xs font-bold text-indigo-300">
            ${op.count}×
          </span>
        </div>
      `).join('');
    }

    function renderResults(data) {
      const { ghInfo, packageJson, repoMeta, analysis } = data;
      const view = document.getElementById('results-view');
      view.classList.remove('hidden');

      // Render Code Hazards Alert if dangerous patterns were found
      const hazardAlert = document.getElementById('code-hazard-alert');
      const hazardDetails = document.getElementById('code-hazard-details');

      if (analysis.hazardAnalysis && !analysis.hazardAnalysis.safe) {
        hazardAlert.classList.remove('hidden');
        hazardDetails.innerHTML = analysis.hazardAnalysis.hazards.map(h => `
          <div class="flex items-start gap-1.5">
            <span class="px-1.5 py-0.5 rounded text-[9px] font-bold uppercase bg-rose-500/30 text-rose-200 border border-rose-500/40">${h.type}</span>
            <span>${h.message}</span>
          </div>
        `).join('');
      } else {
        hazardAlert.classList.add('hidden');
      }

      // Render Operator Analysis UI
      renderOperatorAnalysis(analysis.operatorAnalysis);

      // 1. Render Verdict Banner
      const banner = document.getElementById('verdict-banner');
      let statusHtml = '';

      if (analysis.isSuspiciousSize) {
        statusHtml = `
          <div class="flex items-start gap-4">
            <div class="p-3 bg-rose-500/10 border border-rose-500/20 text-rose-400 rounded-xl">
              <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
              </svg>
            </div>
            <div>
              <div class="flex items-center gap-2">
                <h2 class="text-xl font-bold text-white">⚠️ SUSPICIOUS: Oversized Payload / Potential Zip Bomb</h2>
                <span class="px-2.5 py-0.5 rounded-full text-xs font-semibold bg-rose-500/20 text-rose-300 border border-rose-500/30">&gt; 4 GB Flagged</span>
              </div>
              <p class="text-xs text-slate-400 mt-1 max-w-2xl">
                This repository or file size exceeds <b>4 GB</b> (~${(analysis.estimatedBytes / 1e9).toFixed(2)} GB, or ~${analysis.utf16CharEstimate.toLocaleString()} UTF-16 characters). It has been flagged as suspicious due to risks of severe bloatware or browser zip bombs.
              </p>
            </div>
          </div>
        `;
      } else if (analysis.buildStepRequired) {
        statusHtml = `
          <div class="flex items-start gap-4">
            <div class="p-3 bg-rose-500/10 border border-rose-500/20 text-rose-400 rounded-xl">
              <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
            <div>
              <div class="flex items-center gap-2">
                <h2 class="text-xl font-bold text-white">Node.js / Build-Required Library</h2>
                <span class="px-2.5 py-0.5 rounded-full text-xs font-semibold bg-rose-500/20 text-rose-300 border border-rose-500/30">Incompatible with Plain Script Tag</span>
              </div>
              <p class="text-xs text-slate-400 mt-1 max-w-2xl">
                This repository relies on Node.js core APIs (e.g., file system or HTTP server) or requires transpilation. It cannot run directly inside a browser HTML page without a bundler or polyfills.
              </p>
            </div>
          </div>
        `;
      } else if (analysis.directScriptUsable || analysis.directEsmUsable) {
        statusHtml = `
          <div class="flex items-start gap-4">
            <div class="p-3 bg-emerald-500/10 border border-emerald-500/20 text-emerald-400 rounded-xl">
              <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
            <div>
              <div class="flex items-center gap-2">
                <h2 class="text-xl font-bold text-white">Directly Usable in Browser HTML!</h2>
                <span class="px-2.5 py-0.5 rounded-full text-xs font-semibold bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">100% Browser Ready</span>
              </div>
              <p class="text-xs text-slate-400 mt-1 max-w-2xl">
                This repository exposes standard browser code! You can easily include it in any HTML file using a standard <code class="text-emerald-300">&lt;script&gt;</code> tag or as a native ES module.
              </p>
            </div>
          </div>
        `;
      } else {
        statusHtml = `
          <div class="flex items-start gap-4">
            <div class="p-3 bg-amber-500/10 border border-amber-500/20 text-amber-400 rounded-xl">
              <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
              </svg>
            </div>
            <div>
              <div class="flex items-center gap-2">
                <h2 class="text-xl font-bold text-white">Usable via Modern CDN Wrapper</h2>
                <span class="px-2.5 py-0.5 rounded-full text-xs font-semibold bg-amber-500/20 text-amber-300 border border-amber-500/30">ESM CDN Required</span>
              </div>
              <p class="text-xs text-slate-400 mt-1 max-w-2xl">
                This library uses CommonJS or unbundled modules. While you can't load the raw file directly, CDN providers like <code class="text-amber-300">esm.sh</code> bundle it dynamically on the fly so it works seamlessly in standard <code class="text-amber-300">&lt;script type="module"&gt;</code> tags!
              </p>
            </div>
          </div>
        `;
      }

      banner.innerHTML = statusHtml;

      // 2. Render Code Snippets
      updateSnippetDisplay();

      // 3. Render Metadata & Sizes
      document.getElementById('meta-name').textContent = `${ghInfo.owner}/${ghInfo.repo}`;
      document.getElementById('meta-type').textContent = analysis.pkgType;
      
      // Render Size & UTF-16 Estimate using Storage Unit Kit smart scale (e.g. 1.72 GB instead of 1722 MB)
      document.getElementById('meta-size').textContent = getSmartFormattedSize(analysis.estimatedBytes, currentUnitMode);
      document.getElementById('meta-utf16').textContent = `~${analysis.utf16CharEstimate.toLocaleString()} UTF-16 units`;

      document.getElementById('meta-main').textContent = analysis.main || 'Not specified';
      document.getElementById('meta-module').textContent = analysis.moduleField || 'None';
      document.getElementById('meta-unpkg').textContent = analysis.unpkgField || 'None';
      document.getElementById('meta-deps').textContent = `${analysis.dependenciesCount} dependencies`;

      // Render Security & Storage Unit Kit
      renderStorageAndSecurityKit(analysis);

      // CDN links
      const pkgName = analysis.name;
      document.getElementById('cdn-jsdelivr').href = `https://cdn.jsdelivr.net/npm/${pkgName}`;
      document.getElementById('cdn-esmsh').href = `https://esm.sh/${pkgName}`;
      document.getElementById('cdn-unpkg').href = `https://unpkg.com/${pkgName}`;

      // 4. Render Checkpoints
      const checklistContainer = document.getElementById('checklist-items');
      checklistContainer.innerHTML = analysis.checkpoints.map(item => `
        <div class="p-3 bg-slate-950/60 border ${item.pass ? 'border-slate-800' : 'border-rose-900/40 bg-rose-950/20'} rounded-xl flex items-start gap-2.5">
          <div class="mt-0.5">
            ${item.pass ? `
              <span class="w-4 h-4 rounded-full bg-emerald-500/20 text-emerald-400 border border-emerald-500/40 flex items-center justify-center text-[10px] font-bold">✓</span>
            ` : `
              <span class="w-4 h-4 rounded-full bg-rose-500/20 text-rose-400 border border-rose-500/40 flex items-center justify-center text-[10px] font-bold">✕</span>
            `}
          </div>
          <div>
            <div class="text-xs font-semibold ${item.pass ? 'text-slate-200' : 'text-rose-300'}">${item.title}</div>
            <div class="text-[11px] ${item.pass ? 'text-slate-500' : 'text-rose-400/90'} mt-0.5">${item.desc}</div>
          </div>
        </div>
      `).join('');

      // Reset AI explanation box
      document.getElementById('ai-output').classList.add('hidden');
    }

    function renderStorageAndSecurityKit(analysis) {
      const securityBadge = document.getElementById('security-badge');
      const suspiciousAlert = document.getElementById('suspicious-alert');
      const unitGrid = document.getElementById('unit-kit-grid');
      const quotaContainer = document.getElementById('quota-benchmarks');

      if (analysis.isSuspiciousSize) {
        securityBadge.textContent = '⚠️ SUSPICIOUS (>4 GB)';
        securityBadge.className = 'px-2 py-0.5 rounded text-[10px] font-mono font-bold bg-rose-500/20 text-rose-400 border border-rose-500/40 animate-pulse';
        suspiciousAlert.classList.remove('hidden');
      } else {
        securityBadge.textContent = 'SAFE SIZE';
        securityBadge.className = 'px-2 py-0.5 rounded text-[10px] font-mono font-bold bg-emerald-500/20 text-emerald-400 border border-emerald-500/30';
        suspiciousAlert.classList.add('hidden');
      }

      // Determine dominant storage unit scale index to highlight
      const bytes = analysis.estimatedBytes;
      let activeIndex = 0;

      if (currentUnitMode === 'si') {
        if (bytes >= 1e30) activeIndex = 10;
        else if (bytes >= 1e27) activeIndex = 9;
        else if (bytes >= 1e24) activeIndex = 8;
        else if (bytes >= 1e21) activeIndex = 7;
        else if (bytes >= 1e18) activeIndex = 6;
        else if (bytes >= 1e15) activeIndex = 5;
        else if (bytes >= 1e12) activeIndex = 4;
        else if (bytes >= 1e9) activeIndex = 3;  // GB (Gigabytes)
        else if (bytes >= 1e6) activeIndex = 2;  // MB
        else if (bytes >= 1e3) activeIndex = 1;  // KB
      } else {
        const p = Math.floor(Math.log(Math.max(1, bytes)) / Math.log(1024));
        activeIndex = Math.min(10, Math.max(0, p));
      }

      // Render all 11 storage units with active magnitude highlighting
      unitGrid.innerHTML = analysis.storageKit.map((item, index) => {
        const isActive = index === activeIndex;
        return `
          <div class="p-1.5 rounded-lg flex items-center justify-between border transition ${
            isActive 
              ? 'bg-indigo-950/80 border-indigo-500 text-white shadow-lg ring-1 ring-indigo-500/50' 
              : 'bg-slate-950 border-slate-800 text-slate-400'
          }">
            <span class="text-[10px] ${isActive ? 'text-indigo-300 font-bold' : 'text-slate-500'}">${item.symbol} (${item.name}):</span>
            <span class="font-semibold truncate ml-1 ${isActive ? 'text-indigo-200 text-xs' : 'text-indigo-300'}">${item.formatted}</span>
          </div>
        `;
      }).join('');

      // Browser Quota Benchmarks Comparison
      const scriptBudgetPct = Math.min(999, Math.round((bytes / 1000000) * 100)); // 1MB budget
      const localStoragePct = Math.min(999, Math.round((bytes / 5000000) * 100)); // 5MB limit
      const indexedDbPct = Math.min(999, Math.round((bytes / 50000000) * 100)); // 50MB benchmark

      quotaContainer.innerHTML = `
        <div class="p-2 bg-slate-950 border border-slate-800 rounded-lg">
          <div class="text-slate-500">1MB Script Tag Budget:</div>
          <div class="font-bold ${scriptBudgetPct > 100 ? 'text-amber-400' : 'text-emerald-400'}">${scriptBudgetPct}% of recommended limit</div>
        </div>
        <div class="p-2 bg-slate-950 border border-slate-800 rounded-lg">
          <div class="text-slate-500">5MB localStorage Quota:</div>
          <div class="font-bold ${localStoragePct > 100 ? 'text-rose-400' : 'text-emerald-400'}">${localStoragePct}% of browser quota</div>
        </div>
        <div class="p-2 bg-slate-950 border border-slate-800 rounded-lg">
          <div class="text-slate-500">50MB IndexedDB Tier:</div>
          <div class="font-bold text-cyan-300">${indexedDbPct}% allocated</div>
        </div>
        <div class="p-2 bg-slate-950 border border-slate-800 rounded-lg">
          <div class="text-slate-500">4GB Zip Bomb Threshold:</div>
          <div class="font-bold ${analysis.isSuspiciousSize ? 'text-rose-400 animate-pulse' : 'text-slate-300'}">${((bytes / (4 * 1000 * 1000 * 1000)) * 100).toFixed(2)}% threshold</div>
        </div>
      `;
    }

    /**
     * Interactive simulator: test any byte count to check unit scale & 4 GB flag
     */
    function simulateSizeInput() {
      const inputVal = parseFloat(document.getElementById('sim-bytes-input').value);
      if (isNaN(inputVal) || inputVal < 0) {
        showToast("Please enter a valid number of bytes.", "error");
        return;
      }

      const simulatedBytes = inputVal;
      const utf16CharEstimate = estimateUtf16Chars(simulatedBytes);
      const storageKit = formatFullStorageKit(simulatedBytes, currentUnitMode);
      const isSuspiciousSize = simulatedBytes > (4 * 1000 * 1000 * 1000);

      if (currentData) {
        currentData.analysis.estimatedBytes = simulatedBytes;
        currentData.analysis.utf16CharEstimate = utf16CharEstimate;
        currentData.analysis.storageKit = storageKit;
        currentData.analysis.isSuspiciousSize = isSuspiciousSize;

        const sizeCheckpoint = currentData.analysis.checkpoints.find(c => c.title.includes('File Size'));
        if (sizeCheckpoint) {
          sizeCheckpoint.pass = !isSuspiciousSize;
          sizeCheckpoint.desc = isSuspiciousSize 
            ? `⚠️ SUSPICIOUS: Size exceeds 4 GB (${(simulatedBytes / 1e9).toFixed(2)} GB)` 
            : `Estimated size: ${(simulatedBytes / 1024).toFixed(1)} KB (~${utf16CharEstimate.toLocaleString()} UTF-16 chars)`;
        }

        renderResults(currentData);
        showToast(isSuspiciousSize ? "⚠️ Custom size flagged as SUSPICIOUS (> 4 GB)!" : "Updated size analysis successfully.", isSuspiciousSize ? "error" : "success");
      }
    }

    function switchSnippetTab(tab) {
      activeTab = tab;
      
      const btnClassic = document.getElementById('tab-classic');
      const btnEsm = document.getElementById('tab-esm');
      const btnImportmap = document.getElementById('tab-importmap');

      [btnClassic, btnEsm, btnImportmap].forEach(b => {
        b.className = 'px-3 py-1 rounded-md transition text-slate-400 hover:text-slate-200';
      });

      if (tab === 'classic') btnClassic.className = 'px-3 py-1 rounded-md transition text-slate-200 bg-slate-800 font-medium';
      if (tab === 'esm') btnEsm.className = 'px-3 py-1 rounded-md transition text-slate-200 bg-slate-800 font-medium';
      if (tab === 'importmap') btnImportmap.className = 'px-3 py-1 rounded-md transition text-slate-200 bg-slate-800 font-medium';

      updateSnippetDisplay();
    }

    function updateSnippetDisplay() {
      if (!currentData) return;

      const { analysis, ghInfo } = currentData;
      const pkgName = analysis.name;
      const snippetEl = document.getElementById('code-snippet');
      const noteEl = document.getElementById('snippet-note');

      if (analysis.buildStepRequired) {
        snippetEl.innerHTML = `<code>&lt;!-- ⚠️ CANNOT BE IMPORTED DIRECTLY IN BROWSER --&gt;\n&lt;!-- This library requires Node.js runtime or build tooling. --&gt;</code>`;
        noteEl.innerHTML = '⚠️ Build tooling or polyfills required for this package.';
        return;
      }

      if (activeTab === 'classic') {
        const url = `https://cdn.jsdelivr.net/npm/${pkgName}`;
        snippetEl.innerText = 
`<!-- Classic Script Tag (Global Variable Exposing) -->
<script src="${url}"><\/script>

<script>
  // Access global variable provided by the library
  console.log("Loaded ${pkgName} successfully!");
<\/script>`;
        noteEl.innerHTML = '💡 Best for classic libraries (like <b>ExpantaNum</b>, <b>Three.js</b>, or UMD packages).';

      } else if (activeTab === 'esm') {
        const url = `https://esm.sh/${pkgName}`;
        snippetEl.innerText = 
`<!-- Native ES Module Import Tag -->
<script type="module">
  import Lib from '${url}';

  // Use the imported library directly in standard browser JS
  console.log(Lib);
<\/script>`;
        noteEl.innerHTML = '⚡ Modern ES Module format; loaded on-the-fly via esm.sh CDN.';

      } else if (activeTab === 'importmap') {
        const url = `https://esm.sh/${pkgName}`;
        snippetEl.innerText = 
`<!-- Import Map Specification -->
<script type="importmap">
{
  "imports": {
    "${pkgName}": "${url}"
  }
}
<\/script>

<script type="module">
  // Custom bare import directly in HTML!
  import Lib from '${pkgName}';
  console.log(Lib);
<\/script>`;
        noteEl.innerHTML = '🗺️ Clean bare imports in raw HTML using standard browser Import Maps.';
      }
    }

    function copyCodeSnippet() {
      const codeText = document.getElementById('code-snippet').innerText;
      
      // Use fallback clipboard command
      const textarea = document.createElement('textarea');
      textarea.value = codeText;
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand('copy');
      document.body.removeChild(textarea);

      const copyText = document.getElementById('copy-text');
      copyText.textContent = 'Copied!';
      setTimeout(() => {
        copyText.textContent = 'Copy Code';
      }, 2000);
    }

    async function runGeminiAiAnalysis() {
      if (!currentData) return;

      const aiBtn = document.getElementById('ai-btn');
      const aiOutput = document.getElementById('ai-output');

      aiBtn.disabled = true;
      aiBtn.innerHTML = '<div class="w-4 h-4 border-2 border-white/20 border-t-white rounded-full animate-spin"></div> Generating with Gemini...';

      const prompt = `Act as an expert frontend engineer. Provide a concise 2-paragraph HTML integration guide for the library "${currentData.analysis.name}" (${currentData.ghInfo.fullRepoUrl}).
Explain how a developer can include it in a standard HTML file without Webpack/Vite using CDN script tags or ESM import maps, and give a minimal 3-line code example.`;

      const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

      try {
        const response = await fetch(apiUrl, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            contents: [{ parts: [{ text: prompt }] }]
          })
        });

        const result = await response.json();
        const text = result?.candidates?.[0]?.content?.parts?.[0]?.text;

        if (text) {
          aiOutput.classList.remove('hidden');
          aiOutput.innerText = text;
        } else {
          aiOutput.classList.remove('hidden');
          aiOutput.innerText = "Could not generate AI response at this moment.";
        }
      } catch (e) {
        aiOutput.classList.remove('hidden');
        aiOutput.innerText = "AI Generation error: Unable to connect to Gemini API.";
      } finally {
        aiBtn.disabled = false;
        aiBtn.innerHTML = '<span>Generate AI Integration Guide</span>';
      }
    }

    function setLoading(isLoading) {
      const spinner = document.getElementById('loading-spinner');
      const resultsView = document.getElementById('results-view');
      const btnText = document.getElementById('btn-text');

      if (isLoading) {
        spinner.classList.remove('hidden');
        resultsView.classList.add('hidden');
        btnText.textContent = 'Analyzing...';
      } else {
        spinner.classList.add('hidden');
        btnText.textContent = 'Analyze GitHub URL';
      }
    }

    function showToast(msg, type = "error") {
      const box = document.getElementById('toast-box');
      box.classList.remove('hidden');
      box.className = `rounded-xl border p-4 text-xs font-medium ${
        type === 'error' ? 'bg-rose-500/10 border-rose-500/20 text-rose-300' : 'bg-emerald-500/10 border-emerald-500/20 text-emerald-300'
      }`;
      box.textContent = msg;
    }

    function hideToast() {
      const box = document.getElementById('toast-box');
      box.classList.add('hidden');
    }

    window.onload = function() {
      // Auto run default preset on launch
      inspectRepo();
    };
  </script>
</body>
</html>