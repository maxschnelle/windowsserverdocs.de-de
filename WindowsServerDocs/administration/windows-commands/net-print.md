---
title: Net print
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 241f9d74cb537924cf69c1e0bb5fd73a422c4b23
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373300"
---
# <a name="net-print"></a>Net print

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu einer angegebenen Drucker Warteschlange oder einem angegebenen Druckauftrag an oder steuert einen angegebenen Druckauftrag.
Beispiele für die Verwendung dieses Befehls finden Sie im Abschnitt " [Beispiele](#BKMK_examples) " in diesem Dokument.
> [!NOTE]
> Dieser Befehl wurde in Windows 7 und Windows Server 2008 R2 als veraltet markiert. Sie können jedoch viele der gleichen Aufgaben mit prnjobs, Windows-Verwaltungsinstrumentation (WMI) oder Windows PowerShell-Cmdlets ausführen. Weitere Informationen finden Sie unter [prnjobs](prnjobs.md), [Windows-Verwaltungsinstrumentation](https://go.microsoft.com/fwlink/?LinkID=29991) (https://go.microsoft.com/fwlink/?LinkID=29991) , [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=128426) (https://go.microsoft.com/fwlink/?LinkID=128426) und im [TechNet Script Center Gallery](https://go.microsoft.com/fwlink/?LinkId=164635) (https://go.microsoft.com/fwlink/?LinkId=164635) ).
> ## <a name="syntax"></a>Syntax
> ```
> Net print {\\<computerName>\<Sharename> | 
> \\<computerName> <JobNumber> [/hold | /release | /delete]} [help]
> ```
> ## <a name="parameters"></a>Parameter
> 
> |               Parameter               |                                                                                                                                                                                                                     Beschreibung                                                                                                                                                                                                                      |
> |----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |    \\\\<computerName>\\<Sharename>     |                                                                                                                                                                            Gibt (nach Name) den Computer und die Druck Warteschlange an, über die Sie Informationen anzeigen möchten.                                                                                                                                                                             |
> |           \\\\<computerName>           |                                                                                                                                 Gibt (nach Name) den Computer an, der den Druckauftrag hostet, den Sie steuern möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer angenommen. Erfordert den <JobNumber>-Parameter.                                                                                                                                  |
> |              <JobNumber>               |                                             Gibt die Nummer des Druckauftrags an, den Sie steuern möchten. Diese Nummer wird von dem Computer zugewiesen, der die Druck Warteschlange hostet, in der der Druckauftrag gesendet wird. Wenn ein Computer einem Druckauftrag eine Zahl zuweist, wird diese Nummer keinem anderen Druckauftrag in einer Warteschlange zugewiesen, die von diesem Computer gehostet wird. Erforderlich, wenn der Parameter "\\ @ no__t-1 @ no__t-2" verwendet wird.                                             |
> | [/Hold &#124; /Release &#124; /DELETE] | Gibt die Aktion an, die mit dem Druckauftrag ausgeführt werden soll.<br /><br />-Der **/Hold** -Parameter verzögert den Auftrag, sodass andere Druckaufträge ihn umgehen können, bis er freigegeben wird.<br />-Der **/Release** -Parameter gibt einen verzögerten Druckauftrag frei.<br />-Der **/Delete** -Parameter entfernt einen Druckauftrag aus einer Druck Warteschlange.<br /><br />Wenn Sie eine Auftragsnummer angeben, aber keine Aktion angeben, werden Informationen zum Druckauftrag angezeigt. |
> |                  Hilfe                  |                                                                                                                                                                                                     Zeigt die Hilfe für den Befehl " **net Print** " an.                                                                                                                                                                                                     |
> 
> ## <a name="remarks"></a>Hinweise
> - **Net Print** \\ @ no__t-2 @ no__t-3 zeigt Informationen über Druckaufträge in einer freigegebenen Drucker Warteschlange an. Im folgenden finden Sie ein Beispiel für einen Bericht für alle Druckaufträge in einer Warteschlange für einen freigegebenen Drucker mit dem Namen "Laser":
>   ```
>   printers at \\PRODUCTION
>   Name              Job #      Size      Status
>   -----------------------------
>   LASER Queue       3 jobs               *printer active*
>      USER1          84        93844      printing
>      USER2          85        12555      Waiting
>      USER3          86        10222      Waiting
>   ```
> - Im folgenden finden Sie ein Beispiel für einen Bericht für einen Druckauftrag:
>   ```
>   Job #            35
>   Status           Waiting
>   Size             3096
>   remark
>   Submitting user  USER2
>   Notify           USER2
>   Job data type
>   Job parameters
>   additional info
>   ```
>   ## <a name="BKMK_examples"></a>Beispiele
>   Dieses Beispiel zeigt, wie Sie den Inhalt der Dotmatrix-Druck Warteschlange auf dem \\ \ Produktions Computer auflisten:
>   ```
>   Net print \\Production\Dotmatrix 
>   ```
>   Dieses Beispiel zeigt, wie Sie Informationen zur Auftragsnummer 35 auf dem Computer \\ \ Produktion anzeigen:
>   ```
>   Net print \\Production 35 
>   ```
>   In diesem Beispiel wird gezeigt, wie die Auftragsnummer 263 auf dem Computer \\ \ Produktion verzögert wird:
>   ```
>   Net print \\Production 263 /hold 
>   ```
>   Dieses Beispiel zeigt, wie Sie die Auftragsnummer 263 auf dem Computer \\ \ Produktion freigeben:
>   ```
>   Net print \\Production 263 /release 
>   ```
>   #### <a name="additional-references"></a>Weitere Verweise
>   [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
>   [Druck Befehlsreferenz](print-command-reference.md)
