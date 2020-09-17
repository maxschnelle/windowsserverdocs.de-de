---
title: Windows Server 2008 R2 sollte mit der empfohlenen Menge an Arbeitsspeicher konfiguriert werden.
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 26872519-ccf0-4757-827f-8df2a7a2b9f9
ms.date: 8/16/2016
ms.openlocfilehash: 70efebe89677f905c1f36e723bcf57fa3b584ccd
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746665"
---
# <a name="windows-server-2008-r2-should-be-configured-with-the-recommended-amount-of-memory"></a>Windows Server 2008 R2 sollte mit der empfohlenen Menge an Arbeitsspeicher konfiguriert werden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Überprüfungen finden Sie unter [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Ein virtueller Computer, auf dem Windows Server 2008 R2 ausgeführt wird, ist mit weniger als der empfohlene RAM-Größe (2 GB) konfiguriert.*

## <a name="impact"></a>Auswirkung

*Das Gast Betriebssystem und die Anwendungen funktionieren möglicherweise nicht gut. Möglicherweise ist nicht genügend Arbeitsspeicher vorhanden, um mehrere Anwendungen gleichzeitig auszuführen. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machine names>

## <a name="resolution"></a>Lösung

*Verwenden Sie den Hyper-V-Manager, um den Arbeitsspeicher, der diesem virtuellen Computer zugeordnet ist, auf mindestens 2 GB zu erhöhen.*

### <a name="to-increase-the-memory-using-hyper-v-manager"></a>So vergrößern Sie den Arbeitsspeicher mit dem Hyper-V-Manager

1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.

2.  Wählen Sie im Ergebnisbereich unter **Virtual Machines**den virtuellen Computer aus, den Sie konfigurieren möchten. Der Status der virtuellen Maschine sollte als **Off**aufgeführt werden. Wenn dies nicht der Fall ist, klicken Sie mit der rechten Maustaste auf den virtuellen Computer und dann auf **herunter**fahren.

3.  Klicken Sie im Bereich **Aktion** unter dem Namen des virtuellen Computers auf **Einstellungen**.

4.  Klicken Sie im Navigationsbereich auf Arbeits **Speicher**.

5.  Legen Sie auf der Seite Arbeits **Speicher** den **Start-RAM** auf mindestens 2 GB fest, und klicken Sie dann auf **OK**.

### <a name="increase-the-memory-using-windows-powershell"></a>Vergrößern des Arbeitsspeichers mithilfe von Windows PowerShell

1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf **Start** , und beginnen Sie mit der Eingabe von **Windows PowerShell**.)

2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.

3.  Führen Sie den folgenden Befehl \<MyVM> aus, nachdem Sie durch den Namen des virtuellen Computers ersetzt haben:

```
Set-VMMemory <MyVM> -StartupBytes 2GB
```

## <a name="see-also"></a>Weitere Informationen
[Set-vmmemory](/powershell/module/hyper-v/set-vmmemory?view=win10-ps)