---
title: bitsadmin setreplyfilename
description: Referenz Artikel für den BITSAdmin-Befehl "* treplyfilename", der den Pfad der Datei angibt, in der der Server Upload-Reply enthalten ist.
ms.topic: reference
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2991503ad558b318f52d07447af18d4f9e6178aa
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033418"
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

| Parameter | Beschreibung |
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
