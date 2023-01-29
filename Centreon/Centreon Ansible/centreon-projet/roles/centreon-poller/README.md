centreon-poller
=========

Pour déployer l'installation d'un poller centreon.

Prérequis
------------
Centreon centreon doit être installé.
Les Dépots doivent être accessibles.

Role Variables
--------------

centreon_local_repo_id

Le fqdn doit être configuré, sinon renseigné le fichier etc hosts.

Le numéro id de l'interface réseau du poller doit être renseigné dans le fichier main du répertoire defaults

Dependances
------------

 roles:
    - common-packages
    - disable-selinux-firewalld

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: centreon_poller
      roles:
         - { role: centreon-poller }

License
-------

BSD

Author Information
------------------

