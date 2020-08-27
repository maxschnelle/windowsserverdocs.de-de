---
ms.assetid: de054ac2-a386-43ec-a537-c0de21549741
title: Festlegen von Standortverknüpfungseigenschaften
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 391427a293aa83057d6850caec0acc297be426e5
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88938420"
---
# <a name="setting-site-link-properties"></a>Festlegen von Standortverknüpfungseigenschaften

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die standortübergreifende Replikation erfolgt gemäß den Eigenschaften der Verbindungs Objekte. Wenn die Konsistenzprüfung (KCC) Verbindungs Objekte erstellt, leitet Sie den Replikations Zeitplan von den Eigenschaften der Standort Verknüpfungs Objekte ab. Jedes Standort Verknüpfungs Objekt stellt die WAN-Verbindung (Wide Area Network) zwischen zwei oder mehr Standorten dar.

Das Festlegen der Eigenschaften von Standort Verknüpfungs Objekten umfasst die folgenden Schritte:

-   Ermitteln der Kosten, die mit diesem Replikations Pfad verknüpft sind. Die KCC verwendet die Kosten, um die kostengünstigste Route für die Replikation zwischen zwei Standorten zu ermitteln, die dieselbe Verzeichnis Partition replizieren.

-   Festlegen des Zeitplans, der die Zeiten definiert, in denen die Replikation Zwischenstand Orten erfolgen kann.

-   Festlegen des Replikations Intervalls, das definiert, wie häufig die Replikation während der zulässigen Replikation erfolgen soll, wie im Zeitplan definiert.

## <a name="in-this-guide"></a>Inhalt dieser Anleitung

-   [Bestimmen der Kosten](../../ad-ds/plan/Determining-the-Cost.md)

-   [Bestimmen des Zeitplans](../../ad-ds/plan/Determining-the-Schedule.md)

-   [Bestimmen des Intervalls](../../ad-ds/plan/Determining-the-Interval.md)



