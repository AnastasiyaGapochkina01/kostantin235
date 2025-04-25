> [!TIP]
> Весь код должен быть организован на gitlab в два репозитория: проектный и инфраструктурный

Имеется проект https://github.com/AnastasiyaGapochkina01/bike-shop/tree/main \
Необходимо
1) Запустить инфраструктуру для этого приложения в YCloud с помощью terraform (характеристики можно взять минимальные):
- ВМ под само приложение
- ВМ под прокси
- ВМ под БД, к инстансу прикрепить дополнительный диск для данных БД
2) Подготовить запущенные ВМ с помощью ansible:
- на ВМ проекта должен быть установлен docker
- на ВМ прокси должен быть установлен nginx самой последней версии из репозитория https://nginx.org/en/linux_packages.html
- на ВМ БД должен быть установлен docker и смонтирован дополнительный диск в папку /opt/mongo_data
3) Запустить проект и БД в docker с помощью ansible (это разоврачивание с нуля):
- реплик проекта должно быть две (на одной ВМ), порты не вывешивать
- БД должна сохранять свои данные в /opt/mongo_data
- доступ к приложению должен осуществляться через proxy на третьей машине (nginx)
- секретные данные (такие как пароли/токены/сертификаты) должны использоваться в файлах .env и НЕ быть закоммичены в репозиторий

<img width="1064" alt="image" src="https://github.com/user-attachments/assets/f2264eba-bd7f-48cc-ba3f-17c5dba5ff16" />

4) Написать пайплайн GitlabCI, который будет осуществлять
- билд image для приложения
- пушить его в container registry gitlab
- деплоить приложение

Требования к пайплайну
- прогонять linter для кода, если были внесены изменения в файлы приложения
- прогонять linter для Dockerfile, если были изменения в нем
- при сборке image tag должен задаваться как bike-api-${VER}, где ${VER} - переменная CI_PIPELINE_ID
- билд тега должен производиться если были изменения в файлах приложения или в Dockerfile ИЛИ вручную
- деплой должен производиться только если был build и он был успешен
- если в сообщении к коммиту есть слово WIP, то пайплайн запускаться НЕ должен ни при каких условиях

5) Написать скрипт для резервного копирования БД в S3

6*) Добавить в пайплайн job для проверки
- отправка данных в приложение. Тестовые данные
```
[
  {
    "name": "Mountain Bike Pro",
    "price": 750,
    "description": "Durable bike for rough terrains"
  },
  {
    "name": "City Cruiser",
    "price": 350,
    "description": "Comfortable bike for urban commuting"
  },
  {
    "name": "Speed Racer",
    "price": 1200,
    "description": "Lightweight bike for high-speed performance"
  },
  {
    "name": "Trail Explorer",
    "price": 600,
    "description": "Perfect for off-road adventures"
  },
  {
    "name": "Electric Commuter",
    "price": 1500,
    "description": "Eco-friendly bike with electric assist"
  },
  {
    "name": "Kids Adventure Bike",
    "price": 200,
    "description": "Safe and fun bike for children"
  },
  {
    "name": "Folding Bike",
    "price": 450,
    "description": "Compact and portable for easy storage"
  },
  {
    "name": "Hybrid Bike",
    "price": 550,
    "description": "Versatile bike for city and light trails"
  },
  {
    "name": "BMX Stunt Bike",
    "price": 400,
    "description": "Built for tricks and stunts"
  },
  {
    "name": "Touring Bike",
    "price": 900,
    "description": "Designed for long-distance travel"
  }
]
```
- получения данных от приложения:
  - всех данных
  - данных по id
