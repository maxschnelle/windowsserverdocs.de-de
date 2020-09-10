---
title: bitsadmin setreplyfilename
description: Referenz Artikel für den BITSAdmin-Befehl "* treplyfilename", der den Pfad der Datei angibt, in der der Server Upload-Reply enthalten ist.
ms.topic: reference
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e517b3b09e287d4364763b433e3209bf8d4794d6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630643"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

Gibt den Pfad der Datei an, in der der Server Upload-Reply enthalten ist.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /setreplyfilename <job> <file_path>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| file_path | Speicherort für den Server Upload-Reply. |

## <a name="examples"></a>Beispiele

So legen Sie den Datei Pfad für den Upload-Reply-Dateinamen für den Auftrag *mydownloadjob*fest:

```
bitsadmin /setreplyfilename myDownloadJob c:\upload-reply
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
