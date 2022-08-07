# Démarrer avec les ACPI

### Explication rapide sur les ACPI

Alors c'est quoi les DSDTs et les SSDTS ? Eh bien, ce sont des tables présentes dans votre logiciel qui gèrent le matériel tel que les controlleurs USB, les coeurs logiques CPU, les controlleurs embarqués, horloges système et bien d'autre.

Un DSDT (Differentiated System Description Table en anglayyyyyy) peut être vu comme le corps qui tiens la plupart des infos avec des plus petites infos qui sont passés dans les SSDT (Secondary System Description Table). Vous pouvez penser que les DSDT en tant que plans de construction, les SSDT étant des notes autocollantes décrivant des détails supplémentaires sur le projet



Plus sur les ACPI/DSDT/SSDT: [ACPI 6.4 Manual](https://uefi.org/sites/default/files/resources/ACPI\_Spec\_6\_4\_Jan22.pdf)

> Alors pourquoi on s'en soucie ?

macOS peut être très pointilleux sur les appareils présents dans le DSDT et notre travail consiste donc à le corriger. Les principaux appareils qui doivent être corrigés pour que macOS fonctionne correctement :

* Controlleurs Embraqués (EC)
  * Toutes les machines Intel semi-modernes ont un EC (généralement appelé H\_EC, ECDV, EC0, etc...) exposé dans leur DSDT, de nombreux systèmes AMD l'ayant également exposé. Ces contrôleurs ne sont généralement pas compatibles avec macOS et peuvent provoquer des paniques, ils doivent donc être cachés à macOS. macOS Catalina nécessite cependant la présence d'un appareil nommé EC, donc un EC factice est créé.
* Type de plugin
  * Cela permet l'utilisation de XCPM fournissant une gestion native de l'alimentation du processeur sur les processeurs Intel Haswell et plus récents, le SSDT se connectera au premier thread du processeur. Non destiné à AMD
* Horloge système Awac.
  * Cela s'applique à toutes les cartes mères de la série 300, y compris de nombreuses cartes Z370, le problème spécifique est que les nouvelles cartes sont livrées avec l'horloge AWAC activée. C'est un problème car macOS ne peut pas communiquer avec les horloges AWAC, cela nous oblige donc à forcer l'horloge RTC héritée ou, si elle n'est pas disponible, à en créer une fausse pour que macOS puisse jouer avec
* NVRAM SSDT
  * Les vraies cartes mères de la série 300 (non-Z370) ne déclarent pas la puce FW comme MMIO dans ACPI et donc le noyau ignore la région MMIO déclarée par la carte mémoire UEFI. Ce SSDT ramène le support NVRAM
* &#x20;SSDT de rétroéclairage
  * Utilisé pour fixer la prise en charge du contrôle du rétroéclairage sur les ordinateurs portables
* GPIO SSDT
  * Utilisé pour créer un stub pour permettre à VoodooI2C de se connecter, pour les PC portables uniquement
* XOSI SSDT
  * Utilisé pour rediriger les appels OSI vers ce SSDT, principalement utilisé pour inciter notre matériel à penser qu'il démarre Windows afin d'obtenir une meilleure prise en charge du trackpad. Il s'agit d'une solution très hacky connue pour casser le démarrage de Windows, utilisez plutôt le GPIO SSDT. L'utilisation de XOSI ne sera pas abordée dans ce guide
*   Correctifs IRQ SSDT et ACPI

    * Nécessaire pour résoudre les conflits d'IRQ au sein du DSDT, principalement pour les ordinateurs portables. Exclusivité SSDTTime
    * Notez que Skylake et les systèmes plus récents ont rarement des conflits d'IRQ, ceci est principalement répandu sur Broadwell et plus anciens

    Maintenant Direction page suivante pour choisir les SSDT pour votre PC !
