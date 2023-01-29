Catalogue de supervision ILO HPE via SNMPv3
---

Prérequis
--
- Configuer SNMPv3 sur les équipements à surveiller
- Ouvrir les flux SNMP (port 161) depuis centreon vers les équipements


1. Liste des points de contrôles :

       FAN : ventilation
       PSU : alimentation
       TEMPERATURE : température
       STORAGE : espace de stockage
       NETWORK : carte réseaux

2. Commandes

FAN 

    /usr/lib/centreon/plugins//centreon_hp_proliant.pl --plugin=hardware::server::hp::proliant::snmp::plugin --mode=hardware --hostname=IP_HOST --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --component='fan' --verbose --threshold-overload='fan,OK,other'
    
PSU 

    /usr/lib/centreon/plugins//centreon_hp_proliant.pl --plugin=hardware::server::hp::proliant::snmp::plugin --mode=hardware --hostname=IP_HOST --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --component='psu' --verbose --threshold-overload='.*,OK,other'
    
TEMPERATURE

    /usr/lib/centreon/plugins//centreon_hp_proliant.pl --plugin=hardware::server::hp::proliant::snmp::plugin --mode=hardware --hostname=IP_HOST --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --component='temperature' --verbose --warning='temperature,.*,70' --critical='temperature,.*,90'

STORAGE

     /usr/lib/centreon/plugins//centreon_hp_proliant.pl --plugin=hardware::server::hp::proliant::snmp::plugin --mode=hardware --hostname=IP_HOST --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --component='storage' --verbose --threshold-overload='.*,OK,other'

NETWORK

    /usr/lib/centreon/plugins//centreon_hp_proliant.pl --plugin=hardware::server::hp::proliant::snmp::plugin --mode=hardware --hostname=IP_HOST --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --component='network' --verbose --threshold-overload='nic,OK,other'

3. Bonnes pratiques centreon :

  - Créer une commande de base avec des macros personnalisés
  
        $CENTREONPLUGINS$/centreon_hp_proliant.pl --plugin=hardware::server::hp::proliant::snmp::plugin --mode=hardware --hostname=$HOSTADDRESS$ --snmp-version='$_HOSTSNMPVERSION$' --snmp-community='$_HOSTSNMPCOMMUNITY$' --snmp-username='$_HOSTUSERSNMPV3$' --authpassphrase='$_HOSTAUTHPASSWD$' --authprotocol='$_HOSTAUTHPROTO$' --privpassphrase='$_HOSTPRIVPASSWD$' --privprotocol='$_HOSTPRIVPROTO$' --component='$_SERVICECOMPONENT$' $_SERVICEEXTRAOPTIONS$

  - Créer un template de service pour chaque point de contrôle
 
  ![image](https://user-images.githubusercontent.com/61230711/200592841-cadee0b8-5b83-41d7-a497-adc6cacd0146.png)
  
  Liste des points de contrôles HPE ILO (modèles de services)

  ![image](https://user-images.githubusercontent.com/61230711/200592981-01aa61b0-1c89-47de-8a74-3a7563032933.png)

  - Créer un template d'hôte globale pour le produit HPE
  
  ![image](https://user-images.githubusercontent.com/61230711/200593806-000ac366-3a4a-4f80-8ad6-0b31809c5c18.png)

  - Lier tous les templates de service à votre template d'hôte
  
  ![image](https://user-images.githubusercontent.com/61230711/200594131-57505153-faa2-47d3-8521-ccafeb7b4074.png)
 
  - Lier ensuite le template d'hôte à un hôte
  - Déployer les services sur l'hôte en question
  - Déployer la configuration du poller option "redémmarer"
  - Aller ensuite dans Supervision > Statut des ressources pour suivre en temps réel votre supervision
  - Bravo


Auteur :
--
Serigne Saliou DIA
