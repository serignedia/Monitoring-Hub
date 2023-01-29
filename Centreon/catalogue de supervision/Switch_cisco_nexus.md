Catalogue de supervision SWITCH CISCO NEXUS via SNMPv3
---

Prérequis
--
- Configuer SNMPv3 sur les équipements à surveiller
- Ouvrir les flux SNMP (port 161) depuis centreon vers les équipements

Liste des points de contrôles
--

- CPU
- TEMPERATURE
- IFSTATUS : statut des interfaces
- IFTRAFFIC : stat du traffic des interfaces
- MEMORY
- PSU
  
 Commandes
 --
 
CPU

    /usr/lib/centreon/plugins//centreon_cisco_standard_snmp.pl --plugin=network::cisco::standard::snmp::plugin --mode=cpu --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --warning-core-5s='80' --critical-core-5s='90' --warning-core-1m='80' --critical-core-1m='90' --warning-core-5m='80' --critical-core-5m='90' --warning-average-5s='80' --critical-average-5s='90' --warning-average-1m='80' --critical-average-1m='90' --warning-average-5m='80' --critical-average-5m='' 


TEMPERATURE
     
    /usr/lib/centreon/plugins//centreon_cisco_standard_snmp.pl --plugin=network::cisco::standard::snmp::plugin --mode=environment --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --component='temperature' --warning='temperature,.*,60' --critical='temperature,.*,70'
  
IFSTATUS
  
    /usr/lib/centreon/plugins//centreon_cisco_standard_snmp.pl --plugin=network::cisco::standard::snmp::plugin --mode=interfaces --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --critical-status='%{admstatus} eq "up" and %{opstatus} eq "down"' --oid-filter='ifAlias' --oid-display='ifAlias' --oid-extra-display='ifName' --name --interface='^(?!(.tag_1.*|.tag_2.*)$)'
   
 
 tag pour exclure certaines interfaces du switch   
    
    tag_x : permet de ne pas superviser les interfaces du switch qui sont taggués (tag_x), avec l'option --interface='^(?!(.tag_1.*|.tag_2.*)$)'
  

IFTRAFFIC
  
    /usr/lib/centreon/plugins//centreon_cisco_standard_snmp.pl --plugin=network::cisco::standard::snmp::plugin --mode=interfaces --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --warning-in-traffic='80' --warning-out-traffic='80' --warning-in-error='2' --warning-out-error='2' --warning-in-discard='2' --warning-out-discard='2' --critical-in-traffic='90' --critical-out-traffic='90' --critical-in-error='4' --critical-out-error='4' --critical-in-discard='4' --critical-out-discard='4' --oid-filter='ifAlias' --oid-display='ifAlias' --oid-extra-display='ifName' --name --interface='^(?!(.tag_1.*|.tag_2.*))'
  

MEMORY
   
    /usr/lib/centreon/plugins//centreon_cisco_standard_snmp.pl --plugin=network::cisco::standard::snmp::plugin --mode=memory --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --warning-usage='80' --critical-usage='90'
   
PSU

    /usr/lib/centreon/plugins//centreon_cisco_standard_snmp.pl --plugin=network::cisco::standard::snmp::plugin --mode=environment --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --component='psu' --threshold-overload='psu,CRITICAL,^(?!(on|normal)$)' --verbose


Variabiliser les commandes : exemple
--

    $CENTREONPLUGINS$/centreon_cisco_standard_snmp.pl --plugin=network::cisco::standard::snmp::plugin --mode=memory --hostname=$HOSTADDRESS$ --snmp-version='$_HOSTSNMPVERSION$' --snmp-community='$_HOSTSNMPCOMMUNITY$' --snmp-username='$_HOSTUSERSNMPV3$' --authpassphrase='$_HOSTAUTHPASSWD$' --authprotocol='$_HOSTAUTHPROTO$' --privpassphrase='$_HOSTPRIVPASSWD$' --privprotocol='$_HOSTPRIVPROTO$' --warning-usage='$_SERVICEWARNING$' --critical-usage='$_SERVICECRITICAL$' $_SERVICEEXTRAOPTIONS$

Appliquer les bonnes pratiques
--

Auteur
--

Serigne S. DIA
  
