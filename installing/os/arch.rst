
Arch Linux
--------------------

Zuerst installieren wir unseren Basis-Software-Stack. Bitte verwende zuerst `pacman -Syu`, um mit den Repositories zu synchronisieren und alle anderen Pakete auf den neuesten Stand zu bringen.

.. code:: bash

	$ sudo pacman -S git nodejs redis imagemagick


Falls du MongoDB, LevelDB oder eine andere Datenbank-Software anstelle von Redis benutzen möchtest, wirf einen Blick auf die Sektion :doc:`Datenbanken konfigurieren <../../configuring/databases>`.

Als nächstes, klone dieses Repository:


.. code:: bash

	$ git clone git://github.com/NodeBB/NodeBB.git nodebb


Ziehe dir alle von NodeBB benötigten Abhängigkeiten:

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
