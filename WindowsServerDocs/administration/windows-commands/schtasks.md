---
title: schtasks
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e713203-3dd8-491b-b9e1-9423618dc7e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fdda956a5da9ec50e44002cd8ab38373396d5713
ms.sourcegitcommit: 0e3c2473a54f915d35687d30d1b4b1ac2bae4068
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68914644"
---
# <a name="schtasks"></a>schtasks



Plant, dass Befehle und Programme regelmäßig oder zu einem bestimmten Zeitpunkt ausgeführt werden. Hinzufügen und Entfernen von Aufgaben aus dem Zeitplan, starten und Beenden von Aufgaben bei Bedarf und anzeigen und Ändern geplanter Aufgaben.

Um die Befehlssyntax anzuzeigen, klicken Sie auf einen der folgenden Befehle:
-   [schtasks erstellen](#BKMK_create)
-   [schtasks ändern](#BKMK_change)
-   [schtasks ausführen](#BKMK_run)
-   [schtasks beenden](#BKMK_end)
-   [schtasks löschen](#BKMK_delete)
-   [schtasks-Abfrage](#BKMK_query)

## <a name="remarks"></a>Hinweise

- " **Schtasks. exe** " führt die gleichen Vorgänge wie für **geplante Aufgaben** in der **Systemsteuerung**aus. Diese Tools können zusammen und austauschbar verwendet werden.
- **Schtasks** ersetzen in **. exe**, einem Tool, das in früheren Versionen von Windows enthalten war. Obwohl " **at. exe** " weiterhin in der Windows Server 2003-Familie enthalten ist, ist " **Schtasks** " das empfohlene Befehlszeilen Tool für die Task Planung.
- Die Parameter in einem **Schtasks** -Befehl können in beliebiger Reihenfolge angezeigt werden. Wenn Sie **Schtasks** ohne Parameter eingeben, wird eine Abfrage ausgeführt.
- Berechtigungen für " **Schtasks** "  
  -   Sie müssen über die Berechtigung zum Ausführen des Befehls verfügen. Jeder Benutzer kann eine Aufgabe auf dem lokalen Computer planen und die geplanten Tasks anzeigen und ändern. Mitglieder der Gruppe "Administratoren" können alle Tasks auf dem lokalen Computer planen, anzeigen und ändern.
  -   Zum Planen, anzeigen oder Ändern einer Aufgabe auf einem Remote Computer müssen Sie Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein, oder Sie müssen den **/u** -Parameter verwenden, um die Anmelde Informationen eines Administrators für den Remote Computer anzugeben.
  -   Sie können den **/u** -Parameter nur in einem **/Create** -oder **/Change** -Vorgang verwenden, wenn sich der lokale Computer und der Remote Computer in derselben Domäne befinden oder der lokale Computer sich in einer Domäne befindet, der die Remote Computer Domäne vertraut. Andernfalls kann der Remote Computer das angegebene Benutzerkonto nicht authentifizieren, und es kann nicht überprüft werden, ob das Konto Mitglied der Gruppe "Administratoren" ist.
  -   Die Aufgabe muss über die Berechtigung zum Ausführen verfügen. Welche Berechtigungen erforderlich sind, hängt von der Aufgabe ab. Standardmäßig werden Tasks mit den Berechtigungen des aktuellen Benutzers des lokalen Computers oder mit den Berechtigungen des Benutzers ausgeführt, der durch den **/u** -Parameter angegeben wird (sofern vorhanden). Verwenden Sie den **/ru** -Parameter, um einen Task mit Berechtigungen eines anderen Benutzerkontos oder mit System Berechtigungen auszuführen.
- Wenn Sie überprüfen möchten, ob eine geplante Aufgabe ausgeführt wurde, oder um herauszufinden, warum eine geplante Aufgabe nicht ausgeführt wurde, finden Sie weitere Informationen im Taskplaner-Dienst Transaktionsprotokoll *systemroot*\SchedLgU.txt. Diese Protokolldaten Sätze wurden von allen Tools initiiert, die den Dienst verwenden, einschließlich **geplanter Tasks** und " **Schtasks. exe**".
- In seltenen Fällen werden Aufgaben Dateien beschädigt. Beschädigte Tasks werden nicht ausgeführt. Wenn Sie versuchen, einen Vorgang für beschädigte Tasks auszuführen, zeigt " **Schtasks. exe** " die folgende Fehlermeldung an:  
  ```
  ERROR: The data is invalid.
  ```  
  Beschädigte Tasks können nicht wieder hergestellt werden. Um die Aufgaben Planungs Features des Systems wiederherzustellen, verwenden Sie " **Schtasks. exe** " oder " **geplante Tasks** ", um die Aufgaben aus dem System zu löschen und Sie neu zu planen.

## <a name="BKMK_create"></a>schtasks erstellen

Plant einen Task.

**Schtasks** verwendet für jeden Zeit Plantyp verschiedene Parameterkombinationen. Klicken Sie auf eine der folgenden Optionen, um die kombinierte Syntax zum Erstellen von Aufgaben oder zum Anzeigen der Syntax für das Erstellen einer Aufgabe mit einem bestimmten Zeit Plantyp anzuzeigen.
-   [Kombinierte Syntax und Parameter Beschreibungen](#BKMK_syntax)
-   [So planen Sie eine Aufgabe, die alle N Minuten ausgeführt wird](#BKMK_minutes)
-   [So planen Sie eine Aufgabe, die alle N Stunden ausgeführt wird](#BKMK_hours)
-   [So planen Sie einen Task, der alle N Tage ausgeführt wird](#BKMK_days)
-   [So planen Sie eine Aufgabe, die alle N Wochen ausgeführt wird](#BKMK_weeks)
-   [So planen Sie einen Task, der alle N Monate ausgeführt wird](#BKMK_months)
-   [So planen Sie einen Task, der an einem bestimmten Tag der Woche ausgeführt wird](#BKMK_spec_day)
-   [So planen Sie einen Task, der in einer bestimmten Woche des Monats ausgeführt wird](#BKMK_spec_week)
-   [So planen Sie einen Task, der monatlich an einem bestimmten Datum ausgeführt wird](#BKMK_spec_date)
-   [So planen Sie einen Task, der am letzten Tag eines Monats ausgeführt wird](#BKMK_last_day)
-   [So planen Sie einen Task, der einmal ausgeführt wird](#BKMK_once)
-   [So planen Sie einen Task, der bei jedem Systemstart ausgeführt wird](#BKMK_startup)
-   [So planen Sie einen Task, der ausgeführt wird, wenn sich ein Benutzer anmeldet](#BKMK_logon)
-   [So planen Sie einen Task, der ausgeführt wird, wenn das System im Leerlauf ist](#BKMK_idle)
-   [So planen Sie einen Task, der jetzt ausgeführt wird](#BKMK_now)
-   [So planen Sie einen Task, der mit unterschiedlichen Berechtigungen ausgeführt wird](#BKMK_diff_perms)
-   [So planen Sie einen Task, der mit System Berechtigungen ausgeführt wird](#BKMK_sys_perms)
-   [So planen Sie einen Task, der mehr als ein Programm ausführt](#BKMK_multi_progs)
-   [So planen Sie einen Task, der auf einem Remote Computer ausgeführt wird](#BKMK_remote)

### <a name="BKMK_syntax"></a>Kombinierte Syntax und Parameter Beschreibungen

#### <a name="syntax"></a>Syntax

```
schtasks /create /sc <ScheduleType> /tn <TaskName> /tr <TaskRun> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]] [/ru {[<Domain>\]<User> | System}] [/rp <Password>] [/mo <Modifier>] [/d <Day>[,<Day>...] | *] [/m <Month>[,<Month>...]] [/i <IdleTime>] [/st <StartTime>] [/ri <Interval>] [{/et <EndTime> | /du <Duration>} [/k]] [/sd <StartDate>] [/ed <EndDate>] [/it] [/z] [/f]
```

#### <a name="parameters"></a>Parameter

##### <a name="sc-scheduletype"></a>/SC \<ScheduleType >

Gibt den Zeit Plantyp an. Gültige Werte sind Minute, stündlich, täglich, wöchentlich, monatlich, einmal, OnStart, onlogon, OnIdle.

|Zeit Plantyp|Beschreibung|
|-------------|-----------|
|MINUTE, STÜNDLICH, TÄGLICH, WÖCHENTLICH, MONATLICH|Gibt die Zeiteinheit für den Zeitplan an.|
|EINMAL|Der Task wird einmal zu einem bestimmten Datum und zu einer bestimmten Uhrzeit ausgeführt.|
|ONSTART|Der Task wird jedes Mal ausgeführt, wenn das System gestartet wird. Wenn das System das nächste Mal gestartet wird, können Sie ein Startdatum angeben oder den Task ausführen.|
|PRO|Der Task wird immer dann ausgeführt, wenn sich ein Benutzer (Benutzer) anmeldet. Sie können ein Datum angeben oder den Task ausführen, wenn sich der Benutzer das nächste Mal anmeldet.|
|ONIDLE|Der Task wird immer dann ausgeführt, wenn sich das System für einen angegebenen Zeitraum im Leerlauf befindet. Sie können ein Datum angeben oder den Task ausführen, wenn sich das System das nächste Mal im Leerlauf befindet.|

##### <a name="tn-taskname"></a>/TN \<Taskname >

Gibt einen Namen für den Task an. Jede Aufgabe im System muss über einen eindeutigen Namen verfügen. Der Name muss den Regeln für Dateinamen entsprechen und darf nicht länger als 238 Zeichen sein. Verwenden Sie Anführungszeichen, um Namen einzuschließen, die Leerzeichen enthalten.

##### <a name="tr-taskrun"></a>/TR \<taskrun >

Gibt das Programm oder den Befehl an, das vom Task ausgeführt wird. Geben Sie den voll qualifizierten Pfad und den Dateinamen einer ausführbaren Datei, einer Skriptdatei oder einer Batchdatei ein. Der Pfadname darf nicht länger als 262 Zeichen sein. Wenn Sie den Pfad weglassen, geht **Schtasks** davon aus, dass sich die Datei im Verzeichnis " *systemroot*\System32" befindet.

##### <a name="s-computer"></a>/s \<Computer >

Plant einen Task auf dem angegebenen Remote Computer. Geben Sie den Namen oder die IP-Adresse eines Remote Computers ein (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden.

##### <a name="u-domainuser"></a>/u [\<Domänen >\]<User>

Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Der Standardwert sind die Berechtigungen des aktuellen Benutzers auf dem lokalen Computer. Die Parameter **/u** und **/p** sind nur für die Planung einer Aufgabe auf einem Remote Computer ( **/s**) gültig.

Die Berechtigungen des angegebenen Kontos werden verwendet, um den Task zu planen und den Task auszuführen. Verwenden Sie den **/ru** -Parameter, um den Task mit den Berechtigungen eines anderen Benutzers auszuführen.

Das Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Außerdem muss sich der lokale Computer in derselben Domäne befinden wie der Remote Computer, oder er muss sich in einer Domäne befinden, die von der Remote Computer Domäne als vertrauenswürdig eingestuft wird.

##### <a name="p-password"></a>/p \<Password >

Gibt das Kennwort für das Benutzerkonto an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter verwenden, aber den **/p** -Parameter oder das Password-Argument weglassen, werden Sie von **Schtasks** zur Eingabe eines Kennworts aufgefordert, und der von Ihnen eingeladene Text wird verdeckt.

Die Parameter **/u** und **/p** sind nur für die Planung einer Aufgabe auf einem Remote Computer ( **/s**) gültig.

##### <a name="ru-domainuser--system"></a>/ru {[\<Domäne >\] <User> | Anlage

Führt den Task mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Task mit den Berechtigungen des aktuellen Benutzers des lokalen Computers oder mit der Berechtigung des Benutzers ausgeführt, der durch den **/u** -Parameter angegeben wird (sofern vorhanden). Der **/ru** -Parameter ist beim Planen von Aufgaben auf lokalen Computern oder Remote Computern gültig.


|       Wert        |                                                    Beschreibung                                                    |
|--------------------|-------------------------------------------------------------------------------------------------------------------|
| [\<Domänen >\]<User> |                                       Gibt ein alternatives Benutzerkonto an.                                        |
|    System oder ""    | Gibt das lokale System Konto an, ein Konto mit hohen Privilegien, das vom Betriebssystem und den System Diensten verwendet wird. |

##### <a name="rp-password"></a>/RP aus \<Password >

Gibt das Kennwort für das Benutzerkonto an, das im **/ru** -Parameter angegeben ist. Wenn Sie diesen Parameter nicht angeben, wenn Sie ein Benutzerkonto angeben, werden Sie von " **Schtasks. exe** " zur Eingabe des Kennworts aufgefordert und der von Ihnen typisierte Text verdeckt.

Verwenden Sie den **/RP aus** -Parameter nicht für Aufgaben, die mit den Anmelde Informationen des System Kontos ( **/ru System**) ausgeführt werden. Das System Konto verfügt nicht über ein Kennwort, und " **Schtasks. exe** " fordert nicht zu einer Eingabe auf.

##### <a name="mo-modifier"></a>/Monat \<-Modifizierer >

Gibt an, wie oft die Aufgabe innerhalb Ihres Zeit Plan Typs ausgeführt wird. Dieser Parameter ist gültig, aber optional für eine Minute, stündlich, täglich, wöchentlich und monatlich. Der Standardwert ist 1.

|Zeit Plantyp|Modifiziererwerte|Beschreibung|
|-------------|---------------|-----------|
|TIGES|1 - 1439|Der Task wird alle \<N > Minuten ausgeführt.|
|LOHNS|1 - 23|Der Task wird alle \<N > Stunden ausgeführt.|
|TÄ|1 - 365|Der Task wird alle \<N > Tage ausgeführt.|
|ARBEI|1 - 52|Der Task wird alle \<N > Wochen ausgeführt.|
|EINMAL|Keine Modifizierer.|Der Task wird einmal ausgeführt.|
|ONSTART|Keine Modifizierer.|Der Task wird beim Start ausgeführt.|
|PRO|Keine Modifizierer.|Der Task wird ausgeführt, wenn sich der durch den **/u** -Parameter angegebene Benutzer anmeldet.|
|ONIDLE|Keine Modifizierer.|Der Task wird ausgeführt, nachdem das System für die Anzahl der Minuten im Leerlauf ist, die durch den **/i** -Parameter angegeben wird, der für die Verwendung mit OnIdle erforderlich ist.|
|MONATLICH|1 - 12|Der Task wird alle \<N > Monaten ausgeführt.|
|MONATLICH|NACHNAME|Der Task wird am letzten Tag des Monats ausgeführt.|
|MONATLICH|ERSTER, ZWEITER, DRITTER, VIERTER, LETZTER|Verwenden Sie mit dem **/d**\<Day >-Parameter, um eine Aufgabe für eine bestimmte Woche und einen bestimmten Tag auszuführen. Beispielsweise am dritten Mittwoch des Monats.|

##### <a name="d-dayday--"></a>/d Day [, Day...] | *

Gibt einen Tag (oder Tage) der Woche oder einen Tag (oder Tage) eines Monats an. Nur mit wöchentlichem oder monatlichem Zeitplan gültig.


| Zeit Plantyp |              Modifikator              |     Tageswerte (/d)      |                                                                                                 Beschreibung                                                                                                 |
|---------------|------------------------------------|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    ARBEI     |               1 - 52               | MON-SUN [, MON-SUN...] |                                                                                                     \*                                                                                                      |
|    MONATLICH    | ERSTER, ZWEITER, DRITTER, VIERTER, LETZTER |        MON-SUN         |                                                                                   Für einen bestimmten Wochen Zeitplan erforderlich.                                                                                    |
|    MONATLICH    |          None oder {1-12}          |          1 - 31          | Optional und gültig nur ohne modifiziererparameter ( **/Monat**) (ein bestimmtes Datums Zeitplan) oder wenn **/Monat** 1-12 ist (ein "alle \<N > Monate"-Zeitplan). Der Standardwert ist Day 1 (der erste Tag des Monats). |

##### <a name="m-monthmonth"></a>/m Monat [, Monat...]

Gibt einen Monat oder einen Monat des Jahres an, in dem die geplante Aufgabe ausgeführt werden soll. Gültige Werte sind "Jan-Dec" und "*" (monatlich). Der **/m** -Parameter ist nur mit einem monatlichen Zeitplan gültig. Dies ist erforderlich, wenn der lastday-Modifizierer verwendet wird. Andernfalls ist Sie optional, und der Standardwert ist * (monatlich).

##### <a name="i-idletime"></a>/i \<IdleTime->

Gibt an, wie viele Minuten sich der Computer im Leerlauf befindet, bevor der Task gestartet wird. Ein gültiger Wert ist eine ganze Zahl zwischen 1 und 999. Dieser Parameter ist nur mit einem OnIdle-Zeitplan gültig und wird dann benötigt.

##### <a name="st-starttime"></a>/St \<StartTime->

Gibt die Uhrzeit an, zu der die Aufgabe gestartet wird (bei jedem Start) \<im Format hh: mm > 24-Stunden-Format. Der Standardwert ist die aktuelle Uhrzeit auf dem lokalen Computer. Der **/St** -Parameter ist mit Minuten-, stündlichen, täglichen, wöchentlichen, monatlichen und Once-Zeitplänen gültig. Er ist für einen einmaligen Zeitplan erforderlich.

##### <a name="ri-interval"></a>/RI \<Intervall >

Gibt das Wiederholungsintervall in Minuten an. Dies gilt nicht für Zeit Plan Typen: Minute, stündlich, OnStart, onlogon und OnIdle. Der gültige Bereich liegt zwischen 1 und 599940 Minuten (599940 Minuten = 9999 Stunden). Wenn entweder/et oder/du angegeben wird, wird das Wiederholungsintervall standardmäßig auf 10 Minuten festgelegt.

##### <a name="et-endtime"></a>/et \<EndTime->

Gibt die Uhrzeit an, zu der ein Minuten-oder stündlicher Aufgaben \<Zeitplan im Format hh: mm > 24-Stunden-Format endet. Nach der angegebenen Endzeit startet **Schtasks** die Aufgabe erst wieder, wenn die Startzeit wiederholt wird. Standardmäßig haben Aufgaben Zeitpläne keine Endzeit. Dieser Parameter ist optional und nur mit einem Minuten-oder stündlichen Zeitplan gültig.

Ein Beispiel finden Sie unter:
-   "So planen Sie einen Task, der während außerhalb der Geschäftszeiten alle 100 Minuten ausgeführt wird" im **, um eine Aufgabe zu planen, die alle** \<N > **Minuten** -Abschnitt ausgeführt wird.

##### <a name="du-duration"></a>/Du \<Dauer >

Gibt eine maximale Zeitdauer für eine Minute oder einen stündlichen Zeitplan \<im Format HHHH: mm > 24-Stunden-Format an. Nachdem die angegebene Zeit abgelaufen ist, startet **Schtasks** die Aufgabe erst wieder, wenn die Startzeit wiederholt wird. Standardmäßig haben Aufgaben Zeitpläne keine maximale Dauer. Dieser Parameter ist optional und nur mit einem Minuten-oder stündlichen Zeitplan gültig.

Ein Beispiel finden Sie unter:
-   "So planen Sie einen Task, der für 10 Stunden alle drei Stunden ausgeführt wird" in der **, um eine Aufgabe zu planen, die alle** \<N > **Stunden** Abschnitt ausgeführt wird.

##### <a name="k"></a>/k

Beendet das Programm, das der Task ausführt, zu dem Zeitpunkt, der durch **/et** oder **/du**angegeben wird. Ohne **/k**startet **Schtasks** das Programm nicht erneut, nachdem es die von **/et** oder **/du**angegebene Zeit erreicht hat, aber das Programm wird nicht beendet, wenn es noch ausgeführt wird. Dieser Parameter ist optional und nur mit einem Minuten-oder stündlichen Zeitplan gültig.

Ein Beispiel finden Sie unter:
-   "So planen Sie einen Task, der während außerhalb der Geschäftszeiten alle 100 Minuten ausgeführt wird" im **, um eine Aufgabe zu planen, die alle** \<N > **Minuten** -Abschnitt ausgeführt wird.

##### <a name="sd-startdate"></a>/SD \<StartDate >

Gibt das Datum an, an dem der Task Zeitplan gestartet wird. Der Standardwert ist das aktuelle Datum auf dem lokalen Computer. Der **/SD** -Parameter ist gültig und für alle Zeit Plan Typen optional.

Das Format für *StartDate* variiert abhängig von dem für den lokalen Computer ausgewählten Gebiets Schema in den Regions **-und Sprachoptionen** in der **Systemsteuerung**. Für jedes Gebiets Schema ist nur ein Format gültig.

Die gültigen Datumsformate sind in der folgenden Tabelle aufgeführt. Verwenden Sie das Format, das in der Systemsteuerung auf dem lokalen Computer in der **Systemsteuerung in der Systemsteuerung** für **kurzes Datum** am ähnlichsten ist.


|       Wert       |                                        Beschreibung                                         |
|-------------------|--------------------------------------------------------------------------------------------|
| \<MM >/<DD>/<YYYY> | Verwenden Sie für month First-Formate, z. b. **Englisch (USA)** und **Spanisch (Panama)** . |
| \<DD >/<MM>/<YYYY> |       Verwenden Sie für Day-First-Formate, z. b. **Bulgarisch** und **Niederländisch (Niederlande)** .        |
| \<YYYY >/<MM>/<DD> |          Verwenden Sie für Year First-Formate, z. b. **Schwedisch** und **Französisch (Kanada)** .          |

/Ed \<EndDate >

Gibt das Datum an, an dem der Zeitplan endet. Dieser Parameter ist optional. Er ist nicht in einem Once-, OnStart-, onlogon-oder OnIdle-Zeitplan gültig. Standardmäßig haben Zeitpläne kein Enddatum.

Das Format für *EndDate* variiert abhängig von dem für den lokalen Computer ausgewählten Gebiets Schema in den Regions **-und Sprachoptionen** in der **Systemsteuerung**. Für jedes Gebiets Schema ist nur ein Format gültig.

Die gültigen Datumsformate sind in der folgenden Tabelle aufgeführt. Verwenden Sie das Format, das in der Systemsteuerung auf dem lokalen Computer in der **Systemsteuerung in der Systemsteuerung** für **kurzes Datum** am ähnlichsten ist.


|       Wert       |                                        Beschreibung                                         |
|-------------------|--------------------------------------------------------------------------------------------|
| \<MM >/<DD>/<YYYY> | Verwenden Sie für month First-Formate, z. b. **Englisch (USA)** und **Spanisch (Panama)** . |
| \<DD >/<MM>/<YYYY> |       Verwenden Sie für Day-First-Formate, z. b. **Bulgarisch** und **Niederländisch (Niederlande)** .        |
| \<YYYY >/<MM>/<DD> |          Verwenden Sie für Year First-Formate, z. b. **Schwedisch** und **Französisch (Kanada)** .          |

##### <a name="it"></a>/it

Gibt an, dass die Aufgabe nur ausgeführt wird, wenn der Benutzer, unter dem der Task ausgeführt wird, auf dem Computer angemeldet ist. Dieser Parameter hat keine Auswirkung auf Aufgaben, die mit System Berechtigungen ausgeführt werden.

Standardmäßig ist der Benutzer "Ausführen als" der aktuelle Benutzer des lokalen Computers, wenn der Task geplant ist, oder das durch den **/u** -Parameter angegebene Konto (sofern verwendet). Wenn der Befehl jedoch den **/ru** -Parameter enthält, ist der Benutzer "Ausführen als" das Konto, das durch den **/ru** -Parameter angegeben wird.

Beispiele finden Sie unter:
-   "Um eine Aufgabe zu planen, die alle 70 Tage ausgeführt wird, wenn ich angemeldet bin" in der **, um eine Aufgabe zu planen, die alle** *N* **Tage** läuft.
-   "So führen Sie eine Aufgabe nur aus, wenn ein bestimmter Benutzer angemeldet ist" im **, um eine Aufgabe zu planen, die mit unterschiedlichen Berechtigungen** ausgeführt wird.

##### <a name="z"></a>"/z

Gibt an, dass die Aufgabe nach Abschluss des Zeitplans gelöscht wird.

##### <a name="f"></a>/f

Gibt an, dass die Aufgabe erstellt und Warnungen unterdrückt werden sollen, wenn die angegebene Aufgabe bereits vorhanden ist.

##### <a name=""></a>/?

Zeigt die Hilfe an der Eingabeaufforderung an.

### <a name="BKMK_minutes"></a>So planen Sie eine Aufgabe, die alle N Minuten ausgeführt wird

#### <a name="minute-schedule-syntax"></a>Syntax für Minuten Zeitplan

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc minute [/mo {1 - 1439}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [{/et <HH:MM> | /du <HHHH:MM>} [/k]] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Der **/SC Minute** -Parameter ist in einem Minuten Zeitplan erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Minuten zwischen den einzelnen Aufgaben an. Der Standardwert für **/Monat** ist 1 (jede Minute). Die Parameter **/et** (Endzeit) und **/du** (Duration) sind optional und können mit oder ohne den Parameter **/k** (End Task) verwendet werden.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-20-minutes"></a>So planen Sie einen Task, der alle 20 Minuten ausgeführt wird

Der folgende Befehl plant, dass ein Sicherheits Skript, "s. VSB", alle 20 Minuten ausgeführt wird. Der Befehl verwendet den **/SC** -Parameter, um einen Minuten Zeitplan anzugeben, und den **/Monat** -Parameter, um ein Intervall von 20 Minuten anzugeben.

Da der Befehl kein Startdatum oder keine Uhrzeit enthält, wird die Aufgabe 20 Minuten nach Abschluss des Befehls gestartet und dann alle 20 Minuten ausgeführt, wenn das System ausgeführt wird. Beachten Sie, dass sich die Sicherheits Skript-Quelldatei auf einem Remote Computer befindet, aber dass der Task geplant und auf dem lokalen Computer ausgeführt wird.
```
schtasks /create /sc minute /mo 20 /tn "Security Script" /tr \\central\data\scripts\sec.vbs
```

#### <a name="to-schedule-a-task-that-runs-every-100-minutes-during-non-business-hours"></a>So planen Sie einen Task, der während außerhalb der Geschäftszeiten alle 100 Minuten ausgeführt wird

Der folgende Befehl plant, dass ein Sicherheits Skript, "s. VSB", alle 100 Minuten zwischen 5:00 Uhr auf dem lokalen Computer ausgeführt wird. und 7:59 Uhr jeden Tag. Der Befehl verwendet den **/SC** -Parameter, um einen Minuten Zeitplan anzugeben, und den **/Monat** -Parameter, um ein Intervall von 100 Minuten anzugeben. Er verwendet die Parameter **/St** und **/et** , um die Startzeit und Endzeit des Zeitplans für jeden Tag anzugeben. Außerdem verwendet er den **/k** -Parameter, um das Skript zu unterbinden, wenn es noch um 7:59 Uhr morgens ausgeführt wird. Ohne **/k**wird das Skript von **Schtasks** nach 7:59 Uhr nicht gestartet, aber wenn die Instanz um 6:20 Uhr gestartet wurde. wird noch ausgeführt, wird Sie nicht angehalten.
```
schtasks /create /tn "Security Script" /tr sec.vbs /sc minute /mo 100 /st 17:00 /et 08:00 /k
```

### <a name="BKMK_hours"></a>So planen Sie eine Aufgabe, die alle N Stunden ausgeführt wird

#### <a name="hourly-schedule-syntax"></a>Syntax für stündliche Zeitpläne

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc hourly [/mo {1 - 23}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [{/et <HH:MM> | /du <HHHH:MM>} [/k]] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

In einem stündlichen Zeitplan ist der **stündliche/SC** -Parameter erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Stunden zwischen den einzelnen Tasks der Aufgabe an. Der Standardwert für **/Monat** ist 1 (stündlich). Der **/k** -Parameter (End-Task) ist optional und kann entweder mit **/et** (Ende zum angegebenen Zeitpunkt) oder **/du** (Ende nach dem angegebenen Intervall) verwendet werden.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-five-hours"></a>So planen Sie einen Task, der alle fünf Stunden ausgeführt wird

Der folgende Befehl plant, dass das MyApp-Programm alle fünf Stunden ab dem ersten Tag des 2002. März ausgeführt wird. Er verwendet den **/Monat** -Parameter, um das Intervall anzugeben, und den **/SD** -Parameter, um das Startdatum anzugeben. Da der Befehl keine Startzeit angibt, wird die aktuelle Uhrzeit als Startzeit verwendet.

Da der lokale Computer auf die Option **Englisch (Simbabwe)** in den Regions **-und Sprachoptionen** in der **Systemsteuerung**festgelegt ist, ist das Format für das Startdatum mm/dd/yyyy (03/01/2002).
```
schtasks /create /sc hourly /mo 5 /sd 03/01/2002 /tn "My App" /tr c:\apps\myapp.exe
```

#### <a name="to-schedule-a-task-that-runs-every-hour-at-five-minutes-past-the-hour"></a>So planen Sie einen Task, der stündlich in fünf Minuten nach der vollen Stunde ausgeführt wird

Mit dem folgenden Befehl wird das Programm "MyApp" auf Stundenbasis mit fünf Minuten nach Mitternacht geplant. Da der **/Monat** -Parameter weggelassen wird, verwendet der Befehl den Standardwert für den stündlichen Zeitplan, der alle (1) Stunde beträgt. Wenn dieser Befehl nach 12:05 Uhr ausgeführt wird, wird das Programm bis zum nächsten Tag nicht ausgeführt.
```
schtasks /create /sc hourly /st 00:05 /tn "My App" /tr c:\apps\myapp.exe
```

#### <a name="to-schedule-a-task-that-runs-every-3-hours-for-10-hours"></a>So planen Sie einen Task, der alle drei Stunden ausgeführt wird, für 10 Stunden

Der folgende Befehl plant, dass das MyApp-Programm 10 Stunden lang alle drei Stunden ausgeführt wird.

Der Befehl verwendet den **/SC** -Parameter, um einen stündlichen Zeitplan anzugeben, und den **/Monat** -Parameter, um das Intervall von drei Stunden anzugeben. Er verwendet den **/St** -Parameter, um den Zeitplan um Mitternacht zu starten, und den **/du** -Parameter, um die rekurrenzen nach 10 Stunden zu beenden. Da das Programm nur wenige Minuten ausgeführt wird, ist der **/k** -Parameter, der das Programm beendet, wenn es noch ausgeführt wird, wenn die Dauer abläuft, nicht erforderlich.
```
schtasks /create /tn "My App" /tr myapp.exe /sc hourly /mo 3 /st 00:00 /du 0010:00
```
In diesem Beispiel wird die Aufgabe um 12:00 Uhr, 3:00 Uhr, 6:00 Uhr und 9:00 Uhr ausgeführt. Da die Dauer 10 Stunden beträgt, wird die Aufgabe nicht erneut um 12:00 Uhr ausgeführt. Stattdessen wird er um 12:00 Uhr wieder gestartet. der nächste Tag.

### <a name="BKMK_days"></a>So planen Sie einen Task, der alle N Tage ausgeführt wird

#### <a name="daily-schedule-syntax"></a>Syntax für den täglichen Zeitplan

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc daily [/mo {1 - 365}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Der **/SC Daily** -Parameter ist in einem täglichen Zeitplan erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Tage zwischen den einzelnen Tasks der Aufgabe an. Der Standardwert für **/Monat** ist 1 (täglich).

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-day"></a>So planen Sie einen täglich ausgeführten Task

Im folgenden Beispiel wird das Programm "MyApp" für jeden Tag um 8:00 Uhr geplant. bis zum 31. Dezember 2002. Da der **/Monat** -Parameter ausgelassen wird, wird das Standardintervall 1 verwendet, um den Befehl jeden Tag auszuführen.

Da in diesem Beispiel das lokale Computersystem auf die Option **Englisch (Großbritannien)** in den Regions **-und Sprachoptionen** in der **Systemsteuerung**festgelegt ist, ist das Format für das Enddatum dd/mm/yyyy (31/12/2002).
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc daily /st 08:00 /ed 31/12/2002
```

#### <a name="to-schedule-a-task-that-runs-every-12-days"></a>So planen Sie einen Task, der alle 12 Tage ausgeführt wird

Im folgenden Beispiel wird geplant, dass das Programm MyApp alle zwölf Tage um 1:00 Uhr ausgeführt wird. (13:00) ab dem 31. Dezember 2002. Der Befehl verwendet den **/Monat** -Parameter, um ein Intervall von zwei (2) Tagen anzugeben, und den **/SD** -und **/St** -Parameter, um das Datum und die Uhrzeit anzugeben.

Da das System in diesem Beispiel auf die Option **Englisch (Simbabwe)** in den Regions **-und Sprachoptionen** in der System **Steuerung**festgelegt ist, ist das Format für das Enddatum mm/dd/yyyy (12/31/2002).
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc daily /mo 12 /sd 12/31/2002 /st 13:00
```

#### <a name="to-schedule-a-task-that-runs-every-70-days-if-i-am-logged-on"></a>So planen Sie einen Task, der alle 70 Tage bei der Anmeldung ausgeführt wird

Der folgende Befehl plant, dass ein Sicherheits Skript, "s. VSB", alle 70 Tage ausgeführt wird. Der Befehl verwendet den **/Monat** -Parameter, um ein Intervall von 70 Tagen anzugeben. Außerdem wird der **/IT** -Parameter verwendet, um anzugeben, dass der Task nur ausgeführt wird, wenn der Benutzer, der den Task ausführt, auf dem Computer angemeldet ist. Da die Aufgabe mit den Berechtigungen des Benutzerkontos ausgeführt wird, wird die Aufgabe nur dann ausgeführt, wenn Sie angemeldet sind.
```
schtasks /create /tn "Security Script" /tr sec.vbs /sc daily /mo 70 /it
```

> [!NOTE]
> Verwenden Sie eine ausführliche Abfrage **(/Query "aus/v**), um Aufgaben mit der interaktiven ( **/IT**)-Eigenschaft zu identifizieren. In einer ausführlichen Abfrage Anzeige einer Aufgabe mit **/IT**hat das Feld **Anmeldemodus** den Wert **interaktiv**.

### <a name="BKMK_weeks"></a>So planen Sie eine Aufgabe, die alle N Wochen ausgeführt wird

#### <a name="weekly-schedule-syntax"></a>Syntax für den wöchentlichen Zeitplan

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc weekly [/mo {1 - 52}] [/d {<MON - SUN>[,MON - SUN...] | *}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

In einem wöchentlichen Zeitplan ist der **wöchentliche/SC** -Parameter erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Wochen zwischen den einzelnen Tasks der Aufgabe an. Der Standardwert für **/Monat** ist 1 (jede Woche).

Wöchentliche Zeitpläne verfügen auch über einen optionalen **/d** -Parameter, um zu planen, dass die Aufgabe an bestimmten Wochentagen oder an allen Tagen *() ausgeführt wird. Der Standardwert ist Mon (Montag). Die Option für jeden*Tag () entspricht dem Planen einer täglichen Aufgabe.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-six-weeks"></a>So planen Sie einen Task, der alle sechs Wochen ausgeführt wird

Der folgende Befehl plant, dass das MyApp-Programm alle sechs Wochen auf einem Remote Computer ausgeführt wird. Der Befehl verwendet den **/Monat** -Parameter, um das Intervall anzugeben. Da der Befehl den **/d** -Parameter auslässt, wird der Task am Montag ausgeführt.

Dieser Befehl verwendet auch den **/s** -Parameter, um den Remote Computer anzugeben, und den **/u** -Parameter, um den Befehl mit den Berechtigungen des Benutzer Administrator Kontos auszuführen. Da der **/p** -Parameter weggelassen wird, fordert " **Schtasks. exe** " den Benutzer zur Eingabe des Kennworts für das Administrator Konto auf.

Da der Befehl auch remote ausgeführt wird, verweisen alle Pfade im Befehl, einschließlich des Pfads zu "MyApp. exe", auf Pfade auf dem Remote Computer.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /mo 6 /s Server16 /u Admin01
```

#### <a name="to-schedule-a-task-that-runs-every-other-week-on-friday"></a>So planen Sie einen Task, der alle anderen Wochen am Freitag ausgeführt wird

Der folgende Befehl plant einen Task, der an jedem anderen Freitag ausgeführt wird. Er verwendet den **/Monat** -Parameter, um das zweiwöchige Intervall anzugeben, und den **/d** -Parameter zum Angeben des Wochentags. Um einen Task zu planen, der jeden Freitag ausgeführt wird, lassen Sie den **/Monat** -Parameter Weg, oder legen Sie ihn auf 1 fest.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /mo 2 /d FRI
```

### <a name="BKMK_months"></a>So planen Sie einen Task, der alle N Monate ausgeführt wird

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly [/mo {1 - 12}] [/d {1 - 31}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

In diesem Zeit Plantyp ist der **monatliche/SC** -Parameter erforderlich. Der **/Monat** (Modifier)-Parameter, der die Anzahl der Monate zwischen den einzelnen Aufgaben der Aufgabe angibt, ist optional, und der Standardwert ist 1 (jeden Monat). Dieser Zeit Plantyp verfügt auch über einen optionalen **/d** -Parameter, um zu planen, dass die Aufgabe an einem bestimmten Tag des Monats ausgeführt wird. Der Standardwert ist 1 (der erste Tag des Monats).

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-on-the-first-day-of-every-month"></a>So planen Sie einen Task, der am ersten Tag eines jeden Monats ausgeführt wird

Der folgende Befehl plant, dass das MyApp-Programm am ersten Tag jedes Monats ausgeführt wird. Da der Wert 1 der Standardwert für den Parameter **/Monat** (Modifier) und den Parameter **/d** (Day) ist, werden diese Parameter im Befehl ausgelassen.
```
schtasks /create /tn "My App" /tr myapp.exe /sc monthly
```

#### <a name="to-schedule-a-task-that-runs-every-three-months"></a>So planen Sie einen Task, der alle drei Monate ausgeführt wird

Der folgende Befehl plant, dass das Programm MyApp alle drei Monate ausgeführt wird. Er verwendet den **/Monat** -Parameter, um das Intervall anzugeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo 3
```

#### <a name="to-schedule-a-task-that-runs-at-midnight-on-the-21st-day-of-every-other-month"></a>So planen Sie einen Task, der am 21. Tag jedes anderen Monats um Mitternacht ausgeführt wird

Der folgende Befehl plant, dass das Programm MyApp jeden anderen Monat am 21. Tag des Monats um Mitternacht ausgeführt wird. Der Befehl gibt an, dass diese Aufgabe ein Jahr, vom 2002 2. Juli bis zum 30. Juni 2003 ausgeführt werden soll.

Der Befehl verwendet den **/Monat** -Parameter, um das monatliche Intervall (alle zwei Monate), den **/d** -Parameter, um das Datum anzugeben, und die **/St** zum Angeben der Zeit anzugeben. Außerdem werden der **/SD** -und der **/Ed** -Parameter verwendet, um das Startdatum bzw. das Enddatum anzugeben. Da der lokale Computer auf die Option **Englisch (Südafrika)** in den Regions **-und Sprachoptionen** in der **Systemsteuerung**festgelegt ist, werden die Datumsangaben im lokalen Format yyyy/mm/dd angegeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo 2 /d 21 /st 00:00 /sd 2002/07/01 /ed 2003/06/30 
```

### <a name="BKMK_spec_day"></a>So planen Sie einen Task, der an einem bestimmten Tag der Woche ausgeführt wird

#### <a name="weekly-schedule-syntax"></a>Syntax für den wöchentlichen Zeitplan

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc weekly [/d {<MON - SUN>[,MON - SUN...] | *}] [/mo {1 - 52}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Der Zeitplan "Wochentag" ist eine Variation des wöchentlichen Zeitplans. In einem wöchentlichen Zeitplan ist der **wöchentliche/SC** -Parameter erforderlich. Der **/Monat** -Parameter (Modifier) ist optional und gibt die Anzahl der Wochen zwischen den einzelnen Tasks der Aufgabe an. Der Standardwert für **/Monat** ist 1 (jede Woche). Der optionale Parameter **/d** plant, dass der Task an bestimmten Wochentagen oder an allen Tagen (\*) ausgeführt wird. Der Standardwert ist Mon (Montag). Die Option für jeden Tag **( \*/d** ) entspricht dem Planen einer täglichen Aufgabe.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-wednesday"></a>So planen Sie einen Task, der jeden Mittwoch ausgeführt wird

Der folgende Befehl plant, dass das Programm MyApp jede Woche am Mittwoch ausgeführt wird. Der Befehl verwendet den **/d** -Parameter zum Angeben des Wochentags. Da der Befehl den **/Monat** -Parameter auslässt, wird die Aufgabe jede Woche ausgeführt.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /d WED
```

#### <a name="to-schedule-a-task-that-runs-every-eight-weeks-on-monday-and-friday"></a>So planen Sie einen Task, der alle acht Wochen am Montag und Freitag ausgeführt wird

Der folgende Befehl plant, dass eine Aufgabe am Montag und Freitag jeder acht Woche ausgeführt wird. Er verwendet den **/d** -Parameter, um die Tage anzugeben, und den **/Monat** -Parameter, um das achtwöchige Intervall anzugeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /mo 8 /d MON,FRI
```

### <a name="BKMK_spec_week"></a>So planen Sie einen Task, der in einer bestimmten Woche des Monats ausgeführt wird

#### <a name="specific-week-syntax"></a>Syntax für bestimmte Wochen

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly /mo {FIRST | SECOND | THIRD | FOURTH | LAST} /d MON - SUN [/m {JAN - DEC[,JAN - DEC...] | *}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

In diesem Zeit Plantyp sind der **/SC monatlich** -Parameter, der **/Monat** -Parameter (Modifier) und der **/d** (Day)-Parameter erforderlich. Der **/Monat** (Modifier)-Parameter gibt die Woche an, in der die Aufgabe ausgeführt wird. Der **/d** -Parameter gibt den Wochentag an. (Sie können für diesen Zeit Plantyp nur einen Tag der Woche angeben.) Dieser Zeitplan verfügt auch über einen optionalen **/m** (month)-Parameter, mit dem Sie den Task für bestimmte Monate oder jeden\*Monat () planen können. Der Standardwert für den **/m** -Parameter ist monatlich\*().

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-for-the-second-sunday-of-every-month"></a>So planen Sie einen Task für den zweiten Sonntag jedes Monats

Der folgende Befehl plant, dass das Programm MyApp am zweiten Sonntag jeden Monats ausgeführt wird. Er verwendet den **/Monat** -Parameter, um die zweite Woche des Monats anzugeben, und den **/d** -Parameter, um den Tag anzugeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo SECOND /d SUN
```

#### <a name="to-schedule-a-task-for-the-first-monday-in-march-and-september"></a>So planen Sie einen Task für den ersten Montag im März und September

Der folgende Befehl plant, dass das MyApp-Programm am ersten Montag im März und September ausgeführt wird. Er verwendet den **/Monat** -Parameter, um die erste Woche des Monats anzugeben, und den **/d** -Parameter, um den Tag anzugeben. Er verwendet den **/m** -Parameter, um den Monat anzugeben, wobei die Month-Argumente durch ein Komma getrennt werden.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo FIRST /d MON /m MAR,SEP
```

### <a name="BKMK_spec_date"></a>So planen Sie einen Task, der monatlich an einem bestimmten Datum ausgeführt wird

#### <a name="specific-date-syntax"></a>Bestimmte Datums Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly /d {1 - 31} [/m {JAN - DEC[,JAN - DEC...] | *}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Der **/SC monatlich** -Parameter und der **/d** (Day)-Parameter sind in einem bestimmten Datums Plantyp erforderlich. Der **/d** -Parameter gibt ein Datum des Monats (1-31) und keinen Wochentag an. Sie können im Zeitplan nur einen Tag angeben. Der **/Monat** -Parameter (Modifier) ist mit diesem Zeit Plantyp nicht gültig.

Der **/m** -Parameter (month) ist für diesen Zeit Plantyp optional, und der Standardwert ist monatlich (<em>). **Schtasks</em>*  ermöglicht keine Planung einer Aufgabe für ein Datum, das nicht in einem durch den **/m** -Parameter angegebenen Monat auftritt. Wenn Sie jedoch den **/m** -Parameter weglassen und eine Aufgabe für ein Datum planen, das nicht in jedem Monat angezeigt wird (z. b. am 31. Tag), wird die Aufgabe nicht in den kürzeren Monaten ausgeführt. Um einen Task für den letzten Tag des Monats zu planen, verwenden Sie den Zeitplan für den letzten Tag des Monats.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-for-the-first-day-of-every-month"></a>So planen Sie einen Task für den ersten Tag eines jeden Monats

Der folgende Befehl plant, dass das MyApp-Programm am ersten Tag jedes Monats ausgeführt wird. Da der Standardmodifizierer None (kein Modifizierer), der Standardtag 1 ist und der Standard Monat jeden Monat ist, benötigt der Befehl keine zusätzlichen Parameter.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly
```

#### <a name="to-schedule-a-task-for-the-15th-days-of-may-and-june"></a>So planen Sie eine Aufgabe für die 15. Tage von Mai und Juni

Der folgende Befehl plant, dass das MyApp-Programm am 15. Mai und 15. Juni um 3:00 Uhr ausgeführt wird. (15:00). Er verwendet den **/m** -Parameter, um das Datum anzugeben, und den **/m** -Parameter, um die Monate anzugeben. Außerdem verwendet er den **/St** -Parameter, um die Startzeit anzugeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /d 15 /m MAY,JUN /st 15:00
```

### <a name="BKMK_last_day"></a>So planen Sie einen Task, der am letzten Tag eines Monats ausgeführt wird

#### <a name="last-day-syntax"></a>Syntax des letzten Tags

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly /mo LASTDAY /m {JAN - DEC[,JAN - DEC...] | *} [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Im Zeit Plantyp für den letzten Tag sind der **/SC monatlich** -Parameter, der **/Monat lastday** -Parameter (Modifier) und der **/m** -Parameter (month) erforderlich. Der **/d** (Day)-Parameter ist ungültig.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-for-the-last-day-of-every-month"></a>So planen Sie einen Task für den letzten Tag eines jeden Monats

Der folgende Befehl plant, dass das Programm MyApp am letzten Tag jedes Monats ausgeführt wird. Er verwendet den **/Monat** -Parameter, um den letzten Tag anzugeben, und den **/m** -Parameter mit dem Platzhalter Zeichen (*), um anzugeben, dass das Programm monatlich ausgeführt wird.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo lastday /m *
```

#### <a name="to-schedule-a-task-at-600-pm-on-the-last-days-of-february-and-march"></a>So planen Sie eine Aufgabe um 6:00 Uhr in den letzten Tagen von Februar und März

Mit dem folgenden Befehl wird das Programm "MyApp" für den letzten Tag von Februar und den letzten Tag des März um 6:00 Uhr geplant. Er verwendet den **/Monat** -Parameter, um den letzten Tag anzugeben, den **/m** -Parameter, um die Monate anzugeben, und den **/St** -Parameter, um die Startzeit anzugeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo lastday /m FEB,MAR /st 18:00
```

### <a name="BKMK_once"></a>So planen Sie einen Task, der einmal ausgeführt wird

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc once /st <HH:MM> [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Der **/sc once** -Parameter ist im Typ "Run-Once Schedule" erforderlich. Der **/St** -Parameter, der die Zeit angibt, zu der die Aufgabe ausgeführt wird, ist erforderlich. Der **/SD** -Parameter, der das Datum angibt, an dem die Aufgabe ausgeführt wird, ist optional. Die Parameter **/Monat** (Modifier) und **/Ed** (Enddatum) sind für diesen Zeit Plantyp ungültig.

Mit " **Schtasks** " können Sie die Ausführung einer Aufgabe nicht planen, wenn das angegebene Datum und die Uhrzeit in der Vergangenheit liegen, und zwar basierend auf der Uhrzeit des lokalen Computers. Um einen Task zu planen, der auf einem Remote Computer in einer anderen Zeitzone einmal ausgeführt wird, müssen Sie ihn vor dem Datum und der Uhrzeit auf dem lokalen Computer planen.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-one-time"></a>So planen Sie einen Task, der nur einmal ausgeführt wird

Der folgende Befehl plant, dass das MyApp-Programm am 1. Januar 2003 um Mitternacht ausgeführt wird. Er verwendet den **/SC** -Parameter, um den Zeit Plantyp anzugeben, und **/SD** und **St** , um das Datum und die Uhrzeit anzugeben.

Da der lokale Computer die Option **Englisch (USA)** in den Regions **-und Sprachoptionen** in der **Systemsteuerung**verwendet, ist das Format für das Startdatum mm/dd/yyyy.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc once /sd 01/01/2003 /st 00:00
```

### <a name="BKMK_startup"></a>So planen Sie einen Task, der bei jedem Systemstart ausgeführt wird

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc onstart [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Beim Typ des Start Zeitplans ist der Parameter **/SC OnStart** erforderlich. Der Parameter **/SD** (Startdatum) ist optional, und der Standardwert ist das aktuelle Datum.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-when-the-system-starts"></a>So planen Sie einen Task, der beim Starten des Systems ausgeführt wird

Der folgende Befehl plant das MyApp-Programm bei jedem Start des Systems, beginnend ab dem 15. März, 2001:

Da der lokale Computer die Option **Englisch (USA)** in den Regions **-und Sprachoptionen** in der **Systemsteuerung**verwendet, ist das Format für das Startdatum mm/dd/yyyy.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc onstart /sd 03/15/2001
```

### <a name="BKMK_logon"></a>So planen Sie einen Task, der ausgeführt wird, wenn sich ein Benutzer anmeldet

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc onlogon [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Mit dem Zeit Plantyp "on LOGON" wird eine Aufgabe geplant, die immer dann ausgeführt wird, wenn sich ein Benutzer am Computer anmeldet. Im Zeit Plantyp "bei der Anmeldung" ist der Parameter " **/SC pro** " erforderlich. Der Parameter **/SD** (Startdatum) ist optional, und der Standardwert ist das aktuelle Datum.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-when-a-user-logs-on-to-a-remote-computer"></a>So planen Sie einen Task, der ausgeführt wird, wenn sich ein Benutzer an einem Remote Computer anmeldet

Der folgende Befehl plant die Ausführung einer Batchdatei, wenn sich ein Benutzer (Benutzer) am Remote Computer anmeldet. Er verwendet den **/s** -Parameter, um den Remote Computer anzugeben. Da der Befehl Remote ist, beziehen sich alle Pfade im Befehl, einschließlich des Pfads zur Batchdatei, auf einen Pfad auf dem Remote Computer.
```
schtasks /create /tn "Start Web Site" /tr c:\myiis\webstart.bat /sc onlogon /s Server23
```

### <a name="BKMK_idle"></a>So planen Sie einen Task, der ausgeführt wird, wenn das System im Leerlauf ist

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc onidle /i {1 - 999} [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Der Zeit Plantyp "im Leerlauf" plant eine Aufgabe, die ausgeführt wird, wenn keine Benutzeraktivität innerhalb der durch den **/i** -Parameter angegebenen Zeit vorhanden ist. Im "on Idle"-Zeit Plantyp sind der **/sc onidle** -Parameter und der **/i** -Parameter erforderlich. **/SD** (Startdatum) ist optional, und der Standardwert ist das aktuelle Datum.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-whenever-the-computer-is-idle"></a>So planen Sie einen Task, der ausgeführt wird, wenn der Computer im Leerlauf ist

Der folgende Befehl plant die Ausführung des MyApp-Programms, wenn sich der Computer im Leerlauf befindet. Er verwendet den erforderlichen **/i** -Parameter, um anzugeben, dass der Computer vor dem Start der Aufgabe 10 Minuten lang im Leerlauf bleiben muss.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc onidle /i 10
```

### <a name="BKMK_now"></a>So planen Sie einen Task, der jetzt ausgeführt wird

**Schtasks** haben keine "jetzt ausführen"-Option, Sie können diese Option aber simulieren, indem Sie eine Aufgabe erstellen, die ein Mal ausgeführt wird und innerhalb weniger Minuten gestartet wird.

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc once [/st <HH:MM>] /sd <MM/DD/YYYY> [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-a-few-minutes-from-now"></a>So planen Sie einen Task, der in wenigen Minuten ausgeführt wird

Der folgende Befehl plant, dass eine Aufgabe einmal am 13. November 2002 um 2:18 Uhr ausgeführt wird. lokale Zeit.

Da der lokale Computer die Option **Englisch (USA)** in den Regions **-und Sprachoptionen** in der **Systemsteuerung**verwendet, ist das Format für das Startdatum mm/dd/yyyy.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc once /st 14:18 /sd 11/13/2002
```

### <a name="BKMK_diff_perms"></a>So planen Sie einen Task, der mit unterschiedlichen Berechtigungen ausgeführt wird

Sie können die Ausführung von Aufgaben aller Typen mit Berechtigungen eines alternativen Kontos auf dem lokalen Computer und auf einem Remote Computer planen. Zusätzlich zu den Parametern, die für den jeweiligen Zeit Plantyp erforderlich sind, ist der **/ru** -Parameter erforderlich, und der **/RP aus** -Parameter ist optional.

#### <a name="examples"></a>Beispiele

#### <a name="to-run-a-task-with-administrator-permissions-on-the-local-computer"></a>So führen Sie eine Aufgabe mit Administrator Berechtigungen auf dem lokalen Computer aus

Der folgende Befehl plant, dass das MyApp-Programm auf dem lokalen Computer ausgeführt wird. Er verwendet **/ru** , um anzugeben, dass der Task mit den Berechtigungen des Administrator Kontos des Benutzers (Admin06) ausgeführt werden soll. In diesem Beispiel ist die Ausführung der Aufgabe jeden Dienstag geplant, aber Sie können einen beliebigen Zeit Plantyp für eine Aufgabe verwenden, die mit alternativen Berechtigungen ausgeführt wird.
```
schtasks /create /tn "My App" /tr myapp.exe /sc weekly /d TUE /ru Admin06
```
Als Antwort fordert " **Schtasks. exe** " das "Ausführen als"-Kennwort für das Admin06-Konto an und zeigt dann eine Erfolgsmeldung an.
```
Please enter the run as password for Admin06: ********
SUCCESS: The scheduled task "My App" has successfully been created.
```

#### <a name="to-run-a-task-with-alternate-permissions-on-a-remote-computer"></a>So führen Sie einen Task mit alternativen Berechtigungen auf einem Remote Computer aus

Der folgende Befehl plant, dass das Programm MyApp alle vier Tage auf dem Computer mit dem Computer ausgeführt wird.

Der Befehl verwendet den **/SC** -Parameter, um einen täglichen Zeitplan anzugeben, und einen **/Monat** -Parameter, um ein Intervall von vier Tagen anzugeben.

Der Befehl verwendet den **/s** -Parameter, um den Namen des Remote Computers anzugeben, und den **/u** -Parameter, um ein Konto anzugeben, das über die Berechtigung zum Planen eines Tasks auf dem Remote Computer verfügt ("Admin01" auf dem Marketing Computer). Außerdem wird der **/ru** -Parameter verwendet, um anzugeben, dass der Task mit den Berechtigungen des nicht-Administrator Kontos des Benutzers (USER01 in der reskits-Domäne) ausgeführt werden soll. Ohne den **/ru** -Parameter wird die Aufgabe mit den Berechtigungen des Kontos ausgeführt, das von **/u**angegeben wird.
```
schtasks /create /tn "My App" /tr myapp.exe /sc daily /mo 4 /s Marketing /u Marketing\Admin01 /ru Reskits\User01
```
**Schtasks** fordert zuerst das Kennwort des Benutzers an, der durch den **/u** -Parameter benannt wird (zum Ausführen des Befehls) und fordert dann das Kennwort des Benutzers an, der durch den **/ru** -Parameter benannt wird (zum Ausführen der Aufgabe). Nach der Authentifizierung der Kenn Wörter zeigt **Schtasks** eine Meldung mit dem Hinweis an, dass die Aufgabe geplant ist.
```
Type the password for Marketing\Admin01:********

Please enter the run as password for Reskits\User01: ********

SUCCESS: The scheduled task "My App" has successfully been created.
```

#### <a name="to-run-a-task-only-when-a-particular-user-is-logged-on"></a>So führen Sie eine Aufgabe nur aus, wenn ein bestimmter Benutzer angemeldet ist

Der folgende Befehl plant, dass das Programm "AdminCheck. exe" jeden Freitag um 4:00 Uhr auf dem öffentlichen Computer ausgeführt wird, aber nur, wenn der Administrator des Computers angemeldet ist.

Der Befehl verwendet den **/SC** -Parameter zum Angeben eines wöchentlichen Zeitplans, des **/d** -Parameters zum Angeben des Tags und des **/St** -Parameters zum Angeben der Startzeit.

Der Befehl verwendet den **/s** -Parameter, um den Namen des Remote Computers anzugeben, und den **/u** -Parameter, um ein Konto anzugeben, das über die Berechtigung zum Planen eines Tasks auf dem Remote Computer verfügt. Außerdem verwendet er den **/ru** -Parameter, um die Aufgabe so zu konfigurieren, dass Sie mit den Berechtigungen des Administrators des öffentlichen Computers (Public\Admin01) und des Parameters **/IT** ausgeführt wird, um anzugeben, dass der Task nur ausgeführt wird, wenn das Konto Public\Admin01 angemeldet ist.
```
schtasks /create /tn "Check Admin" /tr AdminCheck.exe /sc weekly /d FRI /st 04:00 /s Public /u Domain3\Admin06 /ru Public\Admin01 /it
```
**Hinweis**
-   Verwenden Sie eine ausführliche Abfrage **(/Query "aus/v**), um Aufgaben mit der interaktiven ( **/IT**)-Eigenschaft zu identifizieren. In einer ausführlichen Abfrage Anzeige einer Aufgabe mit **/IT**hat das Feld **Anmeldemodus** den Wert **interaktiv**.

### <a name="BKMK_sys_perms"></a>So planen Sie einen Task, der mit System Berechtigungen ausgeführt wird

Tasks aller Typen können mit Berechtigungen des System Kontos auf dem lokalen Computer und auf einem Remote Computer ausgeführt werden. Zusätzlich zu den Parametern, die für den jeweiligen Zeit Plantyp erforderlich sind, ist der Parameter **/ru System** (oder **/ru**) erforderlich, und der **/RP aus** -Parameter ist ungültig.

**Wichtig**
-   Das System Konto verfügt nicht über interaktive Anmelde Rechte. Benutzer können weder Programme noch Aufgaben, die mit System Berechtigungen ausgeführt werden, sehen oder mit ihnen interagieren.
-   Der **/ru** -Parameter bestimmt die Berechtigungen, unter denen der Task ausgeführt wird, und nicht die Berechtigungen, die zum Planen der Aufgabe verwendet werden. Nur Administratoren können Aufgaben planen, unabhängig vom Wert des **/ru** -Parameters.

**Hinweis**

Verwenden Sie eine ausführliche Abfrage ( **/Query "aus** **/v**), um Aufgaben zu identifizieren, die mit System Berechtigungen ausgeführt werden. In einer ausführlichen Abfrage Anzeige einer System Ausführungs Aufgabe hat das Feld **als Benutzer ausführen** den Wert **NT-Autorität \ System** , und das Feld **Anmeldemodus** hat nur den Wert **Background**.

#### <a name="examples"></a>Beispiele

#### <a name="to-run-a-task-with-system-permissions"></a>So führen Sie eine Aufgabe mit System Berechtigungen aus

Mit dem folgenden Befehl wird das Programm MyApp auf dem lokalen Computer mit den Berechtigungen des System Kontos ausgeführt. In diesem Beispiel ist geplant, dass die Aufgabe am fünfzehnten Tag jeden Monats ausgeführt wird. Sie können jedoch einen beliebigen Zeit Plantyp für eine Aufgabe verwenden, die mit System Berechtigungen ausgeführt wird.

Der Befehl verwendet den **/ru-System** Parameter, um den System Sicherheitskontext anzugeben. Da System Tasks kein Kennwort verwenden, wird der **/RP aus** -Parameter ausgelassen.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /d 15 /ru System
```
Als Antwort zeigt " **Schtasks. exe** " eine Informations Meldung und eine Erfolgsmeldung an. Sie werden nicht zur Eingabe eines Kennworts aufgefordert.
```
INFO: The task will be created under user name ("NT AUTHORITY\SYSTEM").
SUCCESS: The Scheduled task "My App" has successfully been created.
```

#### <a name="to-run-a-task-with-system-permissions-on-a-remote-computer"></a>So führen Sie einen Task mit System Berechtigungen auf einem Remote Computer aus

Mit dem folgenden Befehl wird geplant, dass das Programm MyApp jeden Morgen um 4:00 Uhr auf dem Computer Finance01 ausgeführt wird. mit System Berechtigungen.

Der Befehl verwendet den **/TN** -Parameter, um den Task zu benennen, und den **/TR** -Parameter, um die Remote Kopie des Programms "MyApp" anzugeben. Er verwendet den **/SC** -Parameter, um einen täglichen Zeitplan anzugeben, lässt jedoch den **/Monat** -Parameter aus, da 1 (täglich) der Standardwert ist. Er verwendet den **/St** -Parameter, um die Startzeit anzugeben. Dies ist auch der Zeitpunkt, an dem der Task jeden Tag ausgeführt wird.

Der Befehl verwendet den **/s** -Parameter, um den Namen des Remote Computers anzugeben, und den **/u** -Parameter, um ein Konto anzugeben, das über die Berechtigung zum Planen eines Tasks auf dem Remote Computer verfügt. Außerdem verwendet er den **/ru** -Parameter, um anzugeben, dass die Aufgabe unter dem System Konto ausgeführt werden soll. Ohne den **/ru** -Parameter wird die Aufgabe mit den Berechtigungen des Kontos ausgeführt, das von **/u**angegeben wird.
```
schtasks /create /tn "My App" /tr myapp.exe /sc daily /st 04:00 /s Finance01 /u Admin01 /ru System
```
**Schtasks** fordert das Kennwort des Benutzers an, der vom **/u** -Parameter benannt wird, und zeigt nach der Authentifizierung des Kennworts eine Meldung an, die angibt, dass die Aufgabe erstellt wurde und mit Berechtigungen des System Kontos ausgeführt wird.
```
Type the password for Admin01:**********

INFO: The Schedule Task "My App" will be created under user name ("NT AUTHORITY\
SYSTEM").
SUCCESS: The scheduled task "My App" has successfully been created.
```

### <a name="BKMK_multi_progs"></a>So planen Sie einen Task, der mehr als ein Programm ausführt

Jeder Task führt nur ein Programm aus. Sie können jedoch eine Batchdatei erstellen, die mehrere Programme ausführt, und dann eine Aufgabe für die Ausführung der Batchdatei planen. Diese Methode wird im folgenden Verfahren veranschaulicht:
1. Erstellen Sie eine Batchdatei, mit der die Programme gestartet werden, die Sie ausführen möchten.

   In diesem Beispiel erstellen Sie eine Batchdatei, die Ereignisanzeige (eventvwr. exe) und den System Monitor (Perfmon. exe) startet.  
   - Öffnen Sie einen Text-Editor, z. B. Notepad.
   - Geben Sie den Namen und den voll qualifizierten Pfad zur ausführbaren Datei für jedes Programm ein. In diesem Fall enthält die Datei die folgenden Anweisungen.  
     ```
     C:\Windows\System32\Eventvwr.exe 
     C:\Windows\System32\Perfmon.exe
     ```  
   - Speichern Sie die Datei unter dem Namen myApps. bat.
2. Verwenden Sie " **Schtasks. exe** " zum Erstellen einer Aufgabe, die "myApps. bat" ausführt.

   Mit dem folgenden Befehl wird der Monitor Task erstellt, der immer dann ausgeführt wird, wenn sich jemand anmeldet. Er verwendet den **/TN** -Parameter, um den Task zu benennen, und den **/TR** -Parameter, um myApps. bat auszuführen. Er verwendet den **/SC** -Parameter, um den onlogon-Zeit Plantyp und den **/ru** -Parameter anzugeben, um den Task mit den Berechtigungen des Benutzer Administrator Kontos auszuführen.  
   ```
   schtasks /create /tn Monitor /tr C:\MyApps.bat /sc onlogon /ru Reskit\Administrator
   ```  
   Wenn sich ein Benutzer am Computer anmeldet, startet der Task als Ergebnis dieses Befehls sowohl Ereignisanzeige als auch System Monitor.

### <a name="BKMK_remote"></a>So planen Sie einen Task, der auf einem Remote Computer ausgeführt wird

Wenn Sie planen, dass ein Task auf einem Remote Computer ausgeführt werden soll, müssen Sie den Task dem Zeitplan des Remote Computers hinzufügen. Aufgaben aller Typen können auf einem Remote Computer geplant werden, aber die folgenden Bedingungen müssen erfüllt sein.
-   Sie müssen über die Berechtigung zum Planen der Aufgabe verfügen. Daher müssen Sie auf dem lokalen Computer mit einem Konto angemeldet sein, das Mitglied der Gruppe "Administratoren" auf dem Remote Computer ist, oder Sie müssen den **/u** -Parameter verwenden, um die Anmelde Informationen eines Administrators für den Remote Computer anzugeben.
-   Sie können den **/u** -Parameter nur verwenden, wenn sich der lokale Computer und der Remote Computer in derselben Domäne befinden oder der lokale Computer sich in einer Domäne befindet, der die Remote Computer Domäne vertraut. Andernfalls kann der Remote Computer das angegebene Benutzerkonto nicht authentifizieren, und es kann nicht überprüft werden, ob das Konto Mitglied der Gruppe "Administratoren" ist.
-   Der Task muss über ausreichende Berechtigungen verfügen, um auf dem Remote Computer ausgeführt werden zu können. Welche Berechtigungen erforderlich sind, hängt von der Aufgabe ab. Standardmäßig wird der Task mit der-Berechtigung des aktuellen Benutzers des lokalen Computers ausgeführt, oder wenn der **/u** -Parameter verwendet wird, wird der Task mit der Berechtigung des Kontos ausgeführt, das durch den **/u** -Parameter angegeben wird. Allerdings können Sie den **/ru** -Parameter verwenden, um den Task mit Berechtigungen eines anderen Benutzerkontos oder mit System Berechtigungen auszuführen.

#### <a name="examples"></a>Beispiele

#### <a name="an-administrator-schedules-a-task-on-a-remote-computer"></a>Ein Administrator plant einen Task auf einem Remote Computer.

Der folgende Befehl plant, dass das MyApp-Programm alle zehn Tage, beginnend, alle zehn Tage auf dem Remote Computer SRV01 ausgeführt wird. Der Befehl verwendet den **/s** -Parameter, um den Namen des Remote Computers anzugeben. Da der lokale aktuelle Benutzer ein Administrator des Remote Computers ist, ist der **/u** -Parameter, der Alternative Berechtigungen zum Planen der Aufgabe bietet, nicht erforderlich.

Beachten Sie, dass alle Parameter beim Planen von Aufgaben auf einem Remote Computer auf den Remote Computer verweisen. Daher verweist die durch den **/TR** -Parameter angegebene ausführbare Datei auf die Kopie von "MyApp. exe" auf dem Remote Computer.
```
schtasks /create /s SRV01 /tn "My App" /tr "c:\program files\corpapps\myapp.exe" /sc daily /mo 10
```
Als Antwort zeigt **Schtasks** eine Erfolgsmeldung an, die angibt, dass der Task geplant ist.

#### <a name="a-user-schedules-a-command-on-a-remote-computer-case-1"></a>Ein Benutzer plant einen Befehl auf einem Remote Computer (Fall 1).

Der folgende Befehl plant, dass das Programm MyApp alle drei Stunden auf dem Remote Computer SRV06 ausgeführt wird. Da Administrator Berechtigungen erforderlich sind, um eine Aufgabe zu planen, verwendet der Befehl die Parameter **/u** und **/p** , um die Anmelde Informationen des Administrator Kontos des Benutzers ("Admin01" in der reskits-Domäne) bereitzustellen. Diese Berechtigungen werden standardmäßig auch verwendet, um die Aufgabe auszuführen. Da der Task jedoch keine Administrator Berechtigungen zum Ausführen benötigt, enthält der Befehl die Parameter **/u** und **/RP aus** , um die Standardeinstellung zu überschreiben und die Aufgabe mit der Berechtigung des nicht Administrator Kontos des Benutzers auf dem Remote Computer auszuführen.
```
schtasks /create /s SRV06 /tn "My App" /tr "c:\program files\corpapps\myapp.exe" /sc hourly /mo 3 /u reskits\admin01 /p R43253@4$ /ru SRV06\user03 /rp MyFav!!Pswd
```
Als Antwort zeigt **Schtasks** eine Erfolgsmeldung an, die angibt, dass der Task geplant ist.

#### <a name="a-user-schedules-a-command-on-a-remote-computer-case-2"></a>Ein Benutzer plant einen Befehl auf einem Remote Computer (Fall 2).

Der folgende Befehl plant, dass das Programm MyApp auf dem Remote Computer SRV02 am letzten Tag jedes Monats ausgeführt wird. Da der lokale aktuelle Benutzer (user03) kein Administrator des Remote Computers ist, verwendet der Befehl den **/u** -Parameter, um die Anmelde Informationen des Administrator Kontos des Benutzers ("Admin01" in der reskits-Domäne) bereitzustellen. Die Administrator Konto Berechtigungen werden verwendet, um die Aufgabe zu planen und die Aufgabe auszuführen.
```
schtasks /create /s SRV02 /tn "My App" /tr "c:\program files\corpapps\myapp.exe" /sc monthly /mo LASTDAY /m * /u reskits\admin01
```
Da der Befehl den Parameter **/p** (Password) nicht enthielt, fordert **Schtasks** das Kennwort an. Daraufhin wird eine Erfolgsmeldung angezeigt, in diesem Fall eine Warnung.
```
Type the password for reskits\admin01:********

SUCCESS: The scheduled task "My App" has successfully been created.

WARNING: The Scheduled task "My App" has been created, but may not run because
the account information could not be set.
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

-   Um einen **/Create** -Befehl mit den Berechtigungen eines anderen Benutzers auszuführen, verwenden Sie den **/u** -Parameter. Der **/u** -Parameter ist nur für die Planung von Aufgaben auf Remote Computern gültig.
-   Wenn Sie weitere **schtasks/create** Beispiele anzeigen möchten, geben Sie **schtasks/create/?** ein. an einer Eingabeaufforderung.
-   Verwenden Sie den **/ru** -Parameter, um eine Aufgabe zu planen, die mit Berechtigungen eines anderen Benutzers ausgeführt wird. Der **/ru** -Parameter ist für Aufgaben auf lokalen Computern und Remote Computern gültig.
-   Zum Verwenden des **/u** -Parameters muss sich der lokale Computer in derselben Domäne befinden wie der Remote Computer, oder er muss sich in einer Domäne befinden, der die Remote Computer Domäne vertraut. Andernfalls wird entweder der Task nicht erstellt, oder der Aufgaben Auftrag ist leer, und der Task wird nicht ausgeführt.
-   Von **Schtasks** wird immer ein Kennwort angefordert, es sei denn, Sie geben ein Kennwort an, auch wenn Sie eine Aufgabe auf dem lokalen Computer mit dem aktuellen Benutzerkonto planen. Dies ist das normale Verhalten von **Schtasks**.
-   Von **Schtasks** werden keine Programmdatei Speicherorte oder Benutzerkonto Kennwörter überprüft. Wenn Sie nicht den richtigen Datei Speicherort oder das richtige Kennwort für das Benutzerkonto eingeben, wird die Aufgabe erstellt, aber nicht ausgeführt. Wenn sich das Kennwort für ein Konto ändert oder abläuft und Sie das in der Aufgabe gespeicherte Kennwort nicht ändern, wird der Task nicht ausgeführt.
-   Das System Konto verfügt nicht über interaktive Anmelde Rechte. Benutzer können nicht mit Programmen interagieren, die mit System Berechtigungen ausgeführt werden.
-   Jeder Task führt nur ein Programm aus. Sie können jedoch eine Batchdatei erstellen, die mehrere Aufgaben startet, und dann eine Aufgabe planen, die die Batchdatei ausführt.
-   Sie können eine Aufgabe testen, sobald Sie Sie erstellen. Verwenden Sie den **Run** -Vorgang, um die Aufgabe zu testen, und überprüfen Sie dann die Datei "SchedLgU. txt" (*systemroot*\SchedLgU.txt) auf Fehler.

## <a name="BKMK_change"></a>schtasks ändern

Ändert eine oder mehrere der folgenden Eigenschaften einer Aufgabe.
-   Das Programm, das die Aufgabe ausführt ( **/TR**).
-   Das Benutzerkonto, unter dem der Task ausgeführt wird ( **/ru**).
-   Das Kennwort für das Benutzerkonto ( **/RP aus**).
-   Fügt der Aufgabe die interaktive Eigenschaft ( **/IT**) hinzu.

### <a name="syntax"></a>Syntax

```
schtasks /change /tn <TaskName> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]] [/ru {[<Domain>\]<User> | System}] [/rp <Password>] [/tr <TaskRun>] [/st <StartTime>] [/ri <Interval>] [{/et <EndTime> | /du <Duration>} [/k]] [/sd <StartDate>] [/ed <EndDate>] [/{ENABLE | DISABLE}] [/it] [/z]
```

### <a name="parameters"></a>Parameter

|          Begriff           |                                                                                                                                                                                                                                                                                                                                     Definition                                                                                                                                                                                                                                                                                                                                      |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /TN \<Taskname >     |                                                                                                                                                                                                                                                                                                               Gibt die zu ändernde Aufgabe an. Geben Sie den Namen der Aufgabe ein.                                                                                                                                                                                                                                                                                                               |
|     /s \<Computer >      |                                                                                                                                                                                                                                                                               Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                                                                                                                                                                                                               |
|  /u [\<Domänen >\]<User>  |                                                                                                                                                                 Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Der Standardwert sind die Berechtigungen des aktuellen Benutzers auf dem lokalen Computer. Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur zum Ändern einer Aufgabe auf einem Remote Computer ( **/s**) gültig.                                                                                                                                                                  |
|     /p \<Password >      |                                                                                                                                                                                              Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter verwenden, aber den **/p** -Parameter oder das Password-Argument weglassen, werden Sie von **Schtasks** aufgefordert, ein Kennwort einzugeben.</br>Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden.                                                                                                                                                                                               |
| /ru {[\<Domänen >\]<User> |                                                                                                                                                                                                                                                                                                                                       Anlage                                                                                                                                                                                                                                                                                                                                       |
|     /RP aus \<Password >     |                                                                                                                                                                                                                                                 Gibt ein neues Kennwort für das vorhandene Benutzerkonto oder das durch den **/ru** -Parameter angegebene Benutzerkonto an. Dieser Parameter wird ignoriert, wenn er mit dem lokalen System Konto verwendet wird.                                                                                                                                                                                                                                                  |
|     /TR \<taskrun >      |                                                                                                                                                                                  Ändert das Programm, das der Task ausführt. Geben Sie den voll qualifizierten Pfad und den Dateinamen einer ausführbaren Datei, einer Skriptdatei oder einer Batchdatei ein. Wenn Sie den Pfad weglassen, geht **Schtasks** davon aus, dass sich die \<Datei im Verzeichnis "SystemRoot > \System32" befindet. Das angegebene Programm ersetzt das ursprüngliche Programm, das durch den Task ausgeführt wird.                                                                                                                                                                                  |
|    /St \<StartTime->     |                                                                                                                                                                                                                                                              Gibt die Startzeit für den Task an, wobei das 24-Stunden-Zeitformat HH: mm verwendet wird. Beispielsweise entspricht der Wert 14:30 der 12-Stunden-Zeit von 2:30 Uhr.                                                                                                                                                                                                                                                               |
|     /RI \<Intervall >     |                                                                                                                                                                                                                                                                           Gibt das Wiederholungsintervall für die geplante Aufgabe in Minuten an. Der gültige Bereich ist 1-599940 (599940 Minuten = 9999 Stunden).                                                                                                                                                                                                                                                                            |
|     /et \<EndTime->      |                                                                                                                                                                                                                                                               Gibt die Endzeit für die Aufgabe mit dem 24-Stunden-Zeitformat HH: mm an. Beispielsweise entspricht der Wert 14:30 der 12-Stunden-Zeit von 2:30 Uhr.                                                                                                                                                                                                                                                                |
|     /Du \<Dauer >     |                                                                                                                                                                                                                                                                                                     Gibt an, dass die Aufgabe am \<EndTime-> <Duration>oder, falls angegeben, geschlossen werden soll.                                                                                                                                                                                                                                                                                                      |
|           /k            |                                                                                                                                                                   Beendet das Programm, das der Task ausführt, zu dem Zeitpunkt, der durch **/et** oder **/du**angegeben wird. Ohne **/k**startet **Schtasks** das Programm nicht erneut, nachdem es die von **/et** oder **/du**angegebene Zeit erreicht hat, aber das Programm wird nicht beendet, wenn es noch ausgeführt wird. Dieser Parameter ist optional und nur mit einem Minuten-oder stündlichen Zeitplan gültig.                                                                                                                                                                   |
|    /SD \<StartDate >     |                                                                                                                                                                                                                                                                                              Gibt das erste Datum an, an dem die Aufgabe ausgeführt werden soll. Das Datumsformat ist "mm/dd/yyyy".                                                                                                                                                                                                                                                                                               |
|     /Ed \<EndDate >      |                                                                                                                                                                                                                                                                                                 Gibt das letzte Datum an, an dem die Aufgabe ausgeführt werden soll. Das Format ist "mm/dd/yyyy".                                                                                                                                                                                                                                                                                                  |
|         /ENABLE         |                                                                                                                                                                                                                                                                                                                       Gibt an, dass die geplante Aufgabe aktiviert werden soll.                                                                                                                                                                                                                                                                                                                       |
|        /DISABLE         |                                                                                                                                                                                                                                                                                                                      Gibt an, dass die geplante Aufgabe deaktiviert werden soll.                                                                                                                                                                                                                                                                                                                       |
|           /it           | Gibt an, dass die geplante Aufgabe nur ausgeführt werden soll, wenn der Benutzer, unter dem der Task ausgeführt wird, auf dem Computer angemeldet ist.</br>Dieser Parameter hat keine Auswirkung auf Aufgaben, die mit System Berechtigungen oder Tasks ausgeführt werden, für die die interaktive Eigenschaft bereits festgelegt ist. Sie können einen Change-Befehl nicht verwenden, um die interaktive Eigenschaft aus einer Aufgabe zu entfernen.</br>Standardmäßig ist der Benutzer "Ausführen als" der aktuelle Benutzer des lokalen Computers, wenn der Task geplant ist, oder das durch den **/u** -Parameter angegebene Konto (sofern verwendet). Wenn der Befehl jedoch den **/ru** -Parameter enthält, ist der Benutzer "Ausführen als" das Konto, das durch den **/ru** -Parameter angegeben wird. |
|           "/z            |                                                                                                                                                                                                                                                                                                          Gibt an, dass die Aufgabe nach Abschluss des Zeitplans gelöscht wird.                                                                                                                                                                                                                                                                                                          |
|           /?            |                                                                                                                                                                                                                                                                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                                                         |

### <a name="remarks"></a>Hinweise

-   Der Task wird durch die Parameter **/TN** und **/s** identifiziert. Die Parameter **/TR**, **/ru**und **/RP aus** geben die Eigenschaften der Aufgabe an, die Sie ändern können.
-   Die Parameter **/ru**und **/RP aus** geben die Berechtigungen an, unter denen der Task ausgeführt wird. Die Parameter **/u** und **/p** geben die zum Ändern der Aufgabe verwendeten Berechtigungen an.
-   Um Aufgaben auf einem Remote Computer zu ändern, muss der Benutzer auf dem lokalen Computer mit einem Konto angemeldet sein, das Mitglied der Gruppe "Administratoren" auf dem Remote Computer ist.
-   Um einen **/Change** -Befehl mit den Berechtigungen eines anderen Benutzers ( **/u**, **/p**) auszuführen, muss sich der lokale Computer in derselben Domäne befinden wie der Remote Computer, oder er muss sich in einer Domäne befinden, der die Remote Computer Domäne vertraut.
-   Das System Konto verfügt nicht über interaktive Anmelde Rechte. Benutzer können nicht mit Programmen interagieren, die mit System Berechtigungen ausgeführt werden.
-   Verwenden Sie eine ausführliche Abfrage ( **/Query "aus/v**), um Tasks mit der **/IT** -Eigenschaft zu identifizieren. In einer ausführlichen Abfrage Anzeige einer Aufgabe mit **/IT**hat das Feld **Anmeldemodus** den Wert **interaktiv**.

### <a name="examples"></a>Beispiele

### <a name="to-change-the-program-that-a-task-runs"></a>So ändern Sie das Programm, das von einem Task ausgeführt wird

Mit dem folgenden Befehl wird das Programm, das der Virus Check Task ausführt, von "virscheck. exe" in "VirusCheck2. exe" geändert. Dieser Befehl verwendet den **/TN** -Parameter, um die Aufgabe zu identifizieren, und den **/TR** -Parameter, um das neue Programm für die Aufgabe anzugeben. (Sie können den Namen der Aufgabe nicht ändern.)
```
schtasks /change /tn "Virus Check" /tr C:\VirusCheck2.exe
```
In der Antwort zeigt " **Schtasks. exe** " die folgende Erfolgsmeldung an:
```
SUCCESS: The parameters of the scheduled task "Virus Check" have been changed.
```
Als Ergebnis dieses Befehls führt der Virus Check Task jetzt VirusCheck2. exe aus.

### <a name="to-change-the-password-for-a-remote-task"></a>So ändern Sie das Kennwort für eine Remote Aufgabe

Der folgende Befehl ändert das Kennwort des Benutzerkontos für die RemindMe-Aufgabe auf dem Remote Computer Svr01. Der Befehl verwendet den **/TN** -Parameter, um den Task zu identifizieren, und den **/s** -Parameter, um den Remote Computer anzugeben. Er verwendet den **/RP aus** -Parameter, p@ssWord3um das neue Kennwort anzugeben.

Dieses Verfahren ist erforderlich, wenn das Kennwort für ein Benutzerkonto abläuft oder geändert wird. Wenn das in einer Aufgabe gespeicherte Kennwort nicht mehr gültig ist, wird der Task nicht ausgeführt.
```
schtasks /change /tn RemindMe /s Svr01 /rp p@ssWord3
```
In der Antwort zeigt " **Schtasks. exe** " die folgende Erfolgsmeldung an:
```
SUCCESS: The parameters of the scheduled task "RemindMe" have been changed.
```
Aufgrund dieses Befehls wird die RemindMe-Aufgabe nun unter dem ursprünglichen Benutzerkonto ausgeführt, jedoch mit einem neuen Kennwort.

### <a name="to-change-the-program-and-user-account-for-a-task"></a>So ändern Sie das Programm und das Benutzerkonto für eine Aufgabe

Der folgende Befehl ändert das Programm, das von einem Task ausgeführt wird, und ändert das Benutzerkonto, unter dem der Task ausgeführt wird. Im Wesentlichen wird ein Alter Zeitplan für eine neue Aufgabe verwendet. Dieser Befehl ändert die ChkNews-Aufgabe, die "Notepad. exe" jeden Morgen um 9:00 Uhr startet, um stattdessen Internet Explorer zu starten.

Der Befehl verwendet den **/TN** -Parameter, um die Aufgabe zu identifizieren. Er verwendet den **/TR** -Parameter, um das Programm zu ändern, das der Task ausführt, und den **/ru** -Parameter, um das Benutzerkonto zu ändern, unter dem der Task ausgeführt wird.

Der Parameter **/ru**und **/RP aus** , der das Kennwort für das Benutzerkonto bereitstellt, wird ausgelassen. Sie müssen ein Kennwort für das Konto angeben. Sie können jedoch den Parameter **/ru**und **/RP aus** verwenden und das Kennwort als Klartext eingeben. Alternativ können Sie auf " **Schtasks. exe** " warten, um ein Kennwort einzugeben, und das Kennwort dann in den verdeckten Text eingeben.
```
schtasks /change /tn ChkNews /tr "c:\program files\Internet Explorer\iexplore.exe" /ru DomainX\Admin01
```
Als Antwort fordert " **Schtasks. exe** " das Kennwort für das Benutzerkonto an. Dadurch wird der von Ihnen Typisierungs Text verdeckt, sodass das Kennwort nicht angezeigt wird.
```
Please enter the password for DomainX\Admin01: 
```
Beachten Sie, dass der **/TN** -Parameter die Aufgabe identifiziert und dass die Parameter **/TR** und **/ru** die Eigenschaften der Aufgabe ändern. Sie können keinen anderen Parameter verwenden, um den Task zu identifizieren, und Sie können den Aufgaben Namen nicht ändern.

In der Antwort zeigt " **Schtasks. exe** " die folgende Erfolgsmeldung an:
```
SUCCESS: The parameters of the scheduled task "ChkNews" have been changed.
```
Durch diesen Befehl führt die ChkNews-Aufgabe nun Internet Explorer mit den Berechtigungen eines Administrator Kontos aus.

### <a name="to-change-a-program-to-the-system-account"></a>So ändern Sie ein Programm in das System Konto

Mit dem folgenden Befehl wird der securityscript-Task so geändert, dass er mit den Berechtigungen des System Kontos ausgeführt wird. Er verwendet den **/ru-Parameter ""** , um das System Konto anzugeben.
```
schtasks /change /tn SecurityScript /ru ""
```
In der Antwort zeigt " **Schtasks. exe** " die folgende Erfolgsmeldung an:
```
INFO: The run as user name for the scheduled task "SecurityScript" will be changed to "NT AUTHORITY\SYSTEM".
SUCCESS: The parameters of the scheduled task "SecurityScript" have been changed.
```
Da Aufgaben, die mit System Konto Berechtigungen ausgeführt werden, kein Kennwort erfordern, werden Sie von " **Schtasks. exe** " nicht dazu aufgefordert.

### <a name="to-run-a-program-only-when-i-am-logged-on"></a>So führen Sie ein Programm nur aus, wenn ich angemeldet bin

Mit dem folgenden Befehl wird die interaktive Eigenschaft zu MyApp hinzugefügt, eine vorhandene Aufgabe. Diese Eigenschaft stellt sicher, dass der Task nur ausgeführt wird, wenn der Benutzer "Ausführen als", d. h. das Benutzerkonto, unter dem der Task ausgeführt wird, auf dem Computer angemeldet ist.

Der Befehl verwendet den **/TN** -Parameter, um die Aufgabe zu identifizieren, und den **/IT** -Parameter, um der Aufgabe die interaktive Eigenschaft hinzuzufügen. Da der Task bereits mit den Berechtigungen des Benutzerkontos ausgeführt wird, muss der **/ru** -Parameter für die Aufgabe nicht geändert werden.
```
schtasks /change /tn MyApp /it
```
In der Antwort zeigt " **Schtasks. exe** " die folgende Erfolgsmeldung an.
```
SUCCESS: The parameters of the scheduled task "MyApp" have been changed.
```

## <a name="BKMK_run"></a>schtasks ausführen

Startet eine geplante Aufgabe sofort. Der Ausführungs Vorgang ignoriert den Zeitplan, verwendet jedoch den Programmdatei Speicherort, das Benutzerkonto und das Kennwort, die in der Aufgabe gespeichert sind, um den Task sofort auszuführen.

### <a name="syntax"></a>Syntax

```
schtasks /run /tn <TaskName> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>Parameter

|         Begriff          |                                                                                                                                                                 Definition                                                                                                                                                                  |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /TN \<Taskname >    |                                                                                                                                                       Erforderlich. Identifiziert den Task.                                                                                                                                                        |
|    /s \<Computer >     |                                                                                                           Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                                           |
| /u [\<Domänen >\]<User> | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers auf dem lokalen Computer ausgeführt.</br>Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
|    /p \<Password >     |                          Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter verwenden, aber den **/p** -Parameter oder das Password-Argument weglassen, werden Sie von **Schtasks** aufgefordert, ein Kennwort einzugeben.</br>Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden.                           |
|          /?           |                                                                                                                                                    Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                     |

### <a name="remarks"></a>Hinweise

-   Verwenden Sie diesen Vorgang, um Ihre Aufgaben zu testen. Wenn ein Task nicht ausgeführt wird, überprüfen Sie das Taskplaner-Dienst \<Transaktionsprotokoll systemroot > \SchedLgU.txt, um Fehler zu erhalten.
-   Das Ausführen einer Aufgabe wirkt sich nicht auf den Task Zeitplan aus und ändert nicht die nächste Ausführungszeit, die für den Task geplant ist.
-   Um einen Task Remote auszuführen, muss die Aufgabe auf dem Remote Computer geplant werden. Wenn Sie die Aufgabe ausführen, wird Sie nur auf dem Remote Computer ausgeführt. Um sicherzustellen, dass eine Aufgabe auf einem Remote Computer ausgeführt wird, verwenden Sie den Task-Manager oder \<das Taskplaner Transaktionsprotokoll systemroot > \SchedLgU.txt.

### <a name="examples"></a>Beispiele

### <a name="to-run-a-task-on-the-local-computer"></a>So führen Sie einen Task auf dem lokalen Computer aus

Mit dem folgenden Befehl wird die Aufgabe "Sicherheits Skript" gestartet.
```
schtasks /run /tn "Security Script"
```
Als Antwort startet " **Schtasks. exe** " das Skript, das mit der Aufgabe verknüpft ist, und zeigt die folgende Meldung an:
```
SUCCESS: Attempted to run the scheduled task "Security Script".
```
Wie die Meldung impliziert, versucht **Schtasks** , das Programm zu starten, aber es kann nicht sehr sein, dass das Programm tatsächlich gestartet wurde.

### <a name="to-run-a-task-on-a-remote-computer"></a>So führen Sie eine Aufgabe auf einem Remote Computer aus

Der folgende Befehl startet den Aktualisierungs Task auf einem Remote Computer Svr01:
```
schtasks /run /tn Update /s Svr01
```
In diesem Fall zeigt " **Schtasks. exe** " die folgende Fehlermeldung an:
```
ERROR: Unable to run the scheduled task "Update".
```
Um die Ursache des Fehlers zu ermitteln, sehen Sie sich das Transaktionsprotokoll für geplante Aufgaben an, c:\windows\schedlgu.txt auf SVR01. In diesem Fall wird der folgende Eintrag im Protokoll angezeigt:
```
"Update.job" (update.exe) 3/26/2001 1:15:46 PM ** ERROR **
The attempt to log on to the account associated with the task failed, therefore, the task did not run.
The specific error is:
0x8007052e: Logon failure: unknown user name or bad password.
Verify that the task's Run-as name and password are valid and try again.
```
Anscheinend ist der Benutzername oder das Kennwort in der Aufgabe im System ungültig. Der folgende **Schtasks/Change** -Befehl aktualisiert den Benutzernamen und das Kennwort für den Aktualisierungs Task auf SVR01:
```
schtasks /change /tn Update /s Svr01 /ru Administrator /rp PassW@rd3
```
Nachdem der **Änderungs** Befehl abgeschlossen wurde, wird der Befehl " **Run** " wiederholt. Dieses Mal wird das Update. exe-Programm gestartet, und " **Schtasks. exe** " zeigt die folgende Meldung an:
```
SUCCESS: Attempted to run the scheduled task "Update".
```
Wie die Meldung impliziert, versucht **Schtasks** , das Programm zu starten, aber es kann nicht sehr sein, dass das Programm tatsächlich gestartet wurde.

## <a name="BKMK_end"></a>schtasks beenden

Beendet ein Programm, das von einer Aufgabe gestartet wurde.

### <a name="syntax"></a>Syntax

```
schtasks /end /tn <TaskName> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>Parameter

|         Begriff          |                                                                                                                                                               Definition                                                                                                                                                                |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /TN \<Taskname >    |                                                                                                                                         Erforderlich. Identifiziert den Task, der das Programm gestartet hat.                                                                                                                                         |
|    /s \<Computer >     |                                                                                                                        Gibt den Namen oder die IP-Adresse eines Remote Computers an. Der Standardwert ist der lokale Computer.                                                                                                                        |
| /u [\<Domänen >\]<User> | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers auf dem lokalen Computer ausgeführt. Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
|    /p \<Password >     |                        Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter verwenden, aber den **/p** -Parameter oder das Password-Argument weglassen, werden Sie von **Schtasks** aufgefordert, ein Kennwort einzugeben.</br>Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden.                         |
|          /?           |                                                                                                                                                             Zeigt die Hilfe an.                                                                                                                                                              |

### <a name="remarks"></a>Hinweise

" **Schtasks. exe** " beendet nur die Instanzen eines Programms, das von einer geplanten Aufgabe gestartet wurde. Verwenden Sie taskkill, um andere Prozesse zu beenden. Weitere Informationen finden Sie unter [taskkill](taskkill.md).

### <a name="examples"></a>Beispiele

### <a name="to-end-a-task-on-a-local-computer"></a>So beenden Sie eine Aufgabe auf einem lokalen Computer

Der folgende Befehl beendet die Instanz von "Notepad. exe", die von der My Editor-Aufgabe gestartet wurde:
```
schtasks /end /tn "My Notepad"
```
Als Antwort hält " **Schtasks. exe** " die Instanz von "Notepad. exe" an, die vom Task gestartet wurde, und zeigt die folgende Erfolgsmeldung an:
```
SUCCESS: The scheduled task "My Notepad" has been terminated successfully.
```

### <a name="to-end-a-task-on-a-remote-computer"></a>So beenden Sie eine Aufgabe auf einem Remote Computer

Der folgende Befehl beendet die Internet Explorer-Instanz, die von der internetton-Aufgabe auf dem Remote Computer gestartet wurde, SVR01:
```
schtasks /end /tn InternetOn /s Svr01
```
Als Antwort hält " **Schtasks. exe** " die Internet Explorer-Instanz an, die die Aufgabe gestartet hat, und zeigt die folgende Erfolgsmeldung an:
```
SUCCESS: The scheduled task "InternetOn" has been terminated successfully.
```

## <a name="BKMK_delete"></a>schtasks löschen

Löscht einen geplanten Task.

### <a name="syntax"></a>Syntax

```
schtasks /delete /tn {<TaskName> | *} [/f] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>Parameter

|         Begriff          |                                                                                                                                                                 Definition                                                                                                                                                                  |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   /TN {\<Taskname >    |                                                                                                                                                                     \*}                                                                                                                                                                     |
|          /f           |                                                                                                                                  Unterdrückt die Bestätigungsmeldung. Der Task wird ohne Warnung gelöscht.                                                                                                                                  |
|    /s \<Computer >     |                                                                                                           Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                                           |
| /u [\<Domänen >\]<User> | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers auf dem lokalen Computer ausgeführt.</br>Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
|    /p \<Password >     |                          Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter verwenden, aber den **/p** -Parameter oder das Password-Argument weglassen, werden Sie von **Schtasks** aufgefordert, ein Kennwort einzugeben.</br>Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden.                           |
|          /?           |                                                                                                                                                    Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                     |

### <a name="remarks"></a>Hinweise

- Der **Lösch** Vorgang löscht die Aufgabe aus dem Zeitplan. Das Programm, das vom Task ausgeführt wird, wird nicht gelöscht, oder es wird ein ausgeführten Programm unterbrochen.
- Mit dem Befehl **Delete \\** * werden alle Aufgaben gelöscht, die für den Computer geplant sind, und nicht nur die vom aktuellen Benutzer geplanten Tasks.

### <a name="examples"></a>Beispiele

### <a name="to-delete-a-task-from-the-schedule-of-a-remote-computer"></a>So löschen Sie einen Task aus dem Zeitplan eines Remote Computers

Der folgende Befehl löscht den Task "e-Mail starten" aus dem Zeitplan eines Remote Computers. Er verwendet den **/s** -Parameter, um den Remote Computer zu identifizieren.
```
schtasks /delete /tn "Start Mail" /s Svr16
```
In der Antwort zeigt " **Schtasks. exe** " die folgende Bestätigungsmeldung an. Drücken Sie Y, um die Aufgabe zu löschen<strong>.</strong> Um den Befehl abzubrechen, geben Sie **n**ein:
```
WARNING: Are you sure you want to remove the task "Start Mail" (Y/N )? 
SUCCESS: The scheduled task "Start Mail" was successfully deleted.
```

### <a name="to-delete-all-tasks-scheduled-for-the-local-computer"></a>So löschen Sie alle Aufgaben, die für den lokalen Computer geplant sind

Mit dem folgenden Befehl werden alle Aufgaben aus dem Zeitplan des lokalen Computers gelöscht, einschließlich der von anderen Benutzern geplanten Tasks. Er verwendet den **/TN \\** *-Parameter, um alle Aufgaben auf dem Computer darzustellen, und den **/f** -Parameter, um die Bestätigungsmeldung zu unterdrücken.
```
schtasks /delete /tn * /f
```
In der Antwort zeigt " **Schtasks. exe** " die folgenden Erfolgsmeldungen an, die angeben, dass nur die geplante Aufgabe "securescript" gelöscht wurde.

`SUCCESS: The scheduled task "SecureScript" was successfully deleted.`

## <a name="BKMK_query"></a>schtasks-Abfrage

Zeigt Tasks an, die für die Ausführung auf dem Computer geplant sind.

### <a name="syntax"></a>Syntax

```
schtasks [/query] [/fo {TABLE | LIST | CSV}] [/nh] [/v] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>Parameter

|         Begriff          |                                                                                                                                                                 Definition                                                                                                                                                                  |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /Query "aus        |                                                                                                                        Der Vorgangs Name ist optional. Wenn Sie **Schtasks** ohne Parameter eingeben, wird eine Abfrage ausgeführt.                                                                                                                         |
|      /FO {Table       |                                                                                                                                                                    LIST                                                                                                                                                                     |
|          /nh          |                                                                                                            Lässt Spaltenüberschriften aus der Tabellen Anzeige aus. Dieser Parameter ist mit den **Tabellen** -und **CSV** -Ausgabeformaten gültig.                                                                                                             |
|          /v           |                                                                                                         Fügt der Anzeige erweiterte Eigenschaften der Aufgaben hinzu.</br>Abfragen, die **/v** verwenden, sollten als **Liste** oder **CSV**formatiert sein.                                                                                                          |
|    /s \<Computer >     |                                                                                                           Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                                           |
| /u [\<Domänen >\]<User> | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers auf dem lokalen Computer ausgeführt.</br>Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
|    /p \<Password >     |                                        Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie **/u**verwenden, aber **/p** oder das Password-Argument weglassen, werden Sie von **Schtasks** aufgefordert, ein Kennwort einzugeben.</br>Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden.                                         |
|          /?           |                                                                                                                                                    Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                     |

### <a name="remarks"></a>Hinweise

" **Schtasks. exe** " beendet nur die Instanzen eines Programms, das von einer geplanten Aufgabe gestartet wurde. Verwenden Sie taskkill, um andere Prozesse zu beenden. Weitere Informationen finden Sie unter [taskkill](taskkill.md).

### <a name="examples"></a>Beispiele

### <a name="to-display-the-scheduled-tasks-on-the-local-computer"></a>So zeigen Sie die geplanten Tasks auf dem lokalen Computer an

Mit den folgenden Befehlen werden alle Aufgaben angezeigt, die für den lokalen Computer geplant sind. Diese Befehle führen zu demselben Ergebnis und können austauschbar verwendet werden.
```
schtasks
schtasks /query
```
In der Antwort zeigt " **Schtasks. exe** " die Aufgaben im standardmäßigen einfachen Tabellenformat an, wie in der folgenden Tabelle dargestellt:
```
TaskName Next Run Time Status
========================= ======================== ==============
Microsoft Outlook At logon time
SecureScript 14:42:00 PM , 2/4/2001
```

### <a name="to-display-advanced-properties-of-scheduled-tasks"></a>So zeigen Sie erweiterte Eigenschaften geplanter Aufgaben an

Der folgende Befehl fordert eine detaillierte Anzeige der Aufgaben auf dem lokalen Computer an. Er verwendet den **/v** -Parameter, um eine ausführliche (ausführliche) Anzeige anzufordern, und den **/FO List** -Parameter, um die Anzeige als Liste für das einfache lesen zu formatieren. Mit diesem Befehl können Sie überprüfen, ob eine von Ihnen erstellte Aufgabe das gewünschte Wiederholungsmuster aufweist.

**schtasks/Query "aus/FO Liste/v**

Als Antwort zeigt " **Schtasks. exe** " eine ausführliche Eigenschaften Liste für alle Aufgaben an. Die folgende Anzeige zeigt die Aufgabenliste für eine Aufgabe, die für die Ausführung um 4:00 Uhr geplant ist. am letzten Freitag jedes Monats:
```
HostName: RESKIT01
TaskName: SecureScript
Next Run Time: 4:00:00 AM , 3/30/2001
Status: Not yet run
Logon mode: Interactive/Background
Last Run Time: Never
Last Result: 0
Creator: user01
Schedule: At 4:00 AM on the last Fri of every month, starting 3/24/2001
Task To Run: C:\WINDOWS\system32\notepad.exe
Start In: notepad.exe
Comment: N/A
Scheduled Task State: Enabled
Scheduled Type: Monthly
Modifier: Last FRIDAY
Start Time: 4:00:00 AM
Start Date: 3/24/2001
End Date: N/A
Days: FRIDAY
Months: JAN,FEB,MAR,APR,MAY,JUN,JUL,AUG,SEP,OCT,NOV,DEC
Run As User: RESKIT\user01
Delete Task If Not Rescheduled: Enabled
Stop Task If Runs X Hours and X Mins: 72:0
Repeat: Until Time: Disabled
Repeat: Duration: Disabled
Repeat: Stop If Still Running: Disabled
Idle: Start Time(For IDLE Scheduled Type): Disabled
Idle: Only Start If Idle for X Minutes: Disabled
Idle: If Not Idle Retry For X Minutes: Disabled
Idle: Stop Task If Idle State End: Disabled
Power Mgmt: No Start On Batteries: Disabled
Power Mgmt: Stop On Battery Mode: Disabled
```

### <a name="to-log-tasks-scheduled-for-a-remote-computer"></a>So protokollieren Sie die für einen Remote Computer geplanten Tasks

Mit dem folgenden Befehl wird eine Liste der Aufgaben angefordert, die für einen Remote Computer geplant sind, und die Aufgaben werden einer durch Trennzeichen getrennten Protokolldatei auf dem lokalen Computer hinzugefügt. Sie können dieses Befehls Format verwenden, um Aufgaben zu erfassen und zu verfolgen, die für mehrere Computer geplant sind.

Der Befehl verwendet den **/s** -Parameter zum Identifizieren des Remote Computers Reskit16, den **/FO** -Parameter, um das Format anzugeben, und den **/NH** -Parameter, um die Spaltenüberschriften zu unterdrücken. Das **>>** Anfüge Symbol leitet die Ausgabe an das Task Protokoll p0102. CSV auf dem lokalen Computer Svr01 um. Da der Befehl auf dem Remote Computer ausgeführt wird, muss der Pfad des lokalen Computers voll qualifiziert sein.
```
schtasks /query /s Reskit16 /fo csv /nh >> \\svr01\data\tasklogs\p0102.csv
```
Als Antwort fügt " **Schtasks. exe** " die Aufgaben, die für den Computer "Reskit16" geplant sind, der Datei p0102. CSV auf dem lokalen Computer Svr01 hinzu.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
