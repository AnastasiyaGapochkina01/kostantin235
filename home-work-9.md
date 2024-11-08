1) Установить docker на ВМ https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
2) Запустить контейнер с python, дать ему имя python-code
3) Выполнить команду python -V в контейнере python-code
4) Зайти в контейнер python-code, создать директорию /scripts, установить nano ```apt update && apt install -y nano```, написать и запустить скрипт

```
#!/usr/bin/python3
print("Hello")
```

выйти из контейнера

5) Остановить и удалить контейнер python-code
6) Запустить контейнер с redis, опубликовать порт 6379 на хост и проверить с помощью nc доступен ли он
7) Запустить контейнер с postgresql, прокинуть папку из контейнера /var/lib/postgresql/data на хост в папку /opt/psql-data
8) Зайти в контейнер с postgresql, создать БД application
9) Создать свой image python, в котором будет "зашит" скрипт из п4, запустить контейнер из этого image
