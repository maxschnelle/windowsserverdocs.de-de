---
title: Wbadmin-Status "Get"
description: Windows-Befehls Artikel zum Abrufen des Status von Wbadmin, der den Status des aktuell laufenden Sicherungs-oder Wiederherstellungs Vorgangs meldet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2911b944-7b95-46aa-8c1e-1d55a2fcc94c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8ebf1a078632f78dc8d58c232550345f0de78f2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829743"
---
# <a name="wbadmin-get-status"></a>Wbadmin-Status "Get"



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

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-wbjob](https://technet.microsoft.com/library/jj902426.aspx) -Cmdlet