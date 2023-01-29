# I. Prérequis

  Installer Ansible sur votre manager : dans notre cas nous allons l'installer sur CentOS 7.
  
    yum install epel-release
    yum install ansible
    
  Installer la collection community crypto
    
    ansible-galaxy collection install community.crypto
    
  Télécharger ensuite le projet : centreon-projet.zip
  Dézipper ensuite le projet
  
    unzip centreon-projet.zip

# II. Mise à jour des variables :

# 1. Répertoire group_vars

  - fichier : **all.yml**

    Positionner les valeurs des variables suivantes :
    
        /* Identifiants Ansible*/
        ansible_ssh_user: root_user
        ansible_ssh_pass: root_pass

        /* Identifiants du user root mysql */
        mysql_root_password
        mysql_root_central_password
        
        /* Identifiants du user admin centreon */
        centreon_central_admin_user
        centreon_central_admin_password

        /* IP du serveur centreon central */
        centreon_central_ip_adress

        /* Url des dépôts */
        centreon_local_repo_dir
        requirement_local_repo_dir

  **Gestion des LVM et des Filesystem**
  
  - fichiers : **centreon_central, centreon_poller et centreon_sgbd**
  
   Si vous êtes dans un environnement de production, vous aurez peut-être besoin de gérer les volumes logiques et les filesystèmes avant l'installation de centreon. Pour chaque serveur, selon votre architecture, positionner les valeurs de la taille des volumes logiques et FS en fonction de votre configuration.
    
# 2. Répertoire environnements

Ce répertoire sert à séparer les environnements de production, de qualification ou de développement afin de pouvoir positionner les variables en fonction de l'environnement. Dans la suite nous allons nous concentrer que sur l'environnement de production.

  - *Répertoire prod*
    - fichier *hosts* : il s'agit du fichier inventory permettant de renseigner les noms des hôtes vers lesquels centreon sera déployé
        
          [centreon_central]
   
          /* Mettre ici le fqdn ou l'adresse IP de votre serveur centreon central */ 
    
          [centreon_sgbd]
   
          /* Mettre ici le fqdn ou l'adresse IP de votre base de données centreon */ 
       
          [centreon_poller]
   
          /* Mettre ici le fqdn ou l'adresse IP de votre/vos serveur(s) centreon poller(s) */ 
       
   #  III. Lancement des playbooks
   
   # 1. Gestion des LVM et des FS (optionnel)
   
   Dans un environnement de production ou de recette, vous avez besoin de gérer les volumes logiques et filesystèmes.
   Pour cela exécuter le playbook : create-logical-volumes.yml
   
   **Commande ansible**
    
      ansible-playbook -i centreon-projet/environnements/prod/hosts create-logical-volumes.yml
   
   # 2. Déploiment du serveur *centreon central* et de sa *base de données*
   
  Pour installer/déployer centreon, le playbook à exécuter est : deploy-sgbd-and-central.yml
  
  **Commande ansible**
  
      ansible-playbook -i centreon-projet/environnements/prod/hosts deploy-sgbd-and-central.yml
  
   - Finir l'installation depuis l'interface web
    - Se connecter à l'interface web via : http://IP_SERVEUR_CENTREON_CENTRAL/centreon
    - L'assistant de configuration s'affiche, cliquer sur next :
    
     ![image](https://user-images.githubusercontent.com/61230711/196719714-03f6c7cd-7d1f-4676-8c01-f64c8e10a3c3.png)
     
     - Cliquer sur Next jusqu'à la cinquième étape puis saisir le mot de passe du compte **admin** puis cliquer sur Next
     NB : le mot doit être le même que celui renseigner sur le fichier all.yml
     
     ![image](https://user-images.githubusercontent.com/61230711/197517519-95c2c803-36b4-48bd-89f3-66dccbb390b1.png)
     
     - A l'étape 6, saisir l’IP du serveur de base de données, le mot de passe root mysql et l’utilisateur centreon à utiliser par le central et Cliquer sur next. 
     
     NB : fichier all.yml pour le mot passe root mysql et hosts pour l'ip de la base de données
     
     ![image](https://user-images.githubusercontent.com/61230711/196722124-d6ff9044-e2c1-4a3a-b537-b0fb3e5de0dd.png)
     
     - Cliquer ensuite sur Next
     - A la 8eme étape, cocher les modules et widgets qui vous intéressent puis cliquer sur Install puis sur Next à la fin des installations
     - Cliquer sur Finish à l'étape 9
     
     - Vous pouvez maintenant vous connecter à l'interface web avec les identifiants que vous avez défini : admin/votre password
     
     ![image](https://user-images.githubusercontent.com/61230711/197518465-743b2ed6-6067-4d0c-9124-c12fb8bce624.png)

     
   # 3. Initialisation de la supervision
   
   - Exporter la configuration en allant sur : **configuration > pollers** puis cliquer **Export configuration**
     
   ![image](https://user-images.githubusercontent.com/61230711/197518906-99260d65-adf9-42ca-8225-e3748654afcc.png)
   
   Cocher les 4 premières cases puis choisier la méthode **restart** puis cliquer sur **Export**
   
   ![image](https://user-images.githubusercontent.com/61230711/197519645-ac283194-0491-42ab-b045-924336e37443.png)

   
   - Redémarrer tous les services du central par le playbook : restart-central-services.yml
   
     **commande ansible**
        
          ansible-playbook -i centreon-projet/environnements/prod/hosts restart-central-services.yml

  # 4. Déploiement des pollers

  Pour installer/déployer les pollers centreon, le playbook à exécuter est : deploy-poller.yml
  
   **Commande ansible**
  
      ansible-playbook -i centreon-projet/environnements/prod/hosts deploy-poller.yml

