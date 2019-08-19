# OTUS ДЗ 4 Работа с Bash, AWK, SED и другими консольными утилитами (Centos 7)
-----------------------------------------------------------------------
### Домашнее задание

### Работа с Bash, AWK, SED и другими консольными утилитами

Пишем скрипт

Цель: В результате этого ДЗ вы научитесь писать простые скрипты, решающие нужны задачи, такие как мониторинг кол-ва 

ошибок в логах Освоите работу с файлами, поиском, парсингом текста, управлением блокировками

написать скрипт для крона

который раз в час присылает на заданную почту:
- X IP адресов (с наибольшим кол-вом запросов) с указанием кол-ва запросов c момента последнего запуска скрипта

- Y запрашиваемых адресов (с наибольшим кол-вом запросов) с указанием кол-ва запросов c момента последнего запуска скрипта

- все ошибки c момента последнего запуска

- список всех кодов возврата с указанием их кол-ва с момента последнего запуска

в письме должно быть прописан обрабатываемый временной диапазон

должна быть реализована защита от мультизапуска
Критерии оценки: 
трапы и функции, а также sed и find +1 балл

### Как запускать (предусмотрена защита от мультизапуска)

В качестве защиты от мультизапуска используется программа flock

1. Добавить в cron скрипт (crontab -e), в виде `/usr/bin/flock /var/tmp/myscript.lock /root/myscript.sh` с указанием расписания
2. Если так произойдет, что скрипт не успеет отработать в отведенное ему время, повторный запуск скрипта не произойдет, а точнее, произойдет запуск программы flock, она будет ждать пока что первый скрипт завершит свою работу и только после этого запустит скрипт.
3. `/var/tmp/myscript.lock` это лок файл, который создается если его нет, и программа flock "держит" его во время выполнения скрипта и отпускает только после того как скрипт завершится.

### Файлы

1. [check_log.sh] - скрипт, который парсит файл логов NGINX
2. [access-4560-644067.log] - сам файл логов
3. [lines] - файл куда записывается последняя доступная строка (при следующем запуске, лог будет парситься со следующей строки, указанной в файле, т.е. 670+1). Если ничего в этом файле не будет то лог будет парситься сначала и до конца.
4. [mail_result.txt] - Результат, который приходит на почту



[check_log.sh]:https://github.com/staybox/otus_dz4/blob/master/check_log.sh
[access-4560-644067.log]:https://github.com/staybox/otus_dz4/blob/master/access-4560-644067.log
[lines]:https://github.com/staybox/otus_dz4/blob/master/lines
[mail_result.txt]:https://github.com/staybox/otus_dz4/blob/master/mail_result.txt