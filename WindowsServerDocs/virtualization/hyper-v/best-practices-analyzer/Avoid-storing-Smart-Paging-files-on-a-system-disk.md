---
title: Vermeiden der Speicherung von Smart Paging-Dateien auf einem Systemdatenträger
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9b57c9b8-76c5-43c7-bfa6-2c95b3cb6510
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6abc84b406de7e7c33628ccee4e3af706efe5c70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886171"
---
# <a name="avoid-storing-smart-paging-files-on-a-system-disk"></a>Vermeiden der Speicherung von Smart Paging-Dateien auf einem Systemdatenträger

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt Text erscheint in der Best Practices Analyzer-Tool zur Lösung dieses Problems Kursivdruck an.  
  
## <a name="issue"></a>Problem  
*Die Speicherkonfiguration für einen oder mehrere virtuelle Computer möglicherweise die Verwendung von Smart Paging, wenn der virtuelle Computer neu gestartet wird und der angegebenen Position für die Smart Paging-Datei den Systemdatenträger des Servers mit Hyper-V.*  
  
## <a name="impact"></a>Auswirkungen  
*Verwendung von den Systemdatenträger für Smart Paging kann es sich um den Server mit Hyper-V zu Problemen führen. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Konfigurieren Sie die virtuellen Computer, um die Smart Paging-Dateien auf einem nicht-System-Datenträger zu speichern.*  
  


