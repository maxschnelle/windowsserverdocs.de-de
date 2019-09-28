---
title: Stellen Sie sicher, dass der virtuelle Funktions Treiber ordnungsgemäß funktioniert, wenn ein virtueller Computer für die Verwendung von SR-IOV konfiguriert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5e2c666973aa1ac0d5eb2c4e0d5d29793dc0ce75
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393617"
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
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>Auflösung  
Führen Sie *im Gast Betriebssystem die folgenden Schritte aus: Vergewissern Sie sich, dass die entsprechenden Treiber installiert sind und alle Netzwerkgeräte aktiviert sind, und überprüfen Sie das Ereignisprotokoll auf Fehler oder Warnungen.*  
  


