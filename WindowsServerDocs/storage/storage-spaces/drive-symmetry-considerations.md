---
title: Laufwerk Symmetrie Überlegungen für "direkte Speicherplätze"
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/08/2018
Keywords: Direkte Speicherplätze
ms.localizationpriority: medium
ms.openlocfilehash: 629e49a0c1919286d8e4f418b3e99d69e720f4fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866881"
---
# <a name="drive-symmetry-considerations-for-storage-spaces-direct"></a>Laufwerk Symmetrie Überlegungen für "direkte Speicherplätze" 

> Gilt für: Windows Server 2019, Windows Server 2016

["Direkte Speicherplätze"](storage-spaces-direct-overview.md) funktioniert am besten, wenn alle Server genau die gleichen Datenträgern verfügt.

In der Realität erkennen wir, dass dies nicht immer möglich ist: "Direkte Speicherplätze" dient zum Ausführen von jahrelang und Skalierung die Anforderungen Ihrer Organisation zunehmen. Heute können Sie Festplatten "spacious" 3 TB kaufen; nächsten Jahr kann es nicht möglich, um diejenigen zu, dass kleine finden werden. Aus diesem Grund werden gewisse mischen und anpassen.

In diesem Thema wird erläutert, die Einschränkungen und Beispiele der unterstützten und nicht unterstützten Konfigurationen.

## <a name="constraints"></a>Einschränkungen

### <a name="type"></a>Typ

Alle Server müssen die gleiche [Laufwerkstypen](choosing-drives.md#drive-types).

Z. B. wenn ein Server NVMe verfügt, sie sollten *alle* NVMe haben.

### <a name="number"></a>Number

Alle Server sollten über die gleiche Anzahl von Laufwerken jedes Typs verfügen.

Z. B. wenn ein Server sechs SSD verfügt, sie sollten *alle* haben sechs SSD.

   > [!NOTE]
   > Es ist in Ordnung, für die Anzahl der Laufwerke, die vorübergehend bei Ausfällen oder beim Hinzufügen oder Entfernen von Laufwerken unterscheiden.

### <a name="model"></a>Modell

Es wird empfohlen, mithilfe des gleichen Modells und der Firmwareversion möglichst-Laufwerke. Wenn Sie nicht möglich ist, wählen Sie sorgfältig Laufwerke, die so ähnlich wie möglich sind. Es wird davon abgeraten mischen und Anpassen von Laufwerken mit klaren unterschiedlichen Leistungs- oder Endurance Eigenschaften desselben Typs (sofern nicht einer Cache und die andere Kapazität) daran, dass "direkte Speicherplätze"-e/a gleichmäßig verteilt und nicht Sie sich für Modell entscheiden .

   > [!NOTE]
   > Es ist in Ordnung, ähnlich wie SATA- und SAS-Laufwerke und kombinieren.

### <a name="size"></a>Größe

Es wird empfohlen, mithilfe der gleichen Größe möglichst-Laufwerke. Kapazität-Laufwerken mit verschiedenen Größen mit möglicherweise in irgendeiner Form kann nicht verwendet werden, und mithilfe von Cachelaufwerken unterschiedlicher Größe kann cacheleistung nicht verbessert. Finden Sie im nächsten Abschnitt.

   > [!WARNING]
   > Verschiedene Laufwerke kapazitätsumfang auf Servern können dazu führen, dass isolierte Kapazität.

## <a name="understand-capacity-imbalance"></a>Zu verstehen: Kapazität Ungleichgewicht

"Direkte Speicherplätze" ist robust, Kapazität Ungleichgewicht über Laufwerke hinweg und auf Servern. Auch wenn die Diskrepanz schwerwiegend ist, wird alles weiterhin funktioniert. Allerdings kann abhängig von verschiedenen Faktoren, Kapazität, die in jedem Server nicht verfügbar ist nicht verwendet werden.

Um festzustellen, warum dies so ist, sollten Sie vereinfachte in der folgenden Abbildung aus. Jedes farbige Feld stellt eine Kopie der Spiegelung der Daten dar. Beispielsweise markiert die Felder ein, wählen Sie ein ", und ein" werden drei Kopien der gleichen Daten. Server-Fehlertoleranz, diese Kopien der bandbreitendrosselung zu berücksichtigen *müssen* auf verschiedenen Servern gespeichert werden.

### <a name="stranded-capacity"></a>Isolierte Kapazität

Gezeichnet wird, sind die Server-1 (10 TB) und Server 2 (10 TB) voll. Server 3 größerer Laufwerke hat, daher die gesamte Kapazität größer (15 TB). Zum Speichern von Daten für weitere drei-Wege-Spiegelung auf Server 3 erfordert Kopien auf Server 1 und 2 für Server, jedoch die bereits voll sind. Die verbleibenden 5 TB Kapazität auf 3-Server kann nicht verwendet werden – es ist *"isolierte"* Kapazität.

![Drei-Wege-Spiegelung, drei Server, isolierte Kapazität](media/drive-symmetry-considerations/Size-Asymmetry-3N-Stranded.png)

### <a name="optimal-placement"></a>Optimale Platzierung

Dagegen mit vier Servern von 10 TB, 10 TB, 10 TB, und 15 TB Kapazität und Stabilität von drei-Wege-Spiegelung es *ist* mit Kopien ordnungsgemäß auf eine Weise zu versehen, die gesamte verfügbare Kapazität als gezeichneten verwendet. Wann immer dies möglich ist, die "direkte Speicherplätze" Zuweisung sucht und verwendet die optimale Platzierung, lassen keine isolierte Kapazität.

![Drei-Wege-Spiegelung, die vier Servern, die keine isolierte Kapazität](media/drive-symmetry-considerations/Size-Asymmetry-4N-No-Stranded.png)

Die Anzahl von Servern, die resilienz, den Schweregrad der Kapazität daher und anderen Faktoren beeinflussen, ob der isolierte Kapazität verfügbar ist. **Sinnvollste als allgemeine Regel gilt, wird davon ausgegangen, dass nur die verfügbare Kapazität in jedem Server garantiert ist, verwendet werden kann.**

## <a name="understand-cache-imbalance"></a>Zu verstehen: Cache-Ungleichgewicht

"Direkte Speicherplätze" ist robust, Cache Ungleichgewicht über Laufwerke hinweg und auf Servern. Auch wenn die Diskrepanz schwerwiegend ist, wird alles weiterhin funktioniert. Darüber hinaus verwendet "direkte Speicherplätze" immer alle verfügbare Cache die modellbindung voll ausschöpfen.

Allerdings Cachelaufwerken unterschiedlicher Größe möglicherweise nicht verbessert, verwenden cacheleistung gleichmäßig oder vorhersagbares: nur e/a an [Laufwerk Bindungen](understand-the-cache.md#server-side-architecture) mit größerer Cache möglicherweise Laufwerke verbesserte Leistung angezeigt. "Direkte Speicherplätze" gleichmäßig verteilt von e/a auf Bindungen, und nicht entscheiden Sie sich auf Cachekapazität-Verhältnis.

![Cache-Klassen](media/drive-symmetry-considerations/Cache-Asymmetry.png)

   > [!TIP]
   > Finden Sie unter [Grundlegendes zu den Cache](understand-the-cache.md) Weitere Informationen zum Cache-Bindungen.

## <a name="example-configurations"></a>Beispielkonfigurationen

Hier sind einige unterstützten und nicht unterstützten Konfigurationen:

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-models-between-servers"></a>![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: unterschiedliche Modelle zwischen Servern

NVMe-Modell "X" für die ersten zwei Server verwenden, aber der dritte Server verwendet NVMe-Modell "Z", die sehr ähnlich ist.

| Server 1                    | Server 2                    | 3-Server                    |
|-----------------------------|-----------------------------|-----------------------------|
| 2 x NVMe-Modell X (Cache)    | 2 x NVMe-Modell X (Cache)    | 2 x NVMe-Modell Z (Cache)    |
| 10 x SSD-Modell Y (Kapazität) | 10 x SSD-Modell Y (Kapazität) | 10 x SSD-Modell Y (Kapazität) |

Dies wird unterstützt.

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-models-within-server"></a>![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: unterschiedliche Modelle innerhalb von server

Jeder Server verwendet eine andere Mischung von HDD-Modellen "Y" und "Z", die sehr ähnlich sind. Jeder Server verfügt über 10 insgesamt HDD.

| Server 1                   | Server 2                   | 3-Server                   |
|----------------------------|----------------------------|----------------------------|
| 2 x SSD-Modell X (Cache)    | 2 x SSD-Modell X (Cache)    | 2 x SSD-Modell X (Cache)    |
| 7 x HDD-Modell Y (Kapazität) | 5 x HDD-Modell Y (Kapazität) | 1 x-Y HDD-Modell (Kapazität) |
| 3 x HDD-Modell Z (Kapazität) | 5 x HDD-Modell Z (Kapazität) | 9 x HDD-Modell Z (Kapazität) |

Dies wird unterstützt.

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-sizes-across-servers"></a>![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: verschiedene Größen für Server

Verwenden Sie die ersten zwei Server 4-TB-HDDS, aber der dritte Server verwendet, ähnlich wie 6 TB HDD.

| Server 1                | Server 2                | 3-Server                |
|-------------------------|-------------------------|-------------------------|
| 2 x 800 GB NVMe (Cache) | 2 x 800 GB NVMe (Cache) | 2 x 800 GB NVMe (Cache) |
| 4 x 4 TB HDDS (Kapazität) | 4 x 4 TB HDDS (Kapazität) | 4 x 6 TB HDDS (Kapazität) |

Dies wird unterstützt, obwohl dies in isolierte Kapazität führt.

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-sizes-within-server"></a>![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: verschiedene Größen innerhalb von server

Jeder Server verwendet eine andere Mischung von 1,2 TB und sehr ähnlich 1,6 TB SSD. Jeder Server verfügt über 4 insgesamt SSD.

| Server 1                 | Server 2                 | 3-Server                 |
|--------------------------|--------------------------|--------------------------|
| 3 x 1,2 TB SSD (Cache)   | 2 x 1,2 TB SSD (Cache)   | 4 x 1,2 TB SSD (Cache)   |
| 1 x 1,6 TB SSD (Cache)   | 2 x 1,6 TB SSD (Cache)   | -                        |
| 20 x 4TB HDDS (Kapazität) | 20 x 4TB HDDS (Kapazität) | 20 x 4TB HDDS (Kapazität) |

Dies wird unterstützt.

### <a name="unsupportedmediadrive-symmetry-considerationsunsupportedpng-not-supported-different-types-of-drives-across-servers"></a>![nicht unterstützt](media/drive-symmetry-considerations/unsupported.png) Nicht unterstützt: verschiedene Arten von Laufwerken auf Servern

Server 1 ist mit NVMe, aber die anderen nicht.

| Server 1            | Server 2            | 3-Server            |
|---------------------|---------------------|---------------------|
| 6 X NVMe (Cache)    | -                   | -                   |
| -                   | 6 X SSD (Cache)     | 6 X SSD (Cache)     |
| 18 X HDD (Kapazität) | 18 X HDD (Kapazität) | 18 X HDD (Kapazität) |

Dies wird nicht unterstützt. Die Arten von Laufwerken sollte in allen Servern identisch sein.

### <a name="unsupportedmediadrive-symmetry-considerationsunsupportedpng-not-supported-different-number-of-each-type-across-servers"></a>![nicht unterstützt](media/drive-symmetry-considerations/unsupported.png) Nicht unterstützt: unterschiedliche Anzahl jedes Typs auf Servern

3-Server verfügt über weitere Laufwerke als andere.

| Server 1            | Server 2            | 3-Server            |
|---------------------|---------------------|---------------------|
| 2 X NVMe (Cache)    | 2 X NVMe (Cache)    | 4 X NVMe (Cache)    |
| 10 X HDD (Kapazität) | 10 X HDD (Kapazität) | 20 X HDD (Kapazität) |

Dies wird nicht unterstützt. Die Anzahl der Laufwerke der einzelnen Typen sollten in allen Servern identisch sein.

### <a name="unsupportedmediadrive-symmetry-considerationsunsupportedpng-not-supported-only-hdd-drives"></a>![nicht unterstützt](media/drive-symmetry-considerations/unsupported.png) Nicht unterstützt: nur die HDD-Laufwerke

Alle Server verfügen, nur HDD-Laufwerke, die verbunden wird.

|Server 1|Server 2|3-Server|
|-|-|-| 
|18 X HDD (Kapazität) |18 X HDD (Kapazität)|18 X HDD (Kapazität)|

Dies wird nicht unterstützt. Sie müssen mindestens zwei Cachelaufwerken (NvME oder SSD) auf allen Servern hinzufügen.

## <a name="summary"></a>Zusammenfassung

Zusammenfassend lässt sich sagen, sollte es sich bei der alle Server im Cluster die gleichen Arten von Laufwerken und die gleiche Anzahl jedes Typs verfügen. Es wird Laufwerksmodelle und kombinieren und Laufwerkgrößen bei Bedarf mit den oben aufgeführten Überlegungen unterstützt.

| Einschränkung                               |               |
|------------------------------------------|---------------|
| Dieselbe Art von Laufwerken in jedem server     | **Erforderlich**  |
| Dieselbe Anzahl von jeden Typ in jedem server | **Erforderlich**  |
| Gleiche Laufwerksmodellen in jedem server        | Empfohlen   |
| Gleiche Laufwerkgrößen in jedem server         | Empfohlen   |

## <a name="see-also"></a>Siehe auch

- [Storage Spaces Direct-hardwareanforderungen](storage-spaces-direct-hardware-requirements.md)
- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)
