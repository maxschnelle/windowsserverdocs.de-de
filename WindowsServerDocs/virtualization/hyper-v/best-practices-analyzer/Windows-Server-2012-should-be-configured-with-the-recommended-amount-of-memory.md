---
title: Windows Server 2012 sollte mit der empfohlenen Menge an Arbeitsspeicher konfiguriert werden.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 12d0b473-cf6a-4746-b03d-2ceeb701c5d0
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 634e36fe4b871ef33d2b2a3f024521901fffe437
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860983"
---
# <a name="windows-server-2012-should-be-configured-with-the-recommended-amount-of-memory"></a>Windows Server 2012 sollte mit der empfohlenen Menge an Arbeitsspeicher konfiguriert werden.

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
*Ein virtueller Computer, auf dem Windows Server 2012 ausgeführt wird, ist mit weniger als der empfohlene RAM-Größe (2 GB) konfiguriert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Das Gast Betriebssystem und die Anwendungen funktionieren möglicherweise nicht gut. Möglicherweise ist nicht genügend Arbeitsspeicher vorhanden, um mehrere Anwendungen gleichzeitig auszuführen. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie den Hyper-V-Manager, um den Arbeitsspeicher, der diesem virtuellen Computer zugeordnet ist, auf mindestens 2 GB zu erhöhen.*  
  
### <a name="increase-the-memory-using-hyper-v-manager"></a>Vergrößern des Arbeitsspeichers mit dem Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Wählen Sie im Ergebnisbereich unter **Virtual Machines**den virtuellen Computer aus, den Sie konfigurieren möchten. Der Status der virtuellen Maschine sollte als **Off**aufgeführt werden. Wenn dies nicht der Fall ist, klicken Sie mit der rechten Maustaste auf den virtuellen Computer und dann auf **herunter**fahren.  
  
3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
4.  Klicken Sie im Navigationsbereich auf Arbeits **Speicher**.  
  
5.  Legen Sie auf der Seite Arbeits **Speicher** den **Start-RAM** auf mindestens 2 GB fest, und klicken Sie dann auf **OK**.  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Vergrößern des Arbeitsspeichers mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **Start** , und beginnen Sie mit der Eingabe von **Windows PowerShell**.)  
  
2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.  
  
3.  Führen Sie den folgenden Befehl aus, nachdem Sie \<MyVM > durch den Namen des virtuellen Computers ersetzt haben:  
  
```  
Set-VMMemory <MyVM> -StartupBytes 2GB  
```  
  
## <a name="see-also"></a>Weitere Informationen  
[Set-vmmemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


