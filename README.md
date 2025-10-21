# birthday_wish
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday 🎉</title>
    <style>
        /* Reset and base styles for mobile responsiveness */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #ff69b4, #8e44ad); /* Romantic gradient: soft pink to purple */
            color: #333;
            text-align: center;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        .container {
            padding: 20px;
            max-width: 100%;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            position: relative;
            z-index: 10;
            background: rgba(255, 255, 255, 0.8); /* Semi-transparent overlay for readability */
            border-radius: 15px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.2);
        }

        h1 {
            font-size: 2.5em;
            color: #d63384;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
            animation: bounce 2s infinite;
            position: relative;
        }

        h1::before, h1::after {
            content: '✨';
            position: absolute;
            animation: sparkle 1.5s infinite alternate;
        }

        h1::before { left: -20px; top: -10px; }
        h1::after { right: -20px; top: -10px; animation-delay: 0.5s; }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }

        @keyframes sparkle {
            from { opacity: 0.5; transform: scale(1); }
            to { opacity: 1; transform: scale(1.2); }
        }

        .countdown {
            background: rgba(255,255,255,0.9);
            padding: 15px;
            border-radius: 15px;
            margin: 20px 0;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            font-size: 1.2em;
            color: #d63384;
            animation: fadeIn 1s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.9); }
            to { opacity: 1; transform: scale(1); }
        }

        .buttons-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
            margin: 20px 0;
            background: rgba(255, 255, 255, 0.8);
            padding: 15px;
            border-radius: 15px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            animation: fadeIn 1s ease-in-out;
        }

        button {
            background: linear-gradient(135deg, #ff69b4, #8e44ad); /* Matching romantic gradient */
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 1.1em;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            animation: pulse 2s infinite ease-in-out;
            touch-action: manipulation;
            margin: 5px;
        }

        button:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 12px rgba(0,0,0,0.3);
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.02); }
            100% { transform: scale(1); }
        }

        .confetti {
            position: fixed;
            z-index: 1000;
            pointer-events: none;
            animation: fall linear infinite;
        }

        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(720deg);
            }
        }

        .gallery {
            display: flex;
            overflow-x: auto;
            margin: 20px 0;
            padding: 10px;
            background: rgba(255,255,255,0.8);
            border-radius: 15px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }

        .gallery img {
            width: 150px;
            height: 150px;
            object-fit: cover;
            margin: 0 10px;
            border-radius: 10px;
            border: 2px solid #ff6b6b;
            transition: transform 0.3s ease;
        }

        .gallery img:hover {
            transform: scale(1.1);
        }
    </style>
</head>
<body>
    <audio id="bgMusic" loop>
        <source src="birthday-tune.mp3" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>

    <div class="container">
        <h1>Happy Birthday  🎂✨</h1>
        <p>On this special day in 2026, I wanted to make something just for you. You're the light in my life, and I'm so grateful for you. Let's celebrate with some magic!</p>

        <div id="countdown" class="countdown">Countdown to October 23, 2026: Loading...</div>

        <div class="gallery">
             <img src="pic3.jpg" alt="Us together">
            <img src="cake.jpg" alt="Birthday cake">
            <img src="birthday.jpg" alt="Kartik lights">
        </div>

        <div class="buttons-container">
            <button onclick="toggleMusic()">Play/Pause Music 🎵</button>
            <button onclick="revealSurprise()">Reveal Hidden Message! 💖</button>
            <button id="finalButton" onclick="revealFinal()">See the Final Message ❤️</button>
            <button onclick="createConfetti()">Even More Confetti! 🎊</button>
            <button onclick="openCamera()">Do you want to see that special person I like? 📸</button>
        </div>
        
        <div id="hiddenMsg" style="display: none;">
            <strong>Hidden Message Revealed:</strong> Remember our first Kartik together? You made it unforgettable. On October 23, 2026, I promise more adventures and love. You're my everything! 🎈
        </div>
        
        <div id="finalMsg" style="display: none;">
            <strong>Final Message:</strong> As October 23, 2026, arrives, know that my heart is yours forever. You've made my world brighter—happy birthday, my dear. I love you more than words can say. 🌟💕
        </div>
    </div>

    <script>
        function updateCountdown() {
            const birthdayDate = new Date(2026, 9, 23);  // October 23, 2026
            if (new Date() > birthdayDate) birthdayDate.setFullYear(birthdayDate.getFullYear() + 1);
            document.getElementById('countdown').innerHTML = `Next Birthday: October 23, 2026 <br> Countdown: Calculating...`;
            const now = new Date().getTime();
            const distance = birthdayDate - now;
            const days = Math.floor(distance / (1000 * 60 * 60 * 24));
            const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((distance % (1000 * 60)) / 1000);
            document.getElementById('countdown').innerHTML = `Next Birthday: October 23, 2026 <br> Countdown: ${days}d ${hours}h ${minutes}m ${seconds}s`;
            if (distance > 0) setTimeout(updateCountdown, 1000);
        }
        window.addEventListener('load', updateCountdown);

        function toggleMusic() {
            const music = document.getElementById('bgMusic');
            if (music.paused) music.play().then(() => music.volume = 0.3);
            else music.pause();
        }

        function createConfetti() {
            for (let i = 0; i < 150; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.width = confetti.style.height = Math.random() * 12 + 6 + 'px';
                confetti.style.background = ['#ff69b4', '#8e44ad', '#d63384', '#96ceb4', #feca57'][Math.floor(Math.random() * 5)];  // Updated to match romantic colors
                document.body.appendChild(confetti);
                setTimeout(() => confetti.remove(), 5000);
            }
        }

        function revealSurprise() {
            document.getElementById('hiddenMsg').style.display = 'block';
            createConfetti();
            document.getElementById('finalButton').style.display = 'block';
        }

        function revealFinal() {
            document.getElementById('finalMsg').style.display = 'block';
            createConfetti();
        }

        function openCamera() {
            const overlay = document.createElement('div');
            overlay.id = 'cameraOverlay';
            overlay.style.cssText = 'position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.8);z-index:3000;display:flex;justify-content:center;align-items:center;flex-direction:column;color:white;';
            const video = document.createElement('video');
            video.id = 'cameraVideo';
            video.style.cssText = 'width:90%;max-width:400px;border-radius:15px;';
            video.autoplay = true;
            overlay.appendChild(video);
            const closeBtn = document.createElement('button');
            closeBtn.innerHTML = 'Close Camera ❤️';
            closeBtn.onclick = () => { document.body.removeChild(overlay); video.srcObject.getTracks()[0].stop(); };
            overlay.appendChild(closeBtn);
            document.body.appendChild(overlay);
            navigator.mediaDevices.getUserMedia({ video: { facingMode: 'user' } }).then(stream => video.srcObject = stream).catch(err => alert('Camera access denied.'));
        }

        window.addEventListener('load', createConfetti);
    </script>
</body>
</html>
