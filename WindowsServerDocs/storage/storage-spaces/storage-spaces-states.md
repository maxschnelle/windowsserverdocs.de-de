---
title: "\"Direkte Speicherplätze\" Integrität des Netzwerkspeichers und Betriebszustände"
description: Informationen zum Suchen und zu verstehen, die anderen integritätsprüfung und Betriebszustände von "direkte Speicherplätze" und Speicherplätze (einschließlich der physischen Datenträger, Pools und virtuelle Datenträger), und was für sie ausführen möchten.
keywords: Speicherplätze getrennt, virtuellen Datenträger, physischer Datenträger beeinträchtigt.
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-spaces
manager: brianlic
ms.openlocfilehash: 5090a68270438bd9a06c7d50f9d4abca066d31e6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849141"
---
# <a name="troubleshoot-storage-spaces-direct-health-and-operational-states"></a>Problembehandlung für "direkte Speicherplätze" Integritäts- und Betriebsstatus

> Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, WindowsServer (Halbjährlicher Kanal), Windows 10, Windows 8.1

In diesem Thema wird beschrieben, die Integrität und Betriebszustände von Speicherpools, virtuelle Datenträger (die unterhalb der Volumes auf Speicherplätzen befinden) und Laufwerken in ["direkte Speicherplätze"](storage-spaces-direct-overview.md) und [Speicherplätze](overview.md). Diese Zustände können überaus hilfreich sein, wenn beim Behandeln von verschiedenen Problemen wie z. B. warum Sie einen virtuellen Datenträger nicht aufgrund einer schreibgeschützten Konfiguration löschen können. Es wird auch erläutert, warum ein Laufwerk eines Pools (die CannotPoolReason) hinzugefügt werden kann.

Für Speicherplätze gelten die drei wichtigsten Objekte - *physische Datenträger* (Festplatten, SSDs, usw.) hinzugefügt werden, eine *Speicherpool*, Virtualisierung von Speicher, damit Sie erstellen können *virtuelle Datenträger* aus den freien Speicherplatz in den Pool, wie hier gezeigt. Pool-Metadaten werden in einzelnen Laufwerke in den Pool geschrieben. Volumes, auf die virtuellen Datenträger erstellt, und speichern Sie Ihre Dateien, aber wir wollen nicht Volumes hier sprechen.

![Physische Datenträger werden zu einem Speicherpool hinzugefügt werden soll, und klicken Sie dann virtuelle Datenträger erstellt, aus der Speicherplatz des Speicherpools](media/storage-spaces-states/storage-spaces-object-model.png)

Sie können Integritäts- und Betriebsstatus im Server-Manager oder mit PowerShell anzeigen. Es folgt ein Beispiel einer Vielzahl von (vor allem schlechte) Integritäts- und Betriebsstatus auf einen "direkte Speicherplätze"-Cluster, der meisten der Clusterknoten nicht vorhanden ist (mit der rechten Maustaste in den Spaltenüberschriften hinzufügen **Betriebsstatus**). Dies ist eine viel Spaß beim Cluster nicht.

![Server-Manager zeigt die Ergebnisse der beiden fehlenden Knoten in einem "direkte Speicherplätze"-Cluster – viele fehlende physische Datenträger und virtuelle Datenträger in einem fehlerhaften Zustand](media/storage-spaces-states/unhealthy-disks-in-server-manager.png)

## <a name="storage-pool-states"></a>Speicher-Pool-Status

Jedem Speicherpool verfügt über einen Integritätsstatus - **fehlerfrei**, **Warnung**, oder **unbekannte**/**fehlerhaft**, auch als ein oder mehrere Betriebszustände.

Um herauszufinden, welcher Zustand in ein Pool ist, verwenden Sie die folgenden PowerShell-Befehle:

```PowerShell
Get-StoragePool -IsPrimordial $False | Select-Object HealthStatus, OperationalStatus, ReadOnlyReason
```

Hier ist eine Beispielausgabe, die einen Speicherpool in den unbekannten Integritätsstatus mit der nur-Lese Betriebsstatus angezeigt:

```
FriendlyName                OperationalStatus HealthStatus IsPrimordial IsReadOnly
------------                ----------------- ------------ ------------ ----------
S2D on StorageSpacesDirect1 Read-only         Unknown      False        True
```

Den folgenden Abschnitten wird die Integrität und Betriebszustände.

### <a name="pool-health-state-healthy"></a>Pool-Integritätsstatus: Fehlerfrei

|Betriebszustand    |Beschreibung|
|---------            |---------  |
|OK|Der Speicherpool ist fehlerfrei.|

### <a name="pool-health-state-warning"></a>Pool-Integritätsstatus: Warnung

Wenn der Speicherpool ist der **Warnung** Integrität aufweist, es bedeutet, dass der Pool zugegriffen werden kann, aber ein oder mehrere Laufwerke fehlgeschlagen ist oder fehlt. Daher kann der Speicherpool Stabilität beeinträchtigt haben.

|Betriebszustand    |Beschreibung|
|---------            |---------  |
|Verringert|Es befinden sich fehlerhaften oder fehlenden Laufwerke im Speicherpool. Diese Bedingung tritt nur mit Laufwerken, die Pool-Metadaten zu hosten. <br><br>**Aktion**: Überprüfen Sie den Status der Laufwerke aus, und Ersetzen Sie alle fehlerhaften Laufwerke aus, bevor weitere Fehler vorhanden sind.|

### <a name="pool-health-state-unknown-or-unhealthy"></a>Pool-Integritätsstatus: Unbekannte oder fehlerhaft

Wenn ein Speicherpool ist der **unbekannte** oder **fehlerhaft** Integrität aufweist, es bedeutet, dass der Speicherpool schreibgeschützt ist und kann nicht geändert werden, bis Sie an der Pool zurückgegeben wird das **Warnung**oder **OK** Integritätsstatus.

|Betriebszustand    |Nur-Lese Ursache |Beschreibung|
|---------            |---------       |--------   |
|Schreibgeschützt|Unvollständig|Dies kann auftreten, wenn der Speicherpool verliert seine [Quorum](understand-quorum.md), was bedeutet, dass die meisten Laufwerke im Pool bestanden haben oder aus irgendeinem Grund offline sind. Beim ein Pool sein Quorum verliert, legt Speicherplätze der Poolkonfiguration automatisch in den schreibgeschützten Modus, bis wieder genügend Laufwerke verfügbar sind.<br><br>**Aktion:** <br>1. Schließen Sie alle fehlenden Laufwerke aus, und fahren Sie alle Server online, wenn Sie "direkte Speicherplätze" verwenden. <br>2. Legen Sie den Pool wieder mit Lese-/ Schreibzugriff durch Öffnen einer PowerShell-Sitzungs mit Administratorrechten, und klicken Sie dann eingeben:<br><br> <code>Get-StoragePool <PoolName> -IsPrimordial $False \| Set-StoragePool -IsReadOnly $false</code>|
||Richtlinie|Ein Administrator festlegen den Speicherpool in den schreibgeschützten Modus.<br><br>**Aktion:** Um einen clusterspeicherpool Lese-/ Schreibzugriff-Zugriff im Failovercluster-Manager festzulegen, wechseln Sie zu **Pools**mit der rechten Maustaste auf den Pool, und wählen Sie dann **Online schalten**.<br><br>Öffnen Sie für andere Server und die PCs eine PowerShell-Sitzung mit Administratorrechten, und geben Sie dann aus:<br><br><code>Get-StoragePool <PoolName> \| Set-StoragePool -IsReadOnly $false</code><br><br> |
||Starten|Speicherplätze gestartet oder Warten von Laufwerken im Pool verbunden sein. Dabei sollte es sich um einen vorübergehenden Zustand handeln. Nachdem vollständig gestartet wurde, sollte der Pool in einen anderen operativen Zustand übergehen.<br><br>**Aktion:** Wenn der Pool im bleibt die *ab* angeben, stellen Sie sicher, dass alle Laufwerke im Pool ordnungsgemäß verbunden sind.|

Siehe auch [ändern einen Speicherpool aus, die über eine Read-Only-Konfiguration verfügt](https://social.technet.microsoft.com/wiki/contents/articles/14861.modifying-a-storage-pool-that-has-a-read-only-configuration.aspx).

## <a name="virtual-disk-states"></a>Status des virtuellen Datenträgers

In Storage Spaces werden Volumes auf virtuelle Datenträger (Speicherplätze) platziert, die in einem Pool freier Speicherplatz beansprucht werden. Alle virtuellen Datenträger verfügt über einen Integritätsstatus - **fehlerfrei**, **Warnung**, **fehlerhaft**, oder **unbekannte** sowie eine oder mehrere Betriebszustände.

Um herauszufinden, welche Status virtuelle Datenträger werden, verwenden Sie die folgenden PowerShell-Befehle aus:

```PowerShell
Get-VirtualDisk | Select-Object FriendlyName,HealthStatus, OperationalStatus, DetachedReason
```

Hier ist ein Beispiel der Ausgabe zeigt einen getrennten virtuellen Datenträger und eine heruntergestuft/unvollständige virtuelle Festplatte:

```
FriendlyName HealthStatus OperationalStatus      DetachedReason
------------ ------------ -----------------      --------------
Volume1      Unknown      Detached               By Policy
Volume2      Warning      {Degraded, Incomplete} None
```

Den folgenden Abschnitten wird die Integrität und Betriebszustände.

### <a name="virtual-disk-health-state-healthy"></a>Integritätsstatus des virtuellen Datenträgers: Fehlerfrei

|Betriebszustand    |Beschreibung|
|---------            |---------          |
|OK    |Der virtuelle Datenträger ist fehlerfrei.|
|Suboptimale    |Daten wird nicht gleichmäßig auf Laufwerken geschrieben. <br><br>**Aktion**: Optimieren der laufwerknutzung im Speicherpool mit der [Optimize-StoragePool](https://technet.microsoft.com/itpro/powershell/windows/storage/optimize-storagepool) Cmdlet.|

### <a name="virtual-disk-health-state-warning"></a>Integritätsstatus des virtuellen Datenträgers: Warnung

Wenn der virtuelle Datenträger wird ein **Warnung** Integrität aufweist, es bedeutet, dass eine oder mehrere Kopien Ihrer Daten nicht verfügbar sind, aber die Speicherplätze können mindestens eine Kopie Ihrer Daten weiterhin lesen.

|Betriebszustand    |Beschreibung|
|---------            |---------          |
|Im Dienst            |Windows ist des virtuellen Datenträgers, z. B. nach dem Hinzufügen oder entfernen ein Laufwerk repariert werden. Wenn die Reparatur abgeschlossen ist, muss der virtuelle Datenträger an den Zustand des OK zurückgeben.|
|Unvollständig           |Die resilienz des virtuellen Datenträgers wird reduziert, da eine oder mehrere Festplatten fehlgeschlagen ist oder fehlt. Allerdings enthalten die fehlenden Laufwerke auf dem neuesten Stand Kopien Ihrer Daten.<br><br> **Aktion**: <br>1. Schließen Sie alle fehlenden Laufwerke wieder, ersetzen Sie alle fehlerhaften Laufwerke aus, und wenn Sie "direkte Speicherplätze" verwenden, schalten Sie online alle Server, die offline sind. <br>2. Wenn Sie "direkte Speicherplätze" nicht verwenden, als Nächstes reparieren Sie die virtuellen Datenträger mithilfe der [Repair-VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) Cmdlet.<br> "Direkte Speicherplätze" startet automatisch eine Reparatur, bei Bedarf nach dem Wiederherstellen der Verbindung oder ein Laufwerk zu ersetzen.|
|Verringert             |Die resilienz des virtuellen Datenträgers wird reduziert, da eine oder mehrere Festplatten Fehler oder fehlen und veraltete Kopien Ihrer Daten auf diesen Laufwerken vorhanden sind. <br><br>**Aktion**: <br> 1. Schließen Sie alle fehlenden Laufwerke wieder, ersetzen Sie alle fehlerhaften Laufwerke aus, und wenn Sie "direkte Speicherplätze" verwenden, schalten Sie online alle Server, die offline sind. <br> 2. Wenn Sie "direkte Speicherplätze" nicht verwenden, als Nächstes reparieren Sie die virtuellen Datenträger mithilfe der [Repair-VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) Cmdlet. <br>"Direkte Speicherplätze" startet automatisch eine Reparatur, bei Bedarf nach dem Wiederherstellen der Verbindung oder ein Laufwerk zu ersetzen.|

### <a name="virtual-disk-health-state-unhealthy"></a>Integritätsstatus des virtuellen Datenträgers: Unhealthy

Wenn ein virtueller Datenträger ist einer **fehlerhaft** Integritätsstatus, dass einige oder alle Daten auf dem virtuellen Datenträger ist zurzeit nicht verfügbar.

|Betriebszustand    |Beschreibung|
|---------            |--------   |
|Keine Redundanz|Der virtuelle Datenträger hat Daten verloren gehen, da zu viele Laufwerke fehlgeschlagen ist.<br><br>**Aktion**: Ersetzen Sie fehlerhafte Laufwerke aus, und klicken Sie dann wiederherstellen Sie die Daten aus einer Sicherung.|

### <a name="virtual-disk-health-state-informationunknown"></a>Integritätsstatus des virtuellen Datenträgers: Informationen/unbekannt

Das virtuelle Laufwerk kann auch sein, der **Informationen** Integritätsstatus (Siehe das Storage Spaces Control Panel-Element) oder **unbekannte** Integrität Status (wie in PowerShell gezeigt), wenn ein Administrator den virtuellen Datenträger übernommen hat. Offline oder wurde der virtuelle Datenträger getrennt werden.

|Betriebszustand    |Getrennte Grund |Beschreibung|
|---------            |---------       |--------   |
|„Getrennt“             |Von der Richtlinie            |Ein Administrator hat Sie den virtuellen Datenträger offline, oder legen Sie die virtuelle Datenträger manuell Anlage erforderlich ist, in diesem Fall müssen Sie den virtuellen Datenträger manuell angefügt wird, jedes Mal, wenn Windows neu gestartet wird.,<br><br>**Aktion**: Schalten Sie den virtuellen Datenträger wieder online geschaltet. Zu diesem Zweck, wenn der virtuelle Datenträger in einen clusterspeicherpool befindet, wählen Sie im Failovercluster-Manager **Storage** > **Pools** > **virtuelle Datenträger** , wählen Sie den virtuellen Datenträger, die zeigt, die **Offline** Status, und wählen Sie dann **Online schalten**. <br><br>Um einen virtuellen Datenträger wieder online geschaltet, nicht in einem Cluster zu bringen, öffnen Sie eine PowerShell-Sitzung als Administrator aus, und wiederholen Sie dann mithilfe des folgenden Befehls:<br><br> <code>Get-VirtualDisk \| Where-Object -Filter { $_.OperationalStatus -eq "Detached" } \| Connect-VirtualDisk</code><br><br>Um automatisch alle nicht gruppierten virtuellen Datenträger anzufügen, nachdem Windows neu gestartet wurde, öffnen Sie eine PowerShell-Sitzung als Administrator aus, und klicken Sie dann verwenden Sie den folgenden Befehl:<br><br> <code>Get-VirtualDisk \| Set-VirtualDisk -ismanualattach $false</code>|
|            |Mehrheit Datenträger fehlerhaft |Zu viele Laufwerke, die von diesem virtuellen Datenträger verwendet werden. Fehler bei, fehlen oder veralteten Daten.   <br><br>**Aktion**: <br> 1. Schließen Sie alle fehlenden Laufwerke, und wenn Sie "direkte Speicherplätze" verwenden, schalten Sie online alle Server, die offline sind. <br> 2. Nachdem alle Laufwerke und Server online sind, ersetzen Sie alle fehlerhaften Laufwerke. Finden Sie unter [Integritätsdienst](../../failover-clustering/health-service-overview.md) Details. <br>"Direkte Speicherplätze" startet automatisch eine Reparatur, bei Bedarf nach dem Wiederherstellen der Verbindung oder ein Laufwerk zu ersetzen.<br>3. Wenn Sie "direkte Speicherplätze" nicht verwenden, als Nächstes reparieren Sie die virtuellen Datenträger mithilfe der [Repair-VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) Cmdlet.  <br><br>Wenn weitere Datenträger fehlgeschlagen ist, als Sie Kopien Ihrer Daten und des virtuellen Datenträgers nicht reparierten dazwischen Fehler war, alle Daten auf dem virtuellen Datenträger dauerhaft verloren ist. Löschen Sie in diesem Fall leider den virtuellen Datenträger, erstellen Sie einen neuen virtuellen Datenträger und dann aus einer Sicherung wiederherstellen.|
|                     |Unvollständig |Nicht genügend Laufwerke sind vorhanden, um den virtuellen Datenträger zu lesen.    <br><br>**Aktion**: <br> 1. Schließen Sie alle fehlenden Laufwerke, und wenn Sie "direkte Speicherplätze" verwenden, schalten Sie online alle Server, die offline sind. <br> 2. Nachdem alle Laufwerke und Server online sind, ersetzen Sie alle fehlerhaften Laufwerke. Finden Sie unter [Integritätsdienst](../../failover-clustering/health-service-overview.md) Details. <br>"Direkte Speicherplätze" startet automatisch eine Reparatur, bei Bedarf nach dem Wiederherstellen der Verbindung oder ein Laufwerk zu ersetzen.<br>3. Wenn Sie "direkte Speicherplätze" nicht verwenden, als Nächstes reparieren Sie die virtuellen Datenträger mithilfe der [Repair-VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) Cmdlet.<br><br>Wenn weitere Datenträger fehlgeschlagen ist, als Sie Kopien Ihrer Daten und des virtuellen Datenträgers nicht reparierten dazwischen Fehler war, alle Daten auf dem virtuellen Datenträger dauerhaft verloren ist. Löschen Sie in diesem Fall leider den virtuellen Datenträger, erstellen Sie einen neuen virtuellen Datenträger und dann aus einer Sicherung wiederherstellen.|
| |Zeitüberschreitung|Anfügen des virtuellen Datenträgers hat zu lange gedauert <br><br> **Aktion:** Dies sollte nicht häufig vorkommen, sodass Sie möglicherweise versuchen, festzustellen, ob die Bedingung, in Zeit erfüllt. Oder Sie können versuchen, trennen den virtuellen Datenträger mit der [Disconnect-VirtualDisk](https://docs.microsoft.com/powershell/module/storage/disconnect-virtualdisk?view=win10-ps) -Cmdlet, klicken Sie dann mit der [Connect-VirtualDisk](https://docs.microsoft.com/powershell/module/storage/connect-virtualdisk?view=win10-ps) Cmdlets, die Verbindung herzustellen. |

## <a name="drive-physical-disk-states"></a>Laufwerkstatus (physischer Datenträger)

Den folgenden Abschnitten werden die Zustände, die ein Laufwerk in sein kann. Laufwerke in einem Pool werden dargestellt in PowerShell als *physischer Datenträger* Objekte.

### <a name="drive-health-state-healthy"></a>Laufwerk-Integritätsstatus: Fehlerfrei

|Betriebszustand    |Beschreibung|
|---------            |---------          |
|OK|Das Laufwerk ist fehlerfrei.|
|Im Dienst|Das Laufwerk ist einige interne organisatorische Vorgänge ausführen. Wenn die Aktion abgeschlossen ist, sollte das Laufwerk zum Zurückgeben der *OK* Integritätsstatus.|

### <a name="drive-health-state-warning"></a>Laufwerk-Integritätsstatus: Warnung

Ein Laufwerk in der Warnung Zustand kann lesen und Schreiben von Daten erfolgreich, aber hat ein Problem.

|Betriebszustand    |Beschreibung|
|---------            |---------          |
|Verlust der Kommunikation|Das Laufwerk ist nicht vorhanden. Wenn Sie "direkte Speicherplätze" verwenden, kann dies sein, da ein Server ausgefallen ist.<br><br>**Aktion**: Wenn Sie "direkte Speicherplätze" verwenden, schalten Sie alle Server wieder online geschaltet. Wenn, die sie nicht beheben, schließen Sie das Laufwerk wieder, ersetzen oder Abrufen ausführliche Diagnoseinformationen zu diesem Laufwerk mithilfe der Schritte zur Problembehandlung mithilfe der Windows-Fehlerberichterstattung > [Timeout des physischen Datenträgers](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-timed-out).|
|Aus Pool entfernen|Speicherplätze sind beim Entfernen des Laufwerks aus dem Speicherpool. <br><br> Dies ist ein temporärer Zustand. Nach der Deinstallation ist abgeschlossen, wenn für das System, das Laufwerk angefügt ist geht das Laufwerk in einem anderen Betriebsstatus (in der Regel OK) in einem ursprünglichen Pool.|
|Wartungsmodus starten|Speicherplätze sind gerade platzieren das Laufwerk in den Wartungsmodus versetzt, nachdem ein Administrator das Laufwerk in den Wartungsmodus versetzt. Dies ist ein temporärer Zustand: das Laufwerk muss sich in Kürze der *In den Wartungsmodus* Zustand.|
|In den Wartungsmodus|Ein Administrator platziert das Laufwerk im Wartungsmodus befindet, liest und schreibt in das Laufwerk anhalten. Dies erfolgt in der Regel vor dem Aktualisieren der Firmware oder beim Testen von Fehlern.<br><br>**Aktion**: Um das Laufwerk aus dem Wartungsmodus nutzen zu können, verwenden Sie die [Disable-StorageMaintenanceMode](https://technet.microsoft.com/itpro/powershell/windows/storage/disable-storagemaintenancemode) Cmdlet.|
|Beenden des Wartungsmodus|Ein Administrator hat das Laufwerk aus dem Wartungsmodus, und Speicherplätze das Laufwerk wieder online geschaltet wird. Dies ist ein temporärer Zustand: das Laufwerk sollte in Kürze in einen anderen Zustand – im Idealfall *fehlerfrei*.|
|Vorhersehbarer Fehler|Das Laufwerk hat gemeldet, dass sie in der Nähe fehlerhaften ist.<br><br>**Aktion**: Ersetzen Sie das Laufwerk an.|
|E/a-Fehler|Es wurde ein temporärer Fehler, die Zugriff auf das Laufwerk ein.<br><br>**Aktion**: <br>1. Wenn das Laufwerk an Übergang nicht die **OK** aufweist, können Sie versuchen, mithilfe der [Reset-PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk) Cmdlet, um das Laufwerk zu löschen. <br> 2. Verwendung [Repair-VirtualDisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk) die resilienz des betroffenen virtuellen Datenträger wiederherstellen. <br>3. Wenn dies häufiger auftritt, ersetzen Sie das Laufwerk ein.|
|Vorübergehender Fehler|Es wurde ein vorübergehender Fehler bei dem Laufwerk. Dies bedeutet normalerweise das Laufwerk hat nicht reagiert, aber es kann auch bedeuten, dass die Speicherplätze Schutzpartition aus dem Laufwerk nicht ordnungsgemäß entfernt wurde. <br><br>**Aktion**: <br>1. Wenn das Laufwerk an Übergang nicht die **OK** aufweist, können Sie versuchen, mithilfe der [Reset-PhysicalDisk](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk) Cmdlet, um das Laufwerk zu löschen. <br> 2. Verwendung [Repair-VirtualDisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk) die resilienz des betroffenen virtuellen Datenträger wiederherstellen. <br>3. Wenn dies häufiger auftritt, ersetzen Sie das Laufwerk, oder Abrufen von ausführliche Diagnoseinformationen zu diesem Laufwerk mithilfe der Schritte zur Problembehandlung mithilfe der Windows-Fehlerberichterstattung > [physischer Datenträger konnte nicht online geschaltet](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online).|
|Ungewöhnliche Latenz|Das Laufwerk ist langsam, gemessen an den Health-Dienst in "direkte Speicherplätze" ausführen.<br><br>**Aktion**: Wenn dies häufiger auftritt, ersetzen Sie das Laufwerk, damit es nicht die Leistung von Speicherplätzen als Ganzes reduziert wird.

### <a name="drive-health-state-unhealthy"></a>Laufwerk-Integritätsstatus: Unhealthy

Ein Laufwerk in einem fehlerhaften Zustand kann nicht gerade geschrieben oder zugegriffen werden.

|Betriebszustand    |Beschreibung|
|---------            |---------          |
|Nicht verwendet werden.|Dieses Laufwerk kann nicht von Speicherplätze verwendet werden. Weitere Informationen finden Sie unter ["direkte Speicherplätze" hardwareanforderungen](storage-spaces-direct-hardware-requirements.md); Wenn Sie "direkte Speicherplätze", nicht verwenden, finden Sie unter [Storage Spaces Overview](https://technet.microsoft.com/library/hh831739(v=ws.11).aspx#Requirements).|
|Teilen|Das Laufwerk wurde aus dem Pool getrennt werden.<br><br>**Aktion**: Setzen Sie das Laufwerk, löschen alle Daten aus dem Laufwerk und das Hinzufügen an den Pool ein leeres Laufwerk zurück. Zu diesem Zweck öffnen Sie eine PowerShell-Sitzung als Administrator führen Sie die [Reset-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) -Cmdlet, und führen Sie dann [Repair-VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk). <br><br>Führen Sie die Schritte zur Problembehandlung mithilfe der Windows-Fehlerberichterstattung, rufen Sie ausführliche Diagnoseinformationen zu diesem Laufwerk > [physischer Datenträger konnte nicht online geschaltet](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online).|
|Veraltete Metadaten|Speicherplätze wurde die alten Metadaten auf dem Laufwerk gefunden.<br><br>**Aktion**: Dabei sollte es sich um einen vorübergehenden Zustand handeln. Wenn das Laufwerk an OK Übergang nicht, können Sie ausführen [Repair-VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) zum Starten eines Reparaturvorgangs auf die betroffenen virtuellen Datenträger. Wenn es sich bei, die das Problem nicht behoben wird, können Sie das Laufwerk, auf dem Zurücksetzen der [Reset-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) -Cmdlet, alle Daten aus dem Laufwerk, und führen Sie dann [Repair-VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk).|
|Nicht erkannte Metadaten|Speicherplätze nicht erkannte Metadaten auf dem Laufwerk, in der Regel bedeutet, dass das Laufwerk Metadaten aus einem anderen Pool darauf zu finden.<br><br>**Aktion**: Um das Laufwerk zurücksetzen und den aktuellen Pool hinzufügen, setzen Sie das Laufwerk zurück. Öffnen Sie eine PowerShell-Sitzung als Administrator ausführen, um das Laufwerk zurückgesetzt, die [Reset-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) -Cmdlet, und führen Sie dann [Repair-VirtualDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk).|
|Fehlerhafter Datenträger|Das Laufwerk ist fehlgeschlagen und wird nicht mehr von Speicherplätzen verwendet werden.<br><br>**Aktion**: Ersetzen Sie das Laufwerk an. <br><br>Führen Sie die Schritte zur Problembehandlung mithilfe der Windows-Fehlerberichterstattung, rufen Sie ausführliche Diagnoseinformationen zu diesem Laufwerk > [physischer Datenträger konnte nicht online geschaltet](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online).|
|Hardwarefehler des Geräts|Es wurde ein Hardwarefehler auf diesem Laufwerk. <br><br>**Aktion**: Ersetzen Sie das Laufwerk an.|
|Aktualisieren der Firmware|Die Firmware auf dem Laufwerk wird von Windows aktualisiert werden. Dies ist ein temporärer Zustand, der in der Regel weniger als eine Minute dauert und während der Zeit, die anderen Laufwerken im Pool alle verarbeiten liest und schreibt. Weitere Informationen finden Sie unter [Aktualisieren von laufwerkfirmware](../update-firmware.md).|
|Starten|Das Laufwerk erhält betriebsbereit. Dies sollte ein temporärer Zustand – nach Abschluss des Vorgangs das Laufwerk in einen anderen operativen Zustand wechseln sollte.|

## <a name="reasons-a-drive-cant-be-pooled"></a>Aus Gründen, ein Laufwerk können nicht in einem Pool zusammengefasst werden

Einige Laufwerke sind, nicht nur in einem Speicherpool bereit. Sie können herausfinden, warum ein Laufwerk für anhand pooling geeignet ist, nicht die `CannotPoolReason` Eigenschaft eines physischen Datenträgers. Hier ist ein Beispiel-PowerShell-Skript zum Anzeigen der CannotPoolReason-Eigenschaft ein:

```PowerShell
Get-PhysicalDisk | Format-Table FriendlyName,MediaType,Size,CanPool,CannotPoolReason
```

Hier ist eine Beispielausgabe:

```
FriendlyName          MediaType          Size CanPool CannotPoolReason
------------          ---------          ---- ------- ----------------
ATA MZ7LM120HCFD00D3  SSD        120034123776   False Insufficient Capacity
Msft Virtual Disk     SSD         10737418240    True
Generic Physical Disk SSD        119990648832   False In a Pool
```

Die folgende Tabelle enthält ein wenig detaillierter auf jeder der Gründe an.

|Grund|Beschreibung|
|---|---|
|In einem pool|Das Laufwerk gehört bereits zu einem Speicherpool. <br><br>Laufwerke können jeweils nur einem einzelnen Speicherpool angehören. Um dieses Laufwerk in einem anderen Speicherpool zu verwenden, entfernen Sie zuerst das Laufwerk, aus dem vorhandenen Pool, der Speicherplätze zum Verschieben der Daten auf dem Laufwerk auf anderen Laufwerken im Pool darüber informiert werden. Oder das Laufwerk zurückgesetzt, wenn das Laufwerk ohne Benachrichtigung Speicherplätze aus dem Pool getrennt wurde. <br><br>Um ein Laufwerk sicher aus einem Speicherpool zu entfernen, verwenden [Remove-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/remove-physicaldisk), oder wechseln Sie zum Server-Manager > **Datei- und Speicherdienste** > **Speicherpools**, > **Physische Datenträger**mit der rechten Maustaste auf das Laufwerk, und wählen Sie dann **Datenträger entfernen**.<br><br>Verwenden Sie zum Zurücksetzen eines Laufwerks [Reset-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk).|
|Nicht fehlerfrei|Das Laufwerk ist nicht in einem fehlerfreien Zustand und möglicherweise ersetzt werden müssen.|
|Wechselmedien|Das Laufwerk wird als ein Wechseldatenträger klassifiziert. <br><br>Speicherplätze unterstützt keine Medien, die von Windows als Wechseldatenträger, z. B. Blu-Ray-Laufwerke erkannt werden. Obwohl Sie repariert viele Laufwerke werden Wechselmedien Slots im Allgemeinen Medien, die *klassifiziert* von Windows als Wechselmedium nicht für die Verwendung mit Speicherplätzen geeignet sind.|
|Vom Cluster verwendet|Das Laufwerk wird derzeit von einem Failovercluster verwendet.|
|Offline|Das Laufwerk ist offline. <br><br>Um alle offline-Laufwerke online und legen Lese-/Schreibzugriff zu bringen, öffnen Sie eine PowerShell-Sitzung als Administrator aus, und verwenden Sie die folgenden Skripts:<br><br><code>Get-Disk \| Where-Object -Property OperationalStatus -EQ "Offline" \| Set-Disk -IsOffline $false</code><br><br><code>Get-Disk \| Where-Object -Property IsReadOnly -EQ $true \| Set-Disk -IsReadOnly $false</code>|
|Nicht genügend Kapazität|Dies tritt normalerweise auf, wenn der freie Speicherplatz auf dem Laufwerk und verbraucht dabei Partitionen vorhanden sind. <br><br>**Aktion**: Löschen Sie alle Volumes auf dem Laufwerk, das alle Daten auf dem Laufwerk gelöscht werden. Eine Möglichkeit, dies ist die Verwendung der [Clear-Disk](https://docs.microsoft.com/powershell/module/storage/clear-disk?view=win10-ps) PowerShell-Cmdlet.|
|Überprüfung wird durchgeführt|Die [Integritätsdienst](../../failover-clustering/health-service-overview.md#supported-components-document) wird überprüft, um festzustellen, ob das Laufwerk oder die Firmware auf dem Laufwerk für die Verwendung der Serveradministrator genehmigt wird.|
|Fehler bei der Überprüfung|Die [Integritätsdienst](../../failover-clustering/health-service-overview.md#supported-components-document) konnten nicht überprüfen, um festzustellen, ob das Laufwerk oder die Firmware auf dem Laufwerk für die Verwendung der Serveradministrator genehmigt wird.|
|Nicht konforme Firmware|Die Firmware auf dem physischen Laufwerk befindet sich nicht in der Liste der genehmigten Firmwareversionen, die vom Serveradministrator mithilfe von angegeben die [Integritätsdienst](../../failover-clustering/health-service-overview.md#supported-components-document). |
|Hardware, die nicht kompatibel.|Das Laufwerk ist nicht in der Liste der genehmigten Speichermodelle, die vom Serveradministrator mithilfe von angegeben die [Integritätsdienst](../../failover-clustering/health-service-overview.md#supported-components-document).|

## <a name="see-also"></a>Siehe auch

- ["Direkte Speicherplätze"](storage-spaces-direct-overview.md)
- [Storage Spaces Direct-hardwareanforderungen](storage-spaces-direct-hardware-requirements.md)
- [Grundlegendes zu-Cluster und Pool-quorum](understand-quorum.md)