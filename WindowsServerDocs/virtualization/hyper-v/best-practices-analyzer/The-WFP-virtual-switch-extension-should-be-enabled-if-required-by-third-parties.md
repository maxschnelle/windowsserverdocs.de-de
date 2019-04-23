---
title: Die WFP-Erweiterung für virtuelle Switches sollte aktiviert werden, wenn sie für Erweiterungen von Drittanbietern erforderlich ist.
description: Die Onlineversion des Texts für diese Best Practices Analyzer-Regel.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8aa8a9a5-e3fa-4c9b-8331-ba5a3de22429
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5afe706c246276597b32400109370ba3129e5a24
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850621"
---
# <a name="the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions"></a>Die WFP-Erweiterung für virtuelle Switches sollte aktiviert werden, wenn sie für Erweiterungen von Drittanbietern erforderlich ist.

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
*Die Windows-Filterplattform (WFP)-Erweiterung für virtuelle Switches ist deaktiviert.*  
  
## <a name="impact"></a>**Auswirkungen**  
*Einige Drittanbieter-Erweiterungen für virtuelle Switches funktionieren möglicherweise nicht ordnungsgemäß auf den folgenden virtuellen Switches:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Verwenden Sie das Windows PowerShell-Cmdlet Enable-VMSwitchExtension, um die Windows-Filterplattform zu aktivieren, wenn sie Erweiterungen von Drittanbietern erforderlich ist.*  
  
### <a name="enable-the-windows-filtering-platform-using-windows-powershell"></a>Aktivieren Sie die Windows-Filterplattform mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **starten** und beginnen mit der Eingabe **Windows PowerShell**.)  
  
2.  Mit der rechten Maustaste **Windows PowerShell** , und klicken Sie auf **als Administrator ausführen**.  
  
3.  Führen Sie diesen Befehl nach dem Ersetzen von externen mit dem Namen des externen Switches:  
  
```  
Enable-VMSwitchExtension -VMSwitchName External -Name "Microsoft Windows Filtering Platform"  
```  
  
## <a name="see-also"></a>Siehe auch  
[Enable-VMSwitchExtension](https://technet.microsoft.com/library/hh848541.aspx)  
  


