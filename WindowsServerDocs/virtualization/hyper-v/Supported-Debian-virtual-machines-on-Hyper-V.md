---
title: Virtuelle Debian-Computer unterstützt auf Hyper-V
description: Enthält die Linux-Integrationsdienste und Features, die unterschiedlichen Versionen
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cc62c10-02a3-4633-960c-23bf91a45bd5
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 6ec089f501a0999a4460501dbc4d03428d36af40
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863831"
---
# <a name="supported-debian-virtual-machines-on-hyper-v"></a>Virtuelle Debian-Computer unterstützt auf Hyper-V

>Gilt für: Windows Server 2016 Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Die folgende Funktion Verteilung Karte gibt an, die Funktionen, die in den einzelnen Versionen vorhanden sind. Nach der Tabelle werden die bekannten Probleme und problemumgehungen für die einzelnen Verteilungspunkte aufgeführt.

## <a name="table-legend"></a>Tabellenlegende

* **Integrierte** -LIS als Teil dieser Linux-Verteilung enthalten sind. Die von Microsoft bereitgestelltes LIS-Download-Paket funktioniert nicht für diese Verteilung, damit Sie nicht installiert werden. Die Versionsnummern von Kernel-Modul für den integrierten LIS (siehe **Lsmod**, z. B.) unterscheiden sich die Versionsnummer für das von Microsoft bereitgestelltes LIS-Download-Paket. Ein Konflikt, nicht dass die integrierten LIS veraltet ist.

* &#10004;-Funktion

* (*leere*)-Funktion nicht verfügbar.

|**Funktion**|**Windows Server-Betriebssystemversion**|**9.0-9.6 (stretch)**|**8.0-8.11 (Jessie)**|**7.0-7.11 (wheezy)**|
|-|-|-|-|-|
|**Verfügbarkeit**||Erstellt|Erstellt|Integriert (Notiz 6)|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 – genaue Uhrzeit|2019, 2016|&#10004;Beachten Sie 8||
|**[Netzwerkfunktionen](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Networking)**|
|Großrahmen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|VLAN-Kennzeichnung und trunking|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|Livemigration|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|Statische IP-Injection|2019, 2016, 2012 R2, 2012|||
|vRSS|2019, 2016, 2012 R2|&#10004;Beachten Sie 8|||
|Segmentierung von TCP und Prüfsumme Abladungen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;Beachten Sie 8|||
|SR-IOV|2019, 2016|&#10004;Beachten Sie 8||
|**[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Storage)**|
|VHDX resize|2019, 2016, 2012 R2|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|
|Virtueller Fibre Channel|2019, 2016, 2012 R2|||
|VM-Sicherung|2019, 2016, 2012 R2|&#10004;Beachten Sie 4,5|&#10004;Beachten Sie 4,5|&#10004;Anhang 4|
|TRIM-Unterstützung|2019, 2016, 2012 R2|&#10004;Beachten Sie 8|||
|SCSI WWN|2019, 2016, 2012 R2|&#10004;Beachten Sie 8||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Memory)**|
|Kernel-Unterstützung für PAE|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|Konfiguration der MMIO-Lücke|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher - Hot-Add-|2019, 2016, 2012 R2, 2012|&#10004;Beachten Sie 8|||
|Dynamische Speichererweiterungsfunktion-|2019, 2016, 2012 R2, 2012|&#10004;Beachten Sie 8|||
|Laufzeitspeichers|2019, 2016|&#10004;Beachten Sie 8|||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Video)**|
|Hyper-V-spezifischer Videogerät|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;||
|**[Sonstige](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Misc)**|
|Schlüssel-Wert-Paar|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;Anhang 4|&#10004;Anhang 4||
|Nicht maskierbarer Interrupt|2019, 2016, 2012 R2|&#10004;|&#10004;|
|Kopieren von Dateien vom Host zum Gast|2019, 2016, 2012 R2|&#10004;Anhang 4|&#10004;Anhang 4||
|Lsvmbus-Befehl|2019, 2016, 2012 R2, 2012, 2008 R2|||
|Hyper-V-Sockets|2019, 2016|&#10004;Beachten Sie 8|||
|PCI-Pass-Through-/ DDA|2019, 2016|&#10004;Beachten Sie 8|||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_gen2)**|
|Mit UEFI Boot|2019, 2016, 2012 R2|&#10004;Beachten Sie 7|&#10004;Beachten Sie 7||
|Sicherer Start|2019, 2016|||

## <a name="BKMK_notes"></a>Anmerkungen zu dieser Version

1. Erstellen von Dateisystemen auf VHDs größer als 2TB wird nicht unterstützt.

2. Windows Server 2008 R2-SCSI-Datenträger erstellen Sie auf 8 verschiedene Einträge in/Dev/sd *.

3. Windows Server 2012 R2 einen virtuellen Computer mit mindestens 8 Kernen müssen alle Interrupts, die an eine einzelne vCPU weitergeleitet.

4. Beginnend mit Debian 8.3 die Debian-Paket manuell installierte "Hyper-v-Daemons" enthält die Schlüssel-Wert-Paar, Fcopy und VSS-Daemons. Debian 7.x und 8.0-8.2 muss das Hyper-v-Daemons-Paket von stammen [Debian Backports](https://wiki.debian.org/Backports).

5. Livemigration einer virtuellen Maschine Sicherung funktioniert nicht mit ext2-Dateisystemen. Das Standardlayout vom Debian-Installationsprogramm erstellt enthält ext2 Dateisysteme, müssen Sie das Layout nicht erstellt werden diese Dateisystemtyp anpassen.

6. Debian 7.x ist nicht mehr unterstützt und verwendet einen älteren-Kernel, der Kernel in enthalten [Debian Backports](https://wiki.debian.org/Backports) für Debian 7.x Hyper-V-Funktionen verbessert hat.

7. Unter Windows Server 2012 R2 Generation 2 standardmäßig aktiviertem sicheren Start über virtuelle Computer verfügen, und einige virtuelle Linux-Computer wird nicht gestartet werden, es sei denn, die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Deaktivieren der **Firmware** Abschnitt der Einstellungen für den virtuellen Computer in **Hyper-V-Manager** oder Sie können mithilfe von Powershell deaktivieren:

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```
8. Die neuesten upstream-Kernel-Funktionen sind nur verfügbar, mit der Kernel enthalten [Debian Backports](https://wiki.debian.org/Backports).

Siehe auch

* [Unterstützt von CentOS und Red Hat Enterprise Linux-VMs auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux-VMs auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte SUSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte Ubuntu-VMs auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte FreeBSD-Maschinen in Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Eine Beschreibung für Linux und FreeBSD-VMs auf Hyper-V-Funktion](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux in Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)
