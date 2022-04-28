- [Установка сертифицированной RedOS](#install_redos)
- [Обновление до версии 7.3 certified](#update_redos)
- [CryptoPro](#cryptopro)
    + [Установка VeraCrypt](#veracrypt)
    + [Установка Chromium-Gost](#chromium-gost)
- [Р7-офис](#r7-office)
- [Чат](#chat)
- [x11vnc](#x11vnc)
- [remmina](#remmina)
- [Подключение сетевого каталога (межгород)](#cifs_mount)
- [Настройка SSH](#ssh)


## Установка сертифицированной RedOS <a name="install_redos"></a>

Образ сертифицированной версии 7.3 [здесь](https://disk.yandex.ru/d/6Du23QhPuLV6FA)  
Образ сертифицированной версии 7.2 [здесь](https://disk.yandex.ru/d/GTulgkvV7m_qMA)  

Создание загрузочной флешки [тут](https://redos.red-soft.ru/base/manual/red-os-installation/iso-to-usb-cd-dvd/). Для винды рекомендую [rufus](https://github.com/pbatard/rufus/releases/download/v3.17/rufus-3.17.exe)  

## Обновление RedOS 7.2c до версии 7.3c <a name="update_redos"></a>
На сайте редоса есть подробная [статья](https://redos.red-soft.ru/base/update/update-to-7-3/) по обновлению с 7.2 на 7.3  

Дальше опишу, что делал я (чистая сертифицированая система 7.2 сразу после установки):  
`su root`  

    yum update -y
    yum remove anaconda-core firstboot yumex python34-libs ipa-common python2-policycoreutils python2-caja caja-schemas mariadb-server pcs libreport python-ntplib libvncserver bind-libs-lite freerdp* -y
    yum autoremove -y
    sed -i 's!7.2!7.3!g' /etc/yum.repos.d/*.repo && yum clean all && yum makecache

Переходим в консольный режим (в графическом будут ошибки - проверено):  
Жмём __Ctrl+Alt+F2__, логин _root_, пароль (при наборе не виден), набираем `systemctl stop gdm`, опять жмём __Ctrl+Alt+F2__  
`yum update kernel-lt systemd yum grub2 redos-release -x wine* -y`  
`dnf update -y`  
`dnf install libyui-mga-gtk -y`  
`dnf groupinstall mate-desktop -y`  
`reboot`  


## CryptoPro <a name="cryptopro"></a>
Скачай дистрибутив с сайта [КриптоПро](https://www.cryptopro.ru/products/csp/downloads) (КриптоПро CSP 5.0 для Linux (x64, rpm))  
или [отсюда](https://disk.yandex.ru/d/pAfPZadoqroDPA)

    cd ~  
    cd Загрузки
    tar -xzf linux-amd64.tgz
    cd linux-amd64
    su root --command=./install_gui.sh

Далее - Далее - Установить  
Ввести лицензию свою лицензию или: _50500-00000-0Z000-00M22-0GF2D_ Выход  
В менюшке Инструменты КриптоПро - проверь лицензию  

### Установка VeraCrypt <a name="veracrypt"></a>

КриптоПро видит контейнеры HDD только в определённом каталоге  
Флешки и токены видны без танцев с бубном  

Каталог, где КриптоПро видит контейнеры: /var/opt/cprocs/keys/имя_пользователя  

#### Я вместо флэшек использую зашифрованный файловый контейнер __VeraCrypt__  

Скачивай [VeraCrypt](https://veracrypt.fr/en/Downloads.html) (RPM packages: CentOS 8/Fedora 34: GUI)  
Устанавливай, запускай, дальше по шагам:  

- менюшка __Тома__ - __Создать новый том__
- __Создать зашифрованный файловый контейнер__ (можно просто Далее нажать)
- __Обычный том__ (Далее)  
- кнопка __Выбрать файл__ - сохранить куда-нибудь под каким-нибудь именем - __Далее__
- __Далее__
- размер тома - __32Мб__ (или меньше - чем больше том, тем он дольше расшифровывается)
- __задай суперсложный пароль!!!__
- файловая система __FAT__
- __двигай__ энергично мышкой)) полоску до конца можно не доводить - __Разметить__
- __Выход__
- __Слот 1__ - Выбрать файл - __Открыть__ - __Смонтировать__
- Ввести суперсложный пароль и нажать кнопку __Опции!__
- __Смонтировать в каталог__ - __Выбрать__ - __Другие места__ - _Компьютер_ - ___/var/opt/cprocs/keys/имя_пользователя___ - __Открыть__ - __ОК__ (ввести пароль админа)
-  менюшка __Избранное__ - __Добавить смонтированный том в список избранных томов__ - __ОК_

Дальше в зависимости от ситуации   
- если есть __токен__ с контейнерами, стандартными средствами криптопро копируй их на созданный диск - назначение будет HDIMAGE.....(надо проверить - токенами на линуксе не пользовался)  
- если есть __флешка__ с контейнерами, просто скопируй все контейнеры (каталоги) в каталог _/var/opt/cprocs/keys/имя_пользователя_

Для установки сертификата заходи:  
- Инструменты КриптоПро - Контейнеры - Установить сертификат

В дальнейшем для использования этого зашифрованного контейнера с контейнерами)) в __VeraCrypt__ щёлкай __Избранное__ - свой том (внизу)  

В линуксовой версии VeraCrypt нет опции авторазмонтирования по тайм-ауту (или я не нашёл). Размонтируй вручную!  

Если закинуть зашифрованый файловый контейнер на яндекс диск (к примеру), можно использовать его и в других системах на других компьютерах. Не забудь задать суперсложный пароль при создании файлового контейнера!  

Можно создать пару зашифрованных контейнеров - один для неактуальных ЭЦП, второй для актуальных  
VeraCrypt есть для всех ОС - рекомендую пользоваться ей и под виндой (там можно поставить авторазмонтирование - вообще красота)   

### Установка Chromium-Gost <a name="chromium-gost"></a>
Для работы с ЭЦП рекомендую использовать браузер chromium-gost и больше ни для чего его не юзать!  
Он часто обновляется, так что почаще жми ссылку ниже для обновления  

Скачай и установи [посдедний chromium-gost](https://github.com/deemru/Chromium-Gost/releases/latest/) (rpm)  

#### Настройка Chromium-Gost
Открой в chromium-gost:  
[Контур.Веб-диск](https://install.kontur.ru/uc)  

## Установка Р7-офис <a name="r7-office"></a>
Скачать актуальную версию Р7-офис для RedOS (и других ОС) можно по [ссылке](https://r7-office.ru/downloads)  

__Установка шрифта по умолчанию самостоятельно:__  
Открыть от имени админа файлы /opt/r7-office/desktopeditors/converter/empty/new.\*, поменять шрифт на Libre Serif и сохранить  

__Установка шрифта по умолчанию в Windows:__  
Файлы находятся в папке C:\\Program Files\\R7-Office\\Editors\\converter\\empty  

__Плагины:__  
[плагин](https://disk.yandex.ru/d/W9ztR5q_FoXWrg) для подсчёта символов и слов в выделеном фрагменте  

__Лицензия:__  
Если возникают проблемы с лицензией, почистите папку C:\\ProgramData\\R7-Office\\License  
В линуксе файл лицензии лежит в /etc/r7-office/license/  


## Чат <a name="chat"></a>

[Скачать Spark](https://www.igniterealtime.org/downloadServlet?filename=spark/spark_2_9_4-with-jre.exe) для Windows
[Скачать Spark](https://www.igniterealtime.org/downloadServlet?filename=spark/spark-2.9.4.rpm) для Linux

Домен: 10.13.62.50  
Перед первым подключением щёлкнуть Дополнительно - вкладка Security - поставить галочку Disable certificate hostname verification  

## Установка и настройка удалённого доступа x11vnc (RedOS 7.3) <a name="x11vnc"></a>
Для RedOS 7.2 смотри инструкцию [здесь](https://redos.red-soft.ru/base/server-configuring/remote-control/x11vnc/?sphrase_id=12060)  

`su root`

Устанавливаем пакет x11vnc:  

    dnf install x11vnc -y

Сохраняем пароль для доступа (пароль придумываем посложнее):  

    x11vnc -storepasswd "ПРИДУМАЙ_ПАРОЛЬ_И_ВСТАВЬ_СЮДА" /etc/vncpasswd

Настраиваем автоматический запуск:  

    echo '[Unit]
    Description=X11vnc server for GDM
    After=display-manager.service
    [Service]
    ExecStart=/usr/bin/x11vnc -many -shared -display :0 -auth guess -noxdamage -rfbauth /etc/vncpasswd
    Restart=on-failure
    RestartSec=3
    [Install]
    WantedBy=graphical.target' > /lib/systemd/system/x11vnc.service
    systemctl daemon-reload
    systemctl enable --now x11vnc.service
    systemctl status x11vnc.service

Можно запускать клиент Remmina и подключаться  

##  Установка remmina из snap <a name="remmina"></a>
После последнего обновления отвалился плагин RDP для remmina  
Установил из snap:  
Установка самого snapd:  
`su root`  

    dnf install snapd
    ln -s /var/lib/snapd/snap/ /snap/

Установка remmina:  

    snap install remmina
    ln -s /home/$(whoami)/.ssh /home/$(whoami)/snap/remmina/common/  # ссылка на ключи SSH
    sudo snap connect remmina:avahi-observe :avahi-observe # servers discovery
    sudo snap connect remmina:cups-control :cups-control # printing
    sudo snap connect remmina:mount-observe :mount-observe # mount management
    sudo snap connect remmina:password-manager-service :password-manager-service # password manager
    sudo snap connect remmina:audio-playback :audio-playback # audio sharing
    sudo snap connect remmina:audio-record :audio-record # microphone

Чтобы подтянуть сохранённые соединения в параметрах remmina выбрать Папку данных /home/_user_/.local/share/remmina  


## Подключение сетевых каталогов <a name="cifs_mount"></a>  
скрипт не проверяет наличие строки для монтирования в fstab!  
`su root`  

    mkdir /mnt/obmen
    chmod 777 /mnt/obmen
    echo -e "username=user1\npassword=1234\ndomain=SAMBA" > /root/.obmen
    chmod 400 /root/.obmen
    echo "//10.13.62.251/obmen/SHARE /mnt/obmen cifs credentials=/root/.obmen,iocharset=utf8,file_mode=0777,dir_mode=0777 0 0" >> /etc/fstab
    mount -a
    exit

Создаём ссылку на рабочем столе пользователя (запускать под пользователем)  

    ln -s /mnt/obmen /home/`whoami`/Рабочий\ стол/Обмен

Подключение папки с FineReader  

    mkdir /mnt/finereader
    chmod 777 /mnt/finereader
    echo -e "username=Администратор\npassword=1\ndomain=SAMBA" > /root/.finereader
    chmod 400 /root/.finereader
    echo "//10.13.62.1/finereader /mnt/finereader cifs credentials=/root/.finereader,vers=1.0,iocharset=utf8,file_mode=0777,dir_mode=0777 0 0" >> /etc/fstab
    mount -a
    exit

Создаём ссылку на рабочем столе пользователя (запускать под пользователем)  

    ln -s /mnt/finereader /home/`whoami`/Рабочий\ стол/Преобразовать\ в\ Word

Монтирование при входе пользователя  

    echo "mount -a &" >> /etc/gdm/PreSession/Default

## SSH <a name="ssh"></a>
На сервере (локально) запускаем SSHD:  
`su root`  
`systemctl enable --now sshd`

На клиенте (то есть на своей машине) генерируем ключи (один раз!) и копируем их на сервер:  
`ssh-keygen -t rsa`  
`ssh-copy-id -i ~/.ssh/id_rsa.pub user@server`

Логинимся на сервер `ssh user@server` (пароль не запрашивается) и отключаем парольную аутентификацию:  

    sed -i 's!#PasswordAuthentication yes!PasswordAuthentication no!g' /etc/ssh/sshd_config
    systemctl restart sshd  
