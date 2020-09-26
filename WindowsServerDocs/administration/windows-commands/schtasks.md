---
title: schtasks-Befehle
description: Referenz Artikel zu den Schtasks-Befehlen, der Befehle und Programme plant, die in regelmäßigen Abständen oder zu einem bestimmten Zeitpunkt ausgeführt werden, Aufgaben aus dem Zeitplan hinzufügen und entfernen, Aufgaben bei Bedarf starten und beenden und geplante Aufgaben anzeigen und ändern.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/16/2020
ms.openlocfilehash: 50b0bd7f7a55a7aa5889c39e4bf9f4e582af7f3b
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388636"
---
# <a name="schtasks-commands"></a>schtasks-Befehle

Plant, dass Befehle und Programme regelmäßig oder zu einem bestimmten Zeitpunkt ausgeführt werden, Aufgaben aus dem Zeitplan hinzufügen und entfernen, Aufgaben bei Bedarf starten und beenden und geplante Aufgaben anzeigen und ändern.

> [!NOTE]
> Das **schtasks.exe** Tool führt die gleichen Vorgänge wie für **geplante Aufgaben** in der **Systemsteuerung**aus. Diese Tools können zusammen und austauschbar verwendet werden.

## <a name="required-permissions"></a>Erforderliche Berechtigungen

- Um alle Tasks auf dem lokalen Computer zu planen, anzuzeigen und zu ändern, müssen Sie Mitglied der Gruppe "Administratoren" sein.

- Um alle Tasks auf dem Remote Computer zu planen, anzuzeigen und zu ändern, müssen Sie Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein, oder Sie müssen den **/u** -Parameter verwenden, um die Anmelde Informationen eines Administrators für den Remote Computer anzugeben.

- Sie können den **/u** -Parameter in einem **/Create** -oder **/Change** -Vorgang verwenden, wenn sich der lokale Computer und der Remote Computer in derselben Domäne befinden oder wenn sich der lokale Computer in einer Domäne befindet, der die Remote Computer Domäne vertraut. Andernfalls kann der Remote Computer das angegebene Benutzerkonto nicht authentifizieren, und es kann nicht überprüft werden, ob das Konto Mitglied der Gruppe "Administratoren" ist.

- Der Task, den Sie ausführen möchten, muss über die entsprechende Berechtigung verfügen. Diese Berechtigungen variieren je nach Aufgabe. Standardmäßig werden Tasks mit den Berechtigungen des aktuellen Benutzers des lokalen Computers oder mit den Berechtigungen des Benutzers ausgeführt, der durch den **/u** -Parameter angegeben wird (sofern vorhanden). o Ausführen einer Aufgabe mit Berechtigungen eines anderen Benutzerkontos oder mit System Berechtigungen verwenden Sie den **/ru** -Parameter.

## <a name="syntax"></a>Syntax

```
schtasks change
schtasks create
schtasks delete
schtasks end
schtasks query
schtasks run
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [schtasks ändern](schtasks-change.md) | Ändert eine oder mehrere der folgenden Eigenschaften einer Aufgabe:<ul><li>Das Programm, das der Task ausführt (/TR)</li><li>Das Benutzerkonto, unter dem der Task ausgeführt wird (/ru)</li><li>Das Kennwort für das Benutzerkonto (/RP aus)</li><li>Fügt der Aufgabe die interaktive Eigenschaft hinzu (/IT).</li></ul> |
| [schtasks erstellen](schtasks-create.md) | Plant eine neue Aufgabe.|
| [schtasks löschen](schtasks-delete.md) | Löscht einen geplanten Task. |
| [schtasks beenden](schtasks-end.md) | Beendet ein Programm, das von einer Aufgabe gestartet wurde. |
| [schtasks-Abfrage](schtasks-query.md) | Zeigt Tasks an, die für die Ausführung auf dem Computer geplant sind. |
| [schtasks ausführen](schtasks-run.md) | Startet eine geplante Aufgabe sofort. Der **Ausführungs Vorgang ignoriert den Zeitplan** , verwendet jedoch den Programmdatei Speicherort, das Benutzerkonto und das Kennwort, die in der Aufgabe gespeichert sind, um den Task sofort auszuführen. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
