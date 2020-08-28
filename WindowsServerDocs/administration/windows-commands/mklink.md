---
title: mklink
description: Referenz Artikel für den mklink-Befehl, mit dem ein Verzeichnis oder eine Datei als symbolischer oder fester Link erstellt wird.
ms.topic: reference
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13d842dcad62392fa36dc705233f292b7aa1d48f
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037818"
---
# <a name="mklink"></a>mklink

Erstellt einen symbolischen oder festen Link für ein Verzeichnis oder eine Datei.

## <a name="syntax"></a>Syntax

```
mklink [[/d] | [/h] | [/j]] <link> <target>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "del"](del.md)

- [RD-Befehl](rd.md)

- [New-Item in Windows PowerShell](/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
