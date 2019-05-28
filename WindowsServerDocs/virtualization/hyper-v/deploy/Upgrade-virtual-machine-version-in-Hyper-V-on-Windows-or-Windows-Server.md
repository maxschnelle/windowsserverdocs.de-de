---
title: Aktualisieren Sie die Version von Virtual Machine in Hyper-V unter Windows 10 oder Windows Server
description: Bietet Anweisungen und Überlegungen zum Upgrade der Version eines virtuellen Computers
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 897f2454-5aee-445c-a63e-f386f514a0f6
author: jasongerend
ms.author: jgerend
ms.date: 05/22/2019
ms.openlocfilehash: 1d19b3dc7000a4bf5558f351ce67ce7406b3d5d8
ms.sourcegitcommit: b190fac4bfa5599751a60d3fc3b4c4a64dd9afd7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/22/2019
ms.locfileid: "66009078"
---
# <a name="upgrade-virtual-machine-version-in-hyper-v-on-windows-10-or-windows-server"></a>Aktualisieren Sie die Version von Virtual Machine in Hyper-V unter Windows 10 oder Windows Server

>Gilt für: Windows 10, WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)

Stellen Sie die neuesten Hyper-V-Features zur Verfügung auf Ihren virtuellen Computern durch ein Upgrade der Konfigurationsversion. Machen Sie das nicht bis:

- Upgrade auf die neueste Version von Windows oder Windows Server Hyper-V-Hosts.
- Sie aktualisieren die Funktionsebene des Clusters.
- Sie können Sie sicher, dass Sie nicht müssen den virtuellen Computer wieder zu einem Hyper-V-Host verschieben, die eine frühere Version von Windows oder Windows Server ausgeführt wird.

Weitere Informationen finden Sie unter [Cluster Operating System Rolling Upgrade](../../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md) und [ausführen ein paralleles Upgrades eines Hyper-V-Hostclusters in VMM](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade).

## <a name="step-1-check-the-virtual-machine-configuration-versions"></a>Schritt 1: Überprüfen Sie die Versionen von VM-Konfiguration

1. Klicken Sie auf dem Windows-Desktop auf die Schaltfläche „Start“, und geben Sie einen beliebigen Teil des Namens **Windows PowerShell** ein.
2. Mit der rechten Maustaste in Windows PowerShell, und wählen Sie **als Administrator ausführen**.
3. Verwenden der [Get-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm)Cmdlet. Führen Sie den folgenden Befehl aus, um die Versionen Ihrer virtuellen Computer abzurufen.

```PowerShell
Get-VM * | Format-Table Name, Version
```

Sie können auch die Version der Konfiguration im Hyper-V-Manager anzeigen, durch den virtuellen Computer auswählen, und betrachten die **Zusammenfassung** Registerkarte.

## <a name="step-2-upgrade-the-virtual-machine-configuration-version"></a>Schritt 2: Aktualisieren Sie die Konfigurationsversion des virtuellen Computers

1. Die virtuelle Maschine in Hyper-V-Manager wird heruntergefahren.
2. Wählen Sie die Aktion > Upgrade der Konfigurationsversion. Wenn diese Option nicht für den virtuellen Computer verfügbar ist, wird es bereits auf die höchste Konfigurationsversion durch den Hyper-V-Host unterstützt.

Um die Konfigurationsversion des virtuellen Computers mithilfe von Windows PowerShell zu aktualisieren, verwenden die [Update-VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion) Cmdlet. Führen Sie den folgenden Befehl ein Vmname ist der Name des virtuellen Computers.

```PowerShell
Update-VMVersion <vmname>
```

## <a name="BKMK_SupportedConfigVersions"></a>Versionen von unterstützten VM-Konfiguration

Führen Sie das PowerShell-Cmdlet [Get-VMHostSupportedVersion](https://docs.microsoft.com/powershell/module/hyper-v/get-vmhostsupportedversion) , welche Versionen von VM-Konfiguration finden Sie unter Ihrem Hyper-V-Host unterstützt. Wenn Sie einen virtuellen Computer erstellen, wird es mit der Standardversion für die Konfiguration erstellt. Um anzuzeigen, was der Standardwert ist, führen Sie den folgenden Befehl aus.

```PowerShell
Get-VMHostSupportedVersion -Default
```

Wenn Sie einen virtuellen Computer zu erstellen, die Sie auf einem Hyper-V-Host verschieben können müssen ausführt, die eine ältere Version von Windows, verwenden die [New-VM](https://docs.microsoft.com/powershell/module/hyper-v/new-vm) Cmdlet mit dem Versionsparameter. Um einen virtuellen Computer zu erstellen, den Sie auf einem Hyper-V-Host verschieben können, die Windows Server 2012 R2 ausgeführt wird, führen Sie beispielsweise den folgenden Befehl aus. Dieser Befehl erstellt einen virtuellen Computer namens "WindowsCV5" mit einer Konfigurationsversion 5.0.

```PowerShell
New-VM -Name "WindowsCV5" -Version 5.0
```

>[!NOTE]
>Sie können die Importieren von virtuellen Computern, die für einen Hyper-V-Host mit einer älteren Version von Windows erstellt wurden oder aus einer Sicherung wiederherstellen. Wenn der VM Konfigurationsversion nicht aufgeführt ist, da für Ihre Hyper-V-Host-Betriebssystem in der folgenden Tabelle unterstützt, müssen Sie die Version des VM-Konfiguration zu aktualisieren, bevor Sie den virtuellen Computer starten können.

### <a name="supported-vm-configuration-versions-for-long-term-servicing-hosts"></a>Unterstützte Versionen von VM-Konfiguration für Long-term servicing-hosts

Die folgende Tabelle enthält die Versionen der VM-Konfiguration, die auf Hosts, die mit einer Long-term servicing-Version von Windows unterstützt werden.

| Hyper-V-Host-Windows-version | 9.1 | 9.0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
| --- |---|---|---|---|---|---|---|---|---|---|
|Windows Server 2019|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise LTSC 2019|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2016 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2015 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|
|Windows Server 2012 R2|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|
|Windows 8.1|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|

### <a name="supported-vm-configuration-versions-for-semi-annual-channel-hosts"></a>Unterstützte Versionen von VM-Konfiguration für halbjährlicher Kanalhosts

Die folgende Tabelle enthält die Versionen der VM-Konfiguration für eine Version derzeit unterstützten halbjährlicher Kanal von Windows-Hosts an. Weitere Informationen zu halbjährlicher Kanal-Versionen von Windows finden Sie die folgenden Seiten [WindowsServer](../../../get-started-19/servicing-channels-19.md) und [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview#servicing-channels)

| Hyper-V-Host-Windows-version | 9.1 | 9.0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
| --- |---|---|---|---|---|---|---|---|---|---|
| Windows 10 können 2019 (Version 1903) aktualisieren. |&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;| &#10004;|
| Windows Server, version 1903 |&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;| &#10004;|
|Windows Server, Version 1809|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Oktober 2018 Update (Version 1809)|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server, Version 1803|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 April 2018 Update (Version 1803)|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Fall Creators Update (Version 1709)|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Creators Update (Version 1703)|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Anniversary Update (Version 1607)|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|

## <a name="why-should-i-upgrade-the-virtual-machine-configuration-version"></a>Warum sollte ich die Konfigurationsversion des virtuellen Computers aktualisieren?

Beim Verschieben oder Importieren eines virtuellen Computers auf einem Computer mit Hyper-V auf Windows Server-2019, Windows Server 2016 oder Windows 10, die virtuelle Maschine "s-Konfiguration wird nicht automatisch aktualisiert. Dies bedeutet, dass Sie die virtuelle Maschine zurück auf einen Hyper-V-Host verschieben können, die eine frühere Version von Windows oder Windows Server ausgeführt wird. Aber dies bedeutet auch, dass Sie nicht einige der neuen Features für virtuelle Computer verwenden können erst, nachdem Sie die Version der Konfiguration manuell aktualisiert werden. Nachdem Sie sie aktualisiert haben, können Sie die Konfigurationsversion des virtuellen Computers nicht herabstufen.

Die Konfigurationsversion des virtuellen Computers stellt die Kompatibilität der gespeicherte Zustand und Snapshot-Dateien mit der Version von Hyper-V-Konfiguration des virtuellen Computers dar. Wenn Sie die Version der Konfiguration aktualisieren, ändern Sie die Dateistruktur, die zum Speichern der Konfiguration virtueller Computer und die Prüfpunktdateien verwendet wird. Sie aktualisieren die Version der Konfiguration auch auf die neueste Version, die von diesem Hyper-V-Host unterstützt werden. Aktualisierte virtuelle Computer verwenden ein neues Konfigurationsdateiformat, das entworfen wurde, um die Effizienz beim Lesen und Schreiben von VM-Konfigurationsdaten zu steigern. Das Upgrade verringert auch das Potenzial von Datenbeschädigungen bei einem Speicherausfall.

Die folgende Tabelle enthält Beschreibungen, Dateierweiterungen und Standard abweichende Speicherorte für jeden Dateityp, der für neue oder aktualisierte virtuelle Computer verwendet wird.

 |VM-Dateitypen | Beschreibung|
 |---|---|
|Konfiguration |VM-Konfigurationsinformationen, die im binären Format gespeichert wird. <br /> Dateierweiterung: vmcx <br /> Standardspeicherort: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines|
 |Laufzeitstatus|VM-Runtime-Statusinformationen, die im binären Format gespeichert wird. <br />Dateierweiterung: vmrs und .vmgs <br />Standardspeicherort: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines|
|Virtuelle Festplatte|Speichert virtuelle Festplatten für den virtuellen Computer an. <br /> Dateierweiterung: VHD- oder vhdx <br />Standardspeicherort: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Hard Disks|
 |Automatische virtuelle Festplatte |Differenzierenden Datenträgerdateien für die Prüfpunkte für virtuelle Maschinen. <br /> Dateierweiterung: avhdx <br /> Standardspeicherort: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Hard Disks|
 |Checkpoint|Prüfpunkte werden in mehreren Prüfpunktdateien gespeichert. Jeder Prüfpunkt erstellt eine Konfigurationsdatei und eine Datei mit dem Laufzeitzustand. <br /> Dateinamenerweiterungen: vmrs und vmcx <br />Standardspeicherort: C:\ProgramData\Microsoft\Windows\Snapshots|

## <a name="what-happens-if-i-dont-upgrade-the-virtual-machine-configuration-version"></a>Was geschieht, wenn ich die Konfigurationsversion des virtuellen Computers kein Upgrade durchführe?

Wenn Sie virtuelle Computer, die Sie mit einer früheren Version von Hyper-V erstellt haben verfügen, sind einige Funktionen, die auf dem neueren Betriebssystem möglicherweise nicht mit dieser virtuellen Computer funktioniert, bis Sie die Konfigurationsversion aktualisieren Hostbetriebssystem verfügbar.

Eine grundsätzlich gilt wird empfohlen, die Version der Konfiguration wird aktualisiert, sobald Sie die Virtualisierungshosts auf eine neuere Version von Windows wurde erfolgreich aktualisiert haben und sicher sein, dass Sie nicht benötigen, um ein Rollback. Bei Verwendung der [cluster-Upgrades des clusterbetriebssystems](https://docs.microsoft.com/windows-server/failover-clustering/Cluster-Operating-System-Rolling-Upgrade) Feature in der Regel wäre dies nach der Aktualisierung der Funktionsebene des Clusters. Auf diese Weise profitieren Sie von neuen Features "," Interner Änderungen "und" sowie Optimierungen.

>[!NOTE]
>Nachdem die VM-Konfigurationsversion aktualisiert wurde, wird nicht der virtuellen Computer auf Hosts gestartet werden, die nicht die Version der aktualisierten Konfiguration unterstützen.

Die folgende Tabelle zeigt die minimalen VM-Konfigurationsversion erforderlich, um einige Funktionen der Hyper-V verwenden.

|Feature|Mindestversion für VM-Konfiguration|
|---|---|
|Speicher bei laufendem Systembetrieb hinzufügen/entfernen|6.2|
|Sicherer Start für Linux-VMs|6.2|
|Produktionsprüfpunkte|6.2|
|PowerShell Direct |6.2|
|VM-Gruppierung|6.2|
|Virtual Trusted Platform Module (vTPM)|7.0|
|Virtuellen Computer mit mehreren Warteschlangen (VMMQ)|7.1|
|XSAVE-Unterstützung|8.0|
|Wichtige Speicherlaufwerk|8.0|
|Unterstützung für Gastbetriebssysteme virtualisierungsbasierte Sicherheit (VBS)|8.0|
|Geschachtelte Virtualisierung|8.0|
|Anzahl virtueller Prozessoren|8.0|
|Große virtuelle Computer|8.0|
|Erhöhen der maximalen Standardanzahl für virtuelle Geräte, die auf 64 pro Gerät (z. B. Netzwerk- und zugewiesenen Geräte)|8.3|
|Zusätzliche Prozessorfunktionen Perfmon ermöglichen|9.0|
|Automatisch verfügbar zu machen [gleichzeitige multithreading](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#background) Konfiguration für virtuelle Computer auf Hosts mit der [Core Scheduler](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#windows-server-2019-hyper-v-defaults-to-using-the-core-scheduler)|9.0|
|Unterstützung für den Ruhezustand|9.0|

Weitere Informationen zu diesen Funktionen finden Sie unter [Neues in Hyper-V unter Windows Server](../What-s-new-in-Hyper-V-on-Windows.md).

