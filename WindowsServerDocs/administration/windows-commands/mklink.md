---
title: mklink
description: Referenz Thema für den mklink-Befehl, mit dem ein Verzeichnis oder eine Datei als symbolischer oder fester Link erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f998533ce3184213786a341c2413e7323496e96
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354610"
---
# <a name="mklink"></a>mklink

Erstellt einen symbolischen oder festen Link für ein Verzeichnis oder eine Datei.

## <a name="syntax"></a>Syntax

```
mklink [[/d] | [/h] | [/j]] <link> <target>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /d | Erstellt einen symbolischen Verzeichnis Link. Standardmäßig erstellt dieser Befehl einen symbolischen Datei Link. |
| /h | Erstellt einen festen Link anstelle eines symbolischen Links. |
| /j | Erstellt eine Verzeichnis Verknüpfung. |
| `<link>` | Gibt den Namen der symbolischen Verknüpfung an, die erstellt wird. |
| `<target>` | Gibt den Pfad (relative oder absolute) an, auf den die neue symbolische Verknüpfung verweist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Erstellen und Entfernen einer symbolischen Verknüpfung mit dem Namen "MyFolder" und "MyFile. File" aus dem Stammverzeichnis in das Verzeichnis "\Users\User1\Documents" und eine Datei im Verzeichnis "example." geben Sie Folgendes ein:

```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "del"](del.md)

- [RD-Befehl](rd.md)

- [New-Item in Windows PowerShell](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
