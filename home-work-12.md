> [!NOTE]  
> - Для всех БД сделать healthcheck и volumes для данных БД
> - Для всех сервисов прописать зависимость от "здоровья" БД
> - Для всех сервисов убрать публикацию портов и сделать их доступными только через прокси

1) С помощью docker compose запустить drupal
2) С помощью docker compose запустить joomla
3) С помощью docker compose запустить redmine
4) С помощью docker compose запустить mediawiki
