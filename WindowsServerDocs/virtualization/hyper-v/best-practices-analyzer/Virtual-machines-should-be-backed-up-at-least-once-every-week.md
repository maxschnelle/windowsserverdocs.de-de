---
title: Virtuelle Computer sollte mindestens einmal pro Woche gesichert werden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e079e3cb225ec9c712233bbf3efc85bb6f09b218
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826751"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>Virtuelle Computer sollte mindestens einmal pro Woche gesichert werden

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Eine oder mehrere virtuelle Computer wurden nicht in der letzten Woche gesichert.*  
  
## <a name="impact"></a>Auswirkungen  
*Wichtige Daten verloren gehen kann auftreten, wenn es sich bei dem virtuellen Computer ein Fehler auftritt, und eine aktuelle Sicherung ist nicht vorhanden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Planen Sie eine Sicherung der virtuellen Computer mindestens einmal pro Woche ausgeführt. Sie können mit dieser Regel ignorieren, wenn der primäre virtuelle Computer gesichert wird und dieser virtuelle Computer ist ein Replikat oder, wenn dies der primäre virtuelle Computer und dessen Replikat ist, die gesichert werden.*  
  


