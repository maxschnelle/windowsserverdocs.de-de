---
title: mklink
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4bfa1c928b5bc5f4c5a885378f0f1d1c9b99cf5
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437135"
---
# <a name="mklink"></a>mklink
Erstellt eine symbolische Verknüpfung.



## <a name="syntax"></a>Syntax

```
mklink [[/d] | [/h] | [/j]] <Link> <Target>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/d|Erstellt einen symbolischen Verzeichnis Link. Standardmäßig erstellt **mklink** einen symbolischen Datei Link.|
|/h|Erstellt einen festen Link anstelle eines symbolischen Links.|
|/j|Erstellt eine Verzeichnis Verknüpfung.|
|\<Link>|Gibt den Namen der symbolischen Verknüpfung an, die erstellt wird.|
|\<Target>|Gibt den Pfad (relative oder absolute) an, auf den die neue symbolische Verknüpfung verweist.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Veranschaulicht das Erstellen und Entfernen einer symbolischen Verknüpfung mit dem Namen "MyFolder" und "MyFile. File" aus dem Stammverzeichnis in das Verzeichnis "\Users\User1\Documents" und eine Beispieldatei im Verzeichnis:
```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [New-Item](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
-   [del](https://docs.microsoft.com/windows-server/administration/windows-commands/del)
-   [rmdir](https://docs.microsoft.com/windows-server/administration/windows-commands/rd)
