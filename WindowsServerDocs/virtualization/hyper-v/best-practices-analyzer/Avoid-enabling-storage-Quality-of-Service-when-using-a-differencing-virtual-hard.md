---
title: Aktivieren Sie Speicher Quality of Service nicht, wenn Sie eine differenzierende virtuelle Festplatte verwenden, wenn sich die übergeordneten und untergeordneten virtuellen Festplatten auf unterschiedlichen Volumes befinden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 716a32de2f9327e5eca38c470fa1b7c44150e9cb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366438"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>Aktivieren Sie Speicher Quality of Service nicht, wenn Sie eine differenzierende virtuelle Festplatte verwenden, wenn sich die übergeordneten und untergeordneten virtuellen Festplatten auf unterschiedlichen Volumes befinden.

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
*Für eine differenzierende virtuelle Festplatte mit der übergeordneten und der untergeordneten virtuellen Festplatte auf unterschiedlichen Volumes ist Storage Quality of Service aktiviert.*  
  
## <a name="impact"></a>**Auswirkt**  
*diese Konfiguration kann zu unerwartetem Speicher Quality of Service Verhalten für die differenzierende virtuelle Festplatte und andere virtuelle Festplatten auf den übergeordneten und untergeordneten Volumes führen. Dies wirkt sich auf folgende virtuelle Festplatten aus:*  
  
\<liste der virtuellen Festplatten >  
  
## <a name="resolution"></a>**Auflösung**  
*Deaktivieren Sie Speicher Quality of Service auf den virtuellen Festplatten, auf die verwiesen wird, oder führen Sie eine Speicher Migration aus, um die übergeordnete und die untergeordnete virtuelle Festplatte auf dasselbe Volume zu verschieben.*  
  


