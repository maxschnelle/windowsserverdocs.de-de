---
title: regsvr32
description: Referenz Artikel für den regsvr32-Befehl, der DLL-Dateien als Befehls Komponenten in der Registrierung registriert.
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a591813480163a6d43329222d20e2a29651f576
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883879"
---
# <a name="regsvr32"></a>regsvr32

Registriert dll-Dateien als Befehls Komponenten in der Registrierung.

## <a name="syntax"></a>Syntax

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <Dllname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /U | Hebt die Registrierung des Servers auf. |
| /s | Verhindert, dass Meldungen angezeigt werden. |
| /n | Verhindert das Aufrufen von " **DllRegisterServer**". Dieser Parameter erfordert, dass Sie auch den **/i** -Parameter verwenden. |
| /i`<cmdline>` | Übergibt eine optionale Befehlszeilen Zeichenfolge (*CmdLine*) an **DllInstall**. Wenn Sie diesen Parameter mit dem **/u** -Parameter verwenden, wird **DLLUninstall**aufgerufen. |
| `<Dllname>` | Der Name der DLL-Datei, die registriert wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die DLL für das Active Directory Schema zu registrieren:

```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
