---
title: manage-bde Resume
description: Referenz Artikel für den Befehl manage-bde Resume, mit dem die BitLocker-Verschlüsselung oder-Entschlüsselung fortgesetzt wird, nachdem Sie angehalten wurde.
ms.topic: reference
ms.assetid: ca3cd1ca-6f2c-4190-b68f-27816635facb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 57f12ad478e565fa8edbeed0818e83b62c2d17fb
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027498"
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
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Fortsetzen der BitLocker-Verschlüsselung auf Laufwerk C geben Sie Folgendes ein:

```
manage-bde –resume C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "manage-bde on"](manage-bde-on.md)

- [Befehl "manage-bde Off"](manage-bde-off.md)

- [Befehl "manage-bde Pause"](manage-bde-pause.md)

- [Befehl "Manage-BDE"](manage-bde.md)
