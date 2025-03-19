<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Feliz Día del Padre</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow-x: hidden;
        }
        
        .container {
            position: relative;
            width: 90%;
            max-width: 600px;
            background-color: #ffffff;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            padding: 30px;
            text-align: center;
        }
        
        h1 {
            color: #2c3e50;
            margin-bottom: 20px;
            font-size: 28px;
        }
        
        p {
            color: #7f8c8d;
            line-height: 1.6;
            margin-bottom: 20px;
            font-size: 16px;
        }
        
        .btn {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 20px;
            transition: background-color 0.3s;
        }
        
        .btn:hover {
            background-color: #2980b9;
        }
        
        .heart {
            color: #e74c3c;
            display: inline-block;
            animation: pulse 1.5s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.3); }
            100% { transform: scale(1); }
        }
        
        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background-color: #f0f;
            position: absolute;
            top: -10px;
            z-index: -1;
        }
        
        .image-container {
            width: 300px;
            height: 300px;
            margin: 20px auto;
            position: relative;
            overflow: hidden;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .image-slide {
            width: 100%;
            height: 100%;
            background-size: cover;
            background-position: center;
            position: absolute;
            top: 0;
            left: 0;
            opacity: 0;
            transition: opacity 1s ease-in-out;
        }
        
        .image-slide.active {
            opacity: 1;
        }
        
        .carousel-controls {
            display: flex;
            justify-content: center;
            margin-top: 15px;
        }
        
        .carousel-dot {
            width: 12px;
            height: 12px;
            background-color: #ccc;
            border-radius: 50%;
            margin: 0 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .carousel-dot.active {
            background-color: #3498db;
        }
        
        @media (max-width: 600px) {
            h1 {
                font-size: 24px;
            }
            
            p {
                font-size: 14px;
            }
            
            .image-container {
                width: 250px;
                height: 250px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>¡Feliz Día del Padre!</h1>
        <p>Para el mejor padre del mundo</p>
        
        <div class="image-container" id="imageSlider">
            <!-- Placeholder images - reemplazar URLs con imágenes reales cuando sea posible -->
            <div class="image-slide active" style="background-image: url('img/padre2.jpg')"></div>
            <div class="image-slide" style="background-image: url('img/padre3.jpg')"></div>
            <div class="image-slide" style="background-image: url('img/padre4.jpg')"></div>
            <div class="image-slide" style="background-image: url('img/padre5.jpg')"></div>
        </div>
        
        <div class="carousel-controls" id="carouselDots">
            <div class="carousel-dot active" data-index="0"></div>
            <div class="carousel-dot" data-index="1"></div>
            <div class="carousel-dot" data-index="2"></div>
            <div class="carousel-dot" data-index="3"></div>
        </div>
        
        <p>Gracias por ser mi guía, mi apoyo y mi héroe. Por todas las veces que me has ayudado, aconsejado y hecho reír. Por estar siempre ahí para mí.</p>
        <p>Te quiero mucho, papi <span class="heart">❤</span></p>
        
        <button class="btn" id="rotateBtn">Rotar Imágenes</button>
        <button class="btn" id="confettiBtn" style="margin-left: 10px; background-color: #e74c3c;">¡Celebremos!</button>
    </div>

    <script>
        // Variables para el carrusel de imágenes
        const slides = document.querySelectorAll('.image-slide');
        const dots = document.querySelectorAll('.carousel-dot');
        const rotateBtn = document.getElementById('rotateBtn');
        const confettiBtn = document.getElementById('confettiBtn');
        let currentSlide = 0;
        let isRotating = false;
        let rotationInterval;
        
        // Función para mostrar una diapositiva específica
        function showSlide(index) {
            // Desactivar todas las diapositivas y puntos
            slides.forEach(slide => slide.classList.remove('active'));
            dots.forEach(dot => dot.classList.remove('active'));
            
            // Activar la diapositiva y punto actual
            slides[index].classList.add('active');
            dots[index].classList.add('active');
            
            // Actualizar el índice actual
            currentSlide = index;
        }
        
        // Configurar oyentes de eventos para los puntos
        dots.forEach(dot => {
            dot.addEventListener('click', function() {
                const slideIndex = parseInt(this.getAttribute('data-index'));
                showSlide(slideIndex);
                
                // Detener la rotación automática si está activa
                if (isRotating) {
                    clearInterval(rotationInterval);
                    isRotating = false;
                    rotateBtn.textContent = 'Rotar Imágenes';
                }
            });
        });
        
        // Función para rotar a la siguiente diapositiva
        function nextSlide() {
            let next = currentSlide + 1;
            if (next >= slides.length) {
                next = 0;
            }
            showSlide(next);
        }
        
        // Función para alternar la rotación automática
        rotateBtn.addEventListener('click', function() {
            if (isRotating) {
                // Detener la rotación
                clearInterval(rotationInterval);
                isRotating = false;
                this.textContent = 'Rotar Imágenes';
            } else {
                // Iniciar la rotación
                rotationInterval = setInterval(nextSlide, 2000); // Cambiar cada 2 segundos
                isRotating = true;
                this.textContent = 'Detener Rotación';
                
                // Avanzar inmediatamente a la siguiente diapositiva
                nextSlide();
            }
        });
        
        // Función para crear y animar confeti
        confettiBtn.addEventListener('click', function() {
            createConfetti();
        });
        
        function createConfetti() {
            const colors = ['#f94144', '#f3722c', '#f8961e', '#f9c74f', '#90be6d', '#43aa8b', '#577590', '#277da1'];
            const confettiCount = 100;
            
            for (let i = 0; i < confettiCount; i++) {
                let confetti = document.createElement('div');
                confetti.className = 'confetti';
                
                // Propiedades aleatorias para cada confeti
                const size = Math.random() * 10 + 5;
                const background = colors[Math.floor(Math.random() * colors.length)];
                const left = Math.random() * 100 + '%';
                const opacity = Math.random() + 0.5;
                
                confetti.style.width = size + 'px';
                confetti.style.height = size + 'px';
                confetti.style.backgroundColor = background;
                confetti.style.left = left;
                confetti.style.opacity = opacity;
                
                document.body.appendChild(confetti);
                
                // Animación del confeti
                const animation = confetti.animate(
                    [
                        { transform: 'translate3d(0, 0, 0)', opacity: opacity },
                        { transform: `translate3d(${Math.random() * 250 - 125}px, ${window.innerHeight}px, 0)`, opacity: 0 }
                    ],
                    {
                        duration: Math.random() * 3000 + 2000,
                        easing: 'cubic-bezier(0, .9, .57, 1)',
                        delay: Math.random() * 1500
                    }
                );
                
                animation.onfinish = function() {
                    confetti.remove();
                };
            }
        }
    </script>
</body>
</html>
