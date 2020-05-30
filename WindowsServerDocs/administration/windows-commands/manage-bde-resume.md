---
title: manage-bde Resume
description: Referenz Thema für den Befehl "manage-bde Resume", mit dem die BitLocker-Verschlüsselung oder-Entschlüsselung fortgesetzt wird, nachdem Sie angehalten wurde.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ca3cd1ca-6f2c-4190-b68f-27816635facb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 17a41a0a5c97bb20c1010c968e495ffbc81649cf
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222118"
---
# <a name="manage-bde-resume"></a>manage-bde Resume

Setzt die BitLocker-Verschlüsselung oder-Entschlüsselung fort, nachdem Sie angehalten wurde.

## <a name="syntax"></a>Syntax

```
manage-bde -resume [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Computername | Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Fortsetzen der BitLocker-Verschlüsselung auf Laufwerk C geben Sie Folgendes ein:

```
manage-bde –resume C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "manage-bde on"](manage-bde-on.md)

- [Befehl "manage-bde Off"](manage-bde-off.md)

- [Befehl "manage-bde Pause"](manage-bde-pause.md)

- [Befehl "Manage-BDE"](manage-bde.md)
