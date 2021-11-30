# RedOS - настройки после установки  
*Версия redos 7.3*

-----  

Обновление системы  

    sudo dnf update -y

Убираем сообщение при входе в систему  

    sudo sed -i 's!/usr/bin/zenity --warning!#/usr/bin/zenity --warning!' /etc/gdm/PreSession/Default

Отключаем selinux  

    sudo sed -i 's/SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config


Вводим компьютер в домен (изменить под себя: -d имя_домена -n имя_компьютера -u админ_домена -p пароль_админа_домена). Проверить дату время перед подключением!

    sudo /usr/bin/join-to-domain.sh -d uk.lbt -n computer_name -u Administrator -p password -y

#### Pidgin

    sudo yum remove -y pidgin
    sudo yum groupinstall -y "Development tools"
    sudo yum install -y pidgin-devel glib2-devel gtk2-devel gstreamer-devel gnutls-devel cyrus-sasl-devel libcurl-devel libpurple-devel
    cd ~
    wget https://sourceforge.net/projects/pidgin/files/latest/download -O pidgin-source.tar.bz2
    tar -xvf pidgin-source.tar.bz2
    cd pidgin-source
    ./configure --enable-gnutls=yes --disable-screensaver --disable-gtkspell --disable-gevolution --disable-vv --disable-idn --disable-meanwhile --disable-avahi --disable-dbus --disable-tcl
    make -j5
    sudo make install

---
Дальше можно не смотреть  
##### скриншотер (сделать скриншот и отправить)  
https://code.google.com/archive/p/pidgin-sendscreenshot/)

    cd ~
    wget --inet4-only https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/pidgin-sendscreenshot/pidgin-sendscreenshot-0.8-3.tar.bz2
    tar -xvf pidgin-sendscreenshot-0.8-3.tar.bz2
    cd pidgin-sendscreenshot-0.8-3
    sed -i 's!#include <curl/types.h>!/* #include <curl/types.h> */!g' src/main.h
    ./configure
    make -j5
    sudo make install

##### embeded video (поддержка видео в сообщениях)  
https://github.com/stefanistrate/pidgin-embeddedvideo  

    cd ~
    git clone https://github.com/stefanistrate/pidgin-embeddedvideo/
    cd pidgin-embeddedvideo  
    ./configure
    make -j5
    sudo make install

##### birthday reminder (напоминалка о днях рождения)  
https://github.com/kgraefe/pidgin-birthday-reminder  

    cd ~
    git clone https://github.com/kgraefe/pidgin-birthday-reminder
    cd pidgin-birthday-reminder
    ./autogen.sh
    ./configure --prefix=/usr/lib64 --libdir=/usr/lib64/
    make -j5
    sudo make install
