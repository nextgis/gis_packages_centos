Порядок сборки пакетов
======================

1. Создаём пользователя, под которым будем осуществлять сборку:

        useradd rpmbuild
        su - rpmbuild
        cd

2. Создаём структуру каталогов для сборки:

        rpmdev-setuptree

3. В каталог SOURCE помещаем архив с исходным кодом (пример):

        wget http://download.osgeo.org/mapserver/mapserver-6.4.1.tar.gz 

4. В каталог SPECS помещаем spec-файл. Данный файл можно попробовать найти
   в Сети и адаптировать его под себя (наиболее трудозатратный этап):

        nano mapserver.spec

5. Переходим в каталог SPECS и запускаем сборку:

        rpmbuild -ba --target=x86_64 mapserver.spec

6. Проверяем, что пакет устанавливается корректно, для этого переходим в каталог RPMS/x86_64 и устанавливаем пакет:

        rpm -ivh mapserver-6.4.1-0.el6.x86_64.rpm

7. Готовые пакеты можно организовать в репозиторий, [подробнее](http://wiki.centos.org/HowTos/CreateLocalRepos)

Замечания
---------
        
* spec-файлы находятся внутри *.src.rpm
* При сборке использовалась библиотека Boost весрии 1.55 из репозитория [enetres](http://repo.enetres.net/). Данная библиотека использована при сборке Mapnik и CGAL (используется для pgRouting).
* При сборке использовался PostgreSQL 9.3 из [этого](http://yum.postgresql.org/9.3/redhat/rhel-6-x86_64/pgdg-centos93-9.3-1.noarch.rpm) репозитория, [подробнее](http://wiki.postgresql.org/wiki/YUM_Installation).
* При сборке использовался PostGIS 2.1, [подробнее](http://trac.osgeo.org/postgis/wiki/UsersWikiPostGIS21CentOS6pgdg)
* Все пакеты выложены в [репозиторий](http://nextgis.ru/programs/centos/), для его использования скопируйте в директорию */etc/yum.repos.d* файл [nextgis.repo](http://nextgis.ru/programs/centos/nextgis.repo). Теперь можно устанавливать пакеты, все зависимости подтянутся автоматически из доступных репозиториев.

Пример установки пакета:

    yum install mapnik-python