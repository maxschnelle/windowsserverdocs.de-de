---
title: Eine neusynchronisierung der Replikation sollte für Zeiten geplant werden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2d6c18b7e37c5d17f56f41c7ff03ed8796457de0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840021"
---
# <a name="resynchronization-of-replication-should-be-scheduled-for-off-peak-hours"></a>Eine neusynchronisierung der Replikation sollte für Zeiten geplant werden

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Eine neusynchronisierung der Replikation für den primären virtuellen Computern ist nicht für Zeiten geplant werden.*  
  
## <a name="impact"></a>Auswirkungen  
*Je länger ein virtueller Computer befindet sich in einem Zustand, erfordern eine neusynchronisierung, je länger die Replikation Protokolldateien anwachsen, und die mehr nicht replizierten Änderungen, die auf dem primären virtuellen Computer auftreten. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie Hyper-V-Manager, um die replikationseinstellungen für den virtuellen Computer zum Ausführen der neusynchronisierung automatisch außerhalb der Spitzenzeiten zu ändern.*  
  


