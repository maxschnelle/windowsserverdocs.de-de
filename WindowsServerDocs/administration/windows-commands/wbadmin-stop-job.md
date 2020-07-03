---
title: wbadmin stop job
description: Referenz Artikel für den Auftrag zum Abbrechen von Wbadmin, mit dem der derzeit laufende Sicherungs-oder Wiederherstellungs Vorgang abgebrochen wird. Abgebrochene Vorgänge können nicht neu gestartet werden – Sie müssen einen abgebrochenen Sicherungs-oder Wiederherstellungs Vorgang von Anfang an erneut ausführen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c6961b1fae425d06577fce3a93dca6262dd7127
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930878"
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

|Parameter|Beschreibung|
|---------|-----------|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)