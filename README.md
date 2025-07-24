<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="utf-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,%3Csvg width='32' height='32' viewBox='0 0 100 100' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='50' cy='50' r='35' fill='%231A237E'/%3E%3Cellipse cx='50' cy='50' rx='45' ry='25' transform='rotate(-30 50 50)' stroke='%2300BCD4' stroke-width='6' fill='none'/%3E%3Ccircle cx='50' cy='50' r='10' fill='%23FFFFFF'/%3E%3C/svg%3E"/>
    <title>Presentación Omega - Video</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        /* Paleta de Colores Base - Tomada de Omega_updated.html */
        :root {
            --azul-oscuro: #1A237E;
            --morado: #6A1B9A;
            --turquesa: #00BCD4;
            --gris-claro: #F0F0F0;
            --blanco: #FFFFFF;
            --texto-oscuro: #333;
            --texto-intermedio: #555;
            --texto-claro: #ccc;
            --rojo-claro: #e74c3c;
            --rojo-oscuro: #c0392b;
            --verde-claro: #28a745;
            --verde-oscuro: #218838;

            /* Colores para la animación de neuronas */
            --neuron-color-1-rgb: "106, 27, 154"; /* Morado */
            --neuron-color-2-rgb: "0, 188, 212";   /* Turquesa */
            --neuron-color-3-rgb: "26, 35, 126";   /* Azul Oscuro */
            --neuron-connection-rgb: "106, 27, 154"; /* Morado para conexiones por defecto */
        }

        /* Estilos Generales del Cuerpo y Página */
        body {
            font-family: 'Roboto', sans-serif;
            background-color: var(--gris-claro);
            color: var(--texto-oscuro);
            min-height: 100vh;
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            overflow: hidden; /* Ocultar scroll si el contenido no lo necesita */
        }

        #neuronCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }

        #presentationPage {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            width: 100%;
            min-height: 100vh;
            text-align: center;
            position: relative;
            z-index: 2;
            padding: 20px; /* Añadir padding para evitar que el contenido toque los bordes */
            box-sizing: border-box;
        }

        #presentationPage h1 {
            font-size: 4em;
            margin-bottom: 40px;
            color: var(--azul-oscuro);
            text-shadow: 2px 2px 8px rgba(26, 35, 126, 0.4);
            letter-spacing: 2px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        #presentationPage h1 .logo-inline {
            width: 1.8em;
            height: 1.8em;
            vertical-align: middle;
        }

        .video-container {
            width: 100%;
            max-width: 1280px; /* Ancho máximo para el video */
            height: 0;
            padding-bottom: 56.25%; /* 16:9 Aspect Ratio (720 / 1280 = 0.5625) */
            position: relative;
            background-color: rgba(0, 0, 0, 0.8); /* Fondo oscuro para el recuadro del video */
            border-radius: 20px;
            overflow: hidden; /* Asegura que el iframe no se desborde */
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5); /* Sombra más pronunciada */
            margin-top: 20px; /* Espacio debajo del título */
            display: flex; /* Para centrar el iframe */
            justify-content: center;
            align-items: center;
        }

        .video-container iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: none;
            border-radius: 20px; /* Heredar el border-radius del contenedor */
        }

        /* Responsive Adjustments */
        @media (max-width: 1300px) {
            #presentationPage h1 { font-size: 3em; }
            .video-container {
                max-width: 90%; /* Ajustar el ancho máximo para pantallas más pequeñas */
                padding-bottom: 50.625%; /* Mantener el aspecto para 16:9 */
            }
        }

        @media (max-width: 768px) {
            #presentationPage h1 { font-size: 2.2em; margin-bottom: 20px; }
            #presentationPage h1 .logo-inline { width: 1.5em; height: 1.5em; }
            .video-container {
                max-width: 95%;
                padding-bottom: 53.33%; /* Ajuste para 4:3 en móviles si es necesario, o mantener 16:9 */
                border-radius: 15px;
            }
        }

        @media (max-width: 480px) {
            #presentationPage h1 { font-size: 1.8em; margin-bottom: 15px; }
            #presentationPage h1 .logo-inline { width: 1.2em; height: 1.2em; }
            .video-container {
                max-width: 100%;
                padding-bottom: 56.25%; /* Volver a 16:9 para móviles si el ancho es limitado */
                border-radius: 10px;
            }
        }
    </style>
</head>
<body>
    <canvas id="neuronCanvas"></canvas>

    <div id="presentationPage">
        <h1>
            <svg width="100" height="100" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg" class="logo-inline">
              <circle cx="50" cy="50" r="35" fill="var(--blanco)"/>
              <circle cx="50" cy="50" r="30" fill="var(--azul-oscuro)"/>
              <ellipse cx="50" cy="50" rx="45" ry="25" transform="rotate(-30 50 50)" stroke="var(--turquesa)" stroke-width="3" fill="none"/>
              <ellipse cx="50" cy="50" rx="45" ry="25" transform="rotate(30 50 50)" stroke="var(--morado)" stroke-width="3" fill="none"/>
              <circle cx="50" cy="50" r="40" stroke="var(--azul-oscuro)" stroke-width="2" fill="none"/>
              <circle cx="28" cy="58" r="5" fill="var(--turquesa)" class="electron-dot"/>
              <circle cx="72" cy="42" r="5" fill="var(--blanco)" class="electron-dot"/>
              <circle cx="28" cy="42" r="5" fill="var(--morado)" class="electron-dot"/>
              <circle cx="72" cy="58" r="5" fill="var(--blanco)" class="electron-dot"/>
              <circle cx="50" cy="10" r="5" fill="var(--turquesa)" class="electron-dot"/>
              <circle cx="50" cy="90" r="5" fill="var(--blanco)" class="electron-dot"/>
            </svg>
            Presentación Omega
        </h1>

        <div class="video-container">
            <iframe src="https://unireformadaedu.sharepoint.com/sites/clarogt/_layouts/15/embed.aspx?UniqueId=85ede5fc-4b26-4d53-96dc-53120f14078a&nav=%7B%22playbackOptions%22%3A%7B%22startTimeInSeconds%22%3A0%7D%7D&embed=%7B%22ust%22%3Atrue%2C%22hv%22%3A%22CopyEmbedCode%22%7D&referrer=StreamWebApp&referrerScenario=EmbedDialog.Create"
                    width="1280" height="720" frameborder="0" scrolling="no" allowfullscreen title="omega fijo soporte.mp4"></iframe>
        </div>
    </div>

    <script>
        // Colores globales para la animación de neuronas (tomados de Omega_updated.html)
        let globalNeuronColorsRGB = [
            "106, 27, 154", // Morado
            "0, 188, 212",   // Turquesa
            "26, 35, 126"    // Azul Oscuro
        ];
        let globalNeuronConnectionRGB = "106, 27, 154"; // Morado para conexiones por defecto

        (function() {
            const canvas = document.getElementById('neuronCanvas');
            if (!canvas) {
                console.error("Error: Canvas element #neuronCanvas not found for animation.");
                return;
            }
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            let particlesArray = [];

            class Particle {
                constructor(x, y, size, color, speedX, speedY) {
                    this.x = x; this.y = y; this.size = size; this.color = color;
                    this.speedX = speedX; this.speedY = speedY;
                }
                draw() {
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                    ctx.fillStyle = this.color;
                    ctx.fill();
                }
                update() {
                    if (this.x + this.size > canvas.width || this.x - this.size < 0) this.speedX = -this.speedX;
                    if (this.y + this.size > canvas.height || this.y - this.size < 0) this.speedY = -this.speedY;
                    this.x += this.speedX; this.y += this.speedY;
                    this.draw();
                }
            }

            window.init_particles = function() { // Hecho global para actualizaciones de tema
                particlesArray = [];
                const numberOfParticles = (canvas.height * canvas.width) / 10000;
                for (let i = 0; i < numberOfParticles; i++) {
                    const size = Math.random() * 2.5 + 1.5;
                    const x = Math.random() * (innerWidth - size * 2) + size;
                    const y = Math.random() * (innerHeight - size * 2) + size;
                    const speedX = (Math.random() * 0.8) - 0.4;
                    const speedY = (Math.random() * 0.8) - 0.4;
                    const randomRgbString = globalNeuronColorsRGB[Math.floor(Math.random() * globalNeuronColorsRGB.length)];
                    const color = `rgba(${randomRgbString}, 0.7)`;
                    particlesArray.push(new Particle(x, y, size, color, speedX, speedY));
                }
            }

            function animate_particles() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                particlesArray.forEach(particle => particle.update());
                connect_particles();
                requestAnimationFrame(animate_particles);
            }

            window.connect_particles = function() { // Hecho global para actualizaciones de tema
                let opacityValue = 1;
                const connectionRgb = globalNeuronConnectionRGB;
                for (let a = 0; a < particlesArray.length; a++) {
                    for (let b = a + 1; b < particlesArray.length; b++) {
                        let distance = Math.sqrt(((particlesArray[a].x - particlesArray[b].x) ** 2) + ((particlesArray[a].y - particlesArray[b].y) ** 2));
                        if (distance < (canvas.width / 100 * 12) ) {
                            opacityValue = 1 - (distance / (canvas.width / 100 * 12) );
                            ctx.strokeStyle = `rgba(${connectionRgb}, ${opacityValue * 0.4})`;
                            ctx.lineWidth = 0.5;
                            ctx.beginPath();
                            ctx.moveTo(particlesArray[a].x, particlesArray[a].y);
                            ctx.lineTo(particlesArray[b].x, particlesArray[b].y);
                            ctx.stroke();
                        }
                    }
                }
            }
            init_particles();
            animate_particles();
            window.addEventListener('resize', () => {
                canvas.width = innerWidth; canvas.height = innerHeight;
                init_particles();
            });
        })();
    </script>
</body>
</html>
