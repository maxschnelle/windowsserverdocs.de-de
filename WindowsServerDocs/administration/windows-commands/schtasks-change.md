---
title: schtasks ändern
description: Referenz Artikel für den Schtasks-Änderungs Befehl, der Befehle und Programme plant, die in regelmäßigen Abständen oder zu einem bestimmten Zeitpunkt ausgeführt werden, Aufgaben aus dem Zeitplan hinzufügen und entfernen, Aufgaben bei Bedarf starten und beenden und geplante Aufgaben anzeigen und ändern.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/16/2020
ms.openlocfilehash: 06cbceaaa0e428743a725127d9495759dd0097e1
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91390772"
---
# <a name="schtasks-change"></a>schtasks ändern

Ändert eine oder mehrere der folgenden Eigenschaften einer Aufgabe:

- Das Programm, das der Task ausführt (**/TR**)

- Das Benutzerkonto, unter dem der Task ausgeführt wird (**/ru**)

- Das Kennwort für das Benutzerkonto (**/RP aus**)

- Fügt der Aufgabe die interaktive Eigenschaft hinzu (**/IT**).

## <a name="required-permissions"></a>Erforderliche Berechtigungen

- Um alle Tasks auf dem lokalen Computer zu planen, anzuzeigen und zu ändern, müssen Sie Mitglied der Gruppe "Administratoren" sein.

- Um alle Tasks auf dem Remote Computer zu planen, anzuzeigen und zu ändern, müssen Sie Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein, oder Sie müssen den **/u** -Parameter verwenden, um die Anmelde Informationen eines Administrators für den Remote Computer anzugeben.

- Sie können den **/u** -Parameter in einem **/Create** -oder **/Change** -Vorgang verwenden, wenn sich der lokale Computer und der Remote Computer in derselben Domäne befinden oder wenn sich der lokale Computer in einer Domäne befindet, der die Remote Computer Domäne vertraut. Andernfalls kann der Remote Computer das angegebene Benutzerkonto nicht authentifizieren, und es kann nicht überprüft werden, ob das Konto Mitglied der Gruppe "Administratoren" ist.

- Der Task, den Sie ausführen möchten, muss über die entsprechende Berechtigung verfügen. Diese Berechtigungen variieren je nach Aufgabe. Standardmäßig werden Tasks mit den Berechtigungen des aktuellen Benutzers des lokalen Computers oder mit den Berechtigungen des Benutzers ausgeführt, der durch den **/u** -Parameter angegeben wird (sofern vorhanden). o Ausführen einer Aufgabe mit Berechtigungen eines anderen Benutzerkontos oder mit System Berechtigungen verwenden Sie den **/ru** -Parameter.

## <a name="syntax"></a>Syntax

```
schtasks /change /tn <Taskname> [/s <computer> [/u [<domain>\]<user> [/p <password>]]] [/ru <username>] [/rp <password>] [/tr <Taskrun>] [/st <Starttime>] [/ri <interval>] [{/et <Endtime> | /du <duration>} [/k]] [/sd <Startdate>] [/ed <Enddate>] [/{ENABLE | DISABLE}] [/it] [/z]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /TN `<Taskname>` | Gibt die zu ändernde Aufgabe an. Geben Sie den Namen der Aufgabe ein. |
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u `[<domain>]` | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers auf dem lokalen Computer ausgeführt. Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter ohne den **/p** -Parameter oder das Password-Argument verwenden, werden Sie von schtasks aufgefordert, ein Kennwort einzugeben. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /ru `<username>` | Ändert den Benutzernamen, unter dem die geplante Aufgabe ausgeführt werden muss. Gültige Werte für das Systemkonto sind *""*, *"NT-Autorität \ System"* oder *"System"*. |
| /RP aus `<password>` | Gibt ein neues Kennwort für das vorhandene Benutzerkonto oder das durch den **/ru** -Parameter angegebene Benutzerkonto an. Dieser Parameter wird ignoriert, wenn er mit dem lokalen System Konto verwendet wird. |
| /tr `<Taskrun>` | Ändert das Programm, das der Task ausführt. Geben Sie den voll qualifizierten Pfad und den Dateinamen einer ausführbaren Datei, einer Skriptdatei oder einer Batchdatei ein. Wenn Sie den Pfad nicht hinzufügen, geht **Schtasks** davon aus, dass sich die Datei im `<systemroot>\System32` Verzeichnis befindet. Das angegebene Programm ersetzt das ursprüngliche Programm, das durch den Task ausgeführt wird. |
| /St `<Starttime>` | Gibt die Startzeit für den Task an, wobei das 24-Stunden-Zeitformat HH: mm verwendet wird. Beispielsweise entspricht der Wert 14:30 der 12-Stunden-Zeit von 2:30 Uhr. |
| /ri `<interval>` | Gibt das Wiederholungsintervall für die geplante Aufgabe in Minuten an. Der gültige Bereich ist 1-599940 (599940 Minuten = 9999 Stunden). Wenn entweder der **/et** -Parameter oder der **/du** -Parameter angegeben wird, beträgt der Standardwert **10 Minuten**. |
| /et `<Endtime>` | Gibt die Endzeit für die Aufgabe mit dem 24-Stunden-Zeitformat HH: mm an. Beispielsweise entspricht der Wert 14:30 der 12-Stunden-Zeit von 2:30 Uhr. |
| /du `<duration>` | Ein-Wert, der die Dauer angibt, mit der der Task ausgeführt wird. Das Zeitformat ist hh: mm (24-Stunden-Zeit). Beispielsweise entspricht der Wert 14:30 der 12-Stunden-Zeit von 2:30 Uhr. |
| /k | Beendet das Programm, das der Task ausführt, zu dem Zeitpunkt, der durch **/et** oder **/du**angegeben wird. Ohne **/k**startet Schtasks das Programm nicht erneut, nachdem es die von **/et** oder **/du** angegebene Zeit erreicht hat, oder das Programm beendet, wenn es noch ausgeführt wird. Dieser Parameter ist optional und nur mit einem Minuten-oder stündlichen Zeitplan gültig. |
| /sd `<Startdate>` | Gibt das erste Datum an, an dem die Aufgabe ausgeführt werden soll. Das Datumsformat ist "mm/dd/yyyy". |
| /ed `<Enddate>` | Gibt das letzte Datum an, an dem die Aufgabe ausgeführt werden soll. Das Format ist "mm/dd/yyyy". |
| /ENABLE | Gibt an, dass die geplante Aufgabe aktiviert werden soll. |
| /Disable | Gibt an, dass die geplante Aufgabe deaktiviert werden soll. |
| /it | Gibt an, dass die geplante Aufgabe nur ausgeführt werden soll, wenn die Ausführung als Benutzer (das Benutzerkonto, unter dem der Task ausgeführt wird) auf dem Computer angemeldet ist. Dieser Parameter hat keine Auswirkung auf Aufgaben, die mit System Berechtigungen oder Tasks ausgeführt werden, für die die interaktive Eigenschaft bereits festgelegt ist. Sie können einen Change-Befehl nicht verwenden, um die interaktive Eigenschaft aus einer Aufgabe zu entfernen. Standardmäßig ist die Ausführung als Benutzer der aktuelle Benutzer des lokalen Computers, wenn der Task geplant ist, oder das durch den **/u** -Parameter angegebene Konto (sofern verwendet). Wenn der Befehl jedoch den **/ru** -Parameter enthält, ist das Konto "Ausführen als" das Konto, das durch den **/ru** -Parameter angegeben wird. |
| /z | Gibt an, dass die Aufgabe nach Abschluss des Zeitplans gelöscht wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Der Task wird durch die Parameter **/TN** und **/s** identifiziert. Die Parameter **/TR**, **/ru**und **/RP aus** geben die Eigenschaften der Aufgabe an, die Sie ändern können.

- Die Parameter **/ru** und **/RP aus** geben die Berechtigungen an, unter denen der Task ausgeführt wird. Die Parameter **/u** und **/p** geben die zum Ändern der Aufgabe verwendeten Berechtigungen an.

- Um Aufgaben auf einem Remote Computer zu ändern, muss der Benutzer auf dem lokalen Computer mit einem Konto angemeldet sein, das Mitglied der Gruppe "Administratoren" auf dem Remote Computer ist.

- Um einen **/Change** -Befehl mit den Berechtigungen eines anderen Benutzers (**/u**, **/p**) auszuführen, muss sich der lokale Computer in derselben Domäne befinden wie der Remote Computer, oder er muss sich in einer Domäne befinden, der die Remote Computer Domäne vertraut.

- Das System Konto verfügt nicht über interaktive Anmelde Rechte. Benutzern werden Programme mit System Berechtigungen nicht angezeigt, und Sie können nicht mit ihnen interagieren.
Verwenden Sie eine ausführliche Abfrage (**/Query "aus/v**), um Tasks mit der **/IT** -Eigenschaft zu identifizieren. In einer ausführlichen Abfrage Anzeige einer Aufgabe mit **/IT**hat das Feld Anmeldemodus den Wert interaktiv.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Programm zu ändern, von dem der Virus Check Task ausgeführt wird, *VirusCheck.exe* auf *VirusCheck2.exe*.

```
schtasks /change /tn Virus Check /tr C:\VirusCheck2.exe
```

Dieser Befehl verwendet den **/TN** -Parameter, um die Aufgabe zu identifizieren, und den **/TR** -Parameter, um das neue Programm für die Aufgabe anzugeben. (Sie können den Namen der Aufgabe nicht ändern.)

Um das Kennwort des Benutzerkontos für die *RemindMe* -Aufgabe auf dem Remote Computer, *Svr01*, zu ändern, geben Sie Folgendes ein:

```
schtasks /change /tn RemindMe /s Svr01 /rp p@ssWord3
```

Dieses Verfahren ist erforderlich, wenn das Kennwort für ein Benutzerkonto abläuft oder geändert wird. Wenn das in einer Aufgabe gespeicherte Kennwort nicht mehr gültig ist, wird der Task nicht ausgeführt. Der Befehl verwendet den **/TN** -Parameter, um den Task zu identifizieren, und den **/s** -Parameter, um den Remote Computer anzugeben. Er verwendet den **/RP aus** -Parameter, um das neue Kennwort anzugeben *p@ssWord3* .

Um die ChkNews-Aufgabe zu ändern, Notepad.exe die jeden Tag um 9:00 Uhr morgens gestartet wird, geben Sie Folgendes ein, um Internet Explorer zu starten:

```
schtasks /change /tn ChkNews /tr c:\program files\Internet Explorer\iexplore.exe /ru DomainX\Admin01
```

Der Befehl verwendet den **/TN** -Parameter, um die Aufgabe zu identifizieren. Er verwendet den **/TR** -Parameter, um das Programm zu ändern, das der Task ausführt, und den/ru-Parameter, um das Benutzerkonto zu ändern, unter dem der Task ausgeführt wird. Die Parameter **/ru** und **/RP aus** , die das Kennwort für das Benutzerkonto bereitstellen, werden nicht verwendet. Sie müssen ein Kennwort für das Konto angeben. Sie können jedoch den Parameter **/ru** und **/RP aus** verwenden und das Kennwort als Klartext eingeben oder auf SchTasks.exe warten, um Sie zur Eingabe eines Kennworts aufzufordern, und dann das Kennwort in verdeckten Text eingeben.

Geben Sie Folgendes ein, um den Task "securityscript" so zu ändern, dass er mit Berechtigungen für das System Konto ausgeführt wird:

```
schtasks /change /tn SecurityScript /ru
```

Der Befehl verwendet den **/ru** -Parameter, um das System Konto anzugeben. Da für Aufgaben, die mit System Konto Berechtigungen ausgeführt werden, kein Kennwort erforderlich ist, werden SchTasks.exe nicht zur Eingabe eines Kennworts aufgefordert.

Zum Hinzufügen der interaktiven Eigenschaft zu MyApp geben Sie eine vorhandene Aufgabe ein, und geben Sie Folgendes ein:

```
schtasks /change /tn MyApp /it
```

Diese Eigenschaft stellt sicher, dass der Task nur ausgeführt wird, wenn die Ausführung als Benutzer, d. h. das Benutzerkonto, unter dem der Task ausgeführt wird, auf dem Computer angemeldet ist. Der Befehl verwendet den **/TN** -Parameter, um die Aufgabe zu identifizieren, und den **/IT** -Parameter, um der Aufgabe die interaktive Eigenschaft hinzuzufügen. Da der Task bereits mit den Berechtigungen des Benutzerkontos ausgeführt wird, müssen Sie den **/ru** -Parameter für die Aufgabe nicht ändern.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "schtasks create"](schtasks-create.md)

- [Befehl "Schtasks löschen"](schtasks-delete.md)

- [schtasks-Befehl "Ende"](schtasks-end.md)

- [schtasks-Abfragebefehl](schtasks-query.md)

- [Befehl "Schtasks ausführen"](schtasks-run.md)
