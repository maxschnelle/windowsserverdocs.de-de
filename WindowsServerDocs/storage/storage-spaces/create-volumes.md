---
ms.assetid: a9f229eb-bef4-4231-97d0-0899e17cef32
title: Erstellen von Volumes in Direkte Speicherplätze
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 01/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 277a676d8e53a7847d54039aab6607be8e5a78c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823611"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>Erstellen von Volumes in Direkte Speicherplätze

>Gilt für: Windows Server 2016

In diesem Thema wird beschrieben, wie Volumes in Direkte Speicherplätze mithilfe von PowerShell oder dem Failovercluster-Manager erstellt werden.

   >[!TIP]
   >  Lesen Sie zunächst [Planen von Volumes in Direkte Speicherplätze](plan-volumes.md), falls noch nicht geschehen.

## <a name="create-volumes-using-powershell"></a>Erstellen von Volumes mithilfe von PowerShell

Wir empfehlen die Verwendung des Cmdlets **New-Volume** zum Erstellen von Volumes für Direkte Speicherplätze. Es bietet die schnellste und einfachste Methode dafür. Dieses einzelne Cmdlet erstellt, partitioniert und formatiert automatisch den virtuellen Datenträger, erstellt das Volume mit demselben Namen und fügt es freigegebenen Clustervolumes hinzu – alles in einem einfachen Schritt.

Das Cmdlet **New-Volume** hat vier Parameter, die Sie immer angeben müssen:

- **FriendlyName:** Eine beliebige Zeichenfolge, die Sie, z. B. möchten *"Volume1"*
- **FileSystem:** Entweder **CSVFS_ReFS** (empfohlen) oder **CSVFS_NTFS**
- **StoragePoolFriendlyName:** Den Namen Ihres Speicherkontos pool, z. B. *"S2D auf ClusterName"*
- **Größe:** Die Größe des Volumes, z. B. *"10 TB"*

   >[!NOTE]
   >  Windows, einschließlich PowerShell, zählt mithilfe von binären Zahlen (Basis 2), während Laufwerke häufig mithilfe von Dezimalzahlen (Basis 10) bezeichnet werden. Dies erklärt, warum ein "Ein Terabyte"-Laufwerk, das als 1,000,000,000,000 Bytes definiert ist, in Windows mit etwa "909 GB" angezeigt wird. Dies ist das erwartungsgemäße Verhalten. Beim Erstellen von Volumes mithilfe von **New-Volume**, müssen Sie den Parameter **Größe** in binären (Basis 2) Zahlen angeben. Beispiel: Bei Angaben von "909 GB" oder "0,909495 TB" wird ein Volume von ungefähr 1,000,000,000,000 Bytes erstellt.

### <a name="example-with-2-or-3-servers"></a>Beispiel: Mit 2 oder 3-Servern

Wenn Ihre Bereitstellung nur zwei Server hat, verwendet Direkte Speicherplätze zur Vereinfachung automatisch die Zweiwegespiegelung, um Robustheit zu erzielen. Wenn Ihre Bereitstellung nur drei Server hat, wird automatisch die Dreiwegespiegelung verwendet.

```
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>Beispiel: Mit 4 +-Servern

Wenn Sie vier oder mehr Server haben, können Sie mithilfe des optionalen Parameters **ResiliencySettingName** den Resilienztyp auswählen.

-   **ResiliencySettingName:** Entweder **Spiegel** oder **Parität**.

Im folgenden Beispiel verwendet *"Volume2"* die Dreiwegespiegelung und *"Volume3"* die duale Parität (häufig als "Erasure Coding" bezeichnet).

```
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>Beispiel: Verwenden der Speicherebenen

In Bereitstellungen mit drei Arten von Laufwerken kann ein Volume SSD- und HDD-Ebenen umfassen und sich teilweise auf beiden befinden. Ebenso kann ein Volume in Bereitstellungen mit vier oder mehr Servern die Spiegelung und die duale Parität mischen und sich teilweise auf beiden befinden.

Damit Sie solche Volumes erstellen können, bietet Direkte Speicherplätze Standardebenenvorlagen namens *Leistung* und *Kapazität*. Darin sind Definitionen für die Dreiwegespiegelung auf den schnelleren Laufwerken (falls zutreffend) und die duale Parität auf den langsameren Laufwerken (sofern zutreffend) gekapselt.

Sie können diese anzeigen, indem Sie das Cmdlet **Get-StorageTier** ausführen.

```
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![PowerShell-Speicherebenen – Screenshot](media/creating-volumes/storage-tiers-screenshot.png)

Zum Erstellen von Volumes mit mehreren Ebenen verweisen Sie mithilfe der Parameter **StorageTierFriendlyNames** und **StorageTierSizes** des Cmdlets **New-Volume** auf diese Ebenenvorlagen. Beispiel: Das folgende Cmdlet erstellt ein Volume, das die Dreiwegespiegelung und duale Parität im Verhältnis 30:70 mischt.

```
New-Volume -FriendlyName "Volume4" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 300GB, 700GB
```

## <a name="create-volumes-using-failover-cluster-manager"></a>Erstellen von Volumes mithilfe des Failovercluster-Managers

Sie können Volumes auch mithilfe des *Assistenten für neue virtuelle Datenträger (Direkte Speicherplätze)* und anschließend dem *Assistenten für neue Volumes* aus dem Failovercluster-Manager erstellen. Dieser Workflow umfasst allerdings viel mehr manuelle Schritte und wird nicht empfohlen.

Es gibt drei grundlegende Schritte:

### <a name="step-1-create-virtual-disk"></a>Schritt 1: Erstellen des virtuellen Datenträgers

![Neuer virtueller Datenträger](media/creating-volumes/GUI-Step-1.png)

1. Navigieren Sie im Failovercluster-Manager zu **Speicher** -> **Pools**.
2. Wählen Sie im Aktionsbereich rechts **Neuer virtueller Datenträger** aus, oder klicken Sie mit der rechten Maustaste auf den Pool, und wählen Sie **Neuer virtueller Datenträger**.
3. Wählen Sie den Speicherpool aus, und klicken Sie auf **OK**. Der *Assistent für neue virtuelle Datenträger (Direkte Speicherplätze)* wird geöffnet.
4. Verwenden Sie den Assistenten, um den virtuellen Datenträger zu benennen und seine Größe anzugeben.
5. Überprüfen Sie Ihre Auswahl, und klicken Sie auf **Erstellen**.
6. Achten Sie darauf, das Kontrollkästchen **Volume erstellen, wenn dieser Assistent geschlossen wird** zu aktivieren.

### <a name="step-2-create-volume"></a>Schritt 2: Volume erstellen

Der *Assistent für neue Volumes* wird geöffnet.

7. Wählen Sie den virtuellen Datenträger aus, den Sie gerade erstellt haben, und klicken Sie auf **Weiter**.
8. Geben Sie die Größe des Volumes (Standard: die gleiche Größe wie der virtuelle Datenträger) an, und klicken Sie auf **Weiter**. 
9. Weisen Sie das Volume einem Laufwerkbuchstaben zu, oder wählen Sie **Keinem Laufwerkbuchstaben zuweisen**, und klicken Sie auf **Weiter**.
10. Geben Sie das zu verwendende Dateisystem an, behalten Sie als Größe der Zuordnungseinheit die Option *Standard* bei, benennen Sie das Volume, und klicken Sie auf **Weiter**.
11. Überprüfen Sie Ihre Auswahl, und klicken Sie auf **Erstellen**, dann auf **Schließen**.

### <a name="step-3-add-to-cluster-shared-volumes"></a>Schritt 3: Zu freigegebenen Clustervolumes hinzufügen

![„Zu freigegebenen Clustervolumes hinzufügen“](media/creating-volumes/GUI-Step-2.png)

12. Navigieren Sie im Failovercluster-Manager zu **Speicher** -> **Datenträger**.
13. Wählen Sie den virtuellen Datenträger aus, den Sie gerade erstellt haben, und wählen Sie im Aktionsbereich rechts **Zu freigegebenen Clustervolumes hinzufügen**, oder klicken Sie mit der rechten Maustaste auf den virtuellen Datenträger, und wählen Sie **Zu freigegebenen Clustervolumes hinzufügen**.

Fertig! Wiederholen Sie diese Schritte ggf., um mehrere Volumes zu erstellen.

## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)
- [Planen von Volumes im "direkte Speicherplätze"](plan-volumes.md)
