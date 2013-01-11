Installing PostgreSQL on Ubuntu 12.04
#####################################

:date: 2013-01-10 14:00
:slug: installing-postgresql-ubuntu
:summary: Installing PostgreSQL on Ubuntu 12.04

Description
-----------

PostgreSQL_ is a powerful open source relational database system. PostgreSQL_ is the database system we will use in this class. These are the steps I took to get PostgreSQL_ running on a default of Ubuntu_ 12.04. These instructions should also work for Ubuntu 12.10. If you are running a different version of Linux you should be able to adapt these instructions for you distribution. 

Installing PostgreSQL
---------------------

The first step to installing anything new is to make sure that your system has all the latest security patches. Open your terminal and run the following commands.

.. code-block:: console

	sudo apt-get update
	sudo apt-get upgrade --show-upgraded

Next we are actually going to install PostgreSQL_. This will install PostgreSQL server, PostgreSQL client and a few modules that makes working with PostgreSQL easier. 

.. code-block:: console

	sudo apt-get install postgresql postgresql-contrib

Configuring Security
--------------------

By default PostgreSQL_ creates a system user and only allows that user to connect to the database server. If we were deploying live we might select a different security method, but since this is for local development we are going add our personal username to the list of allowed users. You should replace my username kellan with your own username.

.. code-block:: console

	sudo -u postgres createuser
	Enter name of role to add: kellan
	Shall the new role be a superuser? (y/n) y

We gave the user superuser privileges while we are in development to make working easier. This would not be a good practice in deployment. 

Creating a Database
-------------------

Now that you have given yourself permissions you should be ready to use PostgreSQL_. The next step is to make sure our install worked and you can actually create databases.

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
	
	sudo apt-get install python-psycopg2

Lets check our work and make sure that Psycopg_ installed correctly. 

.. code-block:: python
	
	python
	import psycopg2

If you are returned to the >>> prompt than everything went fine. 

Installing SQLAlchemy
---------------------

The last piece we need to install is SQLAlchemy_. We need to install python development package and python-setuptools. We are adding build-essential because it setups the basics we need to do development on ubuntu. Several packages that we will use in this class will be easier to install if we install this now. 

.. code-block:: console

	sudo apt-get install python-dev python-setuptools build-essential
	sudo easy_install sqlalchemy

Again lets check our work and make sure SQLAlchemy installed correctly.

.. code-block:: python
	
	python
	import sqlalchemy

.. _python: http://www.python.org
.. _PostgreSQL: http://postgresql.org
.. _Ubuntu: http://www.ubuntu.com
.. _Psycopg: http://initd.org/psycopg/
.. _SQLAlchemy: http://www.sqlalchemy.org/

