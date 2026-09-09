# Sin-city-eng.github.io
```html
<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rattasurd Sirasen (Sin) | 3D Interactive Portfolio</title>
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&family=Orbitron:wght@500;800&display=swap" rel="stylesheet">
  
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body, html {
      width: 100%;
      height: 100%;
      overflow: hidden;
      font-family: 'Kanit', sans-serif;
      background-color: #0d0e12;
      color: #ffffff;
    }

    /* Three.js Canvas Container */
    #webgl-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: 1;
    }

    /* UI Overlay Layer */
    .ui-layer {
      position: relative;
      z-index: 10;
      width: 100%;
      height: 100%;
      pointer-events: none; /* เพื่อให้เมาส์สามารถลากหมุนมุมกล้อง 3D ได้ */
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      padding: 3rem;
      box-sizing: border-box;
    }

    /* Header / Brand */
    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      pointer-events: auto;
    }

    .logo {
      font-family: 'Orbitron', sans-serif;
      font-size: 1.5rem;
      font-weight: 800;
      letter-spacing: 2px;
      color: #00ffcc;
      text-shadow: 0 0 10px rgba(0, 255, 204, 0.5);
    }

    nav ul {
      display: flex;
      list-style: none;
      gap: 2rem;
    }

    nav a {
      color: #e0e0e0;
      text-decoration: none;
      font-size: 1rem;
      font-weight: 300;
      transition: all 0.3s ease;
      letter-spacing: 1px;
    }

    nav a:hover, nav a.active {
      color: #00ffcc;
      text-shadow: 0 0 8px rgba(0, 255, 204, 0.8);
    }

    /* Main Section Content */
    main {
      pointer-events: auto;
      max-width: 550px;
      background: rgba(13, 14, 18, 0.65);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      padding: 2.5rem;
      border-radius: 16px;
      border: 1px solid rgba(255, 255, 255, 0.1);
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
      transition: all 0.5s ease;
    }

    .badge {
      display: inline-block;
      padding: 4px 12px;
      background: rgba(0, 255, 204, 0.15);
      border: 1px solid #00ffcc;
      color: #00ffcc;
      border-radius: 20px;
      font-size: 0.8rem;
      font-family: 'Orbitron', sans-serif;
      margin-bottom: 1rem;
    }

    h1 {
      font-size: 2.8rem;
      font-weight: 600;
      line-height: 1.2;
      margin-bottom: 0.5rem;
      background: linear-gradient(135deg, #ffffff 0%, #a5a5a5 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    h2 {
      font-family: 'Orbitron', sans-serif;
      font-size: 1.2rem;
      color: #ff0055;
      margin-bottom: 1.5rem;
      letter-spacing: 1.5px;
    }

    p {
      color: #c0c0c0;
      line-height: 1.7;
      font-size: 0.95rem;
      font-weight: 300;
      margin-bottom: 1.5rem;
    }

    .cta-btn {
      display: inline-block;
      padding: 12px 28px;
      background: linear-gradient(45deg, #00ffcc, #0099ff);
      color: #000;
      font-weight: 600;
      text-decoration: none;
      border-radius: 8px;
      transition: transform 0.3s, box-shadow 0.3s;
      cursor: pointer;
      border: none;
    }

    .cta-btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 20px rgba(0, 255, 204, 0.4);
    }

    /* Footer / Controls Hint */
    footer {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      font-size: 0.85rem;
      color: #7a7a7a;
    }

    .hint {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .hint-dot {
      width: 8px;
      height: 8px;
      background-color: #00ffcc;
      border-radius: 50%;
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0% { opacity: 0.3; }
      50% { opacity: 1; filter: drop-shadow(0 0 5px #00ffcc); }
      100% { opacity: 0.3; }
    }

    /* Content Switching Display */
    .content-section {
      display: none;
    }

    .content-section.active {
      display: block;
      animation: fadeIn 0.5s ease-in-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Responsive */
    @media (max-width: 768px) {
      .ui-layer { padding: 1.5rem; }
      main { max-width: 100%; padding: 1.5rem; }
      h1 { font-size: 2rem; }
      nav ul { gap: 1rem; }
    }
  </style>

  <!-- Import Three.js & OrbitControls -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
</head>
<body>

  <!-- WebGL Canvas Background -->
  <div id="webgl-container"></div>

  <!-- UI Overlay -->
  <div class="ui-layer">
    <header>
      <div class="logo">SIN.3D</div>
      <nav>
        <ul>
          <li><a href="#" class="nav-link active" data-target="home">Home</a></li>
          <li><a href="#" class="nav-link" data-target="about">About</a></li>
          <li><a href="#" class="nav-link" data-target="works">Works</a></li>
          <li><a href="#" class="nav-link" data-target="contact">Contact</a></li>
        </ul>
      </nav>
    </header>

    <main>
      <!-- Section: Home -->
      <div id="home" class="content-section active">
        <span class="badge">LIMINAL X 4D PORTFOLIO</span>
        <h1>Rattasurd Sirasen</h1>
        <h2>"SIN" — CREATIVE DEVELOPER & DESIGNER</h2>
        <p>ยินดีต้อนรับสู่พื้นที่จำลอง 3 มิติ การผสมผสานระหว่างสถาปัตยกรรมทางเดินแบบ Liminal Space ที่เงียบสงบ ตัดกันกับเรขาคณิต 4 มิติ (Hypercube) ที่เคลื่อนไหวไม่มีที่สิ้นสุด</p>
        <button class="cta-btn" onclick="switchTab('works')">ชมผลงานทั้งหมด</button>
      </div>

      <!-- Section: About -->
      <div id="about" class="content-section">
        <span class="badge">ABOUT ME</span>
        <h1>เกี่ยวกับ Sin</h1>
        <h2>PASSIONATE CREATOR</h2>
        <p>ผม **รัฐศาสตร์ ศิระเสน (Sin)** สนใจงานออกแบบ Game Design, 3D Interactive, Digital Composition และการนำวัฒนธรรมหรือสไตล์ล้ำยุค (Cyberpunk/Surrealism) มาสร้างสรรค์เป็นประสบการณ์ดิจิทัลรูปแบบใหม่</p>
        <button class="cta-btn" onclick="switchTab('contact')">ติดต่อร่วมงาน</button>
      </div>

      <!-- Section: Works -->
      <div id="works" class="content-section">
        <span class="badge">SELECTED WORKS</span>
        <h1>ผลงานและโปรเจกต์</h1>
        <h2>FEATURED PROJECTS</h2>
        <p>• <strong>Cyberpunk x Thai Literature:</strong> งานออกแบบแนวคิดเกมและปกผสมผสานวรรณคดีไทยเข้ากับโลกอนาคต<br>
           • <strong>3D Environment & Liminal Space:</strong> การจำลองฉาก 3D และโครงสร้างลวงตา<br>
           • <strong>Digital Composition:</strong> การตัดต่อและแต่งภาพความละเอียดสูงสำหรับงานโปรดักชัน</p>
      </div>

      <!-- Section: Contact -->
      <div id="contact" class="content-section">
        <span class="badge">GET IN TOUCH</span>
        <h1>ช่องทางติดต่อ</h1>
        <h2>LET'S WORK TOGETHER</h2>
        <p>สนใจร่วมงานหรือสอบถามรายละเอียดเพิ่มเติม สามารถติดต่อได้ทาง:<br>
        <strong>Email:</strong> rattasurd.sin@example.com<br>
        <strong>Location:</strong> Thailand</p>
      </div>
    </main>

    <footer>
      <div class="hint">
        <div class="hint-dot"></div>
        <span>คลิกลากเพื่อหมุนมุมมอง 3D | สโครลเพื่อย่อ-ขยาย</span>
      </div>
      <div>© 2026 Rattasurd Sirasen. All Rights Reserved.</div>
    </footer>
  </div>

  <!-- Three.js Scene Setup -->
  <script>
    // --- 1. SCENE, CAMERA, RENDERER SETUP ---
    const container = document.getElementById('webgl-container');
    const scene = new THREE.Scene();
    
    // สร้างหมอก (Fog) เพื่อเพิ่มบรรยากาศ Liminal Space เงียบสงบ ลึกลับ
    scene.background = new THREE.Color(0x0a0b10);
    scene.fog = new THREE.FogExp2(0x0a0b10, 0.025);

    const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0, 2, 8);

    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    renderer.shadowMap.enabled = true;
    renderer.shadowMap.type = THREE.PCFSoftShadowMap;
    container.appendChild(renderer.domElement);

    // Controls
    const controls = new THREE.OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;
    controls.dampingFactor = 0.05;
    controls.maxPolarAngle = Math.PI / 2 - 0.01; // ไม่ให้กล้องทะลุลงใต้พื้น
    controls.minDistance = 3;
    controls.maxDistance = 20;

    // --- 2. LIGHTING ---
    const ambientLight = new THREE.AmbientLight(0xffffff, 0.3);
    scene.add(ambientLight);

    // แสงซุ้มทางเดิน (Liminal Warm/Cool Contrast)
    const dirLight = new THREE.DirectionalLight(0xffffff, 0.8);
    dirLight.position.set(5, 15, 5);
    dirLight.castShadow = true;
    dirLight.shadow.mapSize.width = 2048;
    dirLight.shadow.mapSize.height = 2048;
    scene.add(dirLight);

    // แสงสะท้อนสีจากวัตถุ 4D (Neon Glow Effect)
    const tesseractLight = new THREE.PointLight(0x00ffcc, 2, 15);
    tesseractLight.position.set(0, 3, -12);
    scene.add(tesseractLight);

    const tesseractPinkLight = new THREE.PointLight(0xff0055, 2, 15);
    tesseractPinkLight.position.set(0, 3, -12);
    scene.add(tesseractPinkLight);

    // --- 3. LIMINAL SPACE ARCHWAY CORRIDOR (ทางเดิน) ---
    const corridorGroup = new THREE.Group();

    // วัสดุทางเดิน
    const wallMaterial = new THREE.MeshStandardMaterial({ 
      color: 0x1e2029, 
      roughness: 0.8,
      metalness: 0.1
    });
    const floorMaterial = new THREE.MeshStandardMaterial({ 
      color: 0x08090c, 
      roughness: 0.2, // เงา reflection สะท้อนพื้น
      metalness: 0.5 
    });

    // พื้นทางเดิน
    const floorGeo = new THREE.PlaneGeometry(10, 100);
    const floor = new THREE.Mesh(floorGeo, floorMaterial);
    floor.rotation.x = -Math.PI / 2;
    floor.position.z = -30;
    floor.receiveShadow = true;
    corridorGroup.add(floor);

    // ซุ้มประตูเสาซ้ำๆ (Archways) สร้างความรู้สึก Liminal Space
    const archCount = 12;
    const archSpacing = 5;

    for (let i = 0; i < archCount; i++) {
      const zPos = -i * archSpacing + 5;

      // เสาซ้าย-ขวา
      const pillarGeo = new THREE.BoxGeometry(0.8, 6, 0.8);
      const leftPillar = new THREE.Mesh(pillarGeo, wallMaterial);
      leftPillar.position.set(-4, 3, zPos);
      leftPillar.castShadow = true;
      leftPillar.receiveShadow = true;

      const rightPillar = new THREE.Mesh(pillarGeo, wallMaterial);
      rightPillar.position.set(4, 3, zPos);
      rightPillar.castShadow = true;
      rightPillar.receiveShadow = true;

      // คานบน
      const beamGeo = new THREE.BoxGeometry(8.8, 0.8, 0.8);
      const beam = new THREE.Mesh(beamGeo, wallMaterial);
      beam.position.set(0, 5.6, zPos);
      beam.castShadow = true;

      corridorGroup.add(leftPillar);
      corridorGroup.add(rightPillar);
      corridorGroup.add(beam);
    }
    scene.add(corridorGroup);

    // --- 4. 4D OBJECT (TESSERACT / HYPERCUBE) ---
    // จำลองโครงสร้าง Hypercube ล้อมกัน 2 ชั้น (Inner & Outer Wireframe Cube)
    const tesseractGroup = new THREE.Group();
    tesseractGroup.position.set(0, 3.5, -15); // ตั้งไว้สุดปลายทางเดิน

    // Outer Cube Material
    const outerMat = new THREE.MeshBasicMaterial({
      color: 0x00ffcc,
      wireframe: true,
      transparent: true,
      opacity: 0.8
    });
    const outerGeo = new THREE.BoxGeometry(3, 3, 3);
    const outerCube = new THREE.Mesh(outerGeo, outerMat);

    // Inner Cube Material
    const innerMat = new THREE.MeshBasicMaterial({
      color: 0xff0055,
      wireframe: true,
      transparent: true,
      opacity: 0.9
    });
    const innerGeo = new THREE.BoxGeometry(1.5, 1.5, 1.5);
    const innerCube = new THREE.Mesh(innerGeo, innerMat);

    // เส้นเชื่อมระหว่าง Vertex (จำลองมิติที่ 4)
    const lineMaterial = new THREE.LineBasicMaterial({ color: 0xffffff, transparent: true, opacity: 0.4 });
    const linesGroup = new THREE.Group();

    const outerVertices = outerGeo.vertices || []; 
    // ใช้ BufferGeometry ใน Three.js รุ่นใหม่
    const outerPositions = outerGeo.attributes.position.array;
    const innerPositions = innerGeo.attributes.position.array;

    for (let i = 0; i < outerPositions.length; i += 3) {
      const geometry = new THREE.BufferGeometry();
      const points = [
        new THREE.Vector3(outerPositions[i], outerPositions[i+1], outerPositions[i+2]),
        new THREE.Vector3(innerPositions[i]*0.5, innerPositions[i+1]*0.5, innerPositions[i+2]*0.5)
      ];
      geometry.setFromPoints(points);
      const line = new THREE.Line(geometry, lineMaterial);
      linesGroup.add(line);
    }

    tesseractGroup.add(outerCube);
    tesseractGroup.add(innerCube);
    tesseractGroup.add(linesGroup);
    scene.add(tesseractGroup);

    // --- 5. ANIMATION LOOP ---
    let time = 0;
    function animate() {
      requestAnimationFrame(animate);
      time += 0.015;

      // หมุนวัตถุ 4D ในแกนต่างๆ ให้เกิดการลวงตา
      tesseractGroup.rotation.x = time * 0.3;
      tesseractGroup.rotation.y = time * 0.5;

      // เอฟเฟกต์ยืด-หดลูกบาศก์ด้านใน (Simulating 4D rotation through 3D space)
      const scaleFactor = 1 + Math.sin(time * 2) * 0.3;
      innerCube.scale.set(scaleFactor, scaleFactor, scaleFactor);
      innerCube.rotation.x = -time * 0.8;
      innerCube.rotation.z = time * 0.4;

      // ขยับแสงไฟตามจังหวะอนิเมชัน
      tesseractLight.intensity = 1.5 + Math.sin(time * 3) * 0.5;
      tesseractPinkLight.intensity = 1.5 + Math.cos(time * 3) * 0.5;

      controls.update();
      renderer.render(scene, camera);
    }
    animate();

    // --- 6. RESIZE HANDLER ---
    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    // --- 7. UI NAVIGATION LOGIC ---
    const navLinks = document.querySelectorAll('.nav-link');
    const sections = document.querySelectorAll('.content-section');

    function switchTab(targetId) {
      navLinks.forEach(link => {
        if (link.getAttribute('data-target') === targetId) {
          link.classList.add('active');
        } else {
          link.classList.remove('active');
        }
      });

      sections.forEach(sec => {
        if (sec.id === targetId) {
          sec.classList.add('active');
        } else {
          sec.classList.remove('active');
        }
      });
    }

    navLinks.forEach(link => {
      link.addEventListener('click', (e) => {
        e.preventDefault();
        const target = link.getAttribute('data-target');
        switchTab(target);
      });
    });
  </script>
</body>
</html>
