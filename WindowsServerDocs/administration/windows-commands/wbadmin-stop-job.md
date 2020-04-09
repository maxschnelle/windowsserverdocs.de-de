---
title: Auftrag zum Abbrechen von Wbadmin
description: Windows-Befehle-Thema für den Auftrag zum Abbrechen von Wbadmin, mit dem der derzeit laufende Sicherungs-oder Wiederherstellungs Vorgang abgebrochen wird. Abgebrochene Vorgänge können nicht neu gestartet werden – Sie müssen einen abgebrochenen Sicherungs-oder Wiederherstellungs Vorgang von Anfang an erneut ausführen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a00b4a93e0aaa954f8f07adae825a4f582c5581
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829483"
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

|Parameter|Beschreibung|
|---------|-----------|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)