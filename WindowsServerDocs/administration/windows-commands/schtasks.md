---
title: schtasks
description: 'Windows-Befehle Thema ***- '
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
ms.openlocfilehash: 7aed2b88823c117a7424a4d90edd86829a53f786
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822881"
---
# <a name="schtasks"></a>schtasks



Befehle und Programme zum Ausführen in regelmäßigen Abständen oder zu einem bestimmten Zeitpunkt geplant. Hinzugefügt und entfernt Aufgaben aus dem Zeitplan, startet und beendet die Aufgaben nach Bedarf, und zeigt ein, und geplante Aufgaben geändert.

Um die Befehlssyntax anzuzeigen, klicken Sie auf die folgenden Befehle aus:
-   [schtasks create](#BKMK_create)
-   [schtasks change](#BKMK_change)
-   [schtasks run](#BKMK_run)
-   [schtasks end](#BKMK_end)
-   [schtasks delete](#BKMK_delete)
-   [schtasks query](#BKMK_query)

## <a name="remarks"></a>Hinweise

-   **SchTasks.exe** führt die gleichen Vorgänge wie **geplante Tasks** in **Systemsteuerung**. Sie können diese Tools verwenden, zusammen und austauschbar.
-   **SCHTASKS** ersetzt **At.exe**, ein Tool, das in früheren Versionen von Windows enthalten. Obwohl **At.exe** befindet sich noch in der Windows Server 2003-Familie, **"SCHTASKS"** ist die empfohlene Befehlszeilen zum Planen von Tasks.
-   Die Parameter in einer **"SCHTASKS"** Befehl in beliebiger Reihenfolge angezeigt werden kann. Eingabe **"SCHTASKS"** ohne Parameter eine Abfrage ausführt.
-   Berechtigungen für **"SCHTASKS"**  
    -   Sie benötigen die Berechtigung zum Ausführen des Befehls. Alle Benutzer kann eine Aufgabe auf dem lokalen Computer planen, und sie anzeigen und ändern Sie die Aufgaben, die sie geplant werden können. Mitglieder der Gruppe "Administratoren" können planen, anzeigen und ändern alle Aufgaben auf dem lokalen Computer.
    -   Zum Planen, anzeigen oder Ändern eines Tasks auf einem Remotecomputer befindet, müssen Sie Mitglied der Gruppe "Administratoren" auf dem Remotecomputer ausgeführt, oder verwenden Sie die **/u** Parameter, um die Anmeldeinformationen eines Administrators des Remotecomputers angeben.
    -   Können Sie die **/u** Parameter in eine **/ create** oder **/change** Vorgang nur, wenn der lokale Computer und Remotecomputer befinden sich in derselben Domäne oder der lokale Computer in einer Domäne ist, der Remotecomputer mit dem Domänenvertrauensstellungen. Klicken Sie andernfalls den Remotecomputer kann nicht das angegebene Benutzerkonto authentifizieren, und kann nicht überprüfen, dass das Konto ein Mitglied der Gruppe "Administratoren" ist.
    -   Der Vorgang muss über die Berechtigung zum Ausführen. Die erforderlichen Berechtigungen variieren je nach der Aufgabe. Aufgaben werden standardmäßig ausgeführt, mit den Berechtigungen des aktuellen Benutzers des lokalen Computers oder mit den Berechtigungen des Benutzers gemäß dem **/u** -Parameters, wenn eine enthalten ist. Verwenden Sie zum Ausführen einer Aufgabe mit den Berechtigungen eines anderen Benutzerkontos oder mit einer Systemberechtigungen, die **/RU** Parameter.
-   Stellen Sie sicher, dass eine geplante Aufgabe ausgeführt wurde, oder um herauszufinden, warum eine geplante Aufgabe nicht ausgeführt haben, finden in das Transaktionsprotokoll der Taskplaner-Dienst *SystemRoot*\SchedLgU.txt. Diese Protokolldatensätze Ausführungsversuche von allen Tools, mit denen den Dienst, einschließlich **geplante Tasks** und **SchTasks.exe**.
-   In seltenen Fällen Dateien beschädigt. Beschädigte Tasks werden nicht ausgeführt. Wenn Sie versuchen, einen Vorgang auf beschädigte Tasks ausführen **SchTasks.exe** wird die folgende Fehlermeldung angezeigt:  
    ```
    ERROR: The data is invalid.
    ```  
    Beschädigte Tasks kann nicht wiederhergestellt werden. Verwenden Sie zum Wiederherstellen der Features von System-aufgabenplanung **SchTasks.exe** oder **geplante Tasks** auf die Aufgaben aus dem System zu löschen und neu zu planen.

## <a name="BKMK_create"></a>"SCHTASKS" erstellen

Plant eine Aufgabe.

**SCHTASKS** verschiedene Parameterkombinationen für jeden Zeitplan verwendet. Die kombinierte Syntax zum Erstellen von Aufgaben finden Sie unter oder der Syntax für eine Aufgabe mit einem bestimmten Zeitplan erstellen, klicken Sie auf eine der folgenden Optionen.
-   [Kombinierte Syntax- und parameterbeschreibungen](#BKMK_syntax)
-   [Eine Aufgabe zu planen, die alle N Minuten ausgeführt wird.](#BKMK_minutes)
-   [Eine Aufgabe zu planen, die alle N Stunden ausgeführt wird.](#BKMK_hours)
-   [Um eine Aufgabe zu planen, die alle N Tage ausgeführt wird](#BKMK_days)
-   [Eine Aufgabe zu planen, die alle N Wochen ausgeführt wird.](#BKMK_weeks)
-   [Eine Aufgabe zu planen, die alle N Monate ausgeführt wird.](#BKMK_months)
-   [Eine Aufgabe zu planen, die an einem bestimmten Tag der Woche ausgeführt wird.](#BKMK_spec_day)
-   [Um eine Aufgabe zu planen, die auf einer bestimmten Woche des Monats ausgeführt wird](#BKMK_spec_week)
-   [Eine Aufgabe zu planen, die an einem bestimmten Datum jeden Monat ausgeführt wird.](#BKMK_spec_date)
-   [Eine Aufgabe zu planen, die am letzten Tag eines Monats ausgeführt wird.](#BKMK_last_day)
-   [Um eine Aufgabe zu planen, die einmal ausgeführt wird](#BKMK_once)
-   [Eine Aufgabe zu planen, die ausgeführt wird, jedes Mal, wenn das System gestartet wird](#BKMK_startup)
-   [Anmeldet, eine Aufgabe zu planen, die Wenn ein Benutzer ausgeführt wird](#BKMK_logon)
-   [Um eine Aufgabe zu planen, die ausgeführt wird, wenn das System im Leerlauf befindet.](#BKMK_idle)
-   [Eine Aufgabe zu planen, die nun ausgeführt wird](#BKMK_now)
-   [Eine Aufgabe zu planen, die mit anderen Berechtigungen ausgeführt wird.](#BKMK_diff_perms)
-   [Um eine Aufgabe zu planen, die mit einer Systemberechtigungen ausgeführt wird](#BKMK_sys_perms)
-   [Eine Aufgabe zu planen, die mehr als ein Programm ausgeführt wird.](#BKMK_multi_progs)
-   [Eine Aufgabe zu planen, die auf einem Remotecomputer ausgeführt wird.](#BKMK_remote)

### <a name="BKMK_syntax"></a>Kombinierte Syntax- und parameterbeschreibungen

#### <a name="syntax"></a>Syntax

```
schtasks /create /sc <ScheduleType> /tn <TaskName> /tr <TaskRun> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]] [/ru {[<Domain>\]<User> | System}] [/rp <Password>] [/mo <Modifier>] [/d <Day>[,<Day>...] | *] [/m <Month>[,<Month>...]] [/i <IdleTime>] [/st <StartTime>] [/ri <Interval>] [{/et <EndTime> | /du <Duration>} [/k]] [/sd <StartDate>] [/ed <EndDate>] [/it] [/z] [/f]
```

#### <a name="parameters"></a>Parameter

##### <a name="sc-scheduletype"></a>/ SC \<ScheduleType >

Gibt den Zeitplan. Gültige Werte sind pro MINUTE stündlich, täglich, wöchentlich, monatlich, einmal "," ONSTART "," ONLOGON "," ONIDLE.

|Zeitplantyp|Beschreibung|
|-------------|-----------|
|MINUTE, STÜNDLICH, TÄGLICH, WÖCHENTLICH, MONATLICH|Gibt die Zeiteinheit für den Zeitplan an.|
|EINMAL|Der Task wird zu einem angegebenen Datum und Uhrzeit einmal ausgeführt.|
|ONSTART|Der Task ausgeführt wird, jedes Mal, wenn das System gestartet wird. Sie können ein Anfangsdatum oder führen Sie den Task das nächste Mal, wenn das System gestartet wird.|
|ONLOGON|Der Task ausgeführt wird, wenn ein Benutzer (jeder Benutzer) anmeldet. Sie können kein Datum angeben, oder führen Sie den Task das nächste Mal, wenn, das der Benutzer anmeldet.|
|ONIDLE|Der Task ausgeführt wird, wenn das System für einen angegebenen Zeitraum im Leerlauf befindet. Sie können kein Datum angeben oder die Aufgabe der nächsten Ausführung, die das System im Leerlauf befindet.|

##### <a name="tn-taskname"></a>TN \<TaskName >

Gibt einen Namen für den Task. Jeder Task auf dem System muss einen eindeutigen Namen haben. Der Name muss den Regeln für Dateinamen entsprechen und 238 Zeichen nicht überschreiten. Verwenden Sie Anführungszeichen, um Namen einzuschließen, die Leerzeichen enthalten.

##### <a name="tr-taskrun"></a>/tr \<TaskRun>

Gibt an, das Programm oder einen Befehl, der die Aufgabe ausgeführt wird. Geben Sie den vollqualifizierten Pfad und Namen der eine ausführbare Datei, einer Skriptdatei oder einer Batchdatei. Der Pfadname darf die 262 Zeichen nicht überschreiten. Wenn Sie den Pfad weglassen **"SCHTASKS"** wird davon ausgegangen, dass die Datei in die *SystemRoot*\System32-Verzeichnis.

##### <a name="s-computer"></a>/ s \<Computer >

Plant eine Aufgabe auf dem angegebenen Remotecomputer. Geben Sie den Namen oder die IP-Adresse von einem Remotecomputer (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer. Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.

##### <a name="u-domainuser"></a>/u [\<Domain>\]<User>

Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos. Der Standardwert ist die Berechtigungen des aktuellen Benutzers des lokalen Computers. Die **/u** und **/p** Parameter gelten nur für die Planung einer Aufgabe auf einem Remotecomputer (**/s**).

Die Berechtigungen des angegebenen Kontos dienen zur Planung der Aufgabe und zum Ausführen des Tasks. Führen Sie die Aufgabe mit den Berechtigungen eines anderen Benutzers mit der **/RU** Parameter.

Das Benutzerkonto muss Mitglied der Gruppe "Administratoren" auf dem Remotecomputer ausgeführt werden. Darüber hinaus wird mit dem lokalen Computer muss in der gleichen Domäne wie der Remotecomputer sein oder muss in einer Domäne, die von der Domäne der Remotecomputer als vertrauenswürdig eingestuft wird.

##### <a name="p-password"></a>/ p \<Kennwort >

Das Kennwort enthält, für das Benutzerkonto, das im angegebenen die **/u** Parameter. Bei Verwendung der **/u** Parameter jedoch weglassen der **/p** Parameter oder die Password-Argument, **"SCHTASKS"** aufgefordert, ein Kennwort ein, und den eingegebene Text verdeckt.

Die **/u** und **/p** Parameter gelten nur für die Planung einer Aufgabe auf einem Remotecomputer (**/s**).

##### <a name="ru-domainuser--system"></a>/ru {[\<Domain>\]<User> | System}

Führt die Aufgabe mit den Berechtigungen des angegebenen Benutzerkontos. In der Standardeinstellung die Aufgabe ausgeführt wird, mit den Berechtigungen des aktuellen Benutzers des lokalen Computers oder mit der Berechtigung des Benutzers gemäß dem **/u** -Parameters, wenn eine enthalten ist. Die **/RU** Parameter ist gültig, beim Planen von Aufgaben auf lokalen Computern oder Remotecomputern.

|Wert|Beschreibung|
|-----|-----------|
|[\<Domain>\]<User>|Gibt ein anderes Benutzerkonto an.|
|System oder ""|Gibt an, das lokale Systemkonto, ein Konto ein, die das Betriebssystem und die Systemdienste.|

##### <a name="rp-password"></a>RD/RP \<Kennwort >

Gibt das Kennwort für das Benutzerkonto, das im angegebenen die **/RU** Parameter. Wenn Sie diesen Parameter weglassen, wenn Sie ein Benutzerkonto angeben **SchTasks.exe** fordert Sie das Kennwort ein, und den eingegebene Text verdeckt.

Verwenden Sie nicht die **RD/RP** -Parameter für Aufgaben mit den Anmeldeinformationen des Systemkontos ausgeführt (**/ru System**). Das Systemkonto verfügt nicht über ein Kennwort und **SchTasks.exe** fordert nicht für eine.

##### <a name="mo-modifier"></a>/ Monat \<Modifizierer >

Gibt an, wie oft der Task in den Zeitplantyp ausgeführt wird. Dieser Parameter ist gültig, aber optional, eine Minute, stündlich, täglich, wöchentlich oder monatlich zu planen. Der Standardwert ist 1.

|Zeitplantyp|Modifiziererwerte|Beschreibung|
|-------------|---------------|-----------|
|MINUTE|1 - 1439|Der Task ausgeführt wird jede \<N > Minuten.|
|PRO STUNDE|1 - 23|Der Task ausgeführt wird jede \<N > Stunden.|
|PRO TAG|1 - 365|Der Task ausgeführt wird jede \<N > Tage.|
|WÖCHENTLICH|1 - 52|Der Task ausgeführt wird jede \<N > Wochen.|
|EINMAL|Keine Modifizierer.|Der Task wird einmal ausgeführt.|
|ONSTART|Keine Modifizierer.|Die Aufgabe, die beim Start ausgeführt wird.|
|ONLOGON|Keine Modifizierer.|Der Task ausgeführt wird, wenn der Benutzer von angegeben die **/u** Parameter anmeldet.|
|ONIDLE|Keine Modifizierer.|Der Task ausgeführt wird, nachdem das System im Leerlauf, für die Anzahl der Minuten, die gemäß befindet der **/i** -Parameter, der für die Verwendung mit ONIDLE erforderlich ist.|
|MONATLICH|1 - 12|Der Task ausgeführt wird jede \<N > Monate.|
|MONATLICH|LETZTERTAG|Der Task wird am letzten Tag des Monats ausgeführt.|
|MONATLICH|ZUNÄCHST ZWEITE, DRITTE, VIERTE, LETZTE|Verwenden Sie mit der **/d**\<Tag >-Parameter zum Ausführen einer Aufgabe auf einer bestimmten Woche und Tag. Z. B. am dritten Mittwoch des Monats.|

##### <a name="d-dayday--"></a>/ d Tageszeit [,...] | *

Gibt an, täglich oder Tage der Woche oder einen Tag (oder Tage) eines Monats. Nur gültig mit einem wöchentlichen oder MONATLICHEN Zeitplan.

|Zeitplantyp|Modifikator|Tag-Werte (/ d)|Beschreibung|
|-------------|--------|---------------|-----------|
|WÖCHENTLICH|1 - 52|MO - [, MO - SO...] | *|Optional. MON ist die Standardeinstellung. Der Platzhalterwert (*) bedeutet, dass täglich.|
|MONATLICH|ZUNÄCHST ZWEITE, DRITTE, VIERTE, LETZTE|MO-|Für einen bestimmten Woche Zeitplan erforderlich.|
|MONATLICH|None oder {1 bis 12}|1 - 31|Optional und nur gültig mit kein Modifizierer (**/Monat**) Parameter (einem bestimmten Datum Zeitplan) oder wenn die **/Monat** ist 1 bis 12 (ein "jedes \<N > Monate" Zeitplan). Der Standardwert ist Tag 1 (der erste Tag des Monats).|

##### <a name="m-monthmonth"></a>/ m Monat [, Monat...]

Gibt einen oder mehrere Monate des Jahres, in dem die geplante Aufgabe ausgeführt werden soll. Gültige Werte sind JAN - Dez und * (monatlich). Die **/m** Parameter ist nur gültig mit einem MONATLICHEN Zeitplan. Es ist erforderlich, wenn die LETZTERTAG verwendet wird. Andernfalls ist er optional, und der Standardwert ist * (monatlich).

##### <a name="i-idletime"></a>/i \<IdleTime>

Gibt an, wie viele Minuten die Computer im Leerlauf befindet, bevor der Task gestartet wird. Ein gültiger Wert ist eine ganze Zahl zwischen 1 und 999. Dieser Parameter ist nur mit einem ONIDLE-Zeitplan gültig, und es ist erforderlich.

##### <a name="st-starttime"></a>/st \<StartTime>

Gibt die Zeit des Tages, der die Aufgabe beginnt in (jedes Mal, Start) \<hh: mm > 24 - Stunden-Format. Der Standardwert ist die aktuelle Uhrzeit auf dem lokalen Computer. Die **/St** Parameter ist gültig sein und die MINUTE, der stündlich, täglich, wöchentlich, monatlich und einmalig plant. Es ist für einen Zeitplan einmal erforderlich.

##### <a name="ri-interval"></a>/ri \<Interval>

Gibt das Wiederholungsintervall in Minuten an. Dies gilt nicht für die Zeitplantypen: MINUTE, stündlich, ONSTART, ONLOGON und ONIDLE. Gültige Bereich liegt zwischen 1 und 599940 Minuten (599940 Minuten = 9999 Stunden). Wenn entweder/et oder angegeben wird, klicken Sie dann die Wiederholungsintervall standardmäßig auf 10 Minuten.

##### <a name="et-endtime"></a>/ et \<"EndTime" >

Gibt die Zeit des Tages, der auf eine Minute oder stündlich Taskplaners endet \<hh: mm > 24 - Stunden-Format. Nach der angegebenen Endzeit **"SCHTASKS"** erst gestartet, die Aufgabe erneut wiederholt die Startzeit. Standardmäßig haben die Zeitpläne keine Beendigungszeit. Dieser Parameter ist optional und nur mit einem Zeitplan MINUTE bzw. stündlich gültig.

Ein Beispiel finden Sie unter:
-   "Um eine Aufgabe zu planen, die alle 100 Minuten ausgeführt wird während der Geschäftszeiten" in der **eine Aufgabe zu planen, die ausgeführt wird jede** \<N > **Minuten** Abschnitt.

##### <a name="du-duration"></a>/du \<Duration>

Gibt eine maximale Länge der Zeit für eine Minute oder stündlichen Zeitplan in \<HHHH > 24 - Stunden-Format. Nach dem die festgelegte Zeit verstreicht **"SCHTASKS"** erst gestartet, die Aufgabe erneut wiederholt die Startzeit. Standardmäßig haben die Zeitpläne keine maximale Dauer. Dieser Parameter ist optional und nur mit einem Zeitplan MINUTE bzw. stündlich gültig.

Ein Beispiel finden Sie unter:
-   "Um eine Aufgabe zu planen, die ausgeführt wird 10 Stunden lang alle 3 Stunden" in der **eine Aufgabe zu planen, die ausgeführt wird jede** \<N > **Stunden** Abschnitt.

##### <a name="k"></a>/k

Beendet das Programm, das die Aufgabe ausgeführt, die zum Zeitpunkt der gemäß wird **/et** oder **/du**. Ohne **/k**, **"SCHTASKS"** beginnt nicht das Programm erneut, nachdem sie die angegebene Zeit erreicht **/et** oder **/du**, aber es wird nicht beendet das Programm, wenn er noch ausgeführt wird. Dieser Parameter ist optional und nur mit einem Zeitplan MINUTE bzw. stündlich gültig.

Ein Beispiel finden Sie unter:
-   "Um eine Aufgabe zu planen, die alle 100 Minuten ausgeführt wird während der Geschäftszeiten" in der **eine Aufgabe zu planen, die ausgeführt wird jede** \<N > **Minuten** Abschnitt.

##### <a name="sd-startdate"></a>/ SD \<"StartDate" >

Gibt das Datum, an dem der Zeitplan für die Aufgabe beginnt. Der Standardwert ist das aktuelle Datum auf dem lokalen Computer. Die **/SD** Parameter gültig ist und optional für alle Typen zu planen.

Das Format für *"StartDate"* variiert mit dem Gebietsschema für den lokalen Computer im ausgewählten **Regions- und Sprachoptionen** in **Systemsteuerung**. Es ist nur ein Format für jedes Gebietsschema ungültig.

Die gültig Datumsformate werden in der folgenden Tabelle aufgeführt. Verwenden Sie das Format für die ausgewählten Format am ähnlichsten **kurzes Datum** in **Regions- und Sprachoptionen** in **Systemsteuerung** auf dem lokalen Computer.

|Wert|Beschreibung|
|-----|-----------|
|\<MM>/<DD>/<YYYY>|Verwenden Sie für Monat-First-Formate, z. B. **Englisch (Vereinigte Staaten)** und **Spanisch (Panama)**.|
|\<DD>/<MM>/<YYYY>|Verwenden Sie für die Tag-First-Formate, z. B. **Bulgarisch** und **Niederländisch (Niederlande)**.|
|\<YYYY>/<MM>/<DD>|Verwenden Sie für Year-First-Formate, z. B. **Schwedisch** und **Französisch (Kanada)**.|

/ ED \<"EndDate" >

Gibt das Datum, an dem der Zeitplan endet. Dieser Parameter ist optional. Es ist nicht gültig, in einem einmal, ONSTART, ONLOGON oder ONIDLE-Zeitplan. Standardmäßig haben die Zeitpläne kein Enddatum.

Das Format für *"EndDate"* variiert mit dem Gebietsschema für den lokalen Computer im ausgewählten **Regions- und Sprachoptionen** in **Systemsteuerung**. Es ist nur ein Format für jedes Gebietsschema ungültig.

Die gültig Datumsformate werden in der folgenden Tabelle aufgeführt. Verwenden Sie das Format für die ausgewählten Format am ähnlichsten **kurzes Datum** in **Regions- und Sprachoptionen** in **Systemsteuerung** auf dem lokalen Computer.

|Wert|Beschreibung|
|-----|-----------|
|\<MM>/<DD>/<YYYY>|Verwenden Sie für Monat-First-Formate, z. B. **Englisch (Vereinigte Staaten)** und **Spanisch (Panama)**.|
|\<DD>/<MM>/<YYYY>|Verwenden Sie für die Tag-First-Formate, z. B. **Bulgarisch** und **Niederländisch (Niederlande)**.|
|\<YYYY>/<MM>/<DD>|Verwenden Sie für Year-First-Formate, z. B. **Schwedisch** und **Französisch (Kanada)**.|

##### <a name="it"></a>/it

Gibt an, dass der Task ausgeführt werden nur dann, wenn der Benutzer "Ausführen als" (das Benutzerkonto, unter dem der Task ausgeführt wird) auf dem Computer angemeldet ist. Dieser Parameter hat keine Auswirkungen auf die Aufgaben, die mit einer Systemberechtigungen ausgeführt.

Standardmäßig ist der "Ausführen als" Benutzer vom aktuellen Benutzer des lokalen Computers, wenn der Task geplant ist oder das Konto, das gemäß der **/u** -Parameters, sofern einer verwendet wird. Allerdings, wenn der Befehl umfasst die **/RU** Parameter, klicken Sie dann die "Ausführen als" Benutzer ist das Konto, das gemäß der **/RU** Parameter.

Beispiele finden Sie unter:
-   "So planen Sie einen Task, der alle 70 Tage ausgeführt wird, wenn angemeldet bin" in der **eine Aufgabe zu planen, die ausgeführt wird jede** *N* **Tage** Abschnitt.
-   "Zum Ausführen einer Aufgabe nur, wenn ein bestimmter Benutzer angemeldet ist" in der **eine Aufgabe zu planen, die mit anderen Berechtigungen ausgeführt wird** Abschnitt.

##### <a name="z"></a>/z

Gibt an, um den Vorgang bei Abschluss einen Zeitplan zu löschen.

##### <a name="f"></a>/f

Gibt an, um die Aufgabe zu erstellen und Warnungen zu unterdrücken, wenn die angegebene Aufgabe ist bereits vorhanden.

##### <a name=""></a>/?

Zeigt die Hilfe an der Eingabeaufforderung an.

### <a name="BKMK_minutes"></a>Eine Aufgabe zu planen, die alle N Minuten ausgeführt wird.

#### <a name="minute-schedule-syntax"></a>Minutenplans-Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc minute [/mo {1 - 1439}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [{/et <HH:MM> | /du <HHHH:MM>} [/k]] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

In einer Minute Zeitplan die **/SC-Minute** -Parameter ist erforderlich. Die **/Monat** (Modifizierer)-Parameter ist optional und gibt die Anzahl der Minuten zwischen jeder Ausführung des Tasks. Der Standardwert für **/Monat** ist 1 (minütlich). Die **/et** (Endzeit) und **/du** (Dauer)-Parameter sind optional und kann verwendet werden, mit oder ohne die **/k** (Endaufgabe)-Parameter.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-20-minutes"></a>Eine Aufgabe zu planen, die alle 20 Minuten ausgeführt wird.

Der folgende Befehl plant ein Sicherheitsskript Sec.vbs, alle 20 Minuten ausgeführt. Der Befehl verwendet den **/SC** Parameter zum Festlegen eines minutenplans und **/Monat** -Parameter ein Intervall von 20 Minuten fest.

Da der Befehl kein Anfangsdatum oder eine Uhrzeit enthalten ist, startet den Task 20 Minuten nach dem der Befehl abgeschlossen ist, und wird alle 20 Minuten, danach, wenn das System ausgeführt wird. Beachten Sie, dass die Sicherheit Skript-Quelldatei auf einem Remotecomputer befindet, aber, dass der Task ist geplant und auf dem lokalen Computer ausgeführt wird.
```
schtasks /create /sc minute /mo 20 /tn "Security Script" /tr \\central\data\scripts\sec.vbs
```

#### <a name="to-schedule-a-task-that-runs-every-100-minutes-during-non-business-hours"></a>Eine Aufgabe zu planen, die alle 100 Minuten während der Geschäftszeiten ausgeführt wird.

Der folgende Befehl plant ein Sicherheitsskript Sec.vbs, auf dem lokalen Computer alle 100 Minuten zwischen 17:00 Uhr ausgeführt und 7:59 Uhr ausgeführt. jeden Tag. Der Befehl verwendet den **/SC** Parameter zum Festlegen eines minutenplans und **/Monat** Parameter, um ein Intervall von 100 Minuten angeben. Er verwendet den **/St** und **/et** Parameter, um die Start- und Endzeit der einzelnen Zeitplan anzugeben. Darüber hinaus verwendet er die **/k** Parameter, um das Skript zu beenden, wenn er immer noch um 7:59 Uhr ausgeführt wird Ohne **/k**, **"SCHTASKS"** würde das Skript nach 7:59 Uhr, jedoch, wenn die Instanz um 6:20 Uhr gestartet nicht gestartet wurde noch ausgeführt wird, würde nicht beendet werden.
```
schtasks /create /tn "Security Script" /tr sec.vbs /sc minute /mo 100 /st 17:00 /et 08:00 /k
```

### <a name="BKMK_hours"></a>Eine Aufgabe zu planen, die alle N Stunden ausgeführt wird.

#### <a name="hourly-schedule-syntax"></a>Stündlicher Zeitplan-Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc hourly [/mo {1 - 23}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [{/et <HH:MM> | /du <HHHH:MM>} [/k]] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

In einem stundenweise ausgeführten Zeitplan der **/SC stündlich** -Parameter ist erforderlich. Die **/Monat** (Modifizierer)-Parameter ist optional und gibt die Anzahl der Stunden zwischen jeder Ausführung des Tasks. Der Standardwert für **/Monat** ist 1 (einmal pro Stunde). Die **/k** (Endaufgabe)-Parameter ist optional und kann verwendet werden, entweder mit **/et** (End zum angegebenen Zeitpunkt) oder **/du** (Ende nach Ablauf des angegebenen Intervalls).

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-five-hours"></a>Eine Aufgabe zu planen, die alle fünf Stunden ausgeführt wird.

Der folgende Befehl plant die Anwendung "MyApp" alle fünf Stunden ab dem ersten Tag des März 2002 ausgeführt. Er verwendet den **/Monat** Parameter, um das Intervall anzugeben und die **/SD** Parameter, um das Startdatum anzugeben. Da der Befehl keine Startzeit angegeben ist, wird die aktuelle Uhrzeit als die Startzeit verwendet.

Da es sich bei der lokale Computer festgelegt ist, verwendet der **Englisch (Simbabwe)** option **Regions- und Sprachoptionen** in **Systemsteuerung**, das Format für das Startdatum ist MM/TT/JJJJ (03/01/2002).
```
schtasks /create /sc hourly /mo 5 /sd 03/01/2002 /tn "My App" /tr c:\apps\myapp.exe
```

#### <a name="to-schedule-a-task-that-runs-every-hour-at-five-minutes-past-the-hour"></a>Um eine Aufgabe zu planen, die auf fünf Minuten nach der vollen Stunde ausgeführt wird

Der folgende Befehl plant die Anwendung "MyApp" zum Ausführen von fünf Minuten nach Mitternacht pro Stunde ab. Da die **/Monat** Parameter ausgelassen wird, der Befehl verwendet den Standardwert für den stündlichen Zeitplan, die stündlich (1) ist. Wenn dieser Befehl nach 0:05 Uhr ausgeführt wird, führt das Programm nicht bis zum nächsten Tag.
```
schtasks /create /sc hourly /st 00:05 /tn "My App" /tr c:\apps\myapp.exe
```

#### <a name="to-schedule-a-task-that-runs-every-3-hours-for-10-hours"></a>Eine Aufgabe zu planen, die alle drei Stunden für 10 Stunden ausgeführt wird.

Der folgende Befehl plant die Anwendung "MyApp" auf 10 Stunden lang alle drei Stunden ausgeführt.

Der Befehl verwendet den **/SC** Parameter, um einem stundenweise ausgeführten Zeitplan anzugeben und die **/Monat** Parameter, um das Intervall von 3 Stunden anzugeben. Er verwendet die **/St** Parameter, um den Zeitplan um Mitternacht und **/du** Parameter zum Beenden der Wiederholungen nach 10 Stunden. Da das Programm ausgeführt, nur wenigen Minuten wird der **/k** -Parameter, der das Programm beendet wird, wenn er noch ausgeführt wird, wenn die Dauer abläuft, ist nicht erforderlich.
```
schtasks /create /tn "My App" /tr myapp.exe /sc hourly /mo 3 /st 00:00 /du 0010:00
```
In diesem Beispiel ist die Aufgabe ausgeführt wird, um 12:00 Uhr, 3:00 Uhr, 6:00 Uhr und 9:00 Uhr Da die Dauer 10 Stunden ist, wird die Aufgabe erneut um 12:00 Uhr nicht ausgeführt Stattdessen wird es wieder um 12:00 Uhr gestartet am nächsten Tag.

### <a name="BKMK_days"></a>Um eine Aufgabe zu planen, die alle N Tage ausgeführt wird

#### <a name="daily-schedule-syntax"></a>Täglicher Zeitplan-Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc daily [/mo {1 - 365}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

In einen täglichen Zeitplan die **/SC täglich** -Parameter ist erforderlich. Die **/Monat** (Modifizierer)-Parameter ist optional und gibt die Anzahl der Tage zwischen jeder Ausführung des Tasks. Der Standardwert für **/Monat** ist 1 (täglich).

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-day"></a>Eine Aufgabe zu planen, die jeden Tag ausgeführt wird.

Im folgenden Beispiel wird geplant, die Anwendung "MyApp" einmal täglich, täglich um 8:00 Uhr ausgeführt. bis zum 31. Dezember 2002. Da es nicht angegeben, wird die **/Monat** das Standardintervall für 1-Parameter wird verwendet, um den Befehl täglich ausführen.

In diesem Beispiel ist da des lokalen Computersystems, um festgelegt ist die **Englisch (Großbritannien)** option **Regions- und Sprachoptionen** in **Systemsteuerung**, das Format für Das Enddatum ist TT/MM/JJJJ (12/31/2002)
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc daily /st 08:00 /ed 31/12/2002
```

#### <a name="to-schedule-a-task-that-runs-every-12-days"></a>Um eine Aufgabe zu planen, die alle 12 Tage ausgeführt wird

Im folgenden Beispiel wird geplant, die Anwendung "MyApp" alle zwölf Tage um 13:00 Uhr ausgeführt. (13:00) ab dem 31. Dezember 2002. Der Befehl verwendet den **/Monat** Parameter, um ein Intervall von zwei (2) Tage angeben und die **/SD** und **/St** Parameter zur Angabe von Datum und Uhrzeit.

In diesem Beispiel ist da das System, um festgelegt ist die **Englisch (Simbabwe)** option **Regions- und Sprachoptionen** in **Systemsteuerung**, das Format für das Enddatum ist MM/TT / YYYY (12/31/2002)
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc daily /mo 12 /sd 12/31/2002 /st 13:00
```

#### <a name="to-schedule-a-task-that-runs-every-70-days-if-i-am-logged-on"></a>Um eine Aufgabe zu planen, die alle 70 Tage ausgeführt wird, wenn Sie angemeldet sind

Der folgende Befehl plant ein Sicherheitsskript Sec.vbs, Ausführung alle 70 Tage. Der Befehl verwendet den **/Monat** Parameter, um ein Intervall von 70 Tagen angeben. Darüber hinaus verwendet er die **/IT** Parameter, um anzugeben, dass die Aufgabe ausgeführt wird, nur, wenn der Benutzer, dessen Konto sich die Aufgabe ausgeführt wird, auf dem Computer angemeldet ist. Da der Task mit den Berechtigungen des mein Benutzerkonto ausgeführt wird, wird die Aufgabe ausgeführt, nur, wenn Sie angemeldet sind.
```
schtasks /create /tn "Security Script" /tr sec.vbs /sc daily /mo 70 /it
```

> [!NOTE]
> Zur Identifizierung von Aufgaben mit der nur interaktiv (**/IT**)-Eigenschaft, verwenden Sie eine ausführliche Abfrage **(/ Abfrage/v**). In der Anzeige einer ausführlichen Abfrage eines Tasks durch **/IT**, **Anmeldemodus** Feld hat den Wert der **nur interaktiv**.

### <a name="BKMK_weeks"></a>Eine Aufgabe zu planen, die alle N Wochen ausgeführt wird.

#### <a name="weekly-schedule-syntax"></a>Wöchentlicher Zeitplan-Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc weekly [/mo {1 - 52}] [/d {<MON - SUN>[,MON - SUN...] | *}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

In einem wöchentlichen Zeitplan die **/SC wöchentlich** -Parameter ist erforderlich. Die **/Monat** (Modifizierer)-Parameter ist optional und gibt die Anzahl der Wochen zwischen jeder Ausführung des Tasks. Der Standardwert für **/Monat** ist 1 (wöchentlich).

Wöchentliche Zeitpläne verfügen auch über ein optionales **/d** Parameter zur Planung der Aufgabe auszuführenden für bestimmte Tage der Woche oder für alle Tage (*). Der Standardwert ist MON (Montag). Die täglich (*)-Option ist gleichwertig mit tägliche Aufgabe zu planen.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-six-weeks"></a>Eine Aufgabe zu planen, die alle sechs Wochen ausgeführt wird.

Der folgende Befehl plant, die Anwendung "MyApp" auf einem Remotecomputer befindet, die alle sechs Wochen ausgeführt wird. Der Befehl verwendet den **/Monat** Parameter, um das Intervall anzugeben. Da der Befehl lässt die **/d** Parameter, die Aufgabe, die am Montag ausgeführt wird.

Dieser Befehl verwendet außerdem die **/s** Parameter, um den Remotecomputer anzugeben und die **/u** Parameter zum Ausführen des Befehls mit den Berechtigungen des Administratorkonto des Benutzers. Da die **/p** Parameter ausgelassen wird, **SchTasks.exe** fordert den Benutzer für das Kennwort des Administratorkontos.

Darüber hinaus, da der Befehl Remote ausgeführt wird, finden Sie alle Pfade im Befehl einschließlich des Pfads zum MyApp.exe, in Pfade auf dem Remotecomputer.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /mo 6 /s Server16 /u Admin01
```

#### <a name="to-schedule-a-task-that-runs-every-other-week-on-friday"></a>Um eine Aufgabe zu planen, die alle zwei Wochen am Freitag ausgeführt wird.

Der folgende Befehl plant eine Aufgabe, jeden zweiten Freitag ausgeführt. Verwendet die **/Monat** Parameter, um das Intervall von zwei Wochen angeben und die **/d** Parameter, um den Tag der Woche anzugeben. Eine Aufgabe zu planen, die ausgeführt wird jeden Freitag, lassen die **/Monat** Parameter oder auf 1 festlegen.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /mo 2 /d FRI
```

### <a name="BKMK_months"></a>Eine Aufgabe zu planen, die alle N Monate ausgeführt wird.

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly [/mo {1 - 12}] [/d {1 - 31}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Bei diesem Zeitplan kann die **/SC monatlich** -Parameter ist erforderlich. Die **/Monat** (Modifizierer)-Parameter, der die Anzahl der Monate zwischen jeder Ausführung des Tasks angibt, ist optional, und der Standardwert ist 1 (monatlich). Dieser Zeitplantyp verfügt auch über einen optionalen **/d** Parameter, um den Task zur Ausführung auf einem bestimmten Datum des Monats planen. Der Standardwert ist 1 (der erste Tag des Monats).

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-on-the-first-day-of-every-month"></a>Eine Aufgabe zu planen, die am ersten Tag des Monats ausgeführt wird.

Der folgende Befehl plant die Anwendung "MyApp" auf den ersten Tag des Monats ausgeführt. Da der Wert 1 die Standardeinstellung für beide ist die **/Monat** (Modifizierer) Parameter und die **/d** Parameter (Tage), werden diese Parameter im Befehl weggelassen.
```
schtasks /create /tn "My App" /tr myapp.exe /sc monthly
```

#### <a name="to-schedule-a-task-that-runs-every-three-months"></a>Eine Aufgabe zu planen, die alle drei Monate ausgeführt wird.

Der folgende Befehl plant die Anwendung "MyApp" auf alle drei Monate ausgeführt. Er verwendet den **/Monat** Parameter, um das Intervall anzugeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo 3
```

#### <a name="to-schedule-a-task-that-runs-at-midnight-on-the-21st-day-of-every-other-month"></a>Eine Aufgabe zu planen, die am 21. Tag jeden zweiten Monat um Mitternacht ausgeführt wird.

Der folgende Befehl plant die MyApp-Anwendung, jeden zweiten Monat am 21. Tag des Monats um Mitternacht ausgeführt. Der Befehl gibt an, dass diese Aufgabe für ein Jahr von 2. Juli 2002 bis zum 30. Juni 2003 ausgeführt werden soll.

Der Befehl verwendet den **/Monat** Parameter, um das monatliche Intervall (alle zwei Monate), die **/d** Parameter, um das Datum anzugeben und die **/St** die Uhrzeit angeben. Darüber hinaus verwendet er die **/SD** und **/ED** Parameter zum Angeben des Anfangs Datum und Datum bzw. zu beenden. Da auf der lokale Computer festgelegt ist die **Englisch (Südafrika)** option **Regions- und Sprachoptionen** in **Systemsteuerung**, die Datumsangaben werden im lokalen Format angegeben. , JJJJ/MM/TT.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo 2 /d 21 /st 00:00 /sd 2002/07/01 /ed 2003/06/30 
```

### <a name="BKMK_spec_day"></a>Eine Aufgabe zu planen, die an einem bestimmten Tag der Woche ausgeführt wird.

#### <a name="weekly-schedule-syntax"></a>Wöchentlicher Zeitplan-Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc weekly [/d {<MON - SUN>[,MON - SUN...] | *}] [/mo {1 - 52}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Der Zeitplan "Tag der Woche" ist eine Variation des den wöchentlichen Zeitplan. In einem wöchentlichen Zeitplan die **/SC wöchentlich** -Parameter ist erforderlich. Die **/Monat** (Modifizierer)-Parameter ist optional und gibt die Anzahl der Wochen zwischen jeder Ausführung des Tasks. Der Standardwert für **/Monat** ist 1 (wöchentlich). Die **/d** -Parameter, der optional ist, plant die Aufgabe, die für bestimmte Tage der Woche oder für alle Tage (*) ausgeführt. Der Standardwert ist MON (Montag). Die jedem Tag-Option (**/d \*** ) ist äquivalent zum Planen einer täglichen Aufgabe.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-every-wednesday"></a>Eine Aufgabe zu planen, die ausgeführt wird jeden Mittwoch

Der folgende Befehl plant, die Anwendung "MyApp" jede Woche am Mittwoch ausgeführt wird. Der Befehl verwendet den **/d** Parameter, um den Tag der Woche anzugeben. Da der Befehl lässt die **/Monat** Parameter, die Aufgabe wird jede Woche ausgeführt.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /d WED
```

#### <a name="to-schedule-a-task-that-runs-every-eight-weeks-on-monday-and-friday"></a>Eine Aufgabe zu planen, die alle acht Wochen am Montag und Freitag ausgeführt wird.

Der folgende Befehl plant eine Aufgabe, am Montag und Freitag achte wöchentlich ausgeführt. Er verwendet den **/d** Parameter, um die Tage anzugeben und die **/Monat** Parameter, um das Intervall für die acht Wochen anzugeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /mo 8 /d MON,FRI
```

### <a name="BKMK_spec_week"></a>Um eine Aufgabe zu planen, die auf einer bestimmten Woche des Monats ausgeführt wird

#### <a name="specific-week-syntax"></a>Syntax von bestimmten Woche

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly /mo {FIRST | SECOND | THIRD | FOURTH | LAST} /d MON - SUN [/m {JAN - DEC[,JAN - DEC...] | *}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Bei diesem Zeitplan kann die **/SC monatlich** -Parameter der **/Monat** (Modifizierer)-Parameter, und die **/d** (Tag) Parameter sind erforderlich. Die **/Monat** (Modifizierer)-Parameter gibt die Woche, die auf dem der Task ausgeführt wird. Die **/d** Parameter gibt den Tag der Woche. (Sie können nur einen Tag der Woche für diesen Zeitplan angeben.) Dieser Zeitplan verfügt auch über einen optionalen **/m** (Monat)-Parameter, Sie können, Zeit, die für bestimmte Monate oder jedes Monats (*). Der Standardwert für die **/m** -Parameter ist monatlich (*).

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-for-the-second-sunday-of-every-month"></a>Eine Aufgabe für den zweiten Sonntag des Monats planen.

Der folgende Befehl plant, die Anwendung "MyApp" auf der zweiten Sonntag des Monats ausgeführt wird. Er verwendet den **/Monat** Parameter, um der zweiten Woche des Monats anzugeben und die **/d** Parameter, um den Tag angeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo SECOND /d SUN
```

#### <a name="to-schedule-a-task-for-the-first-monday-in-march-and-september"></a>Eine Aufgabe für den ersten Montag im März und September planen

Der folgende Befehl plant, die Anwendung "MyApp" auf der ersten Montag im März und September ausgeführt wird. Er verwendet den **/Monat** Parameter, um die erste Woche des Monats anzugeben und die **/d** Parameter, um den Tag angeben. Er verwendet **/m** Parameter, um den Monat, den Monat Argumente durch ein Komma trennen.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo FIRST /d MON /m MAR,SEP
```

### <a name="BKMK_spec_date"></a>Eine Aufgabe zu planen, die an einem bestimmten Datum jeden Monat ausgeführt wird.

#### <a name="specific-date-syntax"></a>Bestimmtes Datum-syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly /d {1 - 31} [/m {JAN - DEC[,JAN - DEC...] | *}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Geben Sie in das Datum Zeitplan die **/SC monatlich** Parameter und die **/d** (Tag) Parameter sind erforderlich. Die **/d** Parameter gibt an, einen Tag des Monats (1-31), kein Tag der Woche. Sie können nur ein Tag im Zeitplan angeben. Die **/Monat** (Modifizierer)-Parameter ist mit diesem Typ "Zeitplan" ungültig.

Die **/m** (Monat)-Parameter ist optional für diesen Zeitplan aus, und der Standardwert ist monatlich (*). **SCHTASKS** ist nicht möglich, die eine Aufgabe für ein Datum zu planen, die nicht in einem Monat gemäß auftritt der **/m** Parameter. Aber wenn weglassen der **/m** -Parameter, und planen, die eine Aufgabe für ein Datum, das nicht in jeden Monats, z. B. den 31. Tag, und klicken Sie dann auf die Aufgabe angezeigt wird, führt nicht in den kürzeren Monaten. Um eine Aufgabe für den letzten Tag des Monats planen, verwenden Sie den letzten Tag Zeitplantyp aus.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-for-the-first-day-of-every-month"></a>Eine Aufgabe für den ersten Tag des Monats planen.

Der folgende Befehl plant die Anwendung "MyApp" auf den ersten Tag des Monats ausgeführt. Da der Default-Modifizierer (kein Modifizierer) wird, der Tag der Standardwert ist 1, und die Standardmonat sind jeden Monat, der Befehl ohne zusätzliche Parameter.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly
```

#### <a name="to-schedule-a-task-for-the-15th-days-of-may-and-june"></a>Planen Sie eine Aufgabe für den 15. Mai und Juni

Der folgende Befehl plant, die Anwendung "MyApp", 15. Mai und Juni 15 um 15:00 Uhr ausgeführt (15:00). Er verwendet den **/m** Parameter, um das Datum anzugeben und die **/m** Parameter, um den Monaten anzugeben. Darüber hinaus verwendet er die **/St** Parameter, um die Startzeit anzugeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /d 15 /m MAY,JUN /st 15:00
```

### <a name="BKMK_last_day"></a>Eine Aufgabe zu planen, die am letzten Tag eines Monats ausgeführt wird.

#### <a name="last-day-syntax"></a>Letzter Tag-syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly /mo LASTDAY /m {JAN - DEC[,JAN - DEC...] | *} [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

In den letzten Tag Zeitplantyp der **/SC monatlich** -Parameter der **/Monat LETZTERTAG** (Modifizierer)-Parameter, und die **/m** (Monat) Parameter sind erforderlich. Die **/d** (Tag)-Parameter ist ungültig.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-for-the-last-day-of-every-month"></a>Eine Aufgabe für den letzten Tag des Monats planen.

Der folgende Befehl plant die Anwendung "MyApp" auf den letzten Tag des Monats ausgeführt. Er verwendet den **/Monat** Parameter, um den letzten Tag anzugeben und die **/m** Parameter mit dem Platzhalterzeichen (*), um anzugeben, dass das Programm jedes Monats ausgeführt wird.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo lastday /m *
```

#### <a name="to-schedule-a-task-at-600-pm-on-the-last-days-of-february-and-march"></a>Eine Aufgabe 6:00 Uhr planen Klicken Sie auf der letzten Tage Februar und März

Der folgende Befehl plant, die Anwendung "MyApp", um 18:00 Uhr für den letzten Tag des Februar und den letzten Tag des Monats März ausgeführt Verwendet die **/Monat** Parameter am vergangenen Tag, an die **/m** Parameter, um den Monaten anzugeben und die **/St** Parameter, um die Startzeit anzugeben.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo lastday /m FEB,MAR /st 18:00
```

### <a name="BKMK_once"></a>Um eine Aufgabe zu planen, die einmal ausgeführt wird

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc once /st <HH:MM> [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Geben Sie in das für die einmalige Ausführung planen der **/SC einmal** -Parameter ist erforderlich. Die **/St** -Parameter, der die Zeit, die der Task ausgeführt wird angegeben, ist erforderlich. Die **/SD** -Parameter, der das Datum, der die Aufgabe ausgeführt wird angibt, ist optional. Die **/Monat** (Modifizierer) und **/ED** (Enddatum)-Parameter sind ungültig für diesen Zeitplan.

**SCHTASKS** lässt Sie planen, eine Aufgabe einmal ausgeführt wird, wenn das Datum und die Uhrzeit angegeben, in der Vergangenheit sind nicht basierend auf der Uhrzeit des lokalen Computers. Um eine Aufgabe zu planen, die auf einem Remotecomputer in einer anderen Zeitzone einmal ausgeführt wird, müssen Sie es vor diesem Datum planen und die Uhrzeit auf dem lokalen Computer.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-one-time"></a>Eine Aufgabe zu planen, die ein Mal ausgeführt wird.

Der folgende Befehl plant, die Anwendung "MyApp", um Mitternacht am 1. Januar 2003 ausgeführt wird. Verwendet die **/SC** Parameter, um den Zeitplantyp anzugeben und die **/SD** und **St** Datum und Uhrzeit angeben.

Da der lokale Computer verwendet den **Englisch (Vereinigte Staaten)** option **Regions- und Sprachoptionen** in **Systemsteuerung**, das Format für das Startdatum ist MM/TT/JJJJ.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc once /sd 01/01/2003 /st 00:00
```

### <a name="BKMK_startup"></a>Eine Aufgabe zu planen, die ausgeführt wird, jedes Mal, wenn das System gestartet wird

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc onstart [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Geben Sie in das auf die ersten Zeitplan die **/SC, Onstart** -Parameter ist erforderlich. Die **/SD** (Startdatum)-Parameter ist optional, und der Standardwert ist das aktuelle Datum.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-when-the-system-starts"></a>Um eine Aufgabe zu planen, die ausgeführt wird, wenn das System gestartet wird

Der folgende Befehl plant die Anwendung "MyApp" jedes Mal, wenn das System gestartet wird, ab dem 15. März 2001, ausgeführt:

Da der lokale Computer verwendet wird. die **Englisch (Vereinigte Staaten)** option **Regions- und Sprachoptionen** in **Systemsteuerung**, das Format für das Startdatum ist MM/TT/JJJJ .
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc onstart /sd 03/15/2001
```

### <a name="BKMK_logon"></a>Anmeldet, eine Aufgabe zu planen, die Wenn ein Benutzer ausgeführt wird

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc onlogon [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Der Zeitplantyp "bei der Anmeldung" plant eine Aufgabe, die ausgeführt wird, wenn alle Benutzer auf dem Computer anmeldet. In den Zeitplantyp "bei der Anmeldung" die **/sc Onlogon** -Parameter ist erforderlich. Die **/SD** (Startdatum)-Parameter ist optional, und der Standardwert ist das aktuelle Datum.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-when-a-user-logs-on-to-a-remote-computer"></a>Um eine Aufgabe zu planen, die Wenn ein Benutzer ausgeführt wird, protokolliert, mit einem Remotecomputer

Der folgende Befehl plant eine Batchdatei jedem (jeder Benutzer) auf den Remotecomputer anmelden eines Benutzers ausgeführt. Er verwendet den **/s** Parameter, um den Remotecomputer anzugeben. Da der Befehl remote ist, finden Sie alle Pfade im Befehl einschließlich des Pfads in die Batchdatei in einen Pfad auf dem Remotecomputer ein.
```
schtasks /create /tn "Start Web Site" /tr c:\myiis\webstart.bat /sc onlogon /s Server23
```

### <a name="BKMK_idle"></a>Um eine Aufgabe zu planen, die ausgeführt wird, wenn das System im Leerlauf befindet.

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc onidle /i {1 - 999} [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>Hinweise

Der Zeitplan "im Leerlauf" plant eine Aufgabe, die ausgeführt wird, wenn es keine Benutzeraktivität während des Zeitraums, der gemäß gibt der **/i** Parameter. Im Zeitplan "im Leerlauf" Typ der **/sc Onidle** Parameter und die **/i** Parameter sind erforderlich. Die **/SD** (Startdatum) ist optional, und der Standardwert ist das aktuelle Datum.

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-whenever-the-computer-is-idle"></a>Um eine Aufgabe zu planen, die ausgeführt wird, wenn der Computer im Leerlauf befindet.

Der folgende Befehl plant die Anwendung "MyApp" ausgeführt, sobald der Computer im Leerlauf befindet. Er verwendet das erforderliche **/i** Parameter, um anzugeben, dass der Computer im Leerlauf muss zehn Minuten, bevor die Aufgabe gestartet wird.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc onidle /i 10
```

### <a name="BKMK_now"></a>Eine Aufgabe zu planen, die nun ausgeführt wird

**SCHTASKS** ist nicht haben eine "run jetzt" option, aber Sie können diese Option simulieren, indem Sie eine Aufgabe, die einmal ausgeführt wird, und startet in wenigen Minuten erstellen.

#### <a name="syntax"></a>Syntax

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc once [/st <HH:MM>] /sd <MM/DD/YYYY> [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="examples"></a>Beispiele

#### <a name="to-schedule-a-task-that-runs-a-few-minutes-from-now"></a>Um eine Aufgabe zu planen ausführt, ein paar Minuten ab jetzt.

Der folgende Befehl plant eine Aufgabe einmal auf dem 13. November 2002 um 14:18 Uhr ausgeführt lokale Zeit.

Da der lokale Computer verwendet wird. die **Englisch (Vereinigte Staaten)** option **Regions- und Sprachoptionen** in **Systemsteuerung**, das Format für das Startdatum ist MM/TT/JJJJ .
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc once /st 14:18 /sd 11/13/2002
```

### <a name="BKMK_diff_perms"></a>Eine Aufgabe zu planen, die mit anderen Berechtigungen ausgeführt wird.

Sie können Tasks aller Typen mit den Berechtigungen eines anderen Kontos auf dem lokalen und einem Remotecomputer ausführen planen. Zusätzlich zu den Parametern, die erforderlich sind, für den bestimmten Zeitplan-Typ der **/RU** -Parameter ist erforderlich und die **RD/RP** Parameter ist optional.

#### <a name="examples"></a>Beispiele

#### <a name="to-run-a-task-with-administrator-permissions-on-the-local-computer"></a>Zum Ausführen einer Aufgabe mit Administratorberechtigungen auf dem lokalen computer

Der folgende Befehl plant, die Anwendung "MyApp" auf dem lokalen Computer ausgeführt wird. Er verwendet den **/RU** um anzugeben, dass die Aufgabe mit den Berechtigungen des Administrator-Konto des Benutzers (Admin06) ausgeführt werden soll. In diesem Beispiel ist die Aufgabe wird geplant, um jeden Dienstag ausgeführt, aber können Sie jeden Zeitplantyp für eine Aufgabe, die mit anderen Berechtigungen ausgeführt werden.
```
schtasks /create /tn "My App" /tr myapp.exe /sc weekly /d TUE /ru Admin06
```
Im Gegenzug **SchTasks.exe** fordert das "Ausführen als" Kennwort für das Konto Admin06, und klicken Sie dann eine Erfolgsmeldung angezeigt.
```
Please enter the run as password for Admin06: ********
SUCCESS: The scheduled task "My App" has successfully been created.
```

#### <a name="to-run-a-task-with-alternate-permissions-on-a-remote-computer"></a>Zum Ausführen einer Aufgabe mit anderen Berechtigungen auf einem Remotecomputer

Der folgende Befehl plant die Anwendung "MyApp" auf die Marketing-Computer alle vier Tage ausgeführt.

Der Befehl verwendet den **/SC** Parameter, um einen täglichen Zeitplan anzugeben und **/Monat** Parameter, um ein Intervall von vier Tagen angeben.

Der Befehl verwendet den **/s** Parameter, um den Namen des Remotecomputers angeben und die **/u** Parameter, um ein Konto mit der Berechtigung zum Planen eines Tasks auf dem Remotecomputer anzugeben ("Admin01", auf die Marketing Computer). Darüber hinaus verwendet er die **/RU** Parameter, um anzugeben, dass die Aufgabe mit den Berechtigungen des nicht-Administrator-Konto des Benutzers ausgeführt werden soll (in der Domäne Reskits "user01"). Ohne die **/RU** Parameter würde die Aufgabe mit den Berechtigungen des Kontos anhand des ausgeführt **/u**.
```
schtasks /create /tn "My App" /tr myapp.exe /sc daily /mo 4 /s Marketing /u Marketing\Admin01 /ru Reskits\User01
```
**"SCHTASKS"** zuerst fordert das Kennwort des Benutzers mit dem Namen, indem die **/u** Parameter (zum Ausführen des Befehls) und fordert anschließend das Kennwort des Benutzers mit dem Namen, indem die **/RU** Parameter (für die Aufgabe ausgeführt wird). Nach der Authentifizierung von Kennwörtern, **"SCHTASKS"** zeigt eine Meldung gibt an, dass der Task geplant wird.
```
Type the password for Marketing\Admin01:********

Please enter the run as password for Reskits\User01: ********

SUCCESS: The scheduled task "My App" has successfully been created.

```

#### <a name="to-run-a-task-only-when-a-particular-user-is-logged-on"></a>Zum Ausführen einer Aufgabe nur, wenn ein bestimmter Benutzer angemeldet ist

Der folgende Befehl plant AdminCheck.exe auszuführenden Programms auf dem öffentlichen Computer jeden Freitag um 4:00 Uhr, jedoch nur, wenn der Administrator des Computers angemeldet ist.

Der Befehl verwendet den **/SC** Parameter, um einen wöchentlichen Zeitplan anzugeben der **/d** Parameter an den Tag und die **/St** Parameter, um die Startzeit anzugeben.

Der Befehl verwendet den **/s** Parameter, um den Namen des Remotecomputers angeben und die **/u** Parameter, um ein Konto mit der Berechtigung zum Planen eines Tasks auf dem Remotecomputer anzugeben. Darüber hinaus verwendet er die **/RU** Parameter so konfigurieren Sie die Aufgabe mit den Berechtigungen des Administrators der öffentlichen Computer (Public\Admin01) ausgeführt und die **/IT** Parameter, um anzugeben, dass der Task nur ausgeführt wird. Wenn das Public\Admin01-Konto angemeldet ist.
```
schtasks /create /tn "Check Admin" /tr AdminCheck.exe /sc weekly /d FRI /st 04:00 /s Public /u Domain3\Admin06 /ru Public\Admin01 /it
```
**Hinweis**
-   Zur Identifizierung von Aufgaben mit der nur interaktiv (**/IT**)-Eigenschaft, verwenden Sie eine ausführliche Abfrage **(/ Abfrage/v**). In der Anzeige einer ausführlichen Abfrage eines Tasks durch **/IT**, **Anmeldemodus** Feld hat den Wert der **nur interaktiv**.

### <a name="BKMK_sys_perms"></a>Um eine Aufgabe zu planen, die mit einer Systemberechtigungen ausgeführt wird

Tasks aller Typen können mit den Berechtigungen des Systemkontos auf dem lokalen und einem Remotecomputer ausführen. Zusätzlich zu den Parametern, die erforderlich sind, für den bestimmten Zeitplan-Typ der **/RU-System** (oder **/ru ""**)-Parameter ist erforderlich, und die **RD/RP** -Parameter ist ungültig.

**Wichtig**
-   Das System-Konto keine Rechte zur interaktiven Anmeldung. Können nicht finden Sie unter oder Benutzern oder Programmen interagieren Aufgaben, die mit Systemberechtigungen ausgeführt werden.
-   Die **/RU** Parameter bestimmt die Berechtigungen, die unter dem der Task ausgeführt wird, nicht die Berechtigungen, die verwendet, um die Aufgabe zu planen. Nur Administratoren beim Planen von Aufgaben, unabhängig vom Wert der können die **/RU** Parameter.

**Hinweis**

Um Aufgaben zu identifizieren, die mit einer Systemberechtigungen ausgeführt, verwenden Sie eine ausführliche Abfrage (**/Abfragen** **/v**). In der Anzeige einer ausführlichen Abfrage eines System ausgeführten Vorgangs der **als Benutzer ausführen** Feld hat den Wert der **NT AUTHORITY\SYSTEM** und **Anmeldemodus** Feld hat den Wert der  **Nur im Hintergrund**.

#### <a name="examples"></a>Beispiele

#### <a name="to-run-a-task-with-system-permissions"></a>Zum Ausführen einer Aufgabe mit einer Systemberechtigungen

Der folgende Befehl plant die Anwendung "MyApp" auf dem lokalen Computer mit den Berechtigungen des Systemkontos ausgeführt. In diesem Beispiel ist die Aufgabe wird zur Ausführung auf den 15. Tag des Monats geplant, aber können Sie jeden Zeitplantyp für eine Aufgabe, die mit Systemberechtigungen ausgeführt werden.

Der Befehl verwendet den **/ru System** Parameter zur Angabe der System-Sicherheitskontexts. Da Systemtasks kein Kennwort, verwenden die **RD/RP** Parameter ausgelassen wird.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /d 15 /ru System
```
Im Gegenzug **SchTasks.exe** eine informative Meldung und eine Erfolgsmeldung angezeigt. Es wird nicht zur Kennworteingabe aufgefordert.
```
INFO: The task will be created under user name ("NT AUTHORITY\SYSTEM").
SUCCESS: The Scheduled task "My App" has successfully been created.

```

#### <a name="to-run-a-task-with-system-permissions-on-a-remote-computer"></a>Zum Ausführen einer Aufgabe mit einer Systemberechtigungen auf einem Remotecomputer

Der folgende Befehl plant, die Anwendung "MyApp" auf dem Computer Finance01 jeden Morgen um 04:00 Uhr ausgeführt. mit einer Systemberechtigungen.

Der Befehl verwendet den **TN** Parameter, um die Namen der Aufgabe und die **/TR** Parameter, um die Remotekopie der die Anwendung "MyApp" anzugeben. Er verwendet den **/SC** Parameter, um einen täglichen Zeitplan anzugeben, lässt jedoch die **/Monat** Parameter da 1 (täglich) die Standardeinstellung ist. Er verwendet den **/St** Parameter, um die Startzeit, die auch die Zeit ist der Task wird täglich ausgeführt.

Der Befehl verwendet den **/s** Parameter, um den Namen des Remotecomputers angeben und die **/u** Parameter, um ein Konto mit der Berechtigung zum Planen eines Tasks auf dem Remotecomputer anzugeben. Darüber hinaus verwendet er die **/RU** Parameter, um anzugeben, dass die Aufgabe unter dem Systemkonto ausgeführt werden soll. Ohne die **/RU** Parameter würde die Aufgabe mit den Berechtigungen des Kontos anhand des ausgeführt **/u**.
```
schtasks /create /tn "My App" /tr myapp.exe /sc daily /st 04:00 /s Finance01 /u Admin01 /ru System
```
**SCHTASKS** fordert das Kennwort des Benutzers mit dem Namen, indem die **/u** Parameter und zeigt Sie nach der Authentifizierung des Kennworts an, die Meldung an, dass die Aufgabe erstellt wird und sie mit den Berechtigungen des Systems ausgeführt werden soll das Konto.
```
Type the password for Admin01:**********

INFO: The Schedule Task "My App" will be created under user name ("NT AUTHORITY\
SYSTEM").
SUCCESS: The scheduled task "My App" has successfully been created.

```

### <a name="BKMK_multi_progs"></a>Eine Aufgabe zu planen, die mehr als ein Programm ausgeführt wird.

Jede Aufgabe wird nur ein Programm ausgeführt. Allerdings können Sie eine Batchdatei, die mehrere Programme ausgeführt wird und dann einen Task zum Ausführen der Batchdatei planen. Das folgende Verfahren veranschaulicht diese Methode:
1.  Erstellen Sie eine Batchdatei, die Programme startet, die Sie ausführen möchten.

    In diesem Beispiel erstellen Sie eine Batchdatei, die Ereignisanzeige (Eventvwr.exe) und zum Systemmonitor (Perfmon.exe) beginnt.  
    -   Öffnen Sie einen Text-Editor, z. B. Notepad.
    -   Geben Sie den Namen und den vollqualifizierten Pfad zur ausführbaren Datei für jedes Programm. In diesem Fall enthält die Datei die folgenden Anweisungen.  
        ```
        C:\Windows\System32\Eventvwr.exe 
        C:\Windows\System32\Perfmon.exe
        ```  
    -   Speichern Sie die Datei als MyApps.bat.
2.  Verwendung **Schtasks.exe** eine Aufgabe zu erstellen, MyApps.bat ausgeführt wird.

    Der folgende Befehl erstellt die Monitor-Aufgabe, bei der ausgeführt wird, wenn jemand sich anmeldet. Er verwendet den **TN** Parameter, um die Namen der Aufgabe und die **/TR** Parameter, um MyApps.bat auszuführen. Er verwendet den **/SC** Parameter, um den Zeitplantyp OnLogon anzugeben und die **/RU** Parameter zum Ausführen des Tasks mit den Berechtigungen des Administratorkonto des Benutzers.  
    ```
    schtasks /create /tn Monitor /tr C:\MyApps.bat /sc onlogon /ru Reskit\Administrator
    ```  
    Startet, als Ergebnis dieses Befehls Wenn ein Benutzer anmeldet, sich bei dem Computer, der Task sowohl Ereignisanzeige und zum Systemmonitor.

### <a name="BKMK_remote"></a>Eine Aufgabe zu planen, die auf einem Remotecomputer ausgeführt wird.

Um eine Aufgabe zur Ausführung auf einem Remotecomputer zu planen, müssen Sie die Aufgabe auf dem Remotecomputer Zeitplan hinzufügen. Tasks aller Typen können auf einem Remotecomputer geplant werden, aber die folgenden Bedingungen erfüllt sein.
-   Sie müssen die Berechtigung für die Aufgabe zu planen. Daher müssen Sie auf dem lokalen Computer mit einem Konto an, das ein Mitglied der Gruppe "Administratoren" auf dem Remotecomputer angemeldet sein, oder Sie müssen die **/u** Parameter, um die Anmeldeinformationen eines Administrators des Remotecomputers angeben .
-   Sie können die **/u** Parameter nur, wenn der lokale Computer und Remotecomputer befinden sich in derselben Domäne oder der lokale Computer ist in einer Domäne, die die remote-Computer-Domäne vertraut. Klicken Sie andernfalls den Remotecomputer kann nicht das angegebene Benutzerkonto authentifizieren, und kann nicht überprüfen, dass das Konto ein Mitglied der Gruppe "Administratoren" ist.
-   Dieser Task muss über ausreichende Berechtigungen zum Ausführen auf dem Remotecomputer aufweisen. Die erforderlichen Berechtigungen variieren je nach der Aufgabe. In der Standardeinstellung die Aufgabe ausgeführt wird, mit der Berechtigung des aktuellen Benutzers des lokalen Computers oder, wenn Sie die **/u** Parameter wird verwendet, die Aufgabe ausgeführt wird, mit der Berechtigung des Kontos anhand der **/u** Parameter. Sie können jedoch die **/RU** Parameter, um die Aufgabe mit den Berechtigungen eines anderen Benutzerkontos oder mit einer Systemberechtigungen auszuführen.

#### <a name="examples"></a>Beispiele

#### <a name="an-administrator-schedules-a-task-on-a-remote-computer"></a>Ein Administrator plant eine Aufgabe auf einem Remotecomputer

Der folgende Befehl plant die Anwendung "MyApp" auf dem SRV01-Remotecomputer alle zehn Tage, die ab sofort ausgeführt. Der Befehl verwendet den **/s** Parameter, um den Namen des Remotecomputers angeben. Da der aktuelle Benutzer der lokale Administrator des Remotecomputers, ist die **/u** -Parameter, der andere Berechtigungen für die Planung der Aufgabe zur Verfügung stellt, ist nicht erforderlich.

Beachten Sie, dass alle Parameter bei der Planung von Aufgaben auf einem Remotecomputer auf den Remotecomputer verweisen. Aus diesem Grund die ausführbare Datei, die gemäß der **/TR** Parameter verweist auf die Kopie des MyApp.exe auf dem Remotecomputer.
```
schtasks /create /s SRV01 /tn "My App" /tr "c:\program files\corpapps\myapp.exe" /sc daily /mo 10
```
Im Gegenzug **"SCHTASKS"** zeigt einen Erfolg an, die, dass der Task geplant wird.

#### <a name="a-user-schedules-a-command-on-a-remote-computer-case-1"></a>Plant die ein Benutzer einen Befehl auf einem Remotecomputer (Fall 1)

Der folgende Befehl plant, die Anwendung "MyApp" auf dem Remotecomputer SRV06 alle drei Stunden ausgeführt wird. Da Administratorberechtigungen erforderlich sind, um eine Aufgabe zu planen, wird der Befehl verwendet den **/u** und **/p** Parameter, um die Anmeldeinformationen des Benutzers, Administrators-Konto ("Admin01" in der Reskits die Domäne). Standardmäßig werden diese Berechtigungen auch verwendet, um den Task auszuführen. Aber da die Aufgabe keine Administratorberechtigungen zum Ausführen benötigt, der Befehl enthält den **/u** und **RD/RP** Parameter den Standardwert zu überschreiben, und führen Sie den Task mit der Berechtigung des Benutzers nicht-Administratorkonto auf dem Remotecomputer.
```
schtasks /create /s SRV06 /tn "My App" /tr "c:\program files\corpapps\myapp.exe" /sc hourly /mo 3 /u reskits\admin01 /p R43253@4$ /ru SRV06\user03 /rp MyFav!!Pswd
```
Im Gegenzug **"SCHTASKS"** zeigt einen Erfolg an, die, dass der Task geplant wird.

#### <a name="a-user-schedules-a-command-on-a-remote-computer-case-2"></a>Plant die ein Benutzer einen Befehl auf einem Remotecomputer (Fall 2)

Der folgende Befehl plant die Anwendung "MyApp" auf dem Remotecomputer SRV02 am letzten Tag des Monats ausgeführt. Da der aktuelle Benutzer des lokale (Benutzer03) kein Administrator des Remotecomputers ist, verwendet der Befehl die **/u** Parameter, um die Anmeldeinformationen des Benutzers, Administrators bereitzustellen-Konto (in der Domäne Reskits "Admin01"). Die Administratorberechtigungen für das Konto werden zur Planung der Aufgabe und zum Ausführen des Tasks verwendet werden.
```
schtasks /create /s SRV02 /tn "My App" /tr "c:\program files\corpapps\myapp.exe" /sc monthly /mo LASTDAY /m * /u reskits\admin01
```
Da der Befehl nicht enthält die **/p** (Kennwort) Parameter **"SCHTASKS"** fordert das Kennwort. Und dann eine Erfolgsmeldung angezeigt und in diesem Fall eine Warnung.
```
Type the password for reskits\admin01:********

SUCCESS: The scheduled task "My App" has successfully been created.

WARNING: The Scheduled task "My App" has been created, but may not run because
the account information could not be set.

```
Diese Warnung gibt an, dass das angegebene Konto nicht in die Remotedomäne authentifizieren konnte die **/u** Parameter. In diesem Fall konnte die Remotedomäne das Benutzerkonto nicht authentifiziert werden, da der lokale Computer nicht Mitglied einer Domäne ist, die die remote-Computer-Domäne vertraut. In diesem Fall der Auftrag für die Aufgabe wird angezeigt, in der Liste der geplanten Tasks, aber der Task ist jedoch leer, und nicht ausführen.

Die folgende Anzeige von einer ausführlichen Abfrage macht es sich um das Problem mit der Aufgabe. In der Anzeige, beachten Sie, dass der Wert des **Nächster Ausführungszeitpunkt** ist **nie** und den Wert der **als Benutzer ausführen** ist **konnten nicht abgerufen werden, aus dem Taskplaner Datenbank**.

War dieser Computer Mitglied derselben Domäne oder einer vertrauenswürdigen Domäne, die Aufgabe wurde würde wurde erfolgreich geplant und wären wie angegeben.
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

-   Zum Ausführen einer **/ create** Befehl mit den Berechtigungen eines anderen Benutzers, verwenden die **/u** Parameter. Die **/u** Parameter ist nur für die Planung von Aufgaben auf Remotecomputern gültig.
-   Um weitere Komponenten anzuzeigen **"SCHTASKS" / create** Beispiele, Typ **"SCHTASKS" / erstellen /?** an einer Eingabeaufforderung.
-   Um eine Aufgabe zu planen, die mit den Berechtigungen eines anderen Benutzers ausgeführt wird, verwenden Sie die **/RU** Parameter. Die **/RU** Parameter für Aufgaben auf lokalen Computern und Remotecomputern gültig ist.
-   Verwenden der **/u** Parameter dem lokalen Computer muss sich in derselben Domäne wie der Remotecomputer oder in einer Domäne, die der Domäne des remote-Computer vertraut sein. Andernfalls entweder der Vorgang wird nicht erstellt werden, oder der Taskauftrag ist leer und die Aufgabe wird nicht ausgeführt.
-   **SCHTASKS** Aufforderung zur Kennworteingabe immer, es sei denn, Sie Konstruktor bereitstellen, auch wenn Sie planen, dass ein Task auf dem lokalen Computer mithilfe des aktuellen Benutzerkontos. Dies ist ein normales Verhalten für **"SCHTASKS"**.
-   **SCHTASKS** überprüft nicht, Dateispeicherorte für die Anwendung oder Kennwörter von Benutzerkonten. Wenn Sie nicht den richtigen Speicherort oder das richtige Kennwort für das Benutzerkonto eingeben, wird die Aufgabe erstellt, aber er wird nicht ausgeführt. Darüber hinaus wird Wenn das Kennwort eines Kontos ändert oder abläuft und Sie das Kennwort gespeichert, in der Aufgabe nicht ändern, klicken Sie dann die Aufgabe nicht ausgeführt.
-   Das System-Konto keine Rechte zur interaktiven Anmeldung. Benutzer werden nicht angezeigt und können nicht mit Programmen, Ausführen mit einer Systemberechtigungen interagieren.
-   Jede Aufgabe wird nur ein Programm ausgeführt. Sie können jedoch eine Batchdatei, die mehrere Aufgaben gestartet und dann Planen einer Aufgabe, die die Batchdatei ausgeführt wird.
-   Eine Aufgabe können Sie testen, sobald Sie ihn erstellen. Verwenden der **ausführen** Vorgang testen die Aufgabe, und klicken Sie dann Überprüfen dieser Datei (*SystemRoot*\SchedLgU.txt) auf Fehler.

## <a name="BKMK_change"></a>Ändern Sie "SCHTASKS"

Ändert eine oder mehrere der folgenden Eigenschaften eines Tasks.
-   Das Programm, das die Aufgabe ausgeführt wird (**/TR**).
-   Das Benutzerkonto, unter dem der Task ausgeführt wird (**/RU**).
-   Das Kennwort für das Benutzerkonto (**RD/RP**).
-   Fügt die Eigenschaft nur interaktiv an die Aufgabe (**/IT**).

### <a name="syntax"></a>Syntax

```
schtasks /change /tn <TaskName> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]] [/ru {[<Domain>\]<User> | System}] [/rp <Password>] [/tr <TaskRun>] [/st <StartTime>] [/ri <Interval>] [{/et <EndTime> | /du <Duration>} [/k]] [/sd <StartDate>] [/ed <EndDate>] [/{ENABLE | DISABLE}] [/it] [/z]
```

### <a name="parameters"></a>Parameter

|Begriff|Definition|
|----|----------|
|TN \<TaskName >|Identifiziert den Task geändert werden. Geben Sie den Vorgang.|
|/ s \<Computer >|Gibt den Namen oder IP-Adresse eines Remotecomputers an (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer.|
|/u [\<Domain>\]<User>|Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos. Der Standardwert ist die Berechtigungen des aktuellen Benutzers des lokalen Computers. Das angegebene Benutzerkonto muss Mitglied der Gruppe "Administratoren" auf dem Remotecomputer ausgeführt werden. Die **/u** und **/p** Parameter gelten nur für eine Aufgabe auf einem Remotecomputer ändern (**/s**).|
|/ p \<Kennwort >|Gibt das Kennwort des Benutzerkontos im der **/u** Parameter. Bei Verwendung der **/u** Parameter jedoch weglassen der **/p** Parameter oder die Password-Argument, **"SCHTASKS"** aufgefordert, ein Kennwort einzugeben.</br>Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.|
|/ru {[\<Domain>\]<User> | System}|Gibt an, um das Benutzerkonto zu ändern, unter dem der Task ausgeführt wird. Für das lokale Systemkonto angeben, die gültige Einträge sind "", "NT-AUTORITÄT\SYSTEM" oder "SYSTEM".</br>Wenn Sie das Benutzerkonto ändern, müssen Sie auch das Kennwort des Benutzers ändern. Wenn ein Befehl hat eine **/RU** Parameter, nicht jedoch ein **RD/RP** Parameter **"SCHTASKS"** aufgefordert, ein neues Kennwort ein.</br>Aufgaben, die mit den Berechtigungen des lokalen Systemkontos ausgeführt nicht erforderlich, und eines Kennworts aufgefordert.|
|RD/RP \<Kennwort >|Gibt ein neues Kennwort für das vorhandene Benutzerkonto oder das Benutzerkonto, das gemäß der **/RU** Parameter. Dieser Parameter wird ignoriert, mit dem lokalen Systemkonto verwendet.|
|/tr \<TaskRun>|Ändert die Anwendung, die der Task ausgeführt wird. Geben Sie den vollqualifizierten Pfad und Namen der eine ausführbare Datei, einer Skriptdatei oder einer Batchdatei aus. Wenn Sie den Pfad weglassen **"SCHTASKS"** wird davon ausgegangen, dass die Datei in die \<Systemroot > \System32-Verzeichnis. Das angegebene Programm ersetzt das ursprüngliche Programm, das vom Task ausgeführt wird.|
|/ St \<"StartTime" >|Gibt die Startzeit für den Task mit dem 24-Stunden-Format: hh: mm an. Beispielsweise ist ein Wert 14:30, die 12-Stunden-Zeit von 2:30 Uhr entspricht.|
|/ri \<Interval>|Gibt das Wiederholungsintervall für die geplante Aufgabe, in Minuten an. Gültige Bereich ist 1-599940 (599940 Minuten = 9999 Stunden).|
|/ et \<"EndTime" >|Gibt die Endzeit für den Task mit dem 24-Stunden-Format: hh: mm an. Beispielsweise ist ein Wert 14:30, die 12-Stunden-Zeit von 2:30 Uhr entspricht.|
|/du \<Duration>|Gibt an, dass die Aufgabe an schließen die \<"EndTime" > oder <Duration>angegeben.|
|/k|Beendet das Programm, das die Aufgabe ausgeführt, die zum Zeitpunkt der gemäß wird **/et** oder **/du**. Ohne **/k**, **"SCHTASKS"** beginnt nicht das Programm erneut, nachdem sie die angegebene Zeit erreicht **/et** oder **/du**, aber es wird nicht beendet das Programm, wenn er noch ausgeführt wird. Dieser Parameter ist optional und nur mit einem Zeitplan MINUTE bzw. stündlich gültig.|
|/ SD \<"StartDate" >|Gibt das erste Datum auf dem die Aufgabe ausgeführt werden soll. Das Datum das Format ist MM/TT/JJJJ.|
|/ ED \<"EndDate" >|Gibt das letzte Datum, an dem die Aufgabe ausgeführt werden soll. Das Format ist MM/TT/JJJJ.|
|/ AKTIVIEREN|Gibt an, um den geplanten Task zu aktivieren.|
|/DISABLE|Gibt an, um die geplante Aufgabe zu deaktivieren.|
|/it|Gibt an, dass die Ausführung des geplanten Tasks nur, wenn der Benutzer "Ausführen als" (das Benutzerkonto, unter dem der Task ausgeführt wird) auf dem Computer angemeldet ist.</br>Dieser Parameter hat keine Auswirkungen auf Vorgänge, die mit einer Systemberechtigungen ausgeführt oder Vorgänge, die bereits die nur interaktiv-Eigenschaft festgelegt haben. Einen Befehl zum Ändern eines können nicht können Sie um die Eigenschaft nur interaktiv aus einer Aufgabe zu entfernen.</br>Standardmäßig ist der "Ausführen als" Benutzer vom aktuellen Benutzer des lokalen Computers, wenn der Task geplant ist oder das Konto, das gemäß der **/u** -Parameters, sofern einer verwendet wird. Allerdings, wenn der Befehl umfasst die **/RU** Parameter, klicken Sie dann die "Ausführen als" Benutzer ist das Konto, das gemäß der **/RU** Parameter.|
|/z|Gibt an, um die Aufgabe nach dem Abschluss der Zeitplan zu löschen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

-   Die **TN** und **/s** Parameter zu identifizieren, die Aufgabe. Die **/TR**, **/RU**, und **RD/RP** Parameter geben die Eigenschaften des Tasks, die Sie ändern können.
-   Die **/RU**, und **RD/RP** Parameter geben Sie die Berechtigungen, die unter dem der Task ausgeführt wird. Die **/u** und **/p** Parameter geben die Berechtigungen verwendet, um die Aufgabe zu ändern.
-   Um Tasks auf einem Remotecomputer zu ändern, muss der Benutzer auf dem lokalen Computer mit einem Konto angemeldet sein, die ein Mitglied der Gruppe "Administratoren" auf dem Remotecomputer ausgeführt wird.
-   Zum Ausführen einer **/change** Befehl mit den Berechtigungen eines anderen Benutzers (**/u**, **/p**), dem lokalen Computer muss sich in derselben Domäne wie der Remotecomputer oder in einer Domäne sein muss dass die Remotecomputer-Domäne vertraut.
-   Das System-Konto keine Rechte zur interaktiven Anmeldung. Benutzer werden nicht angezeigt und können nicht mit Programmen, Ausführen mit einer Systemberechtigungen interagieren.
-   Zum Identifizieren von Aufgaben mit der **/IT** -Eigenschaft, verwenden Sie eine ausführliche Abfrage (**/Abfrage/v**). In der Anzeige einer ausführlichen Abfrage eines Tasks durch **/IT**, **Anmeldemodus** Feld hat den Wert der **nur interaktiv**.

### <a name="examples"></a>Beispiele

### <a name="to-change-the-program-that-a-task-runs"></a>So ändern Sie die Anwendung, die eine Aufgabe ausgeführt wird.

Der folgende Befehl ändert die Anwendung, die der Task zur Überprüfung der Virus VirusCheck.exe zu VirusCheck2.exe ausgeführt wird. Dieser Befehl verwendet den **TN** Parameter, um den Task zu identifizieren und die **/TR** Parameter, um das neue Programm für den Task angeben. (Sie können nicht den Tasknamen an ändern.)
```
schtasks /change /tn "Virus Check" /tr C:\VirusCheck2.exe
```
Im Gegenzug **SchTasks.exe** die folgende Erfolgsmeldung angezeigt:
```
SUCCESS: The parameters of the scheduled task "Virus Check" have been changed.
```
Als Ergebnis dieses Befehls wird der Task zur Überprüfung der Virus VirusCheck2.exe jetzt ausgeführt.

### <a name="to-change-the-password-for-a-remote-task"></a>Zum Ändern des Kennworts für einen Remotetask

Der folgende Befehl ändert das Kennwort des Benutzerkontos für den Task ErinnerMich auf dem Remotecomputer Svr01. Der Befehl verwendet den **TN** Parameter, um den Task zu identifizieren und die **/s** Parameter, um den Remotecomputer anzugeben. Er verwendet den **RD/RP** Parameter, um das neue Kennwort, p@ssWord3.

Dieses Verfahren ist erforderlich, wenn das Kennwort für ein Benutzerkonto abläuft oder ändert. Wenn das Kennwort gespeichert, die in einer Aufgabe nicht mehr gültig ist, wird die Aufgabe nicht ausgeführt.
```
schtasks /change /tn RemindMe /s Svr01 /rp p@ssWord3
```
Im Gegenzug **SchTasks.exe** die folgende Erfolgsmeldung angezeigt:
```
SUCCESS: The parameters of the scheduled task "RemindMe" have been changed.
```
Als Ergebnis dieses Befehls führt ErinnerMich jetzt unter seinem ursprünglichen Benutzerkonto, aber mit einem neuen Kennwort an.

### <a name="to-change-the-program-and-user-account-for-a-task"></a>So ändern Sie das Programm und das Benutzerkonto für einen Vorgang

Der folgende Befehl ändert das Programm, das eine Aufgabe ausgeführt wird und die Änderungen, die das Benutzerkonto, unter dem der Task ausgeführt wird. Im Wesentlichen wird eine neue Aufgabe einen alten Zeitplan verwendet. Dieser Befehl ändert den ChkNews-Task, der Notepad.exe jeden Morgen um 9:00 Uhr startet, um stattdessen Starten von Internet Explorer.

Der Befehl verwendet den **TN** Parameter, um den Task zu identifizieren. Er verwendet den **/TR** Parameter, um das Programm zu ändern, die der Task ausgeführt wird und die **/RU** Parameter, um das Benutzerkonto zu ändern, unter dem der Task ausgeführt wird.

Die **/RU**, und **RD/RP** -Parameter, der das Kennwort für das Benutzerkonto enthält, wird weggelassen. Müssen Sie ein Kennwort für das Konto angeben, aber Sie können die **/RU**, und **RD/RP** Parameter und geben das Kennwort in Klartext, oder warten **SchTasks.exe** , zur Eingabe einer das Kennwort, und geben Sie dann das Kennwort in verschlüsselter Text.
```
schtasks /change /tn ChkNews /tr "c:\program files\Internet Explorer\iexplore.exe" /ru DomainX\Admin01
```
Im Gegenzug **SchTasks.exe** fordert das Kennwort für das Benutzerkonto an. Es verdeckt den Text, den Sie eingeben, den damit das Kennwort nicht sichtbar ist.
```
Please enter the password for DomainX\Admin01: 
```
Beachten Sie, dass die **TN** Parameter identifiziert die Aufgabe, und dass die **/TR** und **/RU** Parameter ändern Sie die Eigenschaften des Tasks. Sie können nicht einem anderen Parameter verwenden, um den Task zu identifizieren und die Tasknamen nicht ändern.

Im Gegenzug **SchTasks.exe** die folgende Erfolgsmeldung angezeigt:
```
SUCCESS: The parameters of the scheduled task "ChkNews" have been changed.
```
Als Ergebnis dieses Befehls wird die Aufgabe ChkNews Internet Explorer jetzt mit den Berechtigungen eines Administratorkontos ausgeführt.

### <a name="to-change-a-program-to-the-system-account"></a>So ändern Sie ein Programm für das Systemkonto

Der folgende Befehl ändert den Sicherheitsskript-Task aus, sodass sie mit den Berechtigungen des Systemkontos ausgeführt wird. Er verwendet den **/ru ""** Parameter, um das Systemkonto anzugeben.
```
schtasks /change /tn SecurityScript /ru ""
```
Im Gegenzug **SchTasks.exe** die folgende Erfolgsmeldung angezeigt:
```
INFO: The run as user name for the scheduled task "SecurityScript" will be changed to "NT AUTHORITY\SYSTEM".
SUCCESS: The parameters of the scheduled task "SecurityScript" have been changed.
```
Da Aufgaben, die mit den Berechtigungen des Systemkontos ausgeführt kein Kennwort erfordern **SchTasks.exe** fordert nicht für eine.

### <a name="to-run-a-program-only-when-i-am-logged-on"></a>Ausführen eines Programms nur, wenn Sie angemeldet sind

Der folgende Befehl fügt die Eigenschaft nur interaktiv zu "MyApp", eine vorhandene Aufgabe. Diese Eigenschaft stellt sicher, dass die Aufgabe ausgeführt wird, nur, wenn der Benutzer "Ausführen als", also das Benutzerkonto, unter dem der Task ausgeführt wird, auf dem Computer angemeldet ist.

Der Befehl verwendet den **TN** Parameter, um den Task zu identifizieren und die **/IT** Parameter, um die Eigenschaft nur interaktiv die Aufgabe hinzugefügt. Da die Aufgabe bereits mit den Berechtigungen des mein Benutzerkonto ausgeführt wird, ich müssen nicht so ändern Sie die **/RU** Parameter für den Task.
```
schtasks /change /tn MyApp /it
```
Im Gegenzug **SchTasks.exe** die folgende Erfolgsmeldung angezeigt.
```
SUCCESS: The parameters of the scheduled task "MyApp" have been changed.
```

## <a name="BKMK_run"></a>schtasks run

Startet einen geplanten Task sofort an. Die **ausführen** Vorgang ignoriert den Zeitplan, aber die Programmdateispeicherort, Benutzerkonto und Kennwort, die in der Aufgabe gespeichert, den Task direkt auszuführen.

### <a name="syntax"></a>Syntax

```
schtasks /run /tn <TaskName> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>Parameter

|Begriff|Definition|
|----|----------|
|TN \<TaskName >|Erforderlich. Identifiziert den Task.|
|/ s \<Computer >|Gibt den Namen oder IP-Adresse eines Remotecomputers an (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer.|
|/u [\<Domain>\]<User>|Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers des lokalen Computers ausgeführt.</br>Das angegebene Benutzerkonto muss Mitglied der Gruppe "Administratoren" auf dem Remotecomputer ausgeführt werden. Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.|
|/ p \<Kennwort >|Gibt das Kennwort des Benutzerkontos im der **/u** Parameter. Bei Verwendung der **/u** Parameter jedoch weglassen der **/p** Parameter oder die Password-Argument, **"SCHTASKS"** aufgefordert, ein Kennwort einzugeben.</br>Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

-   Verwenden Sie diesen Vorgang, um Ihre Aufgaben zu testen. Wenn eine Aufgabe nicht ausgeführt wird, überprüfen Sie das Transaktionsprotokoll der Taskplanerdienst \<Systemroot > \SchedLgU.txt auf Fehler.
-   Ausführen eines Tasks wirkt sich nicht auf den Task-Zeitplan und ändert sich nicht auf der nächsten Ausführungszeit, die für den Task geplant.
-   Um einen Task Remote ausführen möchten, muss die Aufgabe auf dem Remotecomputer geplant werden. Wenn Sie es ausführen, wird die Aufgabe nur auf dem Remotecomputer ausgeführt. Um sicherzustellen, dass eine Aufgabe auf einem Remotecomputer ausgeführt wird, verwenden Sie Task-Manager oder das Transaktionsprotokoll der Aufgabenplanung \<Systemroot > \SchedLgU.txt.

### <a name="examples"></a>Beispiele

### <a name="to-run-a-task-on-the-local-computer"></a>Zum Ausführen einer Aufgabe auf dem lokalen computer

Der folgende Befehl startet die Aufgabe "Sicherheit Script".
```
schtasks /run /tn "Security Script"
```
Im Gegenzug **SchTasks.exe** startet das Skript, das der Aufgabe zugeordnet und wird die folgende Meldung angezeigt:
```
SUCCESS: Attempted to run the scheduled task "Security Script".
```
Wie die Nachricht schon sagt, **"SCHTASKS"** versucht, Sie starten die Anwendung, aber es nicht überprüfen kann, die das Programm tatsächlich gestartet wurde.

### <a name="to-run-a-task-on-a-remote-computer"></a>Zum Ausführen einer Aufgabe auf einem Remotecomputer

Der folgende Befehl startet den Tasks "Aktualisieren" auf einem Remotecomputer befindet, Svr01:
```
schtasks /run /tn Update /s Svr01
```
In diesem Fall **SchTasks.exe** wird die folgende Fehlermeldung angezeigt:
```
ERROR: Unable to run the scheduled task "Update".
```
Um die Ursache des Fehlers zu finden, suchen Sie in das Transaktionsprotokoll geplante Tasks C:\Windows\SchedLgU.txt auf Svr01. In diesem Fall wird der folgende Eintrag im Protokoll angezeigt:
```
"Update.job" (update.exe) 3/26/2001 1:15:46 PM ** ERROR **
The attempt to log on to the account associated with the task failed, therefore, the task did not run.
The specific error is:
0x8007052e: Logon failure: unknown user name or bad password.
Verify that the task's Run-as name and password are valid and try again.

```
Offensichtlich ist, gilt der Benutzername oder das Kennwort in der Aufgabe nicht auf dem System. Die folgenden **"SCHTASKS" / Change** Befehl aktualisiert den Benutzernamen und das Kennwort für den Update-Vorgang auf Svr01:
```
schtasks /change /tn Update /s Svr01 /ru Administrator /rp PassW@rd3
```
Nach der **ändern** Befehl abgeschlossen ist, die **ausführen** Befehl wiederholt wird. Dieses Mal das Update.exe-Programm wird gestartet und **SchTasks.exe** wird die folgende Meldung angezeigt:
```
SUCCESS: Attempted to run the scheduled task "Update".
```
Wie die Nachricht schon sagt, **"SCHTASKS"** versucht, Sie starten die Anwendung, aber es nicht überprüfen kann, die das Programm tatsächlich gestartet wurde.

## <a name="BKMK_end"></a>schtasks end

Beendet ein Programm, das von einer Aufgabe gestartet.

### <a name="syntax"></a>Syntax

```
schtasks /end /tn <TaskName> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>Parameter

|Begriff|Definition|
|----|----------|
|TN \<TaskName >|Erforderlich. Gibt die Aufgabe, die das Programm gestartet.|
|/ s \<Computer >|Gibt den Namen oder die IP-Adresse eines Remotecomputers. Der Standardwert ist der lokale Computer.|
|/u [\<Domain>\]<User>|Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers des lokalen Computers ausgeführt. Das angegebene Benutzerkonto muss Mitglied der Gruppe "Administratoren" auf dem Remotecomputer ausgeführt werden. Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.|
|/ p \<Kennwort >|Gibt das Kennwort des Benutzerkontos im der **/u** Parameter. Bei Verwendung der **/u** Parameter jedoch weglassen der **/p** Parameter oder die Password-Argument, **"SCHTASKS"** aufgefordert, ein Kennwort einzugeben.</br>Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.|
|/?|Zeigt Hilfe an.|

### <a name="remarks"></a>Hinweise

**SchTasks.exe** beendet nur die Instanzen eines Programms durch einen geplanten Task gestartet. Verwenden Sie TaskKill, um andere Prozesse zu beenden. Weitere Informationen finden Sie unter [Taskkill](taskkill.md).

### <a name="examples"></a>Beispiele

### <a name="to-end-a-task-on-a-local-computer"></a>Um eine Aufgabe auf einem lokalen Computer zu beenden.

Der folgende Befehl beendet die Instanz von Notepad.exe, die von der Aufgabe My Notepad gestartet wurde:
```
schtasks /end /tn "My Notepad"
```
Im Gegenzug **SchTasks.exe** beendet die Instanz von Notepad.exe, dass die Aufgabe gestartet, und es wird die folgende Erfolgsmeldung angezeigt:
```
SUCCESS: The scheduled task "My Notepad" has been terminated successfully.
```

### <a name="to-end-a-task-on-a-remote-computer"></a>Um eine Aufgabe auf einem Remotecomputer zu beenden.

Der folgende Befehl beendet die Instanz von Internet Explorer, die von der Aufgabe InternetAn auf dem Remotecomputer Svr01 gestartet wurde:
```
schtasks /end /tn InternetOn /s Svr01
```
Im Gegenzug **SchTasks.exe** beendet die Instanz von Internet Explorer an, dass die Aufgabe gestartet und die folgende Erfolgsmeldung angezeigt:
```
SUCCESS: The scheduled task "InternetOn" has been terminated successfully.
```

## <a name="BKMK_delete"></a>schtasks delete

Löscht eine geplante Aufgabe an.

### <a name="syntax"></a>Syntax

```
schtasks /delete /tn {<TaskName> | *} [/f] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>Parameter

|Begriff|Definition|
|----|----------|
|/tn {\<TaskName>| *}|Erforderlich. Identifiziert den Task gelöscht wird.</br>**\<TaskName >** -löscht die Aufgabe.</br>**<\*>** -Löscht den geplante Aufgaben auf dem Computer.|
|/f|Unterdrückt die bestätigungsmeldung angezeigt. Der Vorgang wird ohne Warnung gelöscht.|
|/ s \<Computer >|Gibt den Namen oder IP-Adresse eines Remotecomputers an (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer.|
|/u [\<Domain>\]<User>|Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers des lokalen Computers ausgeführt.</br>Das angegebene Benutzerkonto muss Mitglied der Gruppe "Administratoren" auf dem Remotecomputer ausgeführt werden. Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.|
|/ p \<Kennwort >|Gibt das Kennwort des Benutzerkontos im der **/u** Parameter. Bei Verwendung der **/u** Parameter jedoch weglassen der **/p** Parameter oder die Password-Argument, **"SCHTASKS"** aufgefordert, ein Kennwort einzugeben.</br>Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

-   Die **löschen** Vorgang löscht den Task im Zeitplan. Löschen das Programm, das die Aufgabe ausgeführt wird oder kein ausgeführtes Programm zu unterbrechen.
-   Die **löschen \***  Befehl löscht alle geplanten Tasks für den Computer, nicht nur die Aufgaben, die vom aktuellen Benutzer geplant.

### <a name="examples"></a>Beispiele

### <a name="to-delete-a-task-from-the-schedule-of-a-remote-computer"></a>So löschen Sie einen Task im Zeitplan von einem Remotecomputer

Der folgende Befehl löscht den Task "Mail starten" aus dem Zeitplan von einem Remotecomputer befindet. Er verwendet den **/s** Parameter, um den Remotecomputer zu identifizieren.
```
schtasks /delete /tn "Start Mail" /s Svr16
```
Im Gegenzug **SchTasks.exe** wird die folgende Bestätigung angezeigt. Drücken Sie Y, um die Aufgabe zu löschen,**.** Geben Sie den Befehl um abzubrechen, **n**:
```
WARNING: Are you sure you want to remove the task "Start Mail" (Y/N )? 
SUCCESS: The scheduled task "Start Mail" was successfully deleted.
```

### <a name="to-delete-all-tasks-scheduled-for-the-local-computer"></a>So löschen Sie alle für den lokalen Computer geplanten tasks

Der folgende Befehl löscht alle Aufgaben aus dem Zeitplan des lokalen Computers, einschließlich der Aufgaben, die von anderen Benutzern geplant. Er verwendet den **TN \***  Parameter, um alle Aufgaben auf dem Computer darstellen und die **/f** Parameter, um die Bestätigung zu unterdrücken.
```
schtasks /delete /tn * /f
```
Im Gegenzug **SchTasks.exe** zeigt die folgenden Erfolg an, dass die einzige Aufgabe geplant, Sicherheitsskript, gelöscht wird.

`SUCCESS: The scheduled task "SecureScript" was successfully deleted.`

## <a name="BKMK_query"></a>"SCHTASKS"-Abfrage

Zeigt die Aufgaben, die auf dem Computer ausgeführt.

### <a name="syntax"></a>Syntax

```
schtasks [/query] [/fo {TABLE | LIST | CSV}] [/nh] [/v] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>Parameter

|Begriff|Definition|
|----|----------|
|[/query]|Der Name des Vorgangs ist optional. Eingabe **"SCHTASKS"** ohne Parameter eine Abfrage ausführt.|
|/fo {TABLE| LISTE| CSV}|Gibt das Ausgabeformat. **Tabelle** ist die Standardeinstellung.|
|/nh|Lässt die Spaltenüberschriften in der Tabelle werden angezeigt. Dieser Parameter ist gültig, mit der **Tabelle** und **CSV** Ausgabeformate.|
|/v|Fügt die erweiterten Eigenschaften der Tasks auf dem Bildschirm hinzu.</br>Abfragen mit **/v** formatiert werden sollen, als **Liste** oder **CSV**.|
|/ s \<Computer >|Gibt den Namen oder IP-Adresse eines Remotecomputers an (mit oder ohne umgekehrte Schrägstriche). Der Standardwert ist der lokale Computer.|
|/u [\<Domain>\]<User>|Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers des lokalen Computers ausgeführt.</br>Das angegebene Benutzerkonto muss Mitglied der Gruppe "Administratoren" auf dem Remotecomputer ausgeführt werden. Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.|
|/ p \<Kennwort >|Gibt das Kennwort des Benutzerkontos im der **/u** Parameter. Bei Verwendung von **/u**, jedoch weglassen **/p** oder dem Password-Argument, **"SCHTASKS"** aufgefordert, ein Kennwort einzugeben.</br>Die **/u** und **/p** Parameter gültig sind nur bei Verwendung von **/s**.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

**SchTasks.exe** beendet nur die Instanzen eines Programms durch einen geplanten Task gestartet. Verwenden Sie TaskKill, um andere Prozesse zu beenden. Weitere Informationen finden Sie unter [Taskkill](taskkill.md).

### <a name="examples"></a>Beispiele

### <a name="to-display-the-scheduled-tasks-on-the-local-computer"></a>Um den geplanten Tasks auf dem lokalen Computer anzuzeigen.

Die folgenden Befehle anzuzeigen, alle Aufgaben, die für den lokalen Computer geplant wird. Diese Befehle das gleiche Ergebnis erzielt und können austauschbar verwendet werden.
```
schtasks
schtasks /query
```
Im Gegenzug **SchTasks.exe** der Aufgaben in der standardmäßigen, einfachen Tabellenformat angezeigt, wie in der folgenden Tabelle dargestellt:
```
TaskName Next Run Time Status
========================= ======================== ==============
Microsoft Outlook At logon time
SecureScript 14:42:00 PM , 2/4/2001

```

### <a name="to-display-advanced-properties-of-scheduled-tasks"></a>Zum Anzeigen der erweiterter Eigenschaften des geplanten tasks

Der folgende Befehl fordert eine detaillierte Anzeige der Tasks auf dem lokalen Computer. Er verwendet den **/v** Parameter, um eine detaillierte (ausführliche) Anzeige anzufordern und die **/Fo Liste** Parameter, um die Anzeige als Liste zur besseren Lesbarkeit zu formatieren. Sie können diesen Befehl verwenden, um sicherzustellen, dass eine Aufgabe, die Sie erstellt das beabsichtigte Serienmuster verfügt.

**schtasks /query /fo LIST /v**

Im Gegenzug **SchTasks.exe** zeigt eine Liste mit detaillierten Eigenschaften für alle Aufgaben. Die folgende Anzeige zeigt die Aufgabenliste für eine Aufgabe 4:00 Uhr ausgeführt. am letzten Freitag des Monats:
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

### <a name="to-log-tasks-scheduled-for-a-remote-computer"></a>Anmelden für einen Remotecomputer geplante Aufgaben

Der folgende Befehl fordert eine Liste der Aufgaben, die für einen Remotecomputer geplant, und die Aufgaben in eine durch Trennzeichen getrennte-Protokolldatei auf dem lokalen Computer hinzugefügt. Sie können dieses Befehlsformat verwenden, zum Erfassen und Nachverfolgen von Aufgaben, die für mehrere Computer vorgesehen sind.

Der Befehl verwendet den **/s** Parameter, um den Remotecomputer Reskit16, identifizieren die **/Fo** Parameter zum Angeben des Formats und der **NH** Parameter, um die Spalte zu unterdrücken Überschriften. Die **>>** Symbol leitet die Ausgabe an das Taskprotokoll p0102.csv, auf dem lokalen Computer, Svr01 anfügen. Da der Befehl auf dem Remotecomputer ausgeführt wird, muss der Pfad des lokalen Computers vollqualifiziert sein.
```
schtasks /query /s Reskit16 /fo csv /nh >> \\svr01\data\tasklogs\p0102.csv
```
Im Gegenzug **SchTasks.exe** fügt hinzu, die für den Computer Reskit16 zur p0102.csv-Datei auf dem lokalen Computer Svr01 geplanten Aufgaben.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
