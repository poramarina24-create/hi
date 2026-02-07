<!DOCTYPE html>
<html lang="ro">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Be My Valentine? 🐱</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #ffdae0;
            font-family: 'Arial Rounded MT Bold', 'Helvetica', sans-serif;
            overflow: hidden;
            text-align: center;
        }

        .container {
            background: white;
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 15px 35px rgba(255, 20, 147, 0.2);
            max-width: 400px;
            z-index: 1;
        }

        h1 {
            color: #d63384;
            font-size: 2rem;
            margin-bottom: 20px;
        }

        .gif-container img {
            width: 250px;
            border-radius: 20px;
            margin-bottom: 20px;
        }

        .buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin-top: 30px;
        }

        button {
            padding: 15px 35px;
            font-size: 1.2rem;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
        }

        #yesBtn {
            background-color: #ff4d6d;
            color: white;
            box-shadow: 0 8px 0 #c9184a;
        }

        #yesBtn:active {
            box-shadow: none;
            transform: translateY(4px);
        }

        #noBtn {
            background-color: #6c757d;
            color: white;
            position: absolute; /* Esențial pentru mișcare */
        }

        @keyframes dance {
            0% { transform: rotate(0deg); }
            25% { transform: rotate(5deg); }
            75% { transform: rotate(-5deg); }
            100% { transform: rotate(0deg); }
        }

        .cat-dance {
            animation: dance 0.5s infinite;
        }
    </style>
</head>
<body>

    <div class="container" id="mainContainer">
        <div class="gif-container" id="gifBox">
            <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMmo0c3V4eW1ldXN6N3pueGZ3bmZ4bmZ4bmZ4bmZ4bmZ4bmZ4bmZ4JmVwPXYxX2ludGVybmFsX2dpZl9ieV9pZCZjdD1n/MDJ9IbM3vuzY2qEwuk/giphy.gif" alt="Cute Cat">
        </div>
        <h1 id="question">Vrei să fii Valentine-ul meu? ✨</h1>
        
        <div class="buttons">
            <button id="yesBtn" onclick="celebrate()">DA!</button>
            <button id="noBtn" onmouseover="moveButton()">Nu</button>
        </div>
    </div>

    <script>
        // Funcția care face butonul de "Nu" să fugă
        function moveButton() {
            const noBtn = document.getElementById('noBtn');
            const padding = 50;
            
            // Calculăm limitele ecranului pentru a nu ieși din pagină
            const maxX = window.innerWidth - noBtn.offsetWidth - padding;
            const maxY = window.innerHeight - noBtn.offsetHeight - padding;
            
            const randomX = Math.floor(Math.random() * maxX);
            const randomY = Math.floor(Math.random() * maxY);
            
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
        }

        // Funcția de succes
        function celebrate() {
            // Explozie de confetti
            const duration = 5 * 1000;
            const animationEnd = Date.now() + duration;
            const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

            function randomInRange(min, max) {
              return Math.random() * (max - min) + min;
            }

            const interval = setInterval(function() {
              const timeLeft = animationEnd - Date.now();

              if (timeLeft <= 0) {
                return clearInterval(interval);
              }

              const particleCount = 50 * (timeLeft / duration);
              confetti({...defaults, particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 }});
              confetti({...defaults, particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 }});
            }, 250);

            // Schimbăm conținutul paginii
            const container = document.getElementById('mainContainer');
            container.innerHTML = `
                <div class="cat-dance">
                    <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExOHp6eXNia2Z4bmZ4bmZ4bmZ4bmZ4bmZ4bmZ4bmZ4bmZ4bmZ4bmZ4JmVwPXYxX2ludGVybmFsX2dpZl9ieV9pZCZjdD1n/GeimqsH0TLDt4tScGw/giphy.gif" width="250" style="border-radius: 20px;">
                </div>
                <h1 style="color: #ff4d6d; margin-top: 20px;">YAY! Știam eu! ❤️ 🥳</h1>
                <p style="font-size: 1.2rem; color: #555;">Pregătește-te pentru cea mai tare zi!</p>
            `;
        }
    </script>
</body>
</html>
