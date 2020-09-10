---
title: manage-bde ChangeKey
description: Referenz Artikel für den Befehl manage-bde ChangeKey, mit dem der Systemstart Schlüssel für ein Betriebssystem Laufwerk geändert wird.
ms.topic: reference
ms.assetid: 69463db9-7e03-47ff-b233-a95d5055725f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3752d0a3a990488129b99a5ebbe44e830552c00f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622748"
---
# <a name="manage-bde-changekey"></a>manage-bde ChangeKey

Ändert den Systemstart Schlüssel für ein Betriebssystem Laufwerk.

## <a name="syntax"></a>Syntax

```
manage-bde -changekey [<drive>] [<pathtoexternalkeydirectory>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen neuen Systemstart Schlüssel auf Laufwerk E für die Verwendung mit der BitLocker-Verschlüsselung auf Laufwerk C zu erstellen:

```
manage-bde -changekey C: E:\
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
