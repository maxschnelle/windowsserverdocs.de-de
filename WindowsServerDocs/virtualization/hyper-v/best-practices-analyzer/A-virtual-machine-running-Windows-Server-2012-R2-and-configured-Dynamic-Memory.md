---
title: Ein virtueller Computer, auf dem Windows Server 2012 R2 ausgeführt wird und der mit dynamischer Arbeitsspeicher konfiguriert ist, sollte Empfohlene Werte für Arbeitsspeicher Einstellungen verwenden
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 3a53c197-80ce-4b33-a83e-7e89e657a519
ms.date: 8/16/2016
ms.openlocfilehash: ed840c92ba68fb9f616522071ea6b4b4561b31f3
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746535"
---
# <a name="a-virtual-machine-running-windows-server-2012-r2-and-configured-with-dynamic-memory-should-use-recommended-values-for-memory-settings"></a>Ein virtueller Computer, auf dem Windows Server 2012 R2 ausgeführt wird und der mit dynamischer Arbeitsspeicher konfiguriert ist, sollte Empfohlene Werte für Arbeitsspeicher Einstellungen verwenden

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Mindestens ein virtueller Computer ist so konfiguriert, dass er dynamischer Arbeitsspeicher mit weniger als dem für Windows Server 2012 R2 empfohlenen Arbeitsspeicher verwendet wird.*

## <a name="impact"></a>Auswirkung
*Das Gast Betriebssystem auf den folgenden virtuellen Computern wird möglicherweise nicht ausgeführt oder kann nicht zuverlässig ausgeführt werden:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Verwenden Sie den Hyper-V-Manager, um den minimalen Arbeitsspeicher auf mindestens 256 MB, den Start Speicher auf mindestens 512 MB und den maximalen Arbeitsspeicher auf mindestens 2 GB für diesen virtuellen Computer zu erhöhen.*

#### <a name="increase-memory-using-hyper-v-manager"></a>Erhöhen des Arbeitsspeichers mit dem Hyper-V-Manager

1.  Öffnen Sie den Hyper-V-Manager. ( **Klicken Sie** in Server-Manager auf  >  Extras. **Hyper-V-Manager**.)

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



