---
title: net print
description: Referenz Artikel für den Befehl net Print. Dieser Befehl ist veraltet und wird in zukünftigen Versionen von Windows nicht mehr unterstützt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ac91d2226e9a5394d6f7ea00ab6f268eb99015b
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956802"
---
# <a name="net-print"></a>net print

> [!IMPORTANT]
> Dieser Befehl ist veraltet. Sie können jedoch viele der gleichen Aufgaben mit dem [Befehl prnjobs](prnjobs.md)ausführen, [Windows-Verwaltungsinstrumentation (WMI)](/windows/win32/wmisdk/wmi-start-page), [Printmanagement in PowerShell](/powershell/module/printmanagement)oder [Skript Ressourcen für IT-Experten](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing).

Zeigt Informationen zu einer angegebenen Drucker Warteschlange oder einem angegebenen Druckauftrag an oder steuert einen angegebenen Druckauftrag.

## <a name="syntax"></a>Syntax

```
net print {\\<computername>\<sharename> | \\<computername> <jobnumber> [/hold | /release | /delete]} [help]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ---------- | ----------- |
| `\\<computername>\<sharename>` | Gibt (nach Name) den Computer und die Druck Warteschlange an, über die Sie Informationen anzeigen möchten. |
| `\\<computername>` | Gibt (nach Name) den Computer an, der den Druckauftrag hostet, den Sie steuern möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer angenommen. Erfordert den- `<jobnumber>` Parameter. |
| `<jobnumber>` | Gibt die Nummer des Druckauftrags an, den Sie steuern möchten. Diese Nummer wird von dem Computer zugewiesen, der die Druck Warteschlange hostet, in der der Druckauftrag gesendet wird. Wenn ein Computer einem Druckauftrag eine Zahl zuweist, wird diese Nummer keinem anderen Druckauftrag in einer Warteschlange zugewiesen, die von diesem Computer gehostet wird. Erforderlich, wenn der-Parameter verwendet wird `\\<computername>` . |
| `[/hold | /release | /delete]` | Gibt die Aktion an, die mit dem Druckauftrag ausgeführt werden soll. Wenn Sie eine Auftragsnummer angeben, aber keine Aktion angeben, werden Informationen zum Druckauftrag angezeigt.<ul><li>**/Hold** -verzögert den Auftrag, sodass andere Druckaufträge ihn umgehen können, bis er freigegeben wird.</li><li>**/Release** : gibt einen verzögerten Druckauftrag frei.</li><li>**/Delete** -entfernt einen Druckauftrag aus einer Druck Warteschlange.</li></ul> |
| help | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Der- `net print\\<computername>` Befehl zeigt Informationen über Druckaufträge in einer freigegebenen Drucker Warteschlange an. Im folgenden finden Sie ein Beispiel für einen Bericht für alle Druckaufträge in einer Warteschlange für einen freigegebenen Drucker mit dem Namen " *Laser*":

    ```
    printers at \\PRODUCTION
    Name              Job #      Size      Status
    -----------------------------
    LASER Queue       3 jobs               *printer active*
    USER1          84        93844      printing
    USER2          85        12555      Waiting
    USER3          86        10222      Waiting
    ```

- Im folgenden finden Sie ein Beispiel für einen Bericht für einen Druckauftrag:

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

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Inhalt der *Dotmatrix* -Druck Warteschlange auf dem * \\ Produktions* Computer aufzulisten:

```
net print \\Production\Dotmatrix
```

Geben Sie Folgendes ein, um Informationen zur Auftragsnummer *35* auf dem * \\ Produktions* Computer anzuzeigen:

```
net print \\Production 35
```

Geben Sie zum verzögern der Auftragsnummer *263* auf dem * \\ Produktions* Computer Folgendes ein:

```
net print \\Production 263 /hold
```

Geben Sie Folgendes ein, um die Auftragsnummer *263* auf dem * \\ Produktions* Computer freizugeben:

```
net print \\Production 263 /release
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehls Verweis drucken](print-command-reference.md)

- [prnjobs-Befehl](prnjobs.md)

- [Windows-Verwaltungsinstrumentation (WMI)](/windows/win32/wmisdk/wmi-start-page)

- [Printmanagement in PowerShell](/powershell/module/printmanagement)

- [Skripterstellung für Ressourcen für IT-Experten](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing)
