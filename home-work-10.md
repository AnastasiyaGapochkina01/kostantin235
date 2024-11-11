1) Запустить контейнер nginx:
- создать и прокинуть внутрь контейнера папку app (монтировать в /usr/share/nginx/html)
- в папке app создать файл index.html с таким содержимым
```
<Html>    
<Head>  
<title>  
Example of make a text B,I,U  
</title>  
</Head>  
<Body>   
<b> [This text is Bold......] </b>  
<I> [This text is Italic......] </I>  
<U> [This text is Underline......] </U>   
</Body>  
</Html> 
```
- вывесить порт 80 из контейнера на порт хоста 8090 
- при выполнении curl на ip:port должна отдаваться созданная страница
2) Запустить с помощью docker compose mongodb и mongo-express (https://hub.docker.com/_/mongo-express)
- mongo - нереляционная БД
- mongo-express - админка к ней
3) Запустить контейнер с postgres 9:
- задать переменную POSTGRES_PASSWORD со значением passwd
- создать директорию pg_data и прокинуть ее в контейнер по пути /var/lib/postgresql/data
4) Для всех контейнеров, запущенных в п1-3 выяснить с помощью [docker inspect](https://docs.docker.com/reference/cli/docker/inspect/):
- ip-адрес
- volumes
- image
5) Написать Dockerfile для nginx, в котором будет "зашит" файл index.html из задания №1
6) Запустить с помощью docker compose gitea (https://hub.docker.com/r/gitea/gitea) и postgres
7) Запустить с помощью docker compose portainer (https://hub.docker.com/r/portainer/portainer)
