---
title: manage-bde forcerecovery
description: Referenz Artikel für den Befehl manage-bde forcerecovery, der beim Neustart ein durch BitLocker geschütztes Laufwerk in den Wiederherstellungs Modus erzwingt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eecae37c-c9a3-46c5-b615-a0ace1f1d778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d6c9cc9f851d2147cd23e8cc2e6baf3021fdd4c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935380"
---
# <a name="manage-bde-forcerecovery"></a>manage-bde forcerecovery

Erzwingt ein durch BitLocker geschütztes Laufwerk beim Neustart in den Wiederherstellungs Modus. Dieser Befehl löscht alle Trusted Platform Module (TPM)-bezogenen Schlüssel Schutzvorrichtungen vom Laufwerk. Wenn der Computer neu gestartet wird, kann nur ein Wiederherstellungs Kennwort oder ein Wiederherstellungs Schlüssel verwendet werden, um das Laufwerk zu entsperren.

## <a name="syntax"></a>Syntax

```
manage-bde –forcerecovery <drive> [-computername <name>] [{-?|/?}] [{-help|-h}]
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

Um BitLocker im Wiederherstellungs Modus auf Laufwerk C zu starten, geben Sie Folgendes ein:

```
manage-bde –forcerecovery C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
