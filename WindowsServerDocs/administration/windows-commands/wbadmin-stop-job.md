---
title: wbadmin stop job
description: Referenz Artikel für den Befehl "Befehl zum Abbrechen von Wbadmin", mit dem der derzeit laufende Sicherungs-oder Wiederherstellungs Vorgang abgebrochen wird.
ms.topic: reference
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9952f28f674da6eae295dcffc0357cade19fdd1c
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524705"
---
# <a name="wbadmin-stop-job"></a>wbadmin stop job

Bricht den Sicherungs-oder Wiederherstellungs Vorgang ab, der derzeit ausgeführt wird.

> [!IMPORTANT]
> Abgebrochene Vorgänge können nicht neu gestartet werden. Sie müssen eine abgebrochene Sicherung oder einen Wiederherstellungs Vorgang von Anfang an ausführen.

Um einen Sicherungs-oder Wiederherstellungs Vorgang mit diesem Befehl zu verhindern, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

## <a name="syntax"></a>Syntax

```
wbadmin stop job [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)
