---
title: Wiederherstellungs Momentaufnahmen sollten nach dem Failover entfernt werden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 922115fa-e8dd-4055-aaf1-4a4437c5cf28
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: c995293ca67b4cad0837affa854fb4ac366856e1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861843"
---
# <a name="recovery-snapshots-should-be-removed-after-failover"></a>Wiederherstellungs Momentaufnahmen sollten nach dem Failover entfernt werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016| 
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Vorgänge|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Für einen virtuellen Computer, für den ein Failover ausgeführt wurde, ist mindestens ein Wiederherstellungs*  
  
## <a name="impact"></a>**Auswirkt**  
*Der verfügbare Speicherplatz kann auf dem physischen Datenträger, auf dem die Momentaufnahme Dateien gespeichert werden In diesem Fall können keine weiteren Datenträger Vorgänge für den physischen Speicher ausgeführt werden. Jeder virtuelle Computer, der auf dem physischen Speicher basiert, kann beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie für jeden virtuellen Computer, für den ein Failover ausgeführt wurde, das Complete-vmfailover-Cmdlet in Windows PowerShell, um die Wiederherstellungs Momentaufnahmen zu entfernen und die Failover*  
  


