# Sin-city-eng.github.io
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Rattasurd Sirasen — 3D Portfolio</title>

    <!-- Three.js -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            background: #080808;
            color: white;
            font-family: Arial, Helvetica, sans-serif;
            overflow-x: hidden;
        }

        canvas {
            position: fixed;
            inset: 0;
            z-index: -1;
        }

        /* =========================
           NAVBAR
        ========================= */

        nav {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 80px;

            display: flex;
            align-items: center;
            justify-content: space-between;

            padding: 0 7%;
            z-index: 100;

            background: rgba(8, 8, 8, 0.55);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid rgba(255,255,255,0.08);
        }

        .logo {
            font-size: 20px;
            font-weight: bold;
            letter-spacing: 2px;
        }

        .logo span {
            color: #888;
        }

        nav ul {
            display: flex;
            gap: 35px;
            list-style: none;
        }

        nav a {
            color: #aaa;
            text-decoration: none;
            font-size: 13px;
            letter-spacing: 1px;
            transition: 0.3s;
        }

        nav a:hover {
            color: white;
        }

        /* =========================
           GENERAL
        ========================= */

        section {
            min-height: 100vh;
            padding: 120px 8%;
            position: relative;
        }

        .section-title {
            font-size: clamp(40px, 6vw, 80px);
            line-height: 0.95;
            margin-bottom: 50px;
        }

        .section-title span {
            color: #777;
        }

        /* =========================
           HERO
        ========================= */

        #home {
            min-height: 100vh;

            display: flex;
            align-items: center;

            padding-left: 8%;
        }

        .hero-content {
            max-width: 700px;
        }

        .small-title {
            color: #999;
            font-size: 14px;
            letter-spacing: 5px;
            margin-bottom: 25px;
        }

        .hero-title {
            font-size: clamp(55px, 9vw, 130px);
            line-height: 0.85;
            letter-spacing: -5px;
        }

        .hero-title span {
            color: #777;
        }

        .hero-description {
            margin-top: 35px;
            max-width: 500px;
            color: #aaa;
            line-height: 1.7;
            font-size: 16px;
        }

        .hero-buttons {
            margin-top: 40px;
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .button {
            padding: 15px 25px;
            border: 1px solid white;
            color: white;
            text-decoration: none;
            font-size: 13px;
            letter-spacing: 1px;
            transition: 0.3s;
        }

        .button:hover {
            background: white;
            color: black;
        }

        .button.secondary {
            border-color: #444;
            color: #aaa;
        }

        /* =========================
           ABOUT
        ========================= */

        #about {
            background: rgba(8,8,8,0.78);
        }

        .about-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 80px;
            align-items: center;
        }

        .about-text {
            color: #aaa;
            line-height: 1.9;
            font-size: 17px;
        }

        .about-text strong {
            color: white;
        }

        .about-number {
            font-size: 180px;
            font-weight: bold;
            color: #111;
            line-height: 1;
        }

        /* =========================
           SKILLS
        ========================= */

        #skills {
            background: #0b0b0b;
        }

        .skills-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 1px;
            background: #222;
        }

        .skill {
            min-height: 220px;
            padding: 35px;
            background: #0b0b0b;
            transition: 0.4s;
        }

        .skill:hover {
            background: #151515;
            transform: translateY(-5px);
        }

        .skill-number {
            color: #555;
            font-size: 13px;
        }

        .skill h3 {
            margin-top: 50px;
            font-size: 24px;
        }

        .skill p {
            margin-top: 15px;
            color: #777;
            line-height: 1.6;
        }

        /* =========================
           PORTFOLIO
        ========================= */

        #portfolio {
            background: rgba(8,8,8,0.9);
        }

        .portfolio-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 25px;
        }

        .project {
            height: 450px;
            position: relative;
            overflow: hidden;
            background: linear-gradient(
                135deg,
                #191919,
                #080808
            );
            border: 1px solid #222;
            transition: 0.5s;
        }

        .project:hover {
            transform: scale(1.015);
        }

        .project::before {
            content: "";
            position: absolute;
            inset: 0;

            background:
                radial-gradient(
                    circle at 70% 30%,
                    rgba(255,255,255,0.13),
                    transparent 35%
                );
        }

        .project-content {
            position: absolute;
            left: 30px;
            bottom: 30px;
        }

        .project-category {
            color: #777;
            font-size: 12px;
            letter-spacing: 3px;
        }

        .project h3 {
            margin-top: 8px;
            font-size: 32px;
        }

        .project p {
            margin-top: 8px;
            color: #888;
        }

        /* =========================
           CONTACT
        ========================= */

        #contact {
            min-height: 70vh;
            background: #050505;
            display: flex;
            align-items: center;
        }

        .contact-title {
            font-size: clamp(50px, 9vw, 130px);
            line-height: 0.85;
        }

        .contact-title span {
            color: #555;
        }

        .contact-info {
            margin-top: 45px;
            color: #999;
            line-height: 2;
        }

        .contact-info a {
            color: white;
            text-decoration: none;
            border-bottom: 1px solid #555;
        }

        footer {
            padding: 30px 8%;
            background: #050505;
            color: #444;
            border-top: 1px solid #151515;
            font-size: 12px;
            display: flex;
            justify-content: space-between;
        }

        /* =========================
           SCROLL INDICATOR
        ========================= */

        .scroll {
            position: absolute;
            bottom: 35px;
            left: 8%;

            font-size: 11px;
            letter-spacing: 3px;
            color: #666;

            writing-mode: vertical-rl;
        }

        /* =========================
           RESPONSIVE
        ========================= */

        @media (max-width: 800px) {

            nav ul {
                display: none;
            }

            section {
                padding: 100px 6%;
            }

            .about-grid {
                grid-template-columns: 1fr;
                gap: 30px;
            }

            .about-number {
                font-size: 100px;
            }

            .skills-grid {
                grid-template-columns: 1fr;
            }

            .portfolio-grid {
                grid-template-columns: 1fr;
            }

            .project {
                height: 350px;
            }

            .hero-title {
                letter-spacing: -3px;
            }

            footer {
                flex-direction: column;
                gap: 10px;
            }
        }
    </style>
</head>

<body>

    <!-- =========================
         NAVIGATION
    ========================= -->

    <nav>
        <div class="logo">
            RATTASURD<span>.</span>
        </div>

        <ul>
            <li><a href="#home">HOME</a></li>
            <li><a href="#about">ABOUT</a></li>
            <li><a href="#skills">SKILLS</a></li>
            <li><a href="#portfolio">WORK</a></li>
            <li><a href="#contact">CONTACT</a></li>
        </ul>
    </nav>


    <!-- =========================
         HERO
    ========================= -->

    <section id="home">

        <div class="hero-content">

            <div class="small-title">
                3D ARTIST / 3D GENERALIST
            </div>

            <h1 class="hero-title">
                RATTASURD<br>
                <span>SIRASEN</span>
            </h1>

            <p class="hero-description">
                3D Artist focused on creating characters, environments,
                game assets and animations. I enjoy transforming ideas
                into visual experiences through 3D.
            </p>

            <div class="hero-buttons">
                <a href="#portfolio" class="button">
                    VIEW MY WORK
                </a>

                <a href="#contact" class="button secondary">
                    CONTACT ME
                </a>
            </div>

        </div>

        <div class="scroll">
            SCROLL DOWN
        </div>

    </section>


    <!-- =========================
         ABOUT
    ========================= -->

    <section id="about">

        <h2 class="section-title">
            ABOUT <span>ME</span>
        </h2>

        <div class="about-grid">

            <div class="about-text">

                <p>
                    Hello, I'm <strong>Rattasurd Sirasen</strong>.
                </p>

                <br>

                <p>
                    I am a 3D-focused creative who is interested in
                    modeling, animation, game assets and interactive media.
                </p>

                <br>

                <p>
                    My goal is to create 3D work that is not only
                    visually interesting, but also communicates an idea,
                    atmosphere and story.
                </p>

            </div>

            <div class="about-number">
                3D
            </div>

        </div>

    </section>


    <!-- =========================
         SKILLS
    ========================= -->

    <section id="skills">

        <h2 class="section-title">
            MY <span>SKILLS</span>
        </h2>

        <div class="skills-grid">

            <div class="skill">
                <div class="skill-number">01</div>

                <h3>3D MODELING</h3>

                <p>
                    Character modeling, hard surface,
                    props and environment assets.
                </p>
            </div>

            <div class="skill">
                <div class="skill-number">02</div>

                <h3>TEXTURING</h3>

                <p>
                    Creating materials, UVs and textures
                    for 3D assets.
                </p>
            </div>

            <div class="skill">
                <div class="skill-number">03</div>

                <h3>ANIMATION</h3>

                <p>
                    Character animation, object animation
                    and motion design.
                </p>
            </div>

            <div class="skill">
                <div class="skill-number">04</div>

                <h3>RIGGING</h3>

                <p>
                    Character rigs, joints and controls
                    for animation workflows.
                </p>
            </div>

            <div class="skill">
                <div class="skill-number">05</div>

                <h3>GAME ASSET</h3>

                <p>
                    Creating optimized 3D assets
                    for interactive environments.
                </p>
            </div>

            <div class="skill">
                <div class="skill-number">06</div>

                <h3>3D ART</h3>

                <p>
                    Visual development, composition,
                    lighting and 3D presentation.
                </p>
            </div>

        </div>

    </section>


    <!-- =========================
         PORTFOLIO
    ========================= -->

    <section id="portfolio">

        <h2 class="section-title">
            SELECTED <span>WORK</span>
        </h2>

        <div class="portfolio-grid">

            <div class="project">
                <div class="project-content">
                    <div class="project-category">
                        3D MODELING
                    </div>

                    <h3>CHARACTER</h3>

                    <p>
                        Character Design & 3D Modeling
                    </p>
                </div>
            </div>

            <div class="project">
                <div class="project-content">
                    <div class="project-category">
                        GAME ASSET
                    </div>

                    <h3>ENVIRONMENT</h3>

                    <p>
                        Environment & Prop Modeling
                    </p>
                </div>
            </div>

            <div class="project">
                <div class="project-content">
                    <div class="project-category">
                        ANIMATION
                    </div>

                    <h3>MOTION</h3>

                    <p>
                        3D Animation & Motion Design
                    </p>
                </div>
            </div>

            <div class="project">
                <div class="project-content">
                    <div class="project-category">
                        EXPERIMENTAL
                    </div>

                    <h3>3D WORLD</h3>

                    <p>
                        Interactive 3D Environment
                    </p>
                </div>
            </div>

        </div>

    </section>


    <!-- =========================
         CONTACT
    ========================= -->

    <section id="contact">

        <div>

            <div class="small-title">
                LET'S CREATE SOMETHING
            </div>

            <h2 class="contact-title">
                LET'S<br>
                <span>TALK.</span>
            </h2>

            <div class="contact-info">

                <p>
                    Rattasurd Sirasen
                </p>

                <p>
                    3D Artist / 3D Generalist
                </p>

                <p>
                    Email:
                    <a href="mailto:your@email.com">
                        your@email.com
                    </a>
                </p>

            </div>

        </div>

    </section>


    <footer>

        <div>
            © 2026 Rattasurd Sirasen
        </div>

        <div>
            3D PORTFOLIO
        </div>

    </footer>


    <!-- =========================
         THREE.JS
    ========================= -->

    <script>

        // --------------------------------
        // Scene
        // --------------------------------

        const scene = new THREE.Scene();

        scene.background = new THREE.Color(0x080808);

        // --------------------------------
        // Camera
        // --------------------------------

        const camera = new THREE.PerspectiveCamera(
            60,
            window.innerWidth / window.innerHeight,
            0.1,
            1000
        );

        camera.position.z = 7;

        // --------------------------------
        // Renderer
        // --------------------------------

        const renderer = new THREE.WebGLRenderer({
            antialias: true,
            alpha: true
        });

        renderer.setSize(
            window.innerWidth,
            window.innerHeight
        );

        renderer.setPixelRatio(
            Math.min(window.devicePixelRatio, 2)
        );

        document.body.appendChild(renderer.domElement);


        // --------------------------------
        // Lights
        // --------------------------------

        const ambientLight = new THREE.AmbientLight(
            0xffffff,
            0.5
        );

        scene.add(ambientLight);


        const light = new THREE.PointLight(
            0xffffff,
            2,
            20
        );

        light.position.set(3, 3, 5);

        scene.add(light);


        const light2 = new THREE.PointLight(
            0x888888,
            1.5,
            15
        );

        light2.position.set(-4, -2, 3);

        scene.add(light2);


        // --------------------------------
        // Main 3D Object
        // --------------------------------

        const geometry = new THREE.IcosahedronGeometry(
            2,
            2
        );

        const material = new THREE.MeshStandardMaterial({
            color: 0x555555,
            roughness: 0.35,
            metalness: 0.75,
            wireframe: false
        });

        const object = new THREE.Mesh(
            geometry,
            material
        );

        object.position.set(3, 0, 0);

        scene.add(object);


        // --------------------------------
        // Wireframe
        // --------------------------------

        const wireGeometry =
            new THREE.IcosahedronGeometry(2.03, 2);

        const wireMaterial =
            new THREE.MeshBasicMaterial({
                color: 0x888888,
                wireframe: true,
                transparent: true,
                opacity: 0.15
            });

        const wire =
            new THREE.Mesh(
                wireGeometry,
                wireMaterial
            );

        wire.position.copy(object.position);

        scene.add(wire);


        // --------------------------------
        // Particles
        // --------------------------------

        const particleGeometry =
            new THREE.BufferGeometry();

        const particleCount = 1000;

        const positions =
            new Float32Array(particleCount * 3);

        for (let i = 0; i < particleCount * 3; i++) {

            positions[i] =
                (Math.random() - 0.5) * 30;

        }

        particleGeometry.setAttribute(
            'position',
            new THREE.BufferAttribute(
                positions,
                3
            )
        );

        const particleMaterial =
            new THREE.PointsMaterial({
                color: 0xffffff,
                size: 0.025,
                transparent: true,
                opacity: 0.5
            });

        const particles =
            new THREE.Points(
                particleGeometry,
                particleMaterial
            );

        scene.add(particles);


        // --------------------------------
        // Mouse Interaction
        // --------------------------------

        let mouseX = 0;
        let mouseY = 0;

        document.addEventListener(
            'mousemove',
            (event) => {

                mouseX =
                    (event.clientX /
                    window.innerWidth) * 2 - 1;

                mouseY =
                    (event.clientY /
                    window.innerHeight) * 2 - 1;

            }
        );


        // --------------------------------
        // Animation
        // --------------------------------

        function animate() {

            requestAnimationFrame(animate);


            object.rotation.x += 0.003;
            object.rotation.y += 0.006;

            wire.rotation.x =
                object.rotation.x;

            wire.rotation.y =
                object.rotation.y;


            particles.rotation.y += 0.0003;


            // Mouse movement

            object.position.x =
                3 + mouseX * 0.5;

            object.position.y =
                mouseY * -0.4;

            wire.position.copy(
                object.position
            );


            renderer.render(
                scene,
                camera
            );

        }

        animate();


        // --------------------------------
        // Responsive
        // --------------------------------

        window.addEventListener(
            'resize',
            () => {

                camera.aspect =
                    window.innerWidth /
                    window.innerHeight;

                camera.updateProjectionMatrix();

                renderer.setSize(
                    window.innerWidth,
                    window.innerHeight
                );

            }
        );

    </script>

</body>
</html>
```
