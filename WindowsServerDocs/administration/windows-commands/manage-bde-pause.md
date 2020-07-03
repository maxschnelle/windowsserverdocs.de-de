---
title: manage-bde Pause
description: Referenz Artikel für den Befehl manage-bde Pause, der die BitLocker-Verschlüsselung oder-Entschlüsselung anhält.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: efda0e08-b9ff-4e71-83d8-bb666b3032bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 244d18ff9763ccb12c9567fbab68e2fd72f0f076
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935462"
---
# <a name="manage-bde-pause"></a>manage-bde Pause

Hält die BitLocker-Verschlüsselung oder-Entschlüsselung an.

## <a name="syntax"></a>Syntax

```
manage-bde -pause [<volume>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<volume>` | Gibt einen Laufwerk Buchstaben an, gefolgt von einem Doppelpunkt, einem Volume-GUID-Pfad oder einem bereitgestellten Volume. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die BitLocker-Verschlüsselung auf Laufwerk C anzuhalten:

```
manage-bde pause C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "manage-bde on"](manage-bde-on.md)

- [Befehl "manage-bde Off"](manage-bde-off.md)

- [Befehl "manage-bde Resume"](manage-bde-resume.md)

- [Befehl "Manage-BDE"](manage-bde.md)
