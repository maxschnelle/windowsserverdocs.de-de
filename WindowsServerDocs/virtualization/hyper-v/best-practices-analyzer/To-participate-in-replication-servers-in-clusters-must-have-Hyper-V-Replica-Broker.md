---
title: Für Server in Failoverclustern muss ein Hyper-V-Replikat Broker konfiguriert sein.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
ms.date: 8/16/2016
ms.openlocfilehash: 7fdd6167561be4922540a0def1f91f70b519aa0f
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746125"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>Für Server in Failoverclustern muss ein Hyper-V-Replikat Broker konfiguriert sein.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Für Failovercluster erfordert das Hyper-v-Replikat die Verwendung eines Hyper-v-Replikat Broker-namens anstelle eines einzelnen Server namens.*

## <a name="impact"></a>Auswirkung
*Wenn die virtuelle Maschine auf einen anderen Failoverclusterknoten verschoben wird, kann die Replikation nicht fortgesetzt werden.*

## <a name="resolution"></a>Lösung
*Verwenden Sie Failovercluster-Manager zum Konfigurieren des Hyper-V-Replikat Brokers. Stellen Sie im Hyper-v-Manager sicher, dass die Replikationskonfiguration den Namen des Hyper-v-Replikat Brokers als Servernamen verwendet.*



