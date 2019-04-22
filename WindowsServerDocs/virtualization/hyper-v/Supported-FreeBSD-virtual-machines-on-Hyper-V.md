---
title: Unterstützte FreeBSD-Maschinen in Hyper-V
description: Enthält die Linux-Integrationsdienste und Features, die unterschiedlichen Versionen
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 930e758f-bd50-46b4-a3a4-9857110f17b4
author: shirgall
ms.author: kathydav
ms.date: 08/30/2017
ms.openlocfilehash: 013328953321bc66b3fd30759e5be321eea32dde
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824231"
---
# <a name="supported-freebsd-virtual-machines-on-hyper-v"></a>Unterstützte FreeBSD-Maschinen in Hyper-V

>Gilt für: Windows Server 2016 Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Die folgende Funktion Verteilung Karte gibt an, die Funktionen in der jeweiligen Version. Nach der Tabelle werden die bekannten Probleme und problemumgehungen für die einzelnen Verteilungspunkte aufgeführt.

## <a name="table-legend"></a>Tabellenlegende

* **Integrierte** -BIS (FreeBSD-Integration-Dienst) als Teil dieser FreeBSD-Version enthalten sind.

* &#10004;-Funktion

* (*leere*)-Funktion nicht verfügbar.

|**Funktion**|**Windows Server-Betriebssystemversion**|**11.1/11.2**|**11.0**|**10.3**|**10.2**|**10.0 - 10.1**|**9.1 - 9.3, 8.4**|
|-|-|-|-|-|-|-|-|
|**Verfügbarkeit**||Erstellt|Erstellt|Erstellt|Erstellt|Erstellt|[Ports](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) |
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_core)**|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; |
|Windows Server 2016 – genaue Uhrzeit|2016|&#10004;||||||
|**[Netzwerkfunktionen](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Networking)**||||||||
|Großrahmen|2016, 2012 R2, 2012, 2008 R2|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|
|VLAN-Kennzeichnung und trunking|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Livemigration|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injection|2016, 2012 R2, 2012|&#10004;Anhang 4|&#10004;Anhang 4|&#10004;Anhang 4|&#10004;Anhang 4|&#10004;Anhang 4|&#10004;|
|vRSS|2016, 2012 R2|&#10004;|&#10004;|||||
|Segmentierung von TCP und Prüfsumme Abladungen|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|Large Offload (LRO) empfangen|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;||||
|SR-IOV|2016|||||||
|**[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Storage)**||Hinweis 1|Hinweis 1|Hinweis 1|Hinweis 1|Beachten Sie 1,2|Beachten Sie 1,2|
|VHDX resize|2016, 2012 R2|&#10004;Beachten Sie 7|&#10004;Beachten Sie 7|||||
|Virtueller Fibre Channel|2016, 2012 R2|||||||
|VM-Sicherung|2016, 2012 R2|&#10004;||||||
|TRIM-Unterstützung|2016, 2012 R2|&#10004;||||||
|SCSI WWN|2016, 2012 R2|||||||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Memory)**||||||||
|Kernel-Unterstützung für PAE|2016, 2012 R2, 2012, 2008 R2|||||||
|Konfiguration der MMIO-Lücke|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher - Hot-Add-|2016, 2012 R2, 2012|||||||
|Dynamische Speichererweiterungsfunktion-|2016, 2012 R2, 2012|||||||
|Laufzeitspeichers|2016|||||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Video)**||||||||
|Hyper-V-spezifischen Videogerät|2016, 2012 R2, 2012, 2008 R2|||||||
|**[Sonstige](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Misc)**||||||||
|Schlüssel/Wert-Paar|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;Hinweis 6|&#10004;Hinweis 5, 6|&#10004;Hinweis 6|
|Nicht maskierbarer Interrupt|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Kopieren von Dateien vom Host zum Gast|2016, 2012 R2|||||||
|Lsvmbus-Befehl|2016, 2012 R2, 2012, 2008 R2|||||||
|Hyper-V-Sockets|2016|||||||
|PCI-Pass-Through-/ DDA|2016|&#10004;||||||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_gen2)**||||||||
|Mit UEFI Boot|2016, 2012 R2|&#10004;||||||
|Sicherer Start|2016|||||||

## <a name="BKMK_notes"></a>Anmerkungen zu dieser Version

1. Zum vorschlagen [Bezeichnung Datenträgergeräte]( https://www.freebsd.org/doc/handbook/geom-glabel.html) ROOT-bereitstellen-Fehler vermieden werden, während des Starts.

2. Das virtuelle DVD-Laufwerk kann nicht erkannt, wenn BIS Treiber auf FreeBSD geladen werden 8.x und 9.x, wenn Sie die legacy-ATA-Treiber durch den folgenden Befehl aktivieren.
    ```sh
    # echo ‘hw.ata.disk_enable=1’ >> /boot/loader.conf
    # shutdown -r now
    ```

3. 9126 ist, dass die maximale MTU-Größe unterstützt.

4. Sie können nicht in einem failoverszenario umzugehen eine statische IPv6-Adresse in den Replikatserver festgelegt. Verwenden Sie stattdessen eine IPv4-Adresse.

5. KVP wird von Ports auf FreeBSD 10.0 bereitgestellt. Finden Sie unter den [FreeBSD 10.0 Ports](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) auf FreeBSD.org für Weitere Informationen.

6. KVP funktioniert möglicherweise nicht auf Windows Server 2008 R2.

7. Damit VHDX online Größenänderung ordnungsgemäß in FreeBSD 11.0 funktioniert, ist ein spezieller manueller Schritt erforderlich, um ein Problem GEOM in 11.0 und höher, behoben wird, nachdem der Host ändert die Größe der VHDX-Datenträger zu umgehen: Öffnen Sie den Datenträger für das Schreiben und Ausführen "Gpart recover" wie folgt.
    ```sh
    # dd if=/dev/da1 of=/dev/da1 count=0
    # gpart recover da1
    ```
**Zusätzliche Hinweise**: Die featurematrix aus 10 stabile und 11 stabile ist identisch mit FreeBSD 11.1-Version. Zusätzlich, FreeBSD 10.2 und früheren Versionen (10.1, 10.0, 9.x, 8.x) sind Ende ihrer Lebensdauer. Finden Sie unter [hier](https://security.freebsd.org/) für eine aktuelle Liste der unterstützten Versionen und die neuesten sicherheitsempfehlungen.

**Zusätzliche Hinweise**: Die featurematrix aus 10 stabile und 11 stabile ist identisch mit FreeBSD 11.1-Version. Zusätzlich, FreeBSD 10.2 und früheren Versionen (10.1, 10.0, 9.x, 8.x) sind Ende ihrer Lebensdauer. Finden Sie unter [hier](https://security.freebsd.org/) für eine aktuelle Liste der unterstützten Versionen und die neuesten sicherheitsempfehlungen.

## <a name="see-also"></a>Siehe auch

* [Eine Beschreibung für Linux und FreeBSD-VMs auf Hyper-V-Funktion](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)
* [Bewährte Methoden für die Ausführung von FreeBSD in Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
