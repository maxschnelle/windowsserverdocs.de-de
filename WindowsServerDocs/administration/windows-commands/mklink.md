---
title: mklink
description: 'Windows-Befehls Thema für * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7a5f9b819f16d058feb1dee74a8408ed174e04c
ms.sourcegitcommit: b7f55949f166554614f581c9ddcef5a82fa00625
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2019
ms.locfileid: "72588042"
---
# <a name="mklink"></a>mklink
Erstellt eine symbolische Verknüpfung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
mklink [[/d] | [/h] | [/j]] <Link> <Target>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/d|Erstellt einen symbolischen Verzeichnis Link. Standardmäßig erstellt **mklink** einen symbolischen Datei Link.|
|/h|Erstellt einen festen Link anstelle eines symbolischen Links.|
|/j|Erstellt eine Verzeichnis Verknüpfung.|
|\<Link >|Gibt den Namen der symbolischen Verknüpfung an, die erstellt wird.|
|\<Target >|Gibt den Pfad (relative oder absolute) an, auf den die neue symbolische Verknüpfung verweist.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele

Das folgende Beispiel veranschaulicht das Erstellen und Entfernen einer symbolischen Verknüpfung mit dem Namen "MyFolder" und "MyFile. File" aus dem Stammverzeichnis in das Verzeichnis "\Users\User1\Documents" und eine Beispieldatei im Verzeichnis:
```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```
## <a name="additional-references"></a>Weitere Verweise
-   [New-Item](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
-   [del](https://docs.microsoft.com/windows-server/administration/windows-commands/del)
-   [rmdir](https://docs.microsoft.com/windows-server/administration/windows-commands/rd)
