# Architecture applicative Centreon

Le produit Centreon est composé des éléments suivants :

  - L'interface web : serveur apache
  - La base de données : type MySQL 
  - Centreon Engine : le moteur de supervision qui réalise l'ordonnancement et la collecte des données de supervision
  - CBMOD : récupère les informations de centreon engine puis les envoie à Centreon Broker SQL
  - Centreon Broker SQL : permet d'enregistrer les informations à la base de données  
  - Centreon Broker RRD : son rôle est de produire les fichiers rrd nécessaires à la génération des graphiques de performance
  - Centreon Gorgone : utilisé pour exporter (déployer) la configuration depuis l'IHM vers les collecteurs. Il assure également la communication entre le serveur central et ses collecteurs (dans le cas d'une achitecture distribuée) ou avec d'autres serveurs distants.
  
# Architecture simple Centreon
 
  On parle d'architecture simple si tous les éléments cités plus haut sont regroupés dans un seul serveur.

# Architecture distribuée Centreon

  On parle d'architecture distribuée si on a un serveur de supervision centrale qui centralise toutes les données et un serveur de supervision satellite (poller).
  Dans ce cas, la distrbution des modules (composants) se fait comme suit :
  
   **Serveur Centreon Central** :  regroupe les éléments suivants :
   
   - L'interface web
   - La base de données
   - Centreon Engine
   - Centreon Broker
   - Centreon gorgone
   
   **Centreon poller** : c'est un collecteur satellite chargé d'aider le serveur central dans la collecte des données de supervision. Il regroupe :
   
   - Centreon Engine
   - Centreon Broker
   - Centreon gorgone
  
 # Architecture avec base de données déportée
  
  Il s'agit d'une architecture où la base de données est installée sur un serveur dédié et les autres composants sur le collecteur central et, au cas échéant, ses satellites.
  
  # Architecture avec remote serveur
  
  Un remote (distant) serveur est un collecteur (poller) avec une interface web affichant les données supervisées par le remote serveur. Ce qui veut dire qu'il remplit les fonctions du poller simple + la possibilité d'avoir une interface web sur son périmètre.
