<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
            transition: all 0.3s ease;
            color: #fff;
            background: #007bff;
        }

        .theme-toggle {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .theme-toggle img {
            width: 20px;
            height: 20px;
        }

        button:hover {
            background: #0056b3;
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

        #roulette {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 200px;
            height: 200px;
            border-radius: 50%;
            background: conic-gradient(#ff6347 0deg 72deg, #ffd700 72deg 144deg, #32cd32 144deg 216deg, #1e90ff 216deg 288deg, #8a2be2 288deg 360deg);
            position: relative;
            transition: transform 5s cubic-bezier(0.33, 1, 0.68, 1);
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

        .segment1 { transform: rotate(36deg); }
        .segment2 { transform: rotate(108deg); }
        .segment3 { transform: rotate(180deg); }
        .segment4 { transform: rotate(252deg); }
        .segment5 { transform: rotate(324deg); }

        .arrow {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 20px;
            height: 20px;
            background: #fff;
            clip-path: polygon(50% 0, 0 100%, 100% 100%);
            transform: translate(-50%, -100%);
            z-index: 1;
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
        <button id="about">О нас</button>
        <button id="toggle-sound">Отключить звук</button>
        <div class="modal-close" id="close-modal"></div>
    </div>

    <div id="gift-modal" class="modal">
        <div id="roulette">
            <div class="roulette-segment segment1">Приз 1</div>
            <div class="roulette-segment segment2">Приз 2</div>
            <div class="roulette-segment segment3">Приз 3</div>
            <div class="roulette-segment segment4">Приз 4</div>
            <div class="roulette-segment segment5">Приз 5</div>
            <div class="arrow"></div>
        </div>
        <button id="start-roulette">Крутить</button>
        <div class="modal-close" id="close-gift-modal"></div>
    </div>

    <div id="user-info-modal" class="modal">
        <div class="user-info-avatar" id="user-avatar" style="background-image: url('https://via.placeholder.com/80');"></div>
        <div class="user-info-nickname" id="user-nickname">Username</div>
        <div class="user-info-details">
            <p>Дата регистрации: <span id="registration-date">01.01.2020</span></p>
            <p>Количество рефералов: <span id="referrals-count">10</span></p>
        </div>
        <div class="modal-close" id="close-user-info-modal"></div>
    </div>

    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <script>
        Telegram.WebApp.ready();

        const themeToggle = document.getElementById('theme-button');
        const body = document.body;
        const settingsModal = document.getElementById('settings-modal');
        const closeModal = document.getElementById('close-modal');
        const floatingButton = document.getElementById('floating-button');
        const dropdownButtons = document.getElementById('dropdown-buttons');
        const giftButton = document.getElementById('gift-button');
        const giftModal = document.getElementById('gift-modal');
        const closeGiftModal = document.getElementById('close-gift-modal');
        const userInfoButton = document.getElementById('user-info-button');
        const userInfoModal = document.getElementById('user-info-modal');
        const closeUserInfoModal = document.getElementById('close-user-info-modal');
        const startRouletteButton = document.getElementById('start-roulette');
        const settingsButton = document.getElementById('settings-button');
        const roulette = document.getElementById('roulette');

        themeToggle.addEventListener('click', function() {
            body.classList.toggle('dark-theme');
            settingsModal.classList.toggle('dark-theme');
            giftModal.classList.toggle('dark-theme');
            userInfoModal.classList.toggle('dark-theme');
            if (body.classList.contains('dark-theme')) {
                themeToggle.innerHTML = '<img src="https://img.icons8.com/ios-filled/50/000000/sun.png" alt="Sun Icon">';
            } else {
                themeToggle.innerHTML = '<img src="https://img.icons8.com/ios-filled/50/000000/moon-symbol.png" alt="Moon Icon">';
            }
        });

        document.getElementById('buy').addEventListener('click', function() {
            Telegram.WebApp.close();
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

        closeModal.addEventListener('click', function() {
            settingsModal.style.opacity = '0';
            setTimeout(() => {
                settingsModal.style.display = 'none';
                settingsModal.style.opacity = '1';
            }, 200);
        });

        settingsButton.addEventListener('click', function() {
            settingsModal.style.display = 'block';
        });

        startRouletteButton.addEventListener('click', function() {
            const randomDegree = Math.floor(Math.random() * 360) + 360 * 3;
            roulette.style.transform = `rotate(${randomDegree}deg)`;
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
        }, 1000);

        const prefersDarkScheme = window.matchMedia("(prefers-color-scheme: dark)");
        if (prefersDarkScheme.matches) {
            body.classList.add('dark-theme');
            settingsModal.classList.add('dark-theme');
            giftModal.classList.add('dark-theme');
            userInfoModal.classList.add('dark-theme');
            themeToggle.innerHTML = '<img src="https://img.icons8.com/ios-filled/50/000000/sun.png" alt="Sun Icon">';
        }
    </script>
</body>
</html>
