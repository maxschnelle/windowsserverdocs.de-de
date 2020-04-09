---
title: Vermeiden der Speicherung intelligenter Auslagerungs Dateien auf einem System Datenträger
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9b57c9b8-76c5-43c7-bfa6-2c95b3cb6510
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 111cf3b3b95f50d6d36a6b30b5a0bb46e255ee28
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857733"
---
# <a name="avoid-storing-smart-paging-files-on-a-system-disk"></a>Vermeiden der Speicherung intelligenter Auslagerungs Dateien auf einem System Datenträger

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt Kursiv Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Die Speicherkonfiguration für einen oder mehrere virtuelle Computer erfordert möglicherweise die Verwendung von Smart Paging, wenn der virtuelle Computer neu gestartet wird, und der angegebene Speicherort für die Smart Paging-Datei ist der System Datenträger des Servers, auf dem Hyper-V ausgeführt wird.*  
  
## <a name="impact"></a>Auswirkungen  
*Die Verwendung des System Datenträgers für intelligentes Paging kann dazu führen, dass auf dem Server mit Hyper-V Probleme auftreten. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Konfigurieren Sie die virtuellen Computer neu, um die Smart Paging-Dateien auf einem nicht-System Datenträger zu speichern.*  
  


