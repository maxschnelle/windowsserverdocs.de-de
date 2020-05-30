---
title: logman delete
description: Referenz Thema für den logman delete-Befehl, mit dem ein vorhandener Datensammler gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18739f3d7ab5af38dbe369e45aca8393ba3a3152
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222946"
---
# <a name="logman-delete"></a>logman delete

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht einen vorhandenen Datensammler.

## <a name="syntax"></a>Syntax

```
logman delete <[-n] <name>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -s`<computer name>` | Führt den Befehl auf dem angegebenen Remote Computer aus. |
| -config`<value>` | Gibt die Einstellungsdatei an, die Befehlsoptionen enthält. |
| [-n]`<name>` | Name des Zielobjekts |
| -ETS | Sendet Befehle direkt an Ereignis Ablauf Verfolgungs Sitzungen, ohne zu speichern oder zu planen. |
| -[-] u`<user [password]>` | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie einen als Kennwort eingeben, wird \* eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, während Sie es an der Eingabeaufforderung eingeben. |
| /? | Zeigt die kontextbezogene Hilfe an. |

### <a name="examples"></a>Beispiele

Um den Datensammler *perf_log*zu löschen, geben Sie Folgendes ein:

```
logman delete perf_log
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)
