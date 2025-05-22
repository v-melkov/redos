- [Установка сертифицированной RedOS](#install_redos)
- [Обновление до версии 7.3 certified](#update_redos)
- [КриптоПро](#cryptopro)
    + [Установка КриптоПро ЭЦП browser plugin](#cryptopro_browser_plugin)
    + [Установка Окуляр ГОСТ](#ocular)
    + [Расширения для браузеров](#browser_extensions)
    + [Установка Chromium-Gost](#chromium-gost)
    + [Установка VeraCrypt](#veracrypt)
- [Р7-офис](#r7-office)
- [Чат](#chat)
- [x11vnc](#x11vnc)
- [rdesktop](#rdesktop)
- [Подключение сетевого каталога (межгород)](#cifs_mount)
- [Настройка SSH](#ssh)
- [Сетевой принтер](#printing)
- [Проверка диска на ошибки](#fsck)
- [Двухфакторная аутентификация](#2fa)
- [Установка сканера по умолчанию](#scanner)
- [Восстановление шрифта в терминале](#termfonts)

__Все файлы на Яндекс диске загружены мной__

## Установка сертифицированной RedOS <a name="install_redos"></a>
  
Образ сертифицированной версии 7.3 [здесь](https://disk.yandex.ru/d/6Du23QhPuLV6FA)  
Образ сертифицированной версии 7.2 [здесь](https://disk.yandex.ru/d/GTulgkvV7m_qMA)  

Создание загрузочной флешки 
Используйте [Ventoy](https://www.ventoy.net/en/download.html)  
В rufus создавать флешку в режиме **dd**  

## КриптоПро <a name="cryptopro"></a>
Скачай дистрибутив с сайта [КриптоПро](https://www.cryptopro.ru/products/csp/downloads) (КриптоПро CSP 5.0 для Linux (x64, rpm))  
или [отсюда](https://disk.yandex.ru/d/pAfPZadoqroDPA)

    cd ~  
    cd Загрузки
    tar -xzf linux-amd64.tgz
    cd linux-amd64
    su root --command=./install_gui.sh

Далее - Далее - Установить  
КриптоПро CSP 5.0 R2 (12000), R3 (13000).  
Проверено на версии КриптоПро CSP R3 (5.0.13000 с цифровой подписью от 13.05.2024)  

    50501-80007-EZP59-YY5DF-VL8FX
    50504-40000-1Z000-00NUH-U9BH3
    50503-20000-0U000-00554-RPX09  
    50501-30007-4R810-00UQ5-0MMH7  
    50501-80007-E9P59-YY7BP-8D0RB  
    50501-70007-49810-002L6-C1R0P    

КриптоПро CSP 4.0  
    
    4040W-90000-0ZVEN-MBWU1-Q7EUP  
    4040V-Y3010-01C17-Q5YBH-PFB4G  
    4040Y-Q0000-02Q6T-NFYX9-24Z86  
    4040W-20000-0168K-VQCQR-8XH45  

КриптоПро PDF v.2.0  

    PD20P-P000V-ABAC2-YYVZ3-E97RB   


В менюшке Инструменты КриптоПро - проверь лицензию  
  
### Установка КриптоПро ЭЦП Browser plugin <a name="cryptopro_browser_plugin"></a>
Скачиваем [отсюда](https://cryptopro.ru/products/cades/plugin/get_2_0)  

    cd ~  
    cd Загрузки
    tar -xzf cades-linux-amd64.tar.gz
    cd cades-linux-amd64
    su root --command='rpm -i cprocsp-pki-*.rpm'

Для Яндекс браузера качаем расширение [отсюда](https://addons.opera.com/ru/extensions/details/cryptopro-extension-for-cades-browser-plug-in/)  

Проверка плагина [здесь](https://www.cryptopro.ru/sites/default/files/products/cades/demopage/cades_bes_sample.html)  
  
Дополнительно устанавливаем плагин: `sudo dnf install ifcplugin-chromium`  
Установка корневых сертификатов: `sudo dnf install ca-certificates-ru`  

### Установка Окуляр ГОСТ для штампов ЭП в PDF-файлах  <a name="ocular"></a>

    sudo -E dnf install lsb-core-noarch
    sudo -E dnf install cprocsp-rdr-gui-gtk
    sudo -E dnf config-manager --add-repo http://packages.lab50.net/okular/redos/okularcsp.repo
    sudo -E dnf install okular-csp
  
  
### Установка VeraCrypt <a name="veracrypt"></a>

КриптоПро видит контейнеры HDD только в определённом каталоге  
Флешки и токены видны без танцев с бубном  

Каталог, где КриптоПро видит контейнеры: /var/opt/cprocs/keys/имя_пользователя  

#### Зашифрованный файловый контейнер __VeraCrypt__  

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
  
## Установка Р7-офис <a name="r7-office"></a>
Скачать актуальную версию Р7-офис для RedOS (и других ОС) можно по [ссылке](https://r7-office.ru/download_editor#3_2))  

__Плагины:__  
[Плагины для Р7-офиса](https://disk.yandex.ru/d/xIlCcAumIdQucA)  
drawio - вставка диаграмм draw.io  
photoeditor - редактор изображений  
speech - текст в речь  
translator - гугл переводчик  
typograf - исправление типографских ошибок  
wordscounter - подсчёт символов и слов   

__Лицензия:__  
Если возникают проблемы с лицензией, почистите папку `C:\\ProgramData\\R7-Office\\License`  
В линуксе файл лицензии лежит в `/etc/r7-office/license/`  


## Чат <a name="chat"></a>

[Скачать Spark](https://www.igniterealtime.org/downloadServlet?filename=spark/spark_3_0_2-with-jre.exe) для Windows  
[Скачать Spark](https://www.igniterealtime.org/downloadServlet?filename=spark/spark-3.0.2.rpm) для Linux  
 
Перед первым подключением щёлкнуть Дополнительно - вкладка Security - поставить галочку Disable certificate hostname verification  

## Установка и настройка удалённого доступа x11vnc (RedOS 7.3) <a name="x11vnc"></a>

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

## Установка rdesktop <a name="rdesktop"></a>  
Под рутом:  
`dnf install rdesktop`  

Под пользователем:  

    read -p 'Имя пользователя: ' USERNAME && read -p 'Пароль: ' PASSWORD && read -p 'Адрес сервера: ' SERVER_IP && echo -e '#!/usr/bin/env bash\nUSERNAME=user\nPASSWORD=pass\nSERVER_IP=server\nrdesktop -z -P -g 1280x900 -u $USERNAME -p $PASSWORD $SERVER_IP' > /home/$(whoami)/Рабочий\ стол/$(echo $SERVER_IP).connection && sed -i "s|user|$USERNAME|" /home/$(whoami)/Рабочий\ стол/$(echo $SERVER_IP).connection && sed -i "s|pass|$PASSWORD|" /home/$(whoami)/Рабочий\ стол/$(echo $SERVER_IP).connection && sed -i "s|server|$SERVER_IP|" /home/$(whoami)/Рабочий\ стол/$(echo $SERVER_IP).connection && chmod +x /home/$(whoami)/Рабочий\ стол/$(echo $SERVER_IP).connection

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
    echo -e "username=adm\npassword=1\ndomain=SAMBA" > /root/.finereader
    chmod 400 /root/.finereader
    echo "//10.13.62.1/finereader /mnt/finereader cifs credentials=/root/.finereader,vers=1.0,iocharset=utf8,file_mode=0777,dir_mode=0777 0 0" >> /etc/fstab
    mount -a
    exit

Создаём ссылку на рабочем столе пользователя (запускать под пользователем)  

    ln -s /mnt/finereader /home/`whoami`/Рабочий\ стол/Преобразовать\ в\ Word

Монтирование при входе пользователя  

    echo "mount -a &" >> /etc/gdm/PreSession/Default  



Сетевой каталог Школа
    
 `su root`

    dnf install nfs-utils -y
    mkdir -p /mnt/nfs_share
    chmod 777 /mnt/nfs_share
    echo "10.189.0.153:/home/user/share /mnt/nfs_share nfs defaults 0 0" >> /etc/fstab
    mount -a
    exit
    
Под пользователем:  

    ln -s /mnt/nfs_share /home/`whoami`/Рабочий\ стол/Общая\ папка



## SSH <a name="ssh"></a>
На сервере (локально) запускаем SSHD:  
`su root`  
`systemctl enable --now sshd`

На клиенте (то есть на своей машине) генерируем ключи (один раз!) и копируем их на сервер:  
`ssh-keygen -t rsa`  
`ssh-copy-id -i ~/.ssh/id_rsa.pub user@server`

Логинимся на сервер `ssh user@server` (пароль не запрашивается) и отключаем парольную аутентификацию:  

    sudo sed -i 's!#PasswordAuthentication yes!PasswordAuthentication no!g' /etc/ssh/sshd_config
    sudo systemctl restart sshd  


## Простой способ печати с РедОС на принтер в винде <a name="printing"></a>  
#### Windows  
_Включение или отключение компонентов Windows_ > _Службы печати и документов_ > _Служба печати LPD_  
Перезагружаемся, расшариваем принтер как обычно (Имя принтера не должно содержать пробелов и тому подобное т.е. должно быть что то вроде "HP1020")  
#### RedOS  
_Администрирование_ > _Настройки принтера_ > _Добавить_  
_Сетевой принтер_ > _Хост или принтер LPD/LPR_  
В строке Cервер прописываем "_IP или имя машины/название принтера_". Далее устанавливаем драйвер и все.  


## Проверка диска на ошибки <a name="fsck"></a>  
`fsck -y /dev/mapper/ro_redos-root`


## Двухфакторная аутентификация  <a name="2fa"></a>
#### С использованием USB-флешки  
Установить пакет  
`sudo dnf install pam_usb`  
  
Добавить флешку для использования в качестве токена:   
`sudo pamusb-conf --add-device flash`
  
Добавить пользователя:  
`sudo pamusb-conf --add-user=$(whoami)`
  
В файлах /etc/pam.d/system-auth и /etc/pam.d/password-auth нужно в начало файла добавить строку   
`auth required pam_usb.so`  

[Статья](https://redos.red-soft.ru/base/manual/safe-redos/pam-usb/?sphrase_id=290649) по настройке на сайте РедОС  


#### С использованием приложений на телефоне  
Устанавливаем на телефон Google Authenticator  
Устанавливаем пакет   
`sudo dnf install google-authenticator`  

В файлах /etc/pam.d/system-auth и /etc/pam.d/password-auth нужно в начало файла добавить строку   
`auth required pam_google_authenticator.so`  
  
В терминале запускаем `google-authenticator`, на все вопросы отвечаем Y  
Сканируем QR-код приложением на телефоне, в ответ будет выведен код. Вводим этот код в терминал на компе (Enter code from app)  
  
  
## Установка сканера по умолчанию<a name="scanner"></a>  
В терминале набрать `scanimage -L` и найти там нужный сканер  
У меня сканер выглядит так: device \`airscan:e0:Lexmark MX417de' is a eSCL Lexmark MX417de ip=10.13.64.144  
Команда для запуска будет выглядить так: `simple-scan 'airscan:e0:Lexmark MX417de'` (обращайте внимание на кавычки)  
Если всё нормально, создаём кнопку запуска на рабочем столе с данной командой  


## Восстановление шрифта в терминале<a name="termfonts"></a>  
`fc-cache -frv`  





