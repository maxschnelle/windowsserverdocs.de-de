---
title: Eine oder mehrere Netzwerkadapter sollte als Quelle für die Portspiegelung konfiguriert werden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 147fd00f-1440-44d1-94e3-3a8af63aa7ed
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0843c1f302b96d334e8d6649ac5503bbe2b12d02
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831791"
---
# <a name="one-or-more-network-adapters-should-be-configured-as-the-source-for-port-mirroring"></a>Eine oder mehrere Netzwerkadapter sollte als Quelle für die Portspiegelung konfiguriert werden

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Eine oder mehrere virtuelle Computer einen Netzwerkadapter, der als Ziel für die Portspiegelung konfiguriert, es ist jedoch keine entsprechenden Quelle auf dem virtuellen Switch.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Port-Datenbankspiegelung wird für die folgenden virtuellen Switches und virtuelle Computer nicht ordnungsgemäß funktioniert:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie Windows PowerShell oder dem Hyper-V-Manager, um abzuschließen, oder korrigieren Sie die Konfiguration mit Portspiegelung.*  
  


