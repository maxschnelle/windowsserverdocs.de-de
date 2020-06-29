---
title: Erweitern von Volumes in direkte Speicherplätze
description: Ändern der Größe von Volumes in direkte Speicherplätze mithilfe von Windows Admin Center und PowerShell.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 03/10/2020
ms.openlocfilehash: 4526bdc87bfbb8cdaf6cc3b0e8f3cd1cd80f4a9d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474607"
---
# <a name="extending-volumes-in-storage-spaces-direct"></a>Erweitern von Volumes in direkte Speicherplätze
> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält Anweisungen zum Ändern der Größe von Volumes in einem [direkte Speicherplätze](storage-spaces-direct-overview.md) Cluster mithilfe des Windows Admin Centers.

> [!WARNING]
> **Nicht unterstützt: Ändern der Größe des zugrunde liegenden Speichers, der von direkte Speicherplätze verwendet wird.** Wenn Sie direkte Speicherplätze in einer virtualisierten Speicherumgebung ausführen, einschließlich in Azure, wird das Ändern der Größe oder Änderung der Merkmale der Speichergeräte, die von den virtuellen Computern verwendet werden, nicht unterstützt und führt dazu, dass die Daten nicht mehr verfügbar sind. Befolgen Sie stattdessen die Anweisungen im Abschnitt [Hinzufügen von Servern oder Laufwerken](add-nodes.md) , um vor dem Erweitern von Volumes zusätzliche Kapazität hinzuzufügen.

Sehen Sie sich ein kurzes Video zum Ändern der Größe eines Volumes an.

> [!VIDEO https://www.youtube-nocookie.com/embed/hqyBzipBoTI]

## <a name="extending-volumes-using-windows-admin-center"></a>Erweitern von Volumes mithilfe des Windows Admin Centers

1. Stellen Sie im Windows Admin Center eine Verbindung mit einem direkte Speicherplätze Cluster her, und wählen Sie dann im Bereich **Tools** die Option **Volumes** aus.
2. Wählen Sie auf der Seite Volumes die Registerkarte **Inventar** aus, und wählen Sie dann das Volume aus, das Sie ändern möchten.

    Auf der Seite Volumedetails wird die Speicherkapazität für das Volume angegeben. Sie können die Seite "Volumedetails" auch direkt über das Dashboard öffnen. Wählen Sie auf dem Dashboard im Bereich Warnungen die Warnung aus, die Sie benachrichtigt, wenn die Speicherkapazität eines Volumes geringer ist, und wählen Sie dann **zu Volume**wechseln aus.

4. Wählen Sie oben auf der Seite Volumedetails die Option **Größe ändern**aus.
5. Geben Sie eine neue größere Größe ein, und wählen Sie dann Größe **ändern**aus.

    Auf der Seite Volumedetails wird die größere Speicherkapazität für das Volume angezeigt, und die Warnung wird auf dem Dashboard gelöscht.

## <a name="extending-volumes-using-powershell"></a>Erweitern von Volumes mithilfe von PowerShell

### <a name="capacity-in-the-storage-pool"></a>Kapazität im Speicherpool

Bevor Sie die Größe eines Volumes ändern, stellen Sie sicher, dass genügend Kapazität im Speicherpool vorhanden ist, um den neuen, größeren Ressourcenbedarf zu erfüllen. Wenn Sie z. b. die Größe eines drei-Wege-Spiegelungs Volumens von 1 TB auf 2 TB ändern, wächst der Speicherbedarf zwischen 3 und 6 TB. Damit die Größenänderung erfolgreich ist, benötigen Sie mindestens (6-3) = 3 TB verfügbare Kapazität im Speicherpool.

### <a name="familiarity-with-volumes-in-storage-spaces"></a>Vertrautheit mit Volumes in Speicherplätzen

In direkte Speicherplätze besteht jedes Volume aus mehreren gestapelten Objekten: dem freigegebenen Cluster Volume (CSV), das ein Volume ist. die Partition. der Datenträger, bei dem es sich um eine virtuelle Festplatte handelt und eine oder mehrere Speicherebenen (falls zutreffend). Um die Größe eines Volumes zu ändern, müssen Sie die Größe mehrerer dieser Objekte ändern.

![Volumes in-smapi](media/resize-volumes/volumes-in-smapi.png)

Um sich mit Ihnen vertraut zu machen, führen Sie **Get-** mit dem entsprechenden Substantiv in PowerShell aus.

Beispiel:

```PowerShell
Get-VirtualDisk
```

Um Zuordnungen zwischen Objekten im Stapel zu verfolgen, übergeben Sie ein **Get-** Cmdlet an das nächste.

So können Sie beispielsweise von einem virtuellen Datenträger auf das zugehörige Volume gelangen:

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-Disk | Get-Partition | Get-Volume
```

### <a name="step-1--resize-the-virtual-disk"></a>Schritt 1 – Ändern der Größe des virtuellen Datenträgers

Der virtuelle Datenträger verwendet abhängig von der Art der Erstellung möglicherweise Speicherebenen oder nicht.

Um dies zu überprüfen, führen Sie das folgende Cmdlet aus:

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier
```

Wenn das Cmdlet "Nothing" zurückgibt, verwendet der virtuelle Datenträger keine Speicherebenen.

#### <a name="no-storage-tiers"></a>Keine Speicherebenen

Wenn die virtuelle Festplatte keine Speicherebenen hat, können Sie die Größe direkt mithilfe des Cmdlets **Größe-virtualdisk** ändern.

Geben Sie die neue Größe im **-size-** Parameter an.

```PowerShell
Get-VirtualDisk <FriendlyName> | Resize-VirtualDisk -Size <Size>
```

Wenn **Sie die Größe** des virtuellen Datenträgers **ändern, wird der Daten**Träger automatisch befolgt, und die Größe wird ebenfalls geändert.

![Resize-virtualdisk](media/resize-volumes/Resize-VirtualDisk.gif)

#### <a name="with-storage-tiers"></a>Mit Speicherebenen

Wenn die virtuelle Festplatte Speicherebenen verwendet, können Sie die Größe jeder Ebene separat mithilfe des Cmdlets **Größe-storagetier** ändern.

Sie erhalten die Namen der Speicherebenen, indem Sie die Zuordnungen vom virtuellen Datenträger befolgen.

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier | Select FriendlyName
```

Geben Sie dann für jede Ebene die neue Größe im **-size-** Parameter an.

```PowerShell
Get-StorageTier <FriendlyName> | Resize-StorageTier -Size <Size>
```

> [!TIP]
> Wenn es sich bei den Ebenen um verschiedene physische Medientypen handelt (z. b. **mediaType = SSD** und **mediaType = HDD**), müssen Sie sicherstellen, dass Sie über genügend Kapazität für jeden Medientyp im Speicherpool verfügen, um den neuen, größeren Ressourcenbedarf der einzelnen Ebenen zu erfüllen.

Wenn Sie die Größe der **storagetier**(s) ändern, werden **virtualdisk** und **Disk** automatisch befolgt, und die Größe wird ebenfalls geändert.

![Resize-StorageTier](media/resize-volumes/Resize-StorageTier.gif)

### <a name="step-2--resize-the-partition"></a>Schritt 2 – Ändern der Größe der Partition

Ändern Sie als nächstes die Größe der Partition mithilfe des Cmdlets **Größe-Partition** . Der virtuelle Datenträger erwartet zwei Partitionen: der erste ist reserviert und sollte nicht geändert werden. der Wert, den Sie für die Größenänderung benötigen, ist **PARTITIONNUMBER = 2** und **Type = Basic**.

Geben Sie die neue Größe im **-size-** Parameter an. Es wird empfohlen, wie unten dargestellt die maximal unterstützte Größe zu verwenden.

```PowerShell
# Choose virtual disk
$VirtualDisk = Get-VirtualDisk <FriendlyName>

# Get its partition
$Partition = $VirtualDisk | Get-Disk | Get-Partition | Where PartitionNumber -Eq 2

# Resize to its maximum supported size
$Partition | Resize-Partition -Size ($Partition | Get-PartitionSupportedSize).SizeMax
```

Wenn Sie die Größe der **Partition**ändern, werden das **Volume** und das **clustersharedvolume** automatisch befolgt, und die Größe wird ebenfalls geändert.

![Resize-Partition](media/resize-volumes/Resize-Partition.gif)

Das ist alles!

> [!TIP]
> Sie können überprüfen, ob das Volume über die neue Größe verfügt, indem Sie **Get-Volume**ausführen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Direkte Speicherplätze in Windows Server 2016](storage-spaces-direct-overview.md)
- [Planen von Volumes in direkte Speicherplätze](plan-volumes.md)
- [Erstellen von Volumes in direkte Speicherplätze](create-volumes.md)
- [Löschen von Volumes in direkte Speicherplätze](delete-volumes.md)
