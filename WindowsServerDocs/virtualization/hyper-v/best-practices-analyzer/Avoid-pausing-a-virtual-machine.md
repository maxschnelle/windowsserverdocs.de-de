---
title: Verhindern, dass ein virtueller Computer angehalten wird
description: Online Version des Texts für diese Best Practices Analyzer Regel.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 930f927c-e414-4a36-9786-028941e886e4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 6799795ae383fd0522ce0b35eba0443ae536b0dd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969997"
---
# <a name="avoid-pausing-a-virtual-machine"></a>Verhindern, dass ein virtueller Computer angehalten wird

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Schweregrad**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Dieser Server verfügt über einen oder mehrere virtuelle Computer im angehaltenen Zustand.*

## <a name="impact"></a>Auswirkung

*Abhängig von der Menge des verfügbaren Arbeitsspeichers können Sie möglicherweise keine zusätzlichen virtuellen Maschinen ausführen.*

Bei angehaltenen virtuellen Computern wird der zugewiesene Arbeitsspeicher nicht freigegeben, was bedeutet, dass der Arbeitsspeicher zum Starten anderer virtueller Maschinen nicht verfügbar ist

## <a name="resolution"></a>Lösung

*Wenn dies beabsichtigt ist, ist keine weitere Aktion erforderlich. Andernfalls sollten Sie diese virtuellen Computer fortsetzen oder Herunterfahren.*

#### <a name="use-hyper-v-manager-to-resume-the-virtual-machine"></a>Fortsetzen des virtuellen Computers mit dem Hyper-V-Manager

1.  Öffnen Sie den Hyper-V-Manager. (Klicken Sie **im Menü Extras** von Server-Manager auf **Hyper-V-Manager**.)

2.  Suchen Sie in der Liste **Virtual Machines** die virtuellen Computer mit dem Status **angeh**alten.

    > [!IMPORTANT]
    > Der Status " **angehalten-kritisch** " tritt auf, wenn im physischen Speicher für diesen virtuellen Computer nur noch wenig freier Speicherplatz verbleiben. Bevor Sie versuchen, einen virtuellen Computer in diesem Zustand fortzusetzen, geben Sie verfügbaren Speicherplatz im physischen Speicher frei.

3.  Klicken Sie mit der rechten Maustaste auf jeden virtuellen Computer, und klicken Sie **dann auf fort**setzen Dadurch wechselt der virtuelle Computer zurück in den Ausführungszustand. Wenn Sie anschließend den virtuellen Computer herunterfahren möchten, klicken Sie erneut mit der rechten Maustaste darauf, und wählen Sie **herunter**fahren aus.

#### <a name="use-windows-powershell-to-resume-the-virtual-machine"></a>Verwenden von Windows PowerShell zum Fortsetzen des virtuellen Computers

Sie können dies in einem Befehl mithilfe von Filtern und der Pipeline tun, nachdem Sie alle virtuellen Maschinen auf dem Host erhalten haben. Typ:

```
get-vm | where state -eq 'paused' | resume-vm
```



