## Part 1. Установка ОС

- *результат выполнения команды `cat /etc/issue` содержит информацию о текущей версии установленной системы* ![Ubuntu version screenshot](screenshots/ubuntu_version.png)<br>

## Part 2. Создание пользователя

- *команда для создания нового пользователя; флаг g, чтобы добавить нового пользователя в группу `adm`* ![useradd screenshot](screenshots/useradd.png)<br>

- *результат вывода команды `cat /etc/passwd`, новый пользователь на последней строке*![passwd sreenshot](screenshots/passwd.png)<br>

## Part 3. Настройка сети ОС

- *изменила статическое имя машины на user-1 и проверила, что имя изменилось*![hostname screenshot](screenshots/hostname.png)<br>

- *установила временную зону соответствующую моему текущему расположению (Москва)* ![task3_date screenshot](screenshots/task3_date.png)<br>

- *вывела названия сетевых интерфейсов с помощью консольной команды `ip`, флаг `а` - all* ![ip screenshot](screenshots/ip.png)<br>

`Интерфейс lo` (loopback) - это виртуальный сетевой интерфейс, который используют для подключения приложений и процессов на одном компьютере к другим приложениям и процессам. На Unix-подобрых системах присутствует по умолчанию и обычно имеет имя lo. Наиболее широко используемый IP адрес в механизмах loopback — 127.0.0.1.

- *вывела ip адрес устройства от DHCP сервера* 
<br>![ip DHCP screenshot](screenshots/ip_DHCP.png)<br>

DHCP (англ. Dynamic Host Configuration Protocol — протокол динамической настройки узла) — сетевой протокол, позволяющий сетевым устройствам автоматически получать IP-адрес и другие параметры, необходимые для работы в сети TCP/IP. Данный протокол работает по модели «клиент-сервер». 

- определила и вывела внешний ip-адрес шлюза (ip) - 185.61.78.21 и внутренний IP-адрес шлюза, он же ip-адрес по умолчанию (gw) - 10.0.2.2 
<br> *внешний ip-адрес* 
<br>![ip outer screenshot](screenshots/outerip.png)<br> *внутренний ip-адрес* 
<br>![gw screenshot](screenshots/gw.png)<br>

- Задала статичные (заданные вручную, а не полученные от DHCP сервера) настройки ip, gw, dns (используя публичные DNS серверы, например 1.1.1.1 или 8.8.8.8). DHCP автоматически присваивает устройству IP, поэтому сначала необходимо отключить облачную инициализацию.<br>
<br> *открыла файл конфигурации через команду `sudo nano /etc/cloud/cloud.cfg.d/subiquity-disable-cloudinit-networking.cfg`* ![config screenshot](screenshots/cloudinitnetwork.png)<br>
<br> *открыла файл конфигурации netplan в текстовом редакторе nano с помощью команды: `sudo nano /etc/netplan/00-installer-config.yaml`*<br>![netplan dhcp network](screenshots/netplandhcp.png)<br>
<br>*задала статические настройки сети: изменила значение параметра dhcp4 на false, в addresses указала статический IP-адрес: 10.0.2.15/24, и в gateway4 зададим внутренний IP-адрес 10.0.2.2; в параметре addresses раздела nameservers указала публичные серверы.*<br>![netplan static screenshot](screenshots/netplan_static.png)<br>
<br>*для применения изменений использовала команду `sudo netplan apply`*<br>![netplan apply screenshot](screenshots/netplanapply.png)<br><br>

- *после перезагрузки виртуальной машины командой `ip route` проверила сохранились ли выставленные вручную настройки (тип изменился на static)*<br>![static screenshot](screenshots/STATIC.png)<br>
<br>*пропинговала удаленный хост `ya.ru`*<br>![pingyaru screenshot](screenshots/pingyaru.png)<br>*пропинговала удаленный хост `1.1.1.1`*<br>![ping1111 screenshot](screenshots/ping1111.png)

## Part 4. Обновление ОС
- *для обновления системы до последней на момент выполнения задания версии использовала команды `sudo apt update` и `sudo apt upgrade`*
- *после обновления системных пакетов, проверила отсутствие новых обновлений:*
<br>![no new updates screenshot](screenshots/nonewupdates.png)

## Part 5. Использование команды sudo
Утилита `sudo` (substitute user and do — дословно «подменить пользователя и выполнить») —  это утилита для операционных систем семейства Linux, позволяющая пользователю запускать программы с привилегиями другой учётной записи, как правило, суперпользователя root. Смысл выполнения команды от root в том, что у него повышенные права доступа и, применяя sudo, обычный пользователь может выполнить те действия, на которые у него недостаточно прав.

 - чтобы поменять hostname ОС от имени пользователя, созданного в пункте Part 2 (используя sudo), необходимо сначала разрешить пользователю `cucumber` пользоваться командой `sudo`. Ввела команду для управления пользователями Linux и добавила пользователя в группу sudo: `sudo usermod -aG sudo cucumber` (флаг G позволяет указать список дополнительных групп, в которые должен входить пользователь. Флаг а позволяет добавлять новые дополнительные группы, не удаляя старые)
 <br>![sudo group screenshot](screenshots/sudogroup.png)

 - сменила текущего пользователя на пользователя cucumber с помощью команды `su`
  <br>![su screenshot](screenshots/su.png)

 - Для того чтобы изменить hostname на `cucumber` использовала команду `hostnamectl set-hostname cucumber`. Для проверки результата изменения ввела команду `hostname`. 
 <br>![hostname cucumber screenshot](screenshots/hostnamecucumber.png)

 ## Part 6. Установка и настройка службы времени
 - С помощью команды `date` вывела текущее время системы, далее воспользовалась командой ` timedatectl show`, как видно из вывода команды протокол синхронизации времени (NTP) активен:
<br> ![timedate screenshot](screenshots/timedate.png)<br>

## Part 7. Установка и использование текстовых редакторов

- выполнила установку текстовых редакторов командами `sudo apt install vim`, `sudo apt install nano` и `apt install mcedit`

#### Изменение файла c сохранением изменений

- `VIM` <br> выполнила команду `vim test_vim.txt`, для начала ввода текста нажала клавишу `I` (insert). для закрытия файла с сохранением изменений использовала сочетание клавиш `ESC + :wq`
<br> ![vim_test screenshot](screenshots/vim_test.png)<br>

- `NANO` <br> выполнила команду `nano test_nano.txt`. для закрытия файла с сохранением изменений использовала команды `^O` и `^X`
<br> ![nano_test screenshot](screenshots/nano_test.png)<br>

- `mcedit` <br> выполнила команду `mcedit test_mcedit.txt`. для закрытия файла с сохранением изменений использовала команды `F2` и `F10`
<br> ![mcedit_test screenshot](screenshots/mcedit_test.png)<br>

#### Изменение файла без сохранения изменений

- `VIM` <br> снова выполнила команду `vim test_vim.txt`, для начала ввода текста нажала клавишу `I` (insert). для закрытия файла без сохранения изменений использовала сочетание клавиш `ESC + :q!`
<br> ![vim_test_nosave screenshot](screenshots/vim_test_nosave.png)<br>

- `NANO` <br> выполнила команду `nano test_nano.txt`. для закрытия файла без сохранения изменений использовала команду `^X`
<br> ![nano_test_nosave screenshot](screenshots/nano_test_nosave.png)<br>

- `mcedit` <br> выполнила команду `mcedit test_mcedit.txt`. для закрытия файла без сохранения изменений использовала команду `F10`
<br> ![mcedit_test_nosave screenshot](screenshots/mcedit_test_nosave.png)<br>

#### Поиск и замена слова

- `VIM` <br> снова выполнила команду `vim test_vim.txt`. для поиска по содержимому использовала сочетание клавиш `ESC + /samellao`.
<br> ![vim_search screenshot](screenshots/vim_search.png)<br>
для замены было использовано сочетание `:s/samellao/21 School 21` 
<br> ![vim_replace screenshot](screenshots/vim_replace.png)<br>

- `NANO` <br> снова выполнила команду `nano test_nano.txt`. для поиска по содержимому использовала команду `^W`.
<br> ![nano_search screenshot](screenshots/nano_search.png)<br>
для замены было использовано сочетание `^W` -> `^R` + `samellao` + `21 School 21` 
<br> ![nano_replace screenshot](screenshots/nano_replace.png)<br>

- `mcedit` <br> снова выполнила команду `mcedit test_mcedit.txt`. для поиска по содержимому использовала команду `F7`
<br> ![mcedit_search screenshot](screenshots/mcedit_search.png)<br>
для замены была использована команда `F4`
<br> ![mcedit_replace screenshot](screenshots/mcedit_replace.png)
<br> ![mcedit_replace2 screenshot](screenshots/mcedit_replace2.png)<br>

## Part 8. Установка и базовая настройка сервиса SSHD

- для установки службы SSHd использовала команды `sudo apt-get install ssh` и `sudo apt install openssh-server` 
<br> ![ssh install screenshot](screenshots/ssh_install.png)<br>
- добавила автостарт службы при загрузке системы при помощи команды `sudo systemctl start sshd`
<br> ![sshd autostart screenshot](screenshots/sshd_autostart.png)<br>

- Для перенастройки службы SSHd на порт 2022 внесла изменения в файл `\etc\ssh\sshd_config` (раскоментировала строку port и ввела значение 2022)
<br> ![ssh screenshot](screenshots/ssh_config.png)<br>

- для того, чтобы проверить наличие ssh процесса, использовала команду `ps -e`, в команде `ps` опция `-e` выводит все запущенные процессы.
<br> ![ps ssh screenshot](screenshots/ps_ssh.png)<br>

#### команда ps показывает запущенные процессы, выполняемые пользователем в окне терминала;

ключи:
<br> `-e` или `-A` чтобы просмотреть все запущенные процессы;
 <br>`-d` чтобы показать все процессы, кроме лидеров сессии;
<br> `-d` `-N` можно инвертировать вывод с помощью переключателя -N. Например, если хочу вывести только лидеров сеансов;
<br> `T` увидеть только процессы, связанные с этим терминалом;
<br> `r` просмотреть все работающие (running) процессы;
<br> `-p 'pid'` если знать идентификатор процесса PID, можно просто использовать следующую команду, для вывода процесса с этим 'pid';
<br> `U 'userlist'` найти все процессы, выполняемые конкретным пользователем;
<br> `-ef` получить полный список;

- для перезагрузки системы использовала команду `reboot`

- для получения сведений о состоянии сетевых соединений и слушаемых на данной машине портах ТСХ и UPD использовала команду `netstat -tan`. Вывод команды  должен содержать tcp 0 0 0.0.0.0:2022 0.0.0.0:* LISTEN
<br> ![netstat tan screenshot](screenshots/netstat_tan.png)<br>

значение ключей -tan:
<br>`-t` — отображение текущего подключения в состоянии переноса нагрузки с процессора на сетевой адаптер при передаче данных;
<br>`-a` — отображение всех подключений и ожидающих портов;
<br>`-n` — отображение адресов и номеров портов в числовом формате;

`proto` - имя порта, `Recv-Q` - количество байтов, помещенных в буфер обмена приема TCP/IP (не переданных), `Send-Q` - количество байтов помещенных в буфер отправки TCP/IP (не отправленных), `Local Adress` - локальный адрес, `Foreign Address` - внешний адрес, `State` - состояние.

Значение Foreign Addres `0.0.0.0` - это специальный IP-адрес, известный как "маршрут по умолчанию" или "неуказанный адрес". Он используется для указания того, что трафик должен отправляться на все интерфейсы компьютера, независимо от их индивидуальных IP-адресов.

## Part 9. Установка и использование утилит top, htop

### TOP
Утилита `top` — это консольный диспетчер задач. Он показывает общую информацию о системе и информацию о каждом процессе. 
<br>![top screenshot](screenshots/top.png)<br>

- uptime = 43 min
- количество авторизованных пользователей = 1
- общая загрузка системы 0,00 0,00 0,00
- количество процессоров 97 (1 используется, 96 в режиме сна)
- загрузка CPU 99.3% времени простаивания CPU; 0,3% времени запуска ядра (sy); 0,3% времени затрачено на обслуживание программных прерываний на уровне ядра (si)
- загрузка оперативной памяти - используется 143,5 (всего 1971,6 МиБ)
- загрузка памяти подкачки - используется 0 (всего 1481 МиБ)
- `1` - pid процесса занимающего больше всего памяти
- `13` - pid процесса, занимающего больше всего процессорного времени

### HTOP

 Утилита `htop` — это консольный и интерактивный диспетчер задач, который похож на уже рассмотренный выше top.

- Сортировка по PID:
<br>![htop PID screenshot](screenshots/htop_PID.png)

- Сортировка по PERCENT_CPU
<br>![htop CPU screenshot](screenshots/htop_CPU.png)

- Сортировка по PERCENT_MEM
<br>![htop MEM screenshot](screenshots/htop_MEM.png)

- Сортировка по TIME
<br>![htop TIME screenshot](screenshots/htop_TIME.png)

- Фильтр по процессу sshd
<br>![htop sshd screenshot](screenshots/htop_SSHD.png)

- Поиск процессора syslog
<br>![htop syslog screenshot](screenshots/htop_syslog.png)

- Вывод hostname, clock и uptime
<br>![htop hostname screenshot](screenshots/htop_hostname.png)

## Part 10. Использование утилиты fdisk

`fdisk` - интерактивная консольная утилита, которая может создать таблицу разделов и разделы на жестком диске и управлять ими. 

- Результат выполнения `fdisk -l` приведен на скриншоте ниже:
<br>![fdisk screenshot](screenshots/fdisk.png)
<br>Название: /dev/sda
<br>Размер: 10 GiB
<br>Количество секторов: 20971520
<br>Размер swap: 1,8G

## Part 11. Использование утилиты df

Утилита `df` - показывает список всех файловых систем по именам устройств, сообщает их размер, занятое и свободное пространство и точки монтирования.

- Результат вывода `df /`
<br>![df screenshot](screenshots/df.png)
<br>Размер раздела - 8408452 килобайт
<br>Размер занятого пространства - 4784292 килобайт
<br>Размер свободного пространства - 3175444 килобайт
<br>Процент использования - 61%

- Результат вывода `df -Th /`
<br>![df Th screenshot](screenshots/df_Th.png)
<br>Размер раздела - 8.1G
<br>Размер занятого пространства - 4.6G
<br>Размер свободного пространства - 3.1G
<br>Процент использования - 61%
<br>Тип файловой системы ext4

## Part 12. Использование утилиты du

Утилита `du` - стандартная Unix-программа для оценки занимаемого файлового пространства.

- результат вывода размера папок /home, /var, /var/log сначала в байтах `sudo du -bs /home /var/log/ /var`(опция -b --bytes), затем в человекочитаемом виде `sudo du -hs /home /var/log/ /var`(опция -h --human-readable), затем и в том, и в том, но совместно эти два флага не совсем корректно отрабатывают `sudo du -bhs /home /var/log/ /var`
<br>![du screenshot](screenshots/du.png)

- размер всего содержимого в /var/log (не общее, а каждого вложенного элемента, используя *) `sudo du /var/log/*`
<br>![du var log screenshot](screenshots/var_log.png)
<br>![du var log 2 screenshot](screenshots/var_log2.png)

## Part 13. Установка и использование утилиты ncdu

Утилита `ncdu` - это псевдографическая утилита, которая работает в терминале Linux. Она отображает список файлов и директорий по объёму и позволяет удалять ненужные файлы.

- установка с помощью команды `sudo apt install ncdu`
- размер папки /home
<br>![ncdu home screenshot](screenshots/ncdu_home.png)

- размер папки /var
<br>![ncdu var screenshot](screenshots/ncdu_var.png)

- размер папки /var/log
<br>![ncdu var log screenshot](screenshots/ncdu_var_log.png)

## Part 14. Работа с системными журналами

- /var/log/dmesg
<br>![dmesg screenshot](screenshots/dmesg.png)

- /var/log/syslog
<br>![syslog screenshot](screenshots/syslog.png)

- /var/log/auth.log
<br>![authlog screenshot](screenshots/authlog.png)
<br>время последней успешной авторизации - 18:47:54
<br>имя пользователя - aastrokidd
<br>метод входа в систему - tty1 LOGIN

- перезапустила службу SSHd с помощью команды `sudo systemctl restart ssh` 
<br>![ssh restart log screenshot](screenshots/ssh_restart_log.png)

## Part 15. Использование планировщика заданий CRON

`Cron` – это планировщик задач. Если подробнее, то это утилита, позволяющая выполнять скрипты на сервере в назначенное время с заранее определенной периодичностью.

- с помощью команды `crontab -e` открыла конфигурационный файл и внесла туда новую команду `uptime`, которая будет вызываться через каждые 2 минуты.
<br>![crontab uptime screenshot](screenshots/crontab_uptime.png)

- вывела данные из системного журнала с помощью команды `tail /var/log/syslog`, чтобы найти там строчки (минимум две в заданном временном диапазоне) о выполнении;
<br>![crontab uptime syslog screenshot](screenshots/crontab_uptime_syslog.png)

- вывела список текущих заданий для CRON с помощью команды `crontab -l` 
<br>![crontab l screenshot](screenshots/crontab_l.png)

- удалила все задания из планировщика заданий с помощью команды `crontab -r` и вывела список текущих заданий для CRON повторно
<br>![crontab r screenshot](screenshots/crontab_r.png)
