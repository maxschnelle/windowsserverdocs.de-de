---
title: Konfigurieren Sie mindestens die erforderliche Arbeitsspeicher Menge für einen virtuellen Computer, auf dem Windows Server 2008 R2 ausgeführt wird und für den dynamischer Arbeitsspeicher aktiviert ist.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: db0bff4c-39fe-49c1-903a-1f2a0b0db891
ms.date: 8/16/2016
ms.openlocfilehash: eaafc5ba990e30880878c540642b32d2e81f63e0
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746935"
---
# <a name="configure-at-least-the-required-amount-of-memory-for-a-virtual-machine-running-windows-server-2008-r2-and-enabled-for-dynamic-memory"></a>Konfigurieren Sie mindestens die erforderliche Arbeitsspeicher Menge für einen virtuellen Computer, auf dem Windows Server 2008 R2 ausgeführt wird und für den dynamischer Arbeitsspeicher aktiviert ist.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Fehler|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Mindestens ein virtueller Computer ist für die Verwendung von dynamischer Arbeitsspeicher mit weniger als dem für Windows Server 2008 R2 erforderlichen Arbeitsspeicher konfiguriert.*

## <a name="impact"></a>Auswirkung
*Das Gast Betriebssystem auf den folgenden virtuellen Computern wird möglicherweise nicht ausgeführt oder kann nicht zuverlässig ausgeführt werden:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Verwenden Sie den Hyper-V-Manager oder Windows PowerShell, um den minimalen Arbeitsspeicher auf mindestens 256 MB und den Start Speicher und den maximalen Arbeitsspeicher auf mindestens 512 MB zu erhöhen.*

### <a name="increase-memory-using-hyper-v-manager"></a>Erhöhen des Arbeitsspeichers mit dem Hyper-V-Manager

1.  Öffnen Sie den Hyper-V-Manager. ( **Klicken Sie** in Server-Manager auf  >  Extras. **Hyper-V-Manager**.)

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



