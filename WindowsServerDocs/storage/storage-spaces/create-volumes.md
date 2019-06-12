---
title: Erstellen von Volumes in Direkte Speicherplätze
description: 'Vorgehensweise: Erstellen von Volumes in Storage Spaces Direct using Windows Admin Center und PowerShell.'
ms.prod: windows-server-threshold
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 06/06/2019
ms.openlocfilehash: 85eca06a5d8c103851596055099876cb53a902ad
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810557"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>Erstellen von Volumes in Direkte Speicherplätze

> Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema wird beschrieben, wie zum Erstellen von Volumes auf einem Cluster "direkte Speicherplätze" mithilfe des Failovercluster-Manager, PowerShell oder Windows Admin Center wird.

> [!TIP]
> Lesen Sie zunächst [Planen von Volumes in Direkte Speicherplätze](plan-volumes.md), falls noch nicht geschehen.

## <a name="create-a-three-way-mirror-volume"></a>Erstellen Sie ein Volume für die drei-Wege-Spiegelung

So erstellen ein Volume für die drei-Wege-Spiegelung in Windows Admin Center: 

1. Windows Admin Center, eine Verbindung mit einem "direkte Speicherplätze"-Cluster herstellen, und wählen Sie dann **Volumes** aus der **Tools** Bereich.
2. Wählen Sie auf der Seite "Volumes" die **Inventur** Registerkarte, und wählen Sie dann **erstellen Volumes**.
3. In der **erstellen Volumes** , geben Sie einen Namen für das Volume, und lassen Sie **Resilienz** als **drei-Wege-Spiegelung**.
4. In **Größe auf**, geben Sie die Größe des Volumes. Beispiel: 5 TB (Terabyte).
5. Wählen Sie **Erstellen** aus.

Je nach Größe kann das Erstellen des Volumes einige Minuten dauern. Benachrichtigungen in der oberen rechten Ecke teilt Ihnen mit, wenn das Volume erstellt wird. Das neue Volume wird in der Inventarliste angezeigt.

Sehen Sie sich ein kurzes Video zum Erstellen eines Volumes drei-Wege-Spiegelung.

> [!VIDEO https://www.youtube-nocookie.com/embed/o66etKq70N8]

## <a name="create-a-mirror-accelerated-parity-volume"></a>Erstellen Sie ein Volume Parität Mirror-Beschleunigung

Mirror-beschleunigte Parität reduziert den Platzbedarf des Datenträgers auf die HDD. Beispielsweise wäre ein drei-Wege-Spiegelung-Volume, dass der Größe 10 Terabyte, Sie 30 Terabyte als Speicherbedarf benötigen. Um den Aufwand beim Speicherbedarf zu reduzieren, erstellen Sie ein Volume mit Parität Mirror-Beschleunigung. Dies verringert sich der Speicherplatzbedarf von 30 TB nur 22 Terabyte fassen, sogar in nur 4 Server, indem Sie spiegeln die aktivsten 20 Prozent der Daten und Parität für mehr Speicherplatz effizient zum Speichern des Rests ist. Sie können anpassen, dass dieses Verhältnis von Parität und Spiegelung aus, um die Leistung und Kapazität Kompromiss zu machen, die für Ihre Workload geeignet ist. Beispielsweise Parität und 10 Prozent Spiegel von 90 Prozent weniger Leistung ergibt jedoch den Fußabdruck weiter optimiert.

Erstellen eines Volumes mit Spiegelung beschleunigte Parität in Windows Admin Center:

1. Windows Admin Center, eine Verbindung mit einem "direkte Speicherplätze"-Cluster herstellen, und wählen Sie dann **Volumes** aus der **Tools** Bereich.
2. Wählen Sie auf der Seite "Volumes" die **Inventur** Registerkarte, und wählen Sie dann **erstellen Volumes**.
3. In der **erstellen Volumes** Bereich, geben Sie einen Namen für das Volume.
4. In **Resilienz**Option **Mirror-beschleunigte Parität**.
5. In **Parität Prozentsatz**, wählen Sie den Prozentsatz der Parität.
6. Wählen Sie **Erstellen** aus.

Sehen Sie sich ein kurzes Video zum Erstellen eines Volumes Mirror-beschleunigte Parität.

> [!VIDEO https://www.youtube-nocookie.com/embed/R72QHudqWpE]

## <a name="open-volume-and-add-files"></a>Öffnen Sie die Datei und Hinzufügen von Dateien

So öffnen Sie ein Volume aus, und fügen Dateien auf dem Volume in Windows Admin Center:

1. Windows Admin Center, eine Verbindung mit einem "direkte Speicherplätze"-Cluster herstellen, und wählen Sie dann **Volumes** aus der **Tools** Bereich.
2. Wählen Sie auf der Seite Volumes die **Inventur** Registerkarte.
2. Wählen Sie in der Liste der Volumes den Namen des Datenträgers, den Sie öffnen möchten.

    Auf der Detailseite des Volumes sehen Sie den Pfad auf dem Volume.

4. Wählen Sie am oberen Rand der Seite, **öffnen**. Dadurch wird das Dateitool in Windows Admin Center.
5. Navigieren Sie zu dem Pfad des Volumes an. Hier können Sie die Dateien im Volume durchsuchen.
6. Wählen Sie **hochladen**, und wählen Sie dann eine Datei zum Hochladen.
7. Verwenden Sie den Browser **wieder** Schaltfläche, um zurück zum Bereich "Tools" in Windows Admin Center zu wechseln.

Sehen Sie sich ein kurzes Video zum Öffnen eines Volumes und Dateien hinzufügen.

> [!VIDEO https://www.youtube-nocookie.com/embed/j59z7ulohs4]

## <a name="turn-on-deduplication-and-compression"></a>Aktivieren Sie Deduplizierung und Komprimierung

Deduplizierung und Komprimierung wird pro Volume verwaltet. Deduplizierung und Komprimierung verwendet ein nachbearbeitungsmodell, was bedeutet, dass Sie nicht einsparungen sehen, bis er ausgeführt wird. Wenn dies der Fall, arbeiten sie über alle Dateien, auch solche, die von vorher aufgerufen wurden.

1. Windows Admin Center, eine Verbindung mit einem "direkte Speicherplätze"-Cluster herstellen, und wählen Sie dann **Volumes** aus der **Tools** Bereich.
2. Wählen Sie auf der Seite Volumes die **Inventur** Registerkarte.
3. Wählen Sie in der Liste der Volumes den Namen des Volumes, die zu verwaltenden aus.
4. Klicken Sie auf der Detailseite des Volume, auf die Schalter, mit der Bezeichnung **Deduplizierung und Komprimierung**.
5. Wählen Sie im Bereich Datendeduplizierung Aktivieren der deduplizierungsmodus.

    Anstelle von komplizierten Einstellungen Sie können Windows Admin Center auswählen zwischen vordefinierten Profile für verschiedene Workloads. Wenn Sie nicht sicher sind, verwenden Sie die Standardeinstellung.

6. Wählen Sie **Aktivieren** aus.

Sehen Sie sich ein kurzes Video zum Deduplizierung und Komprimierung zu aktivieren.

> [!VIDEO https://www.youtube-nocookie.com/embed/PRibTacyKko]

## <a name="create-volumes-using-powershell"></a>Erstellen von Volumes mithilfe von PowerShell

Wir empfehlen die Verwendung des Cmdlets **New-Volume** zum Erstellen von Volumes für Direkte Speicherplätze. Es bietet die schnellste und einfachste Methode dafür. Dieses einzelne Cmdlet erstellt, partitioniert und formatiert automatisch den virtuellen Datenträger, erstellt das Volume mit demselben Namen und fügt es freigegebenen Clustervolumes hinzu – alles in einem einfachen Schritt.

Das Cmdlet **New-Volume** hat vier Parameter, die Sie immer angeben müssen:

- **FriendlyName:** Eine beliebige Zeichenfolge, die Sie, z. B. möchten *"Volume1"*
- **FileSystem:** Entweder **CSVFS_ReFS** (empfohlen) oder **CSVFS_NTFS**
- **StoragePoolFriendlyName:** Den Namen Ihres Speicherkontos pool, z. B. *"S2D auf ClusterName"*
- **Größe:** Die Größe des Volumes, z. B. *"10 TB"*

   > [!NOTE]
   > Windows, einschließlich PowerShell, zählt mithilfe von binären Zahlen (Basis 2), während Laufwerke häufig mithilfe von Dezimalzahlen (Basis 10) bezeichnet werden. Dies erklärt, warum ein "Ein Terabyte"-Laufwerk, das als 1,000,000,000,000 Bytes definiert ist, in Windows mit etwa "909 GB" angezeigt wird. Dies ist das erwartungsgemäße Verhalten. Beim Erstellen von Volumes mithilfe von **New-Volume**, müssen Sie den Parameter **Größe** in binären (Basis 2) Zahlen angeben. Beispiel: Bei Angaben von "909 GB" oder "0,909495 TB" wird ein Volume von ungefähr 1,000,000,000,000 Bytes erstellt.

### <a name="example-with-2-or-3-servers"></a>Beispiel: Mit 2 oder 3-Servern

Wenn Ihre Bereitstellung nur zwei Server hat, verwendet Direkte Speicherplätze zur Vereinfachung automatisch die Zweiwegespiegelung, um Robustheit zu erzielen. Wenn Ihre Bereitstellung nur drei Server hat, wird automatisch die Dreiwegespiegelung verwendet.

```PowerShell
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>Beispiel: Mit 4 +-Servern

Wenn Sie vier oder mehr Server haben, können Sie mithilfe des optionalen Parameters **ResiliencySettingName** den Resilienztyp auswählen.

-   **ResiliencySettingName:** Entweder **Spiegel** oder **Parität**.

Im folgenden Beispiel verwendet *"Volume2"* die Dreiwegespiegelung und *"Volume3"* die duale Parität (häufig als "Erasure Coding" bezeichnet).

```PowerShell
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>Beispiel: Verwenden der Speicherebenen

In Bereitstellungen mit drei Arten von Laufwerken kann ein Volume SSD- und HDD-Ebenen umfassen und sich teilweise auf beiden befinden. Ebenso kann ein Volume in Bereitstellungen mit vier oder mehr Servern die Spiegelung und die duale Parität mischen und sich teilweise auf beiden befinden.

Damit Sie solche Volumes erstellen können, bietet Direkte Speicherplätze Standardebenenvorlagen namens *Leistung* und *Kapazität*. Darin sind Definitionen für die Dreiwegespiegelung auf den schnelleren Laufwerken (falls zutreffend) und die duale Parität auf den langsameren Laufwerken (sofern zutreffend) gekapselt.

Sie können diese anzeigen, indem Sie das Cmdlet **Get-StorageTier** ausführen.

```PowerShell
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![PowerShell-Speicherebenen – Screenshot](media/creating-volumes/storage-tiers-screenshot.png)

Zum Erstellen von Volumes mit mehreren Ebenen verweisen Sie mithilfe der Parameter **StorageTierFriendlyNames** und **StorageTierSizes** des Cmdlets **New-Volume** auf diese Ebenenvorlagen. Beispiel: Das folgende Cmdlet erstellt ein Volume, das die Dreiwegespiegelung und duale Parität im Verhältnis 30:70 mischt.

```PowerShell
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
- [Erweitern von Volumes in "direkte Speicherplätze"](resize-volumes.md)
- [Löschen von Volumes in "direkte Speicherplätze"](delete-volumes.md)
