---
title: manage-bde Off
description: Referenz Artikel für den Befehl manage-bde off, mit dem das Laufwerk entschlüsselt und BitLocker ausgeschaltet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a27c119-d385-45e5-89fe-e311d4429876
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65749f31750b1f7467539b25b09061ea267636df
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935519"
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
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um BitLocker auf Laufwerk C zu deaktivieren:

```
manage-bde –off C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "manage-bde on"](manage-bde-on.md)

- [Befehl "manage-bde Pause"](manage-bde-pause.md)

- [Befehl "manage-bde Resume"](manage-bde-resume.md)

- [Befehl "Manage-BDE"](manage-bde.md)
