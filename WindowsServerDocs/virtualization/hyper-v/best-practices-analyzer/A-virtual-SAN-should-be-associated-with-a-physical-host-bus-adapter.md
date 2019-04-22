---
title: Ein virtuellen SAN muss einen physischen Hostbusadapter zugeordnet werden.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 14bca69b-e779-4e90-b5c1-1b015625572f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3b9ca1e2da1cf9f4410f465fe95c6cc9c0b07ffc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819081"
---
# <a name="a-virtual-san-should-be-associated-with-a-physical-host-bus-adapter"></a>Ein virtuellen SAN muss einen physischen Hostbusadapter zugeordnet werden.

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
*Ein virtuelles Storage Area Network (SAN) wurde ohne eine Zuordnung zu einem Hostbusadapter (HBA) konfiguriert.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Ein virtuellen Computer nicht gestartet werden, bei Konfiguration mit einem virtuellen Fibre Channel-Adapter mit einem falsch konfigurierten virtuellen SAN verbunden. Dies wirkt sich auf die folgenden virtuellen SANs aus:*  
  
  
\<Liste der virtuellen SANs >  
  
  
## <a name="resolution"></a>**Lösung**  
*Konfigurieren Sie virtuellen SAN an einen Hostbusadapter anschließen.*  
  
  
  


