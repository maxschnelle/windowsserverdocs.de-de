---
title: bcdedit
description: Windows-Befehle Thema **Bcdedit** – neue Niederlassungen erstellen, vorhandene Speicher ändern und fügen Sie im Menü-Startparameter.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab2da47d-3aac-44a0-b7fd-bd9561d61553
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/27/2018
ms.openlocfilehash: c1ac016b299cbd72a406121c54762f4457b24286
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872441"
---
# <a name="bcdedit"></a>bcdedit



Dateien für den Start (Configuration Data, BCD) Geben Sie einen Speicher, der zum Beschreiben von Boot-Anwendungen, und starten die Einstellungen für Anwendungen verwendet wird. Die Objekte und Elemente im Speicher ersetzen effektiv "Boot.ini".

BCDEdit ist ein Befehlszeilentool zum Verwalten von BCD-Speicher. Kann für eine Vielzahl von Zwecken, z. B. zum Erstellen neuer Speicher verwendet werden, vorhandene Speicher ändern, Hinzufügen von Menü-Startparameter und so weiter. BCDEdit dient im Wesentlichen den gleichen Zweck wie Bootcfg.exe in früheren Versionen von Windows, jedoch mit zwei wichtige Verbesserungen vorgenommen:
-   Stellt eine größere Anzahl von Startparameter als Bootcfg.exe an.
-   Unterstützung für Skripting wurde verbessert werden.

> [!NOTE]
> BCDEdit verwenden, um Startkonfigurationsdaten ändern, sind Administratorrechte erforderlich.

BCDEdit ist das wichtigste Tool für die Bearbeitung der Startkonfiguration von Windows Vista und höheren Versionen von Windows. Es ist in der Windows Vista-Verteilung im Ordner %WINDIR%\System32 enthalten.

BCDEdit ist die standard-Datentypen auf, und es dient in erster Linie zum Ausführen der einzelner allgemeine Änderungen, die in BCD. Für komplexere Vorgänge oder nicht dem Standard entsprechende Datentypen sollten Sie in Betracht ziehen, die Startkonfigurationsdaten (Windows Management Instrumentation, WMI)-Anwendungsprogrammierschnittstelle (API) zum Erstellen von leistungsstarken und flexiblen benutzerdefinierte Tools zu verwenden.

## <a name="syntax"></a>Syntax

```
BCDEdit /Command [<Argument1>] [<Argument2>] ...
```

## <a name="parameters"></a>Parameter

### <a name="general-bcdedit-command-line-option"></a>Allgemeine BCDEdit-Befehlszeilenoption

|Option|Beschreibung|
|------|-----------|
|/?|Zeigt eine Liste von BCDEdit-Befehlen. Das Ausführen dieses Befehls ohne Argument zeigt eine Zusammenfassung der verfügbaren Befehle. Führen Sie zum Anzeigen der detaillierten Hilfe für einen bestimmten Befehl **Bcdedit /?** \<Befehl >, wobei <command> ist der Name des Befehls, die Sie suchen Weitere Informationen zu. Z. B. **Bcdedit /? Createstore** zeigt detaillierte Hilfe für den Createstore-Befehl.|

### <a name="parameters-that-operate-on-a-store"></a>Parameter, die für eine Store ausgeführt werden

|Option|Beschreibung|
|------|-----------|
|/createstore|Erstellt einen neuen leeren Boot Configuration-Datenspeicher. Die erstellte Speicher ist kein Systemspeicher.|
|/ Export|Exportiert den Inhalt des Systems in eine Datei zu speichern. Diese Datei kann später verwendet werden, um den Zustand des Systemspeichers wiederherzustellen. Dieser Befehl gilt nur für den Systemspeicher.|
|/import|Hiermit wird der Status des Systemspeichers mithilfe einer Sicherung von Daten-Datei, die zuvor generiert, indem die **/export** Option. Dieser Befehl löscht die Einträge in den Systemspeicher, vor der Import der Durchführung. Dieser Befehl gilt nur für den Systemspeicher.|
|/ Store|Diese Option kann mit den meisten BCDedit-Befehlen verwendet werden, an den Store verwendet werden. Wenn diese Option nicht angegeben wird, klicken Sie dann verarbeitet BCDEdit den Systemspeicher. Ausführen der **Bcdedit/store** Befehl selbst ist äquivalent zur Ausführung der **Bcdedit/Enum active** Befehl.|

### <a name="parameters-that-operate-on-entries-in-a-store"></a>Parameter, die für die Einträge in einem Store verwendet werden

|Parameter|Beschreibung|
|---------|-----------|
|Copy|Eine Kopie einer angegebenen Starteintrag im gleichen Systemspeicher.|
|oder erstellen.|Erstellt einen neuen Eintrag im Boot Configuration Data-Speicher. Wenn ein allgemein bekannte Bezeichner angegeben wird, und klicken Sie dann die **Anwendung/**, **/ erben**, und **/Device** können keine Parameter angegeben werden. Wenn ein Bezeichner nicht angegeben oder nicht bekannt, ist ein **Anwendung/**, **/ erben**, oder **/Device** Option muss angegeben werden.|
|/delete|Löscht ein Element aus einem angegebenen Eintrag.|

### <a name="parameters-that-operate-on-entry-options"></a>Parameter, die für die Optionen für die Einträge verwendet werden

|Parameter|Beschreibung|
|---------|-----------|
|/deletevalue|Löscht ein angegebenes Element aus dem einen Starteintrag.|
|/set|Legt einen Eintrag-Wert fest.|

### <a name="parameters-that-control-output"></a>Parameter, die Ausgabe zu steuern

|Parameter|Beschreibung|
|---------|-----------|
|/ Enum|Listet Einträge in einem Speicher. Die **/enum** Option ist der Standardwert für BCEdit, also die **Bcdedit** Befehl ohne Parameter ist äquivalent zur Ausführung der **Bcdedit/Enum active** Befehl.|
|/v|Ausführlichen Modus fest. In der Regel werden alle bekannten Eintragsbezeichner durch ihren Anzeigenamen Kurzschriftform dargestellt. Angeben von **/v** wie eine Befehlszeilenoption alle Bezeichner vollständig angezeigt. Ausführen der **Bcdedit/v** Befehl selbst ist äquivalent zur Ausführung der **Bcdedit/Enum active/v** Befehl.|

### <a name="parameters-that-control-the-boot-manager"></a>Parameter, die der Start-Manager steuern

|Parameter|Beschreibung|
|---------|-----------|
|/bootsequence|Gibt eine einmalige Anzeigereihenfolge, die für den nächsten Systemstart verwendet werden. Dieser Befehl ähnelt der **/displayorder** Option, mit dem Unterschied, dass die It verwendet wird, nur der nächsten Ausführung des Computers wird gestartet. Anschließend wird der Computer mit der ursprünglichen Anzeigereihenfolge zurückgesetzt.|
|/ Standard|Gibt den Standardeintrag, der der Start-Manager wählt aus, wenn das Timeout abläuft.|
|/displayorder|Gibt an, die Anzeigereihenfolge, die der Start-Manager verwendet werden, wenn Parameter für den Systemstart zu einem Benutzer angezeigt.|
|/timeout|Gibt die Zeit in Sekunden, bevor der Start-Manager den Standardeintrag wählt warten.|
|/toolsdisplayorder|Gibt an, die Anzeigereihenfolge für den Start-Manager verwenden, bei der Anzeige der **Tools** Menü.|

### <a name="parameters-that-control-emergency-management-services"></a>Parameter, die Notverwaltungsdienste steuern.

|Parameter|Beschreibung|
|---------|-----------|
|/bootems|Aktiviert oder deaktiviert (Emergency Management Services, EMS) für den angegebenen Eintrag.|
|/ems|Aktiviert oder deaktiviert EMS für den Starteintrag des angegebenen Betriebssystem.|
|/emssettings|Legt die globalen EMS-Einstellungen für den Computer fest. **/Emssettings** nicht aktivieren oder Deaktivieren von EMS für einen bestimmten Starteintrag.|

### <a name="parameters-that-control-debugging"></a>Parameter, die steuern, Debuggen

|Parameter|Beschreibung|
|---------|-----------|
|/bootdebug|Aktiviert oder deaktiviert den Startdebugger für einen angegebenen Starteintrag. Dieser Befehl für alle Starteintrag funktioniert, es ist zwar nur für die Boot-Anwendungen.|
|/dbgsettings|Gibt an, oder die globalen Debuggereinstellungen den Einstellungen für das System angezeigt. Mit diesem Befehl nicht aktiviert oder deaktiviert den Kerneldebugger; Verwenden Sie die **/debug** Option für diesen Zweck. Um einen einzelnen globalen Debuggereinstellung festzulegen, verwenden die **Bcdedit/Set** \<Dbgsettings > <type> <value> -Befehl abgerufen wird.|
|/debug|Aktiviert oder deaktiviert den Kerneldebugger für einen angegebenen Starteintrag.|

## <a name="examples"></a>Beispiele

Beispiele von BCDEdit finden Sie in der [Verweis von BCDEdit Optionen](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference).