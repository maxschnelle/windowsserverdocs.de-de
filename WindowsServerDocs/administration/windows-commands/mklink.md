---
title: mklink
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1ea80b81b268b31f637c72a828fee8b6f0229a47
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280025"
---
# <a name="mklink"></a>mklink
Erstellt eine symbolische Verknüpfung an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
mklink [[/d] | [/h] | [/j]] <Link> <Target>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/d|Erstellt einen symbolischen Link "Directory". In der Standardeinstellung **Mklink** erstellt einen symbollink für die Datei.|
|/h|Erstellt einen festen Link anstelle einer symbolischen Verknüpfung an.|
|/j|Erstellt eine Verbindung Verzeichnis an.|
|\<Link>|Gibt den Namen der symbolischen Verknüpfung, die erstellt wird.|
|\<Target>|Gibt den Pfad (relativ oder absolut), dem auf die neue symbolische Verknüpfung verweist.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel veranschaulicht die Erstellung und Entfernung von eine symbolische Verknüpfung mit dem Namen MyFolder und MyFile.file aus dem Stammverzeichnis zu dem Verzeichnis \Users\User1\Documents und eine example.file befindet sich im Verzeichnis:
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
