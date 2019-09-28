---
title: rundll32
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46d9cd64-8186-4cd4-a500-44700340fe81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29a87f9f07c25a0c671e47550e0a054d8308f747
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384416"
---
# <a name="rundll32"></a>rundll32



Lädt und führt 32-Bit-DLLs (Dynamic-Link Libraries) aus. Für rundll32 gibt es keine konfigurierbaren Einstellungen. Hilfe Informationen werden für eine bestimmte dll bereitgestellt, die Sie mit dem **rundll32** -Befehl ausführen.

Sie müssen den **rundll32** -Befehl an einer Eingabeaufforderung mit erhöhten Rechten ausführen. Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten auf **Start**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.

## <a name="syntax"></a>Syntax

```
Rundll32 <DLLname>
```

## <a name="commands"></a>Befehle

|Parameter|Beschreibung|
|---------|-----------|
|[Rundll32 printui. dll, PrintUIEntry](rundll32-printui.md)|Zeigt die Benutzeroberfläche des Druckers an|

## <a name="remarks"></a>Hinweise

Rundll32 kann nur Funktionen aus einer DLL aufrufen, die explizit zum Aufrufen durch rundll32 geschrieben wurden. Weitere Informationen zu rundll32-Anforderungen finden Sie in der Microsoft Knowledge Base im [Artikel 164787](https://go.microsoft.com/fwlink/?LinkID=165773) (https://go.microsoft.com/fwlink/?LinkID=165773).

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)