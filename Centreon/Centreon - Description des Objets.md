# Hôte

Un hôte dans Centreon, désigne l'équipement que l'on supervise. Il s'agit d'un équipement supportant la couche 3 c'est à dire ayant une adresse IP. Par exemple, on peut avoir comme hôte : Une imprimante, un switch, une caméra, un onduleur, un serveur, un OS (linux, windows ...), un firewall etc.

Un hôte dans centreon peut prendre un état parmi ces 4 :

 - Indisponible (Down) : l'équipement ne répond pas au ping.
 - Injoignable (Unreachable) : l'équipement est derrière un switch/routeur qui est indisponible. Ce qui veut dire que centreon n'arrive pas à le joindre.
 - Disponible (UP) : l'équipement répond bien au ping.
 - En attente (Pending) : l'équipement est en attente d'être contrôlé par centreon après un nouvel ajout ou modification.

# Plugins

Un plugin dans centreon désigne la sonde que l'on utilise pour interroger l'hôte que l'on supervise. Il peut s'agir d'un script perl pour la plupart des cas, d'un script bash, python ou tout autre type de langage.

En interrogeant l'équipement, le plugin doit être capable de renvoyer les codes de sorties suivants : 0, 1, 2 ou 3. Ces codes sont interprêtés par le moteur de supervision comme :

       0 => qui signifie OK
       1 => qui signifie Warnging
       2 => qui signifie Critique
       3 => qui signifie Inconnu
 En plus de ces codes de sortie, le plugin doit générer un message de sortie pour permettre à l'utilisateur de comprendre ce qui se passe.
 
# Commandes

La commande dans Centreon, à l'image d'une commande shell, se traduit par l'exécution d'un plugin en ligne de commande. Si le plugin prend des arguments, alors la commande prend des arguments.

On distingue quatres types de commandes : 

- Vérifications( pour Contrôler l'état des équipements), 
- Notifications (pour notifier les utilisateurs), 
- Découvertes (pour découvrir des hôtes ou services), 
- Divers (pour les actions diverses utlisées par exemple pour les gestions d'évènements, utilisées par l'ordonnanceur ou par certains modules).
- Connecteur (modules complémentaires et libre (perl (pour accélérer l'exécution des plugins perl) et ssh (pour maintenir les connexions ssh le temps d'exécution des contrôles via ssh)) 

# Services

Un service dans centreon désigne une instance, un élément à mesurer sur un hôte que l'on supervise. On peut définir par exemple un service pour superviser la mémoire d'un serveur, l'état d'une interface d'un switch ou l'utilisation du CPU d'un équipement.

Pour chaque service on lie une commande permettant de récupérer l'information via un plugin. Le service prend l'état que renvoie le plugin. Par exemple si le plugin renvoie OK, le service est en état OK.

Un service peut prendre un état parmi ces 4 :

- OK : état normal
- Warning : état alerte intermédiaire, on a atteint le seuil d'alerte warning; sans interruption de service.
- Critical : état critique, on a atteint le seuil d'alerte critique ; possible interruption de service.
- Unknown : état inconnu, centreon n'arrive pas à interpréter le résultat du contrôle.
- Pending (en attente) : le service est en attente d'être contrôlé par centreon après un nouvel ajout ou modification.

# Meta service

Un meta-service dans centreon est un service "virtuel" permettant d'aggréger plusieurs métriques récupérés de plusieurs autres services. Le but étant d'avoir une métrique globale. Par exemple par avoir le traffic global d'un routeur, on peut créer un méta-service récupérant les métriques des traffics de toutes les interfaces. On peut faire de même pour la charge globale de CPU utilisée en aggérgeant le pourcentage de tous les CPUs d'un serveur.

# Macros

Une macro dans centreon désigne une variable permettant de récupérer certaines valeurs. On peut avoir :

 - Macros personnaliseés : défini lors de la création d'un hôte/service et récupérable via les commandes.
 - Macros standards : défini nativement dans le code source du moteur de supervision et permettant de récupérer la valeur de certains objets 
 - Macros d'environnement (à la demande) : défini pour récupérer des données issues de d'autres objects
 - Macros de ressources : macro globale défini pour récupérer les valeurs des ressources (le chemin des plugins par exemple)

# Contact

Un contact dans centreon désigne un utilisateur. Il peut avoir des droits de connexion à l'interface web, d'accès et d'actions à/sur toutes/certaines ressources et peut recevoir des notifications.

# Template

Un template dans centreon, c'est un modèle de configuration permettant de définir des paramètres prédifinis. On distingue :

- Template d'hôte : modèle d'hôte
- Template de service : modèle de service  
- Template de contact : modèle d'utilisateur 

Les objets liés à un template héritent des paramètres définis sur le template. Un template, un service/hôte/contact peut hériter d'un ou plusieurs templates. 

# Les groupes 

Dans centreon on regroupe les objets selon leur appartenance géographique (segmentation physique) ou logique (selon le type, le rôle,...). On distingue des :

 - Groupe d'hôtes
      
 - Groupe de services
      
 - Groupe de contacts

Les groupes permettent d'appliquer des configurations à un ensemble d'objets et sont utilisés pour construire les tableux de bord (dashboard).

# Les notifications

Dans centreon on peut alerter (notifier) les évènements à des utilisateurs définis pour une période de temps défini. Cette notification peut se faire par mail ou par SMS.

# Les péridodes temporelles

Dans centreon on peut définir les heures d'exécution des controles (checks) et des envoies de notifications par intervalle de temps. Ces intervalles de temps sont appelés périodes temporelles. Par exemple dans la période temporelle (les heures ouvrées du lundi au vendredi), on peut contrôler et notifier sur les pannes des équipements afin de garantir une qualité de service optimale.

# Arborescence logique des objets centreon
![image](https://user-images.githubusercontent.com/61230711/199752538-ff5b9383-40e3-4e18-b0ff-b3c372d6de1a.png)
