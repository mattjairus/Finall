<!DOCTYPE html>
<html>
<head>
    <title>Will you be my Valentine? 💌</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #ffe6f2 0%, #ffc2d1 100%);
            min-height: 100vh;
            font-family: 'Segoe UI', 'Arial', sans-serif;
            overflow-x: hidden;
            position: relative;
        }

        .floating-heart {
            position: absolute;
            color: #ff69b4;
            opacity: 0.5;
            animation: float 8s linear infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% { opacity: 0.5; }
            90% { opacity: 0.5; }
            100% {
                transform: translateY(-20vh) rotate(360deg);
                opacity: 0;
            }
        }

        .container {
            text-align: center;
            padding: 50px 20px;
            position: relative;
            z-index: 10;
            margin-top: 60px;
        }

        .card {
            background: white;
            max-width: 500px;
            margin: 0 auto;
            padding: 40px 30px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(255, 105, 180, 0.2);
            position: relative;
        }

        .card::before, .card::after {
            content: "❤️";
            position: absolute;
            font-size: 24px;
        }

        .card::before { top: 20px; left: 20px; }
        .card::after { top: 20px; right: 20px; }

        h1 {
            color: #d63384;
            font-size: 2.2rem;
            margin-bottom: 30px;
            text-shadow: 2px 2px 4px rgba(255, 105, 180, 0.3);
        }

        .subtitle {
            color: #6c757d;
            font-size: 1.1rem;
            margin-bottom: 40px;
            line-height: 1.5;
        }

        button {
            margin: 10px;
            padding: 15px 35px;
            font-size: 18px;
            cursor: pointer;
            border: none;
            border-radius: 30px;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            position: relative;
        }

        #yesBtn {
            background-color: #ff69b4;
            color: white;
        }

        #yesBtn:hover {
            background-color: #d63384;
            transform: scale(1.05);
            box-shadow: 0 8px 20px rgba(255, 105, 180, 0.3);
        }

        #noBtn {
            background-color: #6495ED;
            color: white;
            transition: transform 0.2s ease;
        }

        #noBtn:hover {
            background-color: #4169e1;
            transform: scale(1.05);
            box-shadow: 0 8px 20px rgba(100, 149, 237, 0.3);
        }

        .moving-btn {
            cursor: default;
            background-color: #b0c4de !important;
        }

        /* Hide GIF by default */
        #happyBoyGif {
            display: none;
            margin: 30px auto;
            max-width: 300px;
            height: auto;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .footer {
            margin-top: 30px;
            color: #6c757d;
            font-style: italic;
        }

        @media (max-width: 480px) {
            h1 { font-size: 1.8rem; }
            #yesBtn {
                display: block;
                width: 80%;
                margin: 15px auto;
            }
            #noBtn {
                position: relative;
                width: 80%;
                margin: 15px auto;
            }
            .card { padding: 30px 20px; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="card">
            <h1>Will you be my Valentine? 💌</h1>
            <p class="subtitle">Every moment with you feels like magic... I want to make this Valentine's Day unforgettable with YOU.</p>
            
            <button id="yesBtn">Yes, I do! ❤️</button>
            <button id="noBtn">No</button>
            
            <!-- Happy boy jumping GIF - hidden by default -->
            <img id="happyBoyGif" src="https://media.giphy.com/media/3ohhwE9cP7p2jp8hqA/giphy.gif" alt="Happy boy jumping in celebration">
            
            <div class="footer">Made with all my love ❤️</div>
        </div>
    </div>

    <script>
        function createFloatingHearts() {
            const heartCount = 15;
            for (let i = 0; i < heartCount; i++) {
                const heart = document.createElement('div');
                heart.className = 'floating-heart';
                heart.textContent = '❤️';
                heart.style.fontSize = `${Math.random() * 20 + 10}px`;
                heart.style.left = `${Math.random() * 100}vw`;
                heart.style.animationDelay = `${Math.random() * 8}s`;
                heart.style.animationDuration = `${Math.random() * 10 + 5}s`;
                document.body.appendChild(heart);
            }
        }

        // Track No button clicks
        let clickCount = 0;
        const messages = [
            "Are you sure? 🥺",
            "why don't we try? 💖",
            "okay try your best"
        ];

        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const happyBoyGif = document.getElementById('happyBoyGif');
        const card = document.querySelector('.card');
        const cardRect = card.getBoundingClientRect();

        // Yes button action
        yesBtn.addEventListener('click', function() {
            alert("Yeyy, you can't take that back");
            // Show the GIF after the alert
            happyBoyGif.style.display = 'block';
            // Optional: Disable buttons after Yes is clicked
            yesBtn.disabled = true;
            noBtn.disabled = true;
            noBtn.style.cursor = 'not-allowed';
        });

        // No button action
        noBtn.addEventListener('click', function() {
            if (clickCount < messages.length) {
                alert(messages[clickCount]);
                clickCount++;
                setTimeout(() => noBtn.focus(), 10);
            }
        });

        // No button movement after 3 clicks
        noBtn.addEventListener('mouseover', function() {
            if (clickCount >= messages.length) {
                noBtn.classList.add('moving-btn');
                const maxX = cardRect.width - noBtn.offsetWidth - 40;
                const maxY = cardRect.height - noBtn.offsetHeight - 80;
                const randomX = Math.floor(Math.random() * maxX);
                const randomY = Math.floor(Math.random() * maxY);
                noBtn.style.left = `${randomX}px`;
                noBtn.style.top = `${randomY}px`;
            }
        });

        createFloatingHearts();
    </script>
</body>
</html>
