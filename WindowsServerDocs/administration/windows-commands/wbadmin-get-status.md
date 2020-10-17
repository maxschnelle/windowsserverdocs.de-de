---
title: wbadmin get status
description: Referenz Artikel für den Befehl "Get Status" von Wbadmin, der den Status des aktuell laufenden Sicherungs-oder Wiederherstellungs Vorgangs meldet.
ms.topic: reference
ms.assetid: 2911b944-7b95-46aa-8c1e-1d55a2fcc94c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 764c5d3dc808b12488e36af5808acf4c895c5af1
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155940"
---
# <a name="wbadmin-get-status"></a>wbadmin get status

Meldet den Status des Sicherungs-oder Wiederherstellungs Vorgangs, der derzeit ausgeführt wird.

Sie müssen Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, um den Status des zurzeit laufenden Sicherungs-oder Wiederherstellungs Vorgangs mit diesem Befehl abrufen zu können, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

> [!IMPORTANT]
> Dieser Befehl wird erst beendet, wenn der Sicherungs-oder Wiederherstellungs Vorgang abgeschlossen ist. Der Befehl wird weiterhin ausgeführt, auch wenn Sie das Befehlsfenster schließen. Um den aktuellen Sicherungs-oder Wiederherstellungs Vorgang zu starten, führen Sie den Befehl Befehl zum [Abbrechen von Wbadmin](wbadmin-stop-job.md) aus.

## <a name="syntax"></a>Syntax

```
wbadmin get status
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Befehl "Auftrag zum Abbrechen von Wbadmin"](wbadmin-stop-job.md)

- [Get-wbjob](/powershell/module/windowserverbackup/Get-WBJob)
