##################
frame
##################

Frame is a boilerplate django project with `django CMS <http://django-cms.org>`_
already installed, along side some other useful apps.

This setup is somewhat personalized for my need, feel free to suggest changes.

You will need to have some dependencies installed globally:

``sudo apt-get install libmysqlclient-dev libtiff5-dev libjpeg8-dev zlib1g-dev 
libfreetype6-dev liblcms2-dev libwebp-dev tcl8.6-dev tk8.6-dev python-tk`` 

============
Known Errors
============

1. mysql-python fails with during install    E: ``EnvironmentError: mysql_config not found``

                  Solution: ``sudo apt-get install libmysqlclient-dev``
      
2. MySQL-python fails during build           E: ``failed with error code 1``
                  
                  Solution: ``sudo apt-get build-dep python-mysqldb``  

3. Pillow fails during build                 E: ``failed with error code 1``

                  Solution: ``sudo apt-get install libtiff5-dev libjpeg8-dev zlib1g-dev \
                  libfreetype6-dev liblcms2-dev libwebp-dev tcl8.6-dev tk8.6-dev python-tk`` 


4. Linux Mint 17.3 - make dev-setup fails    E: ``You must put some 'source' URIs in your sources.list``

                  Solution: ``Go to Software Sources and enable source code repositories.``
                  
                  Same error on Raspberry Pi
                  
                  Solution: ``sudo nano /etc/apt/sources.list & add this line to enable apt-get source: 
                  deb-src http://archive.raspbian.org/raspbian/ jessie main contrib non-free rpi``

==========
Quickstart
==========

To setup a new dev project, inside **virtualenv** run ``make dev-setup``.

This will create a ``local.py`` settings file if it doesn't exist already,
install the requirements for a dev envirionment, and create (migrate) the database
(default one being ``dev.db`` in your project root).

To start the local server, or open a shell use ``make runs`` and ``make shell``.

You can checkout the `Makefile <https://github.com/dinoperovic/djangocms-skeletor/blob/master/Makefile>`_ for some other usefull commands.


====
Apps
====

Your apps should live in ``project/apps`` directory.

========
Frontend
========

This project comes with some basic frontend setup.
You get a ``base.html`` master template, and a ``default.html`` template for CMS pages.

As an option – `SASS <http://sass-lang.com/>`_ css preprocessor is ready to use, simply run ``make sass-watch`` in a separate terminal window to start watching your sass directory.


====================
Internationalization
====================

To use django's internationalization follow this steps in your terminal (from your project root):

.. code:: shell

    cd project
    mkdir locale
    django-admin makemessages -l <lang>

You can then run ``make messages`` from your project root to update.
The ``project/locale`` directory is in the ``.gitignore`` file, so you'll have to
create it separately on your production server.

To translate your project on the web, you can use already setup `djagno-rosetta <https://github.com/mbi/django-rosetta>`_.
Just navigate to ``http://localhost:8000/translate/``


=====
Tests
=====

`django-nose <https://github.com/django-nose/django-nose>`_ is used as a default test runner.
To run the tests first run ``make reqs/test`` to install the test requirements.
Then you can use the ``make test`` command to run the tests.

Additionally you can use ``make lint`` to check for lint errors.
`flake8 <https://flake8.readthedocs.org/en/2.3.0/>`_ is used as default linter.


==========
Deployment
==========

If you want to use **make** for deploying your project, you can run ``make deploy``
on your server.
There is also a ``make restart`` command you can use to restart your server.


=======
Credits
=======

This project base setup idea is based on `djangocms-skeletor <https://github.com/dinoperovic/djangocms-skeletor>`_.
