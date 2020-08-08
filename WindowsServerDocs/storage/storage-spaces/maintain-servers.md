---
title: Offline schalten eines direkte Speicherplätze Servers zur Wartung
ms.author: eldenc
manager: eldenc
ms.topic: article
author: eldenchristensen
ms.date: 10/08/2018
ms.assetid: 73dd8f9c-dcdb-4b25-8540-1d8707e9a148
ms.localizationpriority: medium
ms.openlocfilehash: d3fd3e1c6ca9a7493ac0bcdc809f68fe22f8fa67
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971087"
---
# <a name="taking-a-storage-spaces-direct-server-offline-for-maintenance"></a>Offline schalten eines direkte Speicherplätze Servers zur Wartung

> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält Anleitungen zum ordnungsgemäßen Neustart oder Herunterfahren von Servern mit [direkte Speicherplätze](storage-spaces-direct-overview.md).

Bei direkte Speicherplätze bedeutet das offline schalten eines Servers (durchführen des Servers) auch, dass Offline Teile des Speichers, der von allen Servern im Cluster gemeinsam genutzt wird, offline geschaltet werden. Hierfür ist es erforderlich, den Server, den Sie offline schalten möchten, anzuhalten (anzuhalten), Rollen auf andere Server im Cluster zu verschieben und zu überprüfen, ob alle Daten auf den anderen Servern im Cluster verfügbar sind, damit die Daten während der gesamten Wartung sicher und zugänglich bleiben.

Verwenden Sie die folgenden Verfahren, um einen Server in einem direkte Speicherplätze Cluster ordnungsgemäß anzuhalten, bevor Sie ihn offline schalten.

   > [!IMPORTANT]
   > Verwenden Sie zum Installieren von Updates auf einem direkte Speicherplätze Cluster das Cluster fähige aktualisieren (Cluster-Aware Update, Cau), das die in diesem Thema beschriebenen Verfahren automatisch ausführt, sodass Sie bei der Installation von Updates nicht über das verfügen. Weitere Informationen finden Sie unter [Cluster fähiges aktualisieren (Cau)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831694(v=ws.11)).

## <a name="verifying-its-safe-to-take-the-server-offline"></a>Es ist sicherzustellen, dass der Server sicher offline geschaltet wird.

Vergewissern Sie sich, dass alle Ihre Volumes fehlerfrei sind, bevor Sie einen Server zur Wartung offline schalten.

Öffnen Sie hierzu eine PowerShell-Sitzung mit Administrator Berechtigungen, und führen Sie dann den folgenden Befehl aus, um den Volumestatus anzuzeigen:

```PowerShell
Get-VirtualDisk
```

Im folgenden finden Sie ein Beispiel dafür, wie die Ausgabe aussehen könnte:
```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                OK                Healthy      True           1 TB
MyVolume2    Mirror                OK                Healthy      True           1 TB
MyVolume3    Mirror                OK                Healthy      True           1 TB
```

Vergewissern Sie sich, dass die Eigenschaft **healthstatus** für jedes Volume (virtueller Datenträger) Fehler **frei ist.**

Um dies in Failovercluster-Manager zu tun, navigieren Sie zu **Speicher**Datenträger  >  **Disks**.

Vergewissern Sie sich, dass in der Spalte **Status** für jedes Volume (virtueller Datenträger) **Online**angezeigt wird.

## <a name="pausing-and-draining-the-server"></a>Anhalten und Entleeren des Servers

Vor dem Neustart oder dem Herunterfahren des Servers können Sie alle Rollen, wie z. b. virtuelle Computer, anhalten und entladen. Dadurch haben direkte Speicherplätze die Möglichkeit, Daten ordnungsgemäß zu leeren und zu übertragen, um sicherzustellen, dass das Herunterfahren für alle auf diesem Server ausgelaufenden Anwendungen transparent ist.

   > [!IMPORTANT]
   > Halten Sie Cluster Server vor dem Neustart oder dem Herunterfahren immer an.

Führen Sie in PowerShell das folgende Cmdlet (als Administrator) aus, um anzuhalten und zu entladen.

```PowerShell
Suspend-ClusterNode -Drain
```

Wechseln Sie dazu in Failovercluster-Manager zu **Knoten**, klicken Sie mit der rechten Maustaste auf den Knoten, und **Wählen Sie**dann Ausgleichs  >  **Rollen**anhalten aus.

![Pause-entladen](media/maintain-servers/pause-drain.png)

Alle virtuellen Computer beginnen Live, auf andere Server im Cluster zu migrieren. Dies kann einige Minuten dauern.

   > [!NOTE]
   > Wenn Sie den Cluster Knoten anhalten und ordnungsgemäß entladen, führt Windows eine automatische Sicherheitsüberprüfung durch, um sicherzustellen, dass der Vorgang fortgesetzt werden kann. Wenn fehlerhafte Volumes vorhanden sind, werden Sie angehalten und warnen, dass der Vorgang nicht sicher fortgesetzt werden kann.

![Sicherheitsüberprüfung](media/maintain-servers/safety-check.png)

## <a name="shutting-down-the-server"></a>Der Server wird heruntergefahren.

Nachdem der Server die Ableitung abgeschlossen hat, wird er in Failovercluster-Manager und PowerShell als **angeh** alten angezeigt.

![Angehalten](media/maintain-servers/paused.png)

Sie können ihn jetzt problemlos neu starten oder Herunterfahren, genauso wie normal (z. b. mit den PowerShell-Cmdlets "Restart-Computer" oder "Start-Computer").

```PowerShell
Get-VirtualDisk

FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                Incomplete        Warning      True           1 TB
MyVolume2    Mirror                Incomplete        Warning      True           1 TB
MyVolume3    Mirror                Incomplete        Warning      True           1 TB
```

Der Status "unvollständig" oder "heruntergestuft" ist normal, wenn Knoten heruntergefahren werden oder der Cluster Dienst auf einem Knoten gestartet bzw. angehalten wird und keine Probleme auftreten sollten. Alle Ihre Volumes bleiben online und zugänglich.

## <a name="resuming-the-server"></a>Fortsetzen des Servers

Wenn Sie bereit sind, den Server zum erneuten Hosting von Arbeits Auslastungen zu starten, setzen Sie ihn fort.

Führen Sie in PowerShell das folgende Cmdlet aus (als Administrator), um fortzufahren.

```PowerShell
Resume-ClusterNode
```

Um die Rollen, die zuvor auf diesem Server ausgeführt wurden, zu verschieben, verwenden Sie das Flag "Optionales **Failback** ".

```PowerShell
Resume-ClusterNode –Failback Immediate
```

Wechseln Sie in Failovercluster-Manager zu **Knoten**, klicken Sie mit der rechten Maustaste auf den Knoten, und wählen Sie dann failrollrollbacks **Resume**  >  **wieder**aufnehmen aus.

![Resume-Failback](media/maintain-servers/resume-failback.png)

## <a name="waiting-for-storage-to-resync"></a>Warten auf Neusynchronisierung des Speichers

Beim Fortsetzen des Servers müssen alle neuen Schreibvorgänge, die während der Nichtverfügbarkeit nicht verfügbar waren, neu synchronisiert werden. Dies erfolgt automatisch. Mithilfe der intelligenten Änderungs Nachverfolgung ist es nicht notwendig, dass *alle* Daten gescannt oder synchronisiert werden. nur die Änderungen. Dieser Prozess wird gedrosselt, um die Auswirkungen auf produktionsworkloads zu mindern. Je nachdem, wie lange der Server angehalten wurde und wie viele neue Daten geschrieben wurden, kann es mehrere Minuten dauern, bis der Vorgang abgeschlossen ist.

Sie müssen warten, bis die erneute Synchronisierung beendet ist, bevor Sie andere Server im Cluster offline schalten.

Führen Sie in PowerShell das folgende Cmdlet aus (als Administrator), um den Fortschritt zu überwachen.

```PowerShell
Get-StorageJob
```
Im folgenden finden Sie eine Beispielausgabe, die die Neusynchronisierungs Aufträge (reparieren) anzeigt:
```
Name   IsBackgroundTask ElapsedTime JobState  PercentComplete BytesProcessed BytesTotal
----   ---------------- ----------- --------  --------------- -------------- ----------
Repair True             00:06:23    Running   65              11477975040    17448304640
Repair True             00:06:40    Running   66              15987900416    23890755584
Repair True             00:06:52    Running   68              20104802841    22104819713
```

Das **bytesTotal** zeigt, wie viel Speicher neu synchronisiert werden muss. Die **prozentuumfassende** Ausführung zeigt den Fortschritt an.

   > [!WARNING]
   > Es ist nicht sicher, dass ein anderer Server offline geschaltet wird, bis diese Reparaturaufträge abgeschlossen sind.

Während dieser Zeit werden die Volumes weiterhin als **Warnung**angezeigt, was normal ist.

Wenn Sie z. b. das `Get-VirtualDisk` Cmdlet verwenden, wird möglicherweise die folgende Ausgabe angezeigt:
```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                InService         Warning      True           1 TB
MyVolume2    Mirror                InService         Warning      True           1 TB
MyVolume3    Mirror                InService         Warning      True           1 TB
```

Vergewissern Sie sich nach Abschluss der Aufträge, dass die Volumes mithilfe des Cmdlets **wieder Fehler** frei angezeigt werden `Get-VirtualDisk` . Hier ist eine Beispielausgabe angegeben:

```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                OK                Healthy      True           1 TB
MyVolume2    Mirror                OK                Healthy      True           1 TB
MyVolume3    Mirror                OK                Healthy      True           1 TB
```

Es ist nun sicher, andere Server im Cluster anzuhalten und neu zu starten.

## <a name="how-to-update-storage-spaces-direct-nodes-offline"></a>Vorgehensweise beim Offline Aktualisieren von direkte Speicherplätze Knoten
Führen Sie die folgenden Schritte aus, um das direkte Speicherplätze System schnell zu. Dazu gehört die Planung eines Wartungs Fensters und das herunter schalten des Systems zum Patchen. Wenn ein kritisches Sicherheitsupdate vorliegt, das Sie schnell anwenden müssen, oder wenn Sie sicherstellen müssen, dass das Patchen in Ihrem Wartungsfenster abgeschlossen ist, ist diese Methode möglicherweise für Sie vorgesehen. Durch diesen Vorgang wird der direkte Speicherplätze Cluster herunterskalieren, gepatcht und wieder zusammengeführt. Der Kompromiss ist die Ausfallzeit der gehosteten Ressourcen.

1. Planen Sie Ihr Wartungsfenster.
2. Schalten Sie die virtuellen Datenträger offline.
3. Beendet den Cluster, um den Speicherpool offline zu schalten. Führen Sie das Cmdlet " **stoppt** " aus, oder verwenden Sie Failovercluster-Manager, um den Cluster anzuhalten.
4. Legen Sie in "Services. msc" für jeden Knoten den Cluster Dienst auf " **deaktiviert** " fest. Dadurch wird verhindert, dass der Cluster Dienst beim Patchen gestartet wird.
5. Wenden Sie das kumulative Update für Windows Server und alle erforderlichen Wartungs Stapel Updates auf alle Knoten an. (Sie können alle Knoten gleichzeitig aktualisieren, da der Cluster nicht gewartet werden muss.)
6. Starten Sie die Knoten neu, und stellen Sie sicher, dass alles gut aussieht
7. Legen Sie den Cluster Dienst auf den einzelnen Knoten auf **automatisch** zurück.
8. Starten Sie den Cluster. Führen Sie das Cmdlet **Start-Cluster** aus, oder verwenden Sie Failovercluster-Manager.

   Warten Sie einige Minuten.  Stellen Sie sicher, dass der Speicherpool fehlerfrei ist.
9. Schalten Sie die virtuellen Datenträger wieder online.
10. Überwachen Sie den Status der virtuellen Datenträger, indem Sie die Cmdlets " **Get-Volume** " und " **Get-virtualdisk** " ausführen.


## <a name="additional-references"></a>Weitere Verweise

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
- [Cluster fähiges aktualisieren (Cau)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831694(v=ws.11))
