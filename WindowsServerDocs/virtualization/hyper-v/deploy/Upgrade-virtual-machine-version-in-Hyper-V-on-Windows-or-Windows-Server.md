---
title: Aktualisieren der Version virtueller Computer in Hyper-V unter Windows 10 oder Windows Server
description: Enthält Anweisungen und Überlegungen zum Aktualisieren der Version eines virtuellen Computers.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 897f2454-5aee-445c-a63e-f386f514a0f6
author: jasongerend
ms.author: jgerend
ms.date: 05/22/2019
ms.openlocfilehash: 96678dfab2a3d5b6f503d8ce9d00850a3c437b35
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392930"
---
# <a name="upgrade-virtual-machine-version-in-hyper-v-on-windows-10-or-windows-server"></a>Aktualisieren der Version virtueller Computer in Hyper-V unter Windows 10 oder Windows Server

>Gilt für: Windows 10, Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

Machen Sie die neuesten Hyper-V-Features auf Ihren virtuellen Computern verfügbar, indem Sie die Konfigurations Version aktualisieren. Gehen Sie dazu erst wie folgt vor:

- Sie aktualisieren Ihre Hyper-V-Hosts auf die neueste Version von Windows oder Windows Server.
- Sie aktualisieren die Cluster Funktionsebene.
- Sie müssen den virtuellen Computer nicht auf einen Hyper-V-Host verschieben, auf dem eine frühere Version von Windows oder Windows Server ausgeführt wird.

Weitere Informationen finden Sie unter [Cluster Operating System Rolling Upgrade](../../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md) und [Durchführen eines parallelen Upgrades eines Hyper-V-Host Clusters in VMM](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade).

## <a name="step-1-check-the-virtual-machine-configuration-versions"></a>Schritt 1: Überprüfen Sie die Konfigurations Versionen der virtuellen Maschine.

1. Klicken Sie auf dem Windows-Desktop auf die Schaltfläche „Start“, und geben Sie einen beliebigen Teil des Namens **Windows PowerShell** ein.
2. Klicken Sie mit der rechten Maustaste auf Windows PowerShell, und wählen Sie **als Administrator ausführen**.
3. Verwenden Sie das Cmdlet [Get-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm). Führen Sie den folgenden Befehl aus, um die Versionen Ihrer virtuellen Computer zu erhalten.

```PowerShell
Get-VM * | Format-Table Name, Version
```

Sie können die Konfigurations Version auch im Hyper-V-Manager anzeigen, indem Sie den virtuellen Computer auswählen und sich die Registerkarte **Zusammenfassung** ansehen.

## <a name="step-2-upgrade-the-virtual-machine-configuration-version"></a>Schritt 2: Aktualisieren der Konfigurations Version des virtuellen Computers

1. Fahren Sie den virtuellen Computer im Hyper-V-Manager herunter.
2. Wählen Sie Aktion > upgradekonfigurationsversion aus. Wenn diese Option für den virtuellen Computer nicht verfügbar ist, befindet er sich bereits in der höchsten Konfigurations Version, die vom Hyper-V-Host unterstützt wird.

Um die Konfigurations Version des virtuellen Computers mithilfe von Windows PowerShell zu aktualisieren, verwenden Sie das Cmdlet [Update-VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion) . Führen Sie den folgenden Befehl aus, wobei "VMName" der Name des virtuellen Computers ist.

```PowerShell
Update-VMVersion <vmname>
```

## <a name="supported-virtual-machine-configuration-versions"></a>Unterstützte Konfigurations Versionen für virtuelle Computer

Führen Sie das PowerShell-Cmdlet [Get-vmhostsupportedversion](https://docs.microsoft.com/powershell/module/hyper-v/get-vmhostsupportedversion) aus, um die vom Hyper-V-Host unterstützten VM-Konfigurations Versionen anzuzeigen. Wenn Sie einen virtuellen Computer erstellen, wird er mit der Standard Konfigurations Version erstellt. Führen Sie den folgenden Befehl aus, um zu sehen, was der Standardwert ist.

```PowerShell
Get-VMHostSupportedVersion -Default
```

Wenn Sie einen virtuellen Computer erstellen müssen, der zu einem Hyper-V-Host verschoben werden kann, auf dem eine ältere Version von Windows ausgeführt wird, verwenden Sie das Cmdlet [New-VM](https://docs.microsoft.com/powershell/module/hyper-v/new-vm) mit dem Parameter-Version. Um beispielsweise einen virtuellen Computer zu erstellen, den Sie auf einen Hyper-V-Host mit Windows Server 2012 R2 verschieben können, führen Sie den folgenden Befehl aus. Mit diesem Befehl wird ein virtueller Computer namens "WindowsCV5" mit der Konfigurations Version 5,0 erstellt.

```PowerShell
New-VM -Name "WindowsCV5" -Version 5.0
```

>[!NOTE]
>Sie können virtuelle Maschinen importieren, die für einen Hyper-V-Host erstellt wurden, auf dem eine ältere Version von Windows ausgeführt wird, oder Sie aus einer Sicherung wiederherstellen. Wenn die Konfigurations Version des virtuellen Computers nicht als unterstützt für das Hyper-V-Host Betriebssystem in der folgenden Tabelle aufgeführt ist, müssen Sie die VM-Konfigurations Version aktualisieren, bevor Sie den virtuellen Computer starten können.

### <a name="supported-vm-configuration-versions-for-long-term-servicing-hosts"></a>Unterstützte VM-Konfigurations Versionen für lang Zeit Wartungs Hosts

In der folgenden Tabelle sind die VM-Konfigurations Versionen aufgelistet, die auf Hosts unterstützt werden, auf denen eine langfristige Wartungsversion von Windows ausgeführt wird.

| Windows-Version des Hyper-V-Hosts | 9,1 | 9,0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
| --- |---|---|---|---|---|---|---|---|---|---|
|Windows Server 2019|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise LTSC 2019|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2016 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2015 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|
|Windows Server 2012 R2|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|
|Windows 8.1|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|

### <a name="supported-vm-configuration-versions-for-semi-annual-channel-hosts"></a>Unterstützte VM-Konfigurations Versionen für halbjährliche channelhosts

In der folgenden Tabelle werden die Versionen der VM-Konfiguration für Hosts aufgelistet, auf denen eine derzeit unterstützte halbjährliche Kanal Version von Windows ausgeführt wird. Weitere Informationen zu halbjährlichen Kanal Versionen von Windows finden Sie auf den folgenden Seiten für [Windows Server](../../../get-started-19/servicing-channels-19.md) und [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview#servicing-channels) .

| Windows-Version des Hyper-V-Hosts | 9,1 | 9,0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
| --- |---|---|---|---|---|---|---|---|---|---|
| Windows 10-Update vom Mai 2019 (Version 1903) |&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;| &#10004;|
| Windows Server, Version 1903 |&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;| &#10004;|
|Windows Server, Version 1809|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10-Update vom Oktober 2018 (Version 1809)|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server, Version 1803|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 April 2018-Update (Version 1803)|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Fall Creators Update (Version 1709)|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Creators Update (Version 1703)|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Anniversary Update (Version 1607)|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|

## <a name="why-should-i-upgrade-the-virtual-machine-configuration-version"></a>Warum sollte ich die VM-Konfigurations Version aktualisieren?

Beim Verschieben oder Importieren einer virtuellen Maschine auf einen Computer, auf dem Hyper-V unter Windows Server 2019, Windows Server 2016 oder Windows 10 ausgeführt wird, wird die Konfiguration der virtuellen Maschine nicht automatisch aktualisiert. Dies bedeutet, dass Sie den virtuellen Computer zurück auf einen Hyper-V-Host verschieben können, auf dem eine frühere Version von Windows oder Windows Server ausgeführt wird. Dies bedeutet jedoch auch, dass Sie einige der neuen Features für virtuelle Computer erst verwenden können, wenn Sie die Konfigurations Version manuell aktualisieren. Nachdem Sie das Upgrade ausgeführt haben, können Sie die Konfigurations Version des virtuellen Computers nicht herabstufen.

Die Konfigurations Version des virtuellen Computers stellt die Kompatibilität der Konfiguration der virtuellen Maschine, des gespeicherten Zustands und der Momentaufnahme Dateien mit der Hyper-V-Version dar. Wenn Sie die Konfigurations Version aktualisieren, ändern Sie die Dateistruktur, die zum Speichern der Konfiguration der virtuellen Maschinen und der Prüf Punkt Dateien verwendet wird. Außerdem aktualisieren Sie die Konfigurations Version auf die aktuelle Version, die von diesem Hyper-V-Host unterstützt wird. Aktualisierte virtuelle Computer verwenden ein neues Konfigurationsdateiformat, das entworfen wurde, um die Effizienz beim Lesen und Schreiben von VM-Konfigurationsdaten zu steigern. Das Upgrade verringert auch das Potenzial von Datenbeschädigungen bei einem Speicherausfall.

In der folgenden Tabelle sind Beschreibungen, Dateinamen Erweiterungen und Standard Speicherorte für die einzelnen Dateitypen aufgeführt, die für neue oder aktualisierte virtuelle Maschinen verwendet werden.

 |Dateitypen virtueller Computer | Beschreibung|
 |---|---|
|Konfiguration |Konfigurationsinformationen für virtuelle Computer, die im Binärdatei Format gespeichert werden. <br /> Dateinamenerweiterung: vmcx <br /> Standard Speicherort: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines|
 |Lauf Zeit Status|Lauf Zeit Zustandsinformationen des virtuellen Computers, die im Binärdatei Format gespeichert werden. <br />Dateinamenerweiterung:. VMRS und. vmgs <br />Standard Speicherort: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines|
|Virtuelle Festplatte|Speichert virtuelle Festplatten für die virtuelle Maschine. <br /> Dateinamenerweiterung: VHD-oder vhdx-Datei <br />Standard Speicherort: C:\ProgramData\Microsoft\Windows\Hyper-v\virtuelle Festplatten|
 |Automatische virtuelle Festplatte |Differenzierende Datenträger Dateien, die für Prüfpunkte virtueller Maschinen verwendet werden. <br /> Dateinamenerweiterung:. avhdx <br /> Standard Speicherort: C:\ProgramData\Microsoft\Windows\Hyper-v\virtuelle Festplatten|
 |Checkpoint|Prüfpunkte werden in mehreren Prüfpunktdateien gespeichert. Jeder Prüfpunkt erstellt eine Konfigurationsdatei und eine Datei mit dem Laufzeitzustand. <br /> Dateinamen Erweiterungen:. VMRS und. vmcx <br />Standard Speicherort: C:\ProgramData\Microsoft\Windows\Snapshots|

## <a name="what-happens-if-i-dont-upgrade-the-virtual-machine-configuration-version"></a>Was geschieht, wenn ich die Konfigurations Version des virtuellen Computers nicht Aktualisierungs?

Wenn Sie über virtuelle Computer verfügen, die Sie mit einer früheren Version von Hyper-V erstellt haben, funktionieren einige Features, die auf dem neueren Host Betriebssystem verfügbar sind, möglicherweise erst dann für diese virtuellen Maschinen, wenn Sie die Konfigurations Version aktualisieren.

Als allgemeine Richtlinie wird empfohlen, die Konfigurations Version zu aktualisieren, nachdem Sie die Virtualisierungshosts erfolgreich auf eine neuere Version von Windows aktualisiert haben, und Sie können sicher sein, dass kein Rollback erforderlich ist. Wenn Sie das Feature für parallele [Upgrades des Cluster](https://docs.microsoft.com/windows-server/failover-clustering/Cluster-Operating-System-Rolling-Upgrade) Betriebssystems verwenden, liegt dies in der Regel nach dem Aktualisieren der Cluster Funktionsebene. Auf diese Weise profitieren Sie auch von neuen Features, internen Änderungen und Optimierungen.

>[!NOTE]
>Nachdem die VM-Konfigurations Version aktualisiert wurde, kann der virtuelle Computer nicht auf Hosts gestartet werden, die die aktualisierte Konfigurations Version nicht unterstützen.

In der folgenden Tabelle ist die Mindestversion der VM-Konfiguration aufgeführt, die für die Verwendung einiger Hyper-V-Features erforderlich ist.

|Feature|Mindestversion der VM-Konfiguration|
|---|---|
|Speicher bei laufendem Systembetrieb hinzufügen/entfernen|6.2|
|Sicherer Start für Linux-VMs|6.2|
|Produktionsprüfpunkte|6.2|
|PowerShell Direct |6.2|
|VM-Gruppierung|6.2|
|Virtual Trusted Platform Module (vTPM)|7.0|
|Mehrere Warteschlangen für virtuelle Computer (vmmq)|7.1|
|XSAVE-Unterstützung|8.0|
|Schlüsselspeicher Laufwerk|8.0|
|Virtualisierungsbasierte Sicherheitsunterstützung (VSB)|8.0|
|Netzwerkvirtualisierung|8.0|
|Anzahl virtueller Prozessoren|8.0|
|Große Arbeitsspeicher-VMS|8.0|
|Erhöhen Sie die standardmäßige maximale Anzahl von virtuellen Geräten auf 64 pro Gerät (z. b. Netzwerk und zugewiesene Geräte).|8.3|
|Zusätzliche Prozessor Features für Perfmon zulassen|9,0|
|Automatisches Bereitstellen der [Multithreading](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#background) -Konfiguration für VMS, die auf Hosts mit dem [Kern Planer](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#windows-server-2019-hyper-v-defaults-to-using-the-core-scheduler) ausgeführt werden|9,0|
|Ruhe Zustands Unterstützung|9,0|

Weitere Informationen zu diesen Features finden Sie unter [Neues in Hyper-V unter Windows Server](../What-s-new-in-Hyper-V-on-Windows.md).

