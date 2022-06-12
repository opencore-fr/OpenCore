# Limitations hardware

Avec MacOS, il y a de nombreuses limitations hardware, dont vous devez être conscient des limitations avant de mettre le pied dans une installation. Ceci est du à la faible quantité de matériel qu'Apple prend en charge, donc nous sommes soit limités par Apple ou par les correctifs créés par la communauté.

Les principales sections pour vérifier sont:

\[\[toc]]

Et pour des guides plus détaillés sur le sujet:

* [Guide d'achat de carte graphique](https://dortania.github.io/GPU-Buyers-Guide/)
  * Vérifier si votre GPU est supporté et quelle version de MacOS peut-il faire tourner.
* [Guide d'achat sans fil](https://dortania.github.io/Wireless-Buyers-Guide/)
  * Vérifier si votre carte wifi est supportée.
* [Guide d'achat anti-hardware](https://dortania.github.io/Anti-Hackintosh-Buyers-Guide/)
  * Guide général sur ce qu'il faut éviter et les pièges que votre matériel peut rencontrer.

## Support CPU

Pour le support du CPU, nous avons la répartition suivante:

* Les processeurs 32 et 64 bits sont pris en charge.
  * Cela nécessite toutefois que le système d'exploitation prenne en charge votre architecture, voir la section "Exigences du processeur" ci-dessous.
* Les CPU intel de bureau sont supportés.
  * Yonah à Comet Lake sont soutenus par ce guide.
* Les processeurs haut de gamme d'Intel pour ordinateurs de bureau et serveurs.
  * Nehalem à Cascade Lake X sont pris en charge par ce guide.
* Les Intel Core "i" et la séries des Xeon sur pc portable.
  * Arrandale à Ice Lake sont pris en charge par ce guide.
  * Notez que les processeurs Mobile Atoms, Celeron et Pentium ne sont pas pris en charge.
* Processeurs de bureau Bulldozer (15h), Jaguar (16h) et Ryzen (17h) d'AMD
  * Les CPU de pc portables **ne sont pas** supportés
  * Notez que toutes les fonctionnalité de MacOS ne sont pas supporté avec les processeur AMD, voir ci-dessous

**Pour plus d'information en profondeur, soir ici:**  [**Guide d'achat anti-hardware**](https://dortania.github.io/Anti-Hackintosh-Buyers-Guide/)****

<details>

<summary>Les exigences CPU</summary>

exigences de l'architecture&#x20;

* les CPU 32-bit sont supporté de MacOS 10.4.1 à 10.6.8
  * Notez que les versions 10.7.x demandent un userspace en 64-bit, limitant donc les cpu 32-bit à 10.6.
* les CPU 64-bit sont supporté des versions 10.4.1 au versions actuelle.

Exigences SSE:

* SSE3 est demandé pour toutes les versions Intel de OS X/macOS
* SSSE3 pour toutes les versions 64-bit de OS X/macOS
  * pour les CPUs n'ayant pas SSSE3 (i.e. certain Pentiums 64-bit), nous recommandons de tourner sur un userspace en 32-bit (`i386-user32`)
* SSE4 est demander pour les versions de macOS 10.12 et plus récentes
* SSE4.2 est demandé pour les versions de macOS 10.14 and plus récentes
  * Les CPUs ayant SSE4.1 sont supportés avec [telemetrap.kext](https://forums.macrumors.com/threads/mp3-1-others-sse-4-2-emulation-to-enable-amd-metal-driver.2206682/post-28447707)
  * Les pilotes AMD récent demandent aussi SSE4.2 pour le support de Metal. Pour résoudre cela, voir ici: [MouSSE: SSE4.2 emulation](https://forums.macrumors.com/threads/mp3-1-others-sse-4-2-emulation-to-enable-amd-metal-driver.2206682/)

Exigences firmware:

* De OS X 10.4.1 à 10.4.7, il faut un EFI32 (i.e. La version IA32 (32-bit) d'OpenCore).
  * De OS X 10.4.8 à 10.7.5, supports entre l'EFI32 et l'EFI64.
* De OS X 10.8 aux plus récentes EFI64 (i.e. la version x64 (64-bit) d'OpenCore).
* De OS X 10.7 à 10.9, ces versions demandent OpenPartitionDxe.efi pour démarrer sur la partition du recovery.

Exigences du Kernel:

* Les versions OS X 10.4 à 10.5 demandent des kexts 32-bit à cause du unique du kernelspace 32-bit.
  * Les versions OS X 10.6 à 10.7 supportent les kernelspace 32 et 64-bit.
* Les versions OS X 10.8 et récentes demandent des kexts 64-bit à cause du support unique du kernelspace en 64bit.
  * Lancez `lipo -archs` quelles architecture votre kext supporte (N'oubliez pas d'exécuter cette opération sur le binaire lui-même et non sur le paquet .kext.)

Limites du nombre de cœurs/threads:

* Les versions OS X 10.10 et inférieur ne peuvent pas démarrer avec plus de 24 threads (évident par une panique `mp_cpus_call_wait() timeout`)
* Les versions OS X 10.11 et récentes ont une limite de 64 threads
* l'argument de démarrage `cpus=` peut être utilisé comme solution de contournement, ou en désactivant l'hyperthreading

Notes spéciales:

* Lilu et les autres plugins demandent la version 10.8 ou plus récentes pour fonctionner
  * Nous recommandons de lancer FakeSMC pour les anciennes versions d'OS X
* Les versions OS X 10.6 et plus vielles demandent RebuildAppleMemoryMap d'activer
  * Il s'agit de résoudre un kernet précoce



</details>

#### &#x20;Tableau de support des processeurs Intel

Support basé sur les Kernels Vanilla (i.e. aucune modification):

| Génération du CPU                                                                                                                                                                                                                                                   | Support initial | Dernière version supporté | Notes                                              | CPUID                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | ------------------------- | -------------------------------------------------- | ----------------------------- |
| [Pentium 4](https://en.wikipedia.org/wiki/Pentium\_4)                                                                                                                                                                                                               | 10.4.1          | 10.5.8                    | Seulement utilisés dans les kits de développements | 0x0F41                        |
| [Yonah](https://en.wikipedia.org/wiki/Yonah\_\(microprocessor\))                                                                                                                                                                                                    | 10.4.4          | 10.6.8                    | 32-Bit                                             | 0x0006E6                      |
| [Conroe](https://en.wikipedia.org/wiki/Conroe\_\(microprocessor\)), [Merom](https://en.wikipedia.org/wiki/Merom\_\(microprocessor\))                                                                                                                                | 10.4.7          | 10.11.6                   | Pas d'SSE4                                         | 0x0006F2                      |
| [Penryn](https://en.wikipedia.org/wiki/Penryn\_\(microarchitecture\))                                                                                                                                                                                               | 10.4.10         | 10.13.6                   | Pas d'SSE4.2                                       | 0x010676                      |
| [Nehalem](https://en.wikipedia.org/wiki/Nehalem\_\(microarchitecture\))                                                                                                                                                                                             | 10.5.6          | Current                   | N/A                                                | 0x0106A2                      |
| [Lynnfield](https://en.wikipedia.org/wiki/Lynnfield\_\(microprocessor\)), [Clarksfield](https://en.wikipedia.org/wiki/Clarksfield\_\(microprocessor\))                                                                                                              | 10.6.3          | ^^                        | Pas de support iGPU pour les versions 10.14+       | 0x0106E0                      |
| [Westmere, Clarkdale, Arrandale](https://en.wikipedia.org/wiki/Westmere\_\(microarchitecture\))                                                                                                                                                                     | 10.6.4          | ^^                        | ^^                                                 | 0x0206C0                      |
| [Sandy Bridge](https://en.wikipedia.org/wiki/Sandy\_Bridge)                                                                                                                                                                                                         | 10.6.7          | ^^                        | ^^                                                 | 0x0206A0(M/H)                 |
| [Ivy Bridge](https://en.wikipedia.org/wiki/Ivy\_Bridge\_\(microarchitecture\))                                                                                                                                                                                      | 10.7.3          | ^^                        | Pas de support iGPU pour les versions 12+          | 0x0306A0(M/H/G)               |
| [Ivy Bridge-E5](https://en.wikipedia.org/wiki/Ivy\_Bridge\_\(microarchitecture\))                                                                                                                                                                                   | 10.9.2          | ^^                        | N/A                                                | 0x0306E0                      |
| [Haswell](https://en.wikipedia.org/wiki/Haswell\_\(microarchitecture\))                                                                                                                                                                                             | 10.8.5          | ^^                        | ^^                                                 | 0x0306C0(S)                   |
| [Broadwell](https://en.wikipedia.org/wiki/Broadwell\_\(microarchitecture\))                                                                                                                                                                                         | 10.10.0         | ^^                        | ^^                                                 | 0x0306D4(U/Y)                 |
| [Skylake](https://en.wikipedia.org/wiki/Skylake\_\(microarchitecture\))                                                                                                                                                                                             | 10.11.0         | ^^                        | ^^                                                 | 0x0506e3(H/S) 0x0406E3(U/Y)   |
| [Kaby Lake](https://en.wikipedia.org/wiki/Kaby\_Lake)                                                                                                                                                                                                               | 10.12.4         | ^^                        | ^^                                                 | 0x0906E9(H/S/G) 0x0806E9(U/Y) |
| [Coffee Lake](https://en.wikipedia.org/wiki/Coffee\_Lake)                                                                                                                                                                                                           | 10.12.6         | ^^                        | ^^                                                 | 0x0906EA(S/H/E) 0x0806EA(U)   |
| [Amber](https://en.wikipedia.org/wiki/Kaby\_Lake#List\_of\_8th\_generation\_Amber\_Lake\_Y\_processors), [Whiskey](https://en.wikipedia.org/wiki/Whiskey\_Lake\_\(microarchitecture\)), [Comet Lake](https://en.wikipedia.org/wiki/Comet\_Lake\_\(microprocessor\)) | 10.14.1         | ^^                        | ^^                                                 | 0x0806E0(U/Y)                 |
| [Comet Lake](https://en.wikipedia.org/wiki/Comet\_Lake\_\(microprocessor\))                                                                                                                                                                                         | 10.15.4         | ^^                        | ^^                                                 | 0x0906E0(S/H)                 |
| [Ice Lake](https://en.wikipedia.org/wiki/Ice\_Lake\_\(microprocessor\))                                                                                                                                                                                             | ^^              | ^^                        | ^^                                                 | 0x0706E5(U)                   |
| [Rocket Lake](https://en.wikipedia.org/wiki/Rocket\_Lake)                                                                                                                                                                                                           | ^^              | ^^                        | demandes un CPUID Comet Lake                       | 0x0A0671                      |
| [Tiger Lake](https://en.wikipedia.org/wiki/Tiger\_Lake\_\(microprocessor\))                                                                                                                                                                                         | N/A             | N/A                       | Non-testés                                         | !0x0806C0(U)                  |

<details>

<summary>AMD CPU Limitations in macOS</summary>

Unfortunately many features in macOS are outright unsupported with AMD and many others being partially broken. These include:

* Virtual Machines relying on AppleHV
  * This includes VMWare, Parallels, Docker, Android Studio, etc
  * VirtualBox is the sole exception as they have their own hypervisor
  * VMware 10 and Parallels 13.1.0 do support their own hypervisor, however using such outdated VM software poses a large security threat
* Adobe Support
  * Most of Adobe's suite relies on Intel's Memfast instruction set, resulting in crashes with AMD CPUs
  * You can disable functionality like RAW support to avoid the crashing: [Adobe Fixes](https://gist.github.com/naveenkrdy/26760ac5135deed6d0bb8902f6ceb6bd)
* 32-Bit support
  * For those still relying on 32-Bit software in Mojave and below, note that the Vanilla patches do not support 32-bit instructions
  * A work-around is to install a [custom kernel](https://files.amd-osx.com/?dir=Kernels), however you lose iMessage support and no support is provided for these kernels
* Stability issues on many apps
  * Audio-based apps are the most prone to issues, ie. Logic Pro
  * DaVinci Resolve has been known to have sporadic issues as well

</details>

## GPU Support

GPU support becomes much more complicated due to the near-infinite amount of GPUs on the market, but the general breakdown is as follows:

* AMD's GCN based GPUs are supported in the latest versions of macOS
  * AMD APUs are not supported however
  * AMD's [Lexa based cores](https://www.techpowerup.com/gpu-specs/amd-lexa.g806) from the Polaris series are also not supported
  * Special note for MSI Navi users: [Installer not working with 5700XT #901](https://github.com/acidanthera/bugtracker/issues/901)
    * This issue is no longer present in macOS 11 (Big Sur).
* Nvidia's GPU support is complicated:
  * [Maxwell(9XX)](https://en.wikipedia.org/wiki/GeForce\_900\_series) and [Pascal(10XX)](https://en.wikipedia.org/wiki/GeForce\_10\_series) GPUs are limited to macOS 10.13: High Sierra
  * [Nvidia's Turing(20XX,](https://en.wikipedia.org/wiki/GeForce\_20\_series)[16XX)](https://en.wikipedia.org/wiki/GeForce\_16\_series) GPUs are **not supported in any version of macOS**
  * [Nvidia's Ampere(30XX)](https://en.wikipedia.org/wiki/GeForce\_30\_series) GPUs are **not supported in any version of macOS**
  * [Nvidia's Kepler(6XX,](https://en.wikipedia.org/wiki/GeForce\_600\_series)[7XX)](https://en.wikipedia.org/wiki/GeForce\_700\_series) GPUs are supported up to macOS 11: Big Sur
* Intel's [GT2+ tier](https://en.wikipedia.org/wiki/Intel\_Graphics\_Technology) series iGPUs
  * Ivy Bridge through Ice Lake iGPU support is covered in this guide
    * Info on GMA series iGPUs can be found here: [GMA Patching](https://dortania.github.io/OpenCore-Post-Install/gpu-patching/)
  * Note GT2 refers to the tier of iGPU, low-end GT1 iGPUs found on Pentiums, Celerons and Atoms are not supported in macOS

And an important note for **Laptops with discrete GPUs**:

* 90% of discrete GPUs will not work because they are wired in a configuration that macOS doesn't support (switchable graphics). With NVIDIA discrete GPUs, this is usually called Optimus. It is not possible to utilize these discrete GPUs for the internal display, so it is generally advised to disable them and power them off (will be covered later in this guide).
* However, in some cases, the discrete GPU powers any external outputs (HDMI, mini DisplayPort, etc.), which may or may not work; in the case that it will work, you will have to keep the card on and running.
* However, there are some laptops that rarely do not have switchable graphics, so the discrete card can be used (if supported by macOS), but the wiring and setup usually cause issues.

**For a full list of supported GPUs, see the** [**GPU Buyers Guide**](https://dortania.github.io/GPU-Buyers-Guide/)

::: details Intel GPU Support Chart

| GPU Generation                                                                                              | Initial support | Last supported version | Notes                                                                                                             |
| ----------------------------------------------------------------------------------------------------------- | --------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [3rd Gen GMA](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Third\_generation) | 10.4.1          | 10.7.5                 | [Requires 32-bit kernel and patches](https://dortania.github.io/OpenCore-Post-Install/gpu-patching/legacy-intel/) |
| [4th Gen GMA](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen4)              | 10.5.0          | ^^                     | ^^                                                                                                                |
| [Arrandale(HD Graphics)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen5)   | 10.6.4          | 10.13.6                | Only LVDS is supported, eDP and external outputs are not                                                          |
| [Sandy Bridge(HD 3000)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen6)    | 10.6.7          | ^^                     | N/A                                                                                                               |
| [Ivy Bridge(HD 4000)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen7)      | 10.7.3          | 11.6.1                 | ^^                                                                                                                |
| [Haswell(HD 4XXX, 5XXX)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen7)   | 10.8.5          | Current                | ^^                                                                                                                |
| [Broadwell(5XXX, 6XXX)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen8)    | 10.10.0         | ^^                     | ^^                                                                                                                |
| [Skylake(HD 5XX)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen9)          | 10.11.0         | ^^                     | ^^                                                                                                                |
| [Kaby Lake(HD 6XX)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen9)        | 10.12.4         | ^^                     | ^^                                                                                                                |
| [Coffee Lake(UHD 6XX)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen9)     | 10.13.6         | ^^                     | ^^                                                                                                                |
| [Comet Lake(UHD 6XX)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen9)      | 10.15.4         | ^^                     | ^^                                                                                                                |
| [Ice Lake(Gx)](https://en.wikipedia.org/wiki/List\_of\_Intel\_graphics\_processing\_units#Gen11)            | 10.15.4         | ^^                     | Requires `-igfxcdc` and `-igfxdvmt` in boot-args                                                                  |
| [Tiger Lake(Xe)](https://en.wikipedia.org/wiki/Intel\_Xe)                                                   | N/A             | N/A                    | No drivers available                                                                                              |
| [Rocket Lake](https://en.wikipedia.org/wiki/Rocket\_Lake)                                                   | N/A             | N/A                    | No drivers available                                                                                              |

:::

::: details AMD GPU Support Chart

| GPU Generation                                                                                                                   | Initial support | Last supported version | Notes                                          |
| -------------------------------------------------------------------------------------------------------------------------------- | --------------- | ---------------------- | ---------------------------------------------- |
| [X800](https://en.wikipedia.org/wiki/Radeon\_X800\_series)                                                                       | 10.3.x          | 10.7.5                 | Requires 32 bit kernel                         |
| [X1000](https://en.wikipedia.org/wiki/Radeon\_X1000\_series)                                                                     | 10.4.x          | ^^                     | N/A                                            |
| [TeraScale](https://en.wikipedia.org/wiki/TeraScale\_\(microarchitecture\))                                                      | 10.4.x          | 10.13.6                | ^^                                             |
| [TeraScale 2/3](https://en.wikipedia.org/wiki/TeraScale\_\(microarchitecture\))                                                  | 10.6.x          | ^^                     | ^^                                             |
| [GCN 1](https://en.wikipedia.org/wiki/Graphics\_Core\_Next)                                                                      | 10.8.3          | Current                | ^^                                             |
| [GCN 2/3](https://en.wikipedia.org/wiki/Graphics\_Core\_Next)                                                                    | 10.10.x         | ^^                     | ^^                                             |
| [Polaris 10](https://en.wikipedia.org/wiki/Radeon\_RX\_400\_series), [20](https://en.wikipedia.org/wiki/Radeon\_RX\_500\_series) | 10.12.1         | ^^                     | ^^                                             |
| [Vega 10](https://en.wikipedia.org/wiki/Radeon\_RX\_Vega\_series)                                                                | 10.12.6         | ^^                     | ^^                                             |
| [Vega 20](https://en.wikipedia.org/wiki/Radeon\_RX\_Vega\_series)                                                                | 10.14.5         | ^^                     | ^^                                             |
| [Navi 10](https://en.wikipedia.org/wiki/Radeon\_RX\_5000\_series)                                                                | 10.15.1         | ^^                     | Requires `agdpmod=pikera` in boot-args         |
| [Navi 20](https://en.wikipedia.org/wiki/Radeon\_RX\_6000\_series)                                                                | 11.4            | ^^                     | Currently only some Navi 21 models are working |

:::

::: details Nvidia GPU Support Chart

| GPU Generation                                                                    | Initial support | Last supported version | Notes                                                                                                                       |
| --------------------------------------------------------------------------------- | --------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| [GeForce 6](https://en.wikipedia.org/wiki/GeForce\_6\_series)                     | 10.2.x          | 10.7.5                 | Requires 32 bit kernel and [NVCAP patching](https://dortania.github.io/OpenCore-Post-Install/gpu-patching/nvidia-patching/) |
| [GeForce 7](https://en.wikipedia.org/wiki/GeForce\_7\_series)                     | 10.4.x          | ^^                     | [Requires NVCAP patching](https://dortania.github.io/OpenCore-Post-Install/gpu-patching/nvidia-patching/)                   |
| [Tesla](https://en.wikipedia.org/wiki/Tesla\_\(microarchitecture\))               | 10.4.x          | 10.13.6                | ^^                                                                                                                          |
| [Tesla v2](https://en.wikipedia.org/wiki/Tesla\_\(microarchitecture\)#Tesla\_2.0) | 10.5.x          | ^^                     | ^^                                                                                                                          |
| [Fermi](https://en.wikipedia.org/wiki/Fermi\_\(microarchitecture\))               | 10.7.x          | ^^                     | ^^                                                                                                                          |
| [Kepler](https://en.wikipedia.org/wiki/Kepler\_\(microarchitecture\))             | 10.7.x          | 11.6.1                 | N/A                                                                                                                         |
| [Kepler v2](https://en.wikipedia.org/wiki/Kepler\_\(microarchitecture\))          | 10.8.x          | ^^                     | ^^                                                                                                                          |
| [Maxwell](https://en.wikipedia.org/wiki/Maxwell\_\(microarchitecture\))           | 10.10.x         | 10.13.6                | [Requires NVIDIA Web Drivers](https://www.nvidia.com/download/driverResults.aspx/149652/)                                   |
| [Pascal](https://en.wikipedia.org/wiki/Pascal\_\(microarchitecture\))             | 10.12.4         | ^^                     | ^^                                                                                                                          |
| [Turing](https://en.wikipedia.org/wiki/Turing\_\(microarchitecture\))             | N/A             | N/A                    | No drivers available                                                                                                        |
| [Ampere](https://en.wikipedia.org/wiki/Ampere\_\(microarchitecture\))             | ^^              | ^^                     | ^^                                                                                                                          |

:::

## Motherboard Support

For the most part, all motherboards are supported as long as the CPU is. Previously, B550 boards had issues:

* [~~AMD's B550 boards~~](https://en.wikipedia.org/wiki/List\_of\_AMD\_chipsets)

However thanks to recent developments, B550 boards are now bootable with the addition of [SSDT-CPUR](https://github.com/naveenkrdy/Misc/blob/master/SSDTs/SSDT-CPUR.dsl). More info will be provided in both [Gathering Files](https://github.com/Pressynou/opencore/blob/main/introduction/ktext.md) and [Zen's config.plist section](https://github.com/Pressynou/opencore/blob/main/introduction/AMD/zen.md)

## Storage Support

For the most part, all SATA based drives are supported and the majority of NVMe drives as well. There are only a few exceptions:

* **Samsung PM981, PM991 and Micron 2200S NVMe SSDs**
  * These SSDs are not compatible out of the box (causing kernel panics) and therefore require [NVMeFix.kext](https://github.com/acidanthera/NVMeFix/releases) to fix these kernel panics. Note that these drives may still cause boot issues even with NVMeFix.kext.
  * On a related note, Samsung 970 EVO Plus NVMe SSDs also had the same problem but it was fixed in a firmware update; get the update (Windows via Samsung Magician or bootable ISO) [here](https://www.samsung.com/semiconductor/minisite/ssd/download/tools/).
  * Also to note, laptops that use [Intel Optane Memory](https://www.intel.com/content/www/us/en/architecture-and-technology/optane-memory.html) or [Micron 3D XPoint](https://www.micron.com/products/advanced-solutions/3d-xpoint-technology) for HDD acceleration are unsupported in macOS. Some users have reported success in Catalina with even read and write support but we highly recommend removing the drive to prevent any potential boot issues.
* **Intel 600p**
  * While not unbootable, please be aware this model can cause numerous problems. [Any fix for Intel 600p NVMe Drive? #1286](https://github.com/acidanthera/bugtracker/issues/1286)

## Wired Networking

Virtually all wired network adapters have some form of support in macOS, either by the built-in drivers or community made kexts. The main exceptions:

* Intel I225 2.5Gb NIC
  * Found on high-end Desktop Comet Lake boards
  * Workarounds are possible: [Source](https://www.hackintosh-forum.de/forum/thread/48568-i9-10900k-gigabyte-z490-vision-d-er-l%C3%A4uft/?postID=606059#post606059) and [Example](https://github.com/Pressynou/opencore/blob/main/introduction/config.plist/comet-lake.md#deviceproperties)
* Intel I350 1Gb server NIC
  * Normally found on Intel and Supermicro server boards of various generations
  * [Workaround](https://github.com/Pressynou/opencore/blob/main/introduction/config-HEDT/ivy-bridge-e.md#deviceproperties)
* Intel 10Gb server NICs
  * Workarounds are possible for [X520 and X540 chipsets](https://www.tonymacx86.com/threads/how-to-build-your-own-imac-pro-successful-build-extended-guide.229353/)
* Mellanox and Qlogic server NICs

## Wireless Networking

Most WiFi cards that come with laptops are not supported as they are usually Intel/Qualcomm. If you are lucky, you may have a supported Atheros card, but support only runs up to High Sierra.

The best option is getting a supported Broadcom card; see the [WiFi Buyer's Guide](https://dortania.github.io/Wireless-Buyers-Guide/) for recommendations.

Note: Intel WiFi is unofficially (3rd party driver) supported on macOS, check [WiFi Buyer's Guide](https://dortania.github.io/Wireless-Buyers-Guide/) for more information about the drivers and supported cards.

## Miscellaneous

* **Fingerprint sensors**
  * There is currently no way to emulate the Touch ID sensor, so fingerprint sensors will not work.
* **Windows Hello Face Recognition**
  * Some laptops come with WHFR that is I2C connected (and used through your iGPU), those will not work.
  * Some laptops come with WHFR that is USB connected, if you're lucky, you may get camera functionality, but nothing else.
* **Intel Smart Sound Technology**
  * Laptops with Intel SST will not have anything connected through them (usually internal mic) work, as it is not supported. You can check with Device Manager on Windows.
* **Headphone Jack Combo**
  * Some laptops with a combo headphone jack may not get audio input through them and will have to either use the built-in microphone or an external audio input device through USB.
* **Thunderbolt USB-C ports**
  * (Hackintosh) Thunderbolt support is currently still iffy in macOS, even more so with Alpine Ridge controllers, which most current laptops have. There have been attempts to keep the controller powered on, which allows Thunderbolt and USB-C hotplug to work, but it comes at the cost of kernel panics and/or USB-C breaking after sleep. If you want to use the USB-C side of the port and be able to sleep, you must plug it in at boot and keep it plugged in.
  * Note: This does not apply to USB-C only ports - only Thunderbolt 3 and USB-C combined ports.
  * Disabling Thunderbolt in the BIOS will also resolve this.
