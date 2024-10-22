<!DOCTYPE html>
<html lang="ru">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"
    />
    <title>Заявка на перевозку</title>
    <style>
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
        width: 100%;
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
      input,
      textarea {
        width: 100%;
        padding: 10px;
        margin-bottom: 20px;
        border: 1px solid #ccc;
        border-radius: 5px;
        font-size: 16px;
      }
      button {
        background-color: #4caf50;
        color: white;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        font-size: 16px;
        width: 100%;
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

      /* Стиль для проверки валидности */
      .valid {
        color: green;
        font-weight: bold;
      }

      .invalid {
        color: red;
        font-weight: bold;
      }

      /* Адаптивность */
      @media (max-width: 600px) {
        body {
          padding: 10px;
        }
        main {
          margin: 10px;
          padding: 15px;
        }
        button {
          font-size: 14px;
        }
      }

      @media (min-width: 601px) {
        main {
          margin: 40px auto;
        }
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
      <div id="fromAddressValidation" class="invalid"></div>

      <label for="toAddress">Укажите, пожалуйста, адрес доставки:</label>
      <input type="text" id="toAddress" placeholder="Город, Улица, Дом" />
      <div id="toAddressValidation" class="invalid"></div>

      <label for="sendDate">Укажите, пожалуйста, дату отправки:</label>
      <input type="date" id="sendDate" />

      <label for="telegram">Укажите, пожалуйста, никнейм в Телеграм:</label>
      <input type="text" id="telegram" placeholder="username" />
      <div id="telegramValidation" class="invalid"></div>

      <label for="phone">Укажите, пожалуйста, телефон для связи:</label>
      <input type="tel" id="phone" placeholder="+7 999 999 9999 или 8 999 999 9999" />
      <div id="phoneValidation" class="invalid"></div>

      <button onclick="submitForm()">Сформировать заявку</button>

      <div class="output" id="output"></div>
      <button onclick="sendToTelegram()">Отправить</button>
    </main>

    <script>
      const token = 'ab83f3d5c9fdc990f8b067ba9c70220d2a52d01d'; // API-ключ DaData
      const telegramBotToken = '7440917653:AAHLtEKyOJWYHna-YJtMj9wzCeCAx8OZzgk'; // API-ключ Telegram бота
      const telegramChatId = '@zaka_p'; // ID канала Telegram для отправки

      // Генерация уникального номера заявки
      function generateOrderNumber() {
        return Math.floor(Math.random() * (9999 - 343 + 1)) + 343;
      }

      async function validateAddress(address, validationElementId) {
        const url = 'https://suggestions.dadata.ru/suggestions/api/4_1/rs/suggest/address';
        const response = await fetch(url, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': `Token ${token}`,
          },
          body: JSON.stringify({
            query: address,
            count: 1,
          }),
        });

        const data = await response.json();
        const validationElement = document.getElementById(validationElementId);

        if (data.suggestions.length > 0) {
          validationElement.textContent = 'Адрес корректен';
          validationElement.classList.remove('invalid');
          validationElement.classList.add('valid');
          return data.suggestions[0].value;
        } else {
          validationElement.textContent = 'Введите, пожалуйста, существующий адрес';
          validationElement.classList.remove('valid');
          validationElement.classList.add('invalid');
          return null;
        }
      }

      function validateTelegram(nick) {
        const validationElement = document.getElementById('telegramValidation');
        if (nick) {
          validationElement.textContent = 'Никнейм корректен';
          validationElement.classList.remove('invalid');
          validationElement.classList.add('valid');
          return true;
        } else {
          validationElement.textContent = 'Введите корректный никнейм';
          validationElement.classList.remove('valid');
          validationElement.classList.add('invalid');
          return false;
        }
      }

      function validatePhone(phone) {
        const validationElement = document.getElementById('phoneValidation');
        const phonePattern = /^(\+7|8)\s?\d{3}\s?\d{3}\s?\d{2}\s?\d{2}$/;
        if (phonePattern.test(phone)) {
          validationElement.textContent = 'Телефон корректен';
          validationElement.classList.remove('invalid');
          validationElement.classList.add('valid');
          return phone.replace(/^8/, '7').replace(/^\+7/, '7').replace(/\s/g, '');
        } else {
          validationElement.textContent = 'Введите корректный номер телефона (+7 или 8)';
          validationElement.classList.remove('valid');
          validationElement.classList.add('invalid');
          return null;
        }
      }

      async function submitForm() {
        const cargo = document.getElementById('cargo').value;
        const dimensions = document.getElementById('dimensions').value;
        const fromAddress = document.getElementById('fromAddress').value;
        const toAddress = document.getElementById('toAddress').value;
        const sendDateInput = document.getElementById('sendDate').value;
        const telegram = document.getElementById('telegram').value;
        const phone = document.getElementById('phone').value;

        const validFromAddress = await validateAddress(fromAddress, 'fromAddressValidation');
        const validToAddress = await validateAddress(toAddress, 'toAddressValidation');
        const validTelegram = validateTelegram(telegram);
        const validPhone = validatePhone(phone);

        if (validFromAddress && validToAddress && validTelegram && validPhone) {
          // Форматируем дату в формате DD.MM.YYYY
          const sendDate = new Date(sendDateInput);
          const formattedSendDate = `${String(sendDate.getDate()).padStart(2, '0')}.${String(sendDate.getMonth() + 1).padStart(2, '0')}.${sendDate.getFullYear()}`;

          const orderNumber = generateOrderNumber();
          const routeLink = `https://yandex.ru/maps/?rtext=${encodeURIComponent(validFromAddress)}~${encodeURIComponent(validToAddress)}`;
          const output = `
            <p><strong>Номер заявки:</strong> ${orderNumber}</p>
            ✅ <strong>Наименование:</strong> <strong>${cargo}</strong><br/>
            📦 <strong>Габариты:</strong> <strong>${dimensions}</strong><br/>
            🏚️ <strong>Адрес отправления:</strong> <strong>${validFromAddress}</strong><br/>
            🏠 <strong>Адрес доставки:</strong> <strong>${validToAddress}</strong><br/>
            📅 <strong>Дата отправки:</strong> <strong>${formattedSendDate}</strong><br/>
            ⛟ <strong>Маршрут в Яндекс.Картах:</strong> <a href="${routeLink}" target="_blank">Ссылка на маршрут</a><br/>
            ➤ <strong>Предложения по цене присылать:</strong> <a href="https://t.me/${telegram}">t.me/${telegram}</a><br/>
            📲 <strong>Телефон для связи:</strong> <strong>+7 ${validPhone}</strong><br/>
            
          `;

          document.getElementById('output').innerHTML = output;
        } else {
          alert('Пожалуйста, исправьте ошибки в форме');
        }
      }

      function sendToTelegram() {
        const message = document.getElementById('output').innerText;
        const url = `https://api.telegram.org/bot${telegramBotToken}/sendMessage`;

        fetch(url, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            chat_id: telegramChatId,
            text: message,
            parse_mode: 'HTML',
          }),
        })
          .then((response) => response.json())
          .then((data) => {
            if (data.ok) {
              alert('Заявка отправлена в Telegram');
            } else {
              alert('Ошибка отправки заявки');
            }
          });
      }
    </script>
  </body>
</html>
