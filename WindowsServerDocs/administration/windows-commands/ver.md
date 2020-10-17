---
title: ver
description: Referenz Artikel für den Befehl "Ver", in dem die Versionsnummer des Betriebssystems angezeigt wird.
ms.topic: reference
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9e99c5af9ee45b33cb0c050307c83c89874d89cb
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156270"
---
# <a name="ver"></a>ver

Zeigt die Versionsnummer des Betriebssystems an. Dieser Befehl wird in der Windows-Eingabeaufforderung (Cmd.exe), jedoch nicht in PowerShell unterstützt.

## <a name="syntax"></a>Syntax

```
ver
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Versionsnummer des Betriebssystems von der Befehlsshell (cmd.exe) abzurufen:

```
ver
```

Der Befehl " **ver** " funktioniert nicht in PowerShell. Wenn Sie die Versionsnummer des Betriebssystems über PowerShell erhalten möchten, geben Sie Folgendes ein:

```powershell
$PSVersionTable.BuildVersion
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
