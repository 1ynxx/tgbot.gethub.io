<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Shop</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200;500&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            font-weight: 200;
            color: #000;
            background: linear-gradient(to bottom, #ffffff, #000000);
            overflow: hidden;
            position: relative;
            transition: background 0.5s, color 0.5s;
        }

        body.dark-theme {
            background: linear-gradient(to bottom, #000000, #434343);
            color: #fff;
        }

        #main {
            width: 100%;
            padding: 20px;
            text-align: center;
            position: relative;
            z-index: 1;
        }

        h1 {
            margin-top: 30px;
            margin-bottom: 10px;
            transition: color 0.5s;
        }

        body.dark-theme h1 {
            color: #fff;
        }

        img {
            width: 100%;
            max-width: 350px;
            margin: 20px auto;
        }

        p {
            width: 100%;
            max-width: 350px;
            margin: 0 auto;
        }

        .button-container {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            margin-top: 20px;
        }

        button, .theme-toggle {
            border: 0;
            border-radius: 5px;
            height: 50px;
            width: 150px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: all 500ms ease;
            color: #fff;
            background: #007bff;
            position: relative;
            overflow: hidden;
            box-shadow: 0 0 10px rgba(0, 123, 255, 0.7);
        }

        .theme-toggle {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 0;
        }

        .theme-toggle img {
            width: 25px;
            height: 25px;
        }

        .theme-toggle.dark {
            background: #f1c40f;
            box-shadow: 0 0 10px #f1c40f;
        }

        button::before {
            content: "";
            position: absolute;
            top: 50%;
            left: 50%;
            width: 300%;
            height: 300%;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            transform: translate(-50%, -50%) scale(0);
            transition: transform 0.5s ease;
        }

        button:hover {
            background: #0056b3;
            transform: scale(1.05);
            box-shadow: 0 0 20px rgba(0, 123, 255, 0.7);
        }

        button:hover::before {
            transform: translate(-50%, -50%) scale(1);
        }

        .emoji {
            position: absolute;
            font-size: 2rem;
            animation: fall 5s linear infinite, rotate 2s linear infinite;
            z-index: 0;
        }

        @keyframes fall {
            0% {
                top: -10%;
                opacity: 1;
            }
            100% {
                top: 110%;
                opacity: 0;
            }
        }

        @keyframes rotate {
            0% {
                transform: rotate(0deg);
            }
            100% {
                transform: rotate(360deg);
            }
        }

        .extra-buttons {
            margin-top: 20px;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
            gap: 10px;
            justify-items: center;
        }

        .extra-buttons button {
            width: 100%;
            max-width: 150px;
            height: 50px;
            font-size: 16px;
            border-radius: 5px;
            border: none;
            cursor: pointer;
            transition: background 0.3s ease, box-shadow 0.3s ease;
            color: white;
            position: relative;
            box-shadow: 0 0 15px;
        }

        .extra-buttons button:hover {
            background: #5a6268;
            box-shadow: 0 0 20px;
        }

        .extra-buttons button:nth-child(1) { background: #ff6347; box-shadow: 0 0 10px #ff6347; }
        .extra-buttons button:nth-child(2) { background: #ff8c00; box-shadow: 0 0 10px #ff8c00; }
        .extra-buttons button:nth-child(3) { background: #ffd700; box-shadow: 0 0 10px #ffd700; }
        .extra-buttons button:nth-child(4) { background: #32cd32; box-shadow: 0 0 10px #32cd32; }
        .extra-buttons button:nth-child(5) { background: #1e90ff; box-shadow: 0 0 10px #1e90ff; }
        .extra-buttons button:nth-child(6) { background: #8a2be2; box-shadow: 0 0 10px #8a2be2; }
        .extra-buttons button:nth-child(7) { background: #ff1493; box-shadow: 0 0 10px #ff1493; }

        .modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 300px;
            padding: 20px;
            background: #fff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            z-index: 1000;
        }

        .modal.dark-theme {
            background: #333;
            color: #fff;
        }

        .modal button {
            display: block;
            width: 100%;
            margin: 10px 0;
        }

        .modal-close {
            display: block;
            margin: 0 auto;
            width: 30px;
            height: 30px;
            background: url('https://img.icons8.com/ios-filled/50/000000/close-window.png') no-repeat center center;
            background-size: contain;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div id="main">
        <h1>Онлайн магазин</h1>
        <img src="https://t3.ftcdn.net/jpg/00/27/57/96/360_F_27579652_tM7V4fZBBw8RLmZo0Bi8WhtO2EosTRFD.jpg" alt="Пицца">
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
        <div class="button-container">
            <button id="buy">Купить</button>
            <button class="theme-toggle" id="theme-toggle">
                <img src="https://img.icons8.com/ios-filled/50/000000/moon-symbol.png" alt="Moon Icon">
            </button>
        </div>
        <div class="extra-buttons">
            <button>Цели 🎯</button>
            <button>Баланс 🏦</button>
            <button>Пополнение 💵</button>
            <button>Вывод 💸</button>
            <button>Стейкинг 🥩</button>
            <button>Справочник 📕</button>
            <button>Настройки ⚙️</button>
        </div>
    </div>

    <div id="settings-modal" class="modal">
        <button id="profile">Профиль</button>
        <button id="change-language">Смена языка</button>
        <button id="about-us">О нас</button>
        <div class="modal-close" id="close-modal"></div>
    </div>

    <audio id="background-music" loop>
        <source src="relaxing_music.wav" type="audio/wav">
        Ваш браузер не поддерживает элемент audio.
    </audio>

    <audio id="click-sound">
        <source src="click_sound.wav" type="audio/wav">
        Ваш браузер не поддерживает элемент audio.
    </audio>

    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <script>
        Telegram.WebApp.ready();

        const backgroundMusic = document.getElementById('background-music');
        const clickSound = document.getElementById('click-sound');
        const themeToggle = document.getElementById('theme-toggle');
        const body = document.body;
        const settingsModal = document.getElementById('settings-modal');
        const closeModal = document.getElementById('close-modal');

        backgroundMusic.volume = 0.5;
        backgroundMusic.play();

        document.getElementById('buy').addEventListener('click', function() {
            clickSound.play();
            Telegram.WebApp.close();
        });

        themeToggle.addEventListener('click', function() {
            body.classList.toggle('dark-theme');
            settingsModal.classList.toggle('dark-theme');
            if (body.classList.contains('dark-theme')) {
                themeToggle.innerHTML = '<img src="https://img.icons8.com/ios-filled/50/000000/sun.png" alt="Sun Icon">';
            } else {
                themeToggle.innerHTML = '<img src="https://img.icons8.com/ios-filled/50/000000/moon-symbol.png" alt="Moon Icon">';
            }
        });

        document.querySelector('.extra-buttons button:nth-child(7)').addEventListener('click', function() {
            settingsModal.style.display = 'block';
        });

        closeModal.addEventListener('click', function() {
            settingsModal.style.display = 'none';
        });

        function createEmoji(emoji) {
            const emojiElement = document.createElement('div');
            emojiElement.classList.add('emoji');
            emojiElement.textContent = emoji;
            emojiElement.style.left = Math.random() * 100 + 'vw';
            emojiElement.style.animationDuration = (Math.random() * 3 + 2) + 's';
            document.body.appendChild(emojiElement);

            setTimeout(() => {
                emojiElement.remove();
            }, 5000);
        }

        setInterval(() => {
            createEmoji('🔥');
            createEmoji('👌');
        }, 500);

        // Adjust theme based on device theme
        const prefersDarkScheme = window.matchMedia("(prefers-color-scheme: dark)");
        if (prefersDarkScheme.matches) {
            body.classList.add('dark-theme');
            settingsModal.classList.add('dark-theme');
            themeToggle.innerHTML = '<img src="https://img.icons8.com/ios-filled/50/000000/sun.png" alt="Sun Icon">';
        }
    </script>
</body>
</html>
