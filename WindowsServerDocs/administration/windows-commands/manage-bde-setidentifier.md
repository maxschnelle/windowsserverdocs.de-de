---
title: manage-bde-Spezifizierer
description: Referenz Artikel für den Befehl manage-bde setidentifier, mit dem das Feld Laufwerks-ID auf dem Laufwerk auf den Wert festgelegt wird, der im Feld Geben Sie die eindeutigen Bezeichner für Ihre Organisation Gruppenrichtlinie festgelegt ist.
ms.topic: reference
ms.assetid: 7092d18f-4ac9-4c73-a20f-1246ca60e75e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 861eca94cb15c70857138b6f9c76b5dcf59089a9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634343"
---
# <a name="manage-bde-setidentifier"></a>manage-bde-Spezifizierer

Legt das Feld Laufwerks-ID auf dem Laufwerk auf den Wert fest, der in der Einstellung **Geben Sie die eindeutigen Bezeichner für Ihre Organisation** Gruppenrichtlinie festgelegt ist.

## <a name="syntax"></a>Syntax

```
manage-bde –setidentifier <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
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

Geben Sie Folgendes ein, um das BitLocker-Laufwerk Bezeichner für C festzulegen:

```
manage-bde –setidentifier C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)

- [Leitfaden zur BitLocker-Wiederherstellung](/windows/security/information-protection/bitlocker/bitlocker-recovery-guide-plan)
