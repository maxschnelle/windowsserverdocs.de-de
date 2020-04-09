---
title: Mindestens ein Netzwerkadapter muss als Quelle für die Port Spiegelung konfiguriert werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 147fd00f-1440-44d1-94e3-3a8af63aa7ed
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b2beb64629f95b04ddf1fa3f43634759899554c5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861863"
---
# <a name="one-or-more-network-adapters-should-be-configured-as-the-source-for-port-mirroring"></a>Mindestens ein Netzwerkadapter muss als Quelle für die Port Spiegelung konfiguriert werden.

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
*Für mindestens einen virtuellen Computer ist ein Netzwerkadapter als Ziel für die Port Spiegelung konfiguriert, aber es ist keine entsprechende Quelle auf dem virtuellen Switch vorhanden.*  
  
## <a name="impact"></a>**Auswirkt**  
*Die Port Spiegelung wird für die folgenden virtuellen Switches und virtuellen Maschinen nicht ordnungsgemäß ausgeführt:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie Windows PowerShell oder Hyper-V-Manager, um die Port Spiegelungs Konfiguration abzuschließen oder zu korrigieren.*  
  


