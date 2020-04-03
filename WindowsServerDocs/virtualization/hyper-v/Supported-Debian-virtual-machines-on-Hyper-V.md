---
title: Unterstützte virtuelle Debian-Computer auf Hyper-V
description: Listet die in jeder Version enthaltenen Linux-Integrationsdienste und-Funktionen auf.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cc62c10-02a3-4633-960c-23bf91a45bd5
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 7a717acf5c132d68d6ee041aeb5af5a430aa171b
ms.sourcegitcommit: 9f7cc76b8c9add44dcbbd97f77b4f881d5a2c073
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2020
ms.locfileid: "80613003"
---
# <a name="supported-debian-virtual-machines-on-hyper-v"></a>Unterstützte virtuelle Debian-Computer auf Hyper-V

>Gilt für: Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7,1, Windows 7

Die folgende featureverteilungskarte gibt die Funktionen an, die in den einzelnen Versionen vorhanden sind. Die bekannten Probleme und Problem Umgehungen für die einzelnen Verteilungen werden nach der Tabelle aufgelistet.

## <a name="table-legend"></a>Tabellen Legende

* **Integrierte** -LIS sind als Teil dieser Linux-Distribution enthalten. Das von Microsoft bereitgestellte LIS-Downloadpaket funktioniert für diese Verteilung nicht. Installieren Sie es also nicht. Die Kernel-Modul Versionsnummern für die integrierten Lis (z. **b. lsmod**) unterscheiden sich von der Versionsnummer des von Microsoft bereitgestellten LIS-Download Pakets. Ein Konflikt weist nicht darauf hin, dass der integrierte LIS veraltet ist.

* &#10004;-Feature verfügbar

* (*leer*): Feature nicht verfügbar

| **Feature**                                                                                                                                  | **Windows Server-Betriebssystemversion** | **10.0-10.3 (Buster)** | **9.0-9.12 (Stretch)** | **8.0-8.11 (Jessie)** | **7.0-7.11 (Wheezy)** |
|----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------|-----------------------|-----------------------|-----------------------|-----------------------|
| **Verfügbarkeit**                                                                                                                             |                                             | Integriert              | Integriert              | Integriert              | Integriert (Notiz 6)     |
| **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                                                   | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Windows Server 2016 genaue Zeit                                                                                                            | 2019, 2016                                  | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| **[Ungs](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                                       |                                             |                       |                       |                       |                       |
| Großrahmen                                                                                                                                 | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| VLAN-Tagging und-Abschneiden                                                                                                                    | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Livemigration                                                                                                                               | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Statische IP-Injektion                                                                                                                          | 2019, 2016, 2012 R2, 2012                   |                       |                       |                       |                       |
| vRSS                                                                                                                                         | 2019, 2016, 2012 R2                         | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| TCP-Segmentierung und Prüfsummen Offloads                                                                                                       | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| SR-IOV                                                                                                                                       | 2019, 2016                                  | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| **[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                                             |                                             |                       |                       |                       |                       |
| Vhdx-Größe ändern                                                                                                                                  | 2019, 2016, 2012 R2                         | &#10004;Hinweis 1       | &#10004;Hinweis 1       | &#10004;Hinweis 1       | &#10004;Hinweis 1       |
| Virtueller Fibre Channel                                                                                                                        | 2019, 2016, 2012 R2                         |                       |                       |                       |                       |
| Sicherung virtueller Computer                                                                                                                  | 2019, 2016, 2012 R2                         | &#10004;Hinweis 4, 5     | &#10004;Hinweis 4, 5     | &#10004;Hinweis 4, 5     | &#10004;Hinweis 4       |
| Trim-Unterstützung                                                                                                                                 | 2019, 2016, 2012 R2                         | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| SCSI-WWN                                                                                                                                     | 2019, 2016, 2012 R2                         | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| **[Gedenkens](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                                               |                                             |                       |                       |                       |                       |
| Unterstützung für den unterstützten Kernel                                                                                                                           | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| MMIO-Lücke konfigurieren                                                                                                                    | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Dynamischer Arbeitsspeicher-Hot-Add                                                                                                                     | 2019, 2016, 2012 R2, 2012                   | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| Dynamischer Arbeitsspeicher-Ballooning                                                                                                                  | 2019, 2016, 2012 R2, 2012                   | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| Größenänderung des Lauf Zeit Speichers                                                                                                                        | 2019, 2016                                  | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                                                 |                                             |                       |                       |                       |                       |
| Hyper-V-spezifisches Videogerät                                                                                                                | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              |                       |
| **[Verschiedensten](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                                 |                                             |                       |                       |                       |                       |
| Schlüssel-Wert-Paar                                                                                                                               | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;Hinweis 4       | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |
| Nicht mastbare Unterbrechung                                                                                                                       | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              |                       |
| Dateikopie von Host zu Gast                                                                                                                 | 2019, 2016, 2012 R2                         | &#10004;Hinweis 4       | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |
| lsvmbus-Befehl                                                                                                                              | 2019, 2016, 2012 R2, 2012, 2008 R2          |                       |                       |                       |                       |
| Hyper-V-Sockets                                                                                                                              | 2019, 2016                                  | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| PCI-Passthrough/DDA                                                                                                                          | 2019, 2016                                  | &#10004;Notiz 8       | &#10004;Notiz 8       |                       |                       |
| **[Virtuelle Maschinen der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                             |                       |                       |                       |                       |
| Starten mithilfe von UEFI                                                                                                                              | 2019, 2016, 2012 R2                         | &#10004;Hinweis 7       | &#10004;Hinweis 7       | &#10004;Hinweis 7       |                       |
| Sicherer Start                                                                                                                                  | 2019, 2016                                  | &#10004;              |                       |                       |                       |


## <a name="notes"></a><a name="BKMK_notes"></a>Anmerkungen

1. Das Erstellen von Dateisystemen auf VHDs, die größer als 2 TB sind, wird nicht unterstützt.

2. Auf Windows Server 2008 R2-SCSI-Datenträgern werden 8 verschiedene Einträge in/dev/sd * erstellt.

3. Windows Server 2012 R2 bei einem virtuellen Computer mit mindestens 8 Kernen werden alle Interrupts an eine einzelne vCPU weitergeleitet.

4. Ab Debian 8,3 enthält das manuell installierte Debian-Paket "HyperV-Daemons" die Schlüssel-Wert-Paare, fCopy und VSS-Daemons. Unter Debian 7. x und 8.0-8.2 muss das HyperV-Daemons-Paket von den [debian-backports](https://wiki.debian.org/Backports)stammen.

5. Die Live Sicherung virtueller Computer funktioniert nicht mit den ext2-Dateisystemen. Das Standardlayout, das durch das Debian-Installationsprogramm erstellt wird, umfasst "ext2 Filesystems"

6. Während Debian 7. x nicht unterstützt wird und einen älteren Kernel verwendet, hat der Kernel, der in den [debian-backports](https://wiki.debian.org/Backports) für Debian 7. x enthalten ist, die Hyper-V-Funktionen verbessert.

7. Auf virtuellen Computern der Windows Server 2012 R2-Generation 2 ist der sichere Start standardmäßig aktiviert, und einige virtuelle Linux-Computer werden erst gestartet, wenn die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Abschnitt **Firmware** der Einstellungen für den virtuellen Computer im **Hyper-V-Manager** deaktivieren, oder Sie können ihn mithilfe von PowerShell deaktivieren:

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```
8. Die neuesten upstreamkernel-Funktionen sind nur verfügbar, wenn der mit dem Kernel enthaltene [debian-backports](https://wiki.debian.org/Backports)verwendet wird.

Siehe auch

* [Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle SuSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Ubuntu-Computer auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux unter Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)
