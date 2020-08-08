---
title: Die WFP-Erweiterung für virtuelle Switches sollte aktiviert werden, wenn sie für Erweiterungen von Drittanbietern erforderlich ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 8aa8a9a5-e3fa-4c9b-8331-ba5a3de22429
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 8a8ee1cae5f1eb64e11494d62bc31ebff295d284
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960473"
---
# <a name="the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions"></a>Die WFP-Erweiterung für virtuelle Switches sollte aktiviert werden, wenn sie für Erweiterungen von Drittanbietern erforderlich ist.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>**Problem**
*Die virtuelle Switcherweiterung der Windows-Filter Plattform (WFP) ist deaktiviert.*

## <a name="impact"></a>**Auswirkungen**
*Einige Erweiterungen für virtuelle Switches von Drittanbietern funktionieren möglicherweise nicht ordnungsgemäß auf den folgenden virtuellen Switches:*

\<list of virtual machines>

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



