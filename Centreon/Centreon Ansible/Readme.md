# Installation de Centreon avec Ansible

Le but de ce projet est de faciliter la prise en main de centreon avec l'automatisation de toutes les taches d'installation. Cela permet de faciliter les montées de version, les mises à jour, l'ajout de fonctionnalités ainsi que l'application des fixes de bug. 

Cette documentation a été réalisée selon les paramètres suivants :

1. *Versions*

- Centreon 21.04
- MariaDB 10.x
- CentOS 7.4

2. Prérequis :

- Avoir des connaissances de base sur Centreon
- Savoir Utiliser ansible
- SSH et Python doivent être installés et configurés sur les serveurs (manager et nodes)
- Ansible doit être installé et configuré sur le manager
- La communication ssh entre le manager et les nodes doit être fonctionnelle

# Le projet
Dans ce projet nous avons créé un certain nombre de répertoires nous permettant de scinder les étapes d'installation et d'isoler les processus d'installation.  Ainsi nous avons : 
-	*centreon-projet* : répertoire principal du projet contenant :
    - *common_tasks* : pour la réalisation des tâches standards
    - _environnements_ : pour la séparation des environnements (production et dev).
    - _group_vars_ : contenant les variables
    - _roles_ : pour la définition des rôles utilisés pour l'installation de chaque serveur

Un certain nombre de fichiers appelés playbook utilisés pour exécuter les rôles.

# Détails des installations

Pour avoir le détail de l'installation, veuillez lire le fichier readme dans centreon-projet.

# Contributeurs

William DEDZOE

Joseph PHUNG

Serigne Saliou DIA
