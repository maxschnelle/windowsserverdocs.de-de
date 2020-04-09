---
title: Überlegungen zur Laufwerk Symmetrie für direkte Speicherplätze
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: b06d69c020ea38a2fb9f23df2cfd9cd4191ae315
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857553"
---
# <a name="drive-symmetry-considerations-for-storage-spaces-direct"></a>Überlegungen zur Laufwerk Symmetrie für direkte Speicherplätze 

> Gilt für: Windows Server 2019, Windows Server 2016

[Direkte Speicherplätze](storage-spaces-direct-overview.md) funktioniert am besten, wenn jeder Server genau über die gleichen Laufwerke verfügt.

In Wirklichkeit erkennen wir, dass dies nicht immer praktikabel ist: direkte Speicherplätze ist für die Jahre entwickelt und skaliert, wenn die Anforderungen Ihres Unternehmens zunehmen. Heute können Sie geräumige 3-TB-Festplattenlaufwerke erwerben. im nächsten Jahr ist es möglicherweise unmöglich, diejenigen zu finden, die klein sind. Daher wird ein gewisser Mix-und abgleichswert unterstützt.

In diesem Thema werden die Einschränkungen erläutert und Beispiele für unterstützte und nicht unterstützte Konfigurationen bereitstellt.

## <a name="constraints"></a>Einschränkungen

### <a name="type"></a>Typ

Alle Server sollten über die gleichen [Laufwerke](choosing-drives.md#drive-types)verfügen.

Wenn ein Server beispielsweise über nvme verfügt, sollte er *alle* über nvme verfügen.

### <a name="number"></a>Number

Alle Server müssen über die gleiche Anzahl von Laufwerken für jeden Typ verfügen.

Wenn z. b. ein Server über sechs SSD verfügt, sollten *alle* über sechs SSD verfügen.

   > [!NOTE]
   > Es ist in Ordnung, dass sich die Anzahl der Laufwerke während des Ausfalls oder beim Hinzufügen oder Entfernen von Laufwerken vorübergehend unterscheiden kann.

### <a name="model"></a>Modell

Es wird empfohlen, nach Möglichkeit Laufwerke desselben Modells und einer Firmwareversion zu verwenden. Wenn dies nicht möglich ist, wählen Sie die Laufwerke aus, die so ähnlich wie möglich sind. Wir raten davon ab, mit stark unterschiedlichen Leistungs-oder Belastungs Merkmalen, bei denen es sich um eine nicht Zwischenspeicherung und die andere um Kapazität handelt, das kombinieren und Anpassen von Laufwerken desselben Typs zu unterscheiden, direkte Speicherplätze da die e/a-Vorgänge gleichmäßig

   > [!NOTE]
   > Es ist in Ordnung, ähnliche SATA-und SAS-Laufwerke zu kombinieren und zu vergleichen.

### <a name="size"></a>Größe

Es empfiehlt sich, möglichst wenige Laufwerke mit denselben Größen zu verwenden. Die Verwendung von Kapazitäts Laufwerken mit unterschiedlichen Größen kann zu einer nicht verwendbaren Kapazität führen, und die Verwendung von Cache Laufwerken mit unterschiedlichen Größen kann die Cache Leistung nicht Weitere Informationen finden Sie im nächsten Abschnitt.

   > [!WARNING]
   > Abweichende Größen von Kapazitäts Laufwerken auf Servern können zu einer nicht verstrandeten Kapazität führen.

## <a name="understand-capacity-imbalance"></a>Grundlegendes: Kapazitäts Ungleichgewicht

Direkte Speicherplätze ist robust auf Kapazitäts Ungleichgewicht Zwischenlauf Werken und Servern. Auch wenn das Ungleichgewicht schwerwiegend ist, wird alles weiterhin funktionieren. Abhängig von mehreren Faktoren ist die Kapazität, die nicht auf jedem Server verfügbar ist, jedoch möglicherweise nicht verwendbar.

Sehen Sie sich die vereinfachte Abbildung unten an, um zu ermitteln, warum dies passiert. Jedes farbige Feld stellt eine Kopie der gespiegelten Daten dar. Beispielsweise sind die Felder, die als, a ' und ' ' gekennzeichnet sind, drei Kopien der gleichen Daten. Um die Server Fehlertoleranz zu beachten, *müssen* diese Kopien auf unterschiedlichen Servern gespeichert werden.

### <a name="stranded-capacity"></a>Gestrandete Kapazität

Wie bereits gezeichnet, sind Server 1 (10 TB) und Server 2 (10 TB) voll. Server 3 weist größere Laufwerke auf, daher ist die Gesamtkapazität größer (15 TB). Zum Speichern von drei-Wege-Spiegelungs Daten auf Server 3 sind jedoch Kopien auf Server 1 und Server 2 erforderlich, die bereits voll sind. Die verbleibenden 5-TB-Kapazität auf Server 3 kann nicht verwendet werden – Sie ist *"Gestrandet"* Kapazität.

![Drei-Wege-Spiegelung, drei Server, gestrandete Kapazität](media/drive-symmetry-considerations/Size-Asymmetry-3N-Stranded.png)

### <a name="optimal-placement"></a>Optimale Platzierung

Mit vier Servern mit einer Kapazität von 10 TB, 10 TB, 10 TB und 15 TB sowie mit drei-Wege-Spiegelungs Resilienz *können Kopien* auf eine Weise ordnungsgemäß platziert werden, die die gesamte verfügbare Kapazität verwendet, wie Sie gezeichnet werden. Wenn dies möglich ist, wird die optimale Platzierung von der direkte Speicherplätze Zuweisung gefunden und verwendet, sodass keine feststehende Kapazität besteht.

![Drei-Wege-Spiegelung, vier Server, keine gestrandete Kapazität](media/drive-symmetry-considerations/Size-Asymmetry-4N-No-Stranded.png)

Die Anzahl der Server, die Resilienz, der Schweregrad des Kapazitäts ungleichseins und andere Faktoren beeinflussen, ob die Kapazität gestrandet ist. **Die umfassendste allgemeine Regel besteht darin, dass nur die in jedem Server verfügbare Kapazität verwendet werden kann.**

## <a name="understand-cache-imbalance"></a>Grundlegendes: Cache Ungleichgewicht

Direkte Speicherplätze ist robust, um das Ungleichgewicht zwischen verschiedenen Laufwerken und Servern zu Zwischenspeichern. Auch wenn das Ungleichgewicht schwerwiegend ist, wird alles weiterhin funktionieren. Außerdem verwendet direkte Speicherplätze stets den gesamten verfügbaren Cache vollständig.

Allerdings kann die Verwendung von Cache Laufwerken mit unterschiedlichen Größen die Cache Leistung nicht gleichmäßig oder vorhersag Bar verbessern: nur e/a zum [Steuern von Bindungen](understand-the-cache.md#server-side-architecture) mit größeren Cache Laufwerken kann eine bessere Leistung Direkte Speicherplätze verteilt e/a-Vorgänge gleichmäßig auf Bindungen und unterscheidet nicht basierend auf dem Verhältnis zwischen Cache und Kapazität.

![Cache Ungleichgewicht](media/drive-symmetry-considerations/Cache-Asymmetry.png)

   > [!TIP]
   > Weitere Informationen zu Cache Bindungen finden Sie Untergrund Legendes [zum Cache](understand-the-cache.md) .

## <a name="example-configurations"></a>Beispielkonfigurationen

Im folgenden finden Sie einige unterstützte und nicht unterstützte Konfigurationen:

### <a name="supported-supported-different-models-between-servers"></a>![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: verschiedene Modelle zwischen Servern

Die ersten beiden Server verwenden das nvme-Modell "X", aber der dritte Server verwendet das nvme-Modell "Z", das sehr ähnlich ist.

| Server 1                    | Server 2                    | Server 3                    |
|-----------------------------|-----------------------------|-----------------------------|
| 2 x nvme-Modell x (Cache)    | 2 x nvme-Modell x (Cache)    | 2 x nvme-Modell Z (Cache)    |
| 10 x SSD-Modell Y (Kapazität) | 10 x SSD-Modell Y (Kapazität) | 10 x SSD-Modell Y (Kapazität) |

Dies wird unterstützt.

### <a name="supported-supported-different-models-within-server"></a>![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: verschiedene Modelle innerhalb des Servers

Jeder Server verwendet eine andere Mischung aus HDD-Modellen "Y" und "Z", die sehr ähnlich sind. Jeder Server hat insgesamt 10 HDD.

| Server 1                   | Server 2                   | Server 3                   |
|----------------------------|----------------------------|----------------------------|
| 2 x SSD-Modell x (Cache)    | 2 x SSD-Modell x (Cache)    | 2 x SSD-Modell x (Cache)    |
| 7 x HDD-Modell Y (Kapazität) | 5 x HDD-Modell Y (Kapazität) | 1 x HDD-Modell Y (Kapazität) |
| 3 x HDD-Modell Z (Kapazität) | 5 x HDD-Modell Z (Kapazität) | 9 x HDD-Modell Z (Kapazität) |

Dies wird unterstützt.

### <a name="supported-supported-different-sizes-across-servers"></a>![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: verschiedene Server übergreifende Größen

Die ersten beiden Server verwenden 4 TB HDD, der dritte Server verwendet jedoch eine sehr ähnliche HDD mit 6 TB.

| Server 1                | Server 2                | Server 3                |
|-------------------------|-------------------------|-------------------------|
| 2 x 800 GB nvme (Cache) | 2 x 800 GB nvme (Cache) | 2 x 800 GB nvme (Cache) |
| 4 x 4 TB HDD (Kapazität) | 4 x 4 TB HDD (Kapazität) | 4 x 6 TB HDD (Kapazität) |

Dies wird zwar unterstützt, wird jedoch zu einer nicht mehrstufigen Kapazität.

### <a name="supported-supported-different-sizes-within-server"></a>![unterstützt](media/drive-symmetry-considerations/supported.png) Unterstützt: unterschiedliche Größen innerhalb des Servers

Jeder Server verwendet eine andere Mischung aus 1,2 TB und sehr ähnlichen 1,6 TB SSD. Jeder Server verfügt über vier SSD-SSD-gesamt.

| Server 1                 | Server 2                 | Server 3                 |
|--------------------------|--------------------------|--------------------------|
| 3 x 1,2 TB SSD (Cache)   | 2 x 1,2 TB SSD (Cache)   | 4 x 1,2 TB SSD (Cache)   |
| 1 x 1,6 TB SSD (Cache)   | 2 x 1,6 TB SSD (Cache)   | -                        |
| 20 x 4 TB HDD (Kapazität) | 20 x 4 TB HDD (Kapazität) | 20 x 4 TB HDD (Kapazität) |

Dies wird unterstützt.

### <a name="unsupported-not-supported-different-types-of-drives-across-servers"></a>![Nicht unterstützt](media/drive-symmetry-considerations/unsupported.png) Nicht unterstützt: verschiedene Arten von Laufwerken Server übergreifend

Server 1 hat nvme, die anderen aber nicht.

| Server 1            | Server 2            | Server 3            |
|---------------------|---------------------|---------------------|
| 6 x nvme (Cache)    | -                   | -                   |
| -                   | 6 x SSD (Cache)     | 6 x SSD (Cache)     |
| 18 x HDD (Kapazität) | 18 x HDD (Kapazität) | 18 x HDD (Kapazität) |

Dies wird nicht unterstützt. Die Laufwerkstypen sollten auf jedem Server identisch sein.

### <a name="unsupported-not-supported-different-number-of-each-type-across-servers"></a>![Nicht unterstützt](media/drive-symmetry-considerations/unsupported.png) Nicht unterstützt: unterschiedliche Anzahl der einzelnen Typen Server übergreifend

Server 3 verfügt über mehr Laufwerke als die anderen.

| Server 1            | Server 2            | Server 3            |
|---------------------|---------------------|---------------------|
| 2 x nvme (Cache)    | 2 x nvme (Cache)    | 4 x nvme (Cache)    |
| 10 x HDD (Kapazität) | 10 x HDD (Kapazität) | 20 x HDD (Kapazität) |

Dies wird nicht unterstützt. Die Anzahl der Laufwerke der einzelnen Typen sollte auf jedem Server identisch sein.

### <a name="unsupported-not-supported-only-hdd-drives"></a>![Nicht unterstützt](media/drive-symmetry-considerations/unsupported.png) Nicht unterstützt: nur HDD-Laufwerke

Auf allen Servern sind nur HDD-Laufwerke verbunden.

|Server 1|Server 2|Server 3|
|-|-|-| 
|18 x HDD (Kapazität) |18 x HDD (Kapazität)|18 x HDD (Kapazität)|

Dies wird nicht unterstützt. Sie müssen mindestens zwei Cache Laufwerke (nvme oder SSD) hinzufügen, die an jeden Server angeschlossen sind.

## <a name="summary"></a>Zusammenfassung

Zur Wiederholung sollte jeder Server im Cluster die gleichen Laufwerke und die gleiche Anzahl der einzelnen Typen aufweisen. Die Kombination von Laufwerk Modellen und Laufwerk Größen nach Bedarf wird mit den oben beschriebenen Überlegungen unterstützt.

| Einschränkung                               |               |
|------------------------------------------|---------------|
| Die gleichen Laufwerkstypen auf jedem Server     | **Erforderlich**  |
| Die gleiche Anzahl der einzelnen Typen auf jedem Server | **Erforderlich**  |
| Die gleichen Laufwerks Modelle in jedem Server        | Empfohlen   |
| Die gleichen Laufwerk Größen auf jedem Server         | Empfohlen   |

## <a name="see-also"></a>Siehe auch

- [Direkte Speicherplätze Hardwareanforderungen](storage-spaces-direct-hardware-requirements.md)
- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
