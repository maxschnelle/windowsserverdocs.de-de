---
title: Net print
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 441a61756869442fb91d26bfacc64bbeb8b902f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826011"
---
# <a name="net-print"></a>Net print

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen über eine Warteschlange angegebenen Drucker oder einem angegebenen Druckauftrag, oder einen angegebenen Druckauftrag steuert.
Beispiele zur Verwendung mit diesem Befehl finden Sie in der [Beispiele](#BKMK_examples) Abschnitt dieses Dokuments.
> [!NOTE]
> Dieser Befehl wurde in Windows 7 und Windows Server 2008 R2 als veraltet markiert. Allerdings können Sie viele der Aufgaben mithilfe von Prnjobs, Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) oder Windows PowerShell-Cmdlets ausführen. Weitere Informationen finden Sie unter [Prnjobs](prnjobs.md), [Windows-Verwaltungsinstrumentation](https://go.microsoft.com/fwlink/?LinkID=29991) (https://go.microsoft.com/fwlink/?LinkID=29991), [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=128426) (https://go.microsoft.com/fwlink/?LinkID=128426), und die [TechNet Script Center-Katalog](https://go.microsoft.com/fwlink/?LinkId=164635) (https://go.microsoft.com/fwlink/?LinkId=164635).
## <a name="syntax"></a>Syntax
```
Net print {\\<computerName>\<Sharename> | 
\\<computerName> <JobNumber> [/hold | /release | /delete]} [help]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|\\\\<computerName>\\<Sharename>|Gibt an (nach Namen) der Computer "und" Print-Warteschlange, die über die Sie Informationen anzeigen möchten.|
|\\\\<computerName>|Gibt an (nach Namen) der Computer, der den Druckauftrag verwaltet wird, den Sie steuern möchten. Wenn Sie einen Computer nicht angeben, wird davon ausgegangen, dass der lokale Computer. Erfordert die <JobNumber> Parameter.|
|<JobNumber>|Gibt die Nummer des Druckauftrags, die Sie steuern möchten. Diese Zahl wird von dem Computer zugewiesen, die von die Druckwarteschlange verwaltet, in dem der Druckauftrag gesendet wird. Nachdem ein Computer einer Zahl einen Druckauftrag, zugewiesen wurde, dass die Anzahl nicht zu anderen Druckaufträgen in einer beliebigen Warteschlange, die von diesem Computer gehosteten zugewiesen ist. Erforderlich, wenn Sie mit der \\ \\ <computerName> Parameter.|
|[/hold &#124; /release &#124; /delete]|Gibt die Aktion an, mit dem Druckauftrag an.<br /><br />– Die **/halten** Parameter verzögert den Auftrag an, dass andere Druckaufträge umgangen werden, bis Sie wieder freigegeben wird.<br />– Die **/release** Parameter Versionen ein Druckauftrags, der verzögert wurde.<br />– Die **/delete** Parameter entfernt einen Druckauftrag aus einer Druckwarteschlange.<br /><br />Wenn Sie eine Auftragsnummer, aber keine Aktionen angeben, werden Informationen über den Druckauftrag angezeigt.|
|Hilfe|Zeigt die Hilfe für die **Net Drucken** Befehl.|
## <a name="remarks"></a>Hinweise
-   **NET-Drucken** \\ \\ <computerName> zeigt Informationen über Druckaufträge in einer freigegebenen Drucker-Warteschlange. Im folgenden finden ein Beispiel für einen Bericht für alle Druckaufträge in einer Warteschlange für einen freigegebenen Drucker mit dem Namen LASER:
    ```
    printers at \\PRODUCTION
    Name              Job #      Size      Status
    -----------------------------
    LASER Queue       3 jobs               *printer active*
       USER1          84        93844      printing
       USER2          85        12555      Waiting
       USER3          86        10222      Waiting
    ```
-   Im folgenden finden ein Beispiel für einen Bericht für einen Druckauftrag:
    ```
    Job #            35
    Status           Waiting
    Size             3096
    remark
    Submitting user  USER2
    Notify           USER2
    Job data type
    Job parameters
    additional info
    ```
## <a name="BKMK_examples"></a>Beispiele für
Dieses Beispiel zeigt den Inhalt der Druckwarteschlange Dotmatrix auf Auflisten der \\\Production Computer:
```
Net print \\Production\Dotmatrix 
```
Dieses Beispiel zeigt die Vorgehensweise beim Anzeigen von Informationen über 35 des Auftrags auf die \\\Production Computer:
```
Net print \\Production 35 
```
In diesem Beispiel wird gezeigt, wie zu verzögern, 263 des Auftrags auf die \\\Production Computer:
```
Net print \\Production 263 /hold 
```
Dieses Beispiel zeigt, wie 263 des Auftrags auf die \\\Production Computer:
```
Net print \\Production 263 /release 
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[druckbefehlsreferenz](print-command-reference.md)
