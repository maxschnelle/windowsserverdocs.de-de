---
title: manage-bde-Spezifizierer
description: Referenz Thema für den Befehl manage-bde setidentifier, der das Feld Laufwerks-ID auf dem Laufwerk auf den Wert festlegt, der in der Einstellung geben Sie die eindeutigen Bezeichner für Ihre Organisation Gruppenrichtlinie festgelegt ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7092d18f-4ac9-4c73-a20f-1246ca60e75e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b4a21df9d177d7bf6813abb0d418d7355d5e59a
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222607"
---
# <a name="manage-bde-setidentifier"></a>manage-bde-Spezifizierer

Legt das Feld Laufwerks-ID auf dem Laufwerk auf den Wert fest, der in der Einstellung **Geben Sie die eindeutigen Bezeichner für Ihre Organisation** Gruppenrichtlinie festgelegt ist.

## <a name="syntax"></a>Syntax

```
manage-bde –setidentifier <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
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

Geben Sie Folgendes ein, um das BitLocker-Laufwerk Bezeichner für C festzulegen:

```
manage-bde –setidentifier C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)

- [Leitfaden zur BitLocker-Wiederherstellung](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-recovery-guide-plan)
