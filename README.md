# zakajiperevezi
для бота закажи перевези
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

      <label for="telegram">Укажите, пожалуйста, никнейм в Телеграм:</label>
      <input type="text" id="telegram" placeholder="@username" />

      <label for="desiredDate">Введите, пожалуйста, желаемую дату:</label>
      <input type="date" id="desiredDate" />

      <label for="phone">Укажите, пожалуйста, телефон для связи:</label>
      <input type="tel" id="phone" placeholder="+7 999 999 9999" />

      <button onclick="submitForm()">Проверьте, пожалуйста, всё указано корректно?</button>

      <div class="output" id="output"></div>
    </main>

    <script>
      function submitForm() {
        const cargo = document.getElementById('cargo').value;
        const dimensions = document.getElementById('dimensions').value;
        const fromAddress = document.getElementById('fromAddress').value;
        const toAddress = document.getElementById('toAddress').value;
        const sendDate = document.getElementById('sendDate').value;
        const telegram = document.getElementById('telegram').value;
        const desiredDate = document.getElementById('desiredDate').value;
        const phone = document.getElementById('phone').value;

        const output = `
          <p><strong>Наименование груза:</strong> ${cargo}</p>
          <p><strong>Габариты:</strong> ${dimensions}</p>
          <p><strong>Адрес отправки:</strong> ${fromAddress}</p>
          <p><strong>Адрес доставки:</strong> ${toAddress}</p>
          <p><strong>Дата отправки:</strong> ${sendDate}</p>
          <p><strong>Никнейм в Телеграм:</strong> ${telegram}</p>
          <p><strong>Желаемая дата:</strong> ${desiredDate}</p>
          <p><strong>Телефон:</strong> ${phone}</p>
        `;

        document.getElementById('output').innerHTML = output;
      }
    </script>
  </body>
</html>


///
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

<!-- Begin Jekyll SEO tag v2.8.0 -->
<title>zakajiperevezi | для бота закажи перевези</title>
<meta name="generator" content="Jekyll v3.10.0" />
<meta property="og:title" content="zakajiperevezi" />
<meta property="og:locale" content="en_US" />
<meta name="description" content="для бота закажи перевези" />
<meta property="og:description" content="для бота закажи перевези" />
<link rel="canonical" href="https://tinatina777.github.io/zakajiperevezi/" />
<meta property="og:url" content="https://tinatina777.github.io/zakajiperevezi/" />
<meta property="og:site_name" content="zakajiperevezi" />
<meta property="og:type" content="website" />
<meta name="twitter:card" content="summary" />
<meta property="twitter:title" content="zakajiperevezi" />
<script type="application/ld+json">
{"@context":"https://schema.org","@type":"WebSite","description":"для бота закажи перевези","headline":"zakajiperevezi","name":"zakajiperevezi","url":"https://tinatina777.github.io/zakajiperevezi/"}</script>
<!-- End Jekyll SEO tag -->

    <link rel="stylesheet" href="/zakajiperevezi/assets/css/style.css?v=69b752e7bc8313dd746969e9bad35d631f5020c1">
    <!-- start custom head snippets, customize with your own _includes/head-custom.html file -->

<!-- Setup Google Analytics -->



<!-- You can set your favicon here -->
<!-- link rel="shortcut icon" type="image/x-icon" href="/zakajiperevezi/favicon.ico" -->

<!-- end custom head snippets -->

  </head>
  <body>
    <div class="container-lg px-3 my-5 markdown-body">
      

      <h1 id="zakajiperevezi">zakajiperevezi</h1>
<p>для бота закажи перевези
&lt;!DOCTYPE html&gt;</p>
<html lang="ru">
<head>
    <meta charset="UTF-8" />
    <title>Форма</title>
</head>
<body>
    <form action="" method="post">
        <label for="name">Наименование:</label><br />
        <input type="text" id="name" name="name" /><br />
        <label for="weight">Вес:</label><br />
        <input type="number" id="weight" name="weight" /><br />
        <label for="length">Длина:</label><br />
        <input type="number" id="length" name="length" /><br />
        <label for="width">Ширина:</label><br />
        <input type="number" id="width" name="width" /><br />
        <label for="depth">Глубина:</label><br />
        <input type="number" id="depth" name="depth" /><br />
        <button type="submit">Отправить</button>
    </form>
</body>
</html>
<p>&lt;?php
if ($_SERVER[‘REQUEST_METHOD’] === ‘POST’) {
    $name = $_POST[‘name’];
    $weight = $_POST[‘weight’];
    $length = $_POST[‘length’];
    $width = $_POST[‘width’];
    $depth = $_POST[‘depth’];</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>// Здесь обрабатываем данные
echo "Наименование: $name&lt;br&gt;";
echo "Вес: $weight&lt;br&gt;";
echo "Габариты: $length x $width x $depth&lt;br&gt;"; } else {
echo "Ошибка при отправке данных."; } ?&gt;
</code></pre></div></div>


      
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/anchor-js/4.1.0/anchor.min.js" integrity="sha256-lZaRhKri35AyJSypXXs4o6OPFTbTmUoltBbDCbdzegg=" crossorigin="anonymous"></script>
    <script>anchors.add();</script>
  </body>
</html>

