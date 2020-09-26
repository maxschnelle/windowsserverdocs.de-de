---
title: rundll32
description: Referenz Artikel für den rundll32-Befehl, der 32-Bit-DLLs (Dynamic-Link Libraries) lädt und ausführt.
ms.topic: reference
ms.assetid: 46d9cd64-8186-4cd4-a500-44700340fe81
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 95bcb4984c3488b2c00a588d972941b4eb840fdb
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388414"
---
# <a name="rundll32"></a>rundll32

Lädt und führt 32-Bit-DLLs (Dynamic-Link Libraries) aus. Für rundll32 gibt es keine konfigurierbaren Einstellungen. Hilfe Informationen werden für eine bestimmte dll bereitgestellt, die Sie mit dem **rundll32** -Befehl ausführen.

Sie müssen den **rundll32** -Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen. Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten auf **Start**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.

## <a name="syntax"></a>Syntax

```
rundll32 <DLLname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [Rundll32 printui.dll, PrintUIEntry](rundll32-printui.md) | Zeigt die Benutzeroberfläche des Druckers an. |

## <a name="remarks"></a>Hinweise

Rundll32 kann nur Funktionen aus einer DLL aufrufen, die explizit für das Aufrufen durch rundll32 geschrieben wurde.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
