---
title: manage-bde ChangePassword
description: Referenz Artikel für den Befehl manage-bde ChangePassword, der das Kennwort für ein Daten Laufwerk ändert.
ms.topic: reference
ms.assetid: b174e152-8442-4fba-8b33-56a81ff4f547
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8c262b6ca123d76af6ebdca09e5546f41350686d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622704"
---
# <a name="manage-bde-changepassword"></a>manage-bde ChangePassword

Ändert das Kennwort für ein Daten Laufwerk. Der Benutzer wird aufgefordert, ein neues Kennwort einzugeben.

## <a name="syntax"></a>Syntax

```
manage-bde -changepassword [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
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

Geben Sie Folgendes ein, um das Kennwort zu ändern, das zum Entsperren von BitLocker auf dem Daten Laufwerk D

```
manage-bde –changepassword D:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
