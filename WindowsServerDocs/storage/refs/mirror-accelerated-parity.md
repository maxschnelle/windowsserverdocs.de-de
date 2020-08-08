---
title: Parität mit Beschleunigung per Spiegelung
ms.author: gawatu
manager: masriniv
ms.topic: article
author: gawatu
ms.date: 10/17/2018
ms.assetid: ''
ms.openlocfilehash: f54eb8db2a71fe8576913d7d2123e822661b0732
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942169"
---
# <a name="mirror-accelerated-parity"></a>Parität mit Beschleunigung per Spiegelung

>Gilt für: Windows Server 2019, Windows Server 2016

Speicherplätze können Fehlertoleranz für Daten mit zwei grundlegenden Techniken bereitstellen: Spiegelung und Parität. In [direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md)führt Refs eine Spiegel beschleunigte Parität ein, mit der Sie Volumes erstellen können, die sowohl Spiegel-als auch Paritäts resilienzen verwenden. Die Spiegel Beschleunigung bietet eine kostengünstige, Speicherplatz effiziente Speicherung ohne Leistungseinbußen.

![Spiegel-Accelerated-Parität-Volume](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume.png)

## <a name="background"></a>Hintergrund

Die resilienzschemas für Spiegelung und Parität haben grundlegend andere Speicher-und Leistungsmerkmale:
- Die Spiegelungs Resilienz ermöglicht es Benutzern, eine schnelle Schreibleistung zu erzielen, aber das Replizieren der Daten für jede Kopie ist nicht Speicher fähig.
- Parität hingegen muss die Parität für jeden Schreibvorgang neu berechnen, wodurch die Leistung von zufälligem Schreibvorgang beeinträchtigt wird. Parität ermöglicht es Benutzern jedoch, Ihre Daten mit größerer Speicherplatz Effizienz zu speichern. Weitere Informationen finden Sie unter [Fehlertoleranz für Speicherplätze](../storage-spaces/Storage-Spaces-Fault-Tolerance.md).

Daher ist die Spiegelung vorab freigegeben, um Leistungs sensitiven Speicher bereitzustellen, während die Parität eine verbesserte Auslastung der Speicherkapazität bietet. Bei der Zusammenführung der Spiegel Beschleunigung nutzt Refs die Vorteile der einzelnen resilienztypen, um die Kapazitäts effiziente und leistungsabhängige Speicherung zu gewährleisten, indem beide resilienzschemas innerhalb eines einzelnen Volumes kombiniert werden.

## <a name="data-rotation-on-mirror-accelerated-parity"></a>Daten Drehung bei Spiegel beschleunigter Parität

Refs dreht Daten in Echtzeit zwischen Spiegelung und Parität. Dadurch können eingehende Schreibvorgänge schnell in die Spiegelung geschrieben und dann in die Parität gedreht werden, um effizient gespeichert zu werden. Auf diese Weise werden eingehende e/a-Vorgänge schnell in der Spiegelung gewartet, während die kalten Daten effizient in Parität gespeichert werden, sodass sowohl eine optimale Leistung als auch ein verlorener Speicherplatz auf demselben Volume erzielt werden

Um Daten zwischen Spiegelung und Parität zu drehen, dividiert Refs das Volume logisch in Bereiche der 64-MIB-Einheit, die die Dreheinheit darstellt. Die folgende Abbildung zeigt ein in Regionen unterteilte Spiegel beschleunigtes Paritäts Volume.

![Spiegel-Accelerated-Parität-Volume-with-Storage-Containers](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume-with-Storage-Containers.png)

Refs beginnt mit dem Drehen der vollständigen Bereiche von der Spiegelung in die Parität, sobald die Spiegelebene eine angegebene Kapazitäts Stufe erreicht hat. Anstatt Daten von Spiegelung in Parität zu verschieben, wartet Refs so lange wie möglich auf die Spiegelung und speichert Daten in der Spiegelung. Dies ermöglicht es Refs, die optimale Leistung für die Daten bereitzustellen (siehe "e/a-Leistung" weiter unten).

Wenn Daten von Spiegelung in Parität verschoben werden, werden die Daten gelesen, Paritäts Codierungen werden berechnet, und dann werden die Daten in die Parität geschrieben. In der folgenden Animation wird dies mithilfe eines drei-Wege-gespiegelten Bereichs veranschaulicht, der während der Rotation in einen von Löschung codierten Bereich konvertiert wird:

![Spiegelung-Accelerated-Parität-Rotation](media/mirror-accelerated-parity/Container-Rotation.gif)

## <a name="io-on-mirror-accelerated-parity"></a>E/a auf der Spiegel beschleunigten Parität
### <a name="io-behavior"></a>IO-Verhalten
**Schreibvorgänge:** Eingehende Schreibvorgänge von refs-Diensten auf drei verschiedene Arten:

1.  **Zu spiegelnde Schreibvorgänge:**

    - **1a.** Wenn der eingehende Schreibvorgang vorhandene Daten in der Spiegelung ändert, werden die Daten von refs geändert.
    - **1B.** Wenn der eingehende Schreibvorgang ein neuer Schreibvorgang ist und Refs den freien Speicherplatz in der Spiegelung erfolgreich finden kann, um diesen Schreibvorgang zu verarbeiten, schreiben Refs in die Spiegelung.
    ![Schreiben in Spiegelung](media/mirror-accelerated-parity/Write-to-Mirror.png)

2. **Schreibvorgänge in Spiegelung, neu zugeordnet aus Parität:**

    Wenn der eingehende Schreibvorgang Daten ändert, die gleichwertig sind, und Refs den freien Speicherplatz in der Spiegelung erfolgreich finden kann, um den eingehenden Schreibvorgang zu verarbeiten, werden die vorherigen Daten von refs zunächst in der Parität ungültig und anschließend in die Spiegelung geschrieben. Diese Invalidierung ist ein schneller und kostengünstiger Metadatenvorgang, der zur sinnvollen Verbesserung der auf Parität vorgenommenen Schreibleistung beiträgt.
    ![Neu zugeordnet-schreiben](media/mirror-accelerated-parity/Reallocated-Write.png)

3. **Schreibvorgänge in Parität:**

    Wenn von refs nicht ausreichend freier Speicherplatz in der Spiegelung gefunden werden kann, werden neue Daten von refs in die Parität geschrieben oder vorhandene Daten direkt in Parität geändert. Der Abschnitt "Leistungsoptimierungen" enthält Anleitungen, mit denen Sie die Parität von Schreibvorgängen minimieren können.
    ![Schreiben in Parität](media/mirror-accelerated-parity/Write-to-Parity.png)

**Lesevorgänge:** Refs liest direkt aus der Ebene, die die relevanten Daten enthält. Wenn die Parität mit HDDs erstellt wird, werden diese Daten vom Cache in direkte Speicherplätze zwischengespeichert, um zukünftige Lesevorgänge zu beschleunigen.

> [!NOTE]
> Lesevorgänge bewirken nie, dass Refs Daten zurück in die Spiegelebene drehen.

### <a name="io-performance"></a>IO-Leistung

**Schreibvorgänge:** Jeder oben beschriebene Schreib Typ weist seine eigenen Leistungsmerkmale auf. Grob gesagt sind Schreibvorgänge auf der Spiegelebene viel schneller als neu zugewiesene Schreibvorgänge, und neu zugeordnete Schreibvorgänge sind deutlich schneller als Schreibvorgänge, die direkt in die Paritäts Ebene gestellt werden. Diese Beziehung wird durch die folgende Ungleichheit veranschaulicht:


- **Spiegelebene > neu zugeordnete Schreibvorgänge >> Paritäts Ebene**


**Lesevorgänge:** Beim Lesen von Parität gibt es keine sinnvollen negativen Auswirkungen auf die Leistung:
- Wenn Spiegelung und Parität mit demselben Medientyp erstellt werden, entspricht die Leseleistung.
- Wenn Spiegelung und Parität mit verschiedenen Medientypen erstellt werden – gespiegelte SSDs, Paritäts-HDDs, z. –.[der Cache in direkte Speicherplätze](../storage-spaces/understand-the-cache.md) unterstützt das Zwischenspeichern von Daten, um Lesevorgänge aus Parität zu beschleunigen.

## <a name="refs-compaction"></a>Refs-Komprimierung

In der halbjährlichen Version dieses Jahres führt Refs eine Komprimierung ein, die die Leistung für Daten mit Spiegelungs beschleunigter Parität von 90 +% erheblich verbessert.

**Hintergrund:** Bisher konnten die Leistung dieser Volumes beeinträchtigt werden, da Volumes mit Spiegelungs beschleunigter Parität vollständig waren. Die Leistung wird beeinträchtigt, da heiße und kalte Daten während der volumeüberstunden gemischt werden. Dies bedeutet, dass weniger heiße Daten in der Spiegel Datenbank gespeichert werden können, da kalte Datenspeicher Platz belegen, der andernfalls von heißen Daten verwendet werden kann. Das Speichern von heißen Daten in der Spiegelung ist wichtig für die Aufrechterhaltung der hohen Leistung, da Schreibvorgänge direkt in die Spiegelung erheblich schneller sind als die Neuzuordnung von Schreibvorgängen und der Größenordnung schneller als direkt Daher ist das vorhanden sein von kaltdaten in Spiegelung für die Leistung schlecht, da dadurch die Wahrscheinlichkeit verringert wird, dass Refs Schreibvorgänge direkt in die Spiegelung schreiben kann.

Refs-Komprimierung behandelt diese Leistungsprobleme, indem für heiße Datenspeicher Platz in der Spiegelung freigegeben wird. Compaction konsolidiert zuerst alle Daten – von Spiegelung und Parität – in Parität. Dies reduziert die Fragmentierung innerhalb des Volumes und erhöht den Umfang des adressierbaren Speicherplatzes in der Spiegelung. Noch wichtiger ist, dass dieser Prozess es Refs ermöglicht, heiße Daten zurück in die Spiegelung zu konsolidieren:
-   Wenn neue Schreibvorgänge eingehen, werden Sie in der Spiegelung gewartet. Daher befinden sich neu geschriebene, heiße Daten in Spiegelung.
-   Wenn ein ändernder Schreibvorgang an Daten in Parität vorgenommen wird, wird von refs ein neu zugeordneter Schreibvorgang durchgeführt, sodass dieser Schreibvorgang auch in Spiegelung verarbeitet wird. Folglich werden heiße Daten, die während der Komprimierung in die Parität verschoben wurden, wieder in den Spiegel zugewiesen.

## <a name="performance-optimizations"></a>Leistungsoptimierungen

>[!IMPORTANT]
> Es wird empfohlen, Schreib intensive virtuelle Festplatten in verschiedenen Unterverzeichnissen zu platzieren. Dies liegt daran, dass Refs Metadatenänderungen auf der Ebene eines Verzeichnisses und seiner Dateien schreibt. Wenn Sie also Schreib intensive Dateien über Verzeichnisse verteilen, sind Metadatenvorgänge kleiner und werden parallel ausgeführt, wodurch die Latenz für apps verringert wird.

### <a name="performance-counters"></a>Leistungsindikatoren

Refs verwaltet Leistungsindikatoren, um die Leistung der Spiegel beschleunigten Parität zu bewerten.
- Wie oben im Abschnitt Schreiben in Parität beschrieben, schreiben Refs direkt in die Parität, wenn der freie Speicherplatz in der Spiegelung nicht gefunden werden kann. Dies tritt im Allgemeinen auf, wenn die gespiegelte Ebene schneller aufgefüllt wird, als Refs Daten in Parität drehen kann. Anders ausgedrückt: die refs-Rotation ist nicht in der Lage, mit der Erfassungs Rate zu mithalten. Die folgenden Leistungsindikatoren identifizieren, wann Refs direkt in die Parität schreibt:

  ```
  # Windows Server 2016
  ReFS\Data allocations slow tier/sec
  ReFS\Metadata allocations slow tier/sec

  # Windows Server 2019
  ReFS\Allocation of Data Clusters on Slow Tier/sec
  ReFS\Allocation of Metadata Clusters on Slow Tier/sec
  ```

- Wenn diese Indikatoren ungleich 0 (null) sind, bedeutet dies, dass Refs Daten nicht schnell genug außerhalb des Spiegels dreht. Um dies zu erleichtern, können Sie entweder die Rotations Aggressivität ändern oder die Größe der gespiegelten Ebene vergrößern.

### <a name="rotation-aggressiveness"></a>Aggressivität der Drehung

Refs beginnt mit dem Drehen von Daten, sobald der Spiegel einen angegebenen Kapazitäts Schwellenwert erreicht hat.
-   Höhere Werte dieses Rotations Schwellenwerts bewirken, dass die Daten in der Spiegelebene von refs beibehalten werden. Das belassen von Hot-Daten auf der Spiegelebene eignet sich optimal für die Leistung, aber Refs ist nicht in der Lage, große Mengen eingehender e/a-Vorgänge effektiv zu verarbeiten.
-   Mit niedrigeren Werten können Refs proaktiv Daten bereitstellen und eingehende e/a-Vorgänge besser erfassen. Dies gilt für Erfassungs intensive Workloads, wie z. b. Archivierung. Niedrigere Werte können jedoch die Leistung für allgemeine Workloads beeinträchtigen. Unnötiges Drehen von Daten aus der Spiegelebene führt zu einer Leistungs Einbuße.

Refs führt einen anpassbaren Parameter ein, um diesen Schwellenwert anzupassen, der mit einem Registrierungsschlüssel konfigurierbar ist. Dieser Registrierungsschlüssel muss auf **jedem Knoten in einer direkte Speicherplätze-Bereitstellung**konfiguriert werden, und ein Neustart ist erforderlich, damit alle Änderungen wirksam werden.
-   **Schlüssel:** HKEY_LOCAL_MACHINE \system\currentcontrolset\policies
-   **ValueName (DWORD):** Datadestagessdfillratiothreshold
-   **ValueType:** Aler

Wenn dieser Registrierungsschlüssel nicht festgelegt ist, wird von refs der Standardwert 85% verwendet.  Dieser Standardwert wird für die meisten bereit Stellungen empfohlen, und Werte unter 50% werden nicht empfohlen. Der folgende PowerShell-Befehl zeigt, wie dieser Registrierungsschlüssel mit einem Wert von 75% festgelegt wird:
```PowerShell
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75
 ```
 Um diesen Registrierungsschlüssel für jeden Knoten in einer direkte Speicherplätze Bereitstellung zu konfigurieren, können Sie den folgenden PowerShell-Befehl verwenden:
 ```PowerShell
 $Nodes = 'S2D-01', 'S2D-02', 'S2D-03', 'S2D-04'
 Invoke-Command $Nodes {Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75}
 ```

### <a name="increasing-the-size-of-the-mirrored-tier"></a>Erhöhen der Größe der gespiegelten Ebene

Das Erhöhen der Größe der gespiegelten Ebene ermöglicht es Refs, einen größeren Teil des Arbeits Satzes in der Spiegelung beizubehalten. Dies verbessert die Wahrscheinlichkeit, dass Refs direkt in die Spiegelung schreiben kann, was zu einer besseren Leistung führt. Die folgenden PowerShell-Cmdlets veranschaulichen, wie Sie die Größe der gespiegelten Ebene vergrößern:
```PowerShell
Resize-StorageTier -FriendlyName “Performance” -Size 20GB
Resize-StorageTier -InputObject (Get-StorageTier -FriendlyName “Performance”) -Size 20GB
```
>[!TIP]
>Stellen Sie sicher, dass die Größe der **Partition** **und des** Volumes geändert wird, nachdem Sie die Größe des **storagetier**geändert haben Weitere Informationen und Beispiele finden Sie unter [Resize-Volumes](../storage-spaces/resize-volumes.md).

## <a name="creating-a-mirror-accelerated-parity-volume"></a>Erstellen eines volumebeschleunigten Paritäts Volumes

Mit dem folgenden PowerShell-Cmdlet wird ein zwischengespeicherten Paritäts Volume mit einem Spiegel-und Paritäts Verhältnis von 20:80 erstellt. Dies ist die empfohlene Konfiguration für die meisten Arbeits Auslastungen. Weitere Informationen und Beispiele finden Sie unter [Erstellen von Volumes in direkte Speicherplätze](../storage-spaces/Create-volumes.md).

```PowerShell
New-Volume – FriendlyName “TestVolume” -FileSystem CSVFS_ReFS -StoragePoolFriendlyName “StoragePoolName” -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 200GB, 800GB
```

## <a name="additional-references"></a>Weitere Verweise

-   [ReFS – Übersicht](refs-overview.md)
-   [Block-Clone-Vorgänge auf ReFS](block-cloning.md)
-   [ReFS Integrity Streams](integrity-streams.md)
-   [Direkte Speicherplätze – Übersicht](../storage-spaces/storage-spaces-direct-overview.md)
