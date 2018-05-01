

.. _installation:

==================
Instalare PHPUnit
==================

.. _installation.requirements:

Cerinte
############

PHPUnit 7.0 necesita PHP 7.1; utilizarea ultimei versiuni de PHP este recomandata.


PHPUnit necesita extensiile `dom <http://php.net/manual/en/dom.setup.php>`_ si `json <http://php.net/manual/en/json.installation.php>`_
, care sunt activat implicit.

PHPUnit de asemenea, necesită extentiile
`pcre <http://php.net/manual/en/pcre.installation.php>`_,
`reflection <http://php.net/manual/en/reflection.installation.php>`_,
si `spl <http://php.net/manual/en/spl.installation.php>`_
. Aceste extensii standard sunt activate implicit si nu pot fi dezactivate fara modifica sursele PHP si/sau surselor C.


Raportul de acoperire cod necesita extensiile
`Xdebug <http://xdebug.org/>`_ (2.5.0 sau mai mare) si
`tokenizer <http://php.net/manual/en/tokenizer.installation.php>`_.
Generarea de rapoarte XML necesita extensia
`xmlwriter <http://php.net/manual/en/xmlwriter.installation.php>`_.

.. _installation.phar:

Arhiva PHP (PHAR)
##################

Cel mai usor mod de a obtine PHPUnit este de a descarca `PHP Archive (PHAR) <http://php.net/phar>`_ care are toate dependintele
(si cateva optionale) necesare intr-un singur fisier.

Extensia `phar <http://php.net/manual/en/phar.installation.php>`_
este necesara pentru a folosii arhive PHP (PHAR).

Daca extensia `Suhosin <http://suhosin.org/>`_ este activata trebuie sa persimeti executia fisierelor PHAR in fisierul
``php.ini``:

.. code-block:: bash

    suhosin.executor.include.whitelist = phar

Pentru a instala global PHAR:

.. code-block:: bash

    $  wget https://phar.phpunit.de/phpunit-7.0.phar
    $  chmod +x phpunit-7.0.phar
    $  sudo mv phpunit-7.0.phar /usr/local/bin/phpunit
    $  phpunit --version
    PHPUnit x.y.z by Sebastian Bergmann and contributors.

Puteti descarca fisierul PHAR direct:

.. code-block:: bash

    $  wget https://phar.phpunit.de/phpunit-7.0.phar
    $  php phpunit-7.0.phar --version
    PHPUnit x.y.z by Sebastian Bergmann and contributors.

.. _installation.phar.windows:

Windows
=======

Instalarea globala a PHAR implica aceasi pasi ca procedura manuala
`installing Composer on Windows <https://getcomposer.org/doc/00-intro.md#installation-windows>`_:

#.

   Creati un director pentru fisierele PHP; e.x. :file:`C:\\bin`

#.

   Adaugati C:\bin la calea ``PATH``
   din mediul de lucru
   (`sfaturi suplimentare <http://stackoverflow.com/questions/6318156/adding-python-path-on-windows-7>`_)

#.

   Descarcati `<https://phar.phpunit.de/phpunit-7.0.phar>`_ si
   salvati fisirul ca :file:`C:\\bin\\phpunit.phar`

#.

   Deschideti o linie de comanda (e.x.
   apasati :kbd:`Windows`:kbd:`R`
   » tastati cmd
   » :kbd:`ENTER`)

#.

   Creati un script batch (rezulta in
   :file:`C:\\bin\\phpunit.cmd`):

   .. code-block:: bash

       C:\Users\username>  cd C:\bin
       C:\bin>  echo @php "%~dp0phpunit.phar" %* > phpunit.cmd
       C:\bin>  exit

#.

   Deschideti o linie de comanda noua si confirmati executia PHPUnit
   din orice cale:

   .. code-block:: bash

       C:\Users\username>  phpunit --version
       PHPUnit x.y.z by Sebastian Bergmann and contributors.

Pentru interpretoarele de comanda Cygwin si/sau MingW32 (e.x. TortoiseGit),
 puteti trece peste pasul 5 de deasupra salvand fisierul ca
:file:`phpunit` (fara extensia :file:`.phar`)
si faceti-l executabil via
chmod 775 phpunit.

.. _installation.phar.verification:

Verificarea lansarilor PHPUnit PHAR
===============================

Toate lansarile de cod oficiale distribuite de Proiectul PHPUnit sunt
 semnate de release manager in parte. Semnaturile PGP si codurile
 hash SHA1 sunt disponibile pentru verificare la `phar.phpunit.de <https://phar.phpunit.de/>`_.

Urmatorul exemplu detaliaza cum functioneaza verificarea. Incepem prin
descarcarea :file:`phpunit.phar` precum si a
semnaturii PGP separat :file:`phpunit.phar.asc`:

.. code-block:: bash

    wget https://phar.phpunit.de/phpunit.phar
    wget https://phar.phpunit.de/phpunit.phar.asc

Vrem sa verificam arhiva PHP PHPUnit (:file:`phpunit.phar`)
impotriva semnaturii separate (:file:`phpunit.phar.asc`):

.. code-block:: bash

    gpg phpunit.phar.asc
    gpg: Signature made Sat 19 Jul 2014 01:28:02 PM CEST using RSA key ID 6372C20A
    gpg: Can't check signature: public key not found

Nu avem cheia publica a managerul de release (``6372C20A``)
in masina locala. Pentru a merge mai departe cu verificarea avem nevoie de
a obtine cheia publica a managerul de release de la server de chei. Un asemenea
server este  :file:`pgp.uni-mainz.de`. Serverele de chei sunt sincronizate impreuna
 asadar puteti sa va conectati si la alt server.

.. code-block:: bash

    gpg --keyserver pgp.uni-mainz.de --recv-keys 0x4AA394086372C20A
    gpg: requesting key 6372C20A from hkp server pgp.uni-mainz.de
    gpg: key 6372C20A: public key "Sebastian Bergmann <sb@sebastian-bergmann.de>" imported
    gpg: Total number processed: 1
    gpg:               imported: 1  (RSA: 1)

Acum avem cheia publica pentru o entitate cunoscuta ca "Sebastian
Bergmann <sb@sebastian-bergmann.de>". Totusi, nu avem cum sa verificam ca aceasta
cheie a fost creata de persoana cunoscuta ca Sebastian
Bergmann. Oricum, sa incercam sa verificam semnatura de release inca o data.

.. code-block:: bash

    gpg phpunit.phar.asc
    gpg: Signature made Sat 19 Jul 2014 01:28:02 PM CEST using RSA key ID 6372C20A
    gpg: Good signature from "Sebastian Bergmann <sb@sebastian-bergmann.de>"
    gpg:                 aka "Sebastian Bergmann <sebastian@php.net>"
    gpg:                 aka "Sebastian Bergmann <sebastian@thephp.cc>"
    gpg:                 aka "Sebastian Bergmann <sebastian@phpunit.de>"
    gpg:                 aka "Sebastian Bergmann <sebastian.bergmann@thephp.cc>"
    gpg:                 aka "[jpeg image of size 40635]"
    gpg: WARNING: This key is not certified with a trusted signature!
    gpg:          There is no indication that the signature belongs to the owner.
    Primary key fingerprint: D840 6D0D 8294 7747 2937  7831 4AA3 9408 6372 C20A

In momentul asta, semnatura este buna, dar nu avem incredere in aceasta cheie.
O semnatura buna inseamna ca fisierul nu a fost modificat. Totusi, datorita
naturii cheii publice trebuie sa verificati cheia ``6372C20A`` ca a fost creata
de adevaratul Sebastian Bergmann.

Orice atacator poate crea o cheie publica si sa o puna pe serverele de chei publice.
Pot crea un release malicios semnat de aceasta cheie falsa. Daca verificati
semnatura falsa cu realeaseul corupt o sa aiba succes pentru ca acea cheie nu este cea reala.
Prin urmare trebuie sa validati authenticitatea acestei chei. Validarea autenticitatii cheii
publice, totusi este in afara scopului acestui document.

Poate fi o abordare prudenta in crearea un script ce administreaza instalarea PHPUnit si
verifica semnatura GnuPG inainte de a rula suita de teste. De exemplu:

.. code-block:: bash

    #!/usr/bin/env bash
    clean=1 # Delete phpunit.phar after the tests are complete?
    aftercmd="php phpunit.phar --bootstrap bootstrap.php src/tests"
    gpg --fingerprint D8406D0D82947747293778314AA394086372C20A
    if [ $? -ne 0 ]; then
        echo -e "\033[33mDownloading PGP Public Key...\033[0m"
        gpg --recv-keys D8406D0D82947747293778314AA394086372C20A
        # Sebastian Bergmann <sb@sebastian-bergmann.de>
        gpg --fingerprint D8406D0D82947747293778314AA394086372C20A
        if [ $? -ne 0 ]; then
            echo -e "\033[31mCould not download PGP public key for verification\033[0m"
            exit
        fi
    fi

    if [ "$clean" -eq 1 ]; then
        # Let's clean them up, if they exist
        if [ -f phpunit.phar ]; then
            rm -f phpunit.phar
        fi
        if [ -f phpunit.phar.asc ]; then
            rm -f phpunit.phar.asc
        fi
    fi

    # Let's grab the latest release and its signature
    if [ ! -f phpunit.phar ]; then
        wget https://phar.phpunit.de/phpunit.phar
    fi
    if [ ! -f phpunit.phar.asc ]; then
        wget https://phar.phpunit.de/phpunit.phar.asc
    fi

    # Verify before running
    gpg --verify phpunit.phar.asc phpunit.phar
    if [ $? -eq 0 ]; then
        echo
        echo -e "\033[33mBegin Unit Testing\033[0m"
        # Run the testing suite
        `$after_cmd`
        # Cleanup
        if [ "$clean" -eq 1 ]; then
            echo -e "\033[32mCleaning Up!\033[0m"
            rm -f phpunit.phar
            rm -f phpunit.phar.asc
        fi
    else
        echo
        chmod -x phpunit.phar
        mv phpunit.phar /tmp/bad-phpunit.phar
        mv phpunit.phar.asc /tmp/bad-phpunit.phar.asc
        echo -e "\033[31mSignature did not match! PHPUnit has been moved to /tmp/bad-phpunit.phar\033[0m"
        exit 1
    fi

.. _installation.composer:

Composer
########

Simplu adaugati (in timpul dezvoltarii) o dependinta la
``phpunit/phpunit`` in fisierul
``composer.json`` din proiectul dumneavoastra daca folositi `Composer <https://getcomposer.org/>`_ pentru a administra dependintetele din proiect:

.. code-block:: bash

    composer require --dev phpunit/phpunit ^7.0

.. _installation.optional-packages:

Pachete optionale
#################

Urmatoarele pachete optionale sunt disponibile:

``PHP_Invoker``

    Clasa utilitara pentru a invoca apelabilele cu o pauza. Acest pachet este necesar pentru a impune pauzele din teste in mod strict.

    Acest pachet este inclus in distributia PHAR a lui PHPUnit. Poate fi instalat prin Composer cu urmatoarea comanda:

    .. code-block:: bash

        composer require --dev phpunit/php-invoker

``DbUnit``

    Portare DbUnit pentru PHP/PHPUnit pentru a suporta interactiunea cu baza de date in teste.

    Acest pachet nu este inclus in distributia PHAR a lui PHPUnit.
    Poate fi instalat prin Composer cu urmatoarea comanda:

    .. code-block:: bash

        composer require --dev phpunit/dbunit


