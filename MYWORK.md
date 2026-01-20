# Операционные системы UNIX/Linux

## Part1 Установка ОС
Скачиваем программу для виртуализации - VirtualBox для Windows.

![alt text](images/image-1.png)

Скачиваем Ubuntu Server без графичческого интерфейса с сайта.

![alt text](images/image-3.png)

Выделяем память под Ubuntu.

![alt text](images/image-2.png)

Запускаем виртуальную машину.

![alt text](images/image-4.png)

Выполняем команду ```cat /etc/issue```, которая показывает информацию о версии ОС.

![alt text](images/image-5.png)



## Part2 Создание пользователя
Создаем нового пользователя cat1.

![alt text](images/image-6.png)

Добавляем в группу adm командой ```sudo usermod -aG adm cat1```

![alt text](images/image-9.png)

Выполняем команду ```cat /etc/passwd```

![alt text](images/image-7.png)

Убедились, что cat1 действительно есть в adm

![alt text](images/image-8.png)



## Part 3 Настройка сети ОС

Меняем имя хоста на user-1.

![alt text](images/image-10.png)

Смотрим, какая установлена временная зона.

![alt text](images/image-11.png)

Смотрим список доступных временных зон.

![alt text](images/image-12.png)

Меняем зону и проверяем замену.

![alt text](images/image-13.png)

Выполняем команду ```ip a``` для вывода названий сетевых интерфейсов.

![alt text](images/image-14.png)

lo (loopback) – виртуальный сетевой интерфейс, присутствующий по умолчанию в любом Linux. Это "замкнутый на себя" сетевой интерфейс, который позволяет компьютеру общаться с самим собой через сетевой стек, как если бы это было сетевое соединение с другим компьютером. Он используется для отладки сетевых программ и запуска серверных приложений на локальной машине. С этим интерфейсом всегда связан адрес 127.0.0.1. У него есть dns-имя – localhost.
Адрес 127.0.0.1 (IPv4) и ::1 (IPv6) всегда указывают на сам компьютер
Позволяет запускать серверные приложения и подключаться к ним с того же компьютера.
Службы, работающие только на 127.0.0.1, недоступны из внешней сети, тем самым это защищает чувствительные приложения от внешнего доступа.
Loopback интерфейс создается автоматически ядром Linux при загрузке потому что:
-он необходим для корректной работы сетевого стека
-многие системные процессы и приложения зависят от него
-это фундаментальная часть сетевой архитектуры UNIX-систем

Используя консольную команду, получили ip адрес устройства, на котором мы работаем, от DHCP-сервера.

![alt text](images/image-16.png)

DHCP - Dinamic Host Configuration Protocol - Протокол динамической настройки хоста

Узнаем внешний IP-адрес шлюза

![alt text](images/image-15.png)


Узнаем внутренний ip-адрес шлюза
![alt text](images/image-17.png)

Выполняем ```sudo nano /etc/netplan/01-netcfg.yaml```

![alt text](images/image-18.png)

Отредактировали - задали статичные настройки ip, gw, dns

![alt text](images/image-19.png)

```sudo reboot``` - перезагружаем систему.

Проверяем, что ip поменялись.

![alt text](images/image-20.png)

Проверяем DNS

![alt text](images/image-21.png)

Пингуем 

![alt text](images/image-22.png)



## Part 4 Обновление ОС

Обновляем ОС

![alt text](images/image-23.png)

```sudo apt update```

```sudo apt upgrade```

Проверяем, что все обновлено до последней версии

![alt text](images/image-24.png)

## Part 5 Использование команды **sudo**

Даем пользователю cat1 права пользоваться sudo

![alt text](images/image-25.png)

sudo (англ. Substitute User and do, дословно «подменить пользователя и выполнить») - это программа для системного администрирования UNIX-систем, позволяющая пользователям выполнять команды с привилегиями другого пользователя, обычно суперпользователя (root), в соответствии с настройками безопасности, определенными в файле /etc/sudoers.

```sudo hostnamectl set-hostname cat2```

```sudo nano /etc/hosts```

```127.0.1.1   cat2```

Убеждаемся, что изменили имя хоста

![alt text](images/image-26.png)


## Part 6 Установка и настройка службы времени

Устанавливаем зону Europe/Moscow

```sudo timedatectl set-timezone Europe/Moscow``` - 

Настраиваем службу автоматической синхронизации времени через NTP: 

```sudo timedatectl set-ntp true```

![alt text](images/image-27.png)


## Part 7 Установка и использование текстовых редакторов 

VIM nano уже установлены 

![alt text](images/image-37.png)

```sudo apt install vim mc```

![alt text](images/image-29.png)

### Создание файлов

```vim test_vim.txt``` - создаем новый файл с vim
esc - выйти из режима редактирования
:wq - сохранить написанное и выйти из vim

![alt text](images/image-30.png)

```nano test_nano.txt``` - создаем новый файл с nano

Ctrl+O - сохранить
Ctrl+X - выйти

![alt text](images/image-31.png)

```mc test_mcedit.txt```
написать что то Fn+F2
выбрать 1
чтобы выйти Fn+F10

![alt text](images/image-34.png)


Убеждаемся, что все файлы созданы и в каждом записано thalasat

![alt text](images/image-28.png)

### Изменение без сохранения 

VIM

```vim test_vim.txt```
нажимаем i чтобы войти в режим вставки

![alt text](images/image-38.png)
редактируем файл

нажимем esc

```:q!``` - выход без сохранения

![alt text](images/image-39.png) -содержимое не поменялось
NANO

```nano test_nano.txt```

редактируем содержимое test_nano.txt
![alt text](images/image-40.png)

нажимаем CTRL+X, N - выходим без сохранения

![alt text](images/image-41.png) - содержимое не поменялось

MCEDIT
```mcedit test_mcedit.txt```

![alt text](images/image-42.png) - редактируем файл

Fn+F10

![alt text](images/image-43.png) - выходим без сохранения

![alt text](images/image-44.png) - содержимое не поменялось

### Поиск слова

VIM

Заменяем в vim thalasat на cat с командой ```s/<find_text>/<replace_text>```
выходим с :wq

![alt text](images/image-45.png) 

/ - это команда для поиска

![alt text](images/image-46.png) 

NANO

ctrl+W 
Ищем вхождения thal

![alt text](images/image-47.png)

nano нашел одно вхождение

![alt text](images/image-48.png)

ctrl + \ - открываем режим замены
меняем thal в файле на cat

![alt text](images/image-49.png)

![alt text](images/image-50.png)

Нажимаем Y

![alt text](images/image-51.png)

MCEDIT
Fn+F7
Ищем sat

![alt text](images/image-52.png) 

Fn+F4
Заменяем sat на cat
Дважды Enter - подтверждаем замену

![alt text](images/image-53.png)

Убеждаемся, что замена успешно проведена во всех файлах

![alt text](images/image-54.png)


## Part 8 Установка и базовая настройка сервиса **SSHD**

Устанавливаем службу SSHd.
```sudo apt update```
```sudo apt install ssh```
```sudo apt install openssh-server```

Автостарт службы при загрузке системы
```sudo systemctl enable ssh```

![alt text](images/image-55.png)

Редактируем файл ```sudo vim /etc/ssh/sshd_config```
Тем самым перенастраиваем службу SSHd на порт 2022.

![alt text](images/image-56.png)

Перезапускаем ssh - службу
```sudo systemctl restart ssh```

Убеждаемся, что процесс запущен

![alt text](images/image-57.png)

Команда ps (process ststus) - утилита для отображения информации о процессах запущенных в системе.

Ключ -C - фильтрует процессы по имени команды, показывая только процессы с указанным именем (в данном случае sshd)

Перезагружаем систему ```sudo reboot```

Смотрим сетевые соединения и порты.

![alt text](images/image-58.png)

- t - отображает только TCP
- a - показывает все прослушивающие порты и активные соединения
- n (numeric) - показывает числовые адреса вместо разрешения хостов и портов

## Part 9 Установка и использование утилит **top**, **htop**

```top```

![alt text](images/image-59.png)

  - uptime - 10;
  - количество авторизованных пользователей - 1;
  - среднюю загрузку системы - 0.00, 0.04, 0.05;
  - общее количество процессов - 96;
  - загрузку cpu - 0.0 us, 0.0 sy, 0.0 ni, 100.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0, st
  - загрузку памяти 1971.6 total, 1492.5 free, 148.8 used, 330.3 buff/cashe
  - pid процесса занимающего больше всего памяти - 1
  - pid процесса, занимающего больше всего процессорного времени - 1
- В отчёт вставь скрин с выводом команды htop:
  - отсортированному по PID, PERCENT_CPU, PERCENT_MEM, TIME;
  - отфильтрованному для процесса sshd;
  - с процессом syslog, найденным, используя поиск;
  - с добавленным выводом hostname, clock и uptime.

```htop```

![alt text](images/image-60.png)

Нажимаем F6 и выбираем нужный вариант сортировки
Отсортированный по PID:
![alt text](images/image-61.png)
Отсортирванный по PERCENT_CPU:
![alt text](images/image-62.png)
Отсортирванный по PERCENT_MEM:
![alt text](images/image-63.png)
Отсортирванный по TIME:
![alt text](images/image-64.png)
Нажимаем F4
![alt text](images/image-65.png)
Отфильтрованный для процесса sshd:
![alt text](images/image-66.png)
С процессом syslog, найденным, используя поиск
![alt text](images/image-67.png)
С добавленным выводом hostname, clock и uptime
![alt text](images/image-68.png)


## Part 10 Использование утилиты **fdisk**

```sudo fdisk -l```

![alt text](images/image-69.png)

Название диска: /dev/sda

Размер диска: 25 GiB (26 843 545 600 bytes)

Количество секторов: 52 428 800 секторов

```free -h ```

![alt text](images/image-70.png)

Swap: 2.0 GiB total (полностью свободен)

# Part 11 Использование утилиты **df** 

```df```

![alt text](images/image-71.png)

  - размер занятого пространства - 11758760
  - размер свободного пространства - 6072996
  - процент использования - 46%

Единица измерения - 1K-блоки (блоки по 1024 байта)

```df -h```

![alt text](images/image-72.png)
    - размер раздела - 12G
    - размер занятого пространства - 4,9G
    - размер свободного пространства - 5,8G
    - процент использования - 46%
Файловая система ext4


## Part 12. Использование утилиты **du**

Запускаем ```du```

![alt text](images/image-73.png)

Выводим размер папок /home, /var, /var/log (в байтах, в человекочитаемом виде)

![alt text](images/image-74.png)

![alt text](images/image-75.png)

Выводим размер всего содержимого в /var/log

```sudo du -h var/log/*```

![alt text](images/image-76.png)

## Part 13. Установка и использование утилиты **ncdu**

```sudo apt install ncdu```

q - для выхода

```ncdu /var/log```

![alt text](images/image-78.png)

```ncdu /var```

![alt text](images/image-79.png)

```ncdu /home```

![alt text](images/image-80.png)

## Part 14. Работа с системными журналами

```vim /var/log/dmesg```

![alt text](images/image-81.png)

```vim /var/log/syslog```

![alt text](images/image-82.png)

```vim /var/auth.log```

![alt text](images/image-83.png)

Последняя успешная авторизация в 20:48:55, пользователь cat2,
метод входа в систему pam_unix

Перезапускаем службу sshd

```sudo systemctl restart ssh```

В логах ищем сообщение о рестарте службы

![alt text](images/image-84.png)

## Part 15. Использование планировщика заданий **CRON**

```crontab -e```

Редактируем планировщик задач: добавляем ```*/2 * * * * uptime```

![alt text](images/image-85.png)

![alt text](images/image-86.png)

```cat var/log/syslog | grep CRON```

![alt text](images/image-87.png)

```crotab -l``` - смотрим текущие cron-задачи

![alt text](images/image-88.png)

Удаление из планировщика всех заданий и проврка, что все действительно удалено

![alt text](images/image-89.png)
