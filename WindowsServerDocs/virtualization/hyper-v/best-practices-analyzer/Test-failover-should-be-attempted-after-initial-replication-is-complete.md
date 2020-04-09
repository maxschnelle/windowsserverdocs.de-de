---
title: Das Test Failover sollte nach Abschluss der ersten Replikation versucht werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cea7eeaa-c1a7-4f87-89be-d4e1208c546f
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 41d96b33c686631f57cd35e76b64ee3dde206655
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858943"
---
# <a name="test-failover-should-be-attempted-after-initial-replication-is-complete"></a>Das Test Failover sollte nach Abschluss der ersten Replikation versucht werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="problem"></a>Problem  
*Es gab in mindestens einem Monat kein Test Failover.*  
  
## <a name="impact"></a>Auswirkungen  
*Es gibt keine Bestätigung, dass ein geplantes oder ungeplantes Failover erfolgreich ist oder Arbeits Auslastungs Vorgänge nach einem Failover ordnungsgemäß fortgesetzt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Hyper-V-Manager, um ein Test Failover durchzuführen.*  
  


