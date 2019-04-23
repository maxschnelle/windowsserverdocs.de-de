---
title: Konfigurieren Sie mindestens die erforderliche Menge an Arbeitsspeicher für einen virtuellen Computer mit ausgeführtem Windows Server 2012 R2 und für dynamischen Arbeitsspeicher aktiviert
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a0e69661-6a1d-4b31-b727-f2429f3977d0
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4af27b8ba626abaadb3ebadf7060ddfb1f145d5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881291"
---
# <a name="configure-at-least-the-required-amount-of-memory-for-a-virtual-machine-running-windows-server-2012-r2-and-enabled-for-dynamic-memory"></a>Konfigurieren Sie mindestens die erforderliche Menge an Arbeitsspeicher für einen virtuellen Computer mit ausgeführtem Windows Server 2012 R2 und für dynamischen Arbeitsspeicher aktiviert

>Gilt für: Windows Server 2016

Weitere Informationen zu best Practices und Überprüfungen finden Sie unter [Run Best Practices Analyzer Scans und Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt /-Funktion**|Hyper-V|  
|**Schweregrad**|Fehler|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten Kursivschrift gibt an Benutzeroberflächentext, die im Best Practices Analyzer-Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>**Problem:**  
*Eine oder mehrere virtuelle Computer werden konfiguriert, um die Verwendung von dynamischem Arbeitsspeicher mit weniger als die Menge des Arbeitsspeichers für Windows Server 2012 R2 erforderlich sind.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Das Gastbetriebssystem auf die folgenden virtuellen Computer möglicherweise nicht ausgeführt oder unberechenbar Verhalten führen kann:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie Hyper-V-Manager, um den minimalen Arbeitsspeicher an, mindestens 256 MB, und der Arbeitsspeicher beim Start und maximale Arbeitsspeicher auf mindestens 512 MB für diesen virtuellen Computer zu erhöhen.*  
  
### <a name="increase-memory-using-hyper-v-manager"></a>Erhöhen Sie den Arbeitsspeicher mit Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. (In Server-Manager, klicken Sie auf **Tools** > **Hyper-V-Manager**.)  
  
2.  In der Liste von virtuellen Computern Maustaste diejenige werden soll, und klicken Sie dann **Einstellungen**.  
  
3.  Klicken Sie im Navigationsbereich auf **Arbeitsspeicher**.  
  
4.  Ändern der **RAM** auf mindestens 512 MB.  
  
5.  Unter **dynamischer Arbeitsspeicher**, ändern Sie die **Mindestarbeitsspeicher** auf mindestens 256 MB und die **maximaler RAM** auf 512 MB.  
  
6.  Klicken Sie auf **OK**.  
  
### <a name="increase-memory-using-windows-powershell"></a>Erhöhen Sie den Arbeitsspeicher, die mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **starten** und beginnen mit der Eingabe **Windows PowerShell**.)  
  
2.  Mit der rechten Maustaste **Windows PowerShell** , und klicken Sie auf **als Administrator ausführen**.  
  
3.  Führen Sie einen Befehl ähnlich dem folgenden und MyVM durch den Namen Ihres virtuellen Computers und den Arbeitsspeicher und Ersetzen Sie dabei Werte mit mindestens die unten aufgeführten Werte.  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512MB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


