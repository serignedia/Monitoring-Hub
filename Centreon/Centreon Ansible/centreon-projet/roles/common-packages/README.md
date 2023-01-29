Role Name : common-packages
=========

Déploie les prérequis (dépendances) nécessaires à l'installation de centreon (central, database et poller).
Install les paquets suivants : epel release, software collection, ect.

Requirements
------------

Si vous avez les dépots locaux : renseigner les dans (group_vars/all.yml) puis décommenter la ligne include: add_repo.yml dans main.yml

Role Variables
--------------


Dependencies
------------


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: common-packages }

License
-------

BSD

Author Information
------------------


