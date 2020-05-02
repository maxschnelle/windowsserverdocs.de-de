---
title: Auftrag zum Abbrechen von Wbadmin
description: Referenz Thema für den Auftrag zum Abbrechen von Wbadmin, mit dem der derzeit laufende Sicherungs-oder Wiederherstellungs Vorgang abgebrochen wird. Abgebrochene Vorgänge können nicht neu gestartet werden – Sie müssen einen abgebrochenen Sicherungs-oder Wiederherstellungs Vorgang von Anfang an erneut ausführen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3133688ac0d60d97d80192611c9b561c53a74c35
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725841"
---
# <a name="wbadmin-stop-job"></a>Auftrag zum Abbrechen von Wbadmin



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

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)