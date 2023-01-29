Catalogue Supervision ESX
---

Prérequis 
--
1. Installer le daemon centreon_vmware
2. Configuer le daemon avec les accès vers le VCenter ou l'ESX

Liste des points de contrôle
--

    Datastore : stokage datastore
    Memory : mémoire
    NET : carte réseaux
    Time-host : synchronisation avec le serveur de temps

Commandes
---

Datastore

    /usr/lib/centreon/plugins//centreon_vmware_connector_client.pl --plugin=apps::vmware::connector::plugin --mode=datastore-usage --custommode=connector --connector-hostname='IP_OR_HOSTNAME_CONNECTOR' --connector-port='5700' --container='default' --filter-host='ESX_HOSTNAME' --unknown-status='%{accessible} !~/^true|1$/i' --warning-usage-prct='85' --critical-usage-prct='92' --verbose

Memory

    /usr/lib/centreon/plugins//centreon_vmware_connector_client.pl --plugin=apps::vmware::connector::plugin --mode=memory-host --custommode=connector --connector-hostname='IP_OR_HOSTNAME_CONNECTOR' --connector-port='5700' --container='default' --filter-host='ESX_HOSTNAME' --unknown-status='%{accessible} !~/^true|1$/i' --warning-consumed-memory='90' --critical-consumed-memory='95'

NET

    /usr/lib/centreon/plugins//centreon_vmware_connector_client.pl --plugin=apps::vmware::connector::plugin --mode=net-host --custommode=connector --connector-hostname='IP_OR_HOSTNAME_CONNECTOR' --connector-port='5700' --container='default' --filter-host='ESX_HOSTNAME' --unknown-status='%{accessible} !~/^true|1$/i' --nic-name='nom_de_la_carte_reseau$'
    
Time-host

    /usr/lib/centreon/plugins//centreon_vmware_connector_client.pl --plugin=apps::vmware::connector::plugin --mode=time-host --custommode=connector --connector-hostname='IP_OR_HOSTNAME_CONNECTOR' --connector-port='5700' --container='default' --filter-host='ESX_HOSTNAME' --unknown-status='%{accessible} !~/^true|1$/i' --warning-usage-prct='85' --critical-usage-prct='92' --warning-time='-10:10' --critical-time='-60:60' --verbose
    

Variabiliser les commandes : exemple
--
    $CENTREONPLUGINS$/centreon_vmware_connector_client.pl --plugin=apps::vmware::connector::plugin --mode=datastore-usage --custommode=connector --connector-hostname='$_HOSTCENTREONVMWAREHOST$' --connector-port='$_HOSTCENTREONVMWAREPORT$' --container='$_HOSTCENTREONVMWARECONTAINER$' --filter-host='$HOSTALIAS$' --unknown-status='$_SERVICEUNKNOWNSTAT$' --warning-usage-prct='$_SERVICEUSAGEWARNING$' --critical-usage-prct='$_SERVICEUSAGECRITICAL$' --verbose
    
Appliquer les bonnes pratiques
--

Auteur
--

Serigne S. DIA
