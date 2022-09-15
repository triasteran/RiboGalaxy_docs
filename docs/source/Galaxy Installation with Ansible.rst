Galaxy Installation with Ansible
=====

.. _Base:

Basic components and useful commands
------------

The first step is installation of the Galaxy web server, client and database. All the steps are described in this tutorial: 
`Ansible-Galaxy <https://training.galaxyproject.org/archive/2021-08-01/topics/admin/tutorials/ansible-galaxy/tutorial.html?utm_source=smorgasbord&utm_medium=website&utm_campaign=gcc2021>`_. Galaxy is configured that way that whenever you start your VM, it automatically starts a galaxy server. 

Some key features of installation: 
* Current commit that is used in RiboGalaxy version is 'release_21.09' (to avoid issues with installing library 'future')
* All of the code, configuration, tools, and mutable-data (like caches, location files, etc.) folders will live by default beneath galaxy_root, which is in /mnt/data. 
* auto-magic restart of Galaxy is implemented via systemd. 
* uWSGI Mules are used to handle processing Galaxy jobs. With Mules, uWSGI launches as many as you request, and then they take turns placing a lock, accepting a job, releasing that lock, and then going on to process that job.
* during PostgreSQL installation, a new user 'galaxy' (matching the system user under which Galaxy will be running) is created. It can be used for accessing the database (e.g. for gathering info about usage and cleaning): 

.. code-block:: console

   $ sudo -iu galaxy 
  

* The main configuration file lives in /srv/galaxy/config/galaxy.yml. 
* Useful commands to check startus and restart Galaxy: 

.. code-block:: console

   $ sudo systemctl status galaxy
   $ sudo systemctl restart galaxy

   
* To check galaxy logs: 
 
.. code-block:: console

   $ sudo journalctl -fu galaxy
 
* if there are issues with sudo again when client is built: 

.. code-block:: console

   $ sudo visudo
   append this line to the file: admin ALL=(ALL) NOPASSWD:ALL 








