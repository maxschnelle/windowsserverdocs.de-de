---
title: wbadmin disable backup
description: Referenz Artikel für den Befehl Wbadmin-Sicherung deaktivieren, der die Ausführung der vorhandenen geplanten täglichen Sicherungen beendet.
ms.topic: reference
ms.assetid: 5176cbd9-0696-4b3f-9c35-272dd84f7898
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f490ede3b6f48285291b1658458d8c8c176bb2c8
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156041"
---
# <a name="wbadmin-disable-backup"></a>wbadmin disable backup

Beendet die Ausführung der vorhandenen geplanten täglichen Sicherungen.

Um eine geplante tägliche Sicherung mit diesem Befehl zu deaktivieren, müssen Sie Mitglied der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

## <a name="syntax"></a>Syntax

```
wbadmin disable backup [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Wbadmin-Befehl zum Aktivieren der Sicherung](wbadmin-enable-backup.md)