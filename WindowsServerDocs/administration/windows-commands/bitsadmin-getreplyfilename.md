---
title: bitsadmin getreplyfilename
description: Referenz Thema für den BITSAdmin getreplyfilename-Befehl, mit dem der Pfad der Datei abgerufen wird, die die Server Upload-Antwort für den Auftrag enthält.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: daed755e0ddc045174b98a8d4f9ee84da155cba6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717594"
---
# <a name="bitsadmin-getreplyfilename"></a>bitsadmin getreplyfilename

Ruft den Pfad der Datei ab, die die Server Upload-Antwort für den Auftrag enthält.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getreplyfilename <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen des Datei namens "Upload-Reply" für den Auftrag " *mydownloadjob*":

```
bitsadmin /getreplyfilename myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
