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
            margin-top: 20px;
            margin-bottom: 10px;
            font-size: 24px;
            transition: color 0.5s;
        }

        body.dark-theme h1 {
            color: #fff;
        }

        img {
            width: 80%;
            max-width: 300px;
            margin: 20px auto;
            display: block;
        }

        p {
            width: 80%;
            max-width: 300px;
            margin: 0 auto 20px;
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
            height: 45px;
            width: 140px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: all 500ms ease;
            color: #fff;
            background: #007bff;
            position: relative;
        }

        .theme-toggle {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 0;
        }

        .theme-toggle img {
            width: 20px;
            height: 20px;
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
        }

        .emoji {
            position: absolute;
            font-size: 2rem;
            animation: fall 8s linear infinite, rotate 5s linear infinite;
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
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            justify-items: center;
        }

        .extra-buttons button {
            width: 100%;
            max-width: 100px;
            height: 40px;
            font-size: 14px;
            border-radius: 5px;
            border: none;
            cursor: pointer;
            transition: background 0.3s ease, box-shadow 0.3s ease;
            color: white;
            position: relative;
            box-shadow: 0 0 5px;
        }

        .extra-buttons button:nth-child(1) { background: #ff6347; box-shadow: 0 0 5px #ff6347; }
        .extra-buttons button:nth-child(2) { background: #ff8c00; box-shadow: 0 0 5px #ff8c00; }
        .extra-buttons button:nth-child(3) { background: #ffd700; box-shadow: 0 0 5px #ffd700; }
        .extra-buttons button:nth-child(4) { background: #32cd32; box-shadow: 0 0 5px #32cd32; }
        .extra-buttons button:nth-child(5) { background: #1e90ff; box-shadow: 0 0 5px #1e90ff; }
        .extra-buttons button:nth-child(6) { background: #8a2be2; box-shadow: 0 0 5px #8a2be2; }
        .extra-buttons button:nth-child(7) { background: #ff1493; box-shadow: 0 0 5px #ff1493; }

        .extra-buttons button:hover {
            box-shadow: 0 0 8px;
        }

        .modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80%;
            max-width: 300px;
            padding: 20px;
            background: #fff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            z-index: 1000;
            opacity: 1;
            transition: opacity 0.2s ease-in-out;
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
            margin: 10px auto 0;
            width: 30px;
            height: 30px;
            background: url('https://img.icons8.com/ios-filled/50/000000/close-window.png') no-repeat center center;
            background-size: contain;
            cursor: pointer;
        }

        .floating-button {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: #007bff;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            transition: transform 0.5s ease;
        }

        .floating-button.clicked {
            transform: rotate(90deg);
        }

        .floating-button img {
            width: 30px;
            height: 30px;
        }

        .dropdown-buttons {
            display: none;
            position: absolute;
            top: 80px;
            right: 20px;
            flex-direction: column;
            gap: 10px;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 10px;
            padding: 10px;
            backdrop-filter: blur(5px);
        }

        .dropdown-buttons button {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: rgba(0, 123, 255, 0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        .dropdown-buttons button img {
            width: 25px;
            height: 25px;
        }

        .dropdown-buttons button:hover {
            background: rgba(0, 86, 179, 0.8);
        }

        .dropdown-buttons.show {
            display: flex;
        }

        #gift-button {
            width: 100%;
            max-width: 100px;
            height: 40px;
            font-size: 14px;
            border-radius: 5px;
            border: none;
            cursor: pointer;
            transition: background 0.3s ease, box-shadow 0.3s ease;
            color: white;
            background: #ff69b4;
            position: relative;
            box-shadow: 0 0 5px #ff69b4;
        }

        #gift-button:hover {
            box-shadow: 0 0 8px;
        }

        .rainbow-button {
            position: fixed;
            bottom: 20px;
            right: 20px;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: linear-gradient(135deg, #ff0099, #493240, #00ff00, #00ffff, #0000ff, #ff00ff);
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            animation: rainbow 5s linear infinite;
        }

        @keyframes rainbow {
            0% { filter: hue-rotate(0deg); }
            100% { filter: hue-rotate(360deg); }
        }

        .rainbow-button-inner {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: #fff;
        }

        #roulette {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 200px;
            height: 200px;
            border-radius: 50%;
            background: conic-gradient(#ff6347 0deg 90deg, #ffd700 90deg 180deg, #32cd32 180deg 270deg, #1e90ff 270deg 360deg);
            position: relative;
        }

        #roulette:after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 20px;
            height: 20px;
            background: #fff;
            border-radius: 50%;
            z-index: 1;
        }

        .roulette-segment {
            position: absolute;
            width: 50%;
            height: 50%;
            top: 0;
            left: 0;
            transform-origin: 100% 100%;
            clip-path: polygon(0 0, 100% 0, 100% 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            font-weight: bold;
            color: #fff;
        }

        .segment1 { transform: rotate(45deg); }
        .segment2 { transform: rotate(135deg); }
        .segment3 { transform: rotate(225deg); }
        .segment4 { transform: rotate(315deg); }

        .user-info-modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80%;
            max-width: 300px;
            padding: 20px;
            background: #fff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            z-index: 1000;
            opacity: 1;
            transition: opacity 0.2s ease-in-out;
        }

        .user-info-modal.dark-theme {
            background: #333;
            color: #fff;
        }

        .user-info-modal button {
            display: block;
            width: 100%;
            margin: 10px 0;
        }

        .user-info-avatar {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            margin: 10px auto;
            background-size: cover;
            background-position: center;
            cursor: pointer;
        }

        .user-info-nickname {
            text-align: center;
            font-size: 18px;
            font-weight: bold;
        }

        .color-picker-modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80%;
            max-width: 300px;
            padding: 20px;
            background: #fff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            z-index: 1000;
            opacity: 1;
            transition: opacity 0.2s ease-in-out;
        }

        .color-picker-modal.dark-theme {
            background: #333;
            color: #fff;
        }

        .color-picker {
            width: 100%;
            height: 150px;
            margin: 20px 0;
            background: linear-gradient(to right, #ff0000, #00ff00, #0000ff);
            border-radius: 10px;
        }

        .color-picker-controls {
            display: flex;
            justify-content: space-between;
        }

        .color-picker-button {
            width: 45%;
            padding: 10px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        .color-picker-button:hover {
            background: #ddd;
        }
    </style>
</head>
<body>
    <div id="main">
        <div class="floating-button" id="floating-button">
            <img src="https://img.icons8.com/ios-filled/50/ffffff/menu.png" alt="Menu Icon">
        </div>
        <div class="dropdown-buttons" id="dropdown-buttons">
            <button id="theme-button"><img src="https://img.icons8.com/ios-filled/50/ffffff/moon-symbol.png" alt="Theme Icon"></button>
            <button id="user-info-button"><img src="https://img.icons8.com/ios-filled/50/ffffff/user.png" alt="User Icon"></button>
            <button><img src="https://img.icons8.com/ios-filled/50/ffffff/info.png" alt="Info Icon"></button>
            <button id="settings-button"><img src="https://img.icons8.com/ios-filled/50/ffffff/settings.png" alt="Settings Icon"></button>
        </div>
        <h1>Онлайн магазин</h1>
        <img src="https://t3.ftcdn.net/jpg/00/27/57/96/360_F_27579652_tM7V4fZBBw8RLmZo0Bi8WhtO2EosTRFD.jpg" alt="Пицца">
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
        <div class="button-container">
            <button id="buy">Купить</button>
            <button id="gift-button">Подарок 🎁</button>
        </div>
        <div class="extra-buttons">
            <button>Цели 🎯</button>
            <button>Баланс 🏦</button>
            <button>Пополнение 💵</button>
            <button>Вывод 💸</button>
            <button>Стейкинг 🥩</button>
            <button>Справочник 📕</button>
        </div>
    </div>

    <div id="settings-modal" class="modal">
        <button id="profile">Профиль</button>
        <button id="change-language">Смена языка</button>
        <button id="toggle-sound">Отключить звук</button>
        <div class="modal-close" id="close-modal"></div>
    </div>

    <div id="gift-modal" class="modal">
        <div id="roulette">
            <div class="roulette-segment segment1">Приз 1</div>
            <div class="roulette-segment segment2">Приз 2</div>
            <div class="roulette-segment segment3">Приз 3</div>
            <div class="roulette-segment segment4">Приз 4</div>
        </div>
        <div class="modal-close" id="close-gift-modal"></div>
    </div>

    <div id="user-info-modal" class="user-info-modal">
        <div class="user-info-avatar" id="user-avatar" style="background-image: url('https://via.placeholder.com/80');"></div>
        <div class="user-info-nickname" id="user-nickname">Username</div>
        <div class="user-info-details">
            <p>Дата регистрации: <span id="registration-date">01.01.2020</span></p>
            <p>Количество рефералов: <span id="referrals-count">10</span></p>
        </div>
        <div class="modal-close" id="close-user-info-modal"></div>
    </div>

    <div id="color-picker-modal" class="color-picker-modal">
        <div class="color-picker" id="color-picker"></div>
        <div class="color-picker-controls">
            <button class="color-picker-button" id="confirm-color">Подтвердить</button>
            <button class="color-picker-button" id="cancel-color">Отменить</button>
        </div>
    </div>

    <audio id="background-music" loop>
        <source src="C:/Users/den/Downloads/relaxing_music.wav" type="audio/wav">
        Ваш браузер не поддерживает элемент audio.
    </audio>

    <audio id="click-sound">
        <source src="C:/Users/den/Downloads/click_sound.wav" type="audio/wav">
        Ваш браузер не поддерживает элемент audio.
    </audio>

    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <script>
        Telegram.WebApp.ready();

        const backgroundMusic = document.getElementById('background-music');
        const clickSound = document.getElementById('click-sound');
        const themeToggle = document.getElementById('theme-button');
        const body = document.body;
        const settingsModal = document.getElementById('settings-modal');
        const closeModal = document.getElementById('close-modal');
        const settingsButton = document.getElementById('settings-button');
        const floatingButton = document.getElementById('floating-button');
        const dropdownButtons = document.getElementById('dropdown-buttons');
        const giftButton = document.getElementById('gift-button');
        const giftModal = document.getElementById('gift-modal');
        const closeGiftModal = document.getElementById('close-gift-modal');
        const userInfoButton = document.getElementById('user-info-button');
        const userInfoModal = document.getElementById('user-info-modal');
        const closeUserInfoModal = document.getElementById('close-user-info-modal');
        const rainbowButton = document.getElementById('rainbow-button');
        const colorPickerModal = document.getElementById('color-picker-modal');
        const confirmColorButton = document.getElementById('confirm-color');
        const cancelColorButton = document.getElementById('cancel-color');
        const colorPicker = document.getElementById('color-picker');
        const toggleSoundButton = document.getElementById('toggle-sound');

        backgroundMusic.volume = 0.5;
        backgroundMusic.play();

        document.getElementById('buy').addEventListener('click', function() {
            clickSound.play();
            Telegram.WebApp.close();
        });

        themeToggle.addEventListener('click', function() {
            body.classList.toggle('dark-theme');
            settingsModal.classList.toggle('dark-theme');
            giftModal.classList.toggle('dark-theme');
            userInfoModal.classList.toggle('dark-theme');
            colorPickerModal.classList.toggle('dark-theme');
            if (body.classList.contains('dark-theme')) {
                themeToggle.innerHTML = '<img src="https://img.icons8.com/ios-filled/50/000000/sun.png" alt="Sun Icon">';
            } else {
                themeToggle.innerHTML = '<img src="https://img.icons8.com/ios-filled/50/000000/moon-symbol.png" alt="Moon Icon">';
            }
        });

        settingsButton.addEventListener('click', function() {
            settingsModal.style.display = 'block';
        });

        closeModal.addEventListener('click', function() {
            settingsModal.style.opacity = '0';
            setTimeout(() => {
                settingsModal.style.display = 'none';
                settingsModal.style.opacity = '1';
            }, 200);
        });

        giftButton.addEventListener('click', function() {
            giftModal.style.display = 'block';
        });

        closeGiftModal.addEventListener('click', function() {
            giftModal.style.opacity = '0';
            setTimeout(() => {
                giftModal.style.display = 'none';
                giftModal.style.opacity = '1';
            }, 200);
        });

        floatingButton.addEventListener('click', function() {
            dropdownButtons.classList.toggle('show');
            floatingButton.classList.toggle('clicked');
        });

        userInfoButton.addEventListener('click', function() {
            userInfoModal.style.display = 'block';
        });

        closeUserInfoModal.addEventListener('click', function() {
            userInfoModal.style.opacity = '0';
            setTimeout(() => {
                userInfoModal.style.display = 'none';
                userInfoModal.style.opacity = '1';
            }, 200);
        });

        rainbowButton.addEventListener('click', function() {
            colorPickerModal.style.display = 'block';
        });

        confirmColorButton.addEventListener('click', function() {
            const selectedColor = getComputedStyle(colorPicker).backgroundColor;
            body.style.background = selectedColor;
            colorPickerModal.style.opacity = '0';
            setTimeout(() => {
                colorPickerModal.style.display = 'none';
                colorPickerModal.style.opacity = '1';
            }, 200);
        });

        cancelColorButton.addEventListener('click', function() {
            colorPickerModal.style.opacity = '0';
            setTimeout(() => {
                colorPickerModal.style.display = 'none';
                colorPickerModal.style.opacity = '1';
            }, 200);
        });

        toggleSoundButton.addEventListener('click', function() {
            if (backgroundMusic.muted) {
                backgroundMusic.muted = false;
                toggleSoundButton.textContent = 'Отключить звук';
            } else {
                backgroundMusic.muted = true;
                toggleSoundButton.textContent = 'Включить звук';
            }
        });

        function createEmoji(emoji) {
            const emojiElement = document.createElement('div');
            emojiElement.classList.add('emoji');
            emojiElement.textContent = emoji;
            emojiElement.style.left = Math.random() * 100 + 'vw';
            emojiElement.style.animationDuration = (Math.random() * 3 + 5) + 's';
            document.body.appendChild(emojiElement);

            setTimeout(() => {
                emojiElement.remove();
            }, 8000);
        }

        setInterval(() => {
            createEmoji('🔥');
            createEmoji('👌');
        }, 1000);

        // Adjust theme based on device theme
        const prefersDarkScheme = window.matchMedia("(prefers-color-scheme: dark)");
        if (prefersDarkScheme.matches) {
            body.classList.add('dark-theme');
            settingsModal.classList.add('dark-theme');
            giftModal.classList.add('dark-theme');
            userInfoModal.classList.add('dark-theme');
            colorPickerModal.classList.add('dark-theme');
            themeToggle.innerHTML = '<img src="https://img.icons8.com/ios-filled/50/000000/sun.png" alt="Sun Icon">';
        }
    </script>
</body>
</html>
