#### Pidgin
Удаляем стандартный pidgin  
`sudo yum remove -y pidgin`  

Установка пакетов для разработки:  
`sudo yum groupinstall "Development tools"`  

Пакеты для компиляции pidgin:  
`sudo yum install -y pidgin-devel glib2-devel gtk2-devel gstreamer-devel gnutls-devel cyrus-sasl-devel`

`wget https://sourceforge.net/projects/pidgin/files/Pidgin/2.14.7/pidgin-2.14.7.tar.bz2`  
`tar -xvf pidgin-2.14.7.tar.bz2`  
`cd pidgin-2.14.7`  

`./configure --enable-gnutls --disable-screensaver --disable-gtkspell --disable-gevolution --disable-vv --disable-idn --disable-meanwhile --disable-avahi --disable-dbus --disable-tcl`  

`make -j5`  вместо 5 поставить количество потоков процессора  

`sudo make install`  
  
---
Дальше можно не смотреть  
##### скриншотер (сделать скриншот и отправить)  

    wget --inet4-only https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/pidgin-sendscreenshot/pidgin-sendscreenshot-0.8-3.tar.bz2
    tar -xvf pidgin-sendscreenshot-0.8-3.tar.bz2
    cd pidgin-sendscreenshot-0.8-3
    sed -i 's!#include <curl/types.h>!/* #include <curl/types.h> */!g' src/main.h
    ./configure --prefix=/usr/lib64
    make
    sudo make install

##### embeded video (поддержка видео в сообщениях)

    git clone https://github.com/stefanistrate/pidgin-embeddedvideo/
    cd pidgin-embeddedvideo  
    sed -i
    ./configure
    make
    sudo make install

##### birthday reminder (напоминалка о днях рождения)

    git clone https://github.com/kgraefe/pidgin-birthday-reminder
    cd pidgin-birthday-reminder
    ./autogen.sh
    ./configure --prefix=/usr/lib64 --libdir=/usr/lib64/
    make
    sudo make install
