---
title: Ein virtuellen Computer mit Windows Server 2012 ausgeführt wird und mit dynamischem Arbeitsspeicher konfiguriert sollten empfohlene Werte für die Einstellungen für den Arbeitsspeicher verwenden.
description: Enthält Anweisungen zur Behebung des Problems gemeldet wird, die von dieser Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aa35e36-8e3b-498b-b71d-003a0a0947be
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: d4a0f4a2700f87a24db812f046cb19cec0e7a4d5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885101"
---
# <a name="a-virtual-machine-running-windows-server-2012-and-configured-with-dynamic-memory-should-use-recommended-values-for-memory-settings"></a>Ein virtuellen Computer mit Windows Server 2012 ausgeführt wird und mit dynamischem Arbeitsspeicher konfiguriert sollten empfohlene Werte für die Einstellungen für den Arbeitsspeicher verwenden.

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Eine oder mehrere virtuelle Computer sind mit weniger als die Menge an Arbeitsspeicher, die für Windows Server 2012 empfohlen für die Verwendung von dynamischem Arbeitsspeicher konfiguriert.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Das Gastbetriebssystem auf die folgenden virtuellen Computer möglicherweise nicht ausgeführt oder unberechenbar Verhalten führen kann:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie Hyper-V-Manager, um den Minimalwert auf mindestens 256 MB, startspeicher auf mindestens 512 MB und der maximale Arbeitsspeicher auf mindestens 2 GB für diesen virtuellen Computer zu erhöhen.*  
  
#### <a name="increase-memory-using-hyper-v-manager"></a>Erhöhen Sie den Arbeitsspeicher mit Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. (In Server-Manager, klicken Sie auf **Tools** > **Hyper-V-Manager**.)  
  
2.  In der Liste von virtuellen Computern Maustaste diejenige werden soll, und klicken Sie dann **Einstellungen**.  
  
3.  Klicken Sie im Navigationsbereich auf **Arbeitsspeicher**.  
  
4.  Ändern der **RAM** auf mindestens 512 MB.  
  
5.  Unter **dynamischer Arbeitsspeicher**, ändern Sie die **Mindestarbeitsspeicher** auf mindestens 256 MB und die **maximaler RAM** auf 2 GB.  
  
6.  Klicken Sie auf **OK**.  
  
### <a name="increase-memory-using-windows-powershell"></a>Erhöhen Sie den Arbeitsspeicher, die mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **starten** und beginnen mit der Eingabe **Windows PowerShell**.)  
  
2.  Mit der rechten Maustaste **Windows PowerShell** , und klicken Sie auf **als Administrator ausführen**.  
  
3.  Führen Sie einen Befehl ähnlich dem folgenden und MyVM durch den Namen Ihres virtuellen Computers und den Arbeitsspeicher und Ersetzen Sie dabei Werte mit mindestens die unten aufgeführten Werte.  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 2GB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


