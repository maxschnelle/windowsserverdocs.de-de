---
title: Ein virtueller Computer, auf dem Windows Server 2012 ausgeführt wird und der mit dynamischer Arbeitsspeicher konfiguriert ist, sollte Empfohlene Werte für Arbeitsspeicher Einstellungen
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aa35e36-8e3b-498b-b71d-003a0a0947be
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 776fbbfc3170ad0c569e57648f8e055f9c68a262
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857863"
---
# <a name="a-virtual-machine-running-windows-server-2012-and-configured-with-dynamic-memory-should-use-recommended-values-for-memory-settings"></a>Ein virtueller Computer, auf dem Windows Server 2012 ausgeführt wird und der mit dynamischer Arbeitsspeicher konfiguriert ist, sollte Empfohlene Werte für Arbeitsspeicher Einstellungen

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
*Mindestens ein virtueller Computer ist für die Verwendung von dynamischer Arbeitsspeicher mit weniger als dem für Windows Server 2012 empfohlenen Arbeitsspeicher konfiguriert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Das Gast Betriebssystem auf den folgenden virtuellen Computern wird möglicherweise nicht ausgeführt oder kann nicht zuverlässig ausgeführt werden:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie den Hyper-V-Manager, um den Minimalwert auf mindestens 256 MB, den Start Speicher auf mindestens 512 MB und den maximalen Arbeitsspeicher für diesen virtuellen Computer auf mindestens 2 GB zu erhöhen.*  
  
#### <a name="increase-memory-using-hyper-v-manager"></a>Erhöhen des Arbeitsspeichers mit dem Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. ( **Klicken Sie** in Server-Manager auf Extras > **Hyper-V-Manager**.)  
  
2.  Klicken Sie in der Liste der virtuellen Computer mit der rechten Maustaste auf das gewünschte, und klicken Sie dann auf **Einstellungen**.  
  
3.  Klicken Sie im Navigationsbereich auf Arbeits **Speicher**.  
  
4.  Ändern Sie den **RAM** auf mindestens 512 MB.  
  
5.  Ändern Sie unter **dynamischer Arbeitsspeicher**den **minimalen RAM** auf mindestens 256 MB und den **maximalen RAM** auf 2 GB.  
  
6.  Klicken Sie auf **OK**.  
  
### <a name="increase-memory-using-windows-powershell"></a>Erhöhen des Arbeitsspeichers mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **Start** , und beginnen Sie mit der Eingabe von **Windows PowerShell**.)  
  
2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.  
  
3.  Führen Sie einen Befehl aus, der dem folgenden ähnelt, und ersetzen Sie dabei MyVM durch den Namen des virtuellen Computers und die Arbeitsspeicher Werte mit mindestens den unten gezeigten Werten.  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 2GB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


