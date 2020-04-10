---
title: Unterstützte virtuelle Debian-Computer auf Hyper-V
description: Listet die in jeder Version enthaltenen Linux-Integrationsdienste und-Funktionen auf.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 3cc62c10-02a3-4633-960c-23bf91a45bd5
author: shirgall
ms.author: kathydav
ms.date: 04/07/2020
ms.openlocfilehash: e5483b9547e67414bd66b3daad1a4b07c3cb7cfc
ms.sourcegitcommit: 7b1ebc4934998af2472962ca8cce1c872f39946f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2020
ms.locfileid: "80994507"
---
# <a name="supported-debian-virtual-machines-on-hyper-v"></a>Unterstützte virtuelle Debian-Computer auf Hyper-V

>Gilt für: Windows Server 2019, Hyper-v Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows 10, Windows 8.1

Die folgende featureverteilungskarte gibt die Funktionen an, die in den einzelnen Versionen vorhanden sind. Die bekannten Probleme und Problem Umgehungen für die einzelnen Verteilungen werden nach der Tabelle aufgelistet.

## <a name="table-legend"></a>Tabellen Legende

* **Integrierte** -LIS sind als Teil dieser Linux-Distribution enthalten. Das von Microsoft bereitgestellte LIS-Downloadpaket funktioniert für diese Verteilung nicht. Installieren Sie es also nicht. Die Kernel-Modul Versionsnummern für die integrierten Lis (z. **b. lsmod**) unterscheiden sich von der Versionsnummer des von Microsoft bereitgestellten LIS-Download Pakets. Ein Konflikt weist nicht darauf hin, dass der integrierte LIS veraltet ist.

* &#10004;-Feature verfügbar

* (*leer*): Feature nicht verfügbar

| **Feature**                                                                                                                                  | **Windows Server-Betriebssystemversion** | **10.0-10.3 (Buster)** | **9.0-9.12 (Stretch)** | **8.0-8.11 (Jessie)** | **7.0-7.11 (Wheezy)** |
|----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------|-----------------------|-----------------------|-----------------------|-----------------------|
| **Verfügbarkeit**                                                                                                                             |                                             | Integriert              | Integriert              | Integriert              | Integriert (Notiz 5)     |
| **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                                                   | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Windows Server 2016 genaue Zeit                                                                                                            | 2019, 2016                                  | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| **[Ungs](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                                       |                                             |                       |                       |                       |                       |
| Großrahmen                                                                                                                                 | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| VLAN-Tagging und-Abschneiden                                                                                                                    | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Livemigration                                                                                                                               | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Statische IP-Injektion                                                                                                                          | 2019, 2016, 2012 R2                   |                       |                       |                       |                       |
| vRSS                                                                                                                                         | 2019, 2016, 2012 R2                         | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| TCP-Segmentierung und Prüfsummen Offloads                                                                                                       | 2019, 2016, 2012 R2          | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| SR-IOV                                                                                                                                       | 2019, 2016                                  | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| **[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                                             |                                             |                       |                       |                       |                       |
| Vhdx-Größe ändern                                                                                                                                  | 2019, 2016, 2012 R2                         | &#10004;Hinweis 1       | &#10004;Hinweis 1       | &#10004;Hinweis 1       | &#10004;Hinweis 1       |
| Virtueller Fibre Channel                                                                                                                        | 2019, 2016, 2012 R2                         |                       |                       |                       |                       |
| Sicherung virtueller Computer                                                                                                                  | 2019, 2016, 2012 R2                         | &#10004;Note2 | &#10004;Note2 | &#10004;Note2 | &#10004;Note2 |
| Trim-Unterstützung                                                                                                                                 | 2019, 2016, 2012 R2                         | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| SCSI-WWN                                                                                                                                     | 2019, 2016, 2012 R2                         | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| **[Gedenkens](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                                               |                                             |                       |                       |                       |                       |
| Unterstützung für den unterstützten Kernel                                                                                                                           | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| MMIO-Lücke konfigurieren                                                                                                                    | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Dynamischer Arbeitsspeicher-Hot-Add                                                                                                                     | 2019, 2016, 2012 R2                   | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| Dynamischer Arbeitsspeicher-Ballooning                                                                                                                  | 2019, 2016, 2012 R2                   | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| Größenänderung des Lauf Zeit Speichers                                                                                                                        | 2019, 2016                                  | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                                                 |                                             |                       |                       |                       |                       |
| Hyper-V-spezifisches Videogerät                                                                                                                | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              |                       |
| **[Verschiedensten](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                                 |                                             |                       |                       |                       |                       |
| Schlüssel-Wert-Paar                                                                                                                               | 2019, 2016, 2012 R2          | &#10004;Hinweis 2       | &#10004;Hinweis 2       | &#10004;Hinweis 2       |                       |
| Nicht mastbare Unterbrechung                                                                                                                       | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              |                       |
| Dateikopie von Host zu Gast                                                                                                                 | 2019, 2016, 2012 R2                         | &#10004;Hinweis 2       | &#10004;Hinweis 2       | &#10004;Hinweis 2       |                       |
| lsvmbus-Befehl                                                                                                                              | 2019, 2016, 2012 R2          |                       |                       |                       |                       |
| Hyper-V-Sockets                                                                                                                              | 2019, 2016                                  | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| PCI-Passthrough/DDA                                                                                                                          | 2019, 2016                                  | &#10004;Hinweis 4       | &#10004;Hinweis 4       |                       |                       |
| **[Virtuelle Maschinen der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                             |                       |                       |                       |                       |
| Starten mithilfe von UEFI                                                                                                                              | 2019, 2016, 2012 R2                         | &#10004;Hinweis 3       | &#10004;Hinweis 3       | &#10004;Hinweis 3       |                       |
| Sicherer Start                                                                                                                                  | 2019, 2016                                  | &#10004;              |                       |                       |                       |


## <a name="notes"></a>Hinweise

1. Das Erstellen von Dateisystemen auf VHDs, die größer als 2 TB sind, wird nicht unterstützt.

2. Ab Debian 8,3 enthält das manuell installierte Debian-Paket "HyperV-Daemons" die Schlüssel-Wert-Paare, fCopy und VSS-Daemons. Unter Debian 7. x und 8.0-8.2 muss das HyperV-Daemons-Paket von den [debian-backports](https://wiki.debian.org/Backports)stammen.

3. Auf virtuellen Computern der Windows Server 2012 R2-Generation 2 ist der sichere Start standardmäßig aktiviert, und einige virtuelle Linux-Computer werden erst gestartet, wenn die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Abschnitt **Firmware** der Einstellungen für den virtuellen Computer im **Hyper-V-Manager** deaktivieren, oder Sie können ihn mithilfe von PowerShell deaktivieren:

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
   ```
4. Die neuesten upstreamkernel-Funktionen sind nur verfügbar, wenn der mit dem Kernel enthaltene [debian-backports](https://wiki.debian.org/Backports)verwendet wird.

5. Während Debian 7. x nicht unterstützt wird und einen älteren Kernel verwendet, hat der Kernel, der in den Debian-backports für Debian 7. x enthalten ist, die Hyper-V-Funktionen verbessert.

Siehe auch

* [Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle SuSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Ubuntu-Computer auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux unter Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)
