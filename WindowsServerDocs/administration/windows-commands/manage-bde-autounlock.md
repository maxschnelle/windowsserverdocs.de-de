---
title: manage-bde Entsperrens
description: Referenz Thema für den Befehl manage-bde Entsperrens, der das automatische Entsperren von mit BitLocker geschützten Daten Laufwerken verwaltet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 063528bf-d235-4b44-887a-52a7d983e01a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a214ba868e04a81e6282dc919c93ab626ef26725
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223001"
---
# <a name="manage-bde-autounlock"></a>manage-bde Entsperrens

Verwaltet das automatische Entsperren von mit BitLocker geschützten Daten Laufwerken.

## <a name="syntax"></a>Syntax

```
manage-bde -autounlock [{-enable|-disable|-clearallkeys}] <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -enable | Aktiviert das automatische Entsperren für ein Daten Laufwerk. |
| -disable | Deaktiviert das automatische Entsperren für ein Daten Laufwerk. |
| -clearallkeys | Entfernt alle gespeicherten externen Schlüssel auf dem Betriebssystem Laufwerk. |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Computername | Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das automatische Entsperren von Daten Laufwerk E zu aktivieren:

```
manage-bde –autounlock -enable E:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)