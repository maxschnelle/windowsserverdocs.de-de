---
title: Windows Server 2008 R2 sollte mit die empfohlene Menge an Arbeitsspeicher konfiguriert werden
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 26872519-ccf0-4757-827f-8df2a7a2b9f9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: a2737ef0001e1859e514f44fccd6d49bd3ae3a48
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865361"
---
# <a name="windows-server-2008-r2-should-be-configured-with-the-recommended-amount-of-memory"></a>Windows Server 2008 R2 sollte mit die empfohlene Menge an Arbeitsspeicher konfiguriert werden

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Ein virtuellen Computer mit Windows Server 2008 R2 wird mit weniger als die empfohlene Menge an RAM, 2 GB konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Die Gast-Betriebssystem und Anwendungen möglicherweise nicht optimal ausgeführt werden. Gibt es möglicherweise nicht genügend Arbeitsspeicher, um mehrere Anwendungen gleichzeitig ausgeführt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*  
  
\<Liste von Namen virtueller Computer >  
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Hyper-V-Manager, um die Speichermenge für diese virtuelle Maschine über mindestens 2 GB zu erhöhen.*  
  
### <a name="to-increase-the-memory-using-hyper-v-manager"></a>Um den Speicher mit Hyper-V-Manager zu erhöhen.  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Klicken Sie im Ergebnisbereich unter **VMs**, wählen Sie den virtuellen Computer, die Sie konfigurieren möchten. Der Status des virtuellen Computers sollte als aufgelistet werden **aus**. Wenn sie nicht der Fall ist, mit der rechten Maustaste den virtuellen Computer, und klicken Sie dann auf **Herunterfahren**.  
  
3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
4.  Klicken Sie im Navigationsbereich auf **Arbeitsspeicher**.  
  
5.  Auf der **Arbeitsspeicher** Seite die **RAM beim Start** mindestens 2 GB, und klicken Sie dann auf **OK**.  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Geben Sie Speicher mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **starten** und beginnen mit der Eingabe **Windows PowerShell**.)  
  
2.  Mit der rechten Maustaste **Windows PowerShell** , und klicken Sie auf **als Administrator ausführen**.  
  
3.  Führen Sie diesen Befehl nach dem Ersetzen \<MyVM > durch den Namen des virtuellen Computers:  
  
```  
Set-VMMemory <MyVM> -StartupBytes 2GB  
```  
  
## <a name="see-also"></a>Siehe auch  
[Set-VMMemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


