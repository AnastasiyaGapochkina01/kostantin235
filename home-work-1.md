1) Добавить к ВМ дополнительный диск
2) Создать директорию /opt/psql/data
3) Смонтировать новый диск в диреткорию /opt/psql/data так, чтобы после ребута монтирование не отваливалось
4) В директории /opt/psql/data создать следующую структуру каталогов и файлов

<img width="567" alt="image" src="https://github.com/user-attachments/assets/6db04843-675c-4142-b85f-5ca80f8e65fa">

5) В директории /opt/psql/data создать папку library_archive
6) Скопировать содержимое директории library в library_archive
7) Перейти в library_archive и сделать копию папки authors с новым именем authors_bk
8) В директории /opt/psql/data создать директорию backups
9) Переместить в backups authors_bk
10) Удалить директорию library_archive
