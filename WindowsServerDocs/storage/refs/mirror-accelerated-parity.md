---
title: Durch Spiegelung beschleunigte Parität
ms.prod: windows-server-threshold
ms.author: gawatu
ms.manager: masriniv
ms.technology: storage-file-systems
ms.topic: article
author: gawatu
ms.date: 10/17/2018
ms.assetid: ''
ms.openlocfilehash: 0f4fb73941c5d6667d3c13356b6f29178d73788f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447684"
---
# <a name="mirror-accelerated-parity"></a>Durch Spiegelung beschleunigte Parität

>Gilt für: Windows Server 2019, Windows Server 2016

Speicherplätze können eine Fehlertoleranz für Daten mithilfe von zwei grundlegende Verfahren anbieten: Spiegelung und Parität. In [Direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md) führt ReFS die durch Spiegelung beschleunigte Parität ein und ermöglicht so das Erstellen von Volumes, die sowohl Spiegelungs- als auch Paritätsresilienz verwenden. Die durch Spiegelung beschleunigte Parität bietet kostengünstigen, platzsparenden Speicher ohne Kompromisse bei der Leistung an. 

![Durch Spiegelung beschleunigte Paritätsvolumes](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume.png)

## <a name="background"></a>Hintergrund

Spiegelungs- und Paritätsresilienz-Schemata weisen grundlegend unterschiedliche Speicherplatz- und Leistungsanforderungsmerkmale auf:
- Spiegelungsresilienz ermöglicht Benutzern, schnell Schreibvorgänge zu erreichen, doch das Replizieren der Daten für jede Kopie ist nicht platzsparend. 
- Parität, muss andererseits für jeden Schreibvorgang die Parität neu berechnen, worunter die zufällige Leistung der Schreibvorgänge leidet. Parität ermöglicht dem Benutzer allerdings, seine Daten Speicherplatz mit einer größeren Effizienz des Speicherplatzes zu speichern. Weitere Informationen finden Sie unter [Speicherplätze Fehlertoleranz](../storage-spaces/Storage-Spaces-Fault-Tolerance.md).

Daher bietet die Spiegelung leistungsrelevante Speicher, während die Parität eine bessere Nutzung der Speicherkapazität bietet. Bei einer durch Spiegelung beschleunigten Parität nutzt ReFS die Vorteile der einzelnen Resilienztypen, um sowohl effizient Speicherkapazität als auch leistungsrelevante Speicherung durch die Kombination der beiden Resilienzschematas innerhalb eines einzelnen Volumes zu bieten.

## <a name="data-rotation-on-mirror-accelerated-parity"></a>Daten-Drehung auf durch Spiegelung beschleunigte Parität

ReFS dreht aktiv Daten zwischen Spiegelung und Parität, und zwar in Echtzeit. Dadurch können eingehende Schreibvorgänge schnell auf die Spiegelung geschrieben werden, und anschließend auf die Parität gedreht und so auf effiziente Weise gespeichert werden. Dadurch werden eingehende E/A-Vorgänge schnell in der Spiegelung bearbeitet, während kalte Daten effizient in der Parität bearbeitet werden. Dies bietet gleichzeitig eine optimale Leistung und kostengünstigen Speicher auf demselben Datenträger. 

Um Daten zwischen Spiegelung und Parität zu drehen, teilt ReFS das Volume logisch in Regionen von 64 MiB ein, der Einheit der Drehung. Das folgende Bild zeigt ein in Regionen unterteiltes durch Spiegelung beschleunigtes Paritätsvolume an. 

![Durch Spiegelung beschleunigte Paritätsvolumes mit Speichercontainern](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume-with-Storage-Containers.png)

ReFS beginnt, vollständige Regionen von Spiegelung auf Parität zu drehen, sobald die Spiegelebene eine angegebene Kapazität erreicht hat. Anstatt die Daten sofort von der Spiegelung auf die Parität zu verschieben, wartet ReFS und speichert Daten so lange wie möglich in der Spiegelung, was ReFS ermöglicht, auch weiterhin eine optimale Leistung für die Daten zu bieten (siehe "E/A-Leistung" weiter unten). 

Wenn Daten von der Spiegelung auf die Parität verschoben werden, werden die Daten gelesen, wird die Paritätscodierung berechnet und die Daten werden anschließend in die Parität geschrieben. Die folgende Animation zeigt dies mithilfe eines gespiegelten Drei-Wege-Bereichs, der während der Drehung in einer Erasure codierten Region konvertiert wird:

![Durch Spiegelung beschleunigte Parität-Drehung](media/mirror-accelerated-parity/Container-Rotation.gif)

## <a name="io-on-mirror-accelerated-parity"></a>E/A auf durch Spiegelung beschleunigter Parität
### <a name="io-behavior"></a>E/A-Verhalten
**Schreibt:** ReFS Services eingehende Schreibvorgänge auf drei verschiedene Arten:

1.  **In den Spiegel geschrieben:**

    - **1a.** wenn der eingehende Schreibvorgang vorhandene Daten in der Spiegelung ändert, ändert ReFS die vorhandenen Daten.
    - **1b.** Wenn der eingehende Schreibvorgang ein neuer Schreibvorgang ist und ReFS erfolgreich genügend freien Speicherplatz in der Spiegelung für den Schreibvorgang findet, schreibt schreibt ReFS auf die Spiegelung.
    ![Write-to-Mirror](media/mirror-accelerated-parity/Write-to-Mirror.png)

2. **Schreibt in die Spiegeldatenbank aus Parität neu zugewiesen:**

    Wenn der eingehende Schreibvorgang Daten in der Parität ändert und ReFS erfolgreich genügend freien Speicherplatz für den eingehenden Schreibvorgang auf der Spiegelung findet, macht ReFS zunächst die vorherigen Daten in der Parität ungültig und schreibt sie anschließend auf die Spiegelung. Diese Ungültigkeit ist ein schneller und kostengünstiger Metadatenvorgang, der nennenswerten dazu beiträgt, die Leistung der Schreibvorgänge für die Parität zu verbessern.
    ![Reallocated-Write](media/mirror-accelerated-parity/Reallocated-Write.png)

3. **Schreibt in Parität erfolgen:**
    
    Wenn ReFS nicht genügend freien Speicherplatz in der Spiegelung finden kann, schreibt ReFS neue Daten auf die Parität oder ändert direkt vorhandene Daten in der Parität. Der Abschnitt "Leistungsoptimierungen" enthält Richtlinien, die die Schreibvorgänge auf die Parität minimieren.
    ![Write-to-Parity](media/mirror-accelerated-parity/Write-to-Parity.png)

**Liest:** ReFS liest direkt aus der Ebene, die die relevanten Daten enthält. Wenn die Parität mit HDDs erstellt wird, wird der Cache in den direkten Speicherplätzen diese Daten zur Beschleunigung zukünftiger Lesevorgänge zwischenspeichern. 

> [!NOTE]
> Lesevorgänge bringen ReFS nie dazu, Daten zurück auf die Spiegelebene zu drehen. 

### <a name="io-performance"></a>E/a-Leistung

**Schreibt:** Jeder der oben beschriebenen schreiben verfügt über eigene Leistungsmerkmale. Grob gesagt sind Schreibvorgänge auf der Spiegelebene viel schneller als neu zugeordnete Schreibvorgänge und neu zugeordnete Schreibvorgänge sind deutlich schneller als Schreibvorgänge, die direkt auf Paritätsebene ausgeführt werden. Diese Beziehung wird durch die folgende Ungleichheit veranschaulicht: 


- **Spiegeln Ebene > zugewiesen Schreibvorgänge >> Paritätsebene**


**Liest:** Beim Lesen aus Parität hat keine sinnvolle und negative Leistung Auswirkungen:
- Wenn Spiegelung und Parität mit dem gleichen Medientyp erstellt werden, ist die Leistung der Lesevorgänge gleichwertig. 
- Wenn Spiegelung und Parität nicht mit dem gleichen Medientyp erstellt werden – z. B. gespiegelte SSDs, Paritäts-HDDs – dient [der Cache in den direkten Speicherplätzen](../storage-spaces/understand-the-cache.md) als Cache für heiße Daten, um alle Lesevorgänge von der Parität aus zu beschleunigen.

## <a name="refs-compaction"></a>ReFS-Komprimierung

In der halbjährliche Herbstversion führt ReFS die Komprimierung ein, die die Leistung für die durch Spiegelung beschleunigte Paritätsvolumes, die 90 % voll ist, erheblich verbessert. 

**Hintergrund:** Zuvor als Spiegel beschleunigte paritätsvolumes auf full festgelegt wurde, kann die Leistung von diesen Volumes beeinträchtigt werden. Die Leistung nimmt ab, da die heißen und kalten Daten der gesamten das Volume im Laufe der Zeit vermischt werden. Dies bedeutet, dass weniger heiße Daten in der Spiegelung gespeichert werden können, da kalte Daten in der Spiegelung den Speicherplatz belegen, der andernfalls von heißen Daten verwendet werden könnte. Das Speichern von heißen Daten in der Spiegelung ist entscheidend, um die optimale Leistung aufrechtzuerhalten, da direkte Schreibvorgänge auf die Spiegelung schneller als das neue Zuordnen von Schreibvorgängen ist, und die Größenordnungen schneller als direkte Schreibvorgänge auf die Parität sind. Daher wirkt sich das Speichern kalter Daten in der Spiegelung negativ auf die Leistung aus, da es die Wahrscheinlichkeit verringert, dass ReFS Schreibvorgänge direkt auf die Spiegelung schreibt. 

Die ReFS-Komprimierung behandelt diese Leistungsprobleme durch das Freigeben von Speicherplatz in der Spiegelung für heiße Daten. Eine Komprimierung konsolidiert zuerst alle Daten – von Spiegelung und Parität – in Parität. Dies reduziert die Fragmentierung des Volumes und erhöht den adressierbaren Speicherplatz in der Spiegelung. Was noch wichtiger ist: dieser Prozess ermöglicht ReFS, heiße Daten wieder in der Spiegelung zu konsolidieren:
-   Wenn neue Schreibvorgänge eingehen, werden diese in der Spiegelung bearbeitet. Die neu geschriebenen heißen Daten befinden sich daher in der Spiegelung. 
-   Beim Ändern des Schreibvorgangs auf Daten in der Parität führt ReFS einen neu zugeordneten Schreibvorgang durch, damit dieser Schreibvorgang ebenfalls in der Spiegelung bearbeitet wird. Aus diesem Grund werden heiße Daten, die bei der Komprimierung in die Parität verschoben wurden erneut der Spiegelung zugewiesen. 

## <a name="performance-optimizations"></a>Leistungsoptimierungen

>[!IMPORTANT]
> Es wird empfohlen, mit vielen Schreibvorgängen VHDs in verschiedenen Unterverzeichnissen platzieren. Dies ist da ReFS schreibt die Metadaten-Änderungen auf der Ebene der ein Verzeichnis und die zugehörigen Dateien. Wenn Sie in Verzeichnissen mit vielen Schreibvorgängen Dateien verteilen, sind Vorgänge mit Metadaten also kleiner und verringert die Latenz für apps gleichzeitig ausführen.

### <a name="performance-counters"></a>Leistungsindikatoren

ReFS behält Leistungsindikatoren, um die Leistung der durch Spiegelung beschleunigten Parität zu bewerten. 
- Wie oben im Abschnitt „Schreibvorgänge auf die Parität” beschrieben, schreibt ReFS direkt in die Parität, wenn es keinen freien Speicherplatz in der Spiegelung finden kann. Das tritt in der Regel dann auf, wenn die gespiegelte Ebene schneller gefüllt wird, als die ReFS Daten auf die Parität drehen kann. Anders ausgedrückt, kann die ReFS-Drehung nicht mit der Aufnahme der Änderungsrate mithalten. Die folgenden Leistungsindikatoren ermitteln, wann ReFS direkt auf die Parität schreibt:
  ```
  ReFS\Data allocations slow tier/sec
  ReFS\Metadata allocations slow tier/sec
  ```
- Wenn diese Indikatoren ungleich NULL sind, bedeutet die, dass ReFS die Daten nicht schnell genug aus der Spiegelung dreht. Damit dies vermieden wird, kann die Aggressivität der Drehung geändert oder die Größe der gespiegelten Ebene erhöht werden.

### <a name="rotation-aggressiveness"></a>Drehung Aggressivität

ReFS beginnt mit dem Drehen der Daten, wenn die Spiegelung einen angegebenen Kapazitätsschwellenwert erreicht hat.
-   Höhere Werte des Drehungsschwellenwerts führen dazu, dass ReFS die Daten in der Spiegelebene länger beibehält. Heiße Daten in der Spiegelebene zu lassen ist für die Leistung optimal, doch ReFS ist nicht in der Lage, große Mengen an eingehenden E/A-Prozessen effektiv zu verarbeiten. 
-   Niedrigere Werte ermöglichen ReFS, proaktiv Daten auszulagern und eingehende E/A-Prozesse besser zu verarbeiten. Dies gilt für Arbeitsauslastungen mit hoher Aufnahmekapazität wie die Archivierungsspeicherung. Niedrigere Werte können jedoch die Leistung für allgemeine Workloads beeinträchtigen. Das Drehen unnötiger Daten aus der Spiegelebene führt zu Leistungseinbußen. 

ReFS führt einen einstellbaren Parameter für diesen Schwellenwert ein, der mit einem Registrierungsschlüssel konfiguriert werden kann. Dieser Registrierungsschlüssel muss unter **jeden Knoten in einer Bereitstellung mit direkten Speicherplätzen** konfiguriert werden, und ein Neustart ist erforderlich, damit die Änderungen wirksam werden. 
-   **Schlüssel:** HKEY_LOCAL_MACHINE\System\CurrentControlSet\Policies
-   **ValueName (DWORD):** DataDestageSsdFillRatioThreshold
-   **ValueType:** Prozentsatz

Wenn dieser Registrierungsschlüssel nicht festgelegt ist, verwendet ReFS einen Standardwert von 85 %.  Dieser Standardwert wird für die meisten Bereitstellungen empfohlen und Werte unter 50 % werden nicht empfohlen. Der folgende PowerShell-Befehl veranschaulicht, wie dieser Registrierungsschlüssel mit dem Wert 75 % erstellt werden kann: 
```PowerShell
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75
 ```
 Um diesen Registrierungsschlüssel auf allen Knoten in einer Bereitstellung mit direkten Speicherplätzen zu konfigurieren, können Sie den folgenden PowerShell-Befehl ausführen:
 ```PowerShell
 $Nodes = 'S2D-01', 'S2D-02', 'S2D-03', 'S2D-04'
 Invoke-Command $Nodes {Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75}
 ```

### <a name="increasing-the-size-of-the-mirrored-tier"></a>Durch Erhöhen der Größe der gespiegelten-Ebene

Das Erhöhen der gespiegelten Ebene ermöglicht ReFS, einen größeren Teil des Arbeitssatzes in der Spiegelung beizubehalten. Dies verbessert die Wahrscheinlichkeit, das ReFS direkt in die Spiegelung schreiben kann, was zur Verbesserung der Leistung führt. Die folgenden PowerShell-Cmdlets veranschaulichen, wie Sie die Größe der gespiegelten Ebene erhöhen können:
```PowerShell
Resize-StorageTier -FriendlyName “Performance” -Size 20GB
Resize-StorageTier -InputObject (Get-StorageTier -FriendlyName “Performance”) -Size 20GB
```
>[!TIP]
>Stellen Sie sicher, dass Sie die Größe der **Partition** und des **Volumes** ändern, nachdem Sie die Größe des **StorageTier** geändert haben. Weitere Informationen und Beispiele finden Sie unter [Volumes skalieren](../storage-spaces/resize-volumes.md).

## <a name="creating-a-mirror-accelerated-parity-volume"></a>Erstellen von durch Spiegelung beschleunigter Paritätsvolumes

Das folgende PowerShell-Cmdlet erstellt ein durch Spiegelung beschleunigtes Paritätsvolumes mit einem Spiegelung: Parität-Verhältnis von 20: 80. Dies ist die empfohlene Konfiguration für die meisten Arbeitslasten. Weitere Informationen und Beispiele finden Sie unter [Erstellen von Volumes in Direkte Speicherplätze](../storage-spaces/Create-volumes.md).

```PowerShell
New-Volume – FriendlyName “TestVolume” -FileSystem CSVFS_ReFS -StoragePoolFriendlyName “StoragePoolName” -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 200GB, 800GB
```

## <a name="see-also"></a>Siehe auch

-   [ReFS-Übersicht](refs-overview.md)
-   [Klonen von ReFS-block](block-cloning.md)
-   [ReFS integritätsdatenströme](integrity-streams.md)
-   [Übersicht über Storage "direkte Speicherplätze"](../storage-spaces/storage-spaces-direct-overview.md)
