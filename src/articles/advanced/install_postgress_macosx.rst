Installing PostgreSQL on Mac OSX 10.8
#####################################

:date: 2013-01-16 14:00
:slug: installing-postgresql-macosx
:summary: Installing PostgreSQL on OSX 10.8

Description
-----------

PostgreSQL_ is a powerful open source relational database system. PostgreSQL_ is the database system we will use in this class. These are the steps I took to get PostgreSQL_ running on a default of OSX 10.8. These instructions should also work for OSX 10.7 with a little modification. If you are running a different version of MacOS you should be able to adapt these instructions for you version. 

Install Command Line Utilities
------------------------------

Before we can start installing software on our Macintosh's we need to install the Linux tools required.

Open Safari and download `Command Line tools for XCode`_ This package installs the command line compilers and libraries needed in this class.

You will need to register at the developer site but registration is free. After you have downloaded the `Command Line tools for XCode`_ locate the file and double click on the .dmg that you downloaded. Next double click on the installer and proceed with the install. 

Install Homebrew
----------------

Homebrew_ is a mac utility that allows you to download and compile many command line utilities. It uses formulas to make the process as painless as possible. Open up terminal and type the following.

.. code-block:: console

	ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"

One the install is complete you will need to make sure everything got installed correctly.

.. code-block:: console

	brew doctor

The brew doctor command will check to make sure your system is ready to use homebrew_ Resolve any errors that you receive and run the command again. Once your system is ready you will see. 

.. code-block:: console

	brew doctor
	Your system is raring to brew.

Install PostgreSQL
------------------

The great part of installing homebrew_ is that the next steps get easier. Lets now install PostgreSQL_. In the terminal type:

.. code-block:: console

	brew install postgresql

After the install completes we will need to do a couple of simple configurations. First we are going to initialize the database system.

.. code-block:: console
	
	initdb /usr/local/var/postgres

After the database has initialized next we want to tell our Macintosh to restart postgresql_ when we restart our computer. These commands get typed on the console.

.. code-block:: console

	mkdir -p ~/Library/LaunchAgents
	ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
	launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist

You should be ready to use PostgreSQL_. The next step is to make sure our install worked and you can actually create databases.

.. code-block:: console

	createdb mytestdb
	psql mytestdb

If everything went well you should now be logged in to your newly created database.

.. code-block:: console

	psql (9.1.7)
	Type "help" for help.

	mytestdb=#

Type \q to exit

.. code-block:: console

	psql (9.1.7)
	Type "help" for help.

	mytestdb=# \q


Installing Psycopg2
-------------------

Next we need to install the python_ bindings for PostgreSQL. SQLAlchemy requires that we use the Psycopg library. Open back up your terminal and type the following

.. code-block:: console
	
	pip install psycopg2

If you did not install python from homebrew you will need to type

.. code-block:: console
	
	pip install psycopg2

Lets check our work and make sure that Psycopg_ installed correctly. 

.. code-block:: python
	
	python
	import psycopg2

If you are returned to the >>> prompt than everything went fine. 

Installing SQLAlchemy
---------------------

The last piece we need to install is SQLAlchemy_. 

.. code-block:: console

	pip install sqlalchemy

Again if you are not using python from homebrew_ you will need to use sudo at the begining of the line.

Again lets check our work and make sure SQLAlchemy installed correctly.

.. code-block:: python
	
	python
	import sqlalchemy

.. _python: http://www.python.org
.. _`Command Line Tools for XCode`: https://developer.apple.com/downloads/index.action
.. _PostgreSQL: http://postgresql.org
.. _Homebrew: http://mxcl.github.com/homebrew/
.. _Psycopg: http://initd.org/psycopg/
.. _SQLAlchemy: http://www.sqlalchemy.org/

