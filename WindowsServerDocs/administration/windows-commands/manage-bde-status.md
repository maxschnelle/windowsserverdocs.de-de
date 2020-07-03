---
title: manage-bde-Status
description: Referenz Artikel zum Befehl "manage-bde Status", der Informationen zu allen Laufwerken auf dem Computer bereitstellt, unabhängig davon, ob Sie durch BitLocker geschützt sind.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20430899b8259207f228219cf0d2ac516866714a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922215"
---
# <a name="manage-bde-status"></a>manage-bde-Status

Enthält Informationen zu allen Laufwerken auf dem Computer. unabhängig davon, ob Sie durch BitLocker geschützt sind, einschließlich:

- Size

- BitLocker-Version

- Konvertierungs Status

- Verschlüsselter Prozentsatz

- Verschlüsselungsmethode

- Schutzstatus

- Sperr Status

- Identifikations Feld

- Schlüssel Schutzvorrichtungen

## <a name="syntax"></a>Syntax

```
manage-bde -status [<drive>] [-protectionaserrorlevel] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -schutzaserrorlevel | Bewirkt, dass das Befehlszeilen Tool manage-bde den Rückgabecode **0** (null) sendet, wenn das Volume geschützt ist, und **1** , wenn das Volume nicht geschützt ist. wird am häufigsten für Batch Skripts verwendet, um zu bestimmen, ob ein Laufwerk durch BitLocker geschützt ist. Sie können auch **-p** als abgekürzte Version dieses Befehls verwenden. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Status von Laufwerk C anzuzeigen:

```
manage-bde –status C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
