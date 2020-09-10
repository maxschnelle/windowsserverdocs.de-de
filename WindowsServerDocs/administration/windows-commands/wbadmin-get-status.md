---
title: wbadmin get status
description: Referenz Artikel zum Abrufen des Status von Wbadmin, mit dem der Status des Sicherungs-oder Wiederherstellungs Vorgangs gemeldet wird, der derzeit ausgeführt wird.
ms.topic: reference
ms.assetid: 2911b944-7b95-46aa-8c1e-1d55a2fcc94c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7dcb1b59de6827500311cfd55245ac6c94a171b0
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624598"
---
# <a name="wbadmin-get-status"></a>wbadmin get status



Meldet den Status des Sicherungs-oder Wiederherstellungs Vorgangs, der derzeit ausgeführt wird.

Um diesen Unterbefehl verwenden zu können, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin get status
```

### <a name="parameters"></a>Parameter

Dieser Unterbefehl weist keine Parameter auf.

## <a name="remarks"></a>Hinweise

-   Dieser Unterbefehl wird erst beendet, wenn der aktuelle Sicherungs-oder Wiederherstellungs Vorgang abgeschlossen ist – der Unterbefehl wird weiterhin ausgeführt, auch wenn Sie das Befehlsfenster schließen.
-   Wenn Sie den aktuellen Sicherungs-oder Wiederherstellungs Vorgang abbrechen möchten, verwenden Sie den Unterbefehl zum Abbrechen des Auftrags unter " **Wbadmin** ".

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-wbjob](/powershell/module/windowserverbackup/?view=winserver2012r2-ps) -Cmdlet
