---
title: wbadmin stop job
description: Referenz Artikel für den Auftrag zum Abbrechen von Wbadmin, mit dem der derzeit laufende Sicherungs-oder Wiederherstellungs Vorgang abgebrochen wird. Abgebrochene Vorgänge können nicht neu gestartet werden – Sie müssen einen abgebrochenen Sicherungs-oder Wiederherstellungs Vorgang von Anfang an erneut ausführen.
ms.topic: reference
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7060fcac4c7a712695800534a23eddbcd043a4f8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633648"
---
# <a name="wbadmin-stop-job"></a>wbadmin stop job



Bricht den Sicherungs-oder Wiederherstellungs Vorgang ab, der derzeit ausgeführt wird. Abgebrochene Vorgänge können nicht neu gestartet werden – Sie müssen einen abgebrochenen Sicherungs-oder Wiederherstellungs Vorgang von Anfang an erneut ausführen.

Um einen Sicherungs-oder Wiederherstellungs Vorgang mit diesem Unterbefehl zu verhindern, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechende Berechtigung muss an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung** und dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin stop job
[-quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)