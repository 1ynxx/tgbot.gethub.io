<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
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
            color: var(--tg-theme-text-color);
            background: var(--tg-theme-bg-color);
        }

        #main {
            width: 100%;
            padding: 20px;
            text-align: center;
        }

        h1 {
            margin-top: 50px;
            margin-bottom: 10px;
        }

        img {
            width: 350px;
            margin: 30px auto;
        }

        p {
            width: 350px;
            margin: 0 auto;
        }

        button {
            border: 0;
            border-radius: 5px;
            margin-top: 50px;
            height: 60px;
            width: 200px;
            font-size: 20px;
            font-weight: 500;
            cursor: pointer;
            transition: all 500ms ease;
            color: var(--tg-theme-button-text-color);
        }

        button:hover {
            background: var(--tg-theme-secondary-bg-color);
        }
    </style>
</head>
<body>
    <div id="main">
        <h1>Онлайн магазин</h1>
        <img src="https://ru.freepik.com/free-vector/hand-drawn-pizza-slice-background_1175454.htm#query=%D0%BA%D1%83%D1%81%D0%BE%D0%BA%20%D0%BF%D0%B8%D1%86%D1%86%D1%8B&position=0&from_view=keyword&track=ais_user_b&uuid=aa60fef0-3779-4e83-8836-6cecfeaca37f" alt="Shop Image">
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
        <button id="buy">Купить</button>
    </div>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
</body>
</html>
