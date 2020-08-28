---
title: manage-bde Entsperrens
description: Referenz Artikel für den Befehl manage-bde Entsperrens, der das automatische Entsperren von mit BitLocker geschützten Daten Laufwerken verwaltet.
ms.topic: reference
ms.assetid: 063528bf-d235-4b44-887a-52a7d983e01a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 35aadb406a2f5d9e10bd7b796dd07ae79a8286a7
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89036548"
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
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das automatische Entsperren von Daten Laufwerk E zu aktivieren:

```
manage-bde –autounlock -enable E:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)