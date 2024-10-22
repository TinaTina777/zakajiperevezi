<html lang="ru">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Заявка на перевозку</title>
    <style>
        /* Основные стили, как ранее */
        * {
            -webkit-user-select: none;
            user-select: none;
            box-sizing: border-box;
        }
        body {
            margin: 0;
            color: black;
            background-color: #f4f4f9;
            display: flex;
            flex-direction: column;
            align-items: center;
            font-family: Arial, sans-serif;
        }
        main {
            max-width: 600px;
            padding: 20px;
            margin: 20px;
            background: white;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        label {
            font-weight: bold;
            margin-bottom: 5px;
            display: block;
        }
        input, textarea {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #45a049;
        }
        .output {
            margin-top: 20px;
            padding: 20px;
            background-color: #eaeaea;
            border-radius: 8px;
            width: 100%;
        }
    </style>
</head>
<body>
<main>
    <h2>Форма заявки на перевозку</h2>
    <label for="cargo">Укажите, пожалуйста, наименование перевозимого груза:</label>
    <input type="text" id="cargo" placeholder="Груз" />

    <label for="dimensions">Укажите, пожалуйста, габариты (ВВ*ШШ*ДД) в метрах:</label>
    <input type="text" id="dimensions" placeholder="Например, 2*2,5*3" />

    <label for="fromAddress">Укажите, пожалуйста, адрес отправки:</label>
    <input type="text" id="fromAddress" placeholder="Город, Улица, Дом" />

    <label for="toAddress">Укажите, пожалуйста, адрес доставки:</label>
    <input type="text" id="toAddress" placeholder="Город, Улица, Дом" />

    <label for="sendDate">Укажите, пожалуйста, дату отправки:</label>
    <input type="date" id="sendDate" />

    <label for="telegram">Укажите, пожалуйста, никнейм в Телеграм (без "@"):</label>
    <input type="text" id="telegram" placeholder="username" />

    <label for="phone">Укажите, пожалуйста, телефон для связи:</label>
    <input type="tel" id="phone" placeholder="8 999 999 9999" />

    <button onclick="submitForm()">Сформировать заявку</button>

    <div class="output" id="output"></div>
</main>

<script>
// Генерация уникального номера заявки
function generateRequestNumber() {
    return Math.floor(Math.random() * (9999 - 343 + 1)) + 343;
}

// Проверка номера телефона и приведение к стандарту с 7
function formatPhoneNumber(phone) {
    let cleaned = phone.replace(/\D/g, '');
    if (cleaned.startsWith('8')) {
        cleaned = '7' + cleaned.slice(1);
    } else if (cleaned.startsWith('7')) {
        return '+' + cleaned;
    }
    return '+7' + cleaned;
}

function submitForm() {
    const cargo = document.getElementById('cargo').value;
    const dimensions = document.getElementById('dimensions').value;
    const fromAddress = document.getElementById('fromAddress').value;
    const toAddress = document.getElementById('toAddress').value;
    const sendDate = document.getElementById('sendDate').value;
    const telegram = document.getElementById('telegram').value;
    const phone = formatPhoneNumber(document.getElementById('phone').value);

    // Формат даты в формате DD.MM.YYYY
    const formattedSendDate = new Date(sendDate).toLocaleDateString('ru-RU');

    const requestNumber = generateRequestNumber();

    const yandexMapLink = `https://yandex.ru/maps/?rtext=${encodeURIComponent(fromAddress)}~${encodeURIComponent(toAddress)}&rtt=auto`;

    const output = `
        <p><strong>📝Номер заявки:</strong> ${requestNumber}</p>
        <p><strong>✅ Наименование:</strong> ${cargo}</p>
        <p><strong>📦 Габариты:</strong> ${dimensions} м</p>
        <p><strong>🏚️ Адрес отправления:</strong> ${fromAddress}</p>
        <p><strong>🏠 Адрес доставки:</strong> ${toAddress}</p>
        <p><strong>📅 Дата отправки:</strong> ${formattedSendDate}</p>
        <p><strong>⛟ <a href="${yandexMapLink}" target="_blank">Маршрут в Яндекс.Картах</a></strong></p>
        <p><strong>➤ Предложения по цене присылать:</strong> <a href="https://t.me/${telegram}" target="_blank">https://t.me/${telegram}</a></p>
        <p><strong>📲 Телефон для связи:</strong> ${phone}</p>
    `;

    document.getElementById('output').innerHTML = output;

    // Отправка заявки в канал Telegram
    sendToTelegram(output, requestNumber, telegram, phone);
}

// Функция отправки заявки в канал Telegram
function sendToTelegram(output, requestNumber, telegram, phone) {
    const message = `
📝Номер заявки: ${requestNumber}
${output.replace(/<\/?[^>]+(>|$)/g, "")}

📰 Заявка направлена в канал в телеграмм Закажи. Перевези 🚚 (https://t.me/zaka_p)
➤ Перевозчики будут направлять свои предложения в телеграмм для t.me/${telegram}
📲 Телефон для связи ${phone}
    `;

    const token = '7440917653:AAHLtEKyOJWYHna-YJtMj9wzCeCAx8OZzgk';
    const chatId = '@zaka_p';
    const url = `https://api.telegram.org/bot${token}/sendMessage`;

    fetch(url, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify({
            chat_id: chatId,
            text: message,
            parse_mode: 'HTML',
        }),
    })
        .then(response => response.json())
        .then(data => {
            if (data.ok) {
                document.getElementById('output').innerHTML += `
                    <p>📰 Заявка направлена в канал в телеграмм <a href="https://t.me/zaka_p" target="_blank">Закажи. Перевези 🚚</a></p>
                    <button onclick="location.reload()">Создание новой заявки</button>
                    <button onclick="window.open('https://t.me/zaka_p', '_blank')">Перейти на канал в телеграм "Закажи. Перевези 🚚"</button>
                `;
            }
        });
}
</script>
</body>
</html>
