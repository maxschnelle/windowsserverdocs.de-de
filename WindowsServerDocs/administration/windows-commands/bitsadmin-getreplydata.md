---
title: bitsadmin getreplydata
description: Referenz Thema für den BITSAdmin getreplydata-Befehl, der die Upload-Antwort-Daten des Servers im Hexadezimal Format für den Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea2a82403fe05776abbbf65e87a4b6e72c8767b8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717627"
---
# <a name="bitsadmin-getreplydata"></a>bitsadmin getreplydata

Ruft die Upload-Antwort-Daten des Servers im Hexadezimal Format für den Auftrag ab.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getreplydata <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen der Upload-Antwort-Daten für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /getreplydata myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
