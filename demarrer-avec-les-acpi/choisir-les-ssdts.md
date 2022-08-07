# Choisir les SSDTs

## Quels SSDT chaque plateforme a besoin

Veuillez consulter la section ACPI spécifique de votre config.plist, tous les SSDT nécessaires y sont couverts avec un bref explicatif. Mais voici un très rapide.

* Quels SSDT chaque plateforme à besoin
  * PC Bureau
  * PC Bureau haut de gamme
  * PC Portable
* Création de ssdt

### PC Bureau <a href="#desktop" id="desktop"></a>

|       Plateformes      |                                                                     **CPU**                                                                     |    **EC**    |  **AWAC** | **NVRAM** |  **USB**  |
| :--------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------: | :----------: | :-------: | :-------: | :-------: |
|         Penryn         |                                                                       N/A                                                                       |    SSDT-EC   |    N/A    |    N/A    |    N/A    |
| Lynnfield et Clarkdale |                                                                        ^^                                                                       |      ^^      |     ^^    |     ^^    |     ^^    |
|       SandyBridge      | [CPU-PM](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#sandy-and-ivy-bridge-power-management) (Lancer en post-installaton) |      ^^      |     ^^    |     ^^    |     ^^    |
|       Ivy Bridge       |                                                                        ^^                                                                       |      ^^      |     ^^    |     ^^    |     ^^    |
|         Haswell        |                                                                    SSDT-PLUG                                                                    |      ^^      |     ^^    |     ^^    |     ^^    |
|        Broadwell       |                                                                        ^^                                                                       |      ^^      |     ^^    |     ^^    |     ^^    |
|         Skylake        |                                                                        ^^                                                                       | SSDT-EC-USBX |     ^^    |     ^^    |     ^^    |
|        Kaby Lake       |                                                                        ^^                                                                       |      ^^      |     ^^    |     ^^    |     ^^    |
|       Coffee Lake      |                                                                        ^^                                                                       |      ^^      | SSDT-AWAC |  SSDT-PMC |     ^^    |
|       Comet Lake       |                                                                        ^^                                                                       |      ^^      |     ^^    |    N/A    | SSDT-RHUB |
|      AMD (15/16h)      |                                                                       N/A                                                                       |      ^^      |    N/A    |     ^^    |    N/A    |
|        AMD (17h)       |       [SSDT-CPUR pour B550 et A520](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml)       |      ^^      |     ^^    |     ^^    |     ^^    |

### High End Desktop

|      Plateforme     |  **CPU**  |    **EC**    |     **RTC**     |  **PCI** |
| :-----------------: | :-------: | :----------: | :-------------: | :------: |
| Nehalem et Westmere |    N/A    |    SSDT-EC   |       N/A       |    N/A   |
|    Sandy Bridge-E   |     ^^    |      ^^      |        ^^       | SSDT-UNC |
|     Ivy Bridge-E    |     ^^    |      ^^      |        ^^       |    ^^    |
|      Haswell-E      | SSDT-PLUG | SSDT-EC-USBX | SSDT-RTC0-RANGE |    ^^    |
|     Broadwell-E     |     ^^    |      ^^      |        ^^       |    ^^    |
|      Skylake-X      |     ^^    |      ^^      |        ^^       |    N/A   |

### Laptop

|              Plateformes              |                                                                      **CPU**                                                                     |    **EC**    | **Backlight** |                  **I2C Trackpad**                 |  **AWAC** |  **USB**  |  **IRQ** |
| :-----------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------: | :----------: | :-----------: | :-----------------------------------------------: | :-------: | :-------: | :------: |
|        Clarksfield et Arrandale       |                                                                        N/A                                                                       |    SSDT-EC   |   SSDT-PNLF   |                        N/A                        |    N/A    |    N/A    | IRQ SSDT |
|              SandyBridge              | [CPU-PM](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#sandy-and-ivy-bridge-power-management) (lancer en post-installation) |      ^^      |       ^^      |                         ^^                        |     ^^    |     ^^    |    ^^    |
|               Ivy Bridge              |                                                                        ^^                                                                        |      ^^      |       ^^      |                         ^^                        |     ^^    |     ^^    |    ^^    |
|                Haswell                |                                                                     SSDT-PLUG                                                                    |      ^^      |       ^^      | SSDT-XOSI/SSDT-GPI0 (Lancer en post-installation) |     ^^    |     ^^    |    ^^    |
|               Broadwell               |                                                                        ^^                                                                        |      ^^      |       ^^      |                         ^^                        |     ^^    |     ^^    |    ^^    |
|                Skylake                |                                                                        ^^                                                                        | SSDT-EC-USBX |       ^^      |                         ^^                        |     ^^    |     ^^    |    N/A   |
|               Kaby Lake               |                                                                        ^^                                                                        |      ^^      |       ^^      |                         ^^                        |     ^^    |     ^^    |    ^^    |
| Coffee Lake (8th Gen) et Whiskey Lake |                                                                        ^^                                                                        |      ^^      |       ^^      |                         ^^                        | SSDT-AWAC |     ^^    |    ^^    |
|         Coffee Lake (9th Gen)         |                                                                        ^^                                                                        |      ^^      |       ^^      |                         ^^                        |     ^^    |     ^^    |    ^^    |
|               Comet Lake              |                                                                        ^^                                                                        |      ^^      |       ^^      |                         ^^                        |     ^^    |     ^^    |    ^^    |
|                Ice Lake               |                                                                        ^^                                                                        |      ^^      |       ^^      |                         ^^                        |     ^^    | SSDT-RHUB |    ^^    |

Continuatuon:

|               Platforms               | **NVRAM** |  **IMEI** |
| :-----------------------------------: | :-------: | :-------: |
|        Clarksfield et Arrandale       |    N/A    |    N/A    |
|              Sandy Bridge             |     ^^    | SSDT-IMEI |
|               Ivy Bridge              |     ^^    |     ^^    |
|                Haswell                |     ^^    |    N/A    |
|               Broadwell               |     ^^    |     ^^    |
|                Skylake                |     ^^    |     ^^    |
|               Kaby Lake               |     ^^    |     ^^    |
| Coffee Lake (8th Gen) et Whiskey Lake |     ^^    |     ^^    |
|         Coffee Lake (9th Gen)         |  SSDT-PMC |     ^^    |
|               Comet Lake              |    N/A    |     ^^    |
|                Ice Lake               |     ^^    |     ^^    |

### Direction page Suivante ->
