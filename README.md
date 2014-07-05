Порядок сборки пакетов
======================

1. Создаём пользователя, под которым будем осуществлять сборку:

        useradd rpmbuild
        su - rpmbuild
        cd

2. Создаём структуру каталогов для сборки:

        rpmdev-setuptree

3. В каталог SOURCE помещаем архив с исходным кодом (пример):

        wget wget http://download.osgeo.org/mapserver/mapserver-6.4.1.tar.gz 

4. В каталог SPECS помещаем spec-файл. Данный файл можно попробовать найти
   в Сети и адаптировать его под себя (наиболее трудозатратный этап):

        nano mapserver.spec

5. Переходим в каталог SPECS и запускаем сборку:

        rpmbuild -ba --target=x86_64 mapserver.spec

6. Переходим в каталог RPMS/x86_64 и устанавливаем пакет:

        rpm -ivh mapserver-6.4.1-0.el6.x86_64.rpm