---
description: Vos premiers pas avec OpenCore
---

# Pré-requis

#### Avant de pouvoir commencé la création d'un système basé sur OpenCore, nous devons passer en revue quelques éléments.

1. _<mark style="color:red;">**\[CRUCIAL]**</mark>_ **Du temps et de la patience.**
   * Ne commencer pas à travailler si vous avez des délais ou du trvail important. Les hackintosh ne sont pas des machines sur lesquelles vous devez compter.
2. _<mark style="color:red;">**\[CRUCIAL]**</mark>_ **Connaître votre hardware.**
   * Le modèle et la génération de votre processeur (CPU)
   * Votre carte graphique (GPU)
   * Votre matériel de stockage (HDD/SSD,configuration NVMe/AHCI/RAID/IDE)
   * Le modèle de votre pc portable ou pc de bureau si celui-ci est un OEM
   * Votre **chipset internet**
   * Votre carte Wifi/Bluetooth
3. _<mark style="color:red;">**\[CRUCIAL]**</mark>_ **LA CONNAISSANCE DES BASES DES LIGNES DE COMMANDES POUR UTILISER LE TERMINAL**
   * ce n'est pas juste \[CRUCIAL], c'est la base de tout le guide. nous ne pouvons pas vous aidez si vous ne savez pas `cd` vers un répertoire ou supprimer des fichiers.
4. _<mark style="color:red;">**\[CRUCIAL]**</mark>_ une machine compatible comme dans la section _**Compatibilité**_.
   * [Page des limites hardware](https://dortania.github.io/OpenCore-Install-Guide/macos-limits.html)
5. _<mark style="color:red;">**\[CRUCIAL]**</mark>_ Au minimum:
   * une clé de 16gb si vous comptez utiliser MacOS pour creer la clé.
   * une clé de 4gb si vous comptez utiliser Windows/Linux pour créer la clé.
6. _<mark style="color:red;">**\[CRUCIAL]**</mark>_ Une **connexion internet** (pas de dongles Wifi, un adaptateur USB vers ethernet peut fonctionner suivant la prise en charge de MacOS) et vous devez savoir la modèle de votre carte ethernet
   * Vous devez disposer d'un port Ethernet physique ou d'un adaptateur/dongle Ethernet compatible avec macOS.. si vous avez [une carte Wifi compatible (ouvre une nouvelle fenêtre)](https://dortania.github.io/Wireless-Buyers-Guide/), vous pouvez aussi l'utiliser.
     * Notez que la majorité des cartes Wifi ne sont pas supporté par MacOS
   * Pour les personnes ne disposant pas de carte Wifi ou de port ethernet fonctionnel mais que vous avez un téléphone Android, vous pouvez connecter votre téléphone Android au Wifi et faire un partage de connexion en USB avec [HoRNDIS (ouvre une nouvelle fenêtre)](https://joshuawise.com/horndis#available\_versions).
7. _<mark style="color:red;">**\[CRUCIAL]**</mark>_ **Installation correcte de votre OS:**
   * Soit:
     * macOS (Un modèle récent serait mieux)
     * Windows (Windows 10, 1703 minimum)
     * Linux (Propre et fonctionelle, avec python 2.7 minimum)
   * Pour les utilisateur de Windows ou Linux, **15GB** d'espace libre sur le disque sur lequel vous travaillez. Sur Windows, votre dique ou est installer l'OS (C:) à besoin d'au moins **15GB** d'espace libre.
   * pour les utilisateurs de MacOS, **30GB** d'espace libre sur votre disque système.
   * la plupart des outils utilisée dans ce guide demande [Python d'installé](https://www.python.org/downloads/)
