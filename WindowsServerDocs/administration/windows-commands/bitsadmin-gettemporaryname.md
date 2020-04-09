---
title: bizadmin gettemporaryname
description: Windows-Befehls Thema für **bizadmin gettemporaryname**, der den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags meldet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c331ecf12cb02d34c76692158c79eafbe5691c5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850453"
---
# <a name="bitsadmin-gettemporaryname"></a>bizadmin gettemporaryname

Meldet den temporären Dateinamen der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /gettemporaryname <job> <file_index>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| file_index | Beginnt bei 0. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der temporäre Dateiname der Datei 2 für den Auftrag *mydownloadjob*gemeldet.

```
C:\>bitsadmin /gettemporaryname myDownloadJob 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)