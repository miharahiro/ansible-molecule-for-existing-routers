=============================================
molecule test against existing routers
=============================================

Requirements
================

- The following software are ready on the ansible host.

  -- ansible

  -- paramiko

  -- molecule

- Name resolution of routers

::

   $ cat roles/cisco-setup/molecule/default/molecule.yml  
   ---
   .
   .
   platforms:
     - name: R1
       groups:
         - cisco
   
::

   $ cat inventories/staging/hosts 
   [cisco]
   R1

::

   $ cat /etc/hosts
   .
   .
   192.168.122.101	      r1

- ssh user and password settings

::

   $ cat inventories/staging/group_vars/cisco.yml 
   ansible_connection: network_cli
   ansible_network_os: ios
   ansible_user: xxx
   ansible_password: xxx
   ansible_ssh_password: xxx
   
   

Setup procedures on ansible host
=====================================

RHEL8.1
------------

Install ansible, paramiko
::

   sudo dnf update
   sudo dnf install python3
   sudo dnf install python3-pip

   sudo subscription-manager repos --enable ansible-2-for-rhel-8-x86_64-rpms
   sudo dnf -y install ansible

   pip3 install paramiko

Install molecule
::
   
   dnf install  -y gcc python3-pip python3-devel openssl-devel libselinux-python3
   pip3 install setuptools -U
   pip3 install molecule


molecule test
===========================

::

   $ pwd
   /ansible-molecule-for-existing-routers/roles/cisco-setup

   $ molecule test
   --> Validating schema /home/mihara/gitrepos/ansible-molecule-for-existing-routers/roles/cisco-setup/molecule/default/molecule.yml.
   Validation completed successfully.
   --> Test matrix
       
   └── default
       ├── lint
       ├── dependency
       ├── cleanup
       ├── destroy
       ├── syntax
       ├── create
       ├── prepare
       ├── converge
       ├── idempotence
       ├── side_effect
       ├── verify
       ├── cleanup
       └── destroy
   .
   .
