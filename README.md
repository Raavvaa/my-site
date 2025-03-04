<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Do you wanna go out with me?</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #ffe5ec; /* Светло-розовый фон */
            font-family: Arial, sans-serif;
            position: relative;
            overflow: hidden; /* Чтобы кнопки не выходили за пределы экрана */
        }
        .card {
            background-color: #fff0f5; /* Более светлый розовый фон для карточки */
            padding: 20px;
            border-radius: 15px;
            border: 5px solid #ff69b4; /* Розовая рамка */
            text-align: center;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            position: relative;
            z-index: 1; /* Чтобы карточка оставалась над кнопками */
        }
        .header-text {
            font-family: 'Indie Flower', cursive; /* Шрифт, как в примере */
            font-size: 50px;
            font-weight: bold;
            color: #ff6b81; /* Розовый цвет текста */
            margin-bottom: 20px;
        }
        .cat {
            font-size: 200px; /* Размер эмодзи кошки */
            cursor: pointer; /* Указатель руки при наведении */
            transition: transform 0.3s; /* Плавная анимация */
        }
        .cat:hover {
            transform: scale(1.1); /* Немного увеличиваем кошку при наведении */
        }
        .buttons {
            margin-top: 20px;
            position: relative; /* Для позиционирования кнопок */
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            margin: 0 10px;
            transition: transform 0.3s, left 0.5s, top 0.5s; /* Плавное перемещение */
            position: absolute; /* Для анимации движения кнопки "No" */
        }
        .no-button {
            background-color: #ff4d4d; /* Красный цвет для "No" */
            color: white;
            left: 0; /* Изначальное положение кнопки "No" */
        }
        .yes-button {
            background-color: #ff69b4; /* Розовый цвет для "Yes" */
            color: white;
            position: static; /* Кнопка "Yes" остаётся на месте */
        }
        button:hover {
            transform: scale(1.1); /* Легкое увеличение при наведении */
        }
        .hearts {
            font-size: 20px;
            color: #ff4d4d; /* Красный цвет для сердечек */
        }
        .message {
            margin-top: 20px;
            font-size: 24px;
            color: #4CAF50; /* Зеленый цвет для сообщения */
            display: none; /* Скрыто по умолчанию */
        }
    </style>
</head>
<body>
    <div class="card">
        <h1 class="header-text">Do you wanna go out with me?</h1>
        <div class="hearts">❤️❤️❤️</div>
        <span class="cat" id="cat">🐱</span>
        <div class="buttons">
            <button class="no-button" id="noButton">No</button>
            <button class="yes-button" id="yesButton">Yes</button>
        </div>
        <div class="message" id="loveMessage">Вы реально любите Равиля</div>
    </div>

    <!-- Подключение библиотеки canvas-confetti для эффекта конфетти -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.2/dist/confetti.browser.min.js"></script>
    <script>
        const noButton = document.getElementById('noButton');
        const yesButton = document.getElementById('yesButton');
        const loveMessage = document.getElementById('loveMessage');
        const cat = document.getElementById('cat');

        // Изначальное положение кнопки "No" относительно контейнера .buttons
        const initialNoPosition = {
            left: 0,
            top: 0
        };

        // Функция для перемещения кнопки "No" на небольшое расстояние
        function moveNoButton() {
            const maxOffset = 200; // Максимальное расстояние улетания (можно настроить)
            const randomX = (Math.random() - 0.5) * maxOffset; // Случайное смещение по X
            const randomY = (Math.random() - 0.5) * maxOffset; // Случайное смещение по Y
            noButton.style.left = (initialNoPosition.left + randomX) + 'px';
            noButton.style.top = (initialNoPosition.top + randomY) + 'px';

            // Возвращаем кнопку на место через 1 секунду
            setTimeout(() => {
                noButton.style.left = initialNoPosition.left + 'px';
                noButton.style.top = initialNoPosition.top + 'px';
            }, 1000); // Время анимации (1 секунда)
        }

        // Обработчик для кнопки "No"
        noButton.addEventListener('click', function(e) {
            e.preventDefault(); // Предотвращаем стандартное поведение
            moveNoButton(); // Перемещаем кнопку на небольшое расстояние и возвращаем
        });

        // Обработчик для кнопки "Yes"
        yesButton.addEventListener('click', function() {
            // Эффект конфетти
            confetti({
                particleCount: 100,
                spread: 70,
                origin: { y: 0.6 }
            });
            loveMessage.style.display = 'block'; // Показываем сообщение
            noButton.style.display = 'none'; // Скрываем кнопку "No"
            yesButton.style.display = 'none'; // Скрываем кнопку "Yes"
            cat.style.display = 'none'; // Скрываем кошку
        });
    </script>
</body>
