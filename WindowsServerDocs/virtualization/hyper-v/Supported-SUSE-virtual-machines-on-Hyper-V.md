---
title: Unterstützte SUSE-Computer auf Hyper-V
description: Enthält die Linux-Integrationsdienste und Features, die unterschiedlichen Versionen
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ec0e14c-4498-4bd9-8fe6-b94260198efc
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: d7b6d3adb4841ea827c56309307549c911a439ea
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222809"
---
# <a name="supported-suse-virtual-machines-on-hyper-v"></a>Unterstützte SUSE-Computer auf Hyper-V

>Gilt für: Windows Server 2016 Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Im folgenden finden eine Zuordnung der Feature-Verteilungspunkt, die die Funktionen in jeder Version angibt. Nach der Tabelle werden die bekannten Probleme und problemumgehungen für die einzelnen Verteilungspunkte aufgeführt.

Die integrierten SUSE Linux Enterprise-Dienst-Treiber für Hyper-V sind von SUSE zertifiziert. Eine Beispielkonfiguration kann in diesem Bulletin angezeigt werden: [SUSE Ja Zertifizierung Bulletin](https://www.suse.com/nbswebapp/yesBulletin.jsp?bulletinNumber=144176).

## <a name="table-legend"></a>Tabellenlegende

* **Integrierte** -LIS als Teil dieser Linux-Verteilung enthalten sind. Die von Microsoft bereitgestelltes LIS-Download-Paket funktioniert nicht für diese Verteilung, damit Sie nicht installiert werden. Die Versionsnummern von Kernel-Modul für den integrierten LIS (siehe **Lsmod**, z. B.) unterscheiden sich die Versionsnummer für das von Microsoft bereitgestelltes LIS-Download-Paket. Ein Konflikt nicht angegeben, den integrierten LIS nicht mehr aktuell ist.

* &#10004;-Funktion

* (*leere*)-Funktion nicht verfügbar.

SLES12 + ist 64-Bit-nur.

|**Funktion**|**Windows Server-Betriebssystemversion**|**SLES 15**|**SLES 12 SP3/SP4**|**SLES 12 SP2**|**SLES 12 SP1**|**SLES 11 SP4**|**SLES 11 SP3**|
|-|-|-|-|-|-|-|-|
|**Verfügbarkeit**||Integrierte|Integrierte|Integrierte|Integrierte|Integrierte|Integrierte|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 – genaue Uhrzeit|2019, 2016|&#10004;|&#10004;|&#10004;||||
|**[Netzwerkfunktionen](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Großrahmen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN-Kennzeichnung und trunking|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Livemigration|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injection|2019, 2016, 2012 R2, 2012|&#10004;Note 1|&#10004;Note 1|&#10004;Note 1|&#10004;Note 1|&#10004;Note 1|&#10004;Note 1|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|Segmentierung von TCP und Prüfsumme Abladungen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SR-IOV|2019, 2016|&#10004;|&#10004;|&#10004;||||
|**[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||||||||
|VHDX resize|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Virtueller Fibre Channel|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VM-Sicherung|2019, 2016, 2012 R2|&#10004;Beachten Sie, 2, 3, 8|&#10004;Beachten Sie, 2, 3, 8|&#10004;Beachten Sie, 2, 3, 8|&#10004;Beachten Sie, 2, 3, 8|&#10004;Beachten Sie, 2, 3, 8|&#10004;Beachten Sie, 2, 3, 8|
|TRIM-Unterstützung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SCSI WWN|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;||||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**||||||||
|Kernel-Unterstützung für PAE|2019, 2016, 2012 R2, 2012, 2008 R2|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|&#10004;|&#10004;|
|Konfiguration der MMIO-Lücke|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher - Hot-Add-|2019, 2016, 2012 R2, 2012|&#10004;Hinweis 5, 6|&#10004;Hinweis 5, 6|&#10004;Hinweis 5, 6|&#10004;Hinweis 5, 6|&#10004;Beachten Sie, 4, 5, 6|&#10004;Beachten Sie, 4, 5, 6|
|Dynamische Speichererweiterungsfunktion-|2019, 2016, 2012 R2, 2012|&#10004;Hinweis 5, 6|&#10004;Hinweis 5, 6|&#10004;Hinweis 5, 6|&#10004;Hinweis 5, 6|&#10004;Beachten Sie, 4, 5, 6|&#10004;Beachten Sie, 4, 5, 6|
|Laufzeitspeichers|2019, 2016|&#10004;Hinweis 5, 6|&#10004;Hinweis 5, 6|&#10004;Hinweis 5, 6||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||||
|Hyper-V-spezifischer Videogerät|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|**[Sonstige](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||||
|Schlüssel/Wert-Paar|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;Beachten Sie 7|&#10004;Beachten Sie 7|
|Nicht maskierbarer Interrupt|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Kopieren von Dateien vom Host zum Gast|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|Lsvmbus-Befehl|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;||||
|Hyper-V-Sockets|2019, 2016|&#10004;|&#10004;|||||
|PCI-Pass-Through-/ DDA|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**||||||||
|Mit UEFI Boot|2019, 2016, 2012 R2|&#10004;Hinweis 9|&#10004;Hinweis 9|&#10004;Hinweis 9|&#10004;Hinweis 9|&#10004;Hinweis 9||
|Sicherer Start|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|||

## <a name="BKMK_notes"></a>Anmerkungen zu dieser Version

1. Statische IP-Injection funktioniert möglicherweise nicht, wenn **Netzwerkmanager** für einen angegebenen Hyper-V-spezifischer Netzwerkadapter auf dem virtuellen Computer konfiguriert wurde. Um sicherzustellen, dass statische IP-Adresse reibungslos funktioniert Injection stellen Sie sicher, dass die Netzwerk-Manager vollständig ausgeschaltet wird oder wurde deaktiviert für einen bestimmten Netzwerkadapter durch seine **Ifcfg-EthX** Datei.

2. Wenn offene Dateihandles vorhanden, während eines Sicherungsvorgangs für die Livemigration einer virtuellen Maschine aus, und klicken Sie dann in einigen Fällen Ecke sind, möglicherweise die gesicherten virtuellen Festplatten auf eine Datei System konsistenzprüfung (Fsck) bei der Wiederherstellung werden.

3. Live Sicherungsvorgänge können im Hintergrund fehl, wenn es sich bei dem virtuellen Computer eine angefügte iSCSI-Gerät oder direkt angeschlossenen Speicher (auch bekannt als Pass-Through-Datenträger) ist.

4. Dynamic Memory-Vorgängen können fehlschlagen, wenn das Gastbetriebssystem für den Arbeitsspeicher zu niedrig ausgeführt wird. Es folgen einige bewährten Methoden:

   * Arbeitsspeicher beim Start und der minimale Arbeitsspeicher sollte gleich oder größer als die Größe des Arbeitsspeichers, die von der Verteilung Anbieter empfohlen wird.

   * Anwendungen, die in der Regel den gesamten verfügbaren Arbeitsspeicher auf einem System zu nutzen sind mit der Nutzung von bis zu 80 Prozent des verfügbaren Arbeitsspeichers beschränkt.

5. Unterstützung für dynamischen Speicher ist nur verfügbar, auf 64-Bit-Computern.

6. Geben Sie bei Verwendung von dynamischem Arbeitsspeicher unter Windows Server 2016 oder Windows Server 2012-Betriebssystemen **startspeicher**, **mindestens Erforderlicher Arbeitsspeicher**, und **Maximaler Serverarbeitsspeicher** die Parameter in Vielfachen von 128 MB (Megabyte). Geschieht dies nicht zu "heiß"-Add-Fehlern führen kann, und Arbeitsspeicher, erhöhen Sie in einem Gastbetriebssystem möglicherweise nicht angezeigt.

7. In Windows Server 2016 oder Windows Server 2012 R2 die Schlüssel/Wert-Paar-Infrastruktur funktionieren möglicherweise nicht ordnungsgemäß ohne ein Linux-Softwareupdate. Wenden Sie sich an Ihren Händler, um das Softwareupdate zu erhalten, falls Sie Probleme mit diesem Feature finden Sie unter.

8. VSS-Sicherung schlägt fehl, wenn Sie eine einzelne Partition mehrmals eingebunden ist.

9. Unter Windows Server 2012 R2 wird die Generation 2 virtuelle Computer sicheren Start, die standardmäßig aktiviert und Generation 2-Linux-Computer verfügen, wenn die Option für sicheren Start deaktiviert, wird nicht gestartet. Sie können den sicheren Start im Abschnitt **Firmware** der Einstellungen für den virtuellen Computer im Hyper-V-Manager oder mithilfe der PowerShell deaktivieren:

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```

## <a name="see-also"></a>Siehe auch

* [Set-VMFirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Unterstützt von CentOS und Red Hat Enterprise Linux-VMs auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Debian-Computer in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux-VMs auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte Ubuntu-VMs auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte FreeBSD-Maschinen in Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Eine Beschreibung für Linux und FreeBSD-VMs auf Hyper-V-Funktion](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux in Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)
