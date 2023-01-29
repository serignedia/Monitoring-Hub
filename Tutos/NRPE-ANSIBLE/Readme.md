# Prérequis

1. Ansible doit être installé sur le manager
2. Les accès ssh depuis le manager vers les nodes doivent être opérationnels
3. Savoir utiliser Ansible
4. Télécharger le répertoire pour avoir accès au projet

Rôle
--------------

- centreon-nrpe-client-install : pour le déploiement de NRPE vers les machines distantes

Dépendances
------------

Remplir le fichier inventory (hosts) avec la liste des machines sur lesquelles vous souhaitez déployer NRPE.

A faire Avant de jouer les playbooks
------------
1. Fichier centreon-nrpe-supervision/files/configs/centreon_nrpe3.cfg

Modifier puis ajouter l'adresse IP de votre serveur de supervision au niveau de la ligne 

        allowed_hosts=IP_SERVEUR_DE_SUP
        
2. Scripts personnalisés

Si vous avez des scripts personnalisés, ajouter les dans le répertoire centreon-nrpe-supervision/files/scripts/scripts_centreon puis ajouter dans centreon_nrpe3.cfg dans la section ### SCRIPTS PERSONNALISES ### les lignes pour chaque script comme dans l'exemple :

        command[nom_commande]=/usr/lib/centreon/plugins/nom_script

3. Les packages nrpe se trouvent dans centreon-nrpe-supervision/files/packages/rpms, vous pouvez télécharger les dernières versions depuis les dépots centreon puis les remplacer.

Playbook
----------------
1. La commande ansible pour déployer NRPE sur les machines distantes est :
    
        ansible-playbook -i hosts install-centreon-nrpe-clients.yml -u user --ask-pass

Saisir ensuite votre mot de passe.

2. La commande ansible pour déployer les scripts est :

        ansible-playbook -i hosts deploy-nrpe-scripts.yml -u user --ask-pass

Saisir ensuite votre mot de passe.
