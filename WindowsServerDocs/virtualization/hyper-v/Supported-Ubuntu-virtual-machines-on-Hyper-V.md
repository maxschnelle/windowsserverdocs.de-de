---
title: Unterstützte Ubuntu-VMs auf Hyper-V
description: Enthält die Linux-Integrationsdienste und Features, die unterschiedlichen Versionen
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95ea5f7c-25c6-494b-8ffd-2a77f631ee94
author: shirgall
ms.author: shirgall
ms.date: 11/19/2018
ms.openlocfilehash: afba885fc49ba129c0ef452704cbfe9f9cf884ba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834041"
---
# <a name="supported-ubuntu-virtual-machines-on-hyper-v"></a>Unterstützte Ubuntu-VMs auf Hyper-V

>Gilt für: WindowsServer 2019, 2016, Hyper-V Server 2019, 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Ubuntu 12.04 ab, installiert Laden des Pakets "Linux virtual" einen Kernel, die für die Verwendung geeignet als eine Gast-VM. Dieses Paket hängt immer die neuesten minimale generisches Kernel-Image und die Header, die für virtuelle Computer verwendet. Ihre Verwendung ist, zwar optional wird der virtuellen Linux-Kernel weniger Treiber zu laden und kann schneller starten und haben weniger Speicherbedarf als ein allgemeines Bild.

Um vollständige Verwendung von Hyper-V zu erhalten, installieren Sie die entsprechenden Linux-Tools und Linux-Cloud-Tools-Pakete, Tools und -Daemons für die Verwendung mit virtuellen Computern zu installieren. Wenn Sie den virtuellen Linux-Kernel verwenden, laden Sie die Linux-Tools-virtual- und Linux-Cloud-Tools-virtual.

Die folgende Funktion Verteilung Karte gibt an, die Funktionen in der jeweiligen Version. Nach der Tabelle werden die bekannten Probleme und problemumgehungen für die einzelnen Verteilungspunkte aufgeführt.

## <a name="table-legend"></a>Tabellenlegende

* **Integrierte** -LIS als Teil dieser Linux-Verteilung enthalten sind. Die von Microsoft bereitgestelltes LIS-Download-Paket funktioniert nicht für diese Verteilung, sodass sie nicht installieren müssen. Die Versionsnummern von Kernel-Modul für den integrierten LIS (siehe **Lsmod**, z. B.) unterscheiden sich die Versionsnummer für das von Microsoft bereitgestelltes LIS-Download-Paket. Ein Konflikt nicht angegeben, den integrierten LIS nicht mehr aktuell ist.

* &#10004;-Funktion

* (*leere*)-Funktion nicht verfügbar.

|**Funktion**|**Windows Server-Betriebssystemversion**|**18.10**|**18.04 LTS**|**16.04 LTS**|**14.04 LTS**|**12.04 LTS**|
|-|-|-|-|-|-|-|
|**Verfügbarkeit**||Integrierte|Integrierte|Integrierte|Integrierte|Integrierte|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 – genaue Uhrzeit|2019, 2016|&#10004;|&#10004;|&#10004;|||
|**[Netzwerkfunktionen](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Networking)**|||||||
|Großrahmen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN-Kennzeichnung und trunking|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Livemigration|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injection|2019, 2016, 2012 R2, 2012|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|Segmentierung von TCP und Prüfsumme Abladungen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|SR-IOV|2019, 2016|&#10004;|&#10004;|&#10004;|||
|**[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Storage)**||||||
|VHDX resize|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|Virtueller Fibre Channel|2019, 2016, 2012 R2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2||
|VM-Sicherung|2019, 2016, 2012 R2|&#10004;Beachten Sie, 3, 4, 6|&#10004;Beachten Sie, 3, 4, 5|&#10004;Beachten Sie, 3, 4, 5|&#10004;Beachten Sie, 3, 4, 5||
|TRIM-Unterstützung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|SCSI WWN|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Memory)**||||||
|Kernel-Unterstützung für PAE|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Konfiguration der MMIO-Lücke|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher - Hot-Add-|2019, 2016, 2012 R2, 2012|&#10004;Beachten Sie, 7, 8, 9|&#10004;Beachten Sie, 7, 8, 9|&#10004;Beachten Sie, 7, 8, 9|&#10004;Beachten Sie, 7, 8, 9||
|Dynamische Speichererweiterungsfunktion-|2019, 2016, 2012 R2, 2012|&#10004;Beachten Sie, 7, 8, 9|&#10004;Beachten Sie, 7, 8, 9|&#10004;Beachten Sie, 7, 8, 9|&#10004;Beachten Sie, 7, 8, 9||
|Laufzeitspeichers|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Video)**|||||||
|Hyper-V-spezifischen Videogerät|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|**[Sonstige](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Misc)**||||||
|Schlüssel/Wert-Paar|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;Hinweis 6, 10|&#10004;Hinweis 5, 10|&#10004;Hinweis 5, 10|&#10004;Hinweis 5, 10|&#10004;Hinweis 5, 10|
|Nicht maskierbarer Interrupt|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Kopieren von Dateien vom Host zum Gast|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|Lsvmbus-Befehl|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|Hyper-V-Sockets|2019, 2016||||||
|PCI-Pass-Through-/ DDA|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_gen2)**||||||
|Mit UEFI Boot|2019, 2016, 2012 R2|&#10004;Hinweis 11, 12|&#10004;Hinweis 11, 12|&#10004;Hinweis 11, 12|&#10004;Hinweis 11, 12||
|Sicherer Start|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;||

## <a name="BKMK_notes"></a>Anmerkungen zu dieser Version

1. Statische IP-Injection funktioniert möglicherweise nicht, wenn **Netzwerkmanager** für einen angegebenen Hyper-V-spezifischer Netzwerkadapter auf dem virtuellen Computer konfiguriert wurde. Um sicherzustellen, dass statische IP-Adresse reibungslos funktioniert Injection stellen Sie sicher, dass die Netzwerk-Manager vollständig ausgeschaltet wird oder wurde deaktiviert für einen bestimmten Netzwerkadapter durch seine **Ifcfg-EthX** Datei.

2. Bei der Verwendung von virtuellen Fibre Channel-Geräten, stellen Sie sicher, dass die logische Gerätenummer (LUN 0)-0 aufgefüllt wurde. Virtuelle Linux-Computer sind möglicherweise nicht Fiber-Channel-Geräten nativ bereitstellen können, wenn die LUN 0 nicht aufgefüllt wurde.

3. Wenn geöffnet sind Dateihandles während eines Sicherungsvorgangs für die Livemigration einer virtuellen Maschine, und klicken Sie dann die gesicherten VHDs möglicherweise in einigen Fällen Ecke eine konsistenzprüfung für Datei-System zu durchlaufen (`fsck`) bei der Wiederherstellung.

4. Live Sicherungsvorgänge können im Hintergrund fehl, wenn es sich bei dem virtuellen Computer eine angefügte iSCSI-Gerät oder direkt angeschlossenen Speicher (auch bekannt als Pass-Through-Datenträger) ist.

5. Zur Unterstützung von langfristig verwenden (LTS) Versionen neueste virtuelle Hardware Enablement (HWE)-Kernel für Linux-Integrationsdienste auf dem neuesten Stand.

   Um die optimierte Azure-Kernel auf 14.04, 16.04 und 18.04 zu installieren, führen Sie die folgenden Befehle als Stamm (oder "sudo"):

   ```bash
   # apt-get update
   # apt-get install linux-azure

   ```

   12.04 muss sich nicht auf einen separaten virtuellen Kernel aus. Führen Sie die folgenden Befehle als Stamm (oder "sudo"), um den generischen HWE-Kernel auf 12.04 zu installieren:

   ```bash
   # apt-get update
   # apt-get install linux-generic-lts-trusty

   ```

   Sind die folgenden Hyper-V-Daemons auf Ubuntu 12.04 in einem getrennt installierten Paket:

   * **VSS-Momentaufnahme-Daemon** : dieser Daemon ist erforderlich, um live Linux-VM-Sicherungen zu erstellen.
   * **KVP-Daemon** : dieser Daemon ermöglicht das Festlegen und Abfragen interner und externer Schlüsselwertpaare Schlüssel-/Wertpaaren.
   * **Fcopy Daemon** : dieser Daemon implementiert einen dateikopierdienst zwischen Host und Gast.

   Um den KVP-Daemon auf 12.04 zu installieren, führen Sie die folgenden Befehle als Stamm (oder "sudo").

   ```bash
   # apt-get install hv-kvp-daemon-init linux-tools-lts-trusty linux-cloud-tools-generic-lts-trusty

   ```

   Sobald der Kernel aktualisiert wird, muss der virtuelle Computer neu gestartet werden, um es zu verwenden.

6. Verwenden Sie auf Ubuntu 18.10 den neuesten virtuellen Kernel, um die auf dem neuesten Stand Hyper-V-Funktionen verwenden zu können.

   Führen Sie die folgenden Befehle als Stamm (oder "sudo"), um den virtuellen Kernel auf 18.10 zu installieren:

   ```bash
   # apt-get update
   # apt-get install linux-azure

   ```

   Sobald der Kernel aktualisiert wird, muss der virtuelle Computer neu gestartet werden, um es zu verwenden.

7. Unterstützung für dynamischen Speicher ist nur verfügbar, auf 64-Bit-Computern.

8. Dynamische Memory-Vorgängen können fehlschlagen, wenn das Gastbetriebssystem für den Arbeitsspeicher zu niedrig ausgeführt wird. Es folgen einige bewährten Methoden:

   * Arbeitsspeicher beim Start und der minimale Arbeitsspeicher sollte gleich oder größer als die Größe des Arbeitsspeichers, die von der Verteilung Anbieter empfohlen wird.

   * Anwendungen, die in der Regel den gesamten verfügbaren Arbeitsspeicher auf einem System zu nutzen sind mit der Nutzung von bis zu 80 Prozent des verfügbaren Arbeitsspeichers beschränkt.

9. Wenn Sie dynamischen Arbeitsspeicher in Windows Server-2019, Windows Server 2016 oder Windows Server 2012/2012 R2-Betriebssystem verwenden, geben Sie **startspeicher**, **mindestens Erforderlicher Arbeitsspeicher**, und **maximale Arbeitsspeicher** Parameter in Vielfachen von 128 MB (Megabyte). Geschieht dies nicht zu "heiß"-Add-Fehlern führen kann, und vergrößern Sie auf der Gast-Betriebssystem Speicher werden möglicherweise nicht angezeigt.

10. In Windows Server-2019, Windows Server 2016 oder Windows Server 2012 R2 die Schlüssel/Wert-Paar-Infrastruktur funktionieren möglicherweise nicht ordnungsgemäß ohne ein Linux-Softwareupdate. Wenden Sie sich an Ihren Händler, um das Softwareupdate zu erhalten, falls Sie Probleme mit diesem Feature finden Sie unter.

11. Unter Windows Server 2012 R2 müssen virtuelle Computer der Generation 2 sicheren Start, die standardmäßig aktiviert und einige Linux, virtuelle Computer nicht gestartet werden, es sei denn, die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Deaktivieren der **Firmware** Abschnitt der Einstellungen für den virtuellen Computer in **Hyper-V-Manager** oder Sie können mithilfe von Powershell deaktivieren:

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```

12. Gehen Sie bevor Sie versuchen, kopieren Sie die virtuelle Festplatte von einem vorhandenen virtuellen Computer von Generation 2-VHD, um neue VMs der Generation 2 zu erstellen folgendermaßen vor:

   1. Melden Sie sich die vorhandenen virtuellen Computer der Generation 2.

   2. Wechseln Sie in der Start-EFI-Verzeichnis:

      ```bash
      # cd /boot/efi/EFI

      ```

   3. Kopieren Sie das Ubuntu-Verzeichnis, in, um ein neues Verzeichnis mit dem Namen Boot:

      ```bash
      # sudo cp -r ubuntu/ boot

      ```

   4. Ändern Sie das Verzeichnis, das neu erstellte Startverzeichnis:

      ```bash
      # cd boot

      ```

   5. Benennen Sie die shimx64.efi-Datei:

      ```bash
      # sudo mv shimx64.efi bootx64.efi

      ```

## <a name="see-also"></a>Siehe auch

* [Unterstützt von CentOS und Red Hat Enterprise Linux-VMs auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Virtuelle Debian-Computer unterstützt auf Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux-VMs auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte SUSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Eine Beschreibung für Linux und FreeBSD-VMs auf Hyper-V-Funktion](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux in Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Set-VMFirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Ubuntu 14.04 in einer Generation 2 VM - ben armstrongs Blog zum Thema Virtualisierung](https://blogs.msdn.com/b/virtual_pc_guy/archive/2014/06/09/ubuntu-14-04-in-a-generation-2-vm.aspx)
