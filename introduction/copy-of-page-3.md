# Trouver votre matériel



## Trouver votre matériel

Cette section est un petit guide sur comment trouver le matériel que vous utilisez actuellement; c'est surtout pertinant pour les utilisateur de PC Portables et ceux qui ont des PC Pré-construitsou le matériel est un peu plus difficile a trouver. Vous pouvez passer cette page et aller a Créer la clé usb si vous savez déjà quel matériel vous avez.

Pour ceci, nous partons du principe que vous avez Windows ou Linux de déjà installé.

### Trouver votre matériel avec Windows

Pour ça nous avons 2 choix principaux :

* Gestionnaire de périphériques de Windows
* [AIDA64](https://www.aida64.com/downloads)

Avec l'interface graphique plus facile a prendre en main, nous recommandons de télécharger AIDA64 et de s'en servir car il est bien plus facile de trouver les sépcifications de votre PC.. On va tout de même vous montrer les 2 manières de trouver votre matériel.

#### Modèle de processeur (CPU)

| AIDA64                                                                                          | Gestionnaire de périphériques                                                                          |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/cpu-model-aida64.aace72f2.png) | ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/cpu-model-devicemanager.e6eedd26.png) |

#### Modèle de carte graphique (GPU)

| AIDA64                                                                                          | Gestionnaire de périphériques                                                                          |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/GPU-model-aida64.b3b2cc00.png) | ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/GPU-model-devicemanager.677068d3.png) |

#### Modèle de 'Chipset'

| AIDA64                                                                                              | Gestionnaire de périphériques                                                                              |
| --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/chipset-model-aida64.782706ee.png) | ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/chipset-model-devicemanager.57f025ae.png) |

* Note: Les processeurs basés sur du Intel SoC (**S**ystem **O**n a **C**hip auront le chipset et d'autres fonctionnalités déjà sur le même bloc au lieu d'être des puces dédiées. Cela signifie que détecter le chipset exsact sera plus difficile.

#### Clavier, pavé tactile et type de connexion d'écran tactile

| Gestionnaire de périphériques                                                                               |
| ----------------------------------------------------------------------------------------------------------- |
| ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/trackpad-model-devicemanager.4e4c4e97.png) |

Malheuresement, AIDA64 ne donne aucune infos utile(s) pour les dispositifs de pointage, alors on recommande l'utilisation du gestiooonnaire de périphériques pour ça.

* Vous pouvez trouvez ces appareils dans la catégorie suivante :
  * `Interfaces Homme-machine`
  * `Claviers`
  * `Souris et autres dispositifs de pointage`
* Pour voir le type de connexion exsact, sélectionnez le périphérique de pointage exsact puis allez dans `Affichage -> Appareils par connection`. Ça clarifiera si c'est du PS2, I2C, SMBus, USB, etc.

Sleon le périphérique, ça devrait montrer plusieurs connextion. Le principal ou on doit garder un oeil dessus est :

* SMBus

Ceux-ci apparaîtront comme un périphérique PCI simple tel que `Synaptics SMBus Driver` ou `ELAN SMBus Driver`

* Les périphériques Synaptics apparaîtrons sous les deux PS2 comme `Périphérique PS2 Synaptics`/`Périphérique de pointage Synaptics` et PCI comme `Pilote SMBus Synaptics`

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/Windows-SMBus-Device.c4154ce4.png)

Comme vous pouvez le voir, on a 2 périphériques Synaptics dans l'image de gauche, Mais, si on regarde de plus près, on voit que l'appareil du haut est en PS2, alors que celui du bas est en SMBus. Bien que vous puissiez utiliser le pavé tactile dans les deux modes, le mode SMBus offre la plupart du temps une meilleure prise en charge et une meilleure précision des gestes.

* USB

| Appareil par type                                                                                  | Appareil par connection                                                                                                |
| -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/USB-trackpad-normal.4415be9a.png) | !\[]\(![image](https://user-images.githubusercontent.com/106166359/182404319-4ae0a03d-af78-4b05-a542-e1f3a35cfa0c.png) |

Ceux si sont notés : `Pavé tactile conforme PS2 (approximatif)`, mais aussi sous USB quand on bascule notre vue de connexion sur `Appareil par connexion`

* I2C

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/i2c-trackpad.3277ba42.png) Ceux la apparaîtront presque toujours comme des périphériques Microsoft HID, mais peuvent également apparaître comme d'autres trackpads. Mais, ils apparaîtront toujours sous I2C.

#### Codec audios

| AIDA64                                                                                                 | Gestionnaire de périphériques                                                                              |
| ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------- |
| ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/audio-controller-aida64.c4a94a0b.png) | ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/audio-controller-aida64.png.bf36cd98.png) |

A cause de la manière dont certains OEM font les noms de périphériques, les infos les plus précises que vous pouvez obtenir avec le gestionnaire de périphériques sont via l'ID PCI (c'est-à-dire pci 14F1,50F4). Cela signifie que vous devrez rechercher l'ID sur Google et déterminer l'ID exact de l'appareil, mais AIDA64 peut présenter le nom correctement, ce qui est un peu plus facile pour vous.

#### Modèle de controlleurs réseaux

| AIDA64                                                                                          | Gestionnaire de périphériques                                                                          |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/nic-model-aida64.794005c8.png) | ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/nic-model-devicemanager.9bc7b615.png) |

A cause de la manière dont certains OEM font les noms de périphériques, les infos les plus précises que vous pouvez obtenir avec le gestionnaire de périphériques sont via l'ID PCI (c'est-à-dire `PCI\VEN_14E4&DEV_43A0` correspond a un ID de marque of `14E4` et un ID d'appareil de `43A0`). Cela signifie que vous devrez rechercher l'ID sur Google et déterminer l'ID exact de l'appareil, mais AIDA64 peut présenter le nom correctement, ce qui est un peu plus facile pour vous.

#### Modèle de disque dur / SSD

| AIDA64                                                                                           | Gestionnaire de périphériques                                                                           |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/disk-model-aida64.72b7da46.png) | ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/disk-model-devicemanager.41243ee5.png) |

A cause de certains OEM qui ne donnent pas beaucoup de détails à propos de leurs disque dur/SSD, Vous aurez besoin de taper sur google quel disque dur correspond au nom affiché.

### Trouver le matériel avec linux

Pour touver le matériel avec linux, on va utilser quelques outils tel que :

* `pciutils`
* `dmidecode`

Vous trouverez en dessous une liste de commandes à exécuter dans le terminal. Heureusement, la plupart des distro Linux sont livrées avec ces outils déjà installés. Sinon, vous les trouverez probablement dans le gestionnaire de paquets de votre distribution, ou avec un sudo apt-get pour les distro basées sur du débian ;).

#### Modèle de processeur (CPU)

```
grep -i "model name" /proc/cpuinfo
```

#### Modèle de carte graphique (GPU)

```
lspci | grep -i --color "vga\|3d\|2d"
```

#### Modèle de 'Chpiset'

```
dmidecode -t baseboard
```

#### Clavier, pavé tactile et type de connexion d'écran tactile

```
dmesg | grep -i input
```

#### Codec audios

```
aplay -l
```

#### Modèle de controlleurs réseaux

Infos basiques:

```
lspci | grep -i network
```

Infos plus poussées:

```
lshw -class network
```

#### Modèle de disque dur / SSD

```
lshw -class disk -class storage
```

### Trouver le matériel avec OCSysInfp

Il y a 2 méthodes pour récupérer et lancer OCSysInfo:

* [Code pré-compilé](https://github.com/KernelWanderers/OCSysInfo/releases)
* [Cloner manuellement le repo](https://github.com/KernelWanderers/OCSysInfo)

::: astuce On vous recommande de télécharger [le code précompilé](https://github.com/KernelWanderers/OCSysInfo/releases), ce qui est la mathode la plus facile.

Si vous voulez en apprendfre plus pour cloner le repo manuellement, vous pouvez aller voir le [mini-guide OCSysInfo](https://github.com/KernelWanderers/OCSysInfo/tree/main/mini-guide). :::

#### Découvir le matériel

::: attention Utilisateurs sur PC Portables: avant de démarrer, nous vous conseillons de déconnecter tout type de stockage externe USB, car ça peut amener à la récolte d'informations ambiguës ou inutiles qui peuvent vous rendre confus. :::

Une fois que l'application a été corrctement installée et lancée, you should be greeted with the following screen:

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/ocsysinfo-example.b6fb71ae.png)

A partir d'ici, vous pouvez appuyer sur `d` et appuyer sur `ENTER`/`RETURN`, après ça, vous devriez être accueilli par un écran similaire :

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/ocsysinfo-hwdisc.0552a0c3.png)

#### Modèle de processeur (CPU)

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/cpu-model-ocsysinfo.6150fbf3.png)

Besides the CPU model, it also lists the CPU's codename, highest SSE version supported and SSSE3 availability.

#### Modèle de carte graphique (GPU)

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/gpu-model-ocsysinfo.a45a8727.png)

Dans ce cas, le PC a 2 GPU (carte graphiques)

* iGPU = garte graphique intégrée : Intel UHD Graphics 630
* dGPU = carte graphique dédiée : AMD Radeon R9 390X

En dehors les noms de modèles, il liste également le nom de code des GPU, les chemins ACPI et PCI, que vous pourriez bientôt trouver utiles au fur et à mesure de votre progression dans votre parcours hackintosh.

#### Clavier, pavé tactile et type de connexion d'écran tactile

* Pavé tactile SMBus ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/id-smbus-ocsysinfo.b4de10bd.png) Pavé tactile : `SMBus`\
  Clavier: `PS/2` Crédit pour cette image: [ThatCopy](https://github.com/ThatCopy)
* Pavé tactile I2C ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/id-i2c-ocsysinfo.4a83c466.png) Pavé tactile: `I2C`\
  Clavier: `PS/2` Crédit pour cette image: [Mahas](https://github.com/Mahas1)
* Pavé tactile PS/2 ![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/id-ps2-ocsysinfo.ea64d0ff.png) Pavé tactile: `PS/2`\
  Clavier: `PS/2` Crédit pour cette image: [Tasty0](https://github.com/Tasty0)

#### Codec audios

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/audio-codec-ocsysinfo.b196d284.png)

#### Modèles réseaux

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/network-model-ocsysinfo.7095f7ef.png)

#### Modèle de disque dur / SSD

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/drive-model-ocsysinfo.40e31cef.png)
