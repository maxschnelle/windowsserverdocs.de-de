---
title: Windows Server 2008 R2 sollte mit mindestens der Mindestmenge an Arbeitsspeicher konfiguriert werden.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 12418668-52d3-4e70-b56f-85dcb144a8c0
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: bf206558460c7ef14b2f2965bb5c247d98942862
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860013"
---
# <a name="windows-server-2008-r2-should-be-configured-with-at-least-the-minimum-amount-of-memory"></a>Windows Server 2008 R2 sollte mit mindestens der Mindestmenge an Arbeitsspeicher konfiguriert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Ein virtueller Computer, auf dem Windows Server 2008 R2 ausgeführt wird, ist mit einer geringeren Anzahl von RAM (512 MB) konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Das Gast Betriebssystem auf den folgenden virtuellen Computern wird möglicherweise nicht ausgeführt oder kann nicht zuverlässig ausgeführt werden:*  
  
  
\<Liste der Namen der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie den Hyper-V-Manager, um den Arbeitsspeicher, der diesem virtuellen Computer zugeordnet ist, auf mindestens 512 MB zu erhöhen.*  
  
### <a name="to-increase-the-memory-using-hyper-v"></a>So vergrößern Sie den Arbeitsspeicher mit Hyper-V  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Wählen Sie im Ergebnisbereich unter **Virtual Machines**den virtuellen Computer aus, den Sie konfigurieren möchten. Der Status der virtuellen Maschine sollte als **Off**aufgeführt werden. Wenn dies nicht der Fall ist, klicken Sie mit der rechten Maustaste auf den virtuellen Computer und dann auf **herunter**fahren.  
  
3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
4.  Klicken Sie im Navigationsbereich auf Arbeits **Speicher**.  
  
5.  Legen Sie auf der Seite Arbeits **Speicher** den **Start-RAM** auf mindestens 512 MB fest, und klicken Sie dann auf **OK**.  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Vergrößern des Arbeitsspeichers mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **Start** , und beginnen Sie mit der Eingabe von **Windows PowerShell**.)  
  
2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.  
  
3.  Führen Sie den folgenden Befehl aus, nachdem Sie \<MyVM > durch den Namen des virtuellen Computers ersetzt haben:  
  
```  
Set-VMMemory <MyVM> -StartupBytes 512MB  
```  
  
## <a name="see-also"></a>Weitere Informationen  
[Set-vmmemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


