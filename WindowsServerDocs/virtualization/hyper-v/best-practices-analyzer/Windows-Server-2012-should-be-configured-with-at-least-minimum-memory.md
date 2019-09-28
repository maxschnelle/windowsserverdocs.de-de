---
title: Windows Server 2012 sollte mit mindestens der Mindestmenge an Arbeitsspeicher konfiguriert werden.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: f218a7c7-4361-45f1-835c-e19761b2565c
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 31d82d680ec77e61821da36d76fd2febe2876c43
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393097"
---
# <a name="windows-server-2012-should-be-configured-with-at-least-the-minimum-amount-of-memory"></a>Windows Server 2012 sollte mit mindestens der Mindestmenge an Arbeitsspeicher konfiguriert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Ein virtueller Computer, auf dem Windows Server 2012 ausgeführt wird, ist mit einer geringeren Anzahl von RAM (512 MB) konfiguriert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Das Gast Betriebssystem auf den folgenden virtuellen Computern wird möglicherweise nicht ausgeführt oder kann nicht zuverlässig ausgeführt werden:*  
  
\<list of Virtual Machines >  
  
## <a name="resolution"></a>**Auflösung**  
*Verwenden Sie den Hyper-V-Manager, um den Arbeitsspeicher, der diesem virtuellen Computer zugeordnet ist, auf mindestens 512 MB zu erhöhen.*  
  
### <a name="increase-the-memory-using-hyper-v-manager"></a>Vergrößern des Arbeitsspeichers mit dem Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Wählen Sie im Ergebnisbereich unter **Virtual Machines**den virtuellen Computer aus, den Sie konfigurieren möchten. Der Status der virtuellen Maschine sollte als **Off**aufgeführt werden. Wenn dies nicht der Fall ist, klicken Sie mit der rechten Maustaste auf den virtuellen Computer und dann auf **herunter**fahren.  
  
3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
4.  Klicken Sie im Navigationsbereich auf Arbeits **Speicher**.  
  
5.  Legen Sie auf der Seite Arbeits **Speicher** den **Start-RAM** auf mindestens 512 MB fest, und klicken Sie dann auf **OK**.  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Vergrößern des Arbeitsspeichers mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **Start** , und beginnen Sie mit der Eingabe von **Windows PowerShell**.)  
  
2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.  
  
3.  Führen Sie den folgenden Befehl aus, nachdem Sie \<myvm > durch den Namen des virtuellen Computers ersetzt haben:  
  
```  
Set-VMMemory <MyVM> -StartupBytes 512MB  
```  
  
## <a name="see-also"></a>Siehe auch  
[Set-vmmemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


