---
title: Windows Server 2008 muss mindestens die Mindestmenge an Arbeitsspeicher mit konfiguriert
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b5065a3f-364d-4aa9-8703-eafa7a46b575
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 51cc459264a89f223be6d5ae76786005d49b8358
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830881"
---
# <a name="windows-server-2008-should-be-configured-with-at-least-the-minimum-amount-of-memory"></a>Windows Server 2008 muss mindestens die Mindestmenge an Arbeitsspeicher mit konfiguriert

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Ein virtuellen Computer unter Windows Server 2008 wird mit weniger als die minimale Größe des Arbeitsspeichers, konfiguriert und 512 MB beträgt.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Das Gastbetriebssystem auf die folgenden virtuellen Computer möglicherweise nicht ausgeführt oder unberechenbar Verhalten führen kann:*  
  
\<Liste von Namen virtueller Computer >
  
## <a name="resolution"></a>Auflösung  
  
*Verwenden Sie Hyper-V-Manager, um die Speichermenge für diese virtuelle Maschine über mindestens 512 MB erhöhen.*  
  
### <a name="to-increase-the-memory-using-hyper-v-manager"></a>Um den Speicher mit Hyper-V-Manager zu erhöhen.  
  
1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.  
  
2.  Klicken Sie im Ergebnisbereich unter **VMs**, wählen Sie den virtuellen Computer, die Sie konfigurieren möchten. Der Status des virtuellen Computers sollte als aufgelistet werden **aus**. Wenn sie nicht der Fall ist, mit der rechten Maustaste den virtuellen Computer, und klicken Sie dann auf **Herunterfahren**.  
  
3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.  
  
4.  Klicken Sie im Navigationsbereich auf **Arbeitsspeicher**.  
  
5.  Auf der **Arbeitsspeicher** Seite die **RAM beim Start** mindestens 512 MB, und klicken Sie dann auf **OK**.  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Geben Sie Speicher mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **starten** und beginnen mit der Eingabe **Windows PowerShell**.)  
  
2.  Mit der rechten Maustaste **Windows PowerShell** , und klicken Sie auf **als Administrator ausführen**.  
  
3.  Führen Sie diesen Befehl nach dem Ersetzen \<MyVM > durch den Namen des virtuellen Computers:  
  
```  
Set-VMMemory <MyVM> -StartupBytes 512MB  
```  
  
## <a name="see-also"></a>Siehe auch  
[Set-VMMemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


