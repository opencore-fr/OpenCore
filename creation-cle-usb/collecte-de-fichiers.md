# Collecte de Fichiers

Cette section sert à récupérer les différents fichiers qui feront démarrer macOS, nous attendons de vous que vous connaissiez bien votre matériel avant de commencer et, espérons-le, que vous ayez déjà fait un Hackintosh, car on rentrera pas profond dans les détails ici

> Quelle est la meilleure façon de savoir si mon matériel est pris en charge?

Voir la [**page des limitations matérielles**](https://opencore.pressynou.ch/introduction/limitations-hardware) pour un meilleur aperçu de ce dont macOS a besoin pour démarrer, le support matériel entre Clover et OpenCore est assez similaire.

> Quels sont les moyens de savoir quel matériel j'ai ?

Voir cette page avant: Trouver votre matériel

### Pilotes Logiciels

Les pilotes logiciels sont des pilotes utilisés par OpenCore pour l'environnemnt UEFI. Ils sont principalement nécessaires pour démarrer le système, soit en étendant la capacité de correction d'OpenCore, soit en vous montrant différents types de lecteurs dans le sélecteur OpenCore (c'est-à-dire les lecteurs HFS (MacOS Étendu)).

* **Note sur l'emplacement de ces fichiers**: Ces fichiers **DOIVENT** être placés dans `EFI/OC/Drivers/`

#### Universal

<details>

<summary>Pilotes nécessaires</summary>

Pour la majorité des systèmes, vous allez avoir besoin de 2 `efi` pour démarrer votre système :

* [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)(Nécessaire)
  * Nécessaire pour les disques en MacOS Etendu (ou HFS) (c'est à dire les installeurs de macOS et les partitions de récupérations). **Ne mixais pas plusieurs pilotes HFS!**
  * Pour les CPU Sandy Bridge et plus vieux (ainsi que les CPU Ivy Bridge bas de gamme (i3 et Celerons), voir la section en dessous.
* [OpenRuntime.efi](https://github.com/acidanthera/OpenCorePkg/releases)(Nécessaire)
  * Héritier de [AptioMemoryFix.efi](https://github.com/acidanthera/AptioFixPkg), utilisé comme une extention d'opencore pour vous aider a patcher boot.efi pour les correctifs NVRAM et une meilleure gestion de la mémoire. (RAM).
  * Rappelez vous que ces EFI sont fournis dans le OpenCorePkg téléchargé plus tôt.

</details>

#### Utilisateurs d'anciens systèmes

En bus des drivers d'au dessus, si votre matériel ne supporte pas les UEFI (2011 et avant), alors vous allez avoir besoin de ces EFI. Faites attention a la description de chacun car vous n'aurez peut-être pas besoin des 4:

* [OpenUsbKbDxe.efi](https://github.com/acidanthera/OpenCorePkg/releases)
  * Utilisés pour le sélectionneur de démarrage d'opencore **pour les utilisateuirs d'anciens systèmes utilisant DuetPkg**, [non recommandé et très nuisible sur les systèmes UEFI(Ivy Bridge et plus récent)](https://applelife.ru/threads/opencore-obsuzhdenie-i-ustanovka.2944066/page-176#post-856653)
* [HfsPlusLegacy.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlusLegacy.efi)
  * Variante ancienne de HfsPlus.efi, utilisée pour les systèmes qui n'ont pas de support d'instruction RDRAND. C'est généralement le cas sur les processeurs Sandy Bridge et plus vieux (tout comme les Ivy Bridge bas de gamme (i3 et Celerons))
  * Ne le mélangait PAS avec HfsPlus.efi, choisissez l'un ou l'autre selon votre PC, mais pas les 2.
* [OpenPartitionDxe](https://github.com/acidanthera/OpenCorePkg/releases)
  * Nécessaire pour lancer la partition de récupération de OS X 10.7 à 10.9
    * Ce fichier est fourni dans OpenCorePkg dans le dossier EFI/OC/Drivers
    * Note: Utilisateurs d'OpenDuet(donc sans UEFI) auront ce pilote déjà intégré, donc 0 utilité de le rajouter.
  * Non nécessaire pour OS X 10.10 Yosemite et plus récent

Ces fichiers vont dans le dossier Drivers dans votre EFI

<details>

<summary>Spécifique aux procésseurs 32-bits</summary>

Pour ceux avec des CPUs 32-Bit, vous allez devoir prendre ce driver.

* [HfsPlus32](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus32.efi)
  * Alternative à HfsPlusLegacy mais pour les CPUs 32-bit, ne PAS mélanger avec les autres pilotes HFS.

</details>

### Kexts

Un kest (pour **K**ernel **Ext**ension), est une sorte de Pilote pour macOS, ces fichiers vont dans le dossier Kexts de votre EFI.

* **Note pour Windows et Linux**: Les kexts ressemblent à des dossiers sur votre PC, **Vérifiez 2 fois** que le dossier que vous installez est in fichier avec un .kext (et n'esseayez pas de l'ajouter manuellement si il est manquant).
  * Si tout les kexts incluent aussi un fichier `.dSYM`, vous pouvez le supprimer. Ils sont uniquement pour le débuggage.
* **Note d'emplacement**: Ces fichiers **DOIVENT** êtres placés dans le dossier `EFI/OC/Kexts/`.

Tout les kexts listés plus bas sont disponibles **pré-complu=és** dans le [Kext Repo](http://kexts.goldfish64.com/). Les kexts sont compilés a chaque fois qu'un "commit" est posté.

#### Nécessaire

* Kexts nécessaire

Sans ces 2 kexts, le système ne DÉMARRERA PAS.

* [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases)(Nécessaire)
  * Émule la puce SMC trouvable dans les vrais macs, sans ça, macOS ne démarrera PAS.
  * Nécessite macOS 10.4 ou plus récent.
* [Lilu](https://github.com/acidanthera/Lilu/releases)(Nécessaire)
  * Un kext qui patche beaucoup de choses, nécessaire pour AppleALC, WhateverGreen, VirtualSMC et beaucoup d'autres kexts. Sans lilu, ils ne fonctionneront pas.
  * Notz que même si Lilu fonctionne à partir de macOS 10.4, beaucoup de plugins ne marcheront que sur les nouvelles versions.

#### Plugins VirtualSMC

Les plugins si dessous ne sont pas nécessaires pour démarrer le système et ajoute principalement des fonctions au systèùe comme du monitoring (Notez que VirtualSMC support 10.4, certains plugins peuvent nécessiter des versions plus récentes):

* SMCProcessor.kext
  * Utilisé pour voir la température CPU, **ne marche pas sur les système basées sur du CPU AMD**
  * Nécessite Mac OS X 10.7 Lion oru plus récent
* [SMCAMDProcessor](https://github.com/trulyspinach/SMCAMDProcessor)
  * Utilisé pour voir la température CPU sur les système basées sur du AMD Zen
  * **Sous developpement actif, peut être instable.**
  * nécessite AMDCPURyzenPowerManagement (voir les kexts spécifiques au CPU AMD plus bas)
  * Nécessite macOS 10.13 High Sierra ou plus récent
* SMCSuperIO.kext
  * Utilisé pour gérer la vitesse du ventilateur CPU, **ne marche pas sur les système basées sur du CPU AMD**
  * Nécessite OS X 10.6 Snow Leopard ou plus récent
* SMCLightSensor.kext
  * Utilisé pour les capteurs de lumière ambiante sur les PC Portables, **les PC Bureaux peuvent ignorer**
  * Ne pas utiliser si vous n'avez pas de capteur de lumière ambiante
  * Nécessite Mac OS X 10.6 Snow Leopard ou plus récent
* SMCBatteryManager.kext
  * utiliser pour gérer les batteries sur PC Portables, **les PC Bureaux peuvent ignorer**
  * Nécessite Mac OS X 10.4 Tiger ou plus récent
* SMCDellSensors.kext \*Permet une surveillance et un contrôle plus précis des ventilateurs sur les machines Dell prenant en charge le mode de gestion du système (SMM)
  * **Ne pas utiliser si vous n'avez pas de machine dell compatible**, la plupart des PC Portables dell devrait l'utiliser, ça sera bénéfique
  * Nécessite OS X 10.7 Lion ou plus récent

#### Partie graphique

* [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases)(Nécessaire)
  * Utilisé pour les patchs graphiques, correctifs DRM, vérification d'ID de carte mère, correctifs de framebuffer, etc; ça sera bénéfique à TOUS les GPUs.
  * Notez que le fichier SSDT-PNLF.dsl inclus est uniquement nécessaire pour les PC Portables et les AIOs, voir [Démarrer avec les ACPI](https://dortania.github.io/Getting-Started-With-ACPI/) pour plus d'infos
  * nécessite OS X 10.6 Snow Leopard ou plus récent

#### Audio

* [AppleALC](https://github.com/acidanthera/AppleALC/releases)
  * Utilisé pour le patch ApplmeHDA, autorisant le support de la majorité des controleurs audios sur carte mère
  * AppleALCU.kext est une version différente d'AppleALC qui supporte UNIQUEMENTR l'audio digital -mais vous pouvez toujours utiliser AppleALC.kext sur les système avec que de l'audio digital-
  * Les CPUs AMD 15h/16h peuvent avoir des problèmes avec AppleALC et les systèmes sous Ryzen et Threadripper ont rarement le support du micro
  * Nécessite OS X 10.8 Mountain Lion
* kext pour les anciens systèmes Pour ceux qui prévoient de démarrer OS X 10.7 Lion et plus vieux devrait opter pour ces kexts la
* [VoodooHDA](https://sourceforge.net/projects/voodoohda/)
  * Nécessite OS X 10.6 Snow Leopard
* [VoodooHDA-FAT](https://github.com/khronokernel/Legacy-Kexts/blob/master/FAT/Zip/VoodooHDA.kext.zip)
  * Similaire a celui du dessus, mais lui supporte les kernel 32 et 64 bits, donc parfait pour OS X 10.4 Tiger-10.5 Leopard et les CPUs 32 bits

#### Ethernet

Ici on part du principe que vous savez quelle carte internet vous avez, on vous rappelle que les pages de spécifications du produit répertorient très probablement le type de carte réseau.

* [IntelMausi](https://github.com/acidanthera/IntelMausi/releases)
  * Nécessaire pour la pluspart des NICs Intel, les chipsets basés sur I211 auront besoin du kext SmallTreeIntel82576
  * Les NICs Intel 82578, 82579, I217, I218 et I219 sont officiellement supportés
  * Nécessite OS X 1.9 Mavericks, les utilisateurs de 10.6 a 10.8 doivent utiliser IntelSnowMausi pour les OSes plus anciens
* [SmallTreeIntel82576 kext](https://github.com/khronokernel/SmallTree-I211-AT-patch/releases)
  * Nécessaire pour les NICs I211,basées sur le Kext SmallTree mais patché pour supporter les I211. (marche pas sur Monterey )
  * Nécessaire pour les systèmes AMD basées sur des NICs Intel.
  * Nécessite OS X 10.9-12(v1.0.6), macOS 10.13-14(v1.2.5), macOS 10.15+(v1.3.0)
* [AtherosE2200Ethernet](https://github.com/Mieze/AtherosE2200Ethernet/releases)
  * Nécessiare pour les NICs Atheros et Killer
  * Nécessite OS X 10.8 Mountain Lion ou plus récent
  * Note: Les modèles Atheros Killer E2500 sont actuellement basées sur du Realtek, pour ces systèmes utilisez plutot[RealtekRTL8111](https://github.com/Mieze/RTL8111\_driver\_for\_OS\_X/releases)
* [RealtekRTL8111](https://github.com/Mieze/RTL8111\_driver\_for\_OS\_X/releases)
  * Pour les ethernet Realtek Gigabit \*Nécessite OS X 10.8 Mountain Lion et plus pour les versions v2.2.0 et inférieures, macOS 10.12 et plus pour la version v2.2.2, macOS 10.14 et plus pour les versions v2.3.0 et plus
  * **NOTE:** Parfois la dernière version de ce Kext ne fonctionnera pas avec votre Ethernet. SI vous avez ce problème, esseayez une ancienne version..
* [LucyRTL8125Ethernet](https://www.insanelymac.com/forum/files/file/1004-lucyrtl8125ethernet/)
  * Pour le Realtek 2.5Gb
  * nécessite macOS 10.15 Catalina ou plus récent. \*Pour les NICs Intel I225-V, les correctifs sont écrits dans la page Propriété d'appareil comet lake. Aucun kext n'est nécessaire.
  * nécessite macOS 10.15 Catalina ou plus récent.
* Pour les NICs Intel I335, les correctifs sont ecrits lans le HEDT Propriété d'appareil Sandy et Ivy Bridge-E . Aucun kext n'est nécessaire.
  * Nécessite OS X 10.10 Yosemite
*   kexts Ethernet pour les anciens systèmes

    Pertinent pour les anciennes installations macOS ou le matériel PC plus ancien.
* [AppleIntele1000e](https://github.com/chris1111/AppleIntelE1000e/releases)
  * Principalement pertinent pour les contrôleurs Intel Ethernet basés sur 10/100MB
  * Nécessite OS X 10.6 Snow Leopard ou plus récent
* [RealtekRTL8100](https://www.insanelymac.com/forum/files/file/259-realtekrtl8100-binary/)
  * Principalement pertinent pour les contrôleurs Ethernet Realtek basés sur 10/100MBe
  * Nécessite macOS 10.12 Sierra ou plus récent avec v2.0.0 [BCM5722D](https://github.com/chris1111/BCM5722D/releases)
  * Principalement pertinent pour les contrôleurs Ethernet Broadcom basés sur BCM5722
  * Nécessite OS X 10.6 Snow Leopard ou plus récent

Et gardez également à l'esprit que certaines cartes réseau sont en fait prises en charge nativement dans macOS :

**Aquantia**

```md
# AppleEthernetAquantiaAqtion.kext
pci1d6a,1    = Aquantia AQC107
pci1d6a,d107 = Aquantia AQC107
pci1d6a,7b1  = Aquantia AQC107
pci1d6a,80b1 = Aquantia AQC107
pci1d6a,87b1 = Aquantia AQC107
pci1d6a,88b1 = Aquantia AQC107
pci1d6a,89b1 = Aquantia AQC107
pci1d6a,91b1 = Aquantia AQC107
pci1d6a,92b1 = Aquantia AQC107
pci1d6a,c0   = Aquantia AQC113
pci1d6a,4c0  = Aquantia AQC113
```

**Note** : En raison de certains micrologiciels obsolètes fournis sur de nombreuses cartes réseau Aquantia, vous devrez peut-être mettre à jour le micrologiciel sous Linux/Windows pour vous assurer qu'il est compatible avec macOS.

**Intel**

```md
# AppleIntel8254XEthernet.kext
pci8086,1096 = Intel 80003ES2LAN
pci8086,100f = Intel 82545EM
pci8086,105e = Intel 82571EB/82571GB

# AppleIntelI210Ethernet.kext
pci8086,1533 = Intel I210
pci8086,15f2 = Intel I225LM (Ajouté dans macOS 10.15 Catalina)

# Intel82574L.kext
pci8086,104b = Intel 82566DC
pci8086,10f6 = Intel 82574L
```

**Broadcom**

```md
# AppleBCM5701Ethernet.kext
pci14e4,1684 = Broadcom BCM5764M
pci14e4,16b0 = Broadcom BCM57761
pci14e4,16b4 = Broadcom BCM57765
pci14e4,1682 = Broadcom BCM57762
pci14e4,1686 = Broadcom BCM57766
```

#### USB

* [USBInjectAll](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/)
  * Utilisé pour injecter les controlleurs USB Intel sur les systèmes sans port USB définis dans l'ACPI.
  * Ne devrait pas être nécessaire pour Skylake sur PC Bureau et plus récent
    * AsRock est complètement con et nécessite ça
    * Les PC Portables sur Coffe Lake et plus vieux devraient utiliser ce Kext.
  * N'est pas cénessaire sur **aucun** CPU AMD
  * Nécessite OS X 10.11 El Capitan ou plus récent
* [XHCI-unsupported](https://github.com/RehabMan/OS-X-USB-Inject-All)
  * Nécessaire pour les contrelleurs USB non-natifs
  * Les systèmes basés sur des CPU AMD n'en ont pas besoin
  * Ces chipsets en ont besoin :
    * H370
    * B360
    * H310
    * Z390 (Non nécessaire sur 10.14 Mojave et plus récent)
    * X79
    * X99
    * Carte mères AsRock (spécificiquement sur les cartes mères basées sur du intel, les cartes B460 et Z490+ n'en ont pas besoin.)

#### WiFi et Bluetooth

**Intel**

* [AirportItlwm](https://github.com/OpenIntelWireless/itlwm/releases)
  * Ajoute un support pour une large variété de carte sans fils Intel et fonctionne nativement en mode réupération, merci pour l'intégration de IO90211Family
  * > Nécessite macO 10.13 High Sierra ou plus récent et nécessite le sécure boot d'apple pour fonctionner correctement.
* [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/releases)
  * Ajoute le support du blutooth dans macOS quand il est appairé avec une carte Intel sans fil.
  * Nécessite macOS 10.13 High Sirra ou plus récent

Plus d'infos pour activer le Kext AirportItlwm Pour activer AirportItlwm dans Opencore, vous devrez soit :

* Activeer `Misc -> Security -> SecureBootModel` soit en le définissant comme `Default` ou une autre valeur valide.
  * On en parle à la fois plus loin dans ce guide et dans le guide de post-installation: [Apple Secure Boot](https://dortania.github.io/OpenCore-Post-Install/universal/security/applesecureboot.html)
* Si vous ne pouvez pas activer le SecureBootModel, vous pouvez toujours injecter de force IO80211Family(**très découragé**)
  * Mettre ce dernier dans `Kernel -> Force` dans votre config.plist(parlé plus tard dans ce guide):

![](https://dortania.github.io/OpenCore-Install-Guide/assets/img/force-io80211.2e4f9bcd.png)

**Broadcom**

* [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup/releases)
  * Utilisé pour patch les cartes broadcom nom apple et non fenvi, **ne marchera pas sur Intel, Killer, Realtek, etc**
  * Nécessite OS X 10.0 Yosemite ou plus récent
  * Pour bigsur, voir Problèmes connus avec BigSUr pour les étapes copémentaires pour les pilotes AirPortBrcm4360.
* [BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM/releases)
  * Utilisé pour télécharger le logiciel sur le chipset Bluetooth Broadcom, requis pour toutes les cartes AirPort non Apple et non Fenvi.
  * Pour être appairé avec BrcmFirmwareData.kext
    * BrcmPatchRAM3 pour 10.15 Catalina+ (doit être lié avec BrcmBluetoothInjector)
    * BrcmPatchRAM2 pour 10.11 El Capitan à 10.14 Mojave
    * BrcmPatchRAM pour 10.8 Mountain Lion à 10.10 Yosemite

<details>

<summary>BrcmPatchRAM Load order</summary>

L'ordre dans `Kernel -> Add` doit être:

1. BrcmBluetoothInjector
2. BrcmFirmwareData
3. BrcmPatchRAM3

Après ProperTree va le faire pour vous, donc vous n'avez pas a vous en soucier

</details>

#### Kexts spécifiques pour les processeurs (CPU) AMD

* [XLNCUSBFIX](https://cdn.discordapp.com/attachments/566705665616117760/566728101292408877/XLNCUSBFix.kext.zip)
  * Correctif USB Pour les systèmes AMD FX, non recommandé por les Ryzen
  * Nécessite macOS 10.13 High Sierra ou plus récent
* [VoodooHDA](https://sourceforge.net/projects/voodoohda/)
  * Audio pour les systèmes FX et prise en charge Mic+Audio du panneau avant pour le système Ryzen, ne pas mixer avec AppleALC. La qualité audio est bien moins bonne lorsqu'on utilise AppleALC sur du AMD Zen
  * Nécessite OS X 10.6 Snow Leopard ou plus récent.
* [AMDCPURyzenPowerManagement](https://github.com/trulyspinach/SMCAMDProcessor)
  * gestion de l'alimentation CPU pour les Ryzen
  * **Sous développement actif, peut-être buggé**
  * Nécessite macOS 10.13 High Sierra Ou plus récent

#### Extras

* [AppleMCEReporterDisabler](https://github.com/acidanthera/bugtracker/files/3703498/AppleMCEReporterDisabler.kext.zip)
  * Nécessaire sur macOS 12.3 Monterey et après sur les systèmes AMD,et sur macOS 10.15 Catalina et après sur les système Intel dual-socket.
  * SMBios Affectés :
    * MacPro6,1
    * MacPro7,1
    * iMacPro1,1
* [CpuTscSync](https://github.com/lvs1974/CpuTscSync/releases)
  * Nécessaire pour synchroniser le TSC sur certaines cartes HEDT et serveurs d'Intel, sans ça, macOS peut être super lent, voire impossible à démarrer.
  * **Ne marche pas sur les processeurs (CPU) AMD.**
  * Nécessite OS X 10.8 Mountain Lion ou plus récent
* [NVMeFix](https://github.com/acidanthera/NVMeFix/releases)
  * Utiliser pour corriger la gestion de l'allumage et initialisation sur les NVMe non apple.
  * Nécessite macOS 10.14 Mojave ou plus récent
* [SATA-Unsupported](https://github.com/khronokernel/Legacy-Kexts/blob/master/Injectors/Zip/SATA-unsupported.kext.zip)
  * Prend en charge une grande variété de contrôleurs SATA, principalement pour les PC portables qui ont des problèmes pour voir le disque SATA dans macOS. Nous vous recommandons de tester d'abord sans ça.
  * Note pour BigSur: [CtlnaAHCIPort](https://github.com/dortania/OpenCore-Install-Guide/blob/master/extra-files/CtlnaAHCIPort.kext.zip) devra être utilisé à la place en raison de la suppression de nombreux contrôleurs du code lui-même
    * Catalina et plus vieux n'en ont pas besoin

<details>

<summary>Legacy SATA Kexts</summary>

* [AHCIPortInjector](https://github.com/khronokernel/Legacy-Kexts/blob/master/Injectors/Zip/AHCIPortInjector.kext.zip)
  * SATA/AHCI pour les anciens systèmes, principalement pertinents pour les anciennes machines des contrôleurs de l'ère Penryn supprimés du code lui-même
* [ATAPortInjector](https://github.com/khronokernel/Legacy-Kexts/blob/master/Injectors/Zip/ATAPortInjector.kext.zip)
  * Injecteur ATA pour les anciens systèmes, Lpertinant pour les apparels IDE et ATA (donc quand aucune option AHCI n'est présente dans le BIOS)

</details>

#### Entrée des PC Portables

Pour déterminer le type de clavier et de pavé tactile que vous avez, direction le Gestionnaire de périphériques sous Windows ou `dmesg | grep -i input` sous Linux

> **Warning** La plupart des PC Portables sont en PS/2 ! Vous allez devoir prendre VoodooPS2 même si vous avec un pavé tactile I2C, USB ou SMBus.

**Claviers et Pavés tactiles PS/2**

* [VoodooPS2](https://github.com/acidanthera/VoodooPS2/releases)
  * Marche avec la plupart des calviers, souris et pavés tactiles PS/2.
  * Nécessite macOS 10.11 El Capitan pour les fonctiions du "Magic Trackpad 2"
* [RehabMan's VoodooPS2](https://bitbucket.org/RehabMan/os-x-voodoo-ps2-controller/downloads/)
  * Pour les anciens systèmes avec des claviers, souris et pavés tactile PS2, ou si vous ne voulez pas utiliser VoodooInput
  * Supporte macOS 10.6 Snow leopard et plus récent

**Pavés tactiles SMBus**

* [VoodooRMI](https://github.com/VoodooSMBus/VoodooRMI/releases/)
  * Pour les systèmes avec des pavés tactils SMBus Synptics
  * nécessite macOS 10.12 Sierra ou plus récent pour les fonctions Magic trackpad 2
  * Dépends de Acidanthera's VoodooPS2
* [VoodooSMBus](https://github.com/VoodooSMBus/VoodooSMBus/releases)
  * Pour les sytèmes avec des pavés tactiles SMBus ELAN
  * Supporte macOS 10.14 Mojave ou plus récent

**Appareils IC2/USB HID**

* [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C/releases)
  * Supporte macOS 10.12 Siera et plus récent
  * Se connecte aux controlleurs IC2 pour autoriser les plugins a communiquer avec les pavés tactiles IC2
  * Les périphériques USB utilisant les les plugins ci-dessous ont toujours besoin de Voodoo I2C
  * Doit être couplé avec un ou plusieurs plugins ci dessous :

> **Note** Plugins Voodoo I2C

| Type de connexion         | Plugin                                                          | Notes                                                                                                                                     |
| ------------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Multitouch HID            | VoodooI2CHID                                                    | Peut être utilisé uniquement avec les pavés tactiles et les écrans taciles I2C et USB                                                     |
| ELAN Proprietary          | VoodooI2CElan                                                   | ELAN1200+ nécessite VoodooI2CHID                                                                                                          |
| FTE1001 touchpad          | VoodooI2CFTE                                                    | X                                                                                                                                         |
| Atmel Multitouch Protocol | VoodooI2CAtmelMXT                                               | X                                                                                                                                         |
| Synaptics HID             | [VoodooRMI](https://github.com/VoodooSMBus/VoodooRMI/releases/) | pavés tactiles Synaptics I2C (Nécessite VoodooI2C UNIQUEMENT pour le mode I2C)                                                            |
| Alps HID                  | [AlpsHID](https://github.com/blankmac/AlpsHID/releases)         | Peut être utilisé avec les pavés tactiles I2C ou USB Alps. Souvent vu sur les PC portables Dell et parfois sur des modèles d'HP Elitebook |

**Divers**

* [ECEnabler](https://github.com/1Revenger1/ECEnabler/releases)
  * Corrige le statut de la batterie sur la pluspart des PC Portables (autorise la lecture de Champs EF au dessus de 8 bits)
* [BrightnessKeys](https://github.com/acidanthera/BrightnessKeys/releases)
  * Corrige la luminosités des touches automatiquement

référez vous à [Kexts.md](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Kexts.md) pour une liste entioère des Kexts supportés

### SSDTs

Vous voyez donc tous ces SSDT dans le dossier AcpiSamples et vous vous demandez si vous en avez besoin. Pour nous, nous passerons en revue les SSDT dont vous avez besoin dans **votre section ACPI spécifique du config.plist**, car les SSDT dont vous avez besoin sont spécifiques à la plate-forme. Avec certains systèmes même spécifiques où ils doivent être configurés et vous pouvez facilement vous perdre si je vous donne une liste de SSDT parmi lesquels choisir maintenant.

[Démarrer avec les ACPI](https://dortania.github.io/Getting-Started-With-ACPI/) a une section étendue sur les SSDT, y compris leur compilation sur différentes plates-formes. Un rapide TL; DR des SSDT nécessaires (il s'agit du code source, vous devrez les compiler dans un fichier .aml) :

#### PC Bureau

|       Plateforme       |                                                                      **CPU**                                                                      |                                           **EC**                                           |                                        **AWAC**                                       |                                       **NVRAM**                                       |                                        **USB**                                        |
| :--------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------: |
|         Penryn         |                                                                        N/A                                                                        |    [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)   |                                          N/A                                          |                                          N/A                                          |                                          N/A                                          |
| Lynnfield et Clarkdale |                                                                         ^^                                                                        |                                             ^^                                             |                                           ^^                                          |                                           ^^                                          |                                           ^^                                          |
|       SandyBridge      | [CPU-PM](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#sandy-and-ivy-bridge-power-management) (Lancer en poste-installation) |                                             ^^                                             |                                           ^^                                          |                                           ^^                                          |                                           ^^                                          |
|       Ivy Bridge       |                                                                         ^^                                                                        |                                             ^^                                             |                                           ^^                                          |                                           ^^                                          |                                           ^^                                          |
|         Haswell        |                               [SSDT-PLUG](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html)                               |                                             ^^                                             |                                           ^^                                          |                                           ^^                                          |                                           ^^                                          |
|        Broadwell       |                                                                         ^^                                                                        |                                             ^^                                             |                                           ^^                                          |                                           ^^                                          |                                           ^^                                          |
|         Skylake        |                                                                         ^^                                                                        | [SSDT-EC-USBX](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html) |                                           ^^                                          |                                           ^^                                          |                                           ^^                                          |
|        Kaby Lake       |                                                                         ^^                                                                        |                                             ^^                                             |                                           ^^                                          |                                           ^^                                          |                                           ^^                                          |
|       Coffee Lake      |                                                                         ^^                                                                        |                                             ^^                                             | [SSDT-AWAC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/awac.html) | [SSDT-PMC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/nvram.html) |                                           ^^                                          |
|       Comet Lake       |                                                                         ^^                                                                        |                                             ^^                                             |                                           ^^                                          |                                          N/A                                          | [SSDT-RHUB](https://dortania.github.io/Getting-Started-With-ACPI/Universal/rhub.html) |
|      AMD (15/16h)      |                                                                        N/A                                                                        |                                             ^^                                             |                                          N/A                                          |                                           ^^                                          |                                          N/A                                          |
|      AMD (17/19h)      |        [SSDT-CPUR pour B550 et A520](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml)        |                                             ^^                                             |                                           ^^                                          |                                           ^^                                          |                                           ^^                                          |

#### PC Bureau haut de gamme

|      Plateforme     |                                        **CPU**                                        |                                           **EC**                                           |                                           **RTC**                                           |                                     **PCI**                                     |
| :-----------------: | :-----------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------: |
| Nehalem et Westmere |                                          N/A                                          |    [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)   |                                             N/A                                             |                                       N/A                                       |
|    Sandy Bridge-E   |                                           ^^                                          |                                             ^^                                             |                                              ^^                                             | [SSDT-UNC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/unc0) |
|     Ivy Bridge-E    |                                           ^^                                          |                                             ^^                                             |                                              ^^                                             |                                        ^^                                       |
|      Haswell-E      | [SSDT-PLUG](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html) | [SSDT-EC-USBX](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html) | [SSDT-RTC0-RANGE](https://dortania.github.io/Getting-Started-With-ACPI/Universal/awac.html) |                                        ^^                                       |
|     Broadwell-E     |                                           ^^                                          |                                             ^^                                             |                                              ^^                                             |                                        ^^                                       |
|      Skylake-X      |                                           ^^                                          |                                             ^^                                             |                                              ^^                                             |                                       N/A                                       |

#### PC Portable

|               Plateforme               |                                                                     **CPU**                                                                     |                                           **EC**                                           |                                      **Luminosité**                                      |                                   **Pavé tactile I2C**                                  |                                        **AWAC**                                       |                                        **USB**                                        |                                       **IRQ**                                       |
| :------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------: |
|        Clarksfield et Arrandale        |                                                                       N/A                                                                       |    [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)   | [SSDT-PNLF](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html) |                                           N/A                                           |                                          N/A                                          |                                          N/A                                          | [IRQ SSDT](https://dortania.github.io/Getting-Started-With-ACPI/Universal/irq.html) |
|               SandyBridge              | [CPU-PM](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#sandy-and-ivy-bridge-power-management) (Lance en post-installation) |                                             ^^                                             |                                            ^^                                            |                                            ^^                                           |                                           ^^                                          |                                           ^^                                          |                                          ^^                                         |
|               Ivy Bridge               |                                                                        ^^                                                                       |                                             ^^                                             |                                            ^^                                            |                                            ^^                                           |                                           ^^                                          |                                           ^^                                          |                                          ^^                                         |
|                 Haswell                |                              [SSDT-PLUG](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html)                              |                                             ^^                                             |                                            ^^                                            | [SSDT-GPI0](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad.html) |                                           ^^                                          |                                           ^^                                          |                                          ^^                                         |
|                Broadwell               |                                                                        ^^                                                                       |                                             ^^                                             |                                            ^^                                            |                                            ^^                                           |                                           ^^                                          |                                           ^^                                          |                                          ^^                                         |
|                 Skylake                |                                                                        ^^                                                                       | [SSDT-EC-USBX](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html) |                                            ^^                                            |                                            ^^                                           |                                           ^^                                          |                                           ^^                                          |                                         N/A                                         |
|                Kaby Lake               |                                                                        ^^                                                                       |                                             ^^                                             |                                            ^^                                            |                                            ^^                                           |                                           ^^                                          |                                           ^^                                          |                                          ^^                                         |
| Coffee Lake (8th Gen) and Whiskey Lake |                                                                        ^^                                                                       |                                             ^^                                             | [SSDT-PNLF](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html) |                                            ^^                                           | [SSDT-AWAC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/awac.html) |                                           ^^                                          |                                          ^^                                         |
|          Coffee Lake (9th Gen)         |                                                                        ^^                                                                       |                                             ^^                                             |                                            ^^                                            |                                            ^^                                           |                                           ^^                                          |                                           ^^                                          |                                          ^^                                         |
|               Comet Lake               |                                                                        ^^                                                                       |                                             ^^                                             |                                            ^^                                            |                                            ^^                                           |                                           ^^                                          |                                           ^^                                          |                                          ^^                                         |
|                Ice Lake                |                                                                        ^^                                                                       |                                             ^^                                             |                                            ^^                                            |                                            ^^                                           |                                           ^^                                          | [SSDT-RHUB](https://dortania.github.io/Getting-Started-With-ACPI/Universal/rhub.html) |                                          ^^                                         |

Continuing:

|              Plateforme              |                                       **NVRAM**                                       |                                        **IMEI**                                       |
| :----------------------------------: | :-----------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------: |
|       Clarksfield et Arrandale       |                                          N/A                                          |                                          N/A                                          |
|             Sandy Bridge             |                                           ^^                                          | [SSDT-IMEI](https://dortania.github.io/Getting-Started-With-ACPI/Universal/imei.html) |
|              Ivy Bridge              |                                           ^^                                          |                                           ^^                                          |
|                Haswell               |                                           ^^                                          |                                          N/A                                          |
|               Broadwell              |                                           ^^                                          |                                           ^^                                          |
|                Skylake               |                                           ^^                                          |                                           ^^                                          |
|               Kaby Lake              |                                           ^^                                          |                                           ^^                                          |
| Coffee Lake (8e Gen) et Whiskey Lake |                                           ^^                                          |                                           ^^                                          |
|         Coffee Lake (9e Gen)         | [SSDT-PMC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/nvram.html) |                                           ^^                                          |
|              Comet Lake              |                                          N/A                                          |                                           ^^                                          |
|               Ice Lake               |                                           ^^                                          |                                           ^^                                          |

## Maintenant que tout ça est fait, direction [Démarrer avec les ACPI](../demarrer-avec-les-acpi/demarrer-avec-les-acpi.md)
