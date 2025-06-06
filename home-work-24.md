1) Запустить приложение https://github.com/AnastasiyaGapochkina01/metric-prj-2/tree/main в docker
2) Написать для этого приложения CI/CD пайплайн, состоящий из следующих шагов
- сборка docker image
- отправка в docker hub собранного image
- деплой приложения
3) Развернуть с помощью docker compsoe сервер мониторинга, состоящий из
- prometheus
- grafana
4) Подключить у мониторингу наше приложение
