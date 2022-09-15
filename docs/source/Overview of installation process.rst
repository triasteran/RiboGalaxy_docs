Overview of installation process
=====

.. _hardware:

Hardware
------------

We will need 1 clean VM (Virtual Machines), we call it Galaxy machine. We used the CloudCIX platform (<https://www.cloudcix.com/>`_).  It is a simplest setup, so everything will be carried out and stored on one machine - web server, database and jobs running. This setup was chosen due to simplicity of configuration, debugging and availability of resources.  

This is not the only possible setup, e.g. cluster can be used for running jobs, or one or multiple ‘pulsar’ machines (‘pulsar’ is a separate remote machine used solely for running jobs). 

We need several ports to be exposed, including 22 (SSH),  80 (HTTP), 443 (SSL, HTTPs). 
The Galaxy machine should have a domain name, because we are going to use SSL certs. 


Basic packages for clean VM
----------------
Once we have a clean machine where we host RiboGalaxy server, we need to add a `"sudo user"` and install some basic packages. 

.. code-block:: console

   $ sudo adduser user 
   $ compgen -u # check that user user is made 
   $ sudo usermod -aG sudo alla 
   $ Exit
   
   $ sudo apt-get update && sudo apt-get upgrade 
   $ sudo apt-get -y install vim git default-jre unzip tar nano pip build-essentials gcc-multilib libncurses-dev tmux htop curl ncdu
   $ sudo apt-get install acl 
   $ sudo apt install mlocate 
   
   $ sudo apt update
   $ sudo apt install software-properties-common
   $ sudo apt-add-repository --yes --update ppa:ansible/ansible
   $ sudo apt install ansible
   $ sudo apt install tree  
   
   
Then we need to check that we have Ansible >= 2.7 and Python > 3.6. 


`"test param"``

Main components of infrastructure
----------------

database, server, ...
