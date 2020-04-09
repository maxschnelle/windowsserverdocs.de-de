---
title: Wbadmin-Sicherung deaktivieren
description: Windows-Befehls Artikel für die Wbadmin-Sicherung deaktivieren, bei der die Ausführung der vorhandenen geplanten täglichen Sicherungen beendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5176cbd9-0696-4b3f-9c35-272dd84f7898
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2fb3d22fc3857cce191ee11381ae6e7e6ac1175
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829853"
---
# <a name="wbadmin-disable-backup"></a>Wbadmin-Sicherung deaktivieren



Beendet die Ausführung der vorhandenen geplanten täglichen Sicherungen.

Um eine geplante tägliche Sicherung zu deaktivieren, müssen Sie Mitglied der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung** und dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin disable backup
[-quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)