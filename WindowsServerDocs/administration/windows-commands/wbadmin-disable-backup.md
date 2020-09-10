---
title: wbadmin disable backup
description: Referenz Artikel für die Wbadmin-Sicherung deaktivieren, bei der die Ausführung der vorhandenen geplanten täglichen Sicherungen beendet wird.
ms.topic: reference
ms.assetid: 5176cbd9-0696-4b3f-9c35-272dd84f7898
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5525dc4c62900f2f250fc36670f83cefd0b55e35
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640754"
---
# <a name="wbadmin-disable-backup"></a>wbadmin disable backup



Beendet die Ausführung der vorhandenen geplanten täglichen Sicherungen.

Um eine geplante tägliche Sicherung zu deaktivieren, müssen Sie Mitglied der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung** und dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin disable backup
[-quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)