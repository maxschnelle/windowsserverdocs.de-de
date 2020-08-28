---
title: regsvr32
description: Referenz Artikel für den regsvr32-Befehl, der DLL-Dateien als Befehls Komponenten in der Registrierung registriert.
ms.topic: reference
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3bb39070ba1744ca261419e5b996144f89b17b11
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027422"
---
# <a name="regsvr32"></a>regsvr32

Registriert dll-Dateien als Befehls Komponenten in der Registrierung.

## <a name="syntax"></a>Syntax

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <Dllname>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
