---
title: Virtuelle Festplatten mit Auslagerungs Dateien sollten von der Replikation ausgeschlossen werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: c0be8a5f-64a1-488a-944e-bb913bb90517
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 94e03cf9de3991d003fad9019b9af33fad2f6bae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855023"
---
# <a name="virtual-hard-disks-with-paging-files-should-be-excluded-from-replication"></a>Virtuelle Festplatten mit Auslagerungs Dateien sollten von der Replikation ausgeschlossen werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Information|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Auslagerungs Dateien sollten von der Teilnahme an der Replikation ausgeschlossen werden, aber es wurden keine Datenträger ausgeschlossen.*  
  
## <a name="impact"></a>Auswirkungen  
*Beim auslagern von Dateien kommt es zu einer hohen Menge an Eingabe-/Ausgabeaktivität, bei der unnötigerweise weniger Ressourcen für die Replikation erforderlich sind. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Wenn Sie dies nicht bereits getan haben, erstellen Sie eine separate virtuelle Festplatte für die Windows-Auslagerungs Datei. Wenn die anfängliche Replikation bereits abgeschlossen ist, entfernen Sie die Replikation mit dem Hyper-V-Manager. Konfigurieren Sie dann die Replikation erneut, und schließen Sie die virtuelle Festplatte mit der Auslagerungs Datei von der Replikation aus.*  
  


