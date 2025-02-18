<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
    <title>Shop</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200;500&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html, body {
            overflow: hidden;
            height: 100%;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            font-weight: 200;
            color: #000;
            background: linear-gradient(to bottom, #ffffff, #000000);
            transition: background 0.5s, color 0.5s;
            user-select: none;
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
            background: conic-gradient(#ADD8E6 0deg 72deg, #B19CD9 72deg 144deg, #ADD8E6 144deg 216deg, #B19CD9 216deg 288deg, #ADD8E6 288deg 360deg);
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
        <h1>Productivity</h1>
        <img src="data:image/webp;base64,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" alt="Productivity">
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
            <div class="roulette-segment segment1"><img src="https://img.icons8.com/ios-filled/50/ffffff/airplane-take-off.png" alt="Приз 1"></div>
            <div class="roulette-segment segment2"><img src="https://img.icons8.com/ios-filled/50/ffffff/telegram-app.png" alt="Приз 2"></div>
            <div class="roulette-segment segment3"><img src="https://img.icons8.com/ios-filled/50/ffffff/rocket.png" alt="Приз 3"></div>
            <div class="roulette-segment segment4"><img src="https://img.icons8.com/ios-filled/50/ffffff/airplane-take-off.png" alt="Приз 4"></div>
            <div class="roulette-segment segment5"><img src="https://img.icons8.com/ios-filled/50/ffffff/sim-card-chip.png" alt="Приз 5"></div>
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

        document.addEventListener('copy', function(e) {
            e.preventDefault();
            alert('Копирование запрещено на этой странице.');
        });

        document.addEventListener('contextmenu', function(e) {
            e.preventDefault();
            alert('Контекстное меню запрещено на этой странице.');
        });

        Telegram.WebApp.expand();
    </script>
</body>
</html>
