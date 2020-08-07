---
title: Es sollten mehrere Netzwerkadapter verfügbar sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 57abcbbc796ab2664d30ca9ff63c1e41f47c17a4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950244"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>Es sollten mehrere Netzwerkadapter verfügbar sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Dieser Server ist mit einem Netzwerkadapter konfiguriert, der vom Verwaltungs Betriebssystem und allen virtuellen Computern gemeinsam genutzt werden muss, die Zugriff auf ein physisches Netzwerk benötigen.*

## <a name="impact"></a>Auswirkung

*Die Netzwerkleistung kann im Verwaltungs Betriebssystem beeinträchtigt werden.*

## <a name="resolution"></a>Lösung

*Fügen Sie diesem Computer weitere Netzwerkadapter hinzu. Um einen Netzwerkadapter für die ausschließliche Verwendung durch das Verwaltungs Betriebssystem zu reservieren, sollten Sie ihn nicht für die Verwendung mit einem externen virtuellen Netzwerk konfigurieren.*

Weitere Informationen zum Hinzufügen eines Netzwerkadapters zum Computer finden Sie in der Dokumentation für den Computer oder den Netzwerkadapter. Um es dann ausschließlich für das Verwaltungs Betriebssystem zu reservieren, verbinden Sie es nicht mit einem virtuellen Switch.



