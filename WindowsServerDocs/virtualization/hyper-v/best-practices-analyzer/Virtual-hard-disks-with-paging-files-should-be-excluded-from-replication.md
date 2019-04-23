---
title: Virtueller Festplatten mit Auslagerungsdateien sollte von der Replikation ausgeschlossen werden
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: c0be8a5f-64a1-488a-944e-bb913bb90517
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8b6289a82c83f3dcfc0de299250ce19ee3782678
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850121"
---
# <a name="virtual-hard-disks-with-paging-files-should-be-excluded-from-replication"></a>Virtueller Festplatten mit Auslagerungsdateien sollte von der Replikation ausgeschlossen werden

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Informationen|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Paging-Dateien sollten aus der Einbeziehung in der Replikation ausgeschlossen werden, aber keine Datenträger wurden ausgeschlossen.*  
  
## <a name="impact"></a>Auswirkungen  
*Paging-Dateien auftreten, eine große Anzahl von e/a-Aktivität, die unnötig viel größere Ressourcen zur Teilnahme an Replikation benötigen. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Wenn Sie nicht bereits geschehen, erstellen Sie eine separate virtuelle Festplatte für die Windows-Auslagerungsdatei. Wenn die Erstreplikation bereits abgeschlossen wurde, verwenden Sie Hyper-V-Manager zum Entfernen der Replikation. Anschließend konfigurieren Sie die Replikation erneut aus, und schließen Sie die virtuelle Festplatte mit der Auslagerungsdatei von der Replikation aus.*  
  


