---
title: VMQ sollte auf VMQ-fähigen physischen Netzwerkadaptern aktiviert werden, die an einen externen virtuellen Switch gebunden sind.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 93d1b155-bf44-46b0-bb69-d34d5b30e574
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: a66c1c4580f8ecda90caa5446e74bc9b12ac0476
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855043"
---
# <a name="vmq-should-be-enabled-on-vmq-capable-physical-network-adapters-bound-to-an-external-virtual-switch"></a>VMQ sollte auf VMQ-fähigen physischen Netzwerkadaptern aktiviert werden, die an einen externen virtuellen Switch gebunden sind.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Die folgenden Netzwerkadapter können eine Warteschlange für virtuelle Maschinen (Virtual Machine Queue, VMQ) haben, die Funktion ist jedoch deaktiviert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Die verfügbaren Hardware Abladungen auf den folgenden Netzwerkadaptern können von Windows nicht voll ausgenutzt werden:*  
  
\<Liste der Netzwerkadapter >  
  
## <a name="resolution"></a>**Lösung**  
*Aktivieren Sie VMQ mithilfe des Windows PowerShell-Cmdlets Enable-netadaptervmq oder mithilfe der Benutzeroberfläche Erweiterte Eigenschaften für den Netzwerkadapter.*  
  


