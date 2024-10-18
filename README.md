# zakajiperevezi
для бота закажи перевези
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Форма</title>
</head>
<body>
    <form action="" method="post">
        <label for="name">Наименование:</label><br>
        <input type="text" id="name" name="name"><br>
        <label for="weight">Вес:</label><br>
        <input type="number" id="weight" name="weight"><br>
        <label for="length">Длина:</label><br>
        <input type="number" id="length" name="length"><br>
        <label for="width">Ширина:</label><br>
        <input type="number" id="width" name="width"><br>
        <label for="depth">Глубина:</label><br>
        <input type="number" id="depth" name="depth"><br>
        <button type="submit">Отправить</button>
    </form>
</body>
</html>
<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $name = $_POST['name'];
    $weight = $_POST['weight'];
    $length = $_POST['length'];
    $width = $_POST['width'];
    $depth = $_POST['depth'];
    
    // Здесь обрабатываем данные
    echo "Наименование: $name<br>";
    echo "Вес: $weight<br>";
    echo "Габариты: $length x $width x $depth<br>";
} else {
    echo "Ошибка при отправке данных.";
}
?>
