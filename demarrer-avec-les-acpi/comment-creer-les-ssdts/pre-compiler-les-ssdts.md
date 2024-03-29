# Pré-Compiler les SSDTs

Détectez simplement le type et la génération de votre matériel, puis téléchargez les fichiers. Une fois téléchargés, placez les dans votre EFI dans EFI/OC/ACPI puis retournez vers [config.plist](https://dortania.github.io/OpenCore-Install-Guide/config.plist/).

* SSDT PC Bureau Intel
  * Penryn, Lynnfield etClarkdale
  * Sandy et Ivy Bridge
  * Haswell et Broadwell
  * Skylake et Kaby Lake
  * Coffee Lake
  * Comet Lake
* SSDT PC Portables intel
  * Clarksfield et Arrandale
  * Sandy et Ivy Bridge
  * Haswell et Broadwell
  * Skylake et Kaby Lake
  * Coffee Lake(8e gen)
  * Coffee et Comet Lake(9e et 10e gen)
  * Ice Lake
* SSDT Intel HEDT
  * Nehalem et Westmere
  * Sandy et Ivy Bridge-E
  * Haswell et Broadwell-E
  * Skylake et Cascade Lake-X/W
* SSDT AMD
  * Bulldozer/Jaguar
  * Zen

### SSDT PC Bureau Intel

* Penryn, Lynnfield et Clarkdale
* Sandy et Ivy Bridge
* Haswell et Broadwell
* Skylake et Kaby Lake
* Coffee Lake
* Comet Lake

#### PC Bureau Penryn, Lynnfield and Clarkdale

<details>

<summary>SSDT Nécessaires</summary>

* [SSDT-EC-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-DESKTOP.aml)

Une fois téléchargés, placez les dans votre EFI dans EFI/OC/ACPI et retournez au guide d'installation

* [config.plist](pre-compiler-les-ssdts.md#intel-desktop-ssdts)

</details>

Infos plus en profondeur sur les SSDTs :

SSDT-EC:

* Utilisé pour désactiver votre réel contrleur embarqué et en faire un faux pour que macOS puisse jouer avec

#### Sandy et Ivy Bridge pour PC Bureau

::: tip SSDTs required

<details>

<summary>SSDT Nécessaires</summary>

* [SSDT-EC-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-DESKTOP.aml)
* [SSDT-IMEI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-IMEI.aml)
  * nécessaire pour les CPU Sandy Bridge avec des carte mères de série 7
    * ex: B75, Q75, Z75, H77, Q77, Z77
  * nécessaire pour les CPU Ivy Bridge avec des carte mères de série 6
    * ex: H61, B65, Q65, P67, H67, Q67, Z68

Une fois téléchargé, mettez les dans votre dossier EFI sous EFI/OC/ACPI et direction le guide d'installation

* [Configuration des config.plist](broken-reference)

</details>

* [SSDT-EC-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-DESKTOP.aml)
* [SSDT-IMEI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-IMEI.aml)
  * Required for Sandy Bridge CPU with 7 series motherboard
    * ie. B75, Q75, Z75, H77, Q77, Z77
  * Required Ivy Bridge CPU with 6 series motherboard
    * ie. H61, B65, Q65, P67, H67, Q67, Z68

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

::: ::: details In-depth info on the SSDTs

SSDT-EC:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with

SSDT-IMEI

* Used for creating an IMEI device when one is not present in ACPI\\
  * Required for Sandy Bridge CPU with 7 series motherboard
    * ie. B75, Q75, Z75, H77, Q77, Z77
  * Required Ivy Bridge CPU with 6 series motherboard
    * ie. H61, B65, Q65, P67, H67, Q67, Z68

:::

#### Desktop Haswell and Broadwell

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-DESKTOP.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with

:::

#### Desktop Skylake and Kaby Lake

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-USBX-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

:::

#### Desktop Coffee Lake

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-USBX-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)
* [SSDT-AWAC](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-AWAC.aml)
* [SSDT-PMC](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PMC.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

SSDT-AWAC:

* Used to enable the legacy RTC clock in macOS, as the newer AWAC clock is unsupported

SSDT-PMC:

* Used to enable native NVRAM on "true" 300 series motherboards
  * ie. B360, B365, H310, H370, Z390
  * Note Z370 is not included

:::

#### Desktop Comet Lake

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-USBX-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)
* [SSDT-AWAC](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-AWAC.aml)
* [SSDT-RHUB](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-RHUB.aml)
  * Specifically for Asus's 400 series motherboards, Gigabyte and others do not need SSDT-RHUB

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

SSDT-AWAC:

* Used to enable the legacy RTC clock in macOS, as the newer AWAC clock is unsupported

SSDT-RHUB:

* Used to reset USB controllers on Asus's 400 series motherboards due to poor ACPI implementation from the OEM
  * Note Gigabyte, MSI, AsRock, etc do not need this SSDT. Only Asus

:::

### Intel Laptop SSDTs

#### Laptop Clarksfield and Arrandale

::: tip SSDTs required

* [SSDT-EC-LAPTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-LAPTOP.aml)
* [SSDT-PNLF](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)
* [SSDT-XOSI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-EC:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with

SSDT-PNLF:

* Used for controlling the backlight on internal displays such as AIOs and laptops

SSDT-XOSI:

* Enables many Windows-only functionality in macOS
  * Requires XOSI patch(covered later on)

:::

#### Laptop Sandy and Ivy Bridge

::: tip SSDTs required

* [SSDT-EC-LAPTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-LAPTOP.aml)
* [SSDT-IMEI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-IMEI.aml)
  * Required for Sandy Bridge CPU with 7 series motherboard
    * ie. B75, Q75, Z75, H77, Q77, Z77
  * Required Ivy Bridge CPU with 6 series motherboard
    * ie. H61, B65, Q65, P67, H67, Q67, Z68
* [SSDT-PNLF](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)
* [SSDT-XOSI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

::: ::: details In-depth info on the SSDTs

SSDT-EC:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with

SSDT-IMEI

* Used for creating an IMEI device when one is not present in ACPI
  * Required for Sandy Bridge CPU with 7 series motherboard
    * ie. B75, Q75, Z75, H77, Q77, Z77
  * Required Ivy Bridge CPU with 6 series motherboard
    * ie. H61, B65, Q65, P67, H67, Q67, Z68

SSDT-PNLF:

* Used for controlling the backlight on internal displays such as AIOs and laptops

SSDT-XOSI:

* Enables many Windows-only functionality in macOS
  * Requires XOSI patch(covered later on)

:::

#### Laptop Haswell and Broadwell

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-LAPTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-LAPTOP.aml)
* [SSDT-PNLF](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)
* [SSDT-XOSI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with

SSDT-PNLF:

* Used for controlling the backlight on internal displays such as AIOs and laptops

SSDT-XOSI:

* Enables many Windows-only functionality in macOS
  * Requires XOSI patch(covered later on)

:::

#### Laptop Skylake and Kaby Lake

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-USBX-LAPTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-LAPTOP.aml)
* [SSDT-PNLF](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)
* [SSDT-XOSI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

SSDT-PNLF:

* Used for controlling the backlight on internal displays such as AIOs and laptops

SSDT-XOSI:

* Enables many Windows-only functionality in macOS
  * Requires XOSI patch(covered later on)

:::

#### Laptop Coffee Lake(8th gen)

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-USBX-LAPTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-LAPTOP.aml)
* [SSDT-AWAC](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-AWAC.aml)
* [SSDT-PNLF](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)
* [SSDT-XOSI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

SSDT-AWAC:

* Used to enable the legacy RTC clock in macOS, as the newer AWAC clock is unsupported

SSDT-PNLF:

* Used for controlling the backlight on internal displays such as AIOs and laptops

SSDT-XOSI:

* Enables many Windows-only functionality in macOS
  * Requires XOSI patch(covered later on)

:::

#### Laptop Coffee and Comet Lake(9th and 10th gen)

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-USBX-LAPTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-LAPTOP.aml)
* [SSDT-AWAC](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-AWAC.aml)
* [SSDT-PMC](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PMC.aml)
  * Only for 9th gen laptops, 10th gen can ignore
* [SSDT-PNLF](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)
* [SSDT-XOSI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

SSDT-AWAC:

* Used to enable the legacy RTC clock in macOS, as the newer AWAC clock is unsupported

SSDT-PMC:

* Used to enable native NVRAM on "true" 300 series motherboards
  * Only for 9th gen laptops

SSDT-PNLF:

* Used for controlling the backlight on internal displays such as AIOs and laptops

SSDT-XOSI:

* Enables many Windows-only functionality in macOS
  * Requires XOSI patch(covered later on)

:::

#### Laptop Ice Lake

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-USBX-LAPTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-LAPTOP.aml)
* [SSDT-AWAC](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-AWAC.aml)
* [SSDT-RHUB](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-RHUB.aml)
* [SSDT-PNLF](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)
* [SSDT-XOSI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

SSDT-AWAC:

* Used to enable the legacy RTC clock in macOS, as the newer AWAC clock is unsupported

SSDT-RHUB:

* Used to reset USB controllers on Ice Lake laptops due to poor OEM ACPI implementation
  * Mainly seen on Dell laptops

SSDT-PNLF:

* Used for controlling the backlight on internal displays such as AIOs and laptops

SSDT-XOSI:

* Enables many Windows-only functionality in macOS
  * Requires XOSI patch(covered later on)

:::

### Intel HEDT SSDTs

#### Nehalem and Westmere

::: tip SSDTs required

* [SSDT-EC-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-DESKTOP.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-EC:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with

:::

#### Sandy and Ivy Bridge-E

::: tip SSDTs required

* [SSDT-EC-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-DESKTOP.aml)
* [SSDT-UNC0](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-UNC0.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-EC:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with

SSDT-UNC0:

* Used to ensure unused or missing uncore bridges are properly disabled, otherwise kernel panic in IOPCIFamily in macOS Big Sur

:::

#### Haswell and Broadwell-E

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-USBX-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)
* [SSDT-RTC0-RANGE-HEDT](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-RTC0-RANGE-HEDT.aml)
* [SSDT-UNC0](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-UNC0.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

SSDT-RTC0-RANGE-HEDT:

* Used to enable the legacy RTC clock in macOS, as the newer AWAC clock is unsupported
  * Added benefit is to resolve early halts in macOS Big Sur's booting due to poor ACPI implementation

SSDT-UNC0:

* Used to ensure unused or missing uncore bridges are properly disabled, otherwise kernel panic in IOPCIFamily in macOS Big Sur

:::

#### Skylake and Cascade Lake-X/W

::: tip SSDTs required

* [SSDT-PLUG-DRTNIA](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
* [SSDT-EC-USBX-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)
* [SSDT-RTC0-RANGE-HEDT](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-RTC0-RANGE-HEDT.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-PLUG:

* Used for enabling Apple's XCPM in macOS, allowing for far better CPU power management

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

SSDT-RTC0-RANGE-HEDT:

* Used to enable the legacy RTC clock in macOS, as the newer AWAC clock is unsupported
  * Added benefit is to resolve early halts in macOS Big Sur's booting due to poor ACPI implementation

:::

### AMD SSDTs

#### AMD Bulldozer/Jaguar

::: tip SSDTs required

* [SSDT-EC-USBX-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

:::

#### AMD Zen

::: tip SSDTs required

* [SSDT-EC-USBX-DESKTOP](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)
* [SSDT-CPUR](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml)
  * Only required for B550, A520 and newer
    * X570 and older **DO NOT** need SSDT-CPUR
    * No threadripper machines need this either

Once downloaded, place them into your EFI folder under EFI/OC/ACPI and head back to the install guide

* [config.plist Setup](https://dortania.github.io/OpenCore-Install-Guide/config.plist/)

:::

::: details In-depth info on the SSDTs

SSDT-EC-USBX:

* Used for disabling your real Embedded controller and creating a fake one for macOS to play with
* USBX portion is used for injection USB power properties missing on Skylake and newer

SSDT-CPUR:

* Used for fixing CPU definitions in ACPI, as macOS does not properly support the ACPI used in B550 and newer boards

:::
