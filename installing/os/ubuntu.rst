
Ubuntu
--------------------

Zuerst installieren wir unseren Basis-Software-Stack:

.. code:: bash

	$ sudo apt-get install git nodejs redis-server imagemagick npm


Falls du MongoDB, LevelDB oder eine andere Datenbank-Software anstelle von Redis benutzen möchtest, wirf einen Blick auf die Sektion :doc:`Datenbanken konfigurieren <../../configuring/databases>`.

**Falls dein Paket-Manager eine Version von Node.js installiert hat, die älter als Version 0.8 ist (z.B. Ubuntu 12.10, 13.04), dann verwende ``node --version``, um deine Version von Node.js festzustellen:**


.. code:: bash

	$ sudo add-apt-repository ppa:chris-lea/node.js
	$ sudo apt-get update && sudo apt-get dist-upgrade


Als nächstes, klone dieses Repository:


.. code:: bash

	$ git clone git://github.com/NodeBB/NodeBB.git nodebb


Lade dir alle von NodeBB benötigten Abhängigkeiten herunter:

.. code:: bash

    $ cd nodebb
    $ npm install


Initialisiere das Setup-Script, indem du die App mit dem ``setup``-Flag startest:


.. code:: bash

	$ ./nodebb setup


Die Standard-Einstellungen sind für lokale Server gedacht, die auf dem Standardport laufen und Redis auf derselben Maschine/Port verwenden.

Als letztes starten wir noch das Forum...


.. code:: bash

	$ ./nodebb start


NodeBB kann auch mit Hilfsprogrammen, wie ``supervisor`` und ``forever`` gestartet werden. :doc:`Schau dir die Möglichkeiten hier an <../../running/index>`.
