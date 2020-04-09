---
title: Die WFP-Erweiterung für virtuelle Switches sollte aktiviert werden, wenn sie für Erweiterungen von Drittanbietern erforderlich ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8aa8a9a5-e3fa-4c9b-8331-ba5a3de22429
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: d4cc23ce638f7b5ee95f80de067b4ad5b360d118
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859303"
---
# <a name="the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions"></a>Die WFP-Erweiterung für virtuelle Switches sollte aktiviert werden, wenn sie für Erweiterungen von Drittanbietern erforderlich ist.

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
*Die virtuelle Switcherweiterung der Windows-Filter Plattform (WFP) ist deaktiviert.*  
  
## <a name="impact"></a>**Auswirkt**  
*Einige Erweiterungen für virtuelle Switches von Drittanbietern funktionieren möglicherweise nicht ordnungsgemäß auf den folgenden virtuellen Switches:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie das Windows PowerShell-Cmdlet Enable-vmswitchextension, um die Windows-Filter Plattform zu aktivieren, wenn Sie für Erweiterungen von Drittanbietern erforderlich ist.*  
  
### <a name="enable-the-windows-filtering-platform-using-windows-powershell"></a>Aktivieren der Windows-Filter Plattform mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **Start** , und beginnen Sie mit der Eingabe von **Windows PowerShell**.)  
  
2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.  
  
3.  Führen Sie den folgenden Befehl aus, nachdem Sie extern durch den Namen des externen Switches ersetzt haben:  
  
```  
Enable-VMSwitchExtension -VMSwitchName External -Name Microsoft Windows Filtering Platform  
```  
  
## <a name="see-also"></a>Weitere Informationen  
[Enable-vmswitchextension](https://technet.microsoft.com/library/hh848541.aspx)  
  


