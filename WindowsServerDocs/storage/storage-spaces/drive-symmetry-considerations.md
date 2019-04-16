---
title: Laufwerk Symmetrie Aspekte für "direkte Speicherplätze"
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/08/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 629e49a0c1919286d8e4f418b3e99d69e720f4fd
ms.sourcegitcommit: f2ef58003da6de049c7c4b578f789a97e0a0f512
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/26/2018
ms.locfileid: "5591846"
---
# Laufwerk Symmetrie Aspekte für "direkte Speicherplätze" 

> Gilt für: WindowsServer 2019, WindowsServer 2016

["Direkte Speicherplätze"](storage-spaces-direct-overview.md) funktioniert am besten, wenn jeder Server genau die gleiche Laufwerke verfügt.

In der Praxis wir erkennen Dies ist nicht immer praktisch: "direkte Speicherplätze" wurde entwickelt, um Jahre lang und Skalierung führen Sie die Bedürfnissen Ihrer Organisation wachsen. Sie können heute großen Raum 3 TB Festplatten kaufen; nächste Jahr kann unmöglich, solche klein gefunden werden. Aus diesem Grund wird gewisse mischen und Operatoren unterstützt.

In diesem Thema wird erläutert, die Einschränkungen und enthält Beispiele für unterstützte und nicht unterstützte Konfigurationen.

## Einschränkungen

### Typ

Alle Server sollten die gleichen [Arten von Laufwerken](choosing-drives.md#drive-types)verfügen.

Wenn ein Server über NVMe verfügt, sollten sie z. B. *Alle* NVMe haben.

### Zahl

Alle Server sollten die gleiche Anzahl von Laufwerken von jedem Typ haben.

Wenn ein Server sechs SSD verfügt, sollten sie z. B. *Alle* sechs SSD haben.

   > [!NOTE]
   > Es ist in Ordnung, für die Anzahl der Laufwerke vorübergehend bei Ausfällen oder beim Hinzufügen oder Entfernen von Laufwerken zu unterscheiden.

### Modell

Wir empfehlen die Verwendung der Laufwerke des gleichen Modell und Firmwareversion wann immer möglich. Wenn dies nicht möglich ist, wählen Sie sorgfältig Laufwerke, die so ähnlich wie möglich sind. Es wird davon abgeraten mischen und Abgleich Laufwerke des gleichen Typs mit klaren unterschiedliche Leistung oder Belastung Eigenschaften (es sei denn, eine Cache ist und der andere Kapazität) da "direkte Speicherplätze" e/a gleichmäßig verteilt und nicht basierend auf Modell unterscheiden .

   > [!NOTE]
   > Es ist in Ordnung, Sortiment-ähnliche SATA- und SAS-Laufwerke.

### Size

Wir empfehlen die Verwendung von Laufwerken für unterschiedliche Größen möglichst. Kapazitätslaufwerke mit verschiedenen Größen können auftreten, einige unbrauchbar Kapazität, und mithilfe der Cache-Laufwerke mit verschiedenen Größen möglicherweise nicht Cache Leistung verbessern. Finden Sie im nächsten Abschnitt Details.

   > [!WARNING]
   > Isolierte Kapazität möglicherweise unterschiedliche Größen von Kapazität Laufwerke auf Servern.

## Zu verstehen: Kapazität Diskrepanz

"Direkte Speicherplätze" ist robust zu Kapazität Diskrepanz zwischen verschiedenen Laufwerken oder Servern. Auch wenn die Diskrepanz schwerwiegende ist, wird alles funktionieren weiterhin. Allerdings kann abhängig von verschiedenen Faktoren ab, Kapazität, die in jedem Server nicht verfügbar ist nicht verwendet werden.

Um festzustellen, warum dies geschieht, sollten Sie die vereinfachte Abbildung unten. Jede farbigen Feld stellt eine Kopie der gespiegelten Daten dar. Z. B. "die Kontrollkästchen" markiert A, A ", und ein '' sind drei Kopien der gleichen Daten. Server-Fehlertoleranz, berücksichtigt diese Kopien *müssen* auf unterschiedlichen Servern gespeichert werden.

### Isolierte Kapazität

Gezeichnet, sind Server 1 (10 TB) und Server 2 (10 TB) voll. Server 3 hat größere Laufwerke, daher ist die Gesamtkapazität größere (15 TB). Jedoch würde zum Speichern von Daten für weitere drei-Wege-Spiegelung auf Server 3 Kopien auf Server 1 und Server 2, erfordern die sind bereits voll. Die verbleibenden 5 TB Kapazität auf Server 3 nicht verwendet werden können – es ist *"isolierte"* Kapazität.

![Drei-Wege-Spiegelung, drei Servern isolierte Kapazität](media/drive-symmetry-considerations/Size-Asymmetry-3N-Stranded.png)

### Eine optimale Platzierung

Im Gegensatz dazu ab vier Servern von 10 TB, 10 TB, 10 TB und 15 TB Kapazität und drei-Wege-spiegelungsresilienz es *ist* möglich, Kopien gültig erworbene in einer Weise zu platzieren, die alle verfügbaren Kapazität, d. h. als gezeichneten verwendet. Wenn dies möglich ist, wird die "direkte Speicherplätze" Zuweisung suchen und verwenden die optimale Platzierung, wenn keine isolierte Kapazität.

![Drei-Wege-Spiegelung, vier Servern, keine isolierte Kapazität](media/drive-symmetry-considerations/Size-Asymmetry-4N-No-Stranded.png)

Die Anzahl von Servern, die resilienz, den Schweregrad der die Kapazität Diskrepanz und anderen Faktoren Einfluss darauf, ob isolierte Kapazität vorhanden ist. **Die meisten vorsichtig in der Regel ist davon ausgehen, dass nur die verfügbare Kapazität in jedem Server garantiert ist, verwendet werden.**

## Zu verstehen: Cache Diskrepanz

"Direkte Speicherplätze" ist robust zu Cache Diskrepanz zwischen verschiedenen Laufwerken oder Servern. Auch wenn die Diskrepanz schwerwiegende ist, wird alles funktionieren weiterhin. Darüber hinaus verwendet "direkte Speicherplätze" immer alle verfügbaren Cache optimal.

Allerdings mit Cache-Laufwerke mit verschiedenen Größen möglicherweise nicht Cache Leistung verbessern einheitlich oder berechenbar: nur e/a auf [laufwerksbindungen](understand-the-cache.md#server-side-architecture) mit größeren Cachelaufwerke bessere Leistung angezeigt werden. "Direkte Speicherplätze" gleichmäßig verteilt die e/a auf Bindungen und nicht basierend auf Cache-Kapazität Verhältnis zu unterscheiden.

![Cache Diskrepanz](media/drive-symmetry-considerations/Cache-Asymmetry.png)

   > [!TIP]
   > Finden Sie unter erfahren Sie mehr über Cache Bindungen [Grundlegendes zum Cache](understand-the-cache.md) .

## Beispielkonfigurationen

Hier sind einige unterstützten und nicht unterstützten Konfigurationen:

### ![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: verschiedene Modelle zwischen Servern

Die ersten zwei Server verwenden NVMe-Modell "X", aber der dritte Server verwendet NVMe-Modell "Z", die sehr ähnlich ist.

| Server 1                    | Server 2                    | Server 3                    |
|-----------------------------|-----------------------------|-----------------------------|
| 2 x NVMe-Modell X (Cache)    | 2 x NVMe-Modell X (Cache)    | 2 x NVMe-Modell Z (Cache)    |
| 10 x SSD-Modells Y (Kapazität) | 10 x SSD-Modells Y (Kapazität) | 10 x SSD-Modells Y (Kapazität) |

Dies wird unterstützt.

### ![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: verschiedene Modelle in server

Jeder Server verwendet einige andere Mischung von der HDD-Modelle "Y" und "Z", die sehr ähnlich sind. Jeder Server verfügt über 10 insgesamt HDD.

| Server 1                   | Server 2                   | Server 3                   |
|----------------------------|----------------------------|----------------------------|
| 2 x SSD-Modell X (Cache)    | 2 x SSD-Modell X (Cache)    | 2 x SSD-Modell X (Cache)    |
| 7 x HDD-Modells Y (Kapazität) | 5 x HDD-Modells Y (Kapazität) | 1 x HDD-Modells Y (Kapazität) |
| 3 x HDD Modell Z (Kapazität) | 5 x HDD Modell Z (Kapazität) | 9 x HDD Modell Z (Kapazität) |

Dies wird unterstützt.

### ![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: verschiedene Größen auf Servern

Die ersten zwei Server verwenden 4 TB HDD, aber der dritte Server sehr ähnlich 6 TB HDD verwendet.

| Server 1                | Server 2                | Server 3                |
|-------------------------|-------------------------|-------------------------|
| 2 x 800 GB NVMe (Cache) | 2 x 800 GB NVMe (Cache) | 2 x 800 GB NVMe (Cache) |
| 4 x 4 TB HDD (Kapazität) | 4 x 4 TB HDD (Kapazität) | 4 x 6 TB HDD (Kapazität) |

Dies wird unterstützt, obwohl isolierte Kapazität ausgegeben werden.

### ![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: verschiedene Größen in server

Jeder Server verwendet einige andere Mischung von 1.2 TB und sehr ähnlich 1,6 TB SSD. Jeder Server verfügt über 4 insgesamt SSD.

| Server 1                 | Server 2                 | Server 3                 |
|--------------------------|--------------------------|--------------------------|
| 3 x 1.2 TB SSD (Cache)   | 2 x 1.2 TB SSD (Cache)   | 4 x 1.2 TB SSD (Cache)   |
| 1 x 1,6 TB SSD (Cache)   | 2 x 1,6 TB SSD (Cache)   | -                        |
| 20 x 4 TB HDD (Kapazität) | 20 x 4 TB HDD (Kapazität) | 20 x 4 TB HDD (Kapazität) |

Dies wird unterstützt.

### ![nicht unterstützt](media/drive-symmetry-considerations/unsupported.png) Nicht unterstützt: verschiedenen Arten von Laufwerken auf Servern

Server 1 über NVMe verfügt, aber die anderen nicht.

| Server 1            | Server 2            | Server 3            |
|---------------------|---------------------|---------------------|
| 6 X NVMe (Cache)    | -                   | -                   |
| -                   | 6 X SSD (Cache)     | 6 X SSD (Cache)     |
| 18 X HDD (Kapazität) | 18 X HDD (Kapazität) | 18 X HDD (Kapazität) |

Dies wird nicht unterstützt. Die Arten von Laufwerken sollte in jedem Server identisch sein.

### ![nicht unterstützt](media/drive-symmetry-considerations/unsupported.png) Nicht unterstützt: andere Anzahl von jedem Typ auf Servern

Server 3 hat weitere Laufwerke als andere.

| Server 1            | Server 2            | Server 3            |
|---------------------|---------------------|---------------------|
| 2 X NVMe (Cache)    | 2 X NVMe (Cache)    | 4 X NVMe (Cache)    |
| 10 X HDD (Kapazität) | 10 X HDD (Kapazität) | 20 X HDD (Kapazität) |

Dies wird nicht unterstützt. Die Anzahl der Laufwerke von jedem Typ sollte in jedem Server identisch sein.

### ![nicht unterstützt](media/drive-symmetry-considerations/unsupported.png) Nicht unterstützt: nur HDD-Laufwerk

Alle Server haben nur HDD-Laufwerk verbunden.

|Server 1|Server 2|Server 3|
|-|-|-| 
|18 X HDD (Kapazität) |18 X HDD (Kapazität)|18 X HDD (Kapazität)|

Dies wird nicht unterstützt. Sie müssen mindestens zwei Cachelaufwerke (NvME oder SSDS) an jedem Server hinzufügen.

## Zusammenfassung

Um die Wiederholung sollten alle Server im Cluster die gleichen Arten von Laufwerken und die gleiche Anzahl von jedem Typ haben. Es wird für Sortiment-Laufwerksmodelle und Laufwerkgrößen mit den oben aufgeführten Vorschlägen bei Bedarf unterstützt.

| Einschränkung                               |               |
|------------------------------------------|---------------|
| Dieselben Typen von Laufwerken auf jedem server     | **Erforderlich**  |
| Dieselbe Anzahl der einzelnen Typen in jedem server | **Erforderlich**  |
| Gleichen Laufwerksmodelle in jedem server        | Empfohlen   |
| Dieselbe Größe in jedem server         | Empfohlen   |

## Weitere Informationen:

- [Hardwareanforderungen für „Direkte Speicherplätze“](storage-spaces-direct-hardware-requirements.md)
- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
