---
ms.assetid: 96a6749c-6c9f-4f2f-ad0a-51272d282ace
title: Bestimmen des Intervalls
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 8230dc9e53184792e91874b1a8b7a44643564999
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939390"
---
# <a name="determining-the-interval"></a>Bestimmen des Intervalls

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie müssen die Eigenschaft Standort Verknüpfungs Replikations Intervall festlegen, um anzugeben, wie häufig die Replikation während der Zeiten erfolgen soll, zu denen der Zeitplan die Replikation zulässt. Wenn der Zeitplan z. b. die Replikation zwischen 02:00 Stunden und 04:00 Stunden zulässt und das Replikations Intervall für 30 Minuten festgelegt ist, kann die Replikation während der geplanten Zeit bis zu vier Mal erfolgen. Das Standard Replikations Intervall beträgt 180 Minuten oder 3 Stunden. Das Mindestintervall beträgt 15 Minuten.

Beachten Sie die folgenden Kriterien, um zu bestimmen, wie oft die Replikation innerhalb des Zeit Plan Fensters erfolgt:

-   Ein kleines Intervall verringert die Latenz und erhöht den WAN-Datenverkehr (Wide Area Network).

-   Um Domänen Verzeichnis Partitionen auf dem neuesten Stand zu halten, wird geringe Latenz bevorzugt.

Bei einer Strategie für die Speicher-und vorwärts Replikation ist es schwierig zu bestimmen, wie lange ein Verzeichnis Update auf jeden Domänen Controller repliziert werden kann. Führen Sie die folgenden Aufgaben aus, um eine konservative Schätzung der maximalen Latenzzeit bereitzustellen:

-   Erstellen Sie eine Tabelle aller Websites in Ihrem Netzwerk, wie im folgenden Beispiel gezeigt:

    |Standorte|Seattle|Boston|Los Angeles|New York|Washington, D.C.|
    |---------|-----------|----------|---------------|------------|--------------------|
    |Seattle|0,25|||||
    |Boston||0,25||||
    |Los Angeles|||0,25|||
    |New York||||0,25||
    |Washington, D.C.|||||0,25|

    Die Latenzzeit des ungünstigsten Falls innerhalb eines Standorts beträgt 15 Minuten.

-   Bestimmen Sie anhand des Replikations Zeitplans die maximale Replikations Wartezeit, die für eine beliebige Standort Verknüpfung möglich ist, die zwei Hub-Standorte verbindet.

    Wenn die Replikation z. b. alle drei Stunden zwischen Seattle und New York erfolgt, beträgt die maximale Verzögerung für die Replikation zwischen diesen Standorten drei Stunden. Wenn die Replikations Verzögerung zwischen New York und Seattle die längste geplante Verzögerung zwischen allen Hub-Standorten ist, beträgt die maximale Latenz zwischen allen Hubs drei Stunden.

-   Erstellen Sie für jede Hub-Site eine Tabelle mit den maximalen Latenzzeiten zwischen dem Hub-Standort und seinen Satellitenstandorten.

    Wenn beispielsweise die Replikation zwischen New York und Washington, D.C. alle vier Stunden erfolgt und dies die längste Replikations Verzögerung zwischen New York und seinen Satellitenstandorten ist, beträgt die maximale Latenz zwischen New York und seinen Satelliten vier Stunden.

-   Kombinieren Sie diese maximalen Latenzzeiten, um die maximale Wartezeit für das gesamte Netzwerk zu ermitteln.

    Wenn beispielsweise die maximale Latenz zwischen Seattle und der Satelliten Site in Los Angeles ein Tag ist, die maximale Replikations Wartezeit für diese Gruppe von Verknüpfungen (Washington, D.C.-New York-Seattle-Los Angeles) beträgt 31 Stunden, d. h. 4 (Washington, D.C.-New York) + 3 (New York-Seattle) + 24 (Seattle-Los Angeles), wie in der folgenden Tabelle gezeigt.

    |Standorte|Seattle|Boston|Los Angeles|New York|Washington, D.C.|
    |---------|-----------|----------|---------------|------------|--------------------|
    |Seattle|0,25|4 + 3|24,00|3.00|4 + 3|
    |Boston||0,25|4 + 3 + 24|4.00|4.00|
    |Los Angeles|||0,25|24 + 3|24 + 3 + 4|
    |New York||||0,25|4.00|
    |Washington, D.C.|||||0,25|



