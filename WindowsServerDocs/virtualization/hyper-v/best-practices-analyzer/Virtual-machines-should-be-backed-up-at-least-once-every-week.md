---
title: Virtuelle Computer sollten mindestens einmal pro Woche gesichert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 6cb425f92926aa1823ed89cd26afccc2d962603d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855033"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>Virtuelle Computer sollten mindestens einmal pro Woche gesichert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Mindestens eine virtuelle Maschine wurde in der letzten Woche nicht gesichert.*  
  
## <a name="impact"></a>Auswirkungen  
*Ein erheblicher Datenverlust kann auftreten, wenn auf dem virtuellen Computer ein Problem auftritt und keine aktuelle Sicherung vorhanden ist. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Planen Sie eine Sicherung der virtuellen Computer so, dass Sie mindestens einmal pro Woche ausgeführt wird. Sie können diese Regel ignorieren, wenn diese virtuelle Maschine ein Replikat ist und der primäre virtuelle Computer gesichert wird, oder wenn dies der primäre virtuelle Computer ist und das zugehörige Replikat gesichert wird.*  
  


