# Crée la clé usb

## Pré-requis:

* [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg/releases), je recommande fortement d'exécuter la version de débogage pour afficher plus d'informations.
* [ProperTree](https://github.com/corpnewt/ProperTree), pour modifié les fichiers .plist (OpenCore Configurator est un autre outil mais il est très obsolète et la version Mackie est connue pour sa corruption. **Veuillez éviter ce type d'outils à tout prix !**).
* Vous devez supprimer entièrement Clover de votre système si vous souhaitez utiliser OpenCore comme boot-loader principal. Gardez une sauvegarde de votre EFI basé sur Clover. Voir ici ce qui doit être nettoyé: [Clover Conversion](https://github.com/dortania/OpenCore-Install-Guide/tree/master/clover-conversion).\\

## Installateur en ligne vs installateur hors ligne

Les installateurs hors ligne ont une copie complète de macOS, tandis que les installateurs en ligne ne sont qu'une image de récupération (\~ 500 Mo) qui télécharge par la suite macOS à partir des serveurs Apple.

* Hors ligne: Ne peut être créé que sous macOS Windows/Linux n'ont pas les pilotes APFS/HFS nécessaires pour assembler un programme d'installation complet
* En ligne: Peut être réalisé sous macOS/Linux/Windows Nécessite une connexion Internet fonctionnelle via un adaptateur réseau pris en charge par macOS sur la machine cible

## Création du programme d'installation

Selon le système d'exploitation sur lequel vous possédé, consultez votre section spécifique sur la création de l'USB :

* [Utilisateur macOS](https://opencore.pressynou.ch/creation-cle-usb/cree-la-cle-usb/macos)
  * Prend en charge de la version 10.4 de macOS à la dernière en date
  * Prend en charge les installations legacy et UEFI
* Utilisateur Windows
  * Prend en charge de la version 10.7 de macOS à la dernière en date
  * Installateur en ligne uniquement
  * Prend en charge les installations legacy et UEFI
* Utilisateur Linux (UEFI)
  * Prend en charge de la version 10.7 de macOS à la dernière en date
  * Installateur en ligne uniquement
  * Destiné aux machines prenant en charge uniquement l'UEFI

{% hint style="info" %}
Les installateurs en ligne peuvent servir à installé macOS via un DMG officiel pour l'installer d'une méthode "hors ligne".
{% endhint %}
