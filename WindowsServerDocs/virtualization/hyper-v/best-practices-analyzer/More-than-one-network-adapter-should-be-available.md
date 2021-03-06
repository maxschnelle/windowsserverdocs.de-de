---
title: Es sollten mehrere Netzwerkadapter verfügbar sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
ms.date: 8/16/2016
ms.openlocfilehash: 05dc0583424ed155c4780f9f0b4c016be850a71c
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746265"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>Es sollten mehrere Netzwerkadapter verfügbar sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Dieser Server ist mit einem Netzwerkadapter konfiguriert, der vom Verwaltungs Betriebssystem und allen virtuellen Computern gemeinsam genutzt werden muss, die Zugriff auf ein physisches Netzwerk benötigen.*

## <a name="impact"></a>Auswirkung

*Die Netzwerkleistung kann im Verwaltungs Betriebssystem beeinträchtigt werden.*

## <a name="resolution"></a>Lösung

*Fügen Sie diesem Computer weitere Netzwerkadapter hinzu. Um einen Netzwerkadapter für die ausschließliche Verwendung durch das Verwaltungs Betriebssystem zu reservieren, sollten Sie ihn nicht für die Verwendung mit einem externen virtuellen Netzwerk konfigurieren.*

Weitere Informationen zum Hinzufügen eines Netzwerkadapters zum Computer finden Sie in der Dokumentation für den Computer oder den Netzwerkadapter. Um es dann ausschließlich für das Verwaltungs Betriebssystem zu reservieren, verbinden Sie es nicht mit einem virtuellen Switch.



