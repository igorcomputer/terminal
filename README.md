## Команды консоли (терминал)

**Примечание:**    
>в консоли не работает команда вставки (CTRL+V),   
>необходимо пользоваться конекстным меню (правой кнопкой мыши - (вставить))

> `^C`  - прерывание текущей команды (CTRL+C)   
> `history` - просмотр истории команд, далее стрелками (вверх-вниз)
> `clear` — очистка консоли
> `man cd` - вызов справки для команды cd (для остальных команд аналогично)

##Подключение к сайту по SSH средствами Mac OS.  

Запускаем терминал и пишем:
> `ssh '-p 2200' root@178.154.84` — подключение к серверу c порта (-p),   
далее жмем `<Enter>` и затем идет запрос пароля (вводим пароль)

##Удаленное подключение к компьютеру    

> `ssh login@10.01.143` — Подключение к комьпютеру c IP 10.01.143 с логином login  
> `ssh '-p 2200' root@178.154.84` - подключение с указанием порта   
> `kill finder` — завершить программу finder на удаленном компе  

##Работа с сетью

> `whois site.ru` — получение информации о сайте с помощью сервиса whois
> `host site.ru` — получение информации о DNS сайта
> `host -a site.ru` - получение расширенную инфу о DNS сайта

##Работа с каталогами и файлами

###Поиск текста в файлах 

> Переходим в папку, в которой собираемся искать текст (с помощью команды `cd`, см. ниже):
> `grep -r "text in files" ./`  - Рекурсивный поиск текста в файлах и папках, относительно текущей папки. 

###Запуск bash скрипта из консоли: 
> `sh bash_script.sh` - запускает на выполнение скрипт, написанный в файле (язык bash)

###Навигация по каталогам

> `pwd` — показать текущий путь  
> `cd dir1` — перейти в каталог dir1  
> `cd ..` — перейти в каталог на уровень выше  
> `cd ~` — перейти в домашний каталог текущего пользователя  
> `ls -l` — показать файлы в текущем каталоге (расширенный вид)  
> `ls -la` — показать скрытые файлы  

###Узнаем размер файлов и папок  

> `du -sh [путь]`   
> `du -sh *` — размер всех папок и файлов в текущем каталоге  

###Создание и копирование файлов   

> `touch file1.txt` — создать файл file1.txt  
> `cp file1 dir1` — скопировать файл file1 в каталог dir1  
> `mkdir dir1` — создать каталог dir1  

###Скопировать каталог в каталог:     

> `cp -R mysite.ru/min yoursite.ru/cat`  

###Перемещение и переименование файлов     

> `mv file1.txt newfile.txt` — переименовать файл file1.txt в файл newfile.txt  
> `mv file.txt dir1` — перенести файл file.txt в каталог dir1  
> `mv file.txt ..` — перенос файла на уровень выше  
> `mv file.txt ~/dir` — перенос файла в каталог dir домашнего каталога  

###Открытие и изменение файлов  

> `cat file.txt` — открыть файл file.txt в консоли  
> `nano file.txt` — открыть файл file.txt в редакторе "nano"     
если нет прав на редактирование файла, файл откроется только в режиме просмотра,   
см. следующую команду. Для выхода из редактора nano используется команда (Ctrl+X)  

> `nano file.txt` — открыть файл c правами администратора (для редактирования)   
> `sudo nano /etc/hosts` — открыть файл hosts c правами администратора   

###Удаление файлов и каталогов   

> `rm file1.txt` — Удалить файл "file1.txt"    
> `rm dir -r` — Удалить каталог "dir" (ключ -r означает рекурсивное удаление).   
Для пустых каталогов ключ -r можно не использовать.

###Cимволические ссылки (симлинки)

> **создать ссылку:** 
> `ln -s [адрес источника] [местоположение ссылки]`  
> `ln -s ../bitrix bitrix` - создание симлинка с именем bitrix в текущей дирректории,   
> адрес ссылки `../bitrix/` (каталог bitrix родительского каталога)   

###Установка прав на файлы и каталоги

> `ls -l` — выведем список файлов и каталогов с указанием прав  

> Например, для CMS Bitrix необходимы следующие права:
>> 775 - права на каталоги  
>> 664 - права на файлы

> `chown -R bitrix:bitrix ./`   
> Установка владельца и группы для текущего каталога (./)   
> R-рекурсия, пользователь:группа ./ - текущий каталог  

> `cmod -R 0777 ./`    
> Установка прав 007 на файлы и папки (выполняется для файлов и папок текущего каталога)

###Раздельная установка прав:     
> 755 для каталогов (-type d),    
> 644 для файлов (-type f))   

>  `find ./ \( -type d -exec chmod 775 '{}' \; \) , \( -type f -exec chmod 664 '{}' \; \)`

###Установка прав в несколько шагов (простой способ)   
> Cначала переходим в нужный раздел, затем последовательно выполняем:   
>   
```
cd ~/www 
find . -type d -exec chmod 755 {} \; 
find . -type f -exec chmod 644 {} \; 
find . -type d -exec chown bitrix:bitrix {} \; 
find . -type f -exec chown bitrix:bitrix {} \;
``` 

##Работа с процессами (утилиты для мониторинга системы)   

> `top` — показать список текущих процессов и их параметры   
> сожалению невозможно увидеть весь список, если он большой, нет возможности листать.  
Для выхода из режима просмотра процессов, используются клавиши `<CTRL+Z>` или `<Q>`

> `ps auxw` — показать слепок процессов (PID - ID процесса).  
> `kill PID` — убить процесс по его PID.   
> Примечание: находим процесс который кушает очень много памяти,   
> находим его PID и можем таким >образом убить процесс используя команду kill и его PID.  

##Процессы, которые необходимо контролировать на серверах:  

> httpd - демон апача
> nginx - веб сервер nginx
> mysqld - демон mysql

###Команды для проверки статусов:

> service httpd status 
> service nginx status
> service mysqld status

###Перезапуск демонов: например для  httpd (для остальных аналогично)

> `service httpd stop` — остановка демона  
> `service httpd start` — запуск демона  
> `service httpd restart` — рестарт демона (аналогично start и stop)   


##Дополнительные утилиты   

> `free` — показывает состояние оперативной памяти в байтах  
> `free -m` — в мегабайтах  
> `free -h` — в гигабайтах  

>Примечание: +/- buffer/cash — дополнительная файловая память  

> `df -h` — cостояние HDD (использованная память в Гагабайтах),   
> вывод данных с разбивкой по разделам жесткого диска   

> `mount` — вывод списка разделов жесткого диска   
> `fdisk -l` — получение информации о жестких дисках с учетом разбивки на разделы  


##Скачивание файлов с удаленного сервера  

> `wget --progress=bar http://www.site.ru/backup/file.tar.gz` 
> скачать файл file.tar.gz c сайта site.ru  
> Примечание: можно использовть ключ: --progress=dot

> `rsync` — аналогичная команда (см. ниже)

##Копирование файла с удаленного сервера в текущий каталог   
> `scp root@31.193.195.61:/backup/www/2014-08-01/site.tar.gz site.tar.gz`  
> `scp -P 2200 root@31.193.195.61:/backup/www/2014-08-01/site.tar.gz site.tar.gz`   
>  C указанием порта

##Копирование файла (из текущего каталога) на удаленный сервер (в каталог)  
> `scp site.tar.gz root@31.193.195.61:/backup/www/2014-08-01/`   
> `scp -P 2200 site.tar.gz root@31.193.195.61:/backup/www/2014-08-01/`  
> С указанием порта  

**Примечание:**  
> Общая идея: csp [-P порт] <откуда> <куда> 

> Пути к каталогам могут не быть как можно предположить из видимой структуры файлов в среде разработки или файловом менеджере, по этой причине могут появляться ошибки типа: `is not a directory`. Реальный адрес (относительно корня сервера) можно узнать через команду `pwd`  

> **Аналогично можно копировать каталоги целиком не архивируя:**      
> Скопировать всё содержимое папки на сервере (рекурсивно) в локальную папку (с подробным выводом):    
> `scp -r root@server.my:/home/dir/ /home/local/my/`  

###Копирование между серверами:  
> `scp -r root@server1.my:/home/dir/ root@server2.my:/home/dir/`  

###Копирование с указанием порта:   
> `scp -P 9999 file.zip user@server.my:~/`   

**Дополнительные флаги:**   
> `-r` - рекурсивное копирование (для директорий)   
> `-C` - использовать сжатие при передачи   
> `-P` - порт ssh:    
> http://wiki.enchtex.info/tools/console/scp   

###Команда `rsync`

**Копирование папки с сайтом на другой сервер с помощью команды `rsync`**

> Сначала нужно на сервере, с которого копируем перейти в каталог,   
> который копируем и ввести команды  
> Например текущий каталог на сервере, с которого делаем копирование: 
> /home/bitrix/www/activecloud/httpdocs/www/site.ru      

**Копирование каталога: site.ru:**  
> `rsync -e 'ssh -p22' -aH --delete  --exclude="CACHE/*" --progress -lzuogthvr --compress-level=9 ./ admin_ftp@89.253.222.122:/var/www/vhosts/site.ru/httpdocs/site.ru/` 

**Копирование каталога bitrix:**  
> `rsync -e 'ssh -p22' -aH --delete  --exclude="CACHE/*" --progress -lzuogthvr --compress-level=9 ./bitrix/ admin_ftp@89.253.222.124:/var/www/vhosts/site.ru/httpdocs/site.ru/bitrix/`

**Копирование каталога upload:**  
> `rsync -e 'ssh -p22' -aH --delete  --exclude="CACHE/*" --progress -lzuogthvr --compress-level=9 ./upload/ admin_ftp@89.253.222.124:/var/www/vhosts/site.ru/httpdocs/site.ru/upload/`  

*Примечание:*  
> `admin_ftp@89.253.222.124` - логин (доступ) и host сервера, на который копируем  
> После вставки команды в консоль система спросит пароль на сервер, на который делается копирование (вставляем пароль, дальше идет копирование с выводом списка файлов на экран)

##Работа с архивами

> Пусть мы скачали один архив разбитый на два файла: archive.tar.gz, archive.tar.gz2  
> Эти два архива можно слить в один файл командой:

> `cat archive.tar* > newfile.tar.gz` — слияние архивов * означает любые символы

> `tar -xzf newfile.tar.gz` — разархивация файла,  
> разархивированные файлы кладутся в соответствии с путями (если исходный архив находится в корне сайта)
работает для архивов: `*.tar.bz2, *.tar.bzip2, *.tbz2, *.tb2, *.tbz` 

> `gzip -d backup.gz` — разархивация файла запакованного как .gz  


##Работа с MYSQL  

**Терминал поддерживает режим команд MySQL, для этого нужно перейти в режим MySQL**   
> `mysql` — переход в режим mysql (если не требуется вводить пароль)  
> `mysql –uUSERNAME –pPASSWORD -hHOST` — подключение к MySQL демону (если требуется вводить пароль)  
> *Указываются доступы USERNAME, PASSWORD к Базе данных, а не к SSH!*  
> Если команда прошла успешно, значит мы находимся в режиме mysql   

##Создание базы данных

**выполняется в режиме `mysql>`**:

> 1) Создать базу данных  
> 2) Назначить права к базе  
> 3) Перезагрузить демон MYSQL  

*Примечание:*  
> - В режиме команд mysql в конце строк обязательно необходимо ставить точку с запятой (;)    
> - Используются кавычки типа: `текст в кавычках`   

> `mysql> create database my_site;` — создать базу данных   
> `mysql> grant all privileges on my_site.* to my_site@'localhost' identified by 'PASSWORD';`   
> назначение прав на базу (указывается база и пароль)  

> `mysql> exit` — Выход из режима MYSQL    
> `service mysql restart` — перезапуск демона MySQL  

###Список типичных действий для существующей базы данных  

> `mysql> SHOW DATABASES;` — показать все базы данных  
> `mysql> USE database;` — переключится на базу database  
> `mysql> describe * from myDB;` - получить описание по всем таблицам  
> `mysql> describe `table1`;` - посмотреть структуру таблицы table1  
> `mysql> SELECT * FROM table;` - получить значение полей из таблицы  
> `mysql> SELECT * FROM table /G;` - получить значение полей из таблицы с разбивкой по строкам (так удобнее)    


###Запись данных в поле таблицы 

> `mysql> USE mytable;` - выбор таблицы, с которой будем работать   
> `mysql> INSERT INTO mytable VALUES ('17','text','site.ru');` - Добавление поля с записью в таблицу   

##Работа с бэкапами MySQL 

**Нижеприведенные команды производятся вне режима mysql:**

> `mysql dbname <  backup_bdname.sql` — залить файл "backup\_bdname.sql" в базу dbname  
> `mysqldump my_site > my_site.sql` — создание файла дампа базы (бэкапа) из базы my\_site в файл my\_site.sql  
> `mysqldump -uUSERNAME -pPASSWORD my_site > my_site.sql`   
> Если пользователь не имеет прав на работу с базой, необходимо указывать права.     
> **Итого: сначала указываем команду, логин и пароль от БАЗЫ, затем действия**    



