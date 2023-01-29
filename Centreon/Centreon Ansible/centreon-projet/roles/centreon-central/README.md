centreon-central
=========
Role pour déployer l'installation du serveur centreon central.

Prérequis
------------

IP configuré
Accès ssh pour le user centreon
Dépots accessible

roles:
        - common-packages
        - disable-selinux-firewalld

Role Variables
--------------

centreon_local_repo_id 

Dependencies
------------


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: centreon_poller
      become: true
      become_method: sudo

      roles:
        - role: centreon-poller

License
-------

BSD

Author Information
------------------


