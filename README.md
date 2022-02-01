## == Mis en place et Patch de sécurité Vmware ESXi 6.7 Professionnel Plus ==
## Préambule projet :
Bonjour à tous, après pas mal de test sur Vmware ES Xi 6.7 et 7.0 j'ai pu voir quelques anomalies mais dans l'ensemble il s'agit d'un très bon hyperviseur quand ton effectue quelque prérogative, notamment sur la version 6.7 qui a une faille de sécurité critique pouvant amener à un contrôle sur l'hyperviseur, précisément sur le L1 TF (L1 terminal Fault). Affectent les microprocesseurs Intel. j'ai donc de ce pas corrigé cette faille et vous explique la procédure, je vous donne toutes les sources qui m'ont permis de configurée mon Vmware ES Xi 6.7 patché avec la possibilité de créer des VM Mac OS

#### Commencer par télécharger tous ces fichiers et mettez-les dans un de vos datstores

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


### CVE-2018-3646 correction faut L1 Terminale évasion code
---------------------------------------------
    esxcli system settings kernel set -s hyperthreadingMitigation -v TRUE
    esxcli system settings kernel set -s hyperthreadingMitigationIntraVM -v FALSE


### Installation patch de mise à jour Vmware 6.7
----------------------------------------------
#### (créer un dossier nommé MAJ dans un de vos data store et placer les fichiers zip des patchs dedans)

    esxcli system maintenanceMode set --enable true
    esxcli software vib install -d /vmfs/volumes/datastore1/MAJ/ESXi670-202103001.zip
    esxcli system maintenanceMode set --enable false
    reboot

    esxcli system maintenanceMode set --enable true
    esxcli software vib install -d /vmfs/volumes/datastore1/MAJ/ESXi670-202201001.zip
    esxcli system maintenanceMode set --enable false
    reboot


### Installation de la compatibilité Mac Os
--------------------------------------
	cp unlocker.zip /vmfs/volumes/datastore1/MAJ/unlocker.zip
	cd /vmfs/volumes/datastore1/MAJ/
	unzip unlocker.zip
	cd unlocker
	chmod +x ./esxi-install.sh 
	(si nécessaire, moi je n'ai pas eu à le faire en étant connecté directement en root en ssh, et parce qu'il les droits sont logiquement directement mis)
	./esxi-install.sh
	reboot


### Installation MacOX
-----------------------
	Consulté cette page :
	https://casagency.fr/VIB/MacOS12MontereyESXi.html
