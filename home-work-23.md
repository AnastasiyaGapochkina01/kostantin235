Дан код на python\
app.py
```
import http.server
import socket
import os
import getpass

# Получаем имя пользователя
username = getpass.getuser()

# Получаем версию ОС
os_version = f"{os.sys.platform} {os.sys.version}"

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.connect(("8.8.8.8", 80))
local_ip = s.getsockname()[0]
s.close()

greeting = f"Привет, {username}!"

class RequestHandler(http.server.BaseHTTPRequestHandler):
    def do_GET(self):
        if self.path != "/":
            self.send_response(404)
            self.send_header("Content-type", "text/plain")
            self.end_headers()
            self.wfile.write(b"404 Not Found")
            return

        self.send_response(200)
        self.send_header("Content-type", "text/plain")
        self.end_headers()

        response = f"Версия ОС: {os_version}\nПриветствие: {greeting}\nЛокальный IP: {local_ip}"
        self.wfile.write(response.encode())

def run_server():
    server_address = ('', 3000)
    httpd = http.server.HTTPServer(server_address, RequestHandler)
    print("Сервер запущен на порту 3000")
    httpd.serve_forever()

if __name__ == "__main__":
    run_server()
```
Необходимо
1) упаковать его в docker
2) написать пайплайн который
- соберет docker image
- запушит его в docker hub
- задеплоит собранный image по ssh на удаленный хост
- соберет из кода app.py исполняемый файл - это делается с помощью библиотеки pyinstaller: ```pyinstaller --onefile app.py``` (соответственно перед выполнением сборки надо установить pyinstaller) и сохранит его в артефактах
