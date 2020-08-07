---
title: manage-bde wipeer FreeSpace
description: Referenz Artikel für den Befehl manage-bde wipeer FreeSpace, mit dem der freie Speicherplatz auf dem Volume gelöscht wird, wodurch alle Daten Fragmente entfernt werden, die möglicherweise im Speicherplatz vorhanden sind.
ms.topic: article
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca4737eae6c152ac01e674efb3e674c88f5d1538
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886580"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde wipeer FreeSpace

Löscht den freien Speicherplatz auf dem Volume und entfernt alle Daten Fragmente, die möglicherweise im Speicherplatz vorhanden sind. Das Ausführen dieses Befehls auf einem Volume, das mithilfe der Verschlüsselungsmethode " **nur verwendeten Speicherplatz** verschlüsseln" verschlüsselt wurde, bietet das gleiche Maß an Schutz wie die Verschlüsselungsmethode für die Verschlüsselung **ganzer** Volumes

## <a name="syntax"></a>Syntax

```
manage-bde -wipefreespace|-w [<drive>] [-cancel] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Abbrechen | Bricht eine Löschung des freien Speicherplatzes ab, der gerade verarbeitet wird. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Um den freien Speicherplatz auf Laufwerk C zu löschen, geben Sie Folgendes ein: \

```
manage-bde -w C:
```

```
manage-bde -wipefreespace C:
```

Um das Löschen des freien Speicherplatzes auf Laufwerk C aufzuheben, geben Sie Folgendes ein:

```
manage-bde -w -cancel C:
```

```
manage-bde -wipefreespace -cancel C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
