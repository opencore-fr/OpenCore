# Processus d'installation

Maintenant que vous avez terminé la configuration d'OpenCore, vous pouvez enfin démarrer, les principales choses à garder à l'esprit :&#x20;

* Activer les paramètres du BIOS optimaux pour macOS&#x20;
* Lisez le [guide OpenCore Multiboot ](https://dortania.github.io/OpenCore-Multiboot/)ainsi que la [configuration de LauncherOption](https://dortania.github.io/OpenCore-Post-Install/multiboot/bootstrap)
  * Principalement pertinent pour ceux qui exécutent sur un seul disque plusieurs systèmes d'exploitations
* Et la page de [dépannage général](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/troubleshooting.html)
* Renseignez-vous sur [le processus de démarrage macOS](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/boot.html)
  * Il peut aider les installateurs débutants à mieux comprendre où ils peuvent être bloqués&#x20;
*   Et une tonne de patience



## Revérifiez votre config

Une dernière chose que nous devrions revoir avant de démarrer est la configuration de votre EFI :&#x20;

| EFI correct                                             | EFI incorrect                                |   |
| ------------------------------------------------------- | -------------------------------------------- | - |
| ![](<../.gitbook/assets/image (3).png>)                 | ![](<../.gitbook/assets/image (7).png>)      |   |
| Le dossier EFI est bien présent dans la partition EFI   | Le dossier EFI n'est pas présent             |   |
| Les fichers ACPI sont compilé (.aml)                    | Les fichiers ACPI ne sont pas compilé (.dsl) |   |
| DSDT ne sont pas présent                                | DSTD sont présent                            |   |
| Les drivers inutile on été retiré                       | Il reste les drivers par défaut              |   |
| Les tools inutile on été retiré                         | Il reste les tools par défaut                |   |
| Tout les fichiers dans le dossier Kexts finit pas .kext | Inclu le code source et les dossiers         |   |
| config.plist est présent dans EFI/OC                    | config.plist est renomé ou absent            |   |
| Uniquement les kexts qui sont nécessaire                | Tout les kext listé sont téléchargé          |   |

## Démarrage de l' USB OpenCore

Vous êtes donc maintenant prêt à mettre enfin la clé USB dans votre ordinateur et à démarrer dessus. N'oubliez pas que la plupart des ordinateurs portables et certains ordinateurs de bureau utiliseront toujours par défaut le lecteur interne avec Windows, et vous devrez sélectionner manuellement OpenCore dans les options de démarrage du BIOS. Vous devrez vérifier dans le manuel de l'utilisateur ou utiliser Google pour savoir quelle touche Fn accède au BIOS et au menu de démarrage (c'est-à-dire Esc, F2, F10 ou F12)

Une fois que vous avez démarré l'USB, vous serez probablement accueilli par les options de démarrage suivantes :

1. Windows
2. Système de base macOS (externe) / Installer macOS Big Sur (externe) / Nom du lecteur USB (externe)&#x20;
3. OpenShell.efi&#x20;
4. Réinitialiser la NVRAM&#x20;

Remarque : Vous devrez peut-être appuyer sur espace pour voir le programme d'installation, car dans les versions ultérieures d'OpenCore, HideAuxiliary est activé par défaut.

Pour nous, l'**option 2**. est celle que nous voulons. Selon la façon dont le programme d'installation a été créé, il peut être signalé comme **"macOS Base System (External)"**, **"Install macOS Big Sur (External)"** ou **"**_**Your USB drive's name**_** (External)".**

## macOS Installer <a href="#macos-installer" id="macos-installer"></a>

\
Donc, vous avez enfin démarré le programme d'installation, terminé le verbeux et lancé le programme d'installation ! Maintenant que vous êtes arrivé jusqu'ici, les principales choses à garder à l'esprit :&#x20;

* Les lecteurs sur lesquels vous souhaitez installer macOS doivent être à la fois du schéma de partition GUID et APFS&#x20;
  * High Sierra sur disque dur et tous les utilisateurs de Sierra devront utiliser macOS Journaled (HFS+)&#x20;
* Le lecteur doit également avoir une partition de 200 Mo&#x20;
  * Par défaut, macOS configurera les disques fraîchement formatés avec 200 Mo&#x20;
  * Consultez le Guide du [multiboot](https://dortania.github.io/OpenCore-Multiboot/) pour plus d'informations sur le partitionnement d'un lecteur Windows

Une fois l'installation lancée, vous devrez attendre que le système redémarre. Vous voudrez à nouveau démarrer dans OpenCore, mais plutôt que de sélectionner votre programme d'installation/récupération USB, vous devrez sélectionner le programme d'installation macOS sur le disque dur pour continuer l'installation. Vous devriez obtenir un logo Apple, et après quelques minutes, vous devriez obtenir une minuterie en bas indiquant "x minutes restantes". Cela peut être un bon moment pour prendre un verre ou une collation car cela prendra un certain temps. Il peut redémarrer quelques fois de plus, mais si tout se passe bien, il devrait enfin vous tomber sur l'écran "Configurer votre Mac"

Vous y êtes! 🎉 Vous pouvez parcourir les pages de post-installation pour terminer la configuration de votre système.

##
