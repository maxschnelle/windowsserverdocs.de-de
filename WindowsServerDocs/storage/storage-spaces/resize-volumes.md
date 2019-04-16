---
title: Erweitern von Volumes in Direkte Speicherplätze
ms.assetid: fa48f8f7-44e7-4a0b-b32d-d127eff470f0
ms.prod: windows-server-threshold
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 01/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51f58ec23c55a6cb1664d800d6f4a75dae545899
ms.sourcegitcommit: dfd25348ea3587e09ea8c2224237a3e8078422ae
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2018
ms.locfileid: "4678649"
---
# Erweitern von Volumes in Direkte Speicherplätze
> Gilt für: WindowsServer 2019, WindowsServer 2016

Dieses Thema enthält Anweisungen zum Anpassen der Volumegröße in [Direkte Speicherplätze](storage-spaces-direct-overview.md).

## Voraussetzungen

### Kapazität im Speicherpool

Bevor Sie die Volumegröße ändern, stellen Sie sicher, dass der Speicherpool über ausreichend Kapazität für den neuen, größeren Speicherbedarf verfügt. Beispielsweise würden beim Ändern der Größe von einem Volume für die Drei-Wege-Spiegelung von 1 TB auf 2 TB der Speicherbedarf von 3 TB auf 6 TB wachsen. Damit die Größenänderung erfolgreich ausgeführt werden kann, benötigen Sie mindestens folgende verfügbare Kapazität im Speicherpool: (6 - 3) = 3 TB.

### Erfahrung mit Volumes in Speicherplätzen

In Direkte Speicherplätze besteht jedes Volume aus mehreren gestapelten Objekten: dem freigegebenen Clustervolume (CSV), bei dem es sich um ein Volume handelt; der Partition; dem Datenträger, der ein virtueller Datenträger ist; und mindestens einer Speicherebene (sofern zutreffend). Zum Ändern der Größe eines Volumes müssen Sie die Größe einiger dieser Objekte ändern.

![volumes-in-smapi](media/resize-volumes/volumes-in-smapi.png)

Um sich damit vertraut zu machen, führen Sie **Get-** mit dem entsprechenden Substantiv in PowerShell aus.

Beispiel:

```PowerShell
Get-VirtualDisk
```

Um die Zuordnungen zwischen Objekten im Stapel zu verfolgen, reichen Sie ein **Get-**-Cmdlet an das nächste weiter.

Hier sehen Sie z.B., wie Sie von einem virtuellen Datenträger bis zum Volume gelangen:

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-Disk | Get-Partition | Get-Volume 
```

## Schritt1 – Ändern der Größe des virtuellen Datenträgers

Der virtuelle Datenträger kann Speicherebenen verwenden oder nicht, je nachdem, wie sie erstellt wurde.

Führen Sie zum Überprüfen das folgende Cmdlet aus:

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier 
```

Wenn das Cmdlet nichts zurückgibt, verwendet der virtuelle Datenträger keine Speicherebenen.

### Keine Speicherebenen

Verfügt der virtuelle Datenträger über keine Speicherkategorien, können Sie seine Größe direkt über das **Resize-VirtualDisk**-Cmdlet anpassen.

Geben Sie die neue Größe im Parameter **-Size** an.

```PowerShell
Get-VirtualDisk <FriendlyName> | Resize-VirtualDisk -Size <Size>
```

Wenn Sie die Größe von **VirtualDisk** anpassen, folgt **Disk** automatisch und wird angepasst.

![Resize-VirtualDisk](media/resize-volumes/Resize-VirtualDisk.gif)

### Mit Speicherebenen

Wenn der virtuelle Datenträger Speicherebenen verwendet, können Sie die Größe jeder Ebene separat mit dem Cmdlet **Resize-StorageTier** anpassen.

Rufen Sie die Namen der Speicherebenen ab, indem Sie den Zuordnungen des virtuellen Datenträgers folgen.

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier | Select FriendlyName
```

Geben Sie dann für jede Ebene die neue Größe im Parameter **-Size** an.

```PowerShell
Get-StorageTier <FriendlyName> | Resize-StorageTier -Size <Size>
```

> [!TIP]
> Wenn es sich bei Ihren Ebenen um unterschiedliche physische Medientypen handelt (z.B. **MediaType = SSD** und **MediaType = HDD**), müssen Sie sicherstellen, dass Sie über ausreichend Kapazität für jeden Medientyp im Speicherpool für den neuen, größeren Speicherbedarf für jede Ebene verfügen.

Wenn Sie die Größe von **StorageTier**-Elementen ändern, folgen **VirtualDisk** und **Disk** automatisch und werden ebenfalls angepasst.

![Resize-StorageTier](media/resize-volumes/Resize-StorageTier.gif)

## Schritt2 – Ändern der Größe der Partition

Passen Sie als Nächstes die Größe der Partition mit dem Cmdlet **Resize-Partition** an. Vom virtuellen Datenträger wird erwartet, dass er zwei Partitionen besitzt: die erste ist reserviert und sollte nicht geändert werden. Für den Datenträger, dessen Größe geändert werden muss, gilt Folgendes **PartitionNumber = 2** und **Type = Basic**.

Geben Sie die neue Größe im Parameter **-Size** an. Wir empfehlen die maximale unterstützte Größe zu verwenden, wie unten dargestellt.

```PowerShell
# Choose virtual disk
$VirtualDisk = Get-VirtualDisk <FriendlyName>

# Get its partition
$Partition = $VirtualDisk | Get-Disk | Get-Partition | Where PartitionNumber -Eq 2

# Resize to its maximum supported size 
$Partition | Resize-Partition -Size ($Partition | Get-PartitionSupportedSize).SizeMax
```

Wenn Sie die Größe von **Partition** anpassen, folgen **Volume** und **ClusterSharedVolume** automatisch und werden ebenfalls angepasst.

![Resize-Partition](media/resize-volumes/Resize-Partition.gif)

Das war's.

> [!TIP]
> Sie können überprüfen, ob das Volume die neue Größe aufweist, indem Sie **Get-Volume** ausführen.

## Weitere Informationen:

- [Direkte Speicherplätze in Windows Server 2016](storage-spaces-direct-overview.md)
- [Planen von Volumes in Direkte Speicherplätze](plan-volumes.md)
- [Erstellen von Volumes in Direkte Speicherplätze](create-volumes.md)
