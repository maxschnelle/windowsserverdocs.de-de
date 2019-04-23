---
title: rundll32
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5b1f288d21a1dcac25ecc00f685ea179d8a6542f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835031"
---
# <a name="rundll32"></a>rundll32



Lädt und 32-Bit-Dynamic Link Libraries (DLLs) führt. Es gibt keine konfigurierbaren Einstellungen für Rundll32. Hilfeinformationen gelten für eine bestimmte DLL, die Sie ausführen, mit der **rundll32** Befehl.

Führen Sie die **rundll32** eine Eingabeaufforderung mit erhöhten Rechten den Befehl. Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie auf **starten**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.

## <a name="syntax"></a>Syntax

```
Rundll32 <DLLname>
```

## <a name="commands"></a>Befehle

|Parameter|Beschreibung|
|---------|-----------|
|[printui.dll, rundll32 PrintUIEntry](rundll32-printui.md)|Zeigt die Benutzeroberfläche für den Drucker|

## <a name="remarks"></a>Hinweise

RUNDLL32 kann nur Funktionen aufrufen, aus einer DLL, die explizit von Rundll32 aufgerufen werden geschrieben werden. Weitere Informationen zu Rundll32 finden Sie unter [Artikel 164787](https://go.microsoft.com/fwlink/?LinkID=165773) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkID=165773).

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)