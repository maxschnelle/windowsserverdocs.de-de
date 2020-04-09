---
title: Konfigurieren Sie mindestens die erforderliche Arbeitsspeicher Menge für einen virtuellen Computer, auf dem Windows Server 2008 ausgeführt wird und für den dynamischer Arbeitsspeicher aktiviert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aaa7138-ce83-4b17-add7-fdfa3d469bea
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: f34332724bad3d2a0d150496ea8f0c610f5fd2b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862103"
---
# <a name="configure-at-least-the-required-amount-of-memory-for-a-virtual-machine-running-windows-server-2008-and-enabled-for-dynamic-memory"></a>Konfigurieren Sie mindestens die erforderliche Arbeitsspeicher Menge für einen virtuellen Computer, auf dem Windows Server 2008 ausgeführt wird und für den dynamischer Arbeitsspeicher aktiviert ist.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Error|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Mindestens ein virtueller Computer ist für die Verwendung von dynamischer Arbeitsspeicher mit weniger als dem für Windows Server 2008 erforderlichen Arbeitsspeicher konfiguriert.*  
  
## <a name="impact"></a>Auswirkungen  
*Das Gast Betriebssystem auf den folgenden virtuellen Computern wird möglicherweise nicht ausgeführt oder kann nicht zuverlässig ausgeführt werden:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>Auflösung  
*Verwenden Sie den Hyper-V-Manager oder Windows PowerShell, um den minimalen Arbeitsspeicher auf mindestens 256 MB und den Start Speicher und den maximalen Arbeitsspeicher auf mindestens 512 MB zu erhöhen.*  
  
### <a name="increase-memory-using-hyper-v-manager"></a>Erhöhen des Arbeitsspeichers mit dem Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. ( **Klicken Sie** in Server-Manager auf Extras > **Hyper-V-Manager**.)  
  
2.  Klicken Sie in der Liste der virtuellen Computer mit der rechten Maustaste auf das gewünschte, und klicken Sie dann auf **Einstellungen**.  
  
3.  Klicken Sie im Navigationsbereich auf Arbeits **Speicher**.  
  
4.  Ändern Sie den **RAM** auf mindestens 512 MB.  
  
5.  Ändern Sie unter **dynamischer Arbeitsspeicher**den **minimalen RAM** auf mindestens 256 MB und den **maximalen RAM** auf 512 MB.  
  
6.  Klicken Sie auf **OK**.  
  
### <a name="increase-memory-using-windows-powershell"></a>Erhöhen des Arbeitsspeichers mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **Start** , und beginnen Sie mit der Eingabe von **Windows PowerShell**.)  
  
2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.  
  
3.  Führen Sie einen Befehl aus, der dem folgenden ähnelt, und ersetzen Sie dabei MyVM durch den Namen des virtuellen Computers und die Arbeitsspeicher Werte mit mindestens den unten gezeigten Werten.  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512MB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


