# Часть 1: Скрипты
1) Написать скрипт, который будет проверять состояние nginx, php-fpm и mysql, перезапускать их, если они остановлены и записывать в файл /var/log/lemp.log запись об этом
2) Написать скрипт, который для поиска свободных портов из диапазона 8000-8999
3) Написать скрипт для сбора статистики о процессах:
- об использовании cpu
- об использовании памяти
- выводить парамтеры pid, user, command и cpu/mem
- результат должен записываться в файл /var/log/process_stat.log в формате
```
==> Process stats at 2024-24-10_12-11-35 <==
--------------------------------------------
==> CPU usage <==
%CPU     PID USER     COMMAND
15.8     517 jenkins  /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080
 3.8       1 root     /sbin/init
 1.6     554 root     /sbin/agetty -o -p -- \u --keep-baud 115200,57600,38400,9600 ttyS0 vt220
 0.9     270 root     /lib/systemd/systemd-udevd
==> MEM usage <==
SIZE     PID USER     COMMAND
797876    517 jenkins  /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080
26044     431 root     /sbin/dhclient -4 -v -i -pf /run/dhclient.eth0.pid -lf /var/lib/dhcp/dhclient.eth0.leases -I -df /var/lib/dhcp/dhclient6.eth0.leases eth0
26044     458 root     /sbin/dhclient -4 -v -i -pf /run/dhclient.eth0.pid -lf /var/lib/dhcp/dhclient.eth0.leases -I -df /var/lib/dhcp/dhclient6.eth0.leases eth0
18636     519 root     /usr/sbin/rsyslogd -n -iNONE
```
- выводить только первые 5 процессов в списке, отсортированных по нужному параметру
# Часть 2: Раскатка приложений
Запустить приложение https://github.com/AnastasiyaGapochkina01/kostantin235/tree/main/php-app по аналогии с тем, что делали на занятии
