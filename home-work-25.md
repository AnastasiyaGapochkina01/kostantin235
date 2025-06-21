# Часть 1
1) Запустить minikube на ВМ по инструкции https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download (уже должен быть устанволен docker) и kubectl https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-binary-with-curl-on-linux
2) Создать Pod с веб-сервером Nginx
- с помощью команды kubectl
- с помощью манифеста\
после запуска пода посмотреть информацию о нем; сделать запрос на запущенный nginx и посмотреть логи пода
3) Создать Service для доступа к Pod с помощью манифеста; посмотреть информацию о созданном сервисе
4) Проверить доступность приложения через Service

# Часть 2
Развернуть мини-приложение на python в k8s:
```python
from flask import Flask
import sys
import os

app = Flask(__name__)

@app.route('/')
def index():
    python_version = sys.version
    current_directory = os.getcwd()
    return f"Версия Python: {python_version}\nТекущая директория: {current_directory}"

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
```
1) собрать для него docker image
2) запушить этот image в docker hub
3) создать pod и service для запуска приложения в k8s; проверить работоспособность приложения - при запросе curl`ом должно отдаваться что-то похожее на
```
Версия Python: 3.9.2 (default, Mar 20 2025, 02:07:39)
[GCC 10.2.1 20210110]
Текущая директория: /home/anestesia/python
```
