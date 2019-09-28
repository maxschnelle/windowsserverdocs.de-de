---
title: Erstellen von Volumes in Direkte Speicherplätze
description: Erstellen von Volumes in direkte Speicherplätze mithilfe von Windows Admin Center und PowerShell.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 06/06/2019
ms.openlocfilehash: 8c17671f2f15d1373973dcf2fbafc753f0a163a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402887"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>Erstellen von Volumes in Direkte Speicherplätze

> Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema wird beschrieben, wie Volumes auf einem direkte Speicherplätze Cluster mithilfe von Windows Admin Center, PowerShell oder Failovercluster-Manager erstellt werden.

> [!TIP]
> Lesen Sie zunächst [Planen von Volumes in Direkte Speicherplätze](plan-volumes.md), falls noch nicht geschehen.

## <a name="create-a-three-way-mirror-volume"></a>Erstellen eines drei-Wege-Spiegelungs Volumens

So erstellen Sie ein drei-Wege-Spiegelungs Volume im Windows Admin Center: 

1. Stellen Sie im Windows Admin Center eine Verbindung mit einem direkte Speicherplätze Cluster her, und wählen Sie dann im Bereich **Tools** die Option **Volumes** aus.
2. Wählen Sie auf der Seite Volumes die Registerkarte **Inventar** aus, und wählen Sie dann **Volume erstellen**aus.
3. Geben Sie im Bereich **Volume erstellen** einen Namen für das Volume ein, und belassen Sie die **Resilienz** als **drei-Wege-Spiegelung**.
4. Geben Sie unter **HDD**die Größe des Volumes an. Beispielsweise 5 TB (Terabyte).
5. Wählen Sie **Erstellen** aus.

Abhängig von der Größe kann das Erstellen des Volumes einige Minuten dauern. Mit den Benachrichtigungen in der oberen rechten Ecke werden Sie informiert, wenn das Volume erstellt wird. Das neue Volume wird in der Inventur Liste angezeigt.

Sehen Sie sich ein kurzes Video zum Erstellen eines drei-Wege-Spiegelungs Volumes an.

> [!VIDEO https://www.youtube-nocookie.com/embed/o66etKq70N8]

## <a name="create-a-mirror-accelerated-parity-volume"></a>Erstellen eines Volumes mit Spiegelungs beschleunigter Parität

Die Spiegel Beschleunigung verringert den Speicherbedarf des Volumes auf der HDD. Ein Volume mit drei-Wege-Spiegelung bedeutet beispielsweise, dass Sie für alle 10 Terabyte eine Größe von 30 Terabyte benötigen. Um den mehr Aufwand für den Speicherbedarf zu reduzieren, erstellen Sie ein Volume mit einer zwischen spiegelung beschleunigten Parität. Dadurch wird der Speicherbedarf von 30 Terabyte auf nur 22 Terabyte reduziert, auch nur bei vier Servern, indem die aktivsten 20% der Daten gespiegelt werden, und es wird eine Parität verwendet, bei der mehr Speicherplatz zur Speicherung der übrigen Speicherplatz zur Neige geht. Sie können dieses Verhältnis zwischen Parität und Spiegelung anpassen, um die Leistung im Vergleich zur Kapazitätssteigerung zu erzielen, die für ihre Arbeitsauslastung geeignet ist. Beispielsweise ergibt die 90-Prozent Parität und 10-Prozent-Spiegelung weniger Leistung, aber der Speicherbedarf wird noch weiter optimiert.

So erstellen Sie ein Volume mit Spiegel beschleunigter Parität im Windows Admin Center:

1. Stellen Sie im Windows Admin Center eine Verbindung mit einem direkte Speicherplätze Cluster her, und wählen Sie dann im Bereich **Tools** die Option **Volumes** aus.
2. Wählen Sie auf der Seite Volumes die Registerkarte **Inventar** aus, und wählen Sie dann **Volume erstellen**aus.
3. Geben Sie im Bereich **Volume erstellen** einen Namen für das Volume ein.
4. Wählen Sie unter **Resilienz**die Option **Spiegel Beschleunigung der Parität**aus.
5. Wählen Sie in **Prozentsatz der Parität**den Prozentsatz der Parität aus.
6. Wählen Sie **Erstellen** aus.

Sehen Sie sich ein kurzes Video an, in dem das Erstellen eines auf Spiegelung beschleunigten Paritäts Volumens.

> [!VIDEO https://www.youtube-nocookie.com/embed/R72QHudqWpE]

## <a name="open-volume-and-add-files"></a>Volume öffnen und Dateien hinzufügen

So öffnen Sie ein Volume und fügen dem Volume im Windows Admin Center Dateien hinzu:

1. Stellen Sie im Windows Admin Center eine Verbindung mit einem direkte Speicherplätze Cluster her, und wählen Sie dann im Bereich **Tools** die Option **Volumes** aus.
2. Wählen Sie auf der Seite Volumes die Registerkarte **Inventur** aus.
2. Wählen Sie in der Liste der Volumes den Namen des Volumes aus, das Sie öffnen möchten.

    Auf der Seite Volumedetails können Sie den Pfad zum Volume sehen.

4. Wählen Sie oben auf der Seite **Öffnen**aus. Dadurch wird das Tool Dateien im Windows Admin Center gestartet.
5. Navigieren Sie zum Pfad des Volumes. Hier können Sie die Dateien im Volume durchsuchen.
6. Wählen Sie **hochladen**, und wählen Sie dann eine hoch zuladende Datei aus.
7. Verwenden Sie die Schaltfläche **zurück** , um zum Bereich Extras im Windows Admin Center zurückzukehren.

Sehen Sie sich ein kurzes Video zum Öffnen eines Volumes und zum Hinzufügen von Dateien an.

> [!VIDEO https://www.youtube-nocookie.com/embed/j59z7ulohs4]

## <a name="turn-on-deduplication-and-compression"></a>Deduplizierung und Komprimierung aktivieren

Deduplizierung und Komprimierung werden pro Volume verwaltet. Bei der Deduplizierung und Komprimierung wird ein Nachbearbeitungs Modell verwendet. Dies bedeutet, dass Sie die Einsparungen erst sehen, wenn Sie ausgeführt werden. Wenn dies der Fall ist, wird er über alle Dateien, auch über alle Dateien, die zuvor vorhanden waren, funktionieren.

1. Stellen Sie im Windows Admin Center eine Verbindung mit einem direkte Speicherplätze Cluster her, und wählen Sie dann im Bereich **Tools** die Option **Volumes** aus.
2. Wählen Sie auf der Seite Volumes die Registerkarte **Inventur** aus.
3. Wählen Sie in der Liste der Volumes den Namen des Volumes aus, das Sie verwalten möchten.
4. Klicken Sie auf der Seite Volumedetails auf den Switch mit der Bezeichnung **Deduplizierung und Komprimierung**.
5. Wählen Sie im Bereich Deduplizierung aktivieren den deduplizierungsmodus aus.

    Anstelle komplizierter Einstellungen können Sie mit dem Windows Admin Center zwischen vorgefertigten Profilen für verschiedene Workloads wählen. Wenn Sie sich nicht sicher sind, verwenden Sie die Standardeinstellung.

6. Wählen Sie **Aktivieren** aus.

Sehen Sie sich ein kurzes Video zum Aktivieren der Deduplizierung und Komprimierung an.

> [!VIDEO https://www.youtube-nocookie.com/embed/PRibTacyKko]

## <a name="create-volumes-using-powershell"></a>Erstellen von Volumes mithilfe von PowerShell

Wir empfehlen die Verwendung des Cmdlets **New-Volume** zum Erstellen von Volumes für Direkte Speicherplätze. Es bietet die schnellste und einfachste Methode dafür. Dieses einzelne Cmdlet erstellt, partitioniert und formatiert automatisch den virtuellen Datenträger, erstellt das Volume mit demselben Namen und fügt es freigegebenen Clustervolumes hinzu – alles in einem einfachen Schritt.

Das Cmdlet **New-Volume** hat vier Parameter, die Sie immer angeben müssen:

- **FriendlyName** Eine beliebige Zeichenfolge, z. b. *"volume1"*
- **Verwendet** Entweder **CSVFS_ReFS** (empfohlen) oder **CSVFS_NTFS**
- **Storagepoolfriendlyname:** Der Name des Speicherpools, z. b. *"S2D on Cluster Name"*
- **Größe:** Die Größe des Volumes, z. b *. "10 TB"*

   > [!NOTE]
   > Windows, einschließlich PowerShell, zählt mithilfe von binären Zahlen (Basis 2), während Laufwerke häufig mithilfe von Dezimalzahlen (Basis 10) bezeichnet werden. Dies erklärt, warum ein "Ein Terabyte"-Laufwerk, das als 1,000,000,000,000 Bytes definiert ist, in Windows mit etwa "909 GB" angezeigt wird. Dies ist das erwartungsgemäße Verhalten. Beim Erstellen von Volumes mithilfe von **New-Volume**, müssen Sie den Parameter **Größe** in binären (Basis 2) Zahlen angeben. Beispiel: Bei Angaben von "909 GB" oder "0,909495 TB" wird ein Volume von ungefähr 1,000,000,000,000 Bytes erstellt.

### <a name="example-with-2-or-3-servers"></a>Beispiel: Mit 2 oder 3 Servern

Wenn Ihre Bereitstellung nur zwei Server hat, verwendet Direkte Speicherplätze zur Vereinfachung automatisch die Zweiwegespiegelung, um Robustheit zu erzielen. Wenn Ihre Bereitstellung nur drei Server hat, wird automatisch die Dreiwegespiegelung verwendet.

```PowerShell
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>Beispiel: Mit vier Servern

Wenn Sie vier oder mehr Server haben, können Sie mithilfe des optionalen Parameters **ResiliencySettingName** den Resilienztyp auswählen.

-   **ResiliencySettingName** Entweder **Spiegelung** oder **Parität**.

Im folgenden Beispiel verwendet *"Volume2"* die Dreiwegespiegelung und *"Volume3"* die duale Parität (häufig als "Erasure Coding" bezeichnet).

```PowerShell
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>Beispiel: Verwenden von Speicherebenen

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

### <a name="step-1-create-virtual-disk"></a>Schritt 1: Erstellen eines virtuellen Datenträgers

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

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- [Planen von Volumes in direkte Speicherplätze](plan-volumes.md)
- [Erweitern von Volumes in direkte Speicherplätze](resize-volumes.md)
- [Löschen von Volumes in direkte Speicherplätze](delete-volumes.md)
