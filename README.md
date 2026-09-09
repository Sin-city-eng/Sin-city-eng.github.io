<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rattasurd Sirasen (Sin) | Y2K Metallic Portfolio</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@700;900&family=Orbitron:wght@700;900&family=Prompt:wght@300;400;600&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            cursor: none; /* Hide default cursor */
        }

        body {
            background-color: #030303;
            color: #ffffff;
            font-family: 'Prompt', sans-serif;
            overflow-x: hidden;
            background-image: radial-gradient(rgba(255, 255, 255, 0.15) 1px, transparent 1px);
            background-size: 8px 8px; /* Dotted Halftone Pattern background */
        }

        /* WebGL Background */
        #webgl-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 1;
            pointer-events: none;
        }

        /* Y2K Custom Chrome Cursor */
        #custom-cursor {
            position: fixed;
            width: 32px;
            height: 32px;
            pointer-events: none;
            z-index: 9999;
            transform: translate(-50%, -50%);
            transition: transform 0.05s ease-out;
            filter: drop-shadow(0 0 8px rgba(255, 255, 255, 0.9));
        }

        #custom-cursor::before {
            content: '✦';
            position: absolute;
            font-size: 24px;
            color: #ffffff;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-shadow: 0 0 10px #ffffff, 0 0 20px #808080;
        }

        /* Single Page Scroll Overlay */
        .scroll-container {
            position: relative;
            z-index: 10;
            width: 100%;
        }

        .section {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 4rem 2rem;
            position: relative;
        }

        /* Y2K Chrome Metal Card with Tribal Sharp Edges */
        .chrome-card {
            background: rgba(10, 10, 12, 0.65);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            /* Tribal Sharp Corner Cuts */
            clip-path: polygon(0 15px, 15px 0, 100% 0, 100% calc(100% - 15px), calc(100% - 15px) 100%, 0 100%);
            padding: 3rem;
            max-width: 850px;
            width: 90%;
            box-shadow: 0 0 40px rgba(0, 0, 0, 0.9), inset 0 0 15px rgba(255, 255, 255, 0.2);
            position: relative;
            transition: transform 0.3s ease, border-color 0.3s ease;
        }

        .chrome-card:hover {
            border-color: #ffffff;
            transform: scale(1.01);
        }

        /* Metallic Acid Typography */
        .chrome-title {
            font-family: 'Cinzel', serif;
            font-weight: 900;
            text-transform: uppercase;
            font-size: clamp(3rem, 8vw, 5.5rem);
            line-height: 1;
            letter-spacing: 4px;
            background: linear-gradient(180deg, #ffffff 0%, #d4d4d4 35%, #4a4a4a 48%, #ffffff 52%, #888888 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 0 15px rgba(255, 255, 255, 0.6));
            margin-bottom: 0.5rem;
        }

        .subtitle {
            font-family: 'Orbitron', sans-serif;
            color: #e0e0e0;
            letter-spacing: 3px;
            font-size: 1.1rem;
            margin-bottom: 2rem;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
        }

        p {
            line-height: 1.8;
            color: #d1d1d1;
            font-weight: 300;
            font-size: 1.1rem;
            margin-bottom: 1.5rem;
        }

        /* Y2K Star Elements */
        .y2k-star-icon {
            position: absolute;
            font-size: 2rem;
            color: #ffffff;
            filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.9));
            animation: rotateStar 4s infinite linear;
        }

        @keyframes rotateStar {
            0% { transform: rotate(0deg) scale(0.9); }
            50% { transform: rotate(180deg) scale(1.1); }
            100% { transform: rotate(360deg) scale(0.9); }
        }

        .tag-badge {
            display: inline-block;
            padding: 0.5rem 1.2rem;
            background: rgba(255, 255, 255, 0.08);
            border: 1px solid rgba(255, 255, 255, 0.4);
            color: #ffffff;
            font-size: 0.85rem;
            font-family: 'Orbitron', sans-serif;
            margin-right: 0.5rem;
            margin-bottom: 0.5rem;
            letter-spacing: 1px;
            clip-path: polygon(8px 0, 100% 0, 100% calc(100% - 8px), calc(100% - 8px) 100%, 0 100%, 0 8px);
        }

        .scroll-hint {
            position: absolute;
            bottom: 2rem;
            left: 50%;
            transform: translateX(-50%);
            font-family: 'Orbitron', sans-serif;
            font-size: 0.85rem;
            letter-spacing: 4px;
            color: #aaaaaa;
            text-shadow: 0 0 8px rgba(255, 255, 255, 0.5);
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translate(-50%, 0); }
            40% { transform: translate(-50%, -10px); }
            60% { transform: translate(-50%, -5px); }
        }

        .btn-chrome {
            display: inline-block;
            margin-top: 1rem;
            padding: 0.8rem 2rem;
            color: #000;
            background: linear-gradient(180deg, #ffffff 0%, #b0b0b0 100%);
            font-family: 'Orbitron', sans-serif;
            font-weight: 900;
            text-decoration: none;
            letter-spacing: 2px;
            border: none;
            clip-path: polygon(10px 0, 100% 0, 100% calc(100% - 10px), calc(100% - 10px) 100%, 0 100%, 0 10px);
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.6);
            transition: all 0.3s ease;
        }

        .btn-chrome:hover {
            background: #ffffff;
            box-shadow: 0 0 25px rgba(255, 255, 255, 1);
            transform: translateY(-2px);
        }
    </style>
    <!-- Three.js Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

    <!-- Y2K Custom Chrome Mouse Cursor -->
    <div id="custom-cursor"></div>

    <!-- 3D Canvas Background -->
    <div id="webgl-container"></div>

    <!-- Single Page Scroll Content -->
    <div class="scroll-container">

        <!-- SECTION 1: HERO PORTFOLIO -->
        <section class="section">
            <div class="chrome-card" style="text-align: center;">
                <span class="y2k-star-icon" style="top: -10px; left: -10px;">✦</span>
                <span class="y2k-star-icon" style="bottom: -10px; right: -10px;">✦</span>
                <h1 class="chrome-title">PORTFOLIO</h1>
                <div class="subtitle">RATTASURD SIRASEN — "SIN"</div>
                <p style="font-weight: 600; letter-spacing: 2px; color: #ffffff;">INTERN 3D ARTIST / CONCEPT DESIGNER</p>
                <div style="margin-top: 1.5rem;">
                    <span class="tag-badge">CHROME AESTHETIC</span>
                    <span class="tag-badge">CYBERPUNK DESIGN</span>
                    <span class="tag-badge">3D COMPOSITION</span>
                </div>
            </div>
            <div class="scroll-hint">▼ SCROLL TO EXPLORE WORK ▼</div>
        </section>

        <!-- SECTION 2: ABOUT / STYLE CONCEPT -->
        <section class="section">
            <div class="chrome-card">
                <span class="y2k-star-icon" style="top: 15px; right: 20px;">✦</span>
                <h2 class="chrome-title" style="font-size: clamp(2rem, 5vw, 3.5rem);">01 / AESTHETIC</h2>
                <div class="subtitle">Y2K / METALLIC ACID GRAPHIC CONCEPT</div>
                <p>
                    เน้นการนำเสนอผ่านงานภาพสไตล์ <strong>Y2K Chrome Metallic</strong> ที่มีเอกลักษณ์จากเส้นสายรูปทรงโลหะไหลเงาวาว (Liquid Chrome Shapes), ลายกราฟิกวิวัฒน์มุมแหลม (Tribal Sharp Edges) ผสานกับฉากหลัง Dotted Halftone Pattern และการจัดวางองค์ประกอบแบบ 3D Composition คุณภาพสูง
                </p>
            </div>
        </section>

        <!-- SECTION 3: FEATURED PROJECTS -->
        <section class="section">
            <div class="chrome-card">
                <span class="y2k-star-icon" style="bottom: 15px; left: 20px;">✦</span>
                <h2 class="chrome-title" style="font-size: clamp(2rem, 5vw, 3.5rem);">02 / PROJECTS</h2>
                <div class="subtitle">FEATURED 3D & DIGITAL COMPOSITIONS</div>
                <p>
                    <strong>• Cyberpunk Thai Literature (Phra Aphai Mani):</strong> ออกแบบปกเกมและโลโก้ในธีมอนาคต Cyberpunk โดยประยุกต์องค์ประกอบจากวรรณคดีไทย (พระอภัยมณีเป่าปี่)<br><br>
                    <strong>• Medieval Costume Face-Swap & T-Pose:</strong> งานดัดแปลงใบหน้า ตัดต่อเครื่องแต่งกายยุคกลาง และการจัดองค์ประกอบ 3D Asset
                </p>
                <a href="https://www.canva.com/design/DAHUTknG0rs/DZgmxJ9zg1hgUz_mbBs_tA/edit" target="_blank" class="btn-chrome">
                    VIEW CANVA PRESENTATION ✦
                </a>
            </div>
        </section>

        <!-- SECTION 4: CONTACT -->
        <section class="section">
            <div class="chrome-card" style="text-align: center;">
                <h2 class="chrome-title" style="font-size: clamp(2rem, 5vw, 3.5rem);">03 / CONTACT</h2>
                <div class="subtitle">GET IN TOUCH FOR INTERNSHIP</div>
                <p>พร้อมสร้างสรรค์งานออกแบบ 3D VisCom / Graphic Design คุณภาพสูงร่วมกับทีม</p>
                <div class="tag-badge" style="font-size: 1rem; padding: 0.8rem 2rem;">NAME: RATTASURD SIRASEN (SIN)</div>
            </div>
        </section>

    </div>

    <script>
        // --- 1. CUSTOM MOUSE CURSOR TRACKING ---
        const cursor = document.getElementById('custom-cursor');
        let mouseX = 0, mouseY = 0;
        let cursorX = 0, cursorY = 0;

        window.addEventListener('mousemove', (e) => {
            mouseX = e.clientX;
            mouseY = e.clientY;
        });

        function updateCursor() {
            cursorX += (mouseX - cursorX) * 0.25;
            cursorY += (mouseY - cursorY) * 0.25;
            cursor.style.left = `${cursorX}px`;
            cursor.style.top = `${cursorY}px`;
            requestAnimationFrame(updateCursor);
        }
        updateCursor();

        // --- 2. THREE.JS SCENE SETUP ---
        const container = document.getElementById('webgl-container');
        const scene = new THREE.Scene();
        scene.fog = new THREE.FogExp2(0x030303, 0.03);

        const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(0, 0, 8);

        const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
        container.appendChild(renderer.domElement);

        // --- 3. HIGH-GLOSS METALLIC CHROME MATERIAL ---
        // Creating a reflective envMap gradient using Canvas Texture for Chrome Reflection
        const canvas = document.createElement('canvas');
        canvas.width = 512;
        canvas.height = 512;
        const ctx = canvas.getContext('2d');
        const gradient = ctx.createLinearGradient(0, 0, 0, 512);
        gradient.addColorStop(0.0, '#ffffff');
        gradient.addColorStop(0.3, '#888888');
        gradient.addColorStop(0.5, '#111111');
        gradient.addColorStop(0.7, '#ffffff');
        gradient.addColorStop(1.0, '#222222');
        ctx.fillStyle = gradient;
        ctx.fillRect(0, 0, 512, 512);

        const envTexture = new THREE.CanvasTexture(canvas);
        envTexture.mapping = THREE.EquirectangularReflectionMapping;

        const chromeMaterial = new THREE.MeshStandardMaterial({
            color: 0xffffff,
            metalness: 1.0,
            roughness: 0.05,
            envMap: envTexture,
            envMapIntensity: 2.5
        });

        // --- 4. 3D OBJECTS (Y2K Chrome Ring / Bulbs / Stars) ---
        // Main Liquid Chrome Oval Shape (Torus Knot)
        const chromeShapeGeo = new THREE.TorusKnotGeometry(2.2, 0.35, 128, 32, 2, 3);
        const chromeMesh = new THREE.Mesh(chromeShapeGeo, chromeMaterial);
        scene.add(chromeMesh);

        // Floating Y2K 3D Star Objects
        function createStarGeometry() {
            const shape = new THREE.Shape();
            const points = 5;
            const outerRadius = 0.8;
            const innerRadius = 0.3;
            
            for (let i = 0; i < points * 2; i++) {
                const radius = i % 2 === 0 ? outerRadius : innerRadius;
                const angle = (i / (points * 2)) * Math.PI * 2;
                const x = Math.cos(angle) * radius;
                const y = Math.sin(angle) * radius;
                if (i === 0) shape.moveTo(x, y);
                else shape.lineTo(x, y);
            }
            shape.closePath();

            const extrudeSettings = { depth: 0.2, bevelEnabled: true, bevelSegments: 3, steps: 1, bevelSize: 0.1, bevelThickness: 0.1 };
            return new THREE.ExtrudeGeometry(shape, extrudeSettings);
        }

        const starGeo = createStarGeometry();
        const starMesh1 = new THREE.Mesh(starGeo, chromeMaterial);
        starMesh1.position.set(-3.5, 2.2, -1);
        starMesh1.scale.set(0.8, 0.8, 0.8);
        scene.add(starMesh1);

        const starMesh2 = new THREE.Mesh(starGeo, chromeMaterial);
        starMesh2.position.set(3.5, -2.0, -1);
        starMesh2.scale.set(0.6, 0.6, 0.6);
        scene.add(starMesh2);

        // Hanging Chrome Bulbs (Right Top corner like Canva reference)
        const bulbGroup = new THREE.Group();
        for (let i = 0; i < 3; i++) {
            const bulbGeo = new THREE.SphereGeometry(0.25, 32, 32);
            const bulbMesh = new THREE.Mesh(bulbGeo, chromeMaterial);
            bulbMesh.position.set(i * 0.4, -i * 0.3, 0);
            bulbGroup.add(bulbMesh);
        }
        bulbGroup.position.set(3.2, 2.8, 0);
        scene.add(bulbGroup);

        // --- 5. LIGHTING ---
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.8);
        scene.add(ambientLight);

        const dirLight1 = new THREE.DirectionalLight(0xffffff, 2.5);
        dirLight1.position.set(5, 10, 7);
        scene.add(dirLight1);

        const dirLight2 = new THREE.DirectionalLight(0xffffff, 1.5);
        dirLight2.position.set(-5, -5, -5);
        scene.add(dirLight2);

        // --- 6. SCROLL & MOUSE ANIMATION LOGIC ---
        let targetScrollY = 0;

        window.addEventListener('scroll', () => {
            targetScrollY = window.scrollY;
        });

        function animate() {
            requestAnimationFrame(animate);

            const scrollPercent = targetScrollY / (document.documentElement.scrollHeight - window.innerHeight);

            // Rotate Main Chrome Shape based on Scroll and Time
            chromeMesh.rotation.x = scrollPercent * Math.PI * 2 + Date.now() * 0.0005;
            chromeMesh.rotation.y = scrollPercent * Math.PI * 3 + Date.now() * 0.0008;

            // Mouse Parallax for Objects
            const targetX = (mouseX / window.innerWidth - 0.5) * 1.5;
            const targetY = -(mouseY / window.innerHeight - 0.5) * 1.5;

            chromeMesh.position.x += (targetX - chromeMesh.position.x) * 0.05;
            chromeMesh.position.y += (targetY - chromeMesh.position.y) * 0.05;

            // Stars rotation
            starMesh1.rotation.z += 0.01;
            starMesh2.rotation.z -= 0.012;

            // Camera Zoom Effect on Scroll
            camera.position.z = 8 - (scrollPercent * 3);

            renderer.render(scene, camera);
        }

        animate();

        // Window Resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
