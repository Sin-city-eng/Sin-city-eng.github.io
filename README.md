# Sin-city-eng.github.io
```html
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rattasurd Sirasen (Sin) | 3D Portfolio</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@700&family=Orbitron:wght@500;800;900&family=Prompt:wght@300;400;600&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            cursor: none; /* Hide default cursor for custom chrome cursor */
        }

        body {
            background-color: #050505;
            color: #ffffff;
            font-family: 'Prompt', sans-serif;
            overflow-x: hidden;
        }

        /* WebGL Background Canvas */
        #webgl-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 1;
            pointer-events: none;
        }

        /* Y2K Custom Chrome Mouse Cursor */
        #custom-cursor {
            position: fixed;
            width: 24px;
            height: 24px;
            border: 2px solid #e0e0e0;
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            transform: translate(-50%, -50%);
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.8), inset 0 0 8px rgba(0, 255, 204, 0.6);
            transition: transform 0.1s ease-out, width 0.2s, height 0.2s;
        }

        #custom-cursor::after {
            content: '✦';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 10px;
            color: #00ffcc;
        }

        /* Scrollable Overlay Content */
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

        /* Y2K Chrome Glass Card Style */
        .chrome-card {
            background: rgba(15, 15, 18, 0.55);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 16px;
            padding: 2.5rem;
            max-width: 800px;
            width: 90%;
            box-shadow: 0 0 30px rgba(0, 0, 0, 0.8), 
                        inset 0 0 15px rgba(255, 255, 255, 0.1);
            position: relative;
            overflow: hidden;
            transition: transform 0.3s ease, border-color 0.3s ease;
        }

        .chrome-card:hover {
            border-color: rgba(0, 255, 204, 0.6);
            transform: translateY(-5px);
        }

        /* Chrome Metallic Title Style */
        .chrome-text {
            font-family: 'Orbitron', sans-serif;
            font-weight: 900;
            text-transform: uppercase;
            background: linear-gradient(180deg, #ffffff 0%, #a6a6a6 45%, #3a3a3a 50%, #e2e2e2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 0 12px rgba(255, 255, 255, 0.4));
            letter-spacing: 3px;
        }

        h1.chrome-text {
            font-size: clamp(2.5rem, 6vw, 4.5rem);
            margin-bottom: 0.5rem;
        }

        h2.chrome-text {
            font-size: clamp(1.8rem, 4vw, 2.5rem);
            margin-bottom: 1.5rem;
        }

        .subtitle {
            font-family: 'Cinzel', serif;
            color: #00ffcc;
            letter-spacing: 2px;
            font-size: 1.1rem;
            margin-bottom: 2rem;
            text-shadow: 0 0 8px rgba(0, 255, 204, 0.6);
        }

        p {
            line-height: 1.8;
            color: #cccccc;
            font-weight: 300;
            font-size: 1.05rem;
            margin-bottom: 1.5rem;
        }

        /* Y2K Graphic Elements */
        .y2k-star {
            position: absolute;
            color: #ffffff;
            font-size: 1.5rem;
            opacity: 0.7;
            animation: pulse 2s infinite alternate;
        }

        @keyframes pulse {
            0% { transform: scale(0.8) rotate(0deg); opacity: 0.4; }
            100% { transform: scale(1.2) rotate(45deg); opacity: 1; filter: drop-shadow(0 0 8px #00ffcc); }
        }

        .grid-tag {
            display: inline-block;
            padding: 0.4rem 1rem;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(0, 255, 204, 0.4);
            color: #00ffcc;
            font-size: 0.85rem;
            font-family: 'Orbitron', sans-serif;
            border-radius: 4px;
            margin-right: 0.5rem;
            margin-bottom: 0.5rem;
        }

        .scroll-down-hint {
            position: absolute;
            bottom: 2rem;
            left: 50%;
            transform: translateX(-50%);
            font-family: 'Orbitron', sans-serif;
            font-size: 0.8rem;
            letter-spacing: 3px;
            color: #888;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translate(-50%, 0); }
            40% { transform: translate(-50%, -10px); }
            60% { transform: translate(-50%, -5px); }
        }
    </style>
    <!-- Three.js Libraries -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

    <!-- Custom Y2K Cursor -->
    <div id="custom-cursor"></div>

    <!-- WebGL Canvas Background -->
    <div id="webgl-container"></div>

    <!-- Single Page Scrollable Content -->
    <div class="scroll-container">

        <!-- SECTION 1: HERO -->
        <section class="section">
            <div class="chrome-card" style="text-align: center;">
                <span class="y2k-star" style="top: 15px; left: 20px;">✦</span>
                <span class="y2k-star" style="bottom: 15px; right: 20px;">✦</span>
                <h1 class="chrome-text">PORTFOLIO</h1>
                <div class="subtitle">RATTASURD SIRASEN — "SIN"</div>
                <p>INTERN 3D ARTIST & CONCEPT DESIGNER</p>
                <div>
                    <span class="grid-tag">3D COMPOSITION</span>
                    <span class="grid-tag">CYBERPUNK</span>
                    <span class="grid-tag">4D MATH ART</span>
                </div>
            </div>
            <div class="scroll-down-hint">▼ SCROLL TO EXPLORE LIMINAL SPACE ▼</div>
        </section>

        <!-- SECTION 2: CONCEPT & THEME -->
        <section class="section">
            <div class="chrome-card">
                <span class="y2k-star" style="top: 15px; right: 20px;">✦</span>
                <h2 class="chrome-text">01 / CONCEPT</h2>
                <div class="subtitle">LIMINAL SPACE x HYPERDIMENSION</div>
                <p>
                    งานออกแบบชิ้นนี้จำลองบรรยากาศความอ้างว้างอันเงียบสงบในสไตล์ <strong>Liminal Space</strong> 
                    ตัดสลับ (Contrast) ด้วยโครงสร้างคณิตศาสตร์ไร้ขอบเขตของ <strong>4D Tesseract (Hypercube)</strong> 
                    เรืองแสงสีนีออนที่หมุนวนอยู่ตรงปลายทางเดินเพื่อสร้างมิติทางสายตาที่ไม่เหมือนใคร
                </p>
            </div>
        </section>

        <!-- SECTION 3: FEATURED PROJECTS -->
        <section class="section">
            <div class="chrome-card">
                <span class="y2k-star" style="bottom: 15px; left: 20px;">✦</span>
                <h2 class="chrome-text">02 / PROJECTS</h2>
                <div class="subtitle">CYBERPUNK THAI LITERATURE & FACE SWAP</div>
                <p>
                    <strong>• Phra Aphai Mani Cyberpunk Edition:</strong> งานออกแบบโลโก้และปกเกมผสมผสานวรรณคดีไทย (พระอภัยมณีเป่าปี่) เข้ากับโลกอนาคตสไตล์ Cyberpunk<br>
                    <strong>• Character Face-Swap & T-Pose Composition:</strong> งานตัดต่อและดัดแปลงเครื่องแต่งกายตัวละคร ยุคกลาง และเอฟเฟกต์ภาพเชิงดิจิทัล
                </p>
                <div style="margin-top: 1.5rem;">
                    <a href="https://www.canva.com/design/DAHUTknG0rs/DZgmxJ9zg1hgUz_mbBs_tA/edit" target="_blank" style="color: #00ffcc; text-decoration: none; font-family: 'Orbitron', sans-serif; font-weight: 600;">
                        [ OPEN CANVA PRESENTATION ✦ ]
                    </a>
                </div>
            </div>
        </section>

        <!-- SECTION 4: CONTACT -->
        <section class="section">
            <div class="chrome-card" style="text-align: center;">
                <h2 class="chrome-text">03 / CONTACT</h2>
                <div class="subtitle">GET IN TOUCH</div>
                <p>พร้อมสำหรับการฝึกงาน 3D Artist และสร้างสรรค์ผลงานวิชวลสไตล์ใหม่ๆ</p>
                <div class="grid-tag" style="font-size: 1rem; padding: 0.6rem 1.5rem;">NAME: RATTASURD SIRASEN (SIN)</div>
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

        // Smooth cursor follow
        function updateCursor() {
            cursorX += (mouseX - cursorX) * 0.2;
            cursorY += (mouseY - cursorY) * 0.2;
            cursor.style.left = `${cursorX}px`;
            cursor.style.top = `${cursorY}px`;
            requestAnimationFrame(updateCursor);
        }
        updateCursor();

        // --- 2. THREE.JS SCENE SETUP ---
        const container = document.getElementById('webgl-container');
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0x050505);
        scene.fog = new THREE.FogExp2(0x050505, 0.035);

        const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(0, 1.6, 12);

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
        container.appendChild(renderer.domElement);

        // --- 3. LIGHTING (Liminal + Y2K Neon) ---
        const ambientLight = new THREE.AmbientLight(0x333333, 1.5);
        scene.add(ambientLight);

        // Corridor Lights
        for (let z = 10; z >= -40; z -= 8) {
            const light = new THREE.PointLight(0xffeedd, 0.6, 10);
            light.position.set(0, 3.8, z);
            scene.add(light);
        }

        // Hypercube Contrast Light (Neon Cyan)
        const hyperLight = new THREE.PointLight(0x00ffcc, 4, 25);
        hyperLight.position.set(0, 1.6, -30);
        scene.add(hyperLight);

        // --- 4. LIMINAL SPACE CORRIDOR ---
        const corridorGroup = new THREE.Group();

        const wallMat = new THREE.MeshStandardMaterial({ color: 0x222225, roughness: 0.8 });
        const floorMat = new THREE.MeshStandardMaterial({ color: 0x111113, roughness: 0.3, metalness: 0.2 });
        const ceilingMat = new THREE.MeshStandardMaterial({ color: 0x1a1a1c, roughness: 0.9 });

        const length = 70;
        const width = 7;
        const height = 4.5;

        // Floor
        const floor = new THREE.Mesh(new THREE.PlaneGeometry(width, length), floorMat);
        floor.rotation.x = -Math.PI / 2;
        floor.position.z = -20;
        corridorGroup.add(floor);

        // Ceiling
        const ceiling = new THREE.Mesh(new THREE.PlaneGeometry(width, length), ceilingMat);
        ceiling.rotation.x = Math.PI / 2;
        ceiling.position.y = height;
        ceiling.position.z = -20;
        corridorGroup.add(ceiling);

        // Walls
        const leftWall = new THREE.Mesh(new THREE.PlaneGeometry(length, height), wallMat);
        leftWall.rotation.y = Math.PI / 2;
        leftWall.position.x = -width / 2;
        leftWall.position.y = height / 2;
        leftWall.position.z = -20;
        corridorGroup.add(leftWall);

        const rightWall = new THREE.Mesh(new THREE.PlaneGeometry(length, height), wallMat);
        rightWall.rotation.y = -Math.PI / 2;
        rightWall.position.x = width / 2;
        rightWall.position.y = height / 2;
        rightWall.position.z = -20;
        corridorGroup.add(rightWall);

        scene.add(corridorGroup);

        // --- 5. 4D TESSERACT (HYPERCUBE) ---
        const vertices4D = [];
        for (let i = 0; i < 16; i++) {
            vertices4D.push([
                (i & 1) ? 1 : -1,
                (i & 2) ? 1 : -1,
                (i & 4) ? 1 : -1,
                (i & 8) ? 1 : -1
            ]);
        }

        const edges = [];
        for (let i = 0; i < 16; i++) {
            for (let j = i + 1; j < 16; j++) {
                let diff = 0;
                for (let k = 0; k < 4; k++) {
                    if (vertices4D[i][k] !== vertices4D[j][k]) diff++;
                }
                if (diff === 1) edges.push([i, j]);
            }
        }

        const tesseractGroup = new THREE.Group();
        const lineMaterial = new THREE.LineBasicMaterial({
            color: 0x00ffcc,
            transparent: true,
            opacity: 0.85
        });

        const lines = [];
        edges.forEach(() => {
            const geo = new THREE.BufferGeometry();
            geo.setAttribute('position', new THREE.Float32BufferAttribute([0,0,0, 0,0,0], 3));
            const line = new THREE.Line(geo, lineMaterial);
            lines.push(line);
            tesseractGroup.add(line);
        });

        tesseractGroup.position.set(0, 1.8, -30);
        scene.add(tesseractGroup);

        function project4Dto3D(v4, angle) {
            const cos = Math.cos(angle);
            const sin = Math.sin(angle);
            let x = v4[0], y = v4[1], z = v4[2], w = v4[3];

            let x1 = x * cos - w * sin;
            let w1 = x * sin + w * cos;
            let z1 = z * cos - w1 * sin;
            let w2 = z * sin + w1 * cos;

            const distance = 2.3;
            const wPerspective = 1 / (distance - w2);

            return new THREE.Vector3(
                x1 * wPerspective * 2.2,
                y * wPerspective * 2.2,
                z1 * wPerspective * 2.2
            );
        }

        // --- 6. SCROLL & MOUSE INTERACTION LOGIC ---
        let targetCameraZ = 12;
        let angle = 0;

        window.addEventListener('scroll', () => {
            // Calculate scroll progress (0 to 1)
            const scrollPx = window.scrollY;
            const maxScroll = document.documentElement.scrollHeight - window.innerHeight;
            const scrollPercent = scrollPx / maxScroll;

            // Move camera forward into the corridor based on scroll
            targetCameraZ = 12 - (scrollPercent * 32); 
        });

        // --- 7. ANIMATION LOOP ---
        function animate() {
            requestAnimationFrame(animate);

            // Smooth camera movement on Scroll
            camera.position.z += (targetCameraZ - camera.position.z) * 0.05;

            // Interactive mouse parallax on camera orientation
            const targetCamX = (mouseX / window.innerWidth - 0.5) * 1.5;
            const targetCamY = 1.6 - (mouseY / window.innerHeight - 0.5) * 1.0;

            camera.position.x += (targetCamX - camera.position.x) * 0.05;
            camera.position.y += (targetCamY - camera.position.y) * 0.05;
            camera.lookAt(0, 1.6, camera.position.z - 10);

            // Update 4D rotation
            angle += 0.012;
            const projected3D = vertices4D.map(v => project4Dto3D(v, angle));

            edges.forEach((edge, index) => {
                const p1 = projected3D[edge[0]];
                const p2 = projected3D[edge[1]];

                const positions = lines[index].geometry.attributes.position.array;
                positions[0] = p1.x; positions[1] = p1.y; positions[2] = p1.z;
                positions[3] = p2.x; positions[4] = p2.y; positions[5] = p2.z;
                lines[index].geometry.attributes.position.needsUpdate = true;
            });

            // Tesseract subtle movement based on mouse
            tesseractGroup.rotation.y = (mouseX / window.innerWidth) * 0.5;
            tesseractGroup.rotation.x = (mouseY / window.innerHeight) * 0.5;

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
