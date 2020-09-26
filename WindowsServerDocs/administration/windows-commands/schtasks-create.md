---
title: schtasks erstellen
description: Referenz Artikel für den Befehl "schtasks create", der
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/16/2020
ms.openlocfilehash: 4a7c3eb621f4c3d640fcb1f057b9d3cd00834e31
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91390780"
---
# <a name="schtasks-create"></a>schtasks erstellen

Plant einen Task.

## <a name="syntax"></a>Syntax

```
schtasks /create /sc <scheduletype> /tn <taskname> /tr <taskrun> [/s <computer> [/u [<domain>\]<user> [/p <password>]]] [/ru {[<domain>\]<user> | system}] [/rp <password>] [/mo <modifier>] [/d <day>[,<day>...] | *] [/m <month>[,<month>...]] [/i <idletime>] [/st <starttime>] [/ri <interval>] [{/et <endtime> | /du <duration>} [/k]] [/sd <startdate>] [/ed <enddate>] [/it] [/z] [/f]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /SC `<scheduletype>` | Gibt den Zeit Plantyp an. Gültige Werte sind:<ul><li>**Minute** : gibt die Anzahl der Minuten an, bevor der Task ausgeführt werden soll.</li><li>**Stündlich** : gibt die Anzahl der Stunden an, bevor der Task ausgeführt werden soll.</li><li>**Daily** : gibt die Anzahl der Tage an, bevor der Task ausgeführt werden soll.</li><li>**Wöchentlich** Gibt die Anzahl der Wochen an, bevor der Task ausgeführt werden soll.</li><li>**Monatlich** : gibt die Anzahl der Monate an, bevor der Task ausgeführt werden soll.</li><li>**Once** : gibt an, dass diese Aufgabe einmal zu einem bestimmten Datum und zu einer bestimmten Uhrzeit ausgeführt wird.</li><li>**OnStart** : gibt an, dass der Task jedes Mal ausgeführt wird, wenn das System gestartet wird. Wenn das System das nächste Mal gestartet wird, können Sie ein Startdatum angeben oder den Task ausführen.</li><li>**Onlogon** : gibt an, dass der Task immer dann ausgeführt wird, wenn sich ein Benutzer (Benutzer) anmeldet. Sie können ein Datum angeben oder den Task ausführen, wenn sich der Benutzer das nächste Mal anmeldet.</li><li>**OnIdle** : gibt an, dass der Task immer dann ausgeführt wird, wenn sich das System für einen angegebenen Zeitraum im Leerlauf befindet. Sie können ein Datum angeben oder den Task ausführen, wenn sich das System das nächste Mal im Leerlauf befindet.</li></ul> |
| /TN `<taskname>` | Gibt einen Namen für den Task an. Jede Aufgabe im System muss einen eindeutigen Namen aufweisen und den Regeln für Dateinamen entsprechen, die nicht länger als 238 Zeichen sind. Verwenden Sie Anführungszeichen, um Namen einzuschließen, die Leerzeichen enthalten. |
| /tr `<Taskrun>` | Gibt das Programm oder den Befehl an, das vom Task ausgeführt wird. Geben Sie den voll qualifizierten Pfad und den Dateinamen einer ausführbaren Datei, einer Skriptdatei oder einer Batchdatei ein. Der Pfadname darf nicht länger als 262 Zeichen sein. Wenn Sie den Pfad nicht hinzufügen, geht **Schtasks** davon aus, dass sich die Datei im `<systemroot>\System32` Verzeichnis befindet. |
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u `[<domain>]` | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Der Standardwert sind die Berechtigungen des aktuellen Benutzers auf dem lokalen Computer. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. Die Berechtigungen des angegebenen Kontos werden verwendet, um den Task zu planen und den Task auszuführen. Verwenden Sie den **/ru** -Parameter, um den Task mit den Berechtigungen eines anderen Benutzers auszuführen. Das Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Außerdem muss sich der lokale Computer in derselben Domäne befinden wie der Remote Computer, oder er muss sich in einer Domäne befinden, die von der Remote Computer Domäne als vertrauenswürdig eingestuft wird. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter ohne den **/p** -Parameter oder das Password-Argument verwenden, werden Sie von schtasks aufgefordert, ein Kennwort einzugeben. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /ru `{[<domain>\]<user> | system}` | Führt den Task mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Task mit den Berechtigungen des aktuellen Benutzers des lokalen Computers oder mit der Berechtigung des Benutzers ausgeführt, der durch den **/u** -Parameter angegeben wird (sofern vorhanden). Der **/ru** -Parameter ist beim Planen von Aufgaben auf lokalen Computern oder Remote Computern gültig. Folgende Optionen sind gültig:<ul><li>**Domäne** : gibt ein alternatives Benutzerkonto an.</li><li>**System** : Hiermit wird das lokale System Konto, ein Konto mit hohen Privilegien, das vom Betriebssystem und den System Diensten verwendet wird, angegeben.</li></ul> |
| /RP aus `<password>` | Gibt ein Kennwort für das vorhandene Benutzerkonto oder das durch den **/ru** -Parameter angegebene Benutzerkonto an. Wenn Sie diesen Parameter nicht verwenden, wenn Sie ein Benutzerkonto angeben, werden Sie von SchTasks.exe bei der nächsten Anmeldung zur Eingabe des Kennworts aufgefordert. Verwenden Sie den **/RP aus** -Parameter nicht für Aufgaben, die mit den Anmelde Informationen des System Kontos (**/ru System**) ausgeführt werden. Das System Konto verfügt nicht über ein Kennwort, und SchTasks.exe fordert nicht zu einer Eingabe auf. |
| /Monat `<modifiers>` | Gibt an, wie oft die Aufgabe innerhalb Ihres Zeit Plan Typs ausgeführt wird. Folgende Optionen sind gültig:<ul><li>**Minute** : gibt an, dass die Aufgabe alle Minuten ausgeführt wird <n> . Sie können einen beliebigen Wert zwischen 1-1439 Minuten verwenden. Der Standardwert ist 1 Minute.</li><li>**Stündlich** : gibt an, dass die Aufgabe stündlich ausgeführt wird <n> . Sie können einen beliebigen Wert zwischen 1-23 Stunden verwenden. Der Standardwert ist 1 Stunde.</li><li>**Daily** : gibt an, dass der Task jeden Tag ausgeführt wird <n> . Sie können einen beliebigen Wert zwischen 1-365 Tagen verwenden. Standardmäßig ist dies 1 Tag.</li><li>**Wöchentlich** : gibt an, dass die Aufgabe alle Wochen ausgeführt wird <n> . Sie können einen beliebigen Wert zwischen 1-52 Wochen verwenden. Standardmäßig ist dies 1 Woche.</li><li>**Monatlich** : gibt an, dass der Task monatlich ausgeführt wird <n> . Sie können einen der folgenden Werte verwenden:<ul><li>Eine Zahl zwischen 1-12 Monaten</li><li>**Lastday** : Ausführen der Aufgabe am letzten Tag des Monats</li><li>**Erster, zweiter, Dritter oder vierter zusammen mit dem- `/d <day>` Parameter** : gibt die bestimmte Woche und den Tag an, an dem die Aufgabe ausgeführt werden soll. Beispielsweise am dritten Mittwoch des Monats.</li></ul></li><li>**Once** : gibt an, dass der Task einmal ausgeführt wird.</li><li>**OnStart** : gibt an, dass die Aufgabe beim Start ausgeführt wird.</li><li>**Onlogon** : gibt an, dass der Task ausgeführt wird, wenn sich der durch den **/u** -Parameter angegebene Benutzer anmeldet.</li><li>**OnIdle** : gibt an, dass der Task ausgeführt wird, nachdem das System für die durch den **/i** -Parameter angegebene Anzahl von Minuten im Leerlauf ist.</li></ul> |
| /d Tag [, Tag...] | Gibt an, wie oft die Aufgabe innerhalb Ihres Zeit Plan Typs ausgeführt wird. Folgende Optionen sind gültig:<ul><li>**Wöchentlich** : gibt an, dass der Task wöchentlich ausgeführt wird, indem er einen Wert zwischen 1-52 Wochen bereitstellt. Optional können Sie auch einen bestimmten Wochentag hinzufügen, indem Sie den Wert Mon-Sun oder einen Bereich von [Mon-Sun...] hinzufügen.</li><li>**Monatlich** : gibt an, dass die Aufgabe monatlich monatlich ausgeführt wird, indem Sie den ersten, zweiten, Dritten, vierten und letzten Wert bereitstellt. Optional können Sie auch einen bestimmten Wochentag hinzufügen, indem Sie den Wert Mon-Sun hinzufügen oder eine Zahl zwischen 1-12 Monaten angeben. Wenn Sie diese Option verwenden, können Sie auch einen bestimmten Tag des Monats hinzufügen, indem Sie eine Zahl zwischen 1-31 angeben.<p>**Hinweis:** Der Date-Wert von 1-31 ist nur gültig, wenn der **/Monat** -Parameter oder der **/Monat** -Parameter monatlich (1-12) ist. Der Standardwert ist Day 1 (der erste Tag des Monats).</li></ul> |
| /m Monat [, Monat...] | Gibt einen Monat oder einen Monat des Jahres an, in dem die geplante Aufgabe ausgeführt werden soll. Die gültigen Optionen sind Jan-Dec und `*` (jeden Monat). Der **/m** -Parameter ist nur mit einem monatlichen Zeitplan gültig. Dies ist erforderlich, wenn der lastday-Modifizierer verwendet wird. Andernfalls ist Sie optional, und der Standardwert ist `*` (monatlich). |
| /i <Idletime> | Gibt an, wie viele Minuten sich der Computer im Leerlauf befindet, bevor der Task gestartet wird. Ein gültiger Wert ist eine ganze Zahl zwischen 1 und 999. Dieser Parameter ist nur mit einem OnIdle-Zeitplan gültig und wird dann benötigt. |
| /St `<Starttime>` | Gibt die Startzeit für den Task an, wobei das 24-Stunden-Zeitformat HH: mm verwendet wird. Der Standardwert ist die aktuelle Uhrzeit auf dem lokalen Computer. Der **/St** -Parameter ist mit Minuten-, stündlichen, täglichen, wöchentlichen, monatlichen und Once-Zeitplänen gültig. Er ist für einen einmaligen Zeitplan erforderlich. |
| /ri `<interval>` | Gibt das Wiederholungsintervall für die geplante Aufgabe in Minuten an. Dies gilt nicht für Zeit Plan Typen: Minute, stündlich, OnStart, onlogon und OnIdle. Der gültige Bereich ist 1-599940 (599940 Minuten = 9999 Stunden). Wenn entweder der **/et** -Parameter oder der **/du** -Parameter angegeben wird, beträgt der Standardwert **10 Minuten**. |
| /et `<Endtime>` | Gibt die Uhrzeit an, zu der ein Minuten-oder stündlicher Aufgaben Zeitplan in <hh: mm> 24-Stunden-Format endet. Nach der angegebenen Endzeit startet Schtasks die Aufgabe erst wieder, wenn die Startzeit wiederholt wird. Standardmäßig haben Aufgaben Zeitpläne keine Endzeit. Dieser Parameter ist optional und nur mit einem Minuten-oder stündlichen Zeitplan gültig. |
| /du `<duration>` | Gibt eine maximale Zeitdauer für eine Minute oder einen stündlichen Zeitplan in <HHHH: mm> 24-Stunden-Format an. Nachdem die angegebene Zeit abgelaufen ist, startet Schtasks die Aufgabe erst wieder, wenn die Startzeit wiederholt wird. Standardmäßig haben Aufgaben Zeitpläne keine maximale Dauer. Dieser Parameter ist optional und nur mit einem Minuten-oder stündlichen Zeitplan gültig. |
| /k | Beendet das Programm, das der Task ausführt, zu dem Zeitpunkt, der durch **/et** oder **/du**angegeben wird. Ohne **/k**startet Schtasks das Programm nicht erneut, nachdem es die von **/et** oder **/du** angegebene Zeit erreicht hat, oder das Programm beendet, wenn es noch ausgeführt wird. Dieser Parameter ist optional und nur mit einem Minuten-oder stündlichen Zeitplan gültig. |
| /sd <Startdate> | Gibt das Datum an, an dem der Task Zeitplan gestartet wird. Der Standardwert ist das aktuelle Datum auf dem lokalen Computer. Das Format für **StartDate** variiert abhängig von dem für den lokalen Computer ausgewählten Gebiets Schema in den Regions **-und Sprachoptionen**. Für jedes Gebiets Schema ist nur ein Format gültig. Zu den gültigen Datumsformaten gehören (achten Sie darauf, das Format auszuwählen, das in den Regions-und Sprachoptionen **auf dem lokalen Computer in den** Regions **-und Sprachoptionen** am ähnlichsten ist):<ul><li>`<MM>//` : Gibt an, dass Monats First-Formate verwendet werden sollen, z. b. Englisch (USA) und Spanisch (Panama).</li><li>`<DD>//` : Gibt an, dass Day-First-Formate verwendet werden, z. b. Bulgarisch und Niederländisch (Niederlande)</li><li>`<YYYY>//` : Gibt an, dass für die Verwendung durch das erste Jahr verwendet werden soll, z. b. Schwedisch und Französisch (Kanada).</li></ul> |
| /ed `<Enddate>` | Gibt das Datum an, an dem der Zeitplan endet. Dieser Parameter ist optional. Er ist nicht in einem Once-, OnStart-, onlogon-oder OnIdle-Zeitplan gültig. Standardmäßig haben Zeitpläne kein Enddatum. Der Standardwert ist das aktuelle Datum auf dem lokalen Computer. Das Format für **EndDate** variiert abhängig von dem für den lokalen Computer ausgewählten Gebiets Schema in den Regions **-und Sprachoptionen**. Für jedes Gebiets Schema ist nur ein Format gültig. Zu den gültigen Datumsformaten gehören (achten Sie darauf, das Format auszuwählen, das in den Regions-und Sprachoptionen **auf dem lokalen Computer in den** Regions **-und Sprachoptionen** am ähnlichsten ist):<ul><li>`<MM>//` : Gibt an, dass Monats First-Formate verwendet werden sollen, z. b. Englisch (USA) und Spanisch (Panama).</li><li>`<DD>//` : Gibt an, dass Day-First-Formate verwendet werden, z. b. Bulgarisch und Niederländisch (Niederlande)</li><li>`<YYYY>//` : Gibt an, dass für die Verwendung durch das erste Jahr verwendet werden soll, z. b. Schwedisch und Französisch (Kanada).</li></ul> |
| /it | Gibt an, dass die geplante Aufgabe nur ausgeführt werden soll, wenn die Ausführung als Benutzer (das Benutzerkonto, unter dem der Task ausgeführt wird) auf dem Computer angemeldet ist. Dieser Parameter hat keine Auswirkung auf Aufgaben, die mit System Berechtigungen oder Tasks ausgeführt werden, für die die interaktive Eigenschaft bereits festgelegt ist. Sie können einen Change-Befehl nicht verwenden, um die interaktive Eigenschaft aus einer Aufgabe zu entfernen. Standardmäßig ist die Ausführung als Benutzer der aktuelle Benutzer des lokalen Computers, wenn der Task geplant ist, oder das durch den **/u** -Parameter angegebene Konto (sofern verwendet). Wenn der Befehl jedoch den **/ru** -Parameter enthält, ist das Konto "Ausführen als" das Konto, das durch den **/ru** -Parameter angegeben wird. |
| /z | Gibt an, dass die Aufgabe nach Abschluss des Zeitplans gelöscht wird. |
| /f | Gibt an, dass die Aufgabe erstellt und Warnungen unterdrückt werden sollen, wenn die angegebene Aufgabe bereits vorhanden ist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="to-schedule-a-task-to-run-every-n-minutes"></a>So planen Sie die Ausführung einer Aufgabe pro `<n>` Minute

Der **/SC Minute** -Parameter ist in einem Minuten Zeitplan erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Minuten zwischen den einzelnen Aufgaben an. Der Standardwert für **/Monat** ist *1* (jede Minute). Die Parameter **/et** (Endzeit) und **/du** (Duration) sind optional und können mit oder ohne den Parameter **/k** (End Task) verwendet werden.

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um ein Sicherheits Skript ( *sec. VSB*) zu planen, das alle 20 Minuten ausgeführt werden soll:

    ```
    schtasks /create /sc minute /mo 20 /tn Security Script /tr \\central\data\scripts\sec.vbs
    ```

    Da in diesem Beispiel ein Startdatum oder eine Uhrzeit nicht enthalten ist, wird die Aufgabe 20 Minuten nach Abschluss des Befehls gestartet und dann alle 20 Minuten ausgeführt, wenn das System ausgeführt wird. Beachten Sie, dass sich die Sicherheits Skript-Quelldatei auf einem Remote Computer befindet, aber dass der Task geplant und auf dem lokalen Computer ausgeführt wird.

- So planen Sie die Ausführung eines Sicherheits Skripts ( *sec. VSB*) auf dem lokalen Computer alle 100 Minuten zwischen 5:00 Uhr und 7:59 Uhr Geben Sie jeden Tag Folgendes ein:

    ```
    schtasks /create /tn Security Script /tr sec.vbs /sc minute /mo 100 /st 17:00 /et 08:00 /k
    ```

    In diesem Beispiel wird der **/SC** -Parameter verwendet, um einen Minuten Zeitplan anzugeben, und den **/Monat** -Parameter, um ein Intervall von 100 Minuten anzugeben. Er verwendet die Parameter **/St** und **/et** , um die Startzeit und Endzeit des Zeitplans für jeden Tag anzugeben. Außerdem verwendet er den **/k** -Parameter, um das Skript zu unterbinden, wenn es noch um 7:59 Uhr morgens ausgeführt wird. Ohne **/k**würde Schtasks das Skript nach 7:59 Uhr nicht starten, aber wenn die Instanz um 6:20 Uhr gestartet wurde. wird noch ausgeführt, wird Sie nicht angehalten.

## <a name="to-schedule-a-task-to-run-every-n-hours"></a>So planen Sie die Ausführung einer Aufgabe `<n>` stündlich

In einem stündlichen Zeitplan ist der **stündliche/SC** -Parameter erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Stunden zwischen den einzelnen Tasks der Aufgabe an. Der Standardwert für **/Monat** ist *1* (stündlich). Der **/k** -Parameter (End-Task) ist optional und kann entweder mit **/et** (Ende zum angegebenen Zeitpunkt) oder **/du** (Ende nach dem angegebenen Intervall) verwendet werden.

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" alle fünf Stunden zu planen, beginnend am ersten Tag im März 2002:

    ```
    schtasks /create /sc hourly /mo 5 /sd 03/01/2002 /tn My App /tr c:\apps\myapp.exe
    ```

    In diesem Beispiel verwendet der lokale Computer die Option **Englisch (Simbabwe)** in den Regions **-und Sprachoptionen**, sodass das Format für das Startdatum mm/dd/yyyy (03/01/2002) lautet.

- Geben Sie Folgendes ein, um das MyApp-Programm stündlich auszuführen, beginnend bei fünf Minuten nach Mitternacht:

    ```
    schtasks /create /sc hourly /st 00:05 /tn My App /tr c:\apps\myapp.exe
    ```

- Geben Sie Folgendes ein, um die Ausführung des Programms MyApp alle drei Stunden zu planen:

    ```
    schtasks /create /tn My App /tr myapp.exe /sc hourly /mo 3 /st 00:00 /du 0010:00
    ```

    In diesem Beispiel wird die Aufgabe um 12:00 Uhr, 3:00 Uhr, 6:00 Uhr und 9:00 Uhr ausgeführt. Da die Dauer 10 Stunden beträgt, wird die Aufgabe nicht erneut um 12:00 Uhr ausgeführt. Stattdessen wird er um 12:00 Uhr wieder gestartet. der nächste Tag. Da das Programm nur wenige Minuten ausgeführt wird, ist der **/k** -Parameter, der das Programm beendet, wenn es noch ausgeführt wird, wenn die Dauer abläuft, nicht erforderlich.

## <a name="to-schedule-a-task-to-run-every-n-days"></a>So planen Sie die Ausführung eines Tasks für jeden `<n>` Tag

Der **/SC Daily** -Parameter ist in einem täglichen Zeitplan erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Tage zwischen den einzelnen Tasks der Aufgabe an. Der Standardwert für **/Monat** ist *1* (täglich).

### <a name="examples"></a>Beispiele

- So planen Sie die Ausführung des Programms "MyApp" täglich um 8:00 Uhr Geben Sie bis zum 31. Dezember 2021 Folgendes ein:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc daily /st 08:00 /ed 31/12/2021
    ```

     In diesem Beispiel ist das lokale Computersystem in Regions **-und Sprachoptionen**auf die Option **Englisch (Großbritannien)** festgelegt, sodass das Enddatum das Format dd/mm/yyyy (31/12/2021) hat. Da in diesem Beispiel der **/Monat** -Parameter nicht enthalten ist, wird das Standardintervall *1* verwendet, um den Befehl jeden Tag auszuführen.

- So planen Sie die Ausführung des Programms "MyApp" alle zwölf Tage um 1:00 Uhr (13:00) ab dem 31. Dezember 2021 geben Sie Folgendes ein:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc daily /mo 12 /sd 12/31/2002 /st 13:00
    ```

    In diesem Beispiel ist das System in Regions **-und Sprachoptionen**auf die Option **Englisch (Simbabwe)** festgelegt, sodass das Enddatum das Format mm/dd/yyyy (12/31/2021) hat.

- Geben Sie Folgendes ein, um ein Sicherheits Skript ( *sec. VSB*) zu planen, das alle 70 Tage ausgeführt werden soll:

    ```
    schtasks /create /tn Security Script /tr sec.vbs /sc daily /mo 70 /it
    ```

    In diesem Beispiel wird der **/IT** -Parameter verwendet, um anzugeben, dass der Task nur ausgeführt wird, wenn der Benutzer, der den Task ausführt, auf dem Computer angemeldet ist. Da die Aufgabe mit den Berechtigungen eines bestimmten Benutzerkontos ausgeführt wird, wird diese Aufgabe nur ausgeführt, wenn dieser Benutzer angemeldet ist.

    > [!NOTE]
    > Verwenden Sie eine ausführliche Abfrage (**/Query "aus/v**), um Aufgaben mit der interaktiven (**/IT**)-Eigenschaft zu identifizieren. In einer ausführlichen Abfrage Anzeige einer Aufgabe mit/IT hat das Feld **Anmeldemodus** den Wert interaktiv.

## <a name="to-schedule-a-task-to-run-every-n-weeks"></a>So planen Sie die Ausführung einer Aufgabe pro `<n>` Woche

In einem wöchentlichen Zeitplan ist der **wöchentliche/SC** -Parameter erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Wochen zwischen den einzelnen Tasks der Aufgabe an. Der Standardwert für **/Monat** ist *1* (jede Woche).

Wöchentliche Zeitpläne verfügen auch über einen optionalen **/d** -Parameter, um zu planen, dass die Aufgabe an bestimmten Wochentagen oder an allen Tagen () ausgeführt wird. Der Standardwert ist *Mon (Montag)*. Die Option für jeden Tag () entspricht dem Planen einer täglichen Aufgabe.

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" auf einem Remote Computer alle sechs Wochen zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc weekly /mo 6 /s Server16 /u Admin01
    ```

    Da in diesem Beispiel der **/d** -Parameter weggelassen wird, wird der Task am Montag ausgeführt. In diesem Beispiel wird auch der **/s** -Parameter verwendet, um den Remote Computer anzugeben, und der **/u** -Parameter, um den Befehl mit den Berechtigungen des Benutzer Administrator Kontos auszuführen. Da der **/p** -Parameter ausgelassen wird, fordert SchTasks.exe den Benutzer zur Eingabe des Kennworts für das Administrator Konto auf, und da der Befehl Remote ausgeführt wird, werden alle Pfade im Befehl, einschließlich des Pfads zu MyApp.exe, auf Pfade auf dem Remote Computer verwiesen.

- Geben Sie Folgendes ein, um einen Task für jeden anderen Freitag zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc weekly /mo 2 /d FRI
    ```

    In diesem Beispiel wird der **/Monat** -Parameter verwendet, um das Intervall von zwei Wochen anzugeben, und der **/d** -Parameter zum Angeben des Wochentags. Um einen Task zu planen, der jeden Freitag ausgeführt wird, lassen Sie den **/Monat** -Parameter aus, oder legen Sie ihn auf *1*fest.

## <a name="to-schedule-a-task-to-run-every-n-months"></a>So planen Sie die Ausführung einer Aufgabe in `<n>` Monaten

In diesem Zeit Plantyp ist der **monatliche/SC** -Parameter erforderlich. Der **/Monat** (Modifier)-Parameter, der die Anzahl der Monate zwischen den einzelnen Aufgaben der Aufgabe angibt, ist optional, und der Standardwert ist *1* (jeden Monat). Dieser Zeit Plantyp verfügt auch über einen optionalen **/d** -Parameter, um zu planen, dass die Aufgabe an einem bestimmten Tag des Monats ausgeführt wird. Der Standardwert ist *1* (der erste Tag des Monats).

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" am ersten Tag jedes Monats zu planen:

    ```
    schtasks /create /tn My App /tr myapp.exe /sc monthly
    ```

    Der Standardwert für den Parameter **/Monat** (Modifier) und den Parameter **/d** (Day) ist *1*, sodass Sie keines dieser Parameter für dieses Beispiel verwenden müssen.

- Geben Sie Folgendes ein, um die Ausführung des Programms MyApp alle drei Monate zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc monthly /mo 3
    ```

    In diesem Beispiel wird der **/Monat** -Parameter verwendet, um ein Intervall von drei Monaten anzugeben.

- Geben Sie Folgendes ein, um das MyApp-Programm so zu planen, dass es jeden anderen Monat am 21. Tag des Monats um Mitternacht für ein Jahr ausgeführt wird, vom 2002 2. Juli bis zum 30. Juni 2003:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc monthly /mo 2 /d 21 /st 00:00 /sd 2002/07/01 /ed 2003/06/30
    ```

    In diesem Beispiel wird der **/Monat** -Parameter verwendet, um das monatliche Intervall (alle zwei Monate) anzugeben, den **/d** -Parameter, um das Datum anzugeben, den **/St** -Parameter, um die Uhrzeit anzugeben, und die Parameter **/SD** und **/Ed** , um das Start-und Enddatum anzugeben. In diesem Beispiel ist der lokale Computer in Regions **-und Sprachoptionen**auf die Option **Englisch (Südafrika)** festgelegt, sodass die Datumsangaben im lokalen Format yyyy/mm/dd angegeben werden.

## <a name="to-schedule-a-task-to-run-on-a-specific-day-of-the-week"></a>So planen Sie die Ausführung einer Aufgabe an einem bestimmten Tag der Woche

Der Zeitplan für den Wochentag ist eine Variation des wöchentlichen Zeitplans. In einem wöchentlichen Zeitplan ist der **wöchentliche/SC** -Parameter erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Wochen zwischen den einzelnen Tasks der Aufgabe an. Der Standardwert für **/Monat** ist *1* (jede Woche). Der optionale Parameter **/d** plant, dass der Task an bestimmten Wochentagen oder an allen Tagen (**&#42;**) ausgeführt wird. Der Standardwert ist *Mon (Montag)*. Die Option für jeden Tag `(/d *)` entspricht dem Planen einer täglichen Aufgabe.

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" für jede Woche am Mittwoch zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc weekly /d WED
    ```

    In diesem Beispiel wird der **/d** -Parameter zum Angeben des Wochentags verwendet. Da der Befehl den **/Monat** -Parameter verlässt, wird die Aufgabe jede Woche ausgeführt.

- Geben Sie Folgendes ein, um die Ausführung einer Aufgabe am Montag und Freitag jeder acht Woche zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc weekly /mo 8 /d MON,FRI
    ```

    In diesem Beispiel wird der **/d** -Parameter verwendet, um die Tage anzugeben, und der **/Monat** -Parameter, um das achtwöchige Intervall anzugeben.

## <a name="to-schedule-a-task-to-run-on-a-specific-week-of-the-month"></a>So planen Sie die Ausführung einer Aufgabe für eine bestimmte Woche des Monats

In diesem Zeit Plantyp sind der **/SC monatlich** -Parameter, der **/Monat** -Parameter (Modifier) und der **/d** (Day)-Parameter erforderlich. Der **/Monat** (Modifier)-Parameter gibt die Woche an, in der die Aufgabe ausgeführt wird. Der **/d** -Parameter gibt den Wochentag an. Sie können für diesen Zeit Plantyp nur einen Wochentag angeben. Dieser Zeitplan verfügt auch über einen optionalen **/m** (month)-Parameter, mit dem Sie den Task für bestimmte Monate oder jeden Monat (**&#42;**) planen können. Der Standardwert für den **/m** -Parameter ist monatlich (**&#42;**).

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" am zweiten Sonntag jedes Monats zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc monthly /mo SECOND /d SUN
    ```

    In diesem Beispiel wird der **/Monat** -Parameter verwendet, um die zweite Woche des Monats anzugeben, und den **/d** -Parameter, um den Tag anzugeben.

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" am ersten Montag im März und September zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc monthly /mo FIRST /d MON /m MAR,SEP
    ```

    In diesem Beispiel wird der **/Monat** -Parameter verwendet, um die erste Woche des Monats anzugeben, und den **/d** -Parameter, um den Tag anzugeben. Er verwendet den **/m** -Parameter, um den Monat anzugeben, wobei die Month-Argumente durch ein Komma getrennt werden.

## <a name="to-schedule-a-task-to-run-on-a-specific-day-each-month"></a>So planen Sie die Ausführung einer Aufgabe an einem bestimmten Tag monatlich

In diesem Zeit Plantyp sind der **monatliche Parameter/SC** und der Parameter **/d** (Day) erforderlich. Der **/d** -Parameter gibt ein Datum des Monats an (1-31), nicht den Wochentag, und Sie können nur einen Tag im Zeitplan angeben. Der **/m** -Parameter (month) ist optional, wobei der Standardwert monatlich *()* ist, während der **/Monat** -Parameter (Modifier) mit diesem Zeit Plantyp nicht gültig ist.

Mit Schtasks.exe können Sie eine Aufgabe nicht für ein Datum planen, das nicht in einem Monat liegt, der durch den **/m** -Parameter angegeben wird. Planen Sie z. b. den 31. Tag Februar. Wenn Sie jedoch nicht den **/m** -Parameter verwenden und eine Aufgabe für ein Datum planen, das nicht in jedem Monat angezeigt wird, wird der Task nicht in den kürzeren Monaten ausgeführt. Um einen Task für den letzten Tag des Monats zu planen, verwenden Sie den Zeitplan für den letzten Tag des Monats.

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" am ersten Tag jedes Monats zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc monthly
    ```

    Da der Standardmodifizierer *None* (kein Modifizierer) ist, verwendet dieser Befehl den Standardtag *1*und den Standard Monat *jedes Monats*, ohne dass zusätzliche Parameter erforderlich sind.

- So planen Sie die Ausführung des Programms "MyApp" am 15. Mai und 15. Juni um 3:00 Uhr (15:00), geben Sie Folgendes ein:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc monthly /d 15 /m MAY,JUN /st 15:00
    ```

    In diesem Beispiel wird der **/d** -Parameter verwendet, um das Datum und den **/m** -Parameter anzugeben, um die Monate anzugeben. Außerdem verwendet er den **/St** -Parameter, um die Startzeit anzugeben.

## <a name="to-schedule-a-task-to-run-on-the-last-day-of-a-month"></a>So planen Sie die Ausführung einer Aufgabe am letzten Tag eines Monats

Im Zeit Plantyp für den letzten Tag sind der **/SC monatlich** -Parameter, der **/Monat lastday** -Parameter (Modifier) und der **/m** -Parameter (month) erforderlich. Der **/d** (Day)-Parameter ist ungültig.

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" am letzten Tag jedes Monats zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc monthly /mo lastday /m *
    ```

    In diesem Beispiel wird der **/Monat** -Parameter verwendet, um den letzten Tag und den **/m** -Parameter mit dem Platzhalter Zeichen (**&#42;**) anzugeben, um anzugeben, dass das Programm monatlich ausgeführt wird.

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" für den letzten Tag von Februar und den letzten Tag des März um 6:00 Uhr zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc monthly /mo lastday /m FEB,MAR /st 18:00
    ```

    In diesem Beispiel wird der **/Monat** -Parameter verwendet, um den letzten Tag anzugeben, den **/m** -Parameter, um die Monate anzugeben, und den **/St** -Parameter, um die Startzeit anzugeben.

## <a name="to-schedule-to-run-once"></a>So planen Sie die einmalige Ausführung

Der **/sc once** -Parameter ist im Typ "Run-Once Schedule" erforderlich. Der **/St** -Parameter, der die Zeit angibt, zu der die Aufgabe ausgeführt wird, ist erforderlich. Der **/SD** -Parameter, der das Datum angibt, an dem die Aufgabe ausgeführt wird, ist optional, während die Parameter **/Monat** (Modifizierer) und **/Ed** (Enddatum) nicht gültig sind.

Mit "Schtasks" können Sie die Ausführung einer Aufgabe nicht planen, wenn das angegebene Datum und die Uhrzeit in der Vergangenheit liegen, und zwar basierend auf der Uhrzeit des lokalen Computers. Um einen Task zu planen, der auf einem Remote Computer in einer anderen Zeitzone einmal ausgeführt wird, müssen Sie ihn vor dem Datum und der Uhrzeit auf dem lokalen Computer planen.

### <a name="example"></a>Beispiel

- Geben Sie Folgendes ein, um die Ausführung des Programms MyApp am 1. Januar 2003 um Mitternacht zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc once /sd 01/01/2003 /st 00:00
    ```

    In diesem Beispiel wird der **/SC** -Parameter verwendet, um den Zeit Plantyp und die **/SD** -und **/St** -Parameter anzugeben, um das Datum und die Uhrzeit anzugeben. In diesem Beispiel verwendet der lokale Computer die Option **Englisch (USA)** in Regions **-und Sprachoptionen**, das Format für das Startdatum ist mm/dd/yyyy.

## <a name="to-schedule-a-task-to-run-every-time-the-system-starts"></a>So planen Sie die Ausführung einer Aufgabe bei jedem Systemstart

Beim Typ des Start Zeitplans ist der Parameter **/SC OnStart** erforderlich. Der Parameter **/SD** (Startdatum) ist optional, und der Standardwert ist das aktuelle Datum.

### <a name="example"></a>Beispiel

- Geben Sie Folgendes ein, um das MyApp-Programm zu planen, das bei jedem Start des Systems ausgeführt wird, ab dem 15. März 2001:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc onstart /sd 03/15/2001
    ```

    In diesem Beispiel verwendet der lokale Computer die Option **Englisch (USA)** in Regions **-und Sprachoptionen**, das Format für das Startdatum ist mm/dd/yyyy.

## <a name="to-schedule-a-task-to-run-when-a-user-logs-on"></a>So planen Sie die Ausführung einer Aufgabe, wenn sich ein Benutzer anmeldet

Mit dem Typ bei Anmelde Zeitplan wird eine Aufgabe geplant, die immer dann ausgeführt wird, wenn sich ein Benutzer am Computer anmeldet. Im Typ des Anmeldungs Zeitplans ist der **/SC pro** -Parameter erforderlich. Der Parameter **/SD** (Startdatum) ist optional, und der Standardwert ist das aktuelle Datum.

### <a name="example"></a>Beispiel

- Zum Planen eines Tasks, der ausgeführt wird, wenn sich ein Benutzer an einem Remote Computer anmeldet, geben Sie Folgendes ein:

    ```
    schtasks /create /tn Start Web Site /tr c:\myiis\webstart.bat /sc onlogon /s Server23
    ```

    In diesem Beispiel wird eine Batchdatei so geplant, dass Sie jedes Mal ausgeführt wird, wenn sich ein Benutzer (Benutzer) am Remote Computer anmeldet. Er verwendet den **/s** -Parameter, um den Remote Computer anzugeben. Da der Befehl Remote ist, beziehen sich alle Pfade im Befehl, einschließlich des Pfads zur Batchdatei, auf einen Pfad auf dem Remote Computer.

## <a name="to-schedule-a-task-to-run-when-the-system-is-idle"></a>So planen Sie die Ausführung einer Aufgabe, wenn sich das System im Leerlauf befindet

Mit dem Zeitplan für Leerlauf Zeitpläne wird eine Aufgabe geplant, die immer dann ausgeführt wird, wenn keine Benutzeraktivität innerhalb der durch den **/i** -Parameter angegebenen Zeit vorhanden ist. Im Leerlaufzeit Plantyp sind der **/sc onidle** -Parameter und der **/i** -Parameter erforderlich. **/SD** (Startdatum) ist optional, und der Standardwert ist das aktuelle Datum.

### <a name="example"></a>Beispiel

- Geben Sie Folgendes ein, um die Ausführung des Programms MyApp zu planen, wenn sich der Computer im Leerlauf befindet:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc onidle /i 10
    ```

    In diesem Beispiel wird der erforderliche **/i** -Parameter verwendet, um anzugeben, dass der Computer zehn Minuten lang im Leerlauf bleiben muss, bevor der Task gestartet wird.

## <a name="to-schedule-a-task-to-run-now"></a>So planen Sie die Ausführung einer Aufgabe

"Schtasks" verfügt nicht über eine Option "jetzt ausführen", aber Sie können diese Option simulieren, indem Sie eine Aufgabe erstellen, die ein Mal ausgeführt wird und innerhalb weniger Minuten gestartet wird.

### <a name="example"></a>Beispiel

- So planen Sie die einmalige Ausführung einer Aufgabe am 13. November 2020 um 2:18 Uhr lokale Zeit, geben Sie Folgendes ein:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc once /st 14:18 /sd 11/13/2002
    ```

    In diesem Beispiel verwendet der lokale Computer die Option **Englisch (USA)** in den Regions **-und Sprachoptionen**, sodass das Format für das Startdatum mm/dd/yyyy ist.

## <a name="to-schedule-a-task-that-runs-with-different-permissions"></a>So planen Sie einen Task, der mit unterschiedlichen Berechtigungen ausgeführt wird

Sie können die Ausführung von Aufgaben aller Typen mit Berechtigungen eines alternativen Kontos auf dem lokalen Computer und auf einem Remote Computer planen. Zusätzlich zu den Parametern, die für den jeweiligen Zeit Plantyp erforderlich sind, ist der **/ru** -Parameter erforderlich, und der **/RP aus** -Parameter ist optional.

### <a name="examples"></a>Beispiele

- Um das MyApp-Programm auf dem lokalen Computer auszuführen, geben Sie Folgendes ein:

    ```
    schtasks /create /tn My App /tr myapp.exe /sc weekly /d TUE /ru Admin06
    ```

    In diesem Beispiel wird der **/ru** -Parameter verwendet, um anzugeben, dass der Task mit den Berechtigungen des Administrator Kontos des Benutzers (*Admin06*) ausgeführt werden soll. In diesem Beispiel ist die Ausführung der Aufgabe jeden Dienstag geplant, aber Sie können einen beliebigen Zeit Plantyp für eine Aufgabe verwenden, die mit alternativen Berechtigungen ausgeführt wird.

    In der Antwort werden SchTasks.exe zur Eingabe des Kennworts für das *Admin06* -Konto aufgefordert. Anschließend wird eine Erfolgsmeldung angezeigt:

    ```
    Please enter the run as password for Admin06: ********
    SUCCESS: The scheduled task My App has successfully been created.
    ```

- Um das Programm MyApp alle vier Tage auf *dem Computer mit* dem Computer auszuführen, geben Sie Folgendes ein:

    ```
    schtasks /create /tn My App /tr myapp.exe /sc daily /mo 4 /s Marketing /u Marketing\Admin01 /ru Reskits\User01
    ```

    In diesem Beispiel wird der **/SC** -Parameter verwendet, um einen täglichen Zeitplan anzugeben, und mit dem **/Monat** -Parameter wird ein Intervall von vier Tagen angegeben. Außerdem wird in diesem Beispiel der **/s** -Parameter verwendet, um den Namen des Remote Computers anzugeben, und den **/u** -Parameter, um ein Konto anzugeben, das über die Berechtigung zum Planen eines Tasks auf dem Remote Computer verfügt (*"Admin01" auf dem Marketing Computer*). Schließlich wird in diesem Beispiel der **/ru** -Parameter verwendet, um anzugeben, dass der Task mit den Berechtigungen des nicht-Administrator Kontos des Benutzers (*USER01* in der *reskits* -Domäne) ausgeführt werden soll. Ohne den **/ru** -Parameter wird die Aufgabe mit den Berechtigungen des Kontos ausgeführt, das von **/u**angegeben wird.

    Beim Ausführen dieses Beispiels fordert Schtasks zuerst das Kennwort des Benutzers an, der durch den **/u** -Parameter benannt wird (um den Befehl auszuführen), und fordert dann das Kennwort des Benutzers an, der durch den **/ru** -Parameter benannt wird (zum Ausführen der Aufgabe). Nach der Authentifizierung der Kenn Wörter zeigt SchTasks eine Meldung mit dem Hinweis an, dass der Task geplant ist:

    ```
    Type the password for Marketing\Admin01:********
    Please enter the run as password for Reskits\User01: ********
    SUCCESS: The scheduled task My App has successfully been created.
    ```

- Zum Ausführen eines Zeitplans für die Ausführung des *AdminCheck.exe* Programms auf dem *öffentlichen* Computer jeden Freitag um 4:00 Uhr, aber nur, wenn der Administrator des Computers angemeldet ist, geben Sie Folgendes ein:

    ```
    schtasks /create /tn Check Admin /tr AdminCheck.exe /sc weekly /d FRI /st 04:00 /s Public /u Domain3\Admin06 /ru Public\Admin01 /it
    ```

    In diesem Beispiel wird der **/SC** -Parameter verwendet, um einen wöchentlichen Zeitplan anzugeben, den **/d** -Parameter, um den Tag anzugeben, und den **/St** -Parameter, um die Startzeit anzugeben. Außerdem verwendet er den **/s** -Parameter, um den Namen des Remote Computers anzugeben, mit dem **/u** -Parameter wird ein Konto mit der Berechtigung zum Planen eines Tasks auf dem Remote Computer angegeben, mit dem **/ru** -Parameter wird der Task so konfiguriert, dass er mit den Berechtigungen des Administrators des öffentlichen Computers (*Public\Admin01*) ausgeführt wird, und der Parameter **/IT** , um anzugeben, dass der Task nur ausgeführt wird, wenn das *Public\Admin01* -Konto angemeldet ist.

    > [!NOTE]
    > Verwenden Sie eine ausführliche Abfrage (), um Tasks mit der Interactive-only-Eigenschaft (**/IT**) zu identifizieren `/query /v` . In einer ausführlichen Abfrage Anzeige einer Aufgabe mit **/IT**hat das Feld **Anmeldemodus** den Wert **interaktiv**.

## <a name="to-schedule-a-task-that-runs-with-system-permissions"></a>So planen Sie einen Task, der mit System Berechtigungen ausgeführt wird

Tasks aller Typen können mit Berechtigungen des **System** Kontos auf dem lokalen Computer und auf einem Remote Computer ausgeführt werden. Zusätzlich zu den Parametern, die für den jeweiligen Zeit Plantyp erforderlich sind, ist der **/ru System** -Parameter (oder **/ru**) erforderlich, während der **/RP aus** -Parameter nicht gültig ist.

> [!IMPORTANT]
> Das **System** Konto verfügt nicht über interaktive Anmelde Rechte. Benutzer können weder Programme noch Aufgaben, die mit System Berechtigungen ausgeführt werden, sehen oder mit ihnen interagieren. Der **/ru** -Parameter bestimmt die Berechtigungen, unter denen der Task ausgeführt wird, und nicht die Berechtigungen, die zum Planen der Aufgabe verwendet werden. Nur Administratoren können Aufgaben planen, unabhängig vom Wert des **/ru** -Parameters.
>
> Verwenden Sie eine ausführliche Abfrage (), um Aufgaben zu identifizieren, die mit System Berechtigungen ausgeführt werden `/query /v` . In einer ausführlichen Abfrage Anzeige einer System Ausführungs Aufgabe hat das Feld **als Benutzer ausführen** den Wert **NT-Autorität \ System** , und das Feld **Anmeldemodus** hat nur den Wert **Background**.

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um die Ausführung des MyApp-Programms auf dem lokalen Computer mit Berechtigungen für das **System** Konto zu planen:

    ```
    schtasks /create /tn My App /tr c:\apps\myapp.exe /sc monthly /d 15 /ru System
    ```

    In diesem Beispiel ist geplant, dass die Aufgabe am fünfzehnten Tag jeden Monats ausgeführt wird. Sie können jedoch einen beliebigen Zeit Plantyp für eine Aufgabe verwenden, die mit System Berechtigungen ausgeführt wird. Außerdem wird in diesem Beispiel der System-und **/ru-System** Parameter verwendet, um den System Sicherheitskontext anzugeben. Da System Tasks kein Kennwort verwenden, wird der **/RP aus** -Parameter ausgelassen.

    Als Antwort zeigt SchTasks.exe eine Informations Meldung und eine Erfolgsmeldung an, ohne dass ein Kennwort angefordert wird:

    ```
    INFO: The task will be created under user name (NT AUTHORITY\SYSTEM).
    SUCCESS: The Scheduled task My App has successfully been created.
    ```

- Geben Sie Folgendes ein, um die Ausführung des Programms "MyApp" auf dem *Finance01* -Computer jeden Morgen um 4:00 Uhr zu planen:

    ```
    schtasks /create /tn My App /tr myapp.exe /sc daily /st 04:00 /s Finance01 /u Admin01 /ru System
    ```

    Dieses Beispiel verwendet den **/TN** -Parameter, um den Task zu benennen, und den **/TR** -Parameter, um die Remote Kopie des MyApp-Programms anzugeben, den **/SC** -Parameter, um einen täglichen Zeitplan anzugeben, aber verlässt den **/Monat** -Parameter, da *1* (täglich) der Standardwert ist. In diesem Beispiel wird auch der **/St** -Parameter verwendet, um die Startzeit anzugeben. Dies ist auch der Zeitpunkt, an dem der Task jeden Tag ausgeführt wird, der **/s** **-Parameter,** um den Namen des Remote Computers anzugeben, der **/u** -Parameter, um ein Konto mit der Berechtigung zum Planen einer Aufgabe auf dem Remote Computer anzugeben Ohne den **/ru** -Parameter würde die Aufgabe mit den Berechtigungen des Kontos ausgeführt werden, das durch den **/u** -Parameter angegeben wird.

    Schtasks.exe fordert das Kennwort des Benutzers an, der vom **/u** -Parameter benannt wird, und zeigt nach der Authentifizierung des Kennworts eine Meldung an, die anzeigt, dass die Aufgabe erstellt wurde und mit Berechtigungen des **System** Kontos ausgeführt wird:

    ```
    Type the password for Admin01:**********

    INFO: The Schedule Task My App will be created under user name (NT AUTHORITY\
    SYSTEM).
    SUCCESS: The scheduled task My App has successfully been created.
    ```

## <a name="to-schedule-a-task-that-runs-more-than-one-program"></a>So planen Sie einen Task, der mehr als ein Programm ausführt

Jeder Task führt nur ein Programm aus. Sie können jedoch eine Batchdatei erstellen, die mehrere Programme ausführt, und dann eine Aufgabe für die Ausführung der Batchdatei planen.

1. Erstellen Sie mit einem Text-Editor, z. b. Editor, eine Batchdatei, die den Namen und den voll qualifizierten Pfad zur exe-Datei enthält, die erforderlich ist, um die Ereignisanzeige-(Eventvwr.exe) und System Monitor Programme (Perfmon.exe) zu starten.

    ```
    C:\Windows\System32\Eventvwr.exe
    C:\Windows\System32\Perfmon.exe
    ```

2. Speichern Sie die Datei als *MyApps.bat*, öffnen Sie schtasks.exe, und erstellen Sie dann eine Aufgabe zum Ausführen von *MyApps.bat* , indem Sie Folgendes eingeben:

    ```
    schtasks /create /tn Monitor /tr C:\MyApps.bat /sc onlogon /ru Reskit\Administrator
    ```

    Dieser Befehl erstellt den Monitor Task, der immer dann ausgeführt wird, wenn sich jemand anmeldet. Er verwendet den **/TN** -Parameter, um den Task zu benennen, den **/TR** -Parameter, um MyApps.bat auszuführen, den **/SC** -Parameter, um den onlogon-Zeit Plantyp anzugeben, und den **/ru** -Parameter, um den Task mit den Berechtigungen des Benutzer Administrator Kontos auszuführen.

    Wenn sich ein Benutzer am Computer anmeldet, startet der Task als Ergebnis dieses Befehls sowohl Ereignisanzeige als auch System Monitor.

## <a name="to-schedule-a-task-that-runs-on-a-remote-computer"></a>So planen Sie einen Task, der auf einem Remote Computer ausgeführt wird

Wenn Sie planen, dass ein Task auf einem Remote Computer ausgeführt werden soll, müssen Sie den Task dem Zeitplan des Remote Computers hinzufügen. Aufgaben aller Typen können auf einem Remote Computer geplant werden, die folgenden Bedingungen müssen erfüllt sein:

- Sie müssen über die Berechtigung zum Planen der Aufgabe verfügen. Daher müssen Sie auf dem lokalen Computer mit einem Konto angemeldet sein, das Mitglied der Gruppe "Administratoren" auf dem Remote Computer ist, oder Sie müssen den **/u** -Parameter verwenden, um die Anmelde Informationen eines Administrators für den Remote Computer anzugeben.

- Sie können den **/u** -Parameter nur verwenden, wenn sich der lokale Computer und der Remote Computer in derselben Domäne befinden oder der lokale Computer sich in einer Domäne befindet, der die Remote Computer Domäne vertraut. Andernfalls kann der Remote Computer das angegebene Benutzerkonto nicht authentifizieren, und es kann nicht überprüft werden, ob das Konto Mitglied der Gruppe "Administratoren" ist.

- Der Task muss über ausreichende Berechtigungen verfügen, um auf dem Remote Computer ausgeführt werden zu können. Welche Berechtigungen erforderlich sind, hängt von der Aufgabe ab. Standardmäßig wird der Task mit der-Berechtigung des aktuellen Benutzers des lokalen Computers ausgeführt, oder wenn der **/u** -Parameter verwendet wird, wird der Task mit der Berechtigung des Kontos ausgeführt, das durch den **/u** -Parameter angegeben wird. Allerdings können Sie den **/ru** -Parameter verwenden, um den Task mit Berechtigungen eines anderen Benutzerkontos oder mit System Berechtigungen auszuführen.

### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um zu planen, dass das Programm MyApp (als Administrator) alle zehn Tage, beginnend sofort, auf dem Remote Computer *Srv01* ausgeführt wird:

    ```
    schtasks /create /s SRV01 /tn My App /tr c:\program files\corpapps\myapp.exe /sc daily /mo 10
    ```

    In diesem Beispiel wird der **/s** -Parameter verwendet, um den Namen des Remote Computers anzugeben. Da der lokale aktuelle Benutzer ein Administrator des Remote Computers ist, ist der **/u** -Parameter, der Alternative Berechtigungen zum Planen der Aufgabe bietet, nicht erforderlich.

    > [!NOTE]
    > Beim Planen von Aufgaben auf einem Remote Computer verweisen alle Parameter auf den Remote Computer. Daher verweist die durch den **/TR** -Parameter angegebene Datei auf die Kopie der MyApp.exe auf dem Remote Computer.

- Geben Sie Folgendes ein, um zu planen, dass das Programm MyApp (als Benutzer) alle drei Stunden auf dem Remote Computer *SRV06* ausgeführt werden soll:

    ```
    schtasks /create /s SRV06 /tn My App /tr c:\program files\corpapps\myapp.exe /sc hourly /mo 3 /u reskits\admin01 /p R43253@4$ /ru SRV06\user03 /rp MyFav!!Pswd
    ```

    Da Administrator Berechtigungen erforderlich sind, um eine Aufgabe zu planen, verwendet der Befehl die Parameter **/u** und **/p** , um die Anmelde Informationen des Administrator Kontos des Benutzers (*"Admin01"* in der *reskits* -Domäne) bereitzustellen. Diese Berechtigungen werden standardmäßig auch verwendet, um die Aufgabe auszuführen. Da der Task jedoch keine Administrator Berechtigungen zum Ausführen benötigt, enthält der Befehl die Parameter **/u** und **/RP aus** , um die Standardeinstellung zu überschreiben und die Aufgabe mit der Berechtigung des nicht Administrator Kontos des Benutzers auf dem Remote Computer auszuführen.

- So planen Sie, dass das Programm MyApp (als Benutzer) am letzten Tag jedes Monats auf dem Remote Computer *SRV02* ausgeführt wird.

    ```
    schtasks /create /s SRV02 /tn My App /tr c:\program files\corpapps\myapp.exe /sc monthly /mo LASTDAY /m * /u reskits\admin01
    ```

    Da der lokale aktuelle Benutzer (*user03*) kein Administrator des Remote Computers ist, verwendet der Befehl den **/u** -Parameter, um die Anmelde Informationen des Administrator Kontos des Benutzers (*"Admin01"* in der *reskits* -Domäne) bereitzustellen. Die Administrator Konto Berechtigungen werden verwendet, um die Aufgabe zu planen und die Aufgabe auszuführen.

    Da der Befehl den Parameter **/p** (Password) nicht enthielt, fordert Schtasks das Kennwort an. Daraufhin wird eine Erfolgsmeldung angezeigt, und in diesem Fall wird eine Warnung angezeigt:

    ```
    Type the password for reskits\admin01:********

    SUCCESS: The scheduled task My App has successfully been created.
    WARNING: The scheduled task My App has been created, but may not run because the account information could not be set.
    ```

    Diese Warnung gibt an, dass die Remote Domäne das vom Parameter **/u** angegebene Konto nicht authentifizieren konnte. In diesem Fall konnte die Remote Domäne das Benutzerkonto nicht authentifizieren, da der lokale Computer kein Mitglied einer Domäne ist, der die Remote Computer Domäne vertraut. In diesem Fall wird der Aufgaben Auftrag in der Liste der geplanten Aufgaben angezeigt, aber der Task ist tatsächlich leer und wird nicht ausgeführt.

    In der folgenden Anzeige aus einer ausführlichen Abfrage wird das Problem mit der Aufgabe angezeigt. Beachten Sie in der Anzeige, dass der Wert der **nächsten Laufzeit** **niemals** ist und dass der Wert von " **als Benutzer ausführen** " **nicht aus der Datenbank des Task Planers abgerufen werden konnte**.

    Wenn dieser Computer Mitglied derselben Domäne oder einer vertrauenswürdigen Domäne war, wurde der Task erfolgreich geplant und hätte wie angegeben ausgeführt werden können.

    ```
    HostName: SRV44
    TaskName: My App
    Next Run Time: Never
    Status:
    Logon mode: Interactive/Background
    Last Run Time: Never
    Last Result: 0
    Creator: user03
    Schedule: At 3:52 PM on day 31 of every month, start
    starting 12/14/2001
    Task To Run: c:\program files\corpapps\myapp.exe
    Start In: myapp.exe
    Comment: N/A
    Scheduled Task State: Disabled
    Scheduled Type: Monthly
    Start Time: 3:52:00 PM
    Start Date: 12/14/2001
    End Date: N/A
    Days: 31
    Months: JAN,FEB,MAR,APR,MAY,JUN,JUL,AUG,SEP,OCT,NO
    V,DEC
    Run As User: Could not be retrieved from the task sched
    uler database
    Delete Task If Not Rescheduled: Enabled
    Stop Task If Runs X Hours and X Mins: 72:0
    Repeat: Every: Disabled
    Repeat: Until: Time: Disabled
    Repeat: Until: Duration: Disabled
    Repeat: Stop If Still Running: Disabled
    Idle Time: Disabled
    Power Management: Disabled
    ```

#### <a name="remarks"></a>Hinweise

- Um den **/Create** -Befehl mit den Berechtigungen eines anderen Benutzers auszuführen, verwenden Sie den **/u** -Parameter. Der **/u** -Parameter ist nur für die Planung von Aufgaben auf Remote Computern gültig.

- Wenn Sie weitere `schtasks /create` Beispiele anzeigen möchten, geben Sie `schtasks /create /?` an einer Eingabeaufforderung ein.

- Verwenden Sie den **/ru** -Parameter, um eine Aufgabe zu planen, die mit Berechtigungen eines anderen Benutzers ausgeführt wird. Der **/ru** -Parameter ist für Aufgaben auf lokalen Computern und Remote Computern gültig.

- Zum Verwenden des **/u** -Parameters muss sich der lokale Computer in derselben Domäne befinden wie der Remote Computer, oder er muss sich in einer Domäne befinden, der die Remote Computer Domäne vertraut. Andernfalls wird entweder der Task nicht erstellt, oder der Aufgaben Auftrag ist leer, und der Task wird nicht ausgeführt.

- Von schtasks wird immer ein Kennwort angefordert, es sei denn, Sie geben ein Kennwort an, auch wenn Sie eine Aufgabe auf dem lokalen Computer mit dem aktuellen Benutzerkonto planen. Dies ist das normale Verhalten von Schtasks.

- "Schtasks" überprüft keine Programmdatei Speicherorte oder Kenn Wörter von Benutzerkonten. Wenn Sie nicht den richtigen Datei Speicherort oder das richtige Kennwort für das Benutzerkonto eingeben, wird die Aufgabe erstellt, aber Sie wird nicht ausgeführt. Wenn sich das Kennwort für ein Konto ändert oder abläuft und Sie das in der Aufgabe gespeicherte Kennwort nicht ändern, wird der Task ebenfalls nicht ausgeführt.

- Das **System** Konto verfügt nicht über interaktive Anmelde Rechte. Benutzer können nicht mit Programmen interagieren, die mit System Berechtigungen ausgeführt werden.

- Jeder Task führt nur ein Programm aus. Sie können jedoch eine Batchdatei erstellen, die mehrere Aufgaben startet, und dann eine Aufgabe planen, die die Batchdatei ausführt.

- Sie können eine Aufgabe testen, sobald Sie Sie erstellen. Verwenden Sie den Vorgang ausführen, um die Aufgabe zu testen, und überprüfen Sie dann die SchedLgU.txt Datei (SystemRoot\SchedLgU.txt) auf Fehler.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [schtasks-Änderungs Befehl](schtasks-change.md)

- [Befehl "Schtasks löschen"](schtasks-delete.md)

- [schtasks-Befehl "Ende"](schtasks-end.md)

- [schtasks-Abfragebefehl](schtasks-query.md)

- [Befehl "Schtasks ausführen"](schtasks-run.md)