# == Mis en place et patch de sécuritée vmware ==
#### Commencer par télécherger tout ces fichiers et mettez les dans un de vos datastores

    (version 202103001)
    https://mega.nz/file/erJHiIgD#KuZnnRuCdogyXcbM2jE-zuDaeo9QiJ22eHtuLsJQ27I

    (version 202201001)
    https://mega.nz/file/erJHiIgD#KuZnnRuCdogyXcbM2jE-zuDaeo9QiJ22eHtuLsJQ27I

    ( Pour permettre l'installation de MacOS)
    wget https://github.com/casagency/vmware-esxi-67/blob/main/unlocker.zip

    (lecharger macos)
    https://store4.gofile.io/download/6f235bcc-9bf0-4921-971b-4a7a0cd0f5cc/macOS%20Monterey.iso
    
    ou
    --
    
    https://depannageinformatique.org/telecharger-iso-dmg-macos/


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


### Installation de la compatibitée MacOS
--------------------------------------
	cp unlocker.zip /vmfs/volumes/datastore1/MAJ/unlocker.zip
	cd /vmfs/volumes/datastore1/MAJ/
	unzip unlocker.zip
	cd unlocker
	chmod +x ./esxi-install.sh 
	(si necessaire, moi je n'ai pas eu a le faire en etant connecter directement en root en ssh)
	./esxi-install.sh
	reboot


### Installation MacOX
-----------------------
	Consulté cette page :
	https://casagency.fr/VIB/MacOS12MontereyESXi.html
