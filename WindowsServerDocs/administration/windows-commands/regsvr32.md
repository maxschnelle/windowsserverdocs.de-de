---
title: regsvr32
description: Referenz Artikel für den regsvr32-Befehl, der DLL-Dateien als Befehls Komponenten in der Registrierung registriert.
ms.topic: reference
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 670953ecb5de087d660c2d3b1b504e7301245b96
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639848"
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
