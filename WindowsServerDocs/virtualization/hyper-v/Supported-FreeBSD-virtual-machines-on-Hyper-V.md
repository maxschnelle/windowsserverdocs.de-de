---
title: Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V
description: Listet die in jeder Version enthaltenen Linux-Integrationsdienste und-Funktionen auf.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 930e758f-bd50-46b4-a3a4-9857110f17b4
author: shirgall
ms.author: kathydav
ms.date: 08/30/2017
ms.openlocfilehash: b7b02e1ec93d6255412a89e7e7d7b8246cf5e50e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365511"
---
# <a name="supported-freebsd-virtual-machines-on-hyper-v"></a>Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V

>Gilt für: Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7,1, Windows 7

Die folgende featureverteilungszuordnung gibt die Features in den einzelnen Versionen an. Die bekannten Probleme und Problem Umgehungen für die einzelnen Verteilungen werden nach der Tabelle aufgelistet.

## <a name="table-legend"></a>Tabellen Legende

* **Integrierte in** -bis (FreeBSD Integration Service) sind als Teil dieses FreeBSD-Release enthalten.

* &#10004;-Feature verfügbar

* (*leer*): Feature nicht verfügbar

|**Funktion**|**Windows Server-Betriebssystemversion**|**11.1/11.2**|**11,0**|**10,3**|**10,2**|**10,0-10,1**|**9,1-9,3, 8,4**|
|-|-|-|-|-|-|-|-|
|**Verfügbarkeit**||Integriert|Integriert|Integriert|Integriert|Integriert|[Landungen](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) |
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; |
|Windows Server 2016 genaue Zeit|2019, 2016|&#10004;||||||
|**[Ungs](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Großrahmen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|
|VLAN-Tagging und-Abschneiden|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Livemigration|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injektion|2019, 2016, 2012 R2, 2012|&#10004;Hinweis 4|&#10004;Hinweis 4|&#10004;Hinweis 4|&#10004;Hinweis 4|&#10004;Hinweis 4|&#10004;|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|||||
|TCP-Segmentierung und Prüfsummen Offloads|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|Große Empfangs Abladung (LRO)|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;||||
|SR-IOV|2019, 2016|||||||
|**[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||Hinweis 1|Hinweis 1|Hinweis 1|Hinweis 1|Hinweis 1, 2|Hinweis 1, 2|
|Vhdx-Größe ändern|2019, 2016, 2012 R2|&#10004;Hinweis 7|&#10004;Hinweis 7|||||
|Virtueller Fibre Channel|2019, 2016, 2012 R2|||||||
|Sicherung virtueller Computer|2019, 2016, 2012 R2|&#10004;||||||
|Trim-Unterstützung|2019, 2016, 2012 R2|&#10004;||||||
|SCSI-WWN|2019, 2016, 2012 R2|||||||
|**[Gedenkens](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**||||||||
|Unterstützung für den unterstützten Kernel|2019, 2016, 2012 R2, 2012, 2008 R2|||||||
|MMIO-Lücke konfigurieren|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher-Hot-Add|2019, 2016, 2012 R2, 2012|||||||
|Dynamischer Arbeitsspeicher-Ballooning|2019, 2016, 2012 R2, 2012|||||||
|Größenänderung des Lauf Zeit Speichers|2019, 2016|||||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||||
|Hyper-V-spezifisches Videogerät|2019, 2016, 2012 R2, 2012, 2008 R2|||||||
|**[Verschiedensten](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||||
|Schlüssel-Wert-Paar|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;Hinweis 6|&#10004;Hinweis 5, 6|&#10004;Hinweis 6|
|Nicht mastbare Unterbrechung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dateikopie von Host zu Gast|2019, 2016, 2012 R2|||||||
|lsvmbus-Befehl|2019, 2016, 2012 R2, 2012, 2008 R2|||||||
|Hyper-V-Sockets|2019, 2016|||||||
|PCI-Passthrough/DDA|2019, 2016|&#10004;||||||
|**[Virtuelle Maschinen der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**||||||||
|Starten mithilfe von UEFI|2019, 2016, 2012 R2|&#10004;||||||
|Sicherer Start|2019, 2016|||||||

## <a name="BKMK_notes"></a>Anmerkungen

1. Legen Sie fest, dass Datenträger [Geräte beschriftet]( https://www.freebsd.org/doc/handbook/geom-glabel.html) werden sollen, um den Fehler beim Starten der Stamm

2. Das virtuelle DVD-Laufwerk wird möglicherweise nicht erkannt, wenn bis-Treiber auf FreeBSD 8. x und 9. x geladen werden, es sei denn, Sie aktivieren den Legacy-ATA-Treiber über den folgenden Befehl.
    ```sh
    # echo ‘hw.ata.disk_enable=1' >> /boot/loader.conf
    # shutdown -r now
    ```

3. 9126 ist die maximal unterstützte MTU-Größe.

4. In einem failoverszenario ist es nicht möglich, eine statische IPv6-Adresse auf dem Replikat Server festzulegen. Verwenden Sie stattdessen eine IPv4-Adresse.

5. KVP wird von Ports auf FreeBSD 10,0 bereitgestellt. Weitere Informationen finden Sie in den [FreeBSD 10,0-Ports](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) auf FreeBSD.org.

6. KVP funktioniert möglicherweise nicht unter Windows Server 2008 R2.

7. Damit die Größe von vhdx Online in FreeBSD 11,0 ordnungsgemäß funktioniert, ist ein spezieller manueller Schritt erforderlich, um einen Geom-Fehler zu umgehen, der in 11.0 + behoben ist, nachdem der Host die Größe des vhdx-Datenträgers geändert hat: Öffnen Sie den Datenträger zum Schreiben, und führen Sie "gpart Recover" wie folgt aus.
    ```sh
    # dd if=/dev/da1 of=/dev/da1 count=0
    # gpart recover da1
    ```
   **Weitere Hinweise**: Die Featurematrix von 10 stabilen und 11 stabilen ist mit der Version FreeBSD 11,1 identisch. Außerdem sind FreeBSD 10,2 und frühere Versionen (10,1, 10,0, 9. x, 8. x) das Ende der Lebensdauer. [Hier](https://security.freebsd.org/) finden Sie eine aktuelle Liste der unterstützten Releases und die neuesten Sicherheitsempfehlungen.

**Weitere Hinweise**: Die Featurematrix von 10 stabilen und 11 stabilen ist mit der Version FreeBSD 11,1 identisch. Außerdem sind FreeBSD 10,2 und frühere Versionen (10,1, 10,0, 9. x, 8. x) das Ende der Lebensdauer. [Hier](https://security.freebsd.org/) finden Sie eine aktuelle Liste der unterstützten Releases und die neuesten Sicherheitsempfehlungen.

## <a name="see-also"></a>Siehe auch

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)
* [Bewährte Methoden für die Ausführung von FreeBSD unter Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
