
Debian
======

Die aktuelle Anleitung für Ubuntu ist nicht vollständig kompatibel zu Debian. Es gibt einige Abweichungen, speziell bei der Node.js-Installation und wie man die aktuellste Version von Redis installieren sollte.

Anforderungen
^^^^^^^^^^^^^
Für NodeBB muss folgende Software installiert sein:

* Node.js in der Version 0.10 oder aktueller
* Redis, Version 2.6 oder aktueller
* cURL muss vorhanden sein. Verwende einfach ``sudo apt-get install curl``, um es zu installieren.

Node.js-Installation
^^^^^^^^^^^^^^^^^^^^

Debian 7, Debian 6 und älter haben standardmäßig keine `nodejs`-Pakete an Bord. Dennoch gibt es mehrere Wege, um Node.js auf deiner Debian-Distribution zu installieren.

Wheezy Backport:
----------------

Diese Lösung funktioniert **NUR auf Debian 7**. Führe einfach folgende Befehle **als root** aus:

.. code:: bash

	$ echo "deb http://ftp.us.debian.org/debian wheezy-backports main" >> /etc/apt/sources.list
	$ apt-get update


Führe folgende Befehle aus, um Node.js und NPM zu installieren:

.. code:: bash

	$ apt-get install nodejs-legacy
	$ curl --insecure https://www.npmjs.org/install.sh | bash


Installiere danach eine Node.js-Version, die aktueller als Version 0.8 ist (Stand: 29.03.2014, Version 0.10.21)

Aus dem Quellcode erstellen:
----------------------------

Diese Lösung ist für Debian 6 (Squeeze) oder aktueller. Um Node.js zu installieren, führe folgende Befehle **als root** aus:

.. code:: bash

	$ sudo apt-get install python g++ make checkinstall
	$ src=$(mktemp -d) && cd $src
	$ wget -N http://nodejs.org/dist/node-latest.tar.gz
	$ tar xzvf node-latest.tar.gz && cd node-v*
	$ ./configure
	$ fakeroot checkinstall -y --install=no --pkgversion $(echo $(pwd) | sed -n -re's/.+node-v(.+)$/\1/p') make -j$(($(nproc)+1)) install
	$ sudo dpkg -i node_*


Beziehe die aktuellste Software über Dotdeb:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Dotdeb ist ein Repository, welches Pakete enthält, um deine Debian-Maschinen in leistungsstarke, stabile und aktuelle LAMP-Server zu verwandeln.

* Nginx,
* PHP 5.4 und 5.3 (nützliche PHP-Erweiterungen : APC, imagick, Pinba, xcache, Xdebug, XHpro, ...)
* MySQL 5.5,
* Percona Toolkit,
* Redis,
* Zabbix,
* Passenger,
* …

Dotdeb unterstützt:

* Debian 6.0 “Squeeze“ und 7 “Wheezy“
* die Architekturen amd64 und i386

Debian 7 (Wheezy):
------------------

Für die kompletten Dotdeb-Repositories:

.. code:: bash

	$ sudo echo 'deb http://packages.dotdeb.org wheezy all' >> /etc/apt/sources.list
	$ sudo echo 'deb-src http://packages.dotdeb.org wheezy all' >> /etc/apt/sources.list


Danach solltest du folgende GPC-Schüssel hinzufügen:

.. code:: bash

	$ wget http://www.dotdeb.org/dotdeb.gpg
	$ sudo apt-key add dotdeb.gpg


Aktualisiere deine Paketlisten:

.. code:: bash

	$ sudo apt-get update


Debian 6 (Squeeze)
------------------

Für die kompletten Dotdeb-Repositories:

.. code:: bash

	$ sudo echo 'deb http://packages.dotdeb.org squeeze all' >> /etc/apt/sources.list
	$ sudo echo 'deb-src http://packages.dotdeb.org squeeze all' >> /etc/apt/sources.list


Danach solltest du folgende GPC-Schüssel hinzufügen:

.. code:: bash

	$ wget http://www.dotdeb.org/dotdeb.gpg
	$ sudo apt-key add dotdeb.gpg


Aktualisiere deine Paketlisten:

.. code:: bash

	$ sudo apt-get update


NodeBB installieren
^^^^^^^^^^^^^^^^^^^

Nun haben wir Node.js installiert und sind bereit für Redis. Fühle folgenden Befehl aus, um den Basis-Software-Stack zu installieren:

.. code:: bash

	$ apt-get install redis-server imagemagick git


Als nächstes, klone dieses Repository:

.. code:: bash

	$ cd /path/to/nodebb/install/location
	$ git clone git://github.com/NodeBB/NodeBB.git nodebb

Lade dir alle von NodeBB benötigten Abhängigkeiten über NPM herunter:

.. code:: bash

	$ cd /path/to/nodebb/install/location/nodebb (or if you are on your install location directory run : cd nodebb)
	$ npm install

Installiere NodeBB, indem du die App mit dem setup-Flag startest:

.. code:: bash

	$ ./nodebb setup


1. `URL of this installation` ist entweder deine öffentliche IP-Adresse oder ein Domainname, welcher auf diese IP-Adresse zeigt.
    **Beispiel:** ``http://0.0.0.0`` oder ``http://beispiel.org``  

2. ``Port number of your NodeBB`` ist der Port, auf dem NodeBB horcht und über den deine Website erreichbar ist:  
    **Hinweis:** Falls du nicht nginx oder sonst etwas als Proxy nutzt, solltest du spätestens zur Veröffentlichung deiner Website Port 80 verwenden.
    
3. Wenn du den oben genannten Schritten gefolgt bist, um deinen Redis-Server aufzusetzen, dann musst du nur noch die Standard-Einstellungen für Redis verwenden.

Das Beste kommt zum Schluss: Lass uns dein NodeBB-Forum starten!

.. code:: bash

	$ ./nodebb start


**Hinweis:** Falls deine NodeBB-Instanz oder dein Server abstürzt, wird NodeBB nicht automatisch neu starten (verdammt!). Aus diesem Grund solltest du als alternativen Weg, NodeBB auszuführen, einen Blick auf Hilfsprogramme wie ``supervisor`` oder ``forever`` werfen: :doc:`Schau hier! <../../running/index>`

Extras, Tipps und Rat
^^^^^^^^^^^^^^^^^^^^^

Du solltest deine NodeBB-Installation absichern. Wie das geht, `kannst du hier nachlesen <https://github.com/NodeBB/NodeBB#securing-nodebb>`_.

Du solltest Nginx (oder ähnliche Software) als Reverse-Proxy für deine NodeBB-Installation auf Port 80 Nutzen. :doc:`Erfahre hier mehr darüber <../../configuring/proxies>`.

