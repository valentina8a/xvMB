<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>XV-MB</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Lato:wght@400;700;900&family=Playfair+Display:ital,wght@0,700;0,900;1,700;1,900&display=swap" rel="stylesheet">
    
    <script src="https://cdn.jsdelivr.net/npm/qrcodejs@1.0.0/qrcode.min.js"></script>

    <style>
        /* Custom styles to apply the fonts */
        body {
            font-family: 'Lato', sans-serif; 
            /* *** FONDO NEGRO PURO para el BODY: Es crucial para el neón *** */
            background-color: #000000 !important; 
        }
        .font-title { /* Playfair Display para títulos con elegancia */
            font-family: 'Playfair Display', serif;
            font-weight: 900; 
            font-style: italic; 
        }
        .font-body { /* Lato para el cuerpo de texto, legible y moderno */
            font-family: 'Lato', sans-serif;
            font-weight: 400;
        }
        /* Carnival colors */
        .carnival-pink { color: #EC4899; } /* pink-500 */
        .carnival-yellow { color: #f2e9c2; } 
        .carnival-green { color: #34D399; } /* emerald-400 */
        .carnival-blue { color: #60A5FA; } /* blue-400 */

        /* --- CSS PARA ÍCONOS SVG CON EFECTO NEÓN ROSA --- */
        :root {
            --neon-pink-color: #EC4899; 
        }

        .carnival-pink {
            stroke: var(--neon-pink-color);
        }

        .neon-icon-pink {
            filter: drop-shadow(0 0 5px var(--neon-pink-color)) 
                    drop-shadow(0 0 15px rgba(236, 72, 153, 0.7)) 
                    drop-shadow(0 0 30px rgba(236, 72, 153, 0.4));
            transition: filter 0.3s ease-in-out, transform 0.3s ease-in-out; 
        }

        .card-item:hover .neon-icon-pink {
            filter: drop-shadow(0 0 8px var(--neon-pink-color))
                    drop-shadow(0 0 20px var(--neon-pink-color))
                    drop-shadow(0 0 40px rgba(236, 72, 153, 0.8)); 
            transform: scale(1.05);
        }
        /* --- FIN CSS DE ÍCONOS NEÓN --- */

        /* Animation for floating particles - CUBRE TODO EL BODY SIN OPACIDAD */
        #particles-js {
            position: fixed; 
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: 0; 
        }
        
        /* Contenedor de contenido - Asegura que el contenido esté POR ENCIMA de las partículas */
        .content-wrapper {
            position: relative;
            z-index: 10;
        }

        /* Los elementos interiores tienen un fondo opaco para asegurar la legibilidad del texto */
        .card-item {
            background-color: #000000; /* Fondo negro para los cuadros */
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        /* Styling for the countdown timer */
        .countdown-box {
            background: #000000; /* Fondo sólido negro */
            border: 1px solid #EC4899; /* Borde rosa para que destaque */
            box-shadow: 0 0 15px rgba(236, 72, 153, 0.4);
        }
        
        /* Floating Spotify player styles */
        #spotify-player {
            position: fixed;
            bottom: -380px; 
            right: 20px;
            width: 300px;
            height: 352px;
            transition: bottom 0.5s ease-in-out;
            z-index: 1000;
        }
        #spotify-player.spotify-visible {
            bottom: 20px;
        }
        #spotify-toggle {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 1001;
        }

        /* Fade-in animation on scroll */
        .fade-in-section {
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }
        .fade-in-section.is-visible {
            opacity: 1;
            transform: translateY(0);
        }
        
        /* Neon blinking/pulsing effect */
        .neon-pulse-yellow {
            animation: neon-pulse-yellow 1.5s infinite alternate;
        }
        @keyframes neon-pulse-yellow {
            from { text-shadow: 0 0 5px #fff, 0 0 10px #f2e9c2, 0 0 15px #f0e6c0; }
            to { text-shadow: 0 0 10px #fff, 0 0 20px #fff4d8, 0 0 30px #f0e6c0; }
        }

        .neon-pulse-pink {
            animation: neon-pulse-pink 1.5s infinite alternate;
        }
        @keyframes neon-pulse-pink {
            from { text-shadow: 0 0 5px #fff, 0 0 10px #ec4887, 0 0 15px #EC4899; }
            to { text-shadow: 0 0 10px #fff, 0 0 20px #EC4899, 0 0 30px #EC4899; }
        }
        
        /* --- STYLES FOR GIFT SECTION --- */
        .gift-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 1.8rem;
            cursor: pointer; 
            text-decoration: none; 
            animation: float 3s ease-in-out infinite;
        }

        .icon-wrapper {
            position: relative;
            width: 150px;
            height: 150px;
        }

        .money {
            position: absolute;
            top: 25px;
            left: 10px;
            width: 110px;
            height: 110px;
            transform-origin: center bottom;
            animation: moneyFloat 2.5s ease-in-out infinite;
            filter: drop-shadow(0 0 6px rgba(34, 197, 94, 0.5));
        }

        .envelope {
            position: absolute;
            top: 0;
            left: 0;
            width: 150px;
            height: 150px;
            animation: envelopeBounce 2.5s ease-in-out infinite alternate;
        }

        @keyframes moneyFloat {
            0% { transform: translateY(0) rotate(0deg) scale(1); opacity: 1; }
            25% { transform: translateY(-25px) rotate(-6deg) scale(1.05); }
            50% { transform: translateY(-45px) rotate(6deg) scale(1.1); }
            75% { transform: translateY(-25px) rotate(-4deg) scale(1.05); }
            100% { transform: translateY(0) rotate(0deg) scale(1); opacity: 1; }
        }

        @keyframes envelopeBounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(5px); }
        }
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-15px); }
            100% { transform: translateY(0px); }
        }

        .gift-text {
            font-size: 3rem;
            font-weight: 700;
            color: #fbf0d4;
            letter-spacing: 3px;
            text-transform: uppercase;
            text-align: center;
            text-shadow: 0 0 10px rgba(236, 72, 153, 0.7), 0 0 25px rgba(236, 72, 153, 0.4); 
            animation: shimmer 3s infinite alternate;
        }

        @keyframes shimmer {
            0% { text-shadow: 0 0 10px rgba(255, 255, 255, 0.7), 0 0 20px rgba(236, 72, 153, 0.3); }
            100% { text-shadow: 0 0 15px rgba(255, 255, 255, 0.9), 0 0 35px rgba(236, 72, 153, 0.6); }
        }
        /* --- END OF GIFT SECTION STYLES --- */

        .spotify-hidden {
            opacity: 0;
            bottom: -380px; 
            pointer-events: none;
            transition: all 0.8s ease-in-out;
        }

        .spotify-visible {
            opacity: 1;
            bottom: 20px; 
            pointer-events: auto;
            transition: all 0.8s ease-in-out;
        }

        .rotate-180 {
            transform: rotate(180deg);
        }

        #spotify-player iframe {
            box-shadow: 0 0 25px rgba(236, 72, 153, 0.4); 
            transition: all 0.8s ease-in-out;
        }
        
        /* --- CSS PARA EL BOTÓN DISCO --- */
        .dynamic-disco-button {
            overflow: hidden; 
            border: 3px solid transparent; 
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.2);
        }

        .animate-spin-slow {
            animation: spin-slow 8s linear infinite;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
        }

        @keyframes spin-slow {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .dynamic-disco-button:hover .animate-spin-slow {
            opacity: 1;
            animation-duration: 4s; 
        }

        .dynamic-disco-button .bg-gray-900\/80 {
            transition: background-color 0.3s;
        }

        .dynamic-disco-button:hover .bg-gray-900\/80 {
            background-color: #000000; 
        }
        /* --- FIN CSS BOTÓN DISCO --- */

        /* --- CSS PARA BOTÓN DE UBICACIÓN (PULSACIÓN DE NEÓN AMARILLO) --- */
        .location-pulse-button {
            position: relative;
            border: 2px solid #f2e9c2; 
            color: #f2e9c2; 
            box-shadow: 0 0 10px #f2e9c2, 0 0 20px #f2e9c2; 
            animation: pulse-border-yellow 1.5s infinite alternate; 
            transition: background-color 0.3s, transform 0.3s, color 0.3s;
        }

        .location-pulse-button:hover {
            background-color: #f2e9c2; 
            color: #000000; 
        }

        @keyframes pulse-border-yellow { 
            0% { 
                box-shadow: 0 0 10px #f2e9c2, 0 0 20px #f2e9c2;
                transform: scale(1);
            }
            100% { 
                box-shadow: 0 0 20px #f2e9c2, 0 0 40px #fff8e8;
                transform: scale(1.05);
            }
        }
        /* --- FIN CSS DE UBICACIÓN --- */
    </style>
</head>
<body class="text-white font-body overflow-x-hidden"> 
    <audio id="background-audio" loop src="CRAZY IN LOVE _ DANCE CONCEPT _ RADIG BADALOV CHOREOGRAPHY.mp3" style="display: none;"></audio>
    <div id="particles-js"></div>
    
    <div class="content-wrapper">
        <section class="relative min-h-screen flex flex-col items-center justify-center text-center p-6 overflow-hidden">
            <div class="relative z-10">
                <h2 class="text-4xl md:text-6xl font-title tracking-wider leading-tight" style="font-weight: 200; font-style: normal;">¡Te Invito a Celebrar! </h2>
                <h1 class="font-title text-6xl md:text-8xl my-2" style="font-weight: 900;">
                <span class="font-style: normal">Mis</span> <span class="carnival-yellow">XV</span>
                </h1>
                <p class="font-title text-7xl md:text-9xl carnival-yellow leading-none neon-pulse-yellow" style="font-weight: 900;">Maria Belen</p>
                <p class="font-title text-5xl md:text-7xl carnival-pink neon-pulse-pink" style="font-weight: 700; font-style: normal;">Party Disco</p>

                <div id="countdown" class="flex justify-center gap-2 md:gap-5 mt-12 text-white font-body">
                    <div class="countdown-box p-3 md:p-5 rounded-lg w-20 md:w-28">
                        <div id="days" class="text-3xl md:text-5xl font-bold">00</div>
                        <div class="text-sm md:text-lg">Días</div>
                    </div>
                    <div class="countdown-box p-3 md:p-5 rounded-lg w-20 md:w-28">
                        <div id="hours" class="text-3xl md:text-5xl font-bold">00</div>
                        <div class="text-sm md:text-lg">Horas</div>
                    </div>
                    <div class="countdown-box p-3 md:p-5 rounded-lg w-20 md:w-28">
                        <div id="minutes" class="text-3xl md:text-5xl font-bold">00</div>
                        <div class="text-sm md:text-lg">Minutos</div>
                    </div>
                    <div class="countdown-box p-3 md:p-5 rounded-lg w-20 md:w-28">
                        <div id="seconds" class="text-3xl md:text-5xl font-bold">00</div>
                        <div class="text-sm md:text-lg">Segundos</div>
                    </div>
                </div>
            </div>
        </section>

        <section class="py-20 px-6 fade-in-section"> 
<div class="max-w-4xl mx-auto text-center">
            <h2 class="font-title text-5xl md:text-7xl mb-12 carnival-yellow neon-pulse-yellow" style="font-weight: 700; font-style: normal;">Detalles de la Celebración</h2>
            <div class="grid md:grid-cols-3 gap-8 text-xl md:text-2xl font-body">
                
                <div class="card-item p-8 rounded-xl shadow-lg transform hover:scale-105 transition-transform">
                    <svg class="w-16 h-16 mx-auto mb-4 carnival-pink neon-icon-pink " xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" /></svg>
                    <h3 class="font-bold text-2xl mb-2">Fecha y Hora</h3>
                    <p class="mb-1">Sábado, 22 de Noviembre de 2025</p> 
                    <p>7:30 PM</p>
                </div>
                
                <div class="card-item p-8 rounded-xl shadow-lg transform hover:scale-105 transition-transform">
                    <svg class="w-16 h-16 mx-auto mb-4 carnival-pink neon-icon-pink" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                    </svg>
                    <h3 class="font-bold text-2xl mb-2 text-white">Lugar</h3>
                    <p class="text-gray-300 mb-6">La Siria</p>

                    <a href="https://www.google.com/maps?q=9.283052444458008,-75.39720153808594&z=17&hl=en" target="_blank" 
                    class="location-pulse-button inline-block w-full text-center py-2 px-5 rounded-full font-bold text-lg uppercase tracking-wide
                        bg-transparent
                        transition-all duration-300 ease-in-out
                        focus:outline-none focus:ring-2 focus:ring-pink-300">
                    ¡Mira aquí la ubicación!
                    </a>
                </div>
                
                <div class="card-item p-8 rounded-xl shadow-lg transform hover:scale-105 transition-transform">
                    <svg class="w-16 h-16 mx-auto mb-4 carnival-pink neon-icon-pink" xmlns="http://www.w3.org/2000/svg" fill="none"
                        viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8">
                        <path stroke-linecap="round" stroke-linejoin="round"
                                d="M16 3h-2.5a1.5 1.5 0 0 1-3 0H8L4 6v4l2 1v9a1 1 0 0 0 1 1h10a1 1 0 0 0 1-1v-9l2-1V6l-4-3z"/>
                    </svg>

                    <h3 class="font-bold text-2xl mb-2 text-white">Dress Code</h3>
                    <p class="text-lg mb-1 text-gray-200">Mujeres: Estilo Coctel Brillante</p>
                    <p class="text-lg mb-1 text-gray-200">Hombres: Full Black</p>
                </div>

            </div>
        </div>
        </section>

        <section class="py-20 px-6 text-center fade-in-section">
            <div class="max-w-2xl mx-auto">
                <h2 class="font-title text-5xl md:text-7xl mb-6 carnival-yellow neon-pulse-yellow" style="font-weight: 700; font-style: normal;">Confirma tu Asistencia</h2>
                
<p class="text-xl md:text-2xl mb-8 bg-black p-4 rounded-lg font-body">Te espero para celebrar juntos el inicio de un nuevo capítulo lleno de sueños</p>
                <button id="rsvp-button" class="bg-gradient-to-r from-pink-500 to-fuchsia-600 text-white font-bold text-xl py-4 px-10 rounded-full hover:from-pink-600 hover:to-fuchsia-700 transition-all shadow-xl transform hover:scale-110 border border-white/50" style="box-shadow: 0 0 20px #EC4899;">
                    ¡Sí, voy a celebrar contigo!
                </button>
            </div>
        </section>

        <section class="py-16 fade-in-section">
            <a target="_blank" class="gift-container">
                <div class="icon-wrapper">
                    <svg class="money" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg">
                        <rect x="4" y="16" width="56" height="32" rx="4" ry="4" fill="#22c55e" stroke="#14532d" stroke-width="2"/>
                        <rect x="10" y="22" width="44" height="20" rx="2" ry="2" fill="#86efac" stroke="#14532d" stroke-width="1.5"/>
                        <circle cx="32" cy="32" r="6" fill="#15803d"/>
                        <text x="32" y="36" text-anchor="middle" fill="white" font-size="6" font-weight="bold">$</text>
                    </svg>

                    <svg class="envelope" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M4 18L32 36L60 18V50C60 52.2 58.2 54 56 54H8C5.8 54 4 52.2 4 50V18Z" fill="#374151" stroke="#FBBF24" stroke-width="2"/>
                        <path d="M60 18L32 36L4 18L32 8L60 18Z" stroke="#FBBF24" stroke-width="2" stroke-linejoin="round" stroke-linecap="round"/>
                    </svg>
                </div>

                <span class="gift-text font-title" style="font-weight: 200;">Lluvia de sobres</span>
            </a>
        </section>


        <section class="py-20 px-6 fade-in-section"> 
<div class="max-w-xl mx-auto text-center">
                <h2 class="font-title text-5xl md:text-7xl mb-4 carnival-yellow neon-pulse-yellow" style="font-weight: 700; font-style: normal;">Ideas de Vestuarios para Ti</h2>
                <p class="text-xl md:text-2xl mb-12 font-body">¡Acá puedes encontrar diferentes ideas para que luzcas súper iconic y tomarnos fotos espectaculares!</p>
                
                <div class="card-item p-6 rounded-xl text-center flex flex-col justify-between overflow-hidden relative">
                    <a href="https://pin.it/23Ggv8dTu" target="_blank"
                        class="dynamic-disco-button relative flex flex-col items-center justify-center p-6 w-full h-full rounded-lg transition-all duration-500 ease-in-out">
                        
                        <div class="absolute inset-0 rounded-lg animate-spin-slow"
                            style="background: conic-gradient(from 0deg, #ec4899 0%, #f2e9c2 25%, #60A5FA 50%, #ec4899 75%, #f2e9c2 100%); opacity: 0.7;">
                        </div>
                        
                        <div class="relative z-10 p-4 w-full h-full rounded-lg bg-black/80 backdrop-blur-sm flex flex-col items-center justify-center"> 
<h3 class="font-bold text-3xl mb-2 carnival-yellow neon-pulse-yellow font-title" style="font-weight: 700;">
                                Toca Aquí
                            </h3>
                            <p class="text-lg text-gray-300 tracking-wider font-body">¡Inspírate con los looks!</p>
                        </div>
                    </a>
                    
                    <p class="mt-4 text-gray-400 font-body -pulse-yellow">Color Reservado: Palo de Rosa y Dorado.</p>
                </div>
                </div>
        </section>
        
        <footer class="text-center py-8 text-gray-500 " > 
            <p class="font-title text-2xl mt-2 carnival-pink " style="font-weight: 700; font-style: normal;">MB</p>

            <p class="font-title text-2xl mt-2 carnival-yellow neon-pulse-yellow" style="font-weight: 700; font-style: normal;">¡NOS VEMOS EN LA PISTA!</p>
        </footer>
    </div>
    
    <div id="spotify-player" class="spotify-player spotify-hidden"> 
      <iframe style="border-radius:12px"
        src="https://open.spotify.com/embed/playlist/2tl8uKvJq7NPiuw8j37yHk?utm_source=generator"
        width="100%" height="352" frameBorder="0" allowfullscreen=""
        allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
        loading="lazy">
      </iframe>
    </div>

    <button id="spotify-toggle"
      class="relative bg-gradient-to-r from-pink-500 via-fuchsia-600 to-purple-700 text-white w-16 h-16 rounded-full flex items-center justify-center shadow-2xl transform hover:scale-110 transition-transform duration-300 hover:shadow-pink-400/50 border border-white/20"
      style="box-shadow: 0 0 15px #EC4899;">

      <span class="absolute inset-0 rounded-full bg-pink-500 opacity-30 animate-ping"></span>

      <svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" fill="currentColor"
        viewBox="0 0 24 24" class="relative z-10 transition-transform duration-500" id="spotify-icon">
        <path
          d="M12 2a10 10 0 1 0 10 10A10.011 10.011 0 0 0 12 2zm0 14a4 4 0 1 1 4-4 4.005 4 0 0 1-4 4zm0-6a2 2 0 1 0 2 2 2.002 2 0 0 0-2-2z" />
      </svg>
    </button>

    <script>
      // 🎧 Actualiza el reproductor de Spotify cada 5 minutos automáticamente
      setInterval(() => {
        const iframe = document.querySelector("#spotify-player iframe");
        if (iframe) {
          const src = iframe.src;
          iframe.src = src; // recarga el iframe para reflejar nuevas canciones
          console.log("🔁 Playlist de Spotify actualizada automáticamente");
        }
      }, 300000); // 300000 ms = 5 minutos
    </script>


    <script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
    <script>
        // SVG data para un disco de vinilo más elaborado con reflejos y brillo
        const discoVinyl = `data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><radialGradient id="grad1" cx="50%" cy="50%" r="50%" fx="50%" fy="50%"><stop offset="0%" style="stop-color:%23F3F4F6;stop-opacity:1" /><stop offset="100%" style="stop-color:%23EC4899;stop-opacity:1" /></radialGradient></defs><circle cx="50" cy="50" r="45" fill="%23111827" stroke="url(%23grad1)" stroke-width="3" filter="drop-shadow(0 0 8px %23EC4899)"/><circle cx="50" cy="50" r="18" fill="%23EC4899"/><circle cx="50" cy="50" r="7" fill="%23F3F4F6"/><rect x="20" y="48" width="60" height="4" fill="%23F3F4F6" transform="rotate(30 50 50)" opacity="0.4"/><rect x="20" y="48" width="60" height="4" fill="%23F3F4F6" transform="rotate(90 50 50)" opacity="0.4"/><rect x="20" y="48" width="60" height="4" fill="%23F3F4F6" transform="rotate(150 50 50)" opacity="0.4"/></svg>`;
        
        // Particle animation configuration para un party disco (fucsia, plateado, negro) más atrevido
        particlesJS('particles-js', {
            "particles": {
                "number": { "value": 150, "density": { "enable": true, "value_area": 1200 } }, 
                "color": { "value": ["#EC4899", "#FFFFFF", "#A020F0", "#F2E9C2"] }, 
                "shape": {
                    "type": ["circle", "star", "image"], 
                    "stroke": { "width": 0, "color": "#000000" },
                    "polygon": { "nb_sides": 5 },
                    "image": {
                        "src": discoVinyl, 
                        "width": 100,
                        "height": 100
                    }
                },
                "opacity": { "value": 1, "random": true, "anim": { "enable": true, "speed": 3, "opacity_min": 0.4, "sync": false } },
                "size": { "value": 10, "random": true, "anim": { "enable": true, "speed": 8, "size_min": 3, "sync": false } },
                "line_linked": { "enable": false },
                "move": { "enable": true, "speed": 6, "direction": "bottom", "random": true, "straight": false, "out_mode": "out", "bounce": false,
                    "attract": { "enable": true, "rotateX": 800, "rotateY": 1500 } 
                }
            },
            "interactivity": {
                "detect_on": "canvas",
                "events": {
                    "onhover": { "enable": true, "mode": "bubble" }, 
                    "onclick": { "enable": false }
                },
                "modes": {
                    "bubble": { "distance": 200, "size": 15, "duration": 2, "opacity": 1, "speed": 3 }
                }
            },
            "retina_detect": true
        });

        // Countdown Timer Logic
        const countdown = () => {
            const countDate = new Date("November 22, 2025 19:30:00").getTime();
            const now = new Date().getTime();
            const gap = countDate - now;

            if (gap < 0) {
                document.getElementById('countdown').innerHTML = '<div class="text-3xl font-title carnival-pink">¡La fiesta ya comenzó!</div>';
                return;
            }

            const second = 1000;
            const minute = second * 60;
            const hour = minute * 60;
            const day = hour * 24;

            const textDay = Math.floor(gap / day);
            const textHour = Math.floor((gap % day) / hour);
            const textMinute = Math.floor((gap % hour) / minute);
            const textSecond = Math.floor((gap % minute) / second);

            document.getElementById('days').innerText = String(textDay).padStart(2, '0');
            document.getElementById('hours').innerText = String(textHour).padStart(2, '0');
            document.getElementById('minutes').innerText = String(textMinute).padStart(2, '0');
            document.getElementById('seconds').innerText = String(textSecond).padStart(2, '0');
        };
        setInterval(countdown, 1000);
        countdown();

        // WhatsApp RSVP Button Logic (Botón de Confirmación)
        document.getElementById('rsvp-button').addEventListener('click', () => {
            const phoneNumber = '573144657260'; 
            const message = "¡Hola MB! Con mucho gusto confirmo mi asistencia a tu fiesta de 15 años el 22 de noviembre. ¡ Si voy a celebrar contigo!";
            const whatsappUrl = `https://wa.me/${phoneNumber}?text=${encodeURIComponent(message)}`;
            window.open(whatsappUrl, '_blank');
        });

        // Spotify and Background Audio Logic (Botón de Spotify)
        const backgroundAudio = document.getElementById('background-audio');
        const spotifyPlayerContainer = document.getElementById('spotify-player');
        const spotifyIframe = spotifyPlayerContainer.querySelector('iframe');
        const spotifyToggle = document.getElementById('spotify-toggle');
        const spotifyIcon = document.getElementById("spotify-icon");
        let hasInteracted = false;

         function playBackgroundMusic() {
            if (!hasInteracted) {
                backgroundAudio.play().catch(e => console.log("Autoplay blocked, waiting for interaction."));
                hasInteracted = true;
                document.body.removeEventListener('click', playBackgroundMusic);
                document.body.removeEventListener('touchstart', playBackgroundMusic);
            }
        }
        
        window.addEventListener('load', () => {
            backgroundAudio.play().then(() => {
                hasInteracted = true;
            }).catch(e => {
                document.body.addEventListener('click', playBackgroundMusic);
                document.body.addEventListener('touchstart', playBackgroundMusic);
            });
        });

        spotifyToggle.addEventListener('click', () => {
            spotifyPlayerContainer.classList.toggle('spotify-visible');
            spotifyPlayerContainer.classList.toggle('spotify-hidden');
            spotifyIcon.classList.toggle('rotate-180');
        });

        setInterval(() => {
            // Pausa el audio de fondo si el usuario interactúa con el iframe de Spotify
            if (document.activeElement === spotifyIframe && !backgroundAudio.paused) {
                backgroundAudio.pause();
            }
            // Si el reproductor de Spotify se oculta, intenta reanudar el audio de fondo
            if (spotifyPlayerContainer.classList.contains('spotify-hidden') && backgroundAudio.paused && hasInteracted) {
                 backgroundAudio.play().catch(e => console.log("Error al reanudar audio de fondo."));
            }
        }, 300);
        
        // Scroll Animation Logic
        const sections = document.querySelectorAll('.fade-in-section');
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('is-visible');
                }
            });
        }, {
            threshold: 0.1
        });
        sections.forEach(section => {
            observer.observe(section);
        });

    </script>
</body>
</html>
