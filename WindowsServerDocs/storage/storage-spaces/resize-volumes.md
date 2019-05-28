---
title: Erweitern von Volumes in Direkte Speicherplätze
description: Informationen zum Ändern der Größe der Volumes in Storage Spaces Direct using Windows Admin Center und PowerShell.
ms.prod: windows-server-threshold
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 05/07/2019
ms.openlocfilehash: 3be6a4cda20f4d7d7d881ad8a272dc38fd787bba
ms.sourcegitcommit: 75f257d97d345da388cda972ccce0eb29e82d3bc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65613228"
---
# <a name="extending-volumes-in-storage-spaces-direct"></a>Erweitern von Volumes in Direkte Speicherplätze
> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält Anweisungen für die Größenänderung von Volumes auf einem ["direkte Speicherplätze"](storage-spaces-direct-overview.md) -Clusters mit Windows Admin Center.

Sehen Sie sich ein kurzes Video zum Ändern der Größe eines Volumes.

> [!VIDEO https://www.youtube-nocookie.com/embed/hqyBzipBoTI]

## <a name="extending-volumes-using-windows-admin-center"></a>Erweitern von Volumes, die mithilfe von Windows Admin Center

1. Windows Admin Center, eine Verbindung mit einem "direkte Speicherplätze"-Cluster herstellen, und wählen Sie dann **Volumes** aus der **Tools** Bereich.
2. Wählen Sie auf der Seite Volumes die **Inventur** Registerkarte, und wählen Sie das Volume, das Sie anpassen möchten.

    Auf der Detailseite des Volumes wird die Speicherkapazität für das Volume angegeben. Sie können die Detailseite des Volumes auch direkt über das Dashboard öffnen. Klicken Sie auf dem Dashboard, klicken Sie im Bereich "Warnungen" Wählen Sie die Warnung, die Sie benachrichtigt, wenn ein Volume Speicherkapazität knapp wird, und wählen Sie dann **wechseln Sie zum Volume**.

4. Wählen Sie am oberen Rand der Volumes, **Größe**.
5. Geben Sie einen neuen Größe größeren werden soll, und wählen Sie dann **Größe**.

    Klicken Sie auf der Detailseite des Volumes die größere Speicherkapazität für das Volume wird angegeben, und die Warnung auf dem Dashboard wird gelöscht.

## <a name="extending-volumes-using-powershell"></a>Erweitern von Volumes, die mithilfe von PowerShell

### <a name="capacity-in-the-storage-pool"></a>Kapazität im Speicherpool

Bevor Sie die Volumegröße ändern, stellen Sie sicher, dass der Speicherpool über ausreichend Kapazität für den neuen, größeren Speicherbedarf verfügt. Beispielsweise würden beim Ändern der Größe von einem Volume für die Drei-Wege-Spiegelung von 1 TB auf 2 TB der Speicherbedarf von 3 TB auf 6 TB wachsen. Damit die Größenänderung erfolgreich ausgeführt werden kann, benötigen Sie mindestens folgende verfügbare Kapazität im Speicherpool: (6 - 3) = 3 TB.

### <a name="familiarity-with-volumes-in-storage-spaces"></a>Erfahrung mit Volumes in Speicherplätzen

In Direkte Speicherplätze besteht jedes Volume aus mehreren gestapelten Objekten: dem freigegebenen Clustervolume (CSV), bei dem es sich um ein Volume handelt; der Partition; dem Datenträger, der ein virtueller Datenträger ist; und mindestens einer Speicherebene (sofern zutreffend). Zum Ändern der Größe eines Volumes müssen Sie die Größe einiger dieser Objekte ändern.

![volumes-in-smapi](media/resize-volumes/volumes-in-smapi.png)

Um sich damit vertraut zu machen, führen Sie **Get-** mit dem entsprechenden Substantiv in PowerShell aus.

Zum Beispiel:

```PowerShell
Get-VirtualDisk
```

Um die Zuordnungen zwischen Objekten im Stapel zu verfolgen, reichen Sie ein **Get-** -Cmdlet an das nächste weiter.

Hier sehen Sie z. B., wie Sie von einem virtuellen Datenträger bis zum Volume gelangen:

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-Disk | Get-Partition | Get-Volume 
```

### <a name="step-1--resize-the-virtual-disk"></a>Schritt 1 – Ändern der Größe des virtuellen Datenträgers

Der virtuelle Datenträger kann Speicherebenen verwenden oder nicht, je nachdem, wie sie erstellt wurde.

Führen Sie zum Überprüfen das folgende Cmdlet aus:

```PowerShell
Get-VirtualDisk <FriendlyName> | Get-StorageTier 
```

Wenn das Cmdlet nichts zurückgibt, verwendet der virtuelle Datenträger keine Speicherebenen.

#### <a name="no-storage-tiers"></a>Keine Speicherebenen

Verfügt der virtuelle Datenträger über keine Speicherkategorien, können Sie seine Größe direkt über das **Resize-VirtualDisk**-Cmdlet anpassen.

Geben Sie die neue Größe im Parameter **-Size** an.

```PowerShell
Get-VirtualDisk <FriendlyName> | Resize-VirtualDisk -Size <Size>
```

Wenn Sie die Größe von **VirtualDisk** anpassen, folgt **Disk** automatisch und wird angepasst.

![Resize-VirtualDisk](media/resize-volumes/Resize-VirtualDisk.gif)

#### <a name="with-storage-tiers"></a>Mit Speicherebenen

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
> Wenn es sich bei Ihren Ebenen um unterschiedliche physische Medientypen handelt (z. B. **MediaType = SSD** und **MediaType = HDD**), müssen Sie sicherstellen, dass Sie über ausreichend Kapazität für jeden Medientyp im Speicherpool für den neuen, größeren Speicherbedarf für jede Ebene verfügen.

Wenn Sie die Größe von **StorageTier**-Elementen ändern, folgen **VirtualDisk** und **Disk** automatisch und werden ebenfalls angepasst.

![Resize-StorageTier](media/resize-volumes/Resize-StorageTier.gif)

### <a name="step-2--resize-the-partition"></a>Schritt 2 – Ändern der Größe der Partition

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

Das ist alles!

> [!TIP]
> Sie können überprüfen, ob das Volume die neue Größe aufweist, indem Sie **Get-Volume** ausführen.

## <a name="see-also"></a>Siehe auch

- ["Direkte Speicherplätze" unter WindowsServer 2016](storage-spaces-direct-overview.md)
- [Planen von Volumes im "direkte Speicherplätze"](plan-volumes.md)
- [Erstellen von Volumes in "direkte Speicherplätze"](create-volumes.md)
- [Löschen von Volumes in "direkte Speicherplätze"](delete-volumes.md)
