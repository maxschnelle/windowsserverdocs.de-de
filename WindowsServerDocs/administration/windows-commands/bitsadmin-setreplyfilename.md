---
title: bitsadmin setreplyfilename
description: Referenz Thema für den BITSAdmin-Befehl "* treplyfilename", der den Pfad der Datei angibt, in der der Server Upload-Reply enthalten ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f0bd184db274dc915817ff3e26ae2c686190c27
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720477"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
