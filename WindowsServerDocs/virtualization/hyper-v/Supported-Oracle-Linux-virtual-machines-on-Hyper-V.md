---
title: Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V
description: Listet die in jeder Version enthaltenen Linux-Integrationsdienste und-Funktionen auf.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: c02fdb5b-62f3-43cb-a190-ab74b3ebcf77
author: shirgall
ms.author: kathydav
ms.date: 06/05/2020
ms.openlocfilehash: 67f38d11c032e9eb0b98da14c25e01a5f67cabae
ms.sourcegitcommit: 76a3b5f66e47e08e8235e2d152185b304d03b68b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663173"
---
# <a name="supported-oracle-linux-virtual-machines-on-hyper-v"></a>Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V

>Gilt für: Windows Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows 10, Windows 8.1

Die folgende featureverteilungskarte gibt die Funktionen an, die in den einzelnen Versionen vorhanden sind. Die bekannten Probleme und Problem Umgehungen für die einzelnen Verteilungen werden nach der Tabelle aufgelistet.

Inhalt dieses Abschnitts:

* [Oracle Linux 8. x-Serie](#oracle-linux-8x-series)
* [Oracle Linux 7. x-Serie](#oracle-linux-7x-series)
* [Oracle Linux 6. x-Reihe](#oracle-linux-6x-series)
 
   
## <a name="table-legend"></a>Tabellen Legende

* **Integrierte** -LIS sind als Teil dieser Linux-Distribution enthalten. Die Kernel-Modul Versionsnummern für die integrierten Lis (z. **b. lsmod**) unterscheiden sich von der Versionsnummer des von Microsoft bereitgestellten LIS-Download Pakets. Ein Konflikt weist nicht darauf hin, dass der integrierte LIS veraltet ist.

* &#10004;-Feature verfügbar
* (*leer*): Feature nicht verfügbar
* **Rhck** -red hat-Kompilier barer Kernel
* **UEK** -Unbreakable Enterprise Kernel (UEK) 
   * UEK4 basiert auf einer Linux-Upstream-Upstream-Version 4.1.12
   * UEK5 basiert auf der Linux-Upstream-Version 4,14
   * UEK6 basiert auf der Linux-Upstream-Version 5,4

## <a name="oracle-linux-8x-series"></a>Oracle Linux 8. x-Serie

|       **Feature**     |       **Windows Server-Version**      |       **8.0-8.1 (rhck)** |
|-----------------------|---------------------------------------|-------------------|
|       **Verfügbarkeit**        |   |
|       **[Kernspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019, 2016, 2012 R2 | &#10004; | 
|       Windows Server 2016 genaue Zeit       | 2019, 2016 | &#10004; | 
|       **[Netzwerk](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   | 
|       Großrahmen        | 2019, 2016, 2012 R2 | &#10004; | 
|       VLAN-Tagging und-Abschneiden       | 2019, 2016, 2012 R2 | &#10004;  | 
|       Livemigration      | 2019, 2016, 2012 R2 | &#10004; |
|       Statische IP-Injektion     |  2019, 2016, 2012 R2 | &#10004; Hinweis 2 | 
|       vRSS     | 2019, 2016, 2012 R2 | &#10004; |
|       TCP-Segmentierung und Prüfsummen Offloads | 2019, 2016, 2012 R2 | &#10004;|
|       SR-IOV  | 2019, 2016 |  &#10004;   |
|       **[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  | 
|       Vhdx-Größe ändern  | 2019, 2016, 2012 R2 | &#10004; |
|       Virtueller Fibre Channel | 2019, 2016, 2012 R2 | &#10004; Hinweis 3  |
|       Sicherung virtueller Computer  | 2019, 2016, 2012 R2 | &#10004; Hinweis 5 |
|       Trim-Unterstützung | 2019, 2016, 2012 R2 | &#10004;  |
|       SCSI-WWN | 2019, 2016, 2012 R2 | &#10004;  |
|       **[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |
|       Unterstützung für den unterstützten Kernel  | 2019, 2016, 2012 R2 |  – |
|       MMIO-Lücke konfigurieren  | 2019, 2016, 2012 R2 | &#10004; | 
|       Dynamischer Arbeitsspeicher-Hot-Add | 2019, 2016, 2012 R2  | &#10004; Hinweis 7, 8, 9 |
|       Dynamischer Arbeitsspeicher-Ballooning | 2019, 2016, 2012 R2 | &#10004; Hinweis 7, 8, 9 |
|       Größenänderung des Lauf Zeit Speichers | 2019, 2016  | &#10004;  |
|       **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | |
|       Hyper-V-spezifisches Videogerät | 2019, 2016, 2012 R2 | &#10004;   | 
|       **[Verschiedenes](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | |
|       Schlüssel-Wert-Paar  | 2019, 2016, 2012 R2 | &#10004;   | 
|       Nicht mastbare Unterbrechung | 2019, 2016, 2012 R2 | &#10004;  | 
|       Dateikopie von Host zu Gast | 2019, 2016, 2012 R2 | &#10004;  | 
|       lsvmbus-Befehl | 2019, 2016, 2012 R2 | &#10004;  | 
|       Hyper-V-Sockets | 2019, 2016 | &#10004;  | 
|       PCI-Passthrough/DDA | 2019, 2016 | &#10004; | 
| **[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       Starten mithilfe von UEFI | 2019, 2016, 2012 R2 |  &#10004; Hinweis 12  |   
|       Sicherer Start | 2019, 2016 |  &#10004; | 

## <a name="oracle-linux-7x-series"></a>Oracle Linux 7. x-Serie

Diese Reihe hat nur 64-Bit-Kernel.

<table width="100%">
<tr height="50px">
<td width="20%" rowspan="2">

Funktion
</td>
<td width="20%" rowspan="2">

Windows Server-Version
</td>
<td width="30%" colspan="3">

7.5-7.8
</td>
<td width="30%" colspan="3">

7.3-7.4
</td>
</tr>
<tr>
<td width="20%" colspan="2">

RHCK
</td>
<td width="10%">

UEK5
</td>
<td width="20%" colspan="2">

RHCK
</td>
<td width="10%">

UEK4
</td>
</tr>
<tr>
<td width="20%">

Verfügbarkeit
</td>
<td width="20%">


</td>
<td width="10%">

LIS 4,3
</td>
<td width="10%">

Integriert
</td>
<td width="10%">

Integriert
</td>
<td width="10%">

LIS 4,3
</td>
<td width="10%">

Integriert
</td>
<td width="10%">

Integriert
</td>
</tr>
<tr height="50px">
<td width="20%">

**[Kernspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Windows Server 2016 genaue Zeit
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

 **[Netzwerk](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)** 
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Großrahmen
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">
VLAN-Tagging und-Abschneiden
</td>
<td width="20%">
2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Livemigration
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Statische IP-Injektion
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Hinweis 2
</td>
<td width="10%">

&#10004; Hinweis 2
</td>
<td width="10%">

&#10004; Hinweis 2
</td>
<td width="10%">

&#10004; Hinweis 2
</td>
<td width="10%">

&#10004; Hinweis 2
</td>
<td width="10%">

&#10004; Hinweis 2
</td>
</tr>
<tr height="50px">
<td width="20%">

vRSS
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

TCP-Segmentierung und Prüfsummen Offloads
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

SR-IOV
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Vhdx-Größe ändern
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Virtueller Fibre Channel
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Hinweis 3
</td>
<td width="10%">

&#10004; Hinweis 3
</td>
<td width="10%">

&#10004; Hinweis 3
</td>
<td width="10%">

&#10004; Hinweis 3
</td>
<td width="10%">

&#10004; Hinweis 3
</td>
<td width="10%">

&#10004; Hinweis 3
</td>
</tr>
<tr height="50px">
<td width="20%">

Sicherung virtueller Computer
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Hinweis 5
</td>
<td width="10%">

&#10004; Hinweis 4, 5
</td>
<td width="10%">

&#10004; Hinweis 5
</td>
<td width="10%">

&#10004; Hinweis 5
</td>
<td width="10%">

&#10004; Hinweis 4, 5
</td>
<td width="10%">

&#10004; Hinweis 5
</td>
</tr>
<tr height="50px">
<td width="20%">

Trim-Unterstützung
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

SCSI-WWN
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**
</td>
<td width="20%">


</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Unterstützung für den unterstützten Kernel
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

–
</td>
<td width="10%">

–
</td>
<td width="10%">

–
</td>
<td width="10%">

–
</td>
<td width="10%">

–
</td>
<td width="10%">

–
</td>
</tr>
<tr height="50px">
<td width="20%">

MMIO-Lücke konfigurieren
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Dynamischer Arbeitsspeicher Hot-Add
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Hinweis 7, 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
</tr>
<tr height="50px">
<td width="20%">

Dynamischer Arbeitsspeicher
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Hinweis 7, 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
<td width="10%">

&#10004; Hinweis 8, 9
</td>
</tr>
<tr height="50px">
<td width="20%">

Größenänderung des Lauf Zeit Speichers
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Hyper-V-spezifisches Video
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[Verschiedenes](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Schlüssel-Wert-Paar
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Nicht mastbare Unterbrechung
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Dateikopie von Host zu Gast
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

lsvmbus-Befehl
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Hyper-V-Sockets
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

PCI-Passthrough/DDA
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Starten mithilfe von UEFI
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Hinweis 12
</td>
<td width="10%">

&#10004; Hinweis 12
</td>
<td width="10%">

&#10004; Hinweis 12
</td>
<td width="10%">

&#10004; Hinweis 12
</td>
<td width="10%">

&#10004; Hinweis 12
</td>
<td width="10%">

&#10004; Hinweis 12
</td>
</tr>
<tr height="50px">
<td width="20%">

Sicherer Start
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
</table>


## <a name="oracle-linux-6x-series"></a>Oracle Linux 6. x-Reihe

Diese Reihe hat nur 64-Bit-Kernel.

|       **Feature**     |       **Windows Server-Version**      |       **6.8-6.10 (rhck)** |       **6.8-6.10 (UEK4)**     | 
|-----------------------|---------------------------------------|-------------------|-------------------|
|       **Verfügbarkeit**     |   | LIS 4,3  | Integriert  |
|       **[Kernspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019, 2016, 2012 R2 | &#10004; | &#10004;
|       Windows Server 2016 genaue Zeit       | 2019, 2016 | | 
|       **[Netzwerk](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   |  |
|       Großrahmen        | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       VLAN-Tagging und-Abschneiden       | 2019, 2016, 2012 R2 | &#10004; Hinweis 1 | &#10004; Hinweis 1 |
|       Livemigration      | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       Statische IP-Injektion     |  2019, 2016, 2012 R2 | &#10004; Hinweis 2 | &#10004;|
|       vRSS     | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       TCP-Segmentierung und Prüfsummen Offloads | 2019, 2016, 2012 R2 | &#10004;|  &#10004; |
|       SR-IOV  | 2019, 2016 |    |  |
|       **[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  |  |
|       Vhdx-Größe ändern  | 2019, 2016, 2012 R2 | &#10004; | &#10004; |
|       Virtueller Fibre Channel | 2019, 2016, 2012 R2 | &#10004; Hinweis 3  | &#10004; Hinweis 3 |
|       Sicherung virtueller Computer  | 2019, 2016, 2012 R2 | &#10004; Hinweis 5 | &#10004; Hinweis 5|
|       Trim-Unterstützung | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       SCSI-WWN | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       **[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |  |
|       Unterstützung für den unterstützten Kernel  | 2019, 2016, 2012 R2 |  – | –
|       MMIO-Lücke konfigurieren  | 2019, 2016, 2012 R2 | &#10004; | &#10004;  |
|       Dynamischer Arbeitsspeicher-Hot-Add | 2019, 2016, 2012 R2  | &#10004; Hinweis 6, 8, 9 | &#10004; Hinweis 6, 8, 9 |
|       Dynamischer Arbeitsspeicher-Ballooning | 2019, 2016, 2012 R2 | &#10004; Hinweis 6, 8, 9 | &#10004; Hinweis 6, 8, 9 |
|       Größenänderung des Lauf Zeit Speichers | 2019, 2016  |  | |
|       **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | | |
|       Hyper-V-spezifisches Videogerät | 2019, 2016, 2012 R2 | &#10004;   | &#10004; |
|       **[Verschiedenes](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | | |
|       Schlüssel-Wert-Paar  | 2019, 2016, 2012 R2 | &#10004; Notiz 10, 11   | &#10004; Notiz 10, 11  |
|       Nicht mastbare Unterbrechung | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Dateikopie von Host zu Gast | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       lsvmbus-Befehl | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Hyper-V-Sockets | 2019, 2016 | &#10004;  | &#10004; |
|       PCI-Passthrough/DDA | 2019, 2016 | &#10004; | &#10004; |
| **[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       Starten mithilfe von UEFI | 2019, 2016, 2012 R2 |  &#10004; Hinweis 12  | &#10004; Hinweis 12   
|       Sicherer Start | 2019, 2016 |  |  |



## <a name="notes"></a><a name="BKMK_notes"></a>Hinweise

1. Für diese Oracle Linux Version funktioniert das VLAN-Tagging, aber VLAN-abkürzen nicht.

2. Die statische IP-Injektion funktioniert möglicherweise nicht, wenn der Netzwerk-Manager für einen bestimmten synthetischen Netzwerkadapter auf dem virtuellen Computer konfiguriert wurde. Stellen Sie für eine reibungslose Verwendung statischer IP-Einschleusung sicher, dass entweder der Netzwerk-Manager entweder vollständig ausgeschaltet ist oder für einen bestimmten Netzwerkadapter über seine ifcfg-ethX-Datei ausgeschaltet wurde.

3.  Stellen Sie unter Windows Server 2012 R2 bei der Verwendung von virtuellen Fibre Channel-Geräten sicher, dass die logische Gerätenummer 0 (LUN 0) aufgefüllt wurde. Wenn LUN 0 nicht aufgefüllt wurde, kann ein virtueller Linux-Computer möglicherweise keine systemeigenen Fibre Channel-Geräte einbinden.

4. Für integrierte LIS muss das "HyperV-Daemons"-Paket für diese Funktionalität installiert werden.

5.  Wenn während eines Sicherungs Vorgangs für virtuelle Computer geöffnete Datei Handles vorhanden sind, müssen die gesicherten VHDs in einigen Fällen möglicherweise bei der Wiederherstellung eine Dateisystem Konsistenzprüfung (fsck) durchlaufen. Bei Live Sicherungs Vorgängen kann ein Fehler auftreten, wenn der virtuelle Computer über ein angefügtes iSCSI-Gerät oder einen direkt angeschlossenen Speicher (auch als Pass-Through-Datenträger bezeichnet) verfügt.

6. Die Unterstützung dynamischer Arbeitsspeicher ist nur auf virtuellen 64-Bit-Computern verfügbar.

7. Die Unterstützung von "Hot-Add" ist in dieser Verteilung standardmäßig nicht aktiviert. Um die Unterstützung für "Hot-Add" zu aktivieren, müssen Sie eine udev-Regel unter/etc/udev/rules.d/wie folgt hinzufügen:

   1. Erstellen Sie eine Datei **/etc/udev/rules.d/100-Balloon.Rules**. Sie können einen beliebigen anderen gewünschten Namen für die Datei verwenden.

   2. Fügen Sie der Datei den folgenden Inhalt hinzu:`SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. Starten Sie das System neu.

   Während das Herunterladen von Linux-Integration Services diese Regel bei der Installation erstellt, wird die Regel auch entfernt, wenn LIS deinstalliert wird. Daher muss die Regel neu erstellt werden, wenn dynamischer Arbeitsspeicher nach der Installation benötigt wird.

8. Dynamische Arbeitsspeicher Vorgänge können fehlschlagen, wenn für das Gast Betriebssystem zu wenig Arbeitsspeicher verfügbar ist. Im folgenden finden Sie einige bewährte Methoden:

   * Start Speicher und minimaler Arbeitsspeicher müssen größer oder gleich dem vom Verteilungs Anbieter empfohlenen Arbeitsspeicher sein.

   * Anwendungen, die in der Regel den gesamten verfügbaren Arbeitsspeicher auf einem System belegen, können bis zu 80 Prozent des verfügbaren Arbeitsspeichers verbrauchen.

9. Wenn Sie dynamischer Arbeitsspeicher auf einem Windows Server 2016-oder Windows Server 2012 R2-Betriebssystem verwenden, geben Sie den **Start Speicher**, den **minimalen Arbeitsspeicher**und den **maximalen Arbeitsspeicher** Parameter in Vielfachen von 128 Megabyte (MB) an. Wenn dies nicht der Fall ist, kann dies zu Fehlern beim Hinzufügen von Fehlern führen, und in einem Gast Betriebssystem wird möglicherweise keine Erhöhung des Arbeitsspeichers angezeigt.

10. Um die KVP-Infrastruktur (Key/Value Pair) zu aktivieren, installieren Sie das Paket hypervkvpd oder HyperV-Daemons RPM von Ihrer Oracle Linux ISO-Datei. Alternativ kann das Paket direkt aus Oracle Linux yum-Repository installiert werden.

11. Die KVP-Infrastruktur (Key/Value-Paar) funktioniert möglicherweise ohne Linux-Software Update nicht ordnungsgemäß. Wenden Sie sich an Ihren Verteilungs Hersteller, um das Software Update zu erhalten, falls Probleme mit diesem Feature auftreten.

12. Auf virtuellen Computern der Windows Server 2012 R2-Generation 2 ist der sichere Start standardmäßig aktiviert, und einige virtuelle Linux-Computer werden erst gestartet, wenn die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Abschnitt **Firmware** der Einstellungen für den virtuellen Computer im **Hyper-V-Manager** deaktivieren, oder Sie können ihn mithilfe von PowerShell deaktivieren:

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

    Der Download der Linux-Integration Services kann auf vorhandene VMS der Generation 2 angewendet werden, aber nicht die Funktion der Generation 2.


Weitere Informationen

* [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Debian-Computer in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle SuSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Ubuntu-Computer auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux unter Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)
