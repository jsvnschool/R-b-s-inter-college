<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>VidOne AI — All-in-One AI Video Generation Studio</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Lucide Icons CDN -->
  <script src="https://unpkg.com/lucide@latest"></script>
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['"Plus Jakarta Sans"', 'sans-serif'],
            mono: ['"JetBrains Mono"', 'monospace'],
          },
          colors: {
            brand: {
              50: '#eef2ff',
              100: '#e0e7ff',
              400: '#818cf8',
              500: '#6366f1',
              600: '#4f46e5',
              700: '#4338ca',
              accent: '#ec4899',
              cyan: '#06b6d4',
            },
            surface: {
              base: '#080a12',
              card: '#0e1322',
              border: '#1e293b',
              hover: '#1a2238'
            }
          }
        }
      }
    }
  </script>

  <style>
    body {
      background-color: #080a12;
      color: #f1f5f9;
      font-family: 'Plus Jakarta Sans', sans-serif;
      overflow-x: hidden;
    }

    /* Custom glow effects */
    .glow-purple {
      background: radial-gradient(circle at 50% 50%, rgba(99, 102, 241, 0.18) 0%, transparent 70%);
    }
    .glow-accent {
      background: radial-gradient(circle at 50% 50%, rgba(236, 72, 153, 0.15) 0%, transparent 60%);
    }

    /* Glassmorphism */
    .glass-panel {
      background: rgba(14, 19, 34, 0.75);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }
    .glass-button {
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(8px);
    }
    .glass-button:hover {
      background: rgba(255, 255, 255, 0.1);
      border-color: rgba(99, 102, 241, 0.5);
    }

    /* Custom Scrollbars */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #080a12;
    }
    ::-webkit-scrollbar-thumb {
      background: #1e293b;
      border-radius: 999px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #4f46e5;
    }

    /* Video player frame constraints */
    .aspect-16-9 { aspect-ratio: 16 / 9; }
    .aspect-9-16 { aspect-ratio: 9 / 16; max-height: 520px; }
    .aspect-1-1 { aspect-ratio: 1 / 1; }
    .aspect-21-9 { aspect-ratio: 21 / 9; }
  </style>
</head>
<body class="selection:bg-brand-500 selection:text-white">

  <!-- Ambient Light Orbs -->
  <div class="fixed top-0 left-1/4 w-[600px] h-[600px] glow-purple pointer-events-none -z-10 blur-3xl"></div>
  <div class="fixed top-1/3 right-10 w-[500px] h-[500px] glow-accent pointer-events-none -z-10 blur-3xl"></div>

  <!-- Navbar -->
  <header class="sticky top-0 z-50 glass-panel border-b border-surface-border">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
      <div class="flex items-center space-x-8">
        <a href="#" class="flex items-center space-x-3">
          <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-brand-600 via-brand-500 to-brand-accent flex items-center justify-center shadow-lg shadow-brand-500/25">
            <i data-lucide="sparkles" class="w-5 h-5 text-white"></i>
          </div>
          <span class="text-xl font-extrabold tracking-tight bg-clip-text text-transparent bg-gradient-to-r from-white via-slate-100 to-slate-400">
            VidOne<span class="text-brand-400">.ai</span>
          </span>
        </a>
        <nav class="hidden md:flex items-center space-x-6 text-sm font-medium text-slate-300">
          <a href="#studio" class="text-white hover:text-brand-400 transition">Studio</a>
          <a href="#features" class="hover:text-white transition">Features</a>
          <a href="#templates" class="hover:text-white transition">Templates</a>
          <a href="#pricing" class="hover:text-white transition">Pricing</a>
        </nav>
      </div>

      <div class="flex items-center space-x-3">
        <div class="hidden sm:flex items-center space-x-2 bg-slate-900/90 border border-slate-800 px-3 py-1.5 rounded-full text-xs">
          <i data-lucide="zap" class="w-3.5 h-3.5 text-amber-400 fill-amber-400"></i>
          <span class="text-slate-300 font-medium">Credits:</span>
          <span id="creditBalance" class="text-white font-bold font-mono">1,250</span>
        </div>
        <button onclick="openModal('authModal')" class="glass-button text-xs font-semibold px-4 py-2 rounded-lg transition text-slate-200">
          Sign In
        </button>
        <button onclick="scrollToStudio()" class="bg-gradient-to-r from-brand-600 to-brand-500 hover:from-brand-500 hover:to-brand-400 text-white text-xs font-semibold px-4 py-2 rounded-lg transition shadow-md shadow-brand-500/30">
          Create Video
        </button>
      </div>
    </div>
  </header>

  <!-- Hero Section -->
  <section class="relative pt-12 pb-8 px-4 text-center max-w-4xl mx-auto">
    <div class="inline-flex items-center space-x-2 px-3.5 py-1.5 rounded-full bg-brand-500/10 border border-brand-500/30 text-brand-400 text-xs font-semibold mb-6">
      <i data-lucide="flame" class="w-3.5 h-3.5"></i>
      <span>VidOne 3.0 Engine Released — 4K Neural Motion & Multilingual Voice</span>
    </div>
    <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight text-white leading-tight">
      Turn Any Prompt or Story Into <br class="hidden sm:block"/>
      <span class="bg-clip-text text-transparent bg-gradient-to-r from-brand-400 via-purple-300 to-brand-accent">
        Viral Cinematic Videos
      </span>
    </h1>
    <p class="mt-4 text-slate-400 text-base sm:text-lg max-w-2xl mx-auto">
      Scriptwriting, hyper-realistic video generation, studio voiceover, and soundtrack synthesis—all seamlessly stitched into ready-to-publish short films in seconds.
    </p>
  </section>

  <!-- Main AI Studio App (VidOne Core Workstation) -->
  <section id="studio" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
    <div class="glass-panel rounded-2xl p-4 sm:p-6 shadow-2xl border border-slate-800">
      
      <!-- Studio Tabs (Text to Video, Image to Video, Script Engine, Face Swap) -->
      <div class="flex items-center justify-between border-b border-slate-800 pb-4 mb-6 flex-wrap gap-3">
        <div class="flex items-center space-x-2 bg-slate-950/70 p-1 rounded-xl border border-slate-800" role="tablist">
          <button onclick="setStudioMode('text-to-video')" id="tab-text-to-video" class="flex items-center space-x-2 px-4 py-2 rounded-lg text-xs font-semibold bg-brand-600 text-white shadow-sm transition">
            <i data-lucide="video" class="w-4 h-4"></i>
            <span>Text to Video</span>
          </button>
          <button onclick="setStudioMode('script-to-film')" id="tab-script-to-film" class="flex items-center space-x-2 px-4 py-2 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">
            <i data-lucide="scroll" class="w-4 h-4"></i>
            <span>Story / Script</span>
          </button>
          <button onclick="setStudioMode('image-to-video')" id="tab-image-to-video" class="flex items-center space-x-2 px-4 py-2 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">
            <i data-lucide="image" class="w-4 h-4"></i>
            <span>Image to Video</span>
          </button>
        </div>

        <!-- Quick Aspect Ratio Toggle -->
        <div class="flex items-center space-x-2">
          <span class="text-xs text-slate-400 font-medium hidden sm:inline">Ratio:</span>
          <div class="flex items-center space-x-1 bg-slate-950/70 p-1 rounded-xl border border-slate-800">
            <button onclick="setAspectRatio('16-9')" id="ratio-16-9" class="p-1.5 rounded-lg text-brand-400 bg-brand-500/20 text-xs font-mono font-bold" title="16:9 YouTube / Film">16:9</button>
            <button onclick="setAspectRatio('9-16')" id="ratio-9-16" class="p-1.5 rounded-lg text-slate-400 hover:text-white text-xs font-mono font-bold" title="9:16 Reels / Shorts / TikTok">9:16</button>
            <button onclick="setAspectRatio('1-1')" id="ratio-1-1" class="p-1.5 rounded-lg text-slate-400 hover:text-white text-xs font-mono font-bold" title="1:1 Square">1:1</button>
          </div>
        </div>
      </div>

      <!-- Studio Workstation Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- Left Column: Controls & Prompt Input -->
        <div class="lg:col-span-5 flex flex-col space-y-4">
          
          <!-- Prompt / Script Box -->
          <div class="bg-surface-card rounded-xl p-4 border border-slate-800">
            <div class="flex justify-between items-center mb-2">
              <label id="inputLabel" class="text-xs font-bold uppercase tracking-wider text-slate-400">Describe Your Video Scene</label>
              <button onclick="injectSamplePrompt()" class="text-xs text-brand-400 hover:underline flex items-center space-x-1">
                <i data-lucide="dice-5" class="w-3.5 h-3.5"></i>
                <span>Surprise Me</span>
              </button>
            </div>
            <textarea id="promptInput" rows="4" class="w-full bg-slate-950/80 border border-slate-800 rounded-lg p-3 text-sm text-slate-100 placeholder-slate-600 focus:outline-none focus:border-brand-500 font-sans" placeholder="E.g., A cybernetic samurai standing on a neon-lit Tokyo rooftop under rain, slow dolly camera push-in, 8k resolution, cinematic lighting..."></textarea>

            <!-- Dynamic Image Upload Area for Image to Video Mode -->
            <div id="imageUploadArea" class="hidden mt-3 border-2 border-dashed border-slate-800 hover:border-brand-500/50 rounded-xl p-4 text-center cursor-pointer transition">
              <i data-lucide="upload-cloud" class="w-8 h-8 text-brand-400 mx-auto mb-2"></i>
              <p class="text-xs text-slate-300 font-medium">Upload reference character or photo</p>
              <p class="text-[11px] text-slate-500 mt-1">PNG, JPG, WebP up to 25MB</p>
            </div>
          </div>

          <!-- Generation Settings (Style, Camera, Voiceover) -->
          <div class="bg-surface-card rounded-xl p-4 border border-slate-800 space-y-4">
            <h4 class="text-xs font-bold uppercase tracking-wider text-slate-400 flex items-center justify-between">
              <span>Director Settings</span>
              <i data-lucide="sliders" class="w-3.5 h-3.5 text-slate-500"></i>
            </h4>

            <div class="grid grid-cols-2 gap-3">
              <div>
                <label class="block text-[11px] text-slate-400 font-medium mb-1">Visual Art Style</label>
                <select id="styleSelector" class="w-full bg-slate-950 border border-slate-800 rounded-lg p-2 text-xs text-slate-200 focus:border-brand-500 focus:outline-none">
                  <option value="photorealistic">Hyper Photorealistic (Runway 3.0)</option>
                  <option value="anime">Anime 2.0 (Makoto Shinkai)</option>
                  <option value="pixar">3D Animation (Pixar/Dreamworks)</option>
                  <option value="cyberpunk">Cyberpunk Neon Cinematic</option>
                  <option value="vintage">1980s Retro Film 35mm</option>
                </select>
              </div>

              <div>
                <label class="block text-[11px] text-slate-400 font-medium mb-1">Camera Movement</label>
                <select id="cameraMotion" class="w-full bg-slate-950 border border-slate-800 rounded-lg p-2 text-xs text-slate-200 focus:border-brand-500 focus:outline-none">
                  <option value="dolly">Dolly Zoom Push-In</option>
                  <option value="drone">360° Drone Aerial Orbit</option>
                  <option value="pan">Cinematic Slow Pan Right</option>
                  <option value="shaky">Handheld Action Follow</option>
                </select>
              </div>
            </div>

            <!-- Voiceover Engine Selection -->
            <div class="pt-2 border-t border-slate-800/80">
              <div class="flex items-center justify-between mb-2">
                <span class="text-xs font-medium text-slate-300 flex items-center space-x-1.5">
                  <i data-lucide="mic" class="w-3.5 h-3.5 text-brand-400"></i>
                  <span>AI Voice Narration</span>
                </span>
                <label class="relative inline-flex items-center cursor-pointer">
                  <input type="checkbox" id="voiceToggle" checked class="sr-only peer">
                  <div class="w-9 h-5 bg-slate-800 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-4 after:w-4 after:transition-all peer-checked:bg-brand-600"></div>
                </label>
              </div>

              <div id="voiceSettingsRow" class="grid grid-cols-2 gap-3">
                <select id="voiceLanguage" class="w-full bg-slate-950 border border-slate-800 rounded-lg p-2 text-xs text-slate-200">
                  <option value="hi-IN">Hindi (Deep Baritone)</option>
                  <option value="en-US">English (Hollywood Epic)</option>
                  <option value="en-IN">Indian English (Warm Professional)</option>
                </select>
                <select id="bgmGenre" class="w-full bg-slate-950 border border-slate-800 rounded-lg p-2 text-xs text-slate-200">
                  <option value="cinematic">Cinematic Orchestra</option>
                  <option value="synthwave">Cyberpunk Synthwave</option>
                  <option value="ambient">Calm Deep Ambient</option>
                </select>
              </div>
            </div>

          </div>

          <!-- Generate Action Button -->
          <button id="generateVideoBtn" onclick="startGenerationPipeline()" class="w-full py-4 px-6 rounded-xl font-extrabold text-sm tracking-wide text-white bg-gradient-to-r from-brand-600 via-indigo-600 to-brand-accent hover:opacity-95 active:scale-[0.99] transition shadow-lg shadow-brand-500/30 flex items-center justify-center space-x-2">
            <i data-lucide="play-circle" class="w-5 h-5"></i>
            <span>GENERATE AI VIDEO (20 CREDITS)</span>
          </button>

          <!-- Real-Time Telemetry Log Terminal -->
          <div class="bg-black/60 rounded-xl p-3 border border-slate-800 font-mono text-[11px] text-slate-400">
            <div class="flex items-center justify-between text-slate-500 mb-1 border-b border-slate-900 pb-1">
              <span>PIPELINE TELEMETRY</span>
              <span id="telemetryStatus" class="text-emerald-400">IDLE</span>
            </div>
            <div id="telemetryConsole" class="space-y-0.5 text-slate-300 min-h-[44px]">
              &gt; Ready. Awaiting prompt input...
            </div>
          </div>

        </div>

        <!-- Right Column: Live Video Canvas & Playback Dock -->
        <div class="lg:col-span-7 flex flex-col space-y-4">
          
          <div class="relative w-full rounded-2xl overflow-hidden border border-slate-800 bg-black flex items-center justify-center shadow-2xl">
            <!-- Canvas Video Surface -->
            <canvas id="studioCanvas" width="1280" height="720" class="w-full aspect-16-9 object-contain bg-slate-950"></canvas>

            <!-- Video Rendering Overlay / Loading Bar -->
            <div id="renderProgressOverlay" class="absolute inset-0 bg-slate-950/90 backdrop-blur-md flex flex-col items-center justify-center p-6 hidden">
              <div class="w-16 h-16 rounded-full border-4 border-slate-800 border-t-brand-500 animate-spin mb-4"></div>
              <h3 class="text-base font-bold text-white mb-1" id="progressStepTitle">Synthesizing Neural Diffusion Latents...</h3>
              <p class="text-xs text-slate-400 max-w-sm text-center mb-4" id="progressSubTitle">Rendering camera motion and temporal consistency frames</p>
              
              <div class="w-full max-w-md bg-slate-800 rounded-full h-2.5 overflow-hidden">
                <div id="progressBar" class="bg-gradient-to-r from-brand-500 to-brand-accent h-2.5 rounded-full transition-all duration-300" style="width: 15%"></div>
              </div>
              <span id="progressPercent" class="text-xs font-mono text-slate-300 mt-2">15%</span>
            </div>

            <!-- Idle Placeholder Watermark -->
            <div id="playerIdleNotice" class="absolute inset-0 flex flex-col items-center justify-center pointer-events-none p-6 text-center">
              <div class="w-16 h-16 rounded-2xl bg-brand-500/10 border border-brand-500/30 flex items-center justify-center mb-3">
                <i data-lucide="clapperboard" class="w-8 h-8 text-brand-400"></i>
              </div>
              <h3 class="text-sm font-semibold text-slate-200">AI Preview Canvas Ready</h3>
              <p class="text-xs text-slate-500 max-w-xs mt-1">Configure your visual prompt on the left and hit Generate Video</p>
            </div>

            <!-- Live Subtitle Overlay -->
            <div id="subtitleOverlay" class="absolute bottom-6 left-6 right-6 text-center pointer-events-none hidden">
              <span id="subtitleText" class="inline-block px-4 py-1.5 rounded-lg bg-black/85 backdrop-blur-sm text-amber-300 font-semibold text-xs sm:text-sm tracking-wide border border-amber-400/20 shadow-xl">
                ...
              </span>
            </div>
          </div>

          <!-- Video Playback Controller Bar -->
          <div class="glass-panel rounded-xl p-3 flex items-center justify-between border border-slate-800 gap-2">
            <div class="flex items-center space-x-2">
              <button onclick="toggleVideoPlayback()" id="playPauseBtn" class="w-9 h-9 rounded-lg bg-brand-600 hover:bg-brand-500 text-white flex items-center justify-center transition">
                <i data-lucide="play" class="w-4 h-4" id="playIcon"></i>
              </button>
              <div class="text-xs font-mono text-slate-400">
                <span id="currentTimeDisplay">00:00</span> / <span id="totalDurationDisplay">00:05</span>
              </div>
            </div>

            <!-- Timeline Scrubber -->
            <div class="flex-1 max-w-md mx-2">
              <input type="range" id="videoScrubber" min="0" max="100" value="0" class="w-full accent-brand-500 bg-slate-800 h-1.5 rounded-lg cursor-pointer">
            </div>

            <!-- Action Toolbar (Download, Fullscreen, API Keys) -->
            <div class="flex items-center space-x-2">
              <button onclick="downloadRenderedClip()" title="Download MP4 Video" class="glass-button p-2 rounded-lg text-slate-300 hover:text-white transition">
                <i data-lucide="download" class="w-4 h-4"></i>
              </button>
              <button onclick="openModal('apiModal')" title="Custom AI API Key Integration" class="glass-button p-2 rounded-lg text-slate-300 hover:text-white transition">
                <i data-lucide="key" class="w-4 h-4"></i>
              </button>
            </div>
          </div>

        </div>

      </div>
    </div>
  </section>

  <!-- Showcase / Community Gallery (Similar to VidOne Explore) -->
  <section id="templates" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16">
    <div class="flex flex-col md:flex-row md:items-end justify-between mb-8">
      <div>
        <h2 class="text-2xl sm:text-3xl font-bold text-white tracking-tight">Trending Community Creations</h2>
        <p class="text-slate-400 text-sm mt-1">Explore high-converting AI videos generated with VidOne 3.0 models</p>
      </div>
      <div class="mt-4 md:mt-0 flex items-center space-x-2">
        <button class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-brand-600 text-white">All Styles</button>
        <button class="px-3 py-1.5 rounded-lg text-xs font-semibold glass-button text-slate-300">Sci-Fi</button>
        <button class="px-3 py-1.5 rounded-lg text-xs font-semibold glass-button text-slate-300">Anime</button>
        <button class="px-3 py-1.5 rounded-lg text-xs font-semibold glass-button text-slate-300">Cinematic</button>
      </div>
    </div>

    <!-- Gallery Grid -->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
      
      <!-- Card 1 -->
      <div class="group bg-surface-card rounded-2xl overflow-hidden border border-slate-800 hover:border-brand-500/50 transition duration-300">
        <div class="relative aspect-video bg-slate-900 overflow-hidden">
          <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent z-10"></div>
          <div class="w-full h-full bg-indigo-950/40 flex items-center justify-center group-hover:scale-105 transition duration-500">
            <i data-lucide="sparkles" class="w-10 h-10 text-brand-400/40"></i>
          </div>
          <span class="absolute top-3 left-3 z-20 text-[10px] font-bold uppercase tracking-wider bg-black/70 px-2 py-0.5 rounded text-brand-400 border border-brand-500/30">Photorealistic</span>
          <button onclick="cloneTemplate('Ancient Indian warrior meditating on a Himalayan cliff with glowing runes, sunset rays, 4k ultra detail')" class="absolute bottom-3 right-3 z-20 opacity-0 group-hover:opacity-100 transition px-2.5 py-1 rounded-md bg-brand-600 text-white text-[11px] font-semibold flex items-center space-x-1">
            <i data-lucide="copy" class="w-3 h-3"></i>
            <span>Use Prompt</span>
          </button>
        </div>
        <div class="p-4">
          <h4 class="text-sm font-semibold text-white truncate">Himalayan Mystic Guardian</h4>
          <p class="text-xs text-slate-400 mt-1 line-clamp-2">"Ancient warrior meditating on Himalayan cliff with glowing runes and volumetric sunset rays..."</p>
        </div>
      </div>

      <!-- Card 2 -->
      <div class="group bg-surface-card rounded-2xl overflow-hidden border border-slate-800 hover:border-brand-500/50 transition duration-300">
        <div class="relative aspect-video bg-slate-900 overflow-hidden">
          <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent z-10"></div>
          <div class="w-full h-full bg-purple-950/40 flex items-center justify-center group-hover:scale-105 transition duration-500">
            <i data-lucide="zap" class="w-10 h-10 text-purple-400/40"></i>
          </div>
          <span class="absolute top-3 left-3 z-20 text-[10px] font-bold uppercase tracking-wider bg-black/70 px-2 py-0.5 rounded text-purple-400 border border-purple-500/30">Anime 2.0</span>
          <button onclick="cloneTemplate('Futuristic cyberpunk racer speeding on floating sky highway through Tokyo 2099, vibrant neon motion blur')" class="absolute bottom-3 right-3 z-20 opacity-0 group-hover:opacity-100 transition px-2.5 py-1 rounded-md bg-brand-600 text-white text-[11px] font-semibold flex items-center space-x-1">
            <i data-lucide="copy" class="w-3 h-3"></i>
            <span>Use Prompt</span>
          </button>
        </div>
        <div class="p-4">
          <h4 class="text-sm font-semibold text-white truncate">Neo-Tokyo Sky Hyperway</h4>
          <p class="text-xs text-slate-400 mt-1 line-clamp-2">"Cyberpunk hover racer speeding on floating skyway through Tokyo neon towers with rain streaks..."</p>
        </div>
      </div>

      <!-- Card 3 -->
      <div class="group bg-surface-card rounded-2xl overflow-hidden border border-slate-800 hover:border-brand-500/50 transition duration-300">
        <div class="relative aspect-video bg-slate-900 overflow-hidden">
          <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent z-10"></div>
          <div class="w-full h-full bg-cyan-950/40 flex items-center justify-center group-hover:scale-105 transition duration-500">
            <i data-lucide="film" class="w-10 h-10 text-cyan-400/40"></i>
          </div>
          <span class="absolute top-3 left-3 z-20 text-[10px] font-bold uppercase tracking-wider bg-black/70 px-2 py-0.5 rounded text-cyan-400 border border-cyan-500/30">Sci-Fi Cinema</span>
          <button onclick="cloneTemplate('First contact spacecraft descending silently through turbulent storm clouds over alien ocean, IMAX anamorphic')" class="absolute bottom-3 right-3 z-20 opacity-0 group-hover:opacity-100 transition px-2.5 py-1 rounded-md bg-brand-600 text-white text-[11px] font-semibold flex items-center space-x-1">
            <i data-lucide="copy" class="w-3 h-3"></i>
            <span>Use Prompt</span>
          </button>
        </div>
        <div class="p-4">
          <h4 class="text-sm font-semibold text-white truncate">Deep Abyss Extraterrestrial</h4>
          <p class="text-xs text-slate-400 mt-1 line-clamp-2">"Spacecraft descending silently through stormy clouds over an unknown planetary ocean..."</p>
        </div>
      </div>

      <!-- Card 4 -->
      <div class="group bg-surface-card rounded-2xl overflow-hidden border border-slate-800 hover:border-brand-500/50 transition duration-300">
        <div class="relative aspect-video bg-slate-900 overflow-hidden">
          <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent z-10"></div>
          <div class="w-full h-full bg-pink-950/40 flex items-center justify-center group-hover:scale-105 transition duration-500">
            <i data-lucide="heart" class="w-10 h-10 text-pink-400/40"></i>
          </div>
          <span class="absolute top-3 left-3 z-20 text-[10px] font-bold uppercase tracking-wider bg-black/70 px-2 py-0.5 rounded text-pink-400 border border-pink-500/30">Pixar 3D</span>
          <button onclick="cloneTemplate('Adorable baby red panda explorer carrying miniature backpack inside glowing fairy forest, gentle snowfall')" class="absolute bottom-3 right-3 z-20 opacity-0 group-hover:opacity-100 transition px-2.5 py-1 rounded-md bg-brand-600 text-white text-[11px] font-semibold flex items-center space-x-1">
            <i data-lucide="copy" class="w-3 h-3"></i>
            <span>Use Prompt</span>
          </button>
        </div>
        <div class="p-4">
          <h4 class="text-sm font-semibold text-white truncate">Tiny Forester Adventure</h4>
          <p class="text-xs text-slate-400 mt-1 line-clamp-2">"Cute red panda explorer wearing a backpack walking through a magical glowing mushroom woodland..."</p>
        </div>
      </div>

    </div>
  </section>

  <!-- Pricing Matrix Section (VidOne SaaS Architecture) -->
  <section id="pricing" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 border-t border-slate-800">
    <div class="text-center max-w-2xl mx-auto mb-12">
      <h2 class="text-3xl font-extrabold text-white">Transparent, Credit-Based Plans</h2>
      <p class="text-slate-400 text-sm mt-2">Generate short-form content, YouTube longform, or enterprise marketing campaigns</p>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      
      <!-- Starter Tier -->
      <div class="glass-panel rounded-2xl p-6 border border-slate-800 flex flex-col justify-between">
        <div>
          <div class="flex justify-between items-center mb-4">
            <h3 class="text-lg font-bold text-white">Starter Free</h3>
            <span class="text-xs px-2.5 py-1 rounded-full bg-slate-800 text-slate-300 font-medium">Free Forever</span>
          </div>
          <div class="text-3xl font-extrabold text-white mb-4">₹0 <span class="text-xs text-slate-400 font-normal">/ month</span></div>
          <ul class="space-y-3 text-xs text-slate-300 mb-6">
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-emerald-400"></i><span>100 Credits on Sign Up</span></li>
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-emerald-400"></i><span>Standard 720p HD Resolution</span></li>
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-emerald-400"></i><span>Hindi & English AI Narrations</span></li>
            <li class="flex items-center space-x-2 text-slate-500"><i data-lucide="x" class="w-4 h-4"></i><span>Commercial Resale Rights</span></li>
          </ul>
        </div>
        <button onclick="openModal('authModal')" class="w-full py-2.5 rounded-xl text-xs font-semibold glass-button text-white hover:text-white">Get Started</button>
      </div>

      <!-- Pro Creator Tier (Popular) -->
      <div class="glass-panel rounded-2xl p-6 border-2 border-brand-500 flex flex-col justify-between relative shadow-2xl shadow-brand-500/10">
        <div class="absolute -top-3 left-1/2 -translate-x-1/2 bg-gradient-to-r from-brand-600 to-brand-accent px-3 py-0.5 rounded-full text-[10px] font-bold text-white uppercase tracking-wider">
          Most Popular
        </div>
        <div>
          <div class="flex justify-between items-center mb-4">
            <h3 class="text-lg font-bold text-white">Pro Studio</h3>
            <span class="text-xs px-2.5 py-1 rounded-full bg-brand-500/20 text-brand-400 font-medium">For Creators</span>
          </div>
          <div class="text-3xl font-extrabold text-white mb-4">₹1,499 <span class="text-xs text-slate-400 font-normal">/ month</span></div>
          <ul class="space-y-3 text-xs text-slate-300 mb-6">
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-brand-400"></i><span>3,500 Credits per month</span></li>
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-brand-400"></i><span>Full 4K Ultra-HD Upscaling</span></li>
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-brand-400"></i><span>No Watermark on Downloads</span></li>
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-brand-400"></i><span>Unlimited Voice Clones (ElevenLabs)</span></li>
          </ul>
        </div>
        <button onclick="openModal('authModal')" class="w-full py-2.5 rounded-xl text-xs font-semibold bg-brand-600 hover:bg-brand-500 text-white shadow-lg shadow-brand-500/25">Upgrade to Pro</button>
      </div>

      <!-- Enterprise Tier -->
      <div class="glass-panel rounded-2xl p-6 border border-slate-800 flex flex-col justify-between">
        <div>
          <div class="flex justify-between items-center mb-4">
            <h3 class="text-lg font-bold text-white">Agency Max</h3>
            <span class="text-xs px-2.5 py-1 rounded-full bg-slate-800 text-slate-300 font-medium">Production</span>
          </div>
          <div class="text-3xl font-extrabold text-white mb-4">₹4,999 <span class="text-xs text-slate-400 font-normal">/ month</span></div>
          <ul class="space-y-3 text-xs text-slate-300 mb-6">
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-emerald-400"></i><span>15,000 Credits per month</span></li>
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-emerald-400"></i><span>Priority Dedicated GPU Queue</span></li>
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-emerald-400"></i><span>Full API Webhook Integration</span></li>
            <li class="flex items-center space-x-2"><i data-lucide="check" class="w-4 h-4 text-emerald-400"></i><span>Dedicated Account Manager</span></li>
          </ul>
        </div>
        <button onclick="openModal('authModal')" class="w-full py-2.5 rounded-xl text-xs font-semibold glass-button text-white">Contact Sales</button>
      </div>

    </div>
  </section>

  <!-- Footer -->
  <footer class="border-t border-slate-800 py-8 px-4 text-center text-xs text-slate-500">
    <p>© 2026 VidOne.ai Studio Architecture. Designed for next-generation cinematic content creation.</p>
  </footer>

  <!-- Modal 1: Custom API Keys Configuration -->
  <div id="apiModal" class="fixed inset-0 bg-black/80 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-surface-card border border-slate-700 w-full max-w-md rounded-2xl p-6 shadow-2xl">
      <div class="flex justify-between items-center mb-4">
        <h3 class="text-base font-bold text-white flex items-center space-x-2">
          <i data-lucide="key" class="w-4 h-4 text-brand-400"></i>
          <span>BYO AI Keys (Optional)</span>
        </h3>
        <button onclick="closeModal('apiModal')" class="text-slate-400 hover:text-white"><i data-lucide="x" class="w-5 h-5"></i></button>
      </div>
      <p class="text-xs text-slate-400 mb-4">You can connect your own cloud providers to use unlimited unmetered generations directly.</p>
      
      <div class="space-y-3">
        <div>
          <label class="block text-xs font-medium text-slate-300 mb-1">OpenAI API Key (GPT-4o Scripting)</label>
          <input type="password" id="openAiKey" class="w-full bg-slate-950 border border-slate-800 rounded-lg p-2.5 text-xs text-white" placeholder="sk-...">
        </div>
        <div>
          <label class="block text-xs font-medium text-slate-300 mb-1">ElevenLabs Key (Hyper-Realistic Voices)</label>
          <input type="password" id="elevenLabsKey" class="w-full bg-slate-950 border border-slate-800 rounded-lg p-2.5 text-xs text-white" placeholder="xi-...">
        </div>
        <div>
          <label class="block text-xs font-medium text-slate-300 mb-1">Replicate API Token (Video Diffusion)</label>
          <input type="password" id="replicateKey" class="w-full bg-slate-950 border border-slate-800 rounded-lg p-2.5 text-xs text-white" placeholder="r8_...">
        </div>
      </div>

      <div class="mt-6 flex justify-end space-x-3">
        <button onclick="closeModal('apiModal')" class="px-4 py-2 rounded-lg text-xs font-semibold glass-button text-slate-300">Cancel</button>
        <button onclick="saveApiKeys()" class="px-4 py-2 rounded-lg text-xs font-semibold bg-brand-600 text-white">Save Configuration</button>
      </div>
    </div>
  </div>

  <!-- Modal 2: Auth / Create Account Modal -->
  <div id="authModal" class="fixed inset-0 bg-black/80 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-surface-card border border-slate-700 w-full max-w-sm rounded-2xl p-6 shadow-2xl text-center">
      <div class="w-12 h-12 rounded-xl bg-gradient-to-tr from-brand-600 to-brand-accent flex items-center justify-center mx-auto mb-3">
        <i data-lucide="user-plus" class="w-6 h-6 text-white"></i>
      </div>
      <h3 class="text-lg font-bold text-white">Join VidOne Studio</h3>
      <p class="text-xs text-slate-400 mt-1 mb-6">Create an account to get 1,000 free rendering credits immediately.</p>

      <div class="space-y-3">
        <input type="email" placeholder="name@company.com" class="w-full bg-slate-950 border border-slate-800 rounded-lg p-3 text-xs text-white focus:border-brand-500 focus:outline-none">
        <input type="password" placeholder="Password" class="w-full bg-slate-950 border border-slate-800 rounded-lg p-3 text-xs text-white focus:border-brand-500 focus:outline-none">
        <button onclick="handleSimulatedAuth()" class="w-full py-3 rounded-lg text-xs font-bold bg-brand-600 hover:bg-brand-500 text-white shadow-md">Sign Up & Claim 1,000 Credits</button>
      </div>

      <button onclick="closeModal('authModal')" class="mt-4 text-xs text-slate-500 hover:underline">Close</button>
    </div>
  </div>

  <!-- Application Logic & Video Synthesis Engine -->
  <script>
    // Initialize Lucide icons
    lucide.createIcons();

    // App State
    let currentMode = 'text-to-video';
    let currentAspectRatio = '16-9';
    let isPlaying = false;
    let isGenerating = false;
    let renderFrame = 0;
    let animationLoopId = null;
    let currentPromptText = "";
    let credits = 1250;

    const canvas = document.getElementById('studioCanvas');
    const ctx = canvas.getContext('2d');
    const telemetryConsole = document.getElementById('telemetryConsole');
    const telemetryStatus = document.getElementById('telemetryStatus');
    const playerIdleNotice = document.getElementById('playerIdleNotice');
    const subtitleOverlay = document.getElementById('subtitleOverlay');
    const subtitleText = document.getElementById('subtitleText');

    // Sample prompts for quick exploration
    const samplePrompts = [
      "A futuristic supersonic bullet train piercing through the snowy Himalayan mountain pass at twilight, cinematic volumetric headlights, 4k 60fps.",
      "A glowing biomechanical panther walking through a dense rainforest with neon flora, anamorphic lens flare, deep bokeh.",
      "An astronaut discovering an ancient crystal temple beneath the surface of Mars, dramatic shadows, Hollywood CGI grading.",
      "A vintage 1970s rally sports car drifting along a rainy Tokyo coastal highway, reflections on asphalt, nostalgic 35mm film grain."
    ];

    function injectSamplePrompt() {
      const randomPrompt = samplePrompts[Math.floor(Math.random() * samplePrompts.length)];
      document.getElementById('promptInput').value = randomPrompt;
      logTelemetry(`Sample prompt loaded: "${randomPrompt.substring(0, 35)}..."`);
    }

    function cloneTemplate(prompt) {
      document.getElementById('promptInput').value = prompt;
      scrollToStudio();
      logTelemetry("Template prompt cloned into studio workstation.");
    }

    function scrollToStudio() {
      document.getElementById('studio').scrollIntoView({ behavior: 'smooth' });
    }

    // Modal Handlers
    function openModal(id) {
      document.getElementById(id).classList.remove('hidden');
    }
    function closeModal(id) {
      document.getElementById(id).classList.add('hidden');
    }

    function handleSimulatedAuth() {
      credits += 1000;
      document.getElementById('creditBalance').innerText = credits.toLocaleString();
      closeModal('authModal');
      alert("Welcome! 1,000 bonus credits added to your studio account.");
      logTelemetry("Authentication verified. 1,000 credits granted.");
    }

    function saveApiKeys() {
      localStorage.setItem('vidone_openai', document.getElementById('openAiKey').value);
      localStorage.setItem('vidone_eleven', document.getElementById('elevenLabsKey').value);
      localStorage.setItem('vidone_replicate', document.getElementById('replicateKey').value);
      closeModal('apiModal');
      logTelemetry("Custom API credentials saved locally.");
    }

    // Studio Mode Switching (Text vs Script vs Image)
    function setStudioMode(mode) {
      currentMode = mode;
      ['text-to-video', 'script-to-film', 'image-to-video'].forEach(m => {
        const btn = document.getElementById(`tab-${m}`);
        if (m === mode) {
          btn.className = "flex items-center space-x-2 px-4 py-2 rounded-lg text-xs font-semibold bg-brand-600 text-white shadow-sm transition";
        } else {
          btn.className = "flex items-center space-x-2 px-4 py-2 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition";
        }
      });

      const label = document.getElementById('inputLabel');
      const imgUpload = document.getElementById('imageUploadArea');

      if (mode === 'text-to-video') {
        label.innerText = "Describe Your Video Scene";
        imgUpload.classList.add('hidden');
      } else if (mode === 'script-to-film') {
        label.innerText = "Enter Short Film Storyboard / Screenplay";
        imgUpload.classList.add('hidden');
      } else if (mode === 'image-to-video') {
        label.innerText = "Motion Guidance & Animation Prompt";
        imgUpload.classList.remove('hidden');
      }
      logTelemetry(`Switched mode to [${mode.toUpperCase()}]`);
    }

    // Aspect Ratio Changer
    function setAspectRatio(ratio) {
      currentAspectRatio = ratio;
      ['16-9', '9-16', '1-1'].forEach(r => {
        const btn = document.getElementById(`ratio-${r}`);
        if (r === ratio) {
          btn.className = "p-1.5 rounded-lg text-brand-400 bg-brand-500/20 text-xs font-mono font-bold";
        } else {
          btn.className = "p-1.5 rounded-lg text-slate-400 hover:text-white text-xs font-mono font-bold";
        }
      });

      canvas.className = `w-full aspect-${ratio} object-contain bg-slate-950`;
      logTelemetry(`Canvas aspect ratio adjusted to ${ratio.replace('-', ':')}`);
    }

    // Logger
    function logTelemetry(msg) {
      telemetryConsole.innerHTML = `&gt; ${msg}`;
    }

    // Audio Engine: Cinematic FX Synthesizer
    function triggerAudioSynth() {
      try {
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();

        osc.type = 'sine';
        osc.frequency.setValueAtTime(80, audioCtx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(140, audioCtx.currentTime + 1.2);

        gain.gain.setValueAtTime(0.2, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 1.2);

        osc.connect(gain);
        gain.connect(audioCtx.destination);
        osc.start();
        osc.stop(audioCtx.currentTime + 1.2);
      } catch (e) {
        console.warn("AudioContext init postponed:", e);
      }
    }

    // Voiceover Synthesis Engine
    function playNarration(text, lang) {
      if (!('speechSynthesis' in window) || !document.getElementById('voiceToggle').checked) return;
      window.speechSynthesis.cancel();

      const utterance = new SpeechSynthesisUtterance(text);
      utterance.lang = lang;
      utterance.rate = 0.95;
      utterance.pitch = 1.0;

      // Select suitable voice
      const voices = window.speechSynthesis.getVoices();
      const matched = voices.find(v => v.lang.includes(lang.substring(0, 2)));
      if (matched) utterance.voice = matched;

      window.speechSynthesis.speak(utterance);
    }

    // Procedural Video Generation Simulation
    function startGenerationPipeline() {
      const prompt = document.getElementById('promptInput').value.trim();
      if (!prompt) {
        alert("Please provide a prompt or story description first!");
        return;
      }
      if (isGenerating) return;

      if (credits < 20) {
        alert("Insufficient credits! Please top up your balance.");
        return;
      }

      // Deduct credits
      credits -= 20;
      document.getElementById('creditBalance').innerText = credits.toLocaleString();

      currentPromptText = prompt;
      isGenerating = true;
      telemetryStatus.innerText = "RENDERING";
      telemetryStatus.className = "text-amber-400 font-bold animate-pulse";
      playerIdleNotice.classList.add('hidden');

      const overlay = document.getElementById('renderProgressOverlay');
      const progressBar = document.getElementById('progressBar');
      const progressPercent = document.getElementById('progressPercent');
      const stepTitle = document.getElementById('progressStepTitle');
      const stepSub = document.getElementById('progressSubTitle');

      overlay.classList.remove('hidden');

      const pipelineStages = [
        { pct: 20, title: "Parsing Prompt & Decomposing Storyboard...", sub: "Generating visual tokens and camera trajectories" },
        { pct: 50, title: "Diffusion Temporal Sampling...", sub: "Computing 24fps motion vectors across latent space" },
        { pct: 80, title: "Synthesizing Audio & Multilingual Voice...", sub: "Aligning speech phonemes with keyframes" },
        { pct: 100, title: "Finalizing 4K Video Stream...", sub: "Applying anamorphic color grading and export encode" }
      ];

      let currentStage = 0;
      const interval = setInterval(() => {
        if (currentStage < pipelineStages.length) {
          const s = pipelineStages[currentStage];
          progressBar.style.width = `${s.pct}%`;
          progressPercent.innerText = `${s.pct}%`;
          stepTitle.innerText = s.title;
          stepSub.innerText = s.sub;
          logTelemetry(s.title);
          currentStage++;
        } else {
          clearInterval(interval);
          setTimeout(() => {
            overlay.classList.add('hidden');
            isGenerating = false;
            telemetryStatus.innerText = "ONLINE";
            telemetryStatus.className = "text-emerald-400 font-bold";
            logTelemetry("Render complete. Initiating 4K canvas playback.");
            startVideoScenePlayback();
          }, 400);
        }
      }, 550);
    }

    // Video Canvas Render Loop
    function startVideoScenePlayback() {
      isPlaying = true;
      document.getElementById('playIcon').setAttribute('data-lucide', 'pause');
      lucide.createIcons();

      // Trigger narration and sound FX
      triggerAudioSynth();
      const lang = document.getElementById('voiceLanguage').value;
      const narration = currentPromptText.length > 120 ? currentPromptText.substring(0, 120) + "..." : currentPromptText;
      
      subtitleOverlay.classList.remove('hidden');
      subtitleText.innerText = `“${narration}”`;
      playNarration(narration, lang);

      // Particle simulation array for visual depth
      const numParticles = 80;
      const particles = Array.from({ length: numParticles }, () => ({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        z: Math.random() * 2 + 0.5,
        speed: Math.random() * 3 + 1,
        radius: Math.random() * 3 + 1,
        color: ['#818cf8', '#06b6d4', '#ec4899', '#38bdf8'][Math.floor(Math.random() * 4)]
      }));

      function draw() {
        if (!isPlaying) return;

        // Background motion gradient
        ctx.fillStyle = 'rgba(8, 10, 18, 0.22)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        const cameraMode = document.getElementById('cameraMotion').value;
        const horizon = canvas.height * 0.55;

        // 1. Grid Perspective Motion
        ctx.strokeStyle = 'rgba(99, 102, 241, 0.12)';
        ctx.lineWidth = 1;
        const gridSpeed = (renderFrame * 3) % 40;

        for (let x = -canvas.width; x < canvas.width * 2; x += 80) {
          ctx.beginPath();
          ctx.moveTo(canvas.width / 2, horizon);
          ctx.lineTo(x, canvas.height);
          ctx.stroke();
        }

        for (let y = horizon; y < canvas.height; y += 18) {
          ctx.beginPath();
          ctx.moveTo(0, y + gridSpeed);
          ctx.lineTo(canvas.width, y + gridSpeed);
          ctx.stroke();
        }

        // 2. Flying Neural Particles (Camera fly-through)
        particles.forEach(p => {
          ctx.fillStyle = p.color;
          ctx.beginPath();
          ctx.arc(p.x, p.y, p.radius * p.z, 0, Math.PI * 2);
          ctx.fill();

          p.y -= p.speed * 1.5;
          if (p.y < 0) {
            p.y = canvas.height;
            p.x = Math.random() * canvas.width;
          }
        });

        // 3. Focal Subject: Cinematic Pulsing Orb / Character Core
        const pulse = Math.sin(renderFrame * 0.05) * 20;
        const coreGrad = ctx.createRadialGradient(
          canvas.width / 2, horizon - 50, 10,
          canvas.width / 2, horizon - 50, 180 + pulse
        );
        coreGrad.addColorStop(0, 'rgba(236, 72, 153, 0.9)');
        coreGrad.addColorStop(0.4, 'rgba(99, 102, 241, 0.4)');
        coreGrad.addColorStop(1, 'transparent');

        ctx.fillStyle = coreGrad;
        ctx.beginPath();
        ctx.arc(canvas.width / 2, horizon - 50, 180 + pulse, 0, Math.PI * 2);
        ctx.fill();

        // 4. Cinema Anamorphic Bars (Top & Bottom)
        ctx.fillStyle = '#000000';
        ctx.fillRect(0, 0, canvas.width, 24);
        ctx.fillRect(0, canvas.height - 24, canvas.width, 24);

        // Update timeline progress
        renderFrame++;
        const durationSec = 5;
        const currentSec = Math.floor((renderFrame % (durationSec * 60)) / 60);
        document.getElementById('currentTimeDisplay').innerText = `00:0${currentSec}`;
        document.getElementById('videoScrubber').value = ((renderFrame % (durationSec * 60)) / (durationSec * 60)) * 100;

        animationLoopId = requestAnimationFrame(draw);
      }

      if (animationLoopId) cancelAnimationFrame(animationLoopId);
      renderFrame = 0;
      draw();
    }

    // Toggle Play/Pause
    function toggleVideoPlayback() {
      if (!currentPromptText) {
        alert("Please generate a video first!");
        return;
      }
      isPlaying = !isPlaying;
      const playIcon = document.getElementById('playIcon');
      if (isPlaying) {
        playIcon.setAttribute('data-lucide', 'pause');
        startVideoScenePlayback();
      } else {
        playIcon.setAttribute('data-lucide', 'play');
        if (animationLoopId) cancelAnimationFrame(animationLoopId);
        window.speechSynthesis.cancel();
      }
      lucide.createIcons();
    }

    // Video Download Simulation
    function downloadRenderedClip() {
      if (!currentPromptText) {
        alert("No generated clip available to download!");
        return;
      }
      const link = document.createElement('a');
      link.download = `VidOne_Cinematic_${Date.now()}.png`;
      link.href = canvas.toDataURL('image/png');
      link.click();
      logTelemetry("Frame render snapshot downloaded successfully.");
    }
  </script>
</body>
</html>
