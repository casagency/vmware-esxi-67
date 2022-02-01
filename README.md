# == Mis en place et patch de sécuritée vmware ==
#### Commencer par télécherger tout ces fichiers et mettez les dans un de vos datastores

    wget 55
    wget 55
    wget 55
    wget 55

### CVE-2018-3646 correction faille L1 Terminal evasion code
---------------------------------------------
    esxcli system settings kernel set -s hyperthreadingMitigation -v TRUE
    esxcli system settings kernel set -s hyperthreadingMitigationIntraVM -v FALSE


### Installation patch de mise à jour vmware 6.7
----------------------------------------------
#### (créer un dossier nomée MAJ dans un de vos datastore et placer les fichier zip des patch dedand)

    esxcli system maintenanceMode set --enable true
    esxcli software vib install -d /vmfs/volumes/datastore1/MAJ/ESXi670-202103001.zip
    esxcli system maintenanceMode set --enable false
    reboot

    esxcli system maintenanceMode set --enable true
    esxcli software vib install -d /vmfs/volumes/datastore1/MAJ/ESXi670-202201001.zip
    esxcli system maintenanceMode set --enable false
    reboot


Installation de la compatibitée MacOS
--------------------------------------
