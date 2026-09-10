RATTASURD SIRASEN
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Rattasurd Sirasen— Creative Portfolio</title>

    <meta
        name="description"
        content="Portfolio of RATTASURD SIRASEN — 3D modeling, manga illustration, animation, character design and visual development."
    >

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
            background: #070707;
            color: #f2f2f2;
            font-family: Arial, Helvetica, sans-serif;
            overflow-x: hidden;
        }

        a {
            color: inherit;
            text-decoration: none;
        }

        /* =========================
           THREE.JS BACKGROUND
        ========================= */

        #three-container {
            position: fixed;
            inset: 0;
            z-index: -2;
        }

        #three-container canvas {
            display: block;
        }

        .background-overlay {
            position: fixed;
            inset: 0;
            z-index: -1;
            pointer-events: none;

            background:
                radial-gradient(
                    circle at 50% 40%,
                    rgba(255,255,255,0.055),
                    transparent 35%
                ),
                linear-gradient(
                    to bottom,
                    rgba(0,0,0,0.25),
                    rgba(0,0,0,0.85)
                );
        }

        /* =========================
           NAVIGATION
        ========================= */

        nav {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;

            display: flex;
            justify-content: space-between;
            align-items: center;

            padding: 25px 6vw;

            z-index: 20;

            background: linear-gradient(
                to bottom,
                rgba(0,0,0,0.7),
                transparent
            );

            backdrop-filter: blur(3px);
        }

        .logo {
            font-size: 15px;
            font-weight: 700;
            letter-spacing: 0.18em;
            text-transform: uppercase;
        }

        .nav-links {
            display: flex;
            gap: 35px;
            list-style: none;
        }

        .nav-links a {
            font-size: 12px;
            text-transform: uppercase;
            letter-spacing: 0.15em;
            opacity: 0.65;
            transition: opacity 0.25s ease;
        }

        .nav-links a:hover {
            opacity: 1;
        }

        /* =========================
           GENERAL
        ========================= */

        section {
            min-height: 100vh;
            padding: 120px 8vw;
            position: relative;
        }

        .section-label {
            font-size: 11px;
            letter-spacing: 0.25em;
            text-transform: uppercase;
            opacity: 0.45;
            margin-bottom: 25px;
        }

        .section-title {
            font-size: clamp(42px, 7vw, 100px);
            line-height: 0.95;
            font-weight: 700;
            letter-spacing: -0.05em;
        }

        .muted {
            opacity: 0.55;
        }

        /* =========================
           HERO
        ========================= */

        #home {
            min-height: 100vh;

            display: flex;
            flex-direction: column;
            justify-content: center;

            padding-left: 10vw;
        }

        .hero-small {
            font-size: 13px;
            letter-spacing: 0.35em;
            text-transform: uppercase;
            opacity: 0.55;
            margin-bottom: 25px;
        }

        .hero-name {
            font-size: clamp(55px, 11vw, 170px);
            line-height: 0.82;
            letter-spacing: -0.075em;
            max-width: 1000px;
        }

        .hero-name span {
            display: block;
            opacity: 0.38;
        }

        .hero-description {
            max-width: 600px;
            margin-top: 45px;

            font-size: 16px;
            line-height: 1.8;

            color: rgba(255,255,255,0.65);
        }

        .hero-button {
            display: inline-flex;
            margin-top: 40px;

            padding: 15px 24px;

            border: 1px solid rgba(255,255,255,0.25);

            font-size: 11px;
            letter-spacing: 0.2em;
            text-transform: uppercase;

            transition:
                background 0.3s ease,
                color 0.3s ease,
                border 0.3s ease;
        }

        .hero-button:hover {
            background: #fff;
            color: #000;
            border-color: #fff;
        }

        .scroll-indicator {
            position: absolute;
            bottom: 35px;
            left: 10vw;

            font-size: 10px;
            letter-spacing: 0.2em;
            text-transform: uppercase;

            opacity: 0.35;
        }

        /* =========================
           ABOUT
        ========================= */

        #about {
            display: flex;
            align-items: center;
        }

        .about-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10vw;
            width: 100%;
            max-width: 1400px;
        }

        .about-text {
            font-size: 20px;
            line-height: 1.8;
            color: rgba(255,255,255,0.7);
        }

        .about-text strong {
            color: #fff;
        }

        .about-details {
            display: flex;
            flex-direction: column;
            justify-content: center;
            gap: 35px;
        }

        .detail {
            border-top: 1px solid rgba(255,255,255,0.15);
            padding-top: 18px;
        }

        .detail-title {
            font-size: 11px;
            letter-spacing: 0.2em;
            text-transform: uppercase;
            opacity: 0.4;
            margin-bottom: 8px;
        }

        .detail-value {
            font-size: 18px;
        }

        /* =========================
           SKILLS
        ========================= */

        #skills {
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .skills-list {
            margin-top: 80px;
            border-top: 1px solid rgba(255,255,255,0.15);
        }

        .skill {
            display: grid;
            grid-template-columns: 80px 1fr auto;
            align-items: center;

            padding: 28px 0;

            border-bottom: 1px solid rgba(255,255,255,0.15);

            transition: padding 0.3s ease;
        }

        .skill:hover {
            padding-left: 15px;
            padding-right: 15px;
        }

        .skill-number {
            font-size: 11px;
            opacity: 0.35;
        }

        .skill-name {
            font-size: clamp(24px, 4vw, 55px);
            letter-spacing: -0.04em;
        }

        .skill-type {
            font-size: 10px;
            letter-spacing: 0.15em;
            text-transform: uppercase;
            opacity: 0.4;
        }

        /* =========================
           WORKS
        ========================= */

        #works {
            padding-top: 150px;
        }

        .works-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;

            margin-bottom: 80px;
        }

        .works-note {
            max-width: 300px;
            font-size: 13px;
            line-height: 1.7;
            opacity: 0.45;
        }

        .works-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 30px;

            max-width: 1400px;
        }

        .work {
            position: relative;

            min-height: 500px;

            overflow: hidden;

            background:
                linear-gradient(
                    135deg,
                    rgba(255,255,255,0.08),
                    rgba(255,255,255,0.015)
                );

            border: 1px solid rgba(255,255,255,0.1);

            transition:
                transform 0.4s ease,
                border-color 0.4s ease;
        }

        .work:hover {
            transform: translateY(-8px);
            border-color: rgba(255,255,255,0.3);
        }

        .work-image {
            position: absolute;
            inset: 0;

            display: flex;
            align-items: center;
            justify-content: center;

            font-size: 70px;
            font-weight: 700;

            letter-spacing: -0.08em;

            opacity: 0.07;

            transition:
                transform 0.6s ease,
                opacity 0.6s ease;
        }

        .work:hover .work-image {
            transform: scale(1.08);
            opacity: 0.13;
        }

        .work-info {
            position: absolute;
            left: 30px;
            right: 30px;
            bottom: 30px;
        }

        .work-number {
            font-size: 10px;
            letter-spacing: 0.2em;
            opacity: 0.4;
            margin-bottom: 10px;
        }

        .work-title {
            font-size: 32px;
            letter-spacing: -0.04em;
        }

        .work-description {
            margin-top: 10px;
            font-size: 12px;
            line-height: 1.6;
            opacity: 0.45;
            max-width: 400px;
        }

        /* =========================
           CONTACT
        ========================= */

        #contact {
            min-height: 80vh;

            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .contact-title {
            font-size: clamp(50px, 10vw, 150px);
            letter-spacing: -0.07em;
            line-height: 0.85;
            max-width: 1000px;
        }

        .contact-description {
            margin-top: 35px;
            max-width: 500px;

            font-size: 16px;
            line-height: 1.7;

            opacity: 0.5;
        }

        .contact-links {
            display: flex;
            gap: 25px;
            margin-top: 45px;
            flex-wrap: wrap;
        }

        .contact-link {
            border-bottom: 1px solid rgba(255,255,255,0.3);
            padding-bottom: 7px;

            font-size: 11px;
            text-transform: uppercase;
            letter-spacing: 0.18em;

            opacity: 0.65;

            transition: opacity 0.25s ease;
        }

        .contact-link:hover {
            opacity: 1;
        }

        /* =========================
           FOOTER
        ========================= */

        footer {
            padding: 30px 8vw;

            display: flex;
            justify-content: space-between;

            border-top: 1px solid rgba(255,255,255,0.1);

            font-size: 10px;
            letter-spacing: 0.15em;
            text-transform: uppercase;

            opacity: 0.3;
        }

        /* =========================
           RESPONSIVE
        ========================= */

        @media (max-width: 800px) {

            nav {
                padding: 20px 5vw;
            }

            .nav-links {
                gap: 15px;
            }

            .nav-links li:nth-child(2) {
                display: none;
            }

            section {
                padding-left: 7vw;
                padding-right: 7vw;
            }

            #home {
                padding-left: 7vw;
            }

            .hero-description {
                font-size: 14px;
            }

            .about-grid {
                grid-template-columns: 1fr;
                gap: 60px;
            }

            .about-text {
                font-size: 17px;
            }

            .skill {
                grid-template-columns: 45px 1fr;
            }

            .skill-type {
                display: none;
            }

            .works-header {
                display: block;
            }

            .works-note {
                margin-top: 25px;
            }

            .works-grid {
                grid-template-columns: 1fr;
            }

            .work {
                min-height: 400px;
            }

            footer {
                flex-direction: column;
                gap: 10px;
            }
        }
    </style>
</head>

<body>

    <!-- Three.js background -->
    <div id="three-container"></div>
    <div class="background-overlay"></div>

    <!-- Navigation -->
    <nav>
        <a href="#home" class="logo">
            TR
        </a>

        <ul class="nav-links">
            <li><a href="#about">About</a></li>
            <li><a href="#skills">Skills</a></li>
            <li><a href="#works">Works</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>


    <!-- =========================
         HERO
    ========================== -->

    <section id="home">

        <div class="hero-small">
            Creative Portfolio / 2026
        </div>

        <h1 class="hero-name">
            Takdanai
            <span>Ramchuen</span>
        </h1>

        <p class="hero-description">
            I am a creative individual with experience in 3D modeling
            and a strong interest in manga drawing and animation.
            I enjoy developing visual ideas through illustration,
            character design, and 3D work, while continuously improving
            my technical and artistic skills.
        </p>

        <a href="#works" class="hero-button">
            Explore my work
        </a>

        <div class="scroll-indicator">
            Scroll to explore ↓
        </div>

    </section>


    <!-- =========================
         ABOUT
    ========================== -->

    <section id="about">

        <div class="about-grid">

            <div>
                <div class="section-label">
                    01 / Introduction
                </div>

                <h2 class="section-title">
                    About<br>
                    <span class="muted">Me</span>
                </h2>
            </div>

            <div class="about-details">

                <p class="about-text">
                    I enjoy turning ideas into visual work through
                    <strong>illustration, character design, animation,
                    and 3D modeling.</strong>
                    My goal is to continue developing both my artistic
                    and technical skills while building a portfolio
                    of meaningful visual projects.
                </p>

                <div class="detail">
                    <div class="detail-title">
                        Focus
                    </div>

                    <div class="detail-value">
                        Illustration / Animation / 3D
                    </div>
                </div>

                <div class="detail">
                    <div class="detail-title">
                        Current Direction
                    </div>

                    <div class="detail-value">
                        Visual Development & Creative Work
                    </div>
                </div>

            </div>

        </div>

    </section>


    <!-- =========================
         SKILLS
    ========================== -->

    <section id="skills">

        <div class="section-label">
            02 / Capabilities
        </div>

        <h2 class="section-title">
            What I<br>
            <span class="muted">Create</span>
        </h2>

        <div class="skills-list">

            <div class="skill">
                <div class="skill-number">01</div>
                <div class="skill-name">3D Modeling</div>
                <div class="skill-type">Technical / Visual</div>
            </div>

            <div class="skill">
                <div class="skill-number">02</div>
                <div class="skill-name">Manga Illustration</div>
                <div class="skill-type">2D Art</div>
            </div>

            <div class="skill">
                <div class="skill-number">03</div>
                <div class="skill-name">Animation</div>
                <div class="skill-type">Motion</div>
            </div>

            <div class="skill">
                <div class="skill-number">04</div>
                <div class="skill-name">Character Design</div>
                <div class="skill-type">Concept</div>
            </div>

            <div class="skill">
                <div class="skill-number">05</div>
                <div class="skill-name">Visual Development</div>
                <div class="skill-type">Creative</div>
            </div>

        </div>

    </section>


    <!-- =========================
         WORKS
    ========================== -->

    <section id="works">

        <div class="works-header">

            <div>
                <div class="section-label">
                    03 / Selected Work
                </div>

                <h2 class="section-title">
                    Projects
                </h2>
            </div>

            <p class="works-note">
                A selection of personal projects, experiments,
                illustrations and 3D work. Replace these placeholders
                with your actual portfolio pieces.
            </p>

        </div>


        <div class="works-grid">

            <!-- PROJECT 01 -->

            <article class="work">

                <div class="work-image">
                    3D
                </div>

                <div class="work-info">

                    <div class="work-number">
                        PROJECT 01
                    </div>

                    <h3 class="work-title">
                        3D Modeling
                    </h3>

                    <p class="work-description">
                        A selection of 3D modeling experiments,
                        environments, props, or character work.
                    </p>

                </div>

            </article>


            <!-- PROJECT 02 -->

            <article class="work">

                <div class="work-image">
                    MANGA
                </div>

                <div class="work-info">

                    <div class="work-number">
                        PROJECT 02
                    </div>

                    <h3 class="work-title">
                        Manga Illustration
                    </h3>

                    <p class="work-description">
                        Character illustrations, manga panels,
                        visual experiments and personal artwork.
                    </p>

                </div>

            </article>


            <!-- PROJECT 03 -->

            <article class="work">

                <div class="work-image">
                    ANIM
                </div>

                <div class="work-info">

                    <div class="work-number">
                        PROJECT 03
                    </div>

                    <h3 class="work-title">
                        Animation
                    </h3>

                    <p class="work-description">
                        Short animation experiments exploring movement,
                        timing, character acting and visual storytelling.
                    </p>

                </div>

            </article>


            <!-- PROJECT 04 -->

            <article class="work">

                <div class="work-image">
                    ART
                </div>

                <div class="work-info">

                    <div class="work-number">
                        PROJECT 04
                    </div>

                    <h3 class="work-title">
                        Visual Development
                    </h3>

                    <p class="work-description">
                        Character concepts, environments and visual
                        ideas developed through drawing and 3D work.
                    </p>

                </div>

            </article>

        </div>

    </section>


    <!-- =========================
         CONTACT
    ========================== -->

    <section id="contact">

        <div class="section-label">
            04 / Contact
        </div>

        <h2 class="contact-title">
            Let's make<br>
            <span class="muted">something.</span>
        </h2>

        <p class="contact-description">
            I am interested in creative projects involving illustration,
            animation, 3D modeling and visual development.
        </p>

        <div class="contact-links">

            <!-- Replace these with your real links -->

            <a
                class="contact-link"
                href="mailto:your.email@example.com"
            >
                Email
            </a>

            <a
                class="contact-link"
                href="#"
            >
                ArtStation
            </a>

            <a
                class="contact-link"
                href="#"
            >
                Instagram
            </a>

        </div>

    </section>


    <!-- Footer -->

    <footer>
        <div>
            Takdanai Ramchuen
        </div>

        <div>
            Creative Portfolio
        </div>
    </footer>


    <!-- =========================
         THREE.JS
    ========================== -->

    <script type="module">

        import * as THREE from
            "https://cdn.jsdelivr.net/npm/three@0.179.1/build/three.module.js";


        /* =========================
           SCENE
        ========================== */

        const container =
            document.getElementById("three-container");

        const scene =
            new THREE.Scene();


        /* =========================
           CAMERA
        ========================== */

        const camera =
            new THREE.PerspectiveCamera(
                45,
                window.innerWidth / window.innerHeight,
                0.1,
                100
            );

        camera.position.z = 8;


        /* =========================
           RENDERER
        ========================== */

        const renderer =
            new THREE.WebGLRenderer({
                antialias: true,
                alpha: true
            });

        renderer.setPixelRatio(
            Math.min(window.devicePixelRatio, 2)
        );

        renderer.setSize(
            window.innerWidth,
            window.innerHeight
        );

        renderer.outputColorSpace =
            THREE.SRGBColorSpace;

        container.appendChild(
            renderer.domElement
        );


        /* =========================
           LIGHT
        ========================== */

        const ambientLight =
            new THREE.AmbientLight(
                0xffffff,
                0.6
            );

        scene.add(ambientLight);


        const pointLight =
            new THREE.PointLight(
                0xffffff,
                30,
                30
            );

        pointLight.position.set(
            2,
            3,
            5
        );

        scene.add(pointLight);


        /* =========================
           MAIN OBJECT
        ========================= */

        const geometry =
            new THREE.IcosahedronGeometry(
                2.1,
                2
            );

        const material =
            new THREE.MeshPhysicalMaterial({
                color: 0xaaaaaa,
                roughness: 0.28,
                metalness: 0.65,
                wireframe: true,
                transparent: true,
                opacity: 0.42
            });

        const mainObject =
            new THREE.Mesh(
                geometry,
                material
            );

        mainObject.position.set(
            2.8,
            0.2,
            -1
        );

        scene.add(mainObject);


        /* =========================
           SECOND OBJECT
        ========================= */

        const geometry2 =
            new THREE.TorusKnotGeometry(
                1.15,
                0.035,
                140,
                16
            );

        const material2 =
            new THREE.MeshBasicMaterial({
                color: 0xffffff,
                transparent: true,
                opacity: 0.28,
                wireframe: true
            });

        const secondaryObject =
            new THREE.Mesh(
                geometry2,
                material2
            );

        secondaryObject.position.set(
            -2.8,
            1.8,
            -3
        );

        secondaryObject.scale.setScalar(
            0.8
        );

        scene.add(
            secondaryObject
        );


        /* =========================
           FLOATING PARTICLES
        ========================== */

        const particleCount = 800;

        const positions =
            new Float32Array(
                particleCount * 3
            );

        for (
            let i = 0;
            i < particleCount;
            i++
        ) {

            positions[i * 3] =
                (Math.random() - 0.5) * 18;

            positions[i * 3 + 1] =
                (Math.random() - 0.5) * 12;

            positions[i * 3 + 2] =
                (Math.random() - 0.5) * 12;
        }


        const particleGeometry =
            new THREE.BufferGeometry();

        particleGeometry.setAttribute(
            "position",
            new THREE.BufferAttribute(
                positions,
                3
            )
        );


        const particleMaterial =
            new THREE.PointsMaterial({
                color: 0xffffff,
                size: 0.018,
                transparent: true,
                opacity: 0.45
            });


        const particles =
            new THREE.Points(
                particleGeometry,
                particleMaterial
            );

        scene.add(particles);


        /* =========================
           MOUSE
        ========================== */

        const mouse = {
            x: 0,
            y: 0
        };

        window.addEventListener(
            "mousemove",
            (event) => {

                mouse.x =
                    (event.clientX /
                        window.innerWidth) *
                    2 - 1;

                mouse.y =
                    -(
                        event.clientY /
                        window.innerHeight
                    ) *
                    2 + 1;
            }
        );


        /* =========================
           SCROLL
        ========================== */

        let scrollY = 0;

        window.addEventListener(
            "scroll",
            () => {

                scrollY =
                    window.scrollY;
            }
        );


        /* =========================
           ANIMATION
        ========================== */

        const clock =
            new THREE.Clock();


        function animate() {

            requestAnimationFrame(
                animate
            );

            const elapsed =
                clock.getElapsedTime();


            /* Main object */

            mainObject.rotation.x =
                elapsed * 0.12;

            mainObject.rotation.y =
                elapsed * 0.18;


            mainObject.position.y =
                0.2 +
                Math.sin(elapsed * 0.6) *
                0.15;


            /* Secondary object */

            secondaryObject.rotation.x =
                elapsed * 0.15;

            secondaryObject.rotation.y =
                elapsed * 0.22;


            secondaryObject.position.y =
                1.8 +
                Math.sin(elapsed * 0.7) *
                0.25;


            /* Particles */

            particles.rotation.y =
                elapsed * 0.008;

            particles.rotation.x =
                Math.sin(elapsed * 0.1) *
                0.03;


            /* Mouse parallax */

            const targetX =
                mouse.x * 0.35;

            const targetY =
                mouse.y * 0.25;


            camera.position.x +=
                (
                    targetX -
                    camera.position.x
                ) * 0.025;

            camera.position.y +=
                (
                    targetY -
                    camera.position.y
                ) * 0.025;


            /* Scroll movement */

            mainObject.position.y +=
                scrollY * 0.00015;

            secondaryObject.position.y +=
                scrollY * 0.00008;


            camera.lookAt(
                0,
                0,
                0
            );


            renderer.render(
                scene,
                camera
            );
        }


        animate();


        /* =========================
           RESIZE
        ========================== */

        window.addEventListener(
            "resize",
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
