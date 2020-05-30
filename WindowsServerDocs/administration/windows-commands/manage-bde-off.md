---
title: manage-bde Off
description: Referenz Thema für den Befehl manage-bde off, mit dem das Laufwerk entschlüsselt und BitLocker ausgeschaltet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a27c119-d385-45e5-89fe-e311d4429876
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cbcec0cadba870a5f416af50f12e0b2c5eed6d95
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222866"
---
# <a name="manage-bde-off"></a>manage-bde Off

Entschlüsselt das Laufwerk und deaktiviert BitLocker. Alle Schlüssel Schutzvorrichtungen werden entfernt, wenn die Entschlüsselung vollständig ist.

## <a name="syntax"></a>Syntax

```
manage-bde -off [<volume>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<volume>` | Gibt einen Laufwerk Buchstaben an, gefolgt von einem Doppelpunkt, einem Volume-GUID-Pfad oder einem bereitgestellten Volume. |
| -Computername | Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um BitLocker auf Laufwerk C zu deaktivieren:

```
manage-bde –off C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "manage-bde on"](manage-bde-on.md)

- [Befehl "manage-bde Pause"](manage-bde-pause.md)

- [Befehl "manage-bde Resume"](manage-bde-resume.md)

- [Befehl "Manage-BDE"](manage-bde.md)
