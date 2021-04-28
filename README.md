#### Pidgin
https://www.pidgin.im/plugins/?publisher=all&query=&type=  
Полезные модули для pidgin  
Установка пакетов для разработки:  
`yum groupinstall "Development tools"`  
Пакеты для pidgin:  
`sudo yum install -y pidgin-dev glib2-devel libcurl-devel webkitgtk-devel`

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
