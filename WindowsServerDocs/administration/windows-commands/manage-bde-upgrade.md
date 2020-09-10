---
title: manage-bde-Upgrade
description: Referenz Artikel für den Befehl manage-bde Upgrade, mit dem die BitLocker-Version aktualisiert wird.
ms.topic: reference
ms.assetid: 23bfa824-6ff0-44cc-9b8b-b199a769fb8d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a031c06068a8dc1b66b4065e19d85ab5b62ea7e6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635251"
---
# <a name="manage-bde-upgrade"></a>manage-bde-Upgrade

Aktualisiert die BitLocker-Version.

## <a name="syntax"></a>Syntax

```
manage-bde -upgrade [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Zum Aktualisieren der BitLocker-Verschlüsselung auf Laufwerk C geben Sie Folgendes ein:

```
manage-bde –upgrade C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
