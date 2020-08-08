---
title: Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V
description: Listet die in jeder Version enthaltenen Linux-Integrationsdienste und-Funktionen auf.
manager: dongill
ms.topic: article
ms.assetid: 930e758f-bd50-46b4-a3a4-9857110f17b4
author: shirgall
ms.author: kathydav
ms.date: 04/07/2020
ms.openlocfilehash: 3767c56640dd4e4e07e2cdd4a578ec0c3db2f470
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965637"
---
# <a name="supported-freebsd-virtual-machines-on-hyper-v"></a>Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V

>Gilt für: Windows Server 2019, Hyper-v Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows 10, Windows 8.1

Die folgende featureverteilungszuordnung gibt die Features in den einzelnen Versionen an. Die bekannten Probleme und Problem Umgehungen für die einzelnen Verteilungen werden nach der Tabelle aufgelistet.

## <a name="table-legend"></a>Tabellen Legende

* **Integrierte in** -bis (FreeBSD Integration Service) sind als Teil dieses FreeBSD-Release enthalten.

* &#10004;-Feature verfügbar

* (*leer*): Feature nicht verfügbar

|**Feature**|**Windows Server-Betriebssystemversion**|**12-12.1**|**11.1-11.3**|**11,0**|**10.3**|**10,2**|**10,0-10,1**|**9,1-9,3, 8,4**|
|-|-|-|-|-|-|-|-|-|
|**Verfügbarkeit**||Integriert|Integriert|Integriert|Integriert|Integriert|Integriert|[Ports](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) |
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 genaue Zeit|2019, 2016|&#10004;|&#10004;||||||
|**[Netzwerk](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Großrahmen|2019, 2016, 2012 R2|&#10004; Hinweis 3|&#10004; Hinweis 3|&#10004; Hinweis 3|&#10004; Hinweis 3|&#10004; Hinweis 3|&#10004; Hinweis 3|&#10004; Hinweis 3|
|VLAN-Tagging und-Abschneiden|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Livemigration|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injektion|2019, 2016, 2012 R2|&#10004; Hinweis 4|&#10004; Hinweis 4|&#10004; Hinweis 4|&#10004; Hinweis 4|&#10004; Hinweis 4|&#10004; Hinweis 4|&#10004;|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|||||
|TCP-Segmentierung und Prüfsummen Offloads|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|||
|Große Empfangs Abladung (LRO)|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||||
|SR-IOV|2019, 2016|&#10004;|&#10004;|&#10004;|||||
|**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||Note1|Hinweis 1|Hinweis 1|Hinweis 1|Hinweis 1|Hinweis 1, 2|Hinweis 1, 2|
|Vhdx-Größe ändern|2019, 2016, 2012 R2|&#10004; Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 6|||||
|Virtueller Fibre Channel|2019, 2016, 2012 R2||||||||
|Sicherung virtueller Computer|2019, 2016, 2012 R2|&#10004;|&#10004;||||||
|Trim-Unterstützung|2019, 2016, 2012 R2|&#10004;|&#10004;||||||
|SCSI-WWN|2019, 2016, 2012 R2||||||||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**|||||||||
|Unterstützung für den unterstützten Kernel|2019, 2016, 2012 R2||||||||
|MMIO-Lücke konfigurieren|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher-Hot-Add|2019, 2016, 2012 R2||||||||
|Dynamischer Arbeitsspeicher-Ballooning|2019, 2016, 2012 R2||||||||
|Größenänderung des Lauf Zeit Speichers|2019, 2016||||||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**|||||||||
|Hyper-V-spezifisches Videogerät|2019, 2016, 2012 R2||||||||
|**[Verschiedenes](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**|||||||||
|Schlüssel-Wert-Paar|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; Hinweis 5|&#10004;|
|Nicht mastbare Unterbrechung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dateikopie von Host zu Gast|2019, 2016, 2012 R2||||||||
|lsvmbus-Befehl|2019, 2016, 2012 R2||||||||
|Hyper-V-Sockets|2019, 2016||||||||
|PCI-Passthrough/DDA|2019, 2016|&#10004;|&#10004;||||||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**|||||||||
|Starten mithilfe von UEFI|2019, 2016, 2012 R2|&#10004;|&#10004;||||||
|Sicherer Start|2019, 2016||||||||

## <a name="notes"></a><a name="BKMK_notes"></a>Hinweise

1. Legen Sie fest, dass Datenträger [Geräte beschriftet]( https://www.freebsd.org/doc/handbook/geom-glabel.html) werden sollen, um den Fehler beim Starten der Stamm

2. Das virtuelle DVD-Laufwerk wird möglicherweise nicht erkannt, wenn bis-Treiber auf FreeBSD 8. x und 9. x geladen werden, es sei denn, Sie aktivieren den Legacy-ATA-Treiber über den folgenden Befehl.
    ```sh
    # echo ‘hw.ata.disk_enable=1' >> /boot/loader.conf
    # shutdown -r now
    ```

3. 9126 ist die maximal unterstützte MTU-Größe.

4. In einem failoverszenario ist es nicht möglich, eine statische IPv6-Adresse auf dem Replikat Server festzulegen. Verwenden Sie stattdessen eine IPv4-Adresse.

5. KVP wird von Ports auf FreeBSD 10,0 bereitgestellt. Weitere Informationen finden Sie in den [FreeBSD 10,0-Ports](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) auf FreeBSD.org.

6. Damit die Größe von vhdx Online in FreeBSD 11,0 ordnungsgemäß funktioniert, ist ein spezieller manueller Schritt erforderlich, um einen Geom-Fehler zu umgehen, der in 11.0 + behoben ist, nachdem der Host die Größe des vhdx-Datenträgers geändert hat: Öffnen Sie den Datenträger zum Schreiben, und führen Sie "gpart Recover" wie folgt aus.
    ```sh
    # dd if=/dev/da1 of=/dev/da1 count=0
    # gpart recover da1
    ```

**Weitere Hinweise**: die Featurematrix von 10 stabilen und 11 stabilen ist mit der Version FreeBSD 11,1 identisch. Außerdem sind FreeBSD 10,2 und frühere Versionen (10,1, 10,0, 9. x, 8. x) das Ende der Lebensdauer. [Hier](https://security.freebsd.org/) finden Sie eine aktuelle Liste der unterstützten Releases und die neuesten Sicherheitsempfehlungen.

## <a name="see-also"></a>Weitere Informationen

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)
* [Bewährte Methoden für die Ausführung von FreeBSD unter Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
