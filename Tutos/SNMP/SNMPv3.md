# Installation de SNMP sur CentOS

    yum install net-snmp net-snmp-libs net-snmp-utils

# Configuration d'un user snmp v 3

    systemctl stop snmpd && net-snmp-create-v3-user -ro -a SHA -x AES -A 'your_auth_passphrase' -X 'your_priv_passphrase' snmp_user && systemctl start snmpd && systemctl status snmpd

snmp_user => votre utilisateur snmp

your_auth_passphrase => votre clé (password) d'authentification

your_priv_passphrase => votre clé (password de chiffrement

# Test avec snmpwalk

    snmpwalk -l authPriv -v 3 -u snmp_user -a SHA -A 'your_auth_passphrase' -x AES -X 'your_priv_passphrase' IP_ADDRESS OID -On
    
    Exemple :
    
    snmpwalk -l authPriv -v 3 -u snmp -a SHA -A 'Mtmx175o!' -x AES -X 'DTfL765' 192.168.0.11 .1.3.6.1.4.1 -On

# Pour supprimer l’utilisateur snmp v3  

Arrêter le démon snmpd 

    systemctl stop snmpd
    
Editer le fichier 

    vi /var/lib/net-snmp/snmpd.conf> et Supprimer la ligne < usmUser xxxxxxxxxxxx "snmp_user" "snmp_user" NULL .xxxxxxxxx> 
    
Editer le fichier 

    vi /etc/snmp/snmpd.conf> et Supprimer la ligne < rouser snmp_user>
    
Redémarrer le démon snmpd 

    systemctl start snmpd
