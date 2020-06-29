---
title: Erstellen von Volumes in direkte Speicherplätze
description: Erstellen von Volumes in direkte Speicherplätze mithilfe von Windows Admin Center und PowerShell.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 02/25/2020
ms.openlocfilehash: 40750acb260335e858a7763c950dfc4ad2cd7979
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473827"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>Erstellen von Volumes in direkte Speicherplätze

> Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema wird beschrieben, wie Sie mithilfe des Windows Admin Centers und PowerShell Volumes auf einem direkte Speicherplätze-Cluster erstellen.

> [!TIP]
> Wenn Sie dies noch nicht getan haben, besuchen Sie zuerst die [Planungs Volumes in direkte Speicherplätze](plan-volumes.md) .

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

Es wird empfohlen, das Cmdlet **New-Volume** zum Erstellen von Volumes für direkte Speicherplätze zu verwenden. Dies ist die schnellste und einfachste Möglichkeit. Mit diesem Cmdlet wird mit nur einem einfachen Schritt Folgendes durchgeführt: Der virtuelle Datenträger wird automatisch erstellt und anschließend partitioniert und formatiert, und das Volume wird mit dem entsprechenden Namen erstellt und den freigegebenen Clustervolumes hinzugefügt.

Das Cmdlet **New-Volume** verfügt über vier Parameter, die Sie immer angeben müssen:

- **FriendlyName:** Eine beliebige Zeichenfolge, z. B. *„Volume1“* .
- **FileSystem:** Entweder **CSVFS_ReFS** (empfohlen) oder **CSVFS_NTFS**.
- **StoragePoolFriendlyName:** Der Name Ihres Speicherpools, z. B. *„S2D auf Clustername“* .
- **Size:** Die Größe des Volumes, z. B. *„10TB“* .

   > [!NOTE]
   > Unter Windows, einschließlich PowerShell, wird basierend auf Binärzahlen (Basis 2) gezählt, während für Laufwerke häufig Dezimalzahlen (Basis 10) verwendet werden. Dies ist der Grund, warum für ein Laufwerk mit „einem Terabyte“ (als 1.000.000.000.000 Byte definiert) in Windows die Größe als „909 GB“ angezeigt wird. Dies entspricht dem erwarteten Verhalten. Beim Erstellen von Volumes mit **New-Volume** sollten Sie den Parameter **Size** als Binärzahl (Basis 2) angeben. Wenn Sie beispielsweise „909GB“ oder „0,909495TB“ angeben, wird ein Volume mit ca. 1.000.000.000.000 Byte erstellt.

### <a name="example-with-2-or-3-servers"></a>Beispiel: Mit zwei oder drei Servern

Falls Ihre Bereitstellung nur über zwei Server verfügt, nutzt „Direkte Speicherplätze“der Einfachheit halber automatisch die Zwei-Wege-Spiegelung zur Erzielung von Resilienz. Falls Ihre Bereitstellung nur drei Server umfasst, wird automatisch die Drei-Wege-Spiegelung genutzt.

```PowerShell
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>Beispiel: Mit vier oder mehr Servern

Wenn Sie über vier oder mehr Server verfügen, können Sie den optionalen Parameter **ResiliencySettingName** verwenden, um Ihren Resilienztyp zu wählen.

-   **ResiliencySettingName:** Entweder **Mirror** (Spiegelung) oder **Parity** (Parität).

Im folgenden Beispiel wird für *„Volume2“* die Drei-Wege-Spiegelung und für *„Volume3“* die duale Parität (häufig als „Erasure Coding“ bezeichnet) verwendet.

```PowerShell
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>Beispiel: Verwenden von Speicherebenen

Bei Bereitstellungen mit drei Arten von Laufwerken kann ein Volume für die SSD- und HDD-Ebene übergreifend verwendet werden und jeweils teilweise auf diesen Laufwerken angeordnet werden. Bei Bereitstellungen mit vier oder mehr Servern können für ein Volume Spiegelung und duale Parität so gemischt werden, dass sie darauf jeweils teilweise angeordnet sind.

Als Hilfe bei der Erstellung dieser Volumes werden von „Direkte Speicherplätze“ Standardvorlagen für Ebenen bereitgestellt, die die Bezeichnungen *Leistung* und *Kapazität* haben. Sie enthalten Definitionen für die Drei-Wege-Spiegelung auf den schnelleren Kapazitätslaufwerken (falls zutreffend) und für die duale Parität auf den langsameren Kapazitätslaufwerken (falls zutreffend).

Sie können dies anzeigen, indem Sie das Cmdlet **Get-StorageTier** ausführen.

```PowerShell
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![Screenshot: Speicherebenen in PowerShell](media/creating-volumes/storage-tiers-screenshot.png)

Verweisen Sie zum Erstellen von mehrstufigen Volumes auf diese Ebenenvorlagen, indem Sie die Parameter **StorageTierFriendlyNames** und **StorageTierSizes** des Cmdlets **New-Volume** nutzen. Beispielsweise wird mit dem folgenden Cmdlet ein Volume erstellt, für das die Drei-Wege-Spiegelung und die duale Parität im Verhältnis 30:70 gemischt werden.

```PowerShell
New-Volume -FriendlyName "Volume4" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 300GB, 700GB
```

Sie haben es geschafft! Wiederholen Sie diese Schritte bei Bedarf, um mehr als ein Volume zu erstellen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- [Planen von Volumes in direkte Speicherplätze](plan-volumes.md)
- [Erweitern von Volumes in direkte Speicherplätze](resize-volumes.md)
- [Löschen von Volumes in direkte Speicherplätze](delete-volumes.md)
