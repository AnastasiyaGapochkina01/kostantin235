Дан проект "Hello World" на nodejs - https://github.com/AnastasiyaGapochkina01/hello-node/tree/main
Необходимо
1) Запустить его в docker
2) Написать gitlab ci пайплайн, который
- будет прогонять тесты командой ```npx mocha test/app.test.js```
- собирать и пушить в docker hub docker image приложения
- запускать из собранного image контейнер и делать запрос на порт 3000, после этого - удалять контейнер
