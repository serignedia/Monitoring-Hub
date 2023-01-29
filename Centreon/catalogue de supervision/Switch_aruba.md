Catalogue de supervision SWITCH Aruba via SNMPv3
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

    /usr/lib/centreon/plugins//centreon_aruba_aoscx_snmp.pl --plugin=network::aruba::aoscx::snmp::plugin --mode=vsf --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --warning-cpu-utilization='80' --critical-cpu-utilization='90' --warning-status='%{status} !~ //i' --critical-status='%{status} !~ //i'
    
TEMPERATURE
     
    /usr/lib/centreon/plugins//centreon_aruba_aoscx_snmp.pl --plugin=network::aruba::aoscx::snmp::plugin --mode=hardware --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --component='temperature' -warning='temperature,.*,60000' --critical='temperature,.*,70000' --threshold-overload='temperature,WARNING,^(?!(NORMAL|CRITICAL)$)' --threshold-overload='temperature,CRITICAL,^(?!(NORMAL|WARNING)$)'
  
IFSTATUS
  
    /usr/lib/centreon/plugins//centreon_aruba_aoscx_snmp.pl --plugin=network::aruba::aoscx::snmp::plugin --mode=interfaces --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --critical-status='%{admstatus} eq "ignorer" and %{opstatus} eq "ignorer"' --warning-status='%{opstatus} eq "up"' --oid-filter='ifAlias' --oid-display='ifAlias' --oid-extra-display='ifName' --name --interface='^(.tag.*)$' --opt-exit='OK'
   
 
 *tag pour exclure certaines interfaces du switch*      
  

IFTRAFFIC
  
    /usr/lib/centreon/plugins//centreon_aruba_aoscx_snmp.pl --plugin=network::aruba::aoscx::snmp::plugin --mode=interfaces --add-traffic --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --warning-in-traffic='80' --warning-out-traffic='80' --warning-in-error='2' --warning-out-error='2' --warning-in-discard='2' --warning-out-discard='2' --critical-in-traffic='90' --critical-out-traffic='90' --critical-in-error='4' --critical-out-error='4' --critical-in-discard='4' --critical-out-discard='4' --oid-filter='ifAlias' --oid-display='ifAlias' --oid-extra-display='ifName' --name --interface='^(?!(.tag1.*|.tag2.*))'

MEMORY
   
    /usr/lib/centreon/plugins//centreon_aruba_aoscx_snmp.pl --plugin=network::aruba::aoscx::snmp::plugin --mode=vsf --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --warning-memory-usage-prct='80' --critical-memory-usage-prct='90' --warning-status='%{status} !~ //i' --critical-status='%{status} !~ //i'
    
PSU

    /usr/lib/centreon/plugins//centreon_aruba_aoscx_snmp.pl --plugin=network::aruba::aoscx::snmp::plugin --mode=hardware --hostname=IP_SWITCH --snmp-version='3' --snmp-community='' --snmp-username='snmp_user' --authpassphrase='your_auth_pass' --authprotocol='SHA' --privpassphrase='your_priv_pass' --privprotocol='AES' --component='psu' --threshold-overload='psu,CRITICAL,^(?!(up|normal|ok)$)' --verbose

Variabiliser les commandes : exemple
--

      $CENTREONPLUGINS$/centreon_aruba_aoscx_snmp.pl --plugin=network::aruba::aoscx::snmp::plugin --mode=hardware --hostname=$HOSTADDRESS$ --snmp-version='$_HOSTSNMPVERSION$' --snmp-community='$_HOSTSNMPCOMMUNITY$' --snmp-username='$_HOSTUSERSNMPV3$' --authpassphrase='$_HOSTAUTHPASSWD$' --authprotocol='$_HOSTAUTHPROTO$' --privpassphrase='$_HOSTPRIVPASSWD$' --privprotocol='$_HOSTPRIVPROTO$' --component='$_SERVICECOMPONENT$' -warning='$_SERVICEWARNING$' --critical='$_SERVICECRITICAL$' --threshold-overload='$_SERVICEWARNINGSTATUS-REGEX$' --threshold-overload='$_SERVICECRITICALSTATUS-REGEX$'

Appliquer les bonnes pratiques
--

Auteur
--

Serigne S. DIA
