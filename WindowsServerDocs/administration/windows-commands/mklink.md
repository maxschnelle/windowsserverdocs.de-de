---
title: mklink
description: 'Windows-Befehle Thema ***- '
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
ms.openlocfilehash: eabbf159a64ab5df7f45ece390d0c2fdb9956b80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826331"
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

Um eine symbolische Verknüpfung mit dem Namen MyDocs aus dem Stammverzeichnis, in das Verzeichnis \Users\User1\Documents zu erstellen, geben Sie Folgendes ein:
```
mklink /d \MyDocs \Users\User1\Documents
```
## <a name="additional-references"></a>Weitere Verweise
-   [New-Item](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
