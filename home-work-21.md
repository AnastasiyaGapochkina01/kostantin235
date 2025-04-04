1) Создать репозиторий с названием multi-lang-projects. В корне репозитория создать папки
- php
- ruby
- go

В директории php создать файл index.php с содержимым
```
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Простой калькулятор</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        form {
            width: 300px;
            margin: auto;
            padding: 20px;
            background-color: #f0f0f0;
            border: 1px solid #ddd;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        label {
            display: block;
            margin-bottom: 10px;
        }
        input[type="number"] {
            width: 100%;
            height: 30px;
            margin-bottom: 20px;
            padding: 10px;
            box-sizing: border-box;
        }
        select {
            width: 100%;
            height: 30px;
            margin-bottom: 20px;
            padding: 10px;
            box-sizing: border-box;
        }
        button[type="submit"] {
            width: 100%;
            height: 40px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button[type="submit"]:hover {
            background-color: #0056b3;
        }
        .result {
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>

<form action="" method="post">
    <label for="num1">Первое число:</label>
    <input type="number" id="num1" name="num1" required>

    <label for="operation">Операция:</label>
    <select id="operation" name="operation">
        <option value="+">Сложение</option>
        <option value="-">Вычитание</option>
        <option value="*">Умножение</option>
        <option value="/">Деление</option>
    </select>

    <label for="num2">Второе число:</label>
    <input type="number" id="num2" name="num2" required>

    <button type="submit">Вычислить</button>
</form>

<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $num1 = (float)$_POST['num1'];
    $operation = $_POST['operation'];
    $num2 = (float)$_POST['num2'];

    switch ($operation) {
        case '+':
            $result = $num1 + $num2;
            break;
        case '-':
            $result = $num1 - $num2;
            break;
        case '*':
            $result = $num1 * $num2;
            break;
        case '/':
            if ($num2 !== 0) {
                $result = $num1 / $num2;
            } else {
                $result = 'Ошибка: деление на ноль!';
            }
            break;
        default:
            $result = 'Неправильная операция';
            break;
    }

    echo '<div class="result">';
    if (is_string($result)) {
        echo $result;
    } else {
        echo "Результат: $num1 $operation $num2 = $result";
    }
    echo '</div>';
}
?>

</body>
</html>
```
2) Написать dockerfile для запуска кода из п1 в docker (за основу можно взять php:8.1-apache)
3) Написать пайплайн, который будет 
- прогонять линтер для
  - php кода
  - Dockerfile
- собирать и пушить docker image
4) В директории ruby создать файлы\
app.rb
```
require 'webrick'

class App
  def call(env)
    [200, {'Content-Type' => 'text/plain'}, ['Hello, world!']]
  end
end


server = WEBrick::HTTPServer.new(:Port => 3000)

server.mount_proc '/' do |req, res|
  res.status = 200
  res['Content-Type'] = 'text/plain'
  res.body = "Hello, world!"
end

trap "INT" do
  server.shutdown
end

server.start

```
Gemfile
```
source 'https://rubygems.org'

gem 'rails', '~> 7.0'
gem 'puma'
gem 'webrick'

```
config.ru
```
require './app'

Rack::Server.new(
  app: App.new,
  server: 'puma',
  Host: '0.0.0.0',
  Port: 3000
).start

```
5) написать dockerfile для запуска кода из п4 в docker
6) Написать пайплайн, который будет 
- прогонять линтер для
  - ruby кода
  - Dockerfile
- собирать и пушить docker image
