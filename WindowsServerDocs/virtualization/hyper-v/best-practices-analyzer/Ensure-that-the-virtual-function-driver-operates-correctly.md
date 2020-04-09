---
title: Stellen Sie sicher, dass der virtuelle Funktions Treiber ordnungsgemäß funktioniert, wenn ein virtueller Computer für die Verwendung von SR-IOV konfiguriert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 282187d4d5a1243a14c3a0bdaa3088fe1f134bef
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861923"
---
# <a name="ensure-that-the-virtual-function-driver-operates-correctly-when-a-virtual-machine-is-configured-to-use-sr-iov"></a>Stellen Sie sicher, dass der virtuelle Funktions Treiber ordnungsgemäß funktioniert, wenn ein virtueller Computer für die Verwendung von SR-IOV konfiguriert ist.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Der Treiber für virtuelle Funktionen wird im Gast Betriebssystem von mindestens einer virtuellen Maschine nicht ordnungsgemäß ausgeführt.*  
  
## <a name="impact"></a>Auswirkungen  
*Die Netzwerkleistung ist auf den folgenden virtuellen Computern nicht optimal:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Gehen Sie im Gast Betriebssystem wie folgt vor: Überprüfen Sie, ob die entsprechenden Treiber installiert sind und alle Netzwerkgeräte aktiviert sind, und überprüfen Sie das Ereignisprotokoll auf Fehler oder Warnungen.*  
  


