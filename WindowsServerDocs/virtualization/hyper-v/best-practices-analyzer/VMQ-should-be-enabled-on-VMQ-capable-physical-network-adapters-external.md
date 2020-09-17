---
title: VMQ sollte auf VMQ-fähigen physischen Netzwerkadaptern aktiviert werden, die an einen externen virtuellen Switch gebunden sind.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 93d1b155-bf44-46b0-bb69-d34d5b30e574
ms.date: 8/16/2016
ms.openlocfilehash: 169f2ea06bf35c7bbc9bcaec354ca66e118c75d2
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746765"
---
# <a name="vmq-should-be-enabled-on-vmq-capable-physical-network-adapters-bound-to-an-external-virtual-switch"></a>VMQ sollte auf VMQ-fähigen physischen Netzwerkadaptern aktiviert werden, die an einen externen virtuellen Switch gebunden sind.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Die folgenden Netzwerkadapter können eine Warteschlange für virtuelle Maschinen (Virtual Machine Queue, VMQ) haben, die Funktion ist jedoch deaktiviert.*

## <a name="impact"></a>**Auswirkungen**
*Die verfügbaren Hardware Abladungen auf den folgenden Netzwerkadaptern können von Windows nicht voll ausgenutzt werden:*

\<list of network adapters>

## <a name="resolution"></a>**Lösung**
*Aktivieren Sie VMQ mithilfe des Windows PowerShell-Cmdlets Enable-netadaptervmq oder mithilfe der Benutzeroberfläche Erweiterte Eigenschaften für den Netzwerkadapter.*



