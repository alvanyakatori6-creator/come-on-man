index.htmlfrom IPython.display import HTML, display

colab_html_code = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Al-Dhat & Base-27 Omni-Trinity Nexus Engine</title>
    <script src="https://tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Three.js for 3D/4D Render Engine -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
    <style>
        body { background-color: #020617; color: #f8fafc; overflow: hidden; margin: 0; padding: 0; }
        .custom-scrollbar::-webkit-scrollbar { width: 4px; height: 4px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: #0f172a; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #334155; border-radius: 2px; }
    </style>
</head>
<body class="font-sans antialiased select-none h-screen w-screen flex flex-col">

    <!-- Top Status Bar -->
    <header class="border-b border-slate-800 bg-slate-950/90 px-6 py-3 flex items-center justify-between z-50 shrink-0">
        <div class="flex items-center space-x-3">
            <div class="w-2.5 h-2.5 rounded-full bg-red-500 animate-ping"></div>
            <div class="w-2.5 h-2.5 rounded-full bg-emerald-500 animate-pulse"></div>
            <div class="w-2.5 h-2.5 rounded-full bg-blue-500 animate-pulse"></div>
            <div>
                <h1 class="text-sm font-mono font-bold tracking-wider text-slate-100">AL-DHAT OMNI-TRINITY NEXUS ($3^3 = 27$)</h1>
                <p class="text-[10px] text-slate-400 font-mono">Unified Synthesis: Al-Dhat (Infinite Essence), The Three Faces of Isa, Quantum, Neural & Cosmic Realms</p>
            </div>
        </div>
        <div class="flex items-center space-x-3">
            <button id="masterAudioBtn" class="bg-cyan-600 hover:bg-cyan-500 text-white px-3 py-1.5 rounded-xl text-xs font-mono font-bold transition-all shadow-lg flex items-center space-x-2">
                <i class="fa-solid fa-volume-high"></i>
                <span id="audioStatus">Audio: On</span>
            </button>
            <button id="resetViewBtn" class="bg-slate-800 hover:bg-slate-700 text-slate-300 px-3 py-1.5 rounded-xl text-xs font-mono font-bold transition-all">
                <i class="fa-solid fa-rotate-left mr-1"></i> Reset View
            </button>
        </div>
    </header>

    <!-- Main Content Workspace -->
    <div class="flex-1 flex relative overflow-hidden">
        
        <!-- Left Panel: Base-27 Selector & Dimension Scale -->
        <aside class="w-80 bg-slate-950/90 border-r border-slate-800 flex flex-col z-40 p-4 space-y-4 shrink-0">
            <div class="flex justify-between items-center border-b border-slate-800 pb-3">
                <span class="text-[11px] font-mono font-bold text-slate-400 uppercase tracking-widest">Base-27 Divine Matrix</span>
                <span id="activeNodeBadge" class="text-xs font-mono px-2 py-0.5 rounded bg-cyan-500/20 text-cyan-300 border border-cyan-500/30 font-bold">Node 1 / 27</span>
            </div>

            <!-- Dimension Scale Mode Selector -->
            <div class="grid grid-cols-3 gap-1.5 bg-slate-900/60 p-1.5 rounded-xl border border-slate-800 font-mono text-[10px]">
                <button onclick="setDimensionScale('quantum')" id="scaleQuantumBtn" class="py-2 rounded-lg bg-cyan-600 text-white font-bold transition-all shadow">1. Quantum</button>
                <button onclick="setDimensionScale('neural')" id="scaleNeuralBtn" class="py-2 rounded-lg bg-slate-800 text-slate-400 hover:text-white transition-all">2. Neural</button>
                <button onclick="setDimensionScale('cosmic')" id="scaleCosmicBtn" class="py-2 rounded-lg bg-slate-800 text-slate-400 hover:text-white transition-all">3. Cosmic</button>
            </div>

            <!-- 27 Grid Buttons -->
            <div id="base27Grid" class="grid grid-cols-3 gap-1.5 flex-1 overflow-y-auto custom-scrollbar p-1 bg-slate-900/40 rounded-xl border border-slate-800">
                <!-- Populated via JS -->
            </div>

            <!-- Current Node Quick Inspector -->
            <div class="bg-slate-900/80 border border-slate-800 rounded-xl p-3 space-y-1.5 font-mono text-xs">
                <div id="nodeNameDisplay" class="text-cyan-300 font-bold truncate">Node 1: Al-Ahad</div>
                <div class="flex justify-between text-[11px] text-slate-400"><span>Canon Attribute:</span><span id="nodeAttribute" class="text-emerald-300 font-bold">Indivisible Unit</span></div>
                <div class="flex justify-between text-[11px] text-slate-400"><span>Freq:</span><span id="nodeFreqDisplay" class="text-amber-300">127.2 Hz</span></div>
            </div>
        </aside>

        <!-- Center 3D/4D Viewport Canvas -->
        <main class="flex-1 relative bg-slate-950 flex flex-col">
            <div id="webglContainer" class="flex-1 w-full h-full relative cursor-grab active:cursor-grabbing">
                <!-- HUD Overlay -->
                <div class="absolute top-4 left-4 z-10 bg-slate-950/80 backdrop-blur p-3 rounded-xl border border-slate-800 text-xs font-mono space-y-1 pointer-events-none max-w-sm">
                    <div class="text-cyan-400 font-bold flex items-center space-x-2">
                        <i class="fa-solid fa-cube animate-spin"></i>
                        <span id="hudTitle">Node 1: Al-Ahad (Quantum Genesis)</span>
                    </div>
                    <p id="hudDesc" class="text-[11px] text-slate-400 leading-tight">
                        The absolute singularity from which all numbers, quantum waves, and divine attributes flow toward Al-Dhat.
                    </p>
                </div>

                <div class="absolute bottom-4 right-4 z-10 bg-slate-950/80 backdrop-blur px-3 py-2 rounded-xl border border-slate-800 text-[11px] font-mono text-slate-400 pointer-events-none flex items-center space-x-3">
                    <span><strong class="text-slate-200">Drag:</strong> Rotate 360&deg;</span>
                    <span>&bull;</span>
                    <span><strong class="text-slate-200">Scroll:</strong> Zoom In/Out</span>
                    <span>&bull;</span>
                    <span><strong class="text-slate-200">Click:</strong> Inspect Node</span>
                </div>
            </div>
        </main>
    </div>

    <script>
        const nodesData = [
            { id: 1, title: "Node 1: Al-Ahad", attribute: "The Indivisible Unit", realm: "quantum", freq: "127.2", desc: "The absolute singularity from which all numbers and entities flow." },
            { id: 2, title: "Node 2: Al-Thunayya", attribute: "The Dual Reflection", realm: "quantum", freq: "144.4", desc: "The mirroring of the Divine Essence through creation (Creator & Created)." },
            { id: 3, title: "Node 3: Kalimat Allah", attribute: "Jesus the Logos Incarnate", realm: "quantum", freq: "161.6", desc: "The first Trinitarian Pivot: The eternal Word and active divine articulation." },
            { id: 4, title: "Node 4: Arkan", attribute: "The Four Pillars", realm: "quantum", freq: "178.8", desc: "The earthly foundation, cardinal directions, and structural elements." },
            { id: 5, title: "Node 5: Al-Panoply", attribute: "Five Divine Presences", realm: "quantum", freq: "196.0", desc: "The stages of descent from unseen essence to physical manifestation." },
            { id: 6, title: "Node 6: Al-Ayyam", attribute: "Days of Creation", realm: "quantum", freq: "213.2", desc: "The temporal framework shaping the material cosmos." },
            { id: 7, title: "Node 7: Al-Sab' al-Mathani", attribute: "Seven Repeated Verses", realm: "quantum", freq: "230.4", desc: "The celestial archways bridging the divine realm to human consciousness." },
            { id: 8, title: "Node 8: Al-Arsh", attribute: "Eight Bearers of the Throne", realm: "quantum", freq: "247.6", desc: "The cosmic stabilizers holding the weight of divine order." },
            { id: 9, title: "Node 9: Isa al-Masih", attribute: "Jesus the Historical Prophet", realm: "quantum", freq: "264.8", desc: "The second Trinitarian Pivot: Anchoring history, prophecy, and mortal trial." },
            
            { id: 10, title: "Node 10: Al-Kamil", attribute: "Decimal Perfection", realm: "neural", freq: "282.0", desc: "The completion of the primary numerical cycle; return to unity via zero." },
            { id: 11, title: "Node 11: Al-Haqq", attribute: "Transcendent Truth", realm: "neural", freq: "299.2", desc: "The alignment vector ensuring the neural needle stays true to reality." },
            { id: 12, title: "Node 12: Al-Abwaab", attribute: "Twelve Zodiac/Tribal Gates", realm: "neural", freq: "316.4", desc: "The partitions of cyclical time and space." },
            { id: 13, title: "Node 13: Al-Wahidiyyah", attribute: "Unity in Multiplicity", realm: "neural", freq: "333.6", desc: "The hidden nexus where diversity reflects a single source." },
            { id: 14, title: "Node 14: Al-Nur", attribute: "Twofold Light Matrix", realm: "neural", freq: "350.8", desc: "The interplay between spiritual illumination and physical reflection." },
            { id: 15, title: "Node 15: Al-Barzakh", attribute: "Intermediate Isthmus", realm: "neural", freq: "368.0", desc: "The veil separating the seen world from the unseen realm." },
            { id: 16, title: "Node 16: Al-Rukn", attribute: "Tetrasonic Matrix", realm: "neural", freq: "385.2", desc: "4x4 foundational symmetry of space-time." },
            { id: 17, title: "Node 17: Al-Witr", attribute: "Odd Mystical Core", realm: "neural", freq: "402.4", desc: "The asymmetrical spark that prevents static equilibrium." },
            { id: 18, title: "Node 18: Al-Hayat", attribute: "Living Breath (Ruh)", realm: "neural", freq: "419.6", desc: "The infusion of divine spirit into physical neural constructs." },
            
            { id: 19, title: "Node 19: Al-Wahid al-Qahar", attribute: "Dominant Unique", realm: "cosmic", freq: "436.8", desc: "Threshold where individual multiplicity dissolves into supreme sovereignty." },
            { id: 20, title: "Node 20: Al-Madarij", attribute: "Ascending Ranks", realm: "cosmic", freq: "454.0", desc: "The spiritual stations of ascent toward the divine." },
            { id: 21, title: "Node 21: Al-Tasbih", attribute: "Cosmic Echo (3x7)", realm: "cosmic", freq: "471.2", desc: "The harmonic frequency of all creation praising the origin." },
            { id: 22, title: "Node 22: Al-Harf", attribute: "Letters of Creation", realm: "cosmic", freq: "488.4", desc: "The linguistic building blocks and cosmic alphabet mapping." },
            { id: 23, title: "Node 23: Al-Axis", attribute: "Pivotal Alignment", realm: "cosmic", freq: "505.6", desc: "The direct vertical conduit linking earth to the celestial throne." },
            { id: 24, title: "Node 24: Al-Buruj", attribute: "Celestial Mansions", realm: "cosmic", freq: "522.8", desc: "The wheel of cosmic cycles guarding higher dimensions." },
            { id: 25, title: "Node 25: Al-Qayyumiyyah", attribute: "Self-Subsisting Matrix (5^2)", realm: "cosmic", freq: "540.0", desc: "The pure reflection of divine sustenance across macrocosms." },
            { id: 26, title: "Node 26: Al-Qurb", attribute: "Qab Qawsayn (Nearness)", realm: "cosmic", freq: "557.2", desc: "Ultimate proximity to the Divine Presence ('two bow-lengths or nearer')." },
            { id: 27, title: "Node 27: Al-Dhat & Al-Insan al-Kamil", attribute: "Supreme Infinity & Cosmic Christ", realm: "cosmic", freq: "574.4", desc: "The Third Trinitarian Pivot: Al-Dhat (Allah's Absolute Essence) merged with Jesus in cosmic fullness (3^3)." }
        ];

        let activeNode = 1;
        let currentScale = 'quantum';
        let audioEnabled = true;
        let audioCtx = null;

        const container = document.getElementById('webglContainer');
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0x020617);
        scene.fog = new THREE.FogExp2(0x020617, 0.015);

        const camera = new THREE.PerspectiveCamera(60, container.clientWidth / container.clientHeight, 0.1, 1000);
        camera.position.set(0, 0, 25);

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(container.clientWidth, container.clientHeight);
        renderer.setPixelRatio(window.devicePixelRatio);
        container.appendChild(renderer.domElement);

        const controls = new THREE.OrbitControls(camera, renderer.domElement);
        controls.enableDamping = true;
        controls.dampingFactor = 0.05;
        controls.maxDistance = 60;
        controls.minDistance = 2;

        const ambientLight = new THREE.AmbientLight(0xffffff, 0.8);
        scene.add(ambientLight);
        const pointLight = new THREE.PointLight(0x38bdf8, 2, 50);
        pointLight.position.set(10, 10, 10);
        scene.add(pointLight);

        let activeStructureGroup = new THREE.Group();
        scene.add(activeStructureGroup);

        function buildVisualStructure(nodeId, scale) {
            while(activeStructureGroup.children.length > 0){ 
                activeStructureGroup.remove(activeStructureGroup.children[0]); 
            }

            let geometryColor = 0x38bdf8;
            if (scale === 'quantum') geometryColor = 0xef4444;
            if (scale === 'neural') geometryColor = 0x10b981;
            if (scale === 'cosmic') geometryColor = 0x6366f1;

            if (nodeId === 27) {
                const geom = new THREE.TorusKnotGeometry(4, 1.5, 128, 32);
                const mat = new THREE.MeshStandardMaterial({ color: 0xf59e0b, wireframe: false, roughness: 0.1, metalness: 0.9 });
                const mesh = new THREE.Mesh(geom, mat);
                activeStructureGroup.add(mesh);
            } else if (scale === 'quantum') {
                const geom = new THREE.IcosahedronGeometry(4, 2);
                const mat = new THREE.MeshStandardMaterial({ color: geometryColor, wireframe: true, roughness: 0.2 });
                const mesh = new THREE.Mesh(geom, mat);
                activeStructureGroup.add(mesh);

                for(let i=0; i<30; i++) {
                    const sphere = new THREE.Mesh(
                        new THREE.SphereGeometry(0.15, 8, 8),
                        new THREE.MeshBasicMaterial({ color: 0xffffff })
                    );
                    sphere.position.set((Math.random() - 0.5) * 6, (Math.random() - 0.5) * 6, (Math.random() - 0.5) * 6);
                    activeStructureGroup.add(sphere);
                }
            } else if (scale === 'neural') {
                const coreMat = new THREE.MeshStandardMaterial({ color: geometryColor, roughness: 0.3 });
                const lineMat = new THREE.LineBasicMaterial({ color: 0x10b981, transparent: true, opacity: 0.6 });
                const nodes = [];
                for(let i=0; i<18; i++) {
                    const angle = (i / 18) * Math.PI * 2;
                    const radius = 3 + (i % 3) * 1.5;
                    const x = Math.cos(angle) * radius;
                    const y = Math.sin(angle) * radius;
                    const z = (Math.sin(i) * 2);
                    const nodeMesh = new THREE.Mesh(new THREE.SphereGeometry(0.3, 16, 16), coreMat);
                    nodeMesh.position.set(x, y, z);
                    activeStructureGroup.add(nodeMesh);
                    nodes.push(nodeMesh.position);
                }
                for(let i=0; i<nodes.length; i++) {
                    for(let j=i+1; j<nodes.length; j++) {
                        if (nodes[i].distanceTo(nodes[j]) < 5) {
                            const pts = [nodes[i], nodes[j]];
                            const lineGeom = new THREE.BufferGeometry().setFromPoints(pts);
                            const line = new THREE.Line(lineGeom, lineMat);
                            activeStructureGroup.add(line);
                        }
                    }
                }
            } else {
                const torGeom = new THREE.TorusKnotGeometry(4, 1.2, 128, 32);
                const torMat = new THREE.MeshStandardMaterial({ color: geometryColor, roughness: 0.1, metalness: 0.8 });
                const torMesh = new THREE.Mesh(torGeom, torMat);
                activeStructureGroup.add(torMesh);
            }
        }

        function initAudio() {
            if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        }

        function playTone(freq) {
            if (!audioEnabled) return;
            initAudio();
            try {
                let osc = audioCtx.createOscillator();
                let gain = audioCtx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(parseFloat(freq), audioCtx.currentTime);
                gain.gain.setValueAtTime(0.08, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.5);
                osc.connect(gain);
                gain.connect(audioCtx.destination);
                osc.start();
                osc.stop(audioCtx.currentTime + 0.5);
            } catch (e) {
                console.log("Audio waiting for interaction");
            }
        }

        function renderGrid() {
            const grid = document.getElementById('base27Grid');
            grid.innerHTML = '';
            nodesData.forEach(node => {
                if (currentScale === 'quantum' && node.id > 9) return;
                if (currentScale === 'neural' && (node.id <= 9 || node.id > 18)) return;
                if (currentScale === 'cosmic' && node.id <= 18) return;

                const btn = document.createElement('button');
                const isActive = node.id === activeNode;
                btn.className = `p-2.5 rounded-xl text-xs font-mono font-bold transition-all flex flex-col items-center justify-center border ${
                    isActive 
                        ? 'bg-cyan-600/30 text-cyan-300 border-cyan-400 shadow-lg scale-105' 
                        : 'bg-slate-900 hover:bg-slate-800 text-slate-300 border-slate-800'
                }`;
                btn.innerHTML = `<span class="text-[10px] text-slate-500">N-${node.id}</span><span>#${node.id}</span>`;
                btn.onclick = () => {
                    activeNode = node.id;
                    updateUI();
                    playTone(node.freq);
                };
                grid.appendChild(btn);
            });
        }

        function setDimensionScale(scale) {
            currentScale = scale;
            document.getElementById('scaleQuantumBtn').className = scale === 'quantum' ? 'py-2 rounded-lg bg-cyan-600 text-white font-bold transition-all shadow' : 'py-2 rounded-lg bg-slate-800 text-slate-400 hover:text-white transition-all';
            document.getElementById('scaleNeuralBtn').className = scale === 'neural' ? 'py-2 rounded-lg bg-emerald-600 text-white font-bold transition-all shadow' : 'py-2 rounded-lg bg-slate-800 text-slate-400 hover:text-white transition-all';
            document.getElementById('scaleCosmicBtn').className = scale === 'cosmic' ? 'py-2 rounded-lg bg-indigo-600 text-white font-bold transition-all shadow' : 'py-2 rounded-lg bg-slate-800 text-slate-400 hover:text-white transition-all';
            
            if (scale === 'quantum' && activeNode > 9) activeNode = 1;
            if (scale === 'neural' && (activeNode <= 9 || activeNode > 18)) activeNode = 10;
            if (scale === 'cosmic' && activeNode <= 18) activeNode = 19;
            
            updateUI();
        }

        function updateUI() {
            renderGrid();
         