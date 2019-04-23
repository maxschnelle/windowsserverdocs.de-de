---
title: Aktivieren Sie die Storage Quality of Service, wenn Sie eine differenzierende virtuelle Festplatte verwenden, wenn die übergeordneten und untergeordneten virtuellen Festplatten auf unterschiedlichen Volumes befinden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2bdc8462c4d9dc50dbb69792f2f294add0ca3a74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856201"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>Aktivieren Sie die Storage Quality of Service, wenn Sie eine differenzierende virtuelle Festplatte verwenden, wenn die übergeordneten und untergeordneten virtuellen Festplatten auf unterschiedlichen Volumes befinden

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
*Eine differenzierende virtuelle Festplatte mit dem übergeordneten und untergeordneten virtuellen Festplatten auf unterschiedlichen Volumes verfügt über Storage Quality of Service aktiviert.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Diese Konfiguration kann zu unerwarteten Storage Quality of Service-Verhalten für die differenzierende virtuelle Festplatte als auch von anderen virtuellen Festplatten auf den übergeordneten und untergeordneten Volumes führen. Dies wirkt sich auf die folgenden virtuellen Festplatten:*  
  
\<Liste der virtuellen Festplatten >  
  
## <a name="resolution"></a>**Lösung**  
*Storage Quality of Service für die virtuellen Festplatten auf die verwiesen wird, deaktivieren oder eine Speichermigration zum Verschieben von übergeordneten und untergeordneten virtuellen Festplatte auf dem gleichen Volume durchführen.*  
  


