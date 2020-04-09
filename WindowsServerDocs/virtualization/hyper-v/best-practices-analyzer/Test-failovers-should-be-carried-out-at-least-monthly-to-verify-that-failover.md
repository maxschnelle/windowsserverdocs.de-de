---
title: Test Failover sollten mindestens monatlich durchgeführt werden, um zu überprüfen, ob das Failover erfolgreich ist und die Arbeits Auslastungen virtueller Computer nach dem Failover erwartungsgemäß ausgeführt werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 57a8aa50-e59e-4a4b-8571-1099d5a8eee4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: f99ccfe065015d1731978ba5e7f31c766c343efc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858933"
---
# <a name="test-failovers-should-be-carried-out-at-least-monthly-to-verify-that-failover-will-succeed-and-that-virtual-machine-workloads-will-operate-as-expected-after-failover"></a>Test Failover sollten mindestens monatlich durchgeführt werden, um zu überprüfen, ob das Failover erfolgreich ist und die Arbeits Auslastungen virtueller Computer nach dem Failover erwartungsgemäß ausgeführt werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016| 
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Es gab in mindestens einem Monat kein Test Failover.*  
  
## <a name="impact"></a>Auswirkungen  
*Es gibt keine Bestätigung, dass ein geplantes oder ungeplantes Failover erfolgreich ist oder Arbeits Auslastungs Vorgänge nach einem Failover ordnungsgemäß fortgesetzt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Hyper-V-Manager, um ein Test Failover durchzuführen.*  
  


