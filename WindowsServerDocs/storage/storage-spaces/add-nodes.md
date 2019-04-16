---
ms.assetid: 898d72f1-01e7-4b87-8eb3-a8e0e2e6e6da
title: Hinzufügen von Servern oder Laufwerken zu „direkten Speicherplätzen“
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 11/06/2017
description: Das Hinzufügen von Servern oder Laufwerken zu einem "direkte Speicherplätze"-cluster
ms.localizationpriority: medium
ms.openlocfilehash: ae639b920788911dbc16952d7b61aab85b0a391b
ms.sourcegitcommit: dfd25348ea3587e09ea8c2224237a3e8078422ae
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2018
ms.locfileid: "4678599"
---
# Hinzufügen von Servern oder Laufwerken zu Direkte Speicherplätze.

>Gilt für: WindowsServer 2019, WindowsServer 2016

In diesem Thema wird beschrieben, wie Sie Server oder Laufwerke zu Direkte Speicherplätze hinzufügen.

## <a name="adding-servers"></a> Hinzufügen von Servern

Das Hinzufügen von Servern wird häufig auch als Skalierung bezeichnet. Es fügt Speicherkapazität hinzu, kann die Speicherleistung verbessern und erhöht die Speichereffizienz. Bei einer hyperkonvergenten Bereitstellung werden durch Hinzufügen von Servern zudem mehr Computing-Ressourcen für Ihren Workload bereitgestellt.

![Animation für das Hinzufügen von einem Server auf einem Cluster mit vier Knoten](media/add-nodes/Scaling-Out.gif)

Typische Bereitstellungen lassen sich durch Hinzufügen von Servern ganz einfach horizontal skalieren. Dies erfordert nur zwei Schritte:

1. Führen Sie den [Clusterüberprüfungs-Assistenten](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx) mithilfe des Failovercluster-Snap-Ins oder mit dem **Test-Cluster**-Cmdlet in PowerShell aus (als Administrator). Beziehen Sie den neuen Server *\<NewNode>*, den Sie hinzufügen möchten, darin ein.

   ```PowerShell
   Test-Cluster -Node <Node>, <Node>, <Node>, <NewNode> -Include "Storage Spaces Direct", Inventory, Network, "System Configuration"
   ```

   Dadurch wird sichergestellt, dass auf dem neuen Server Windows Server 2016 Datacenter Edition ausgeführt wird, dass der Knoten derselben Active Directory-Domänendienste-Domäne wie die vorhandenen Server angehört, dass er über alle erforderlichen Rollen und Features verfügt und dass das Netzwerk ordnungsgemäß konfiguriert wurde.

   >[!IMPORTANT]
   > Wenn Sie erneut Laufwerke verwenden, die alten Daten oder Metadaten enthalten, die Sie nicht mehr benötigen, löschen Sie diese mithilfe der **Datenträgerverwaltung** oder mit dem **Reset-PhysicalDisk** -Cmdlet. Wenn alte Daten oder Metadaten festgestellt werden, werden die Laufwerke nicht zusammengefasst.

2. Führen Sie das folgende -Cmdlet auf dem Cluster aus, um das Hinzufügen des Servers abzuschließen:

```
Add-ClusterNode -Name NewNode 
```

   >[!NOTE]
   > Das automatische Pooling hängt davon ab, dass Sie über nur einen Pool verfügen. Wenn Sie die Standardkonfiguration zum Erstellen von mehreren Pools umgangen haben, müssen Sie neue Laufwerke selbst mit **Add-PhysicalDisk** zum bevorzugten Pool hinzufügen.

### 2 bis 3-Server: Drei-Wege-Spiegelung entsperren

![Hinzufügen von einem dritten Server zu einem Cluster mit zwei Knoten](media/add-nodes/Scaling-2-to-3.png)

Mit zwei Servern können Sie nur Volumes mit Zwei-Wege-Spiegelung erstellen (vgl. verteiltes RAID-1). Mit drei Servern können Sie Volumes mit Drei-Wege-Spiegelungen für eine bessere Fehlertoleranz erstellen. Es wird empfohlen, wenn möglich, immer die Drei-Wege-Spiegelung zu verwenden.

Volumes mit Zwei-Wege-Spiegelungen können nicht direkt auf Volumes mit Drei-Wege-Spiegelungen aktualisiert werden. Erstellen Sie stattdessen ein neues Volume und migrieren Sie (kopieren Sie, z.B. mithilfe von [Speicher Replikat](../storage-replica/server-to-server-storage-replication.md)) Ihre Daten. Entfernen Sie anschließend das alte Volume.

Als Einstieg in die Erstellung von Volumes mit Drei-Wege-Spiegelung stehen Ihnen mehrere gute Optionen zur Verfügung: Verwenden Sie die von Ihnen gewünschte Option. 

#### Option1

Legen Sie für jedes neue Volume bei der Erstellung **PhysicalDiskRedundancy = 2** fest.

```PowerShell
New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -PhysicalDiskRedundancy 2
```

#### Option2

Sie können stattdessen das **PhysicalDiskRedundancyDefault = 2**-Objekt des Pools unter den **ResiliencySetting** mit dem Namen **Spiegelung** festlegen. Neue gespiegelte Volumes verwenden dann automatisch die *Drei-Wege-* Spiegelung, auch wenn dies nicht angegeben wird.

```PowerShell
Get-StoragePool S2D* | Get-ResiliencySetting -Name Mirror | Set-ResiliencySetting -PhysicalDiskRedundancyDefault 2

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size>
```

#### Option3

Legen Sie **PhysicalDiskRedundancy = 2** für die **StorageTier **-Vorlage namens *Capacity* fest und erstellen Sie dann Volumes durch Verweisen auf die Ebene.

```PowerShell
Set-StorageTier -FriendlyName Capacity -PhysicalDiskRedundancy 2 

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Capacity -StorageTierSizes <Size>
```

### 3 bis 4 Server: duale Parität entsperren

![Hinzufügen eines vierten Servers zu einem Cluster mit drei Knoten](media/add-nodes/Scaling-3-to-4.png)

Bei vier Servern können Sie „duale“ Parität verwenden, oft auch als „Erasure Coding“ bezeichnet (vgl. verteiltes RAID-6). Dies bietet die gleiche Fehlertoleranz wie die Drei-Wege-Spiegelung, allerdings mit einer verbesserten Speichereffizienz. Weitere Informationen hierzu finden Sie unter [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md).

Wenn Sie eine kleinere Bereitstellung haben, existieren mehrere gute Optionen zum Erstellen von dualen Paritätsvolumes. Verwenden Sie die von Ihnen gewünschte Option.

#### Option1

Geben Sie für jedes neue Volume bei der Erstellung **PhysicalDiskRedundancy = 2** und **ResiliencySettingName = Parität** ein.

```PowerShell
New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity
```

#### Option2

Legen Sie das **PhysicalDiskRedundancy = 2**-Objekt des Pools unter **ResiliencySetting** mit dem Namen **Parität** fest. Jedes neue Paritätsvolume wird dann automatisch *duale* Parität verwenden, auch wenn Sie dies nicht angegeben

```PowerShell
Get-StoragePool S2D* | Get-ResiliencySetting -Name Parity | Set-ResiliencySetting -PhysicalDiskRedundancyDefault 2

New-Volume -FriendlyName <Name> -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size <Size> -ResiliencySettingName Parity
```

Ab vier Servern können Sie auch eine durch Spiegelung beschleunigte Parität verwenden, bei der ein einzelnes Volume zum Teil Spiegelung zum Teil Parität darstellt.

Hierzu müssen Sie Ihre **StorageTier**-Vorlage so aktualisieren, dass sie die beiden Ebenen *Performance* und *Capacity* in der Form enthalten, als ob sie erstellt worden wären, indem auf vier Servern zuerst **Enable-ClusterS2D** ausgeführt worden wäre. Insbesondere müssen beide Ebenen den **MediaType** Ihrer Kapazitätsgeräte (z. B. SSD oder HDD) und **PhysicalDiskRedundancy = 2** aufweisen. Die *Performance*-Ebene sollte **ResiliencySettingName = Mirror**, und die *Capacity*-Ebene sollte **ResiliencySettingName = Parity** sein.

#### Option3

Möglicherweise finden Sie es am einfachsten, nur die vorhandene Vorlage zu entfernen und zwei neue zu erstellen. Dies hat keinen Einfluss auf bereits vorhandene Volumes, die anhand der Ebenenvorlage erstellt wurden: Es handelt sich hierbei nur um eine Vorlage.

```PowerShell
Remove-StorageTier -FriendlyName Capacity

New-StorageTier -StoragePoolFriendlyName S2D* -MediaType HDD -PhysicalDiskRedundancy 2 -ResiliencySettingName Mirror -FriendlyName Performance
New-StorageTier -StoragePoolFriendlyName S2D* -MediaType HDD -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity -FriendlyName Capacity
```

Das war's. Sie können nun mithilfe dieser Ebenenvorlage Volumes mit einer durch Spiegelung beschleunigten Parität erstellen.

#### Beispiel

```PowerShell
New-Volume -FriendlyName "Sir-Mix-A-Lot" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes <Size, Size> 
```

### Bei über 4 Servern: größere Paritätseffizienz

Wenn Sie eine Skalierung auf mehr als vier Servern vornehmen, können neue Volumes von immer größerer Effizienz bei der Paritätscodierung profitieren. Beispielsweise verbessert sich die Effizienz zwischen sechs und sieben Servern durch die Möglichkeit der Verwendung von Reed-Solomon 4+2 (statt 2+2) von 50,0% auf 66,7%. Sie brauchen keine Schritte auszuführen, um in den Genuss dieser neuen Effizienz zu kommen. Die optimale Codierung wird jedes Mal, wenn Sie ein Volume erstellen, automatisch bestimmt.

Allerdings werden bereits vorhandene Volumes *nicht* in die neue bessere Codierung konvertiert. Ein guter Grund ist, dass dazu eine massive Berechnung erforderlich wäre, die buchstäblich *jedes einzelne Bit* in der gesamten Bereitstellung betrifft. Wenn bereits vorhandene Daten für höhere Effizienz neu codiert werden sollen, können Sie diese auf neue Volumes migrieren.

Weitere Informationen finden Sie unter [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md).

### Hinzufügen von Servern bei Verwendung von Gehäuse- oder Rackfehlertoleranz

Wenn Ihre Bereitstellung Gehäuse- oder Rackfehlertoleranz verwendet, müssen Sie Gehäuse oder Rack neuer Server angeben, bevor Sie sie zum Cluster hinzufügen. Dadurch kann der „direkte Speicherplatz“ bestimmen, wie die Daten am besten verteilt werden sollen, um die Fehlertoleranz zu maximieren.

1. Erstellen Sie eine temporäre Fehlerdomäne für den Knoten, indem Sie eine PowerShell-Sitzung mit erhöhten Rechten öffnen und dann den folgenden Befehl eingeben, wobei *\<NewNode>* der Name des neuen Clusterknotens ist:

   ```PowerShell
   New-ClusterFaultDomain -Type Node -Name <NewNode> 
   ```

2. Verschieben Sie diese temporäre Fehlerdomäne auf das Gehäuse oder Rack, in dem sich der neue Server physisch befindet, wie durch *\<ParentName>* festgelegt:

   ```PowerShell
   Set-ClusterFaultDomain -Name <NewNode> -Parent <ParentName> 
   ```

   Weitere Informationen finden Sie unter [Fehlerdomänenunterstützung in Windows Server 2016](../../failover-clustering/fault-domains.md).

3. Fügen Sie den Server zum Cluster hinzu, wie unter [Hinzufügen von Servern](#adding-servers) beschrieben. Wenn der neue Server dem Cluster hinzugefügt wird, wird er automatisch der Platzhalterfehlerdomäne (anhand des Namens) zugeordnet.

## <a name="adding-drives"></a> Hinzufügen von Laufwerken

Hinzufügen von Laufwerken (auch als zentrales Hochskalieren bezeichnet) fügt Speicherkapazität hinzu und kann die Leistung verbessern. Wenn Sie über freie Steckplätze verfügen, können Sie jedem Server Laufwerke hinzufügen, um die Speicherkapazität zu erweitern, ohne Server hinzuzufügen. Sie können unabhängig voneinander jederzeit Cache- oder Kapazitätslaufwerke hinzufügen.

   >[!IMPORTANT]
   > Es wird dringend empfohlen, alle Server mit identischen Speicherkonfigurationen zu konfigurieren.

![Animation zur Hinzufügen von Laufwerken auf ein System](media/add-nodes/Scale-Up.gif)

Zum zentralen Hochskalieren verbinden Sie die Laufwerke, und stellen Sie sicher, dass Windows sie erkennt. Sie sollten in der Ausgabe des **Get-PhysicalDisk** PowerShell-Cmdlets angezeigt werden, dessen **CanPool**-Eigenschaft auf **True** festgelegt ist. Wenn diese als **CanPool = False** angezeigt wird, überprüfen Sie den Grund durch Aktivieren der **CannotPoolReason**-Eigenschaft.

```PowerShell
Get-PhysicalDisk | Select SerialNumber, CanPool, CannotPoolReason
```

Innerhalb kurzer Zeit werden geeignete Laufwerke automatisch von Direkte Speicherplätze beansprucht, dem Speicherpool hinzugefügt, und die Volumes werden automatisch [gleichmäßig auf alle Laufwerke verteilt.](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/). Zu diesem Zeitpunkt sind Sie fertig und bereit zum [Erweitern der Volumes](resize-volumes.md) oder zum  [Erstellen neuer Volumes](create-volumes.md).

Wenn die Laufwerke nicht angezeigt werden, suchen Sie manuell nach Hardwareänderungen. Dazu können Sie den **Geräte-Manager** im Menü **Aktion** verwenden. Wenn sie alte Daten oder Metadaten enthalten, sollten Sie sie ggf. neu formatieren. Dies kann unter Verwendung der **Datenträgerverwaltung** oder mithilfe des **Reset-PhysicalDisk**- Cmdlets durchgeführt werden.

   >[!NOTE]
   > Das automatische Pooling hängt davon ab, dass Sie über nur einen Pool verfügen. Wenn Sie die Standardkonfiguration zum Erstellen von mehreren Pools umgangen haben, müssen Sie neue Laufwerke selbst mit **Add-PhysicalDisk** zum bevorzugten Pool hinzufügen.

## Optimieren der Nutzung von Laufwerken nach dem Hinzufügen von Laufwerken oder Servern

Im Laufe der Zeit Wenn Laufwerke hinzugefügt oder entfernt werden, kann die Verteilung von Daten zwischen den Laufwerken im Pool werden ungleichmäßig. In einigen Fällen kann dies dazu führen bestimmte Laufwerke voll sind, während die anderen Laufwerken im Pool einen viel niedrigeren Speicherverbrauch aufweisen.

Um Laufwerk Zuweisung sogar innerhalb des Pools zu schützen, optimiert "direkte Speicherplätze" automatisch Nutzung von Laufwerken nachdem Laufwerke oder Server an den Pool hinzugefügt (Dies ist ein manueller Vorgang für "Speicherplätze"-Systeme, die mit freigegebenen SAS-Gehäusen verwendet). Optimierung startet 15 Minuten nach dem Sie ein neues Laufwerk an den Pool hinzufügen. Pool Optimierung wird als ein Vorgang niedriger Priorität im Hintergrund ausgeführt, sodass Stunden oder Tage abgeschlossen ist, es dauern kann, insbesondere dann, wenn Sie große Festplatten verwenden.

Optimierung verwendet zwei Aufträge – einen namens *Optimieren* und eine namens *neu zu verteilen* -, und Sie können ihren Fortschritt mit dem folgenden Befehl überwachen:

```powershell
Get-StorageJob
```

Sie können einen Speicherpool mit dem Cmdlet [Optimize-StoragePool](https://docs.microsoft.com/powershell/module/storage/optimize-storagepool?view=win10-ps) manuell optimieren. Beispiel:

```powershell
Get-StoragePool <PoolName> | Optimize-StoragePool
```
