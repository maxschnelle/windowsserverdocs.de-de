---
title: bitsadmin anhalten
description: Windows-Befehls Thema für **bigsadmin Suspend**, wodurch der angegebene Auftrag angehalten wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42ed83d4dbf8c3d982c5c186b440cf17997903c9
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123152"
---
# <a name="bitsadmin-suspend"></a>bitsadmin anhalten

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hält den angegebenen Auftrag an. Wenn Sie den Auftrag versehentlich angehalten haben, können Sie den Auftrag mit dem Umschalter [bigsadmin Resume](bitsadmin-resume.md) neu starten.

## <a name="syntax"></a>Syntax

```
bitsadmin /suspend <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ---------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="example"></a>Beispiel

Im folgenden Beispiel wird der Auftrag mit dem Namen *mydownloadjob*angehalten.


```
C:\>bitsadmin /suspend myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
