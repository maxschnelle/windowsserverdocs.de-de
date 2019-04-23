---
title: Verwalten von Funktionen
description: System Insights stellt eine Vielzahl von Einstellungen, die für die einzelnen Funktionen konfiguriert werden können, und diese Einstellungen können in Ihrer Bereitstellung die besonderen Anforderungen Adresse optimiert werden. Dieses Thema beschreibt die verschiedenen Einstellungen für die einzelnen Funktionen über Windows Admin Center oder PowerShell, die grundlegende PowerShell-Beispiele und Windows Admin Center Screenshots veranschaulicht, wie Sie diese Einstellungen anpassen, bereitstellen zu verwalten.
ms.custom: na
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 6/05/2018
ms.openlocfilehash: 9081a0b576ab9871b47df38255047b6cbe889419
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868021"
---
# <a name="managing-capabilities"></a>Verwalten von Funktionen

>Gilt für: Windows Server 2019

In Windows Server-2019 System Insights stellt eine Vielzahl von Einstellungen, die für die einzelnen Funktionen konfiguriert werden können und diese Einstellungen können in Ihrer Bereitstellung die besonderen Anforderungen Adresse optimiert werden. Dieses Thema beschreibt die verschiedenen Einstellungen für die einzelnen Funktionen über Windows Admin Center oder PowerShell, die grundlegende PowerShell-Beispiele und Windows Admin Center Screenshots veranschaulicht, wie Sie diese Einstellungen anpassen, bereitstellen zu verwalten. 

>[!TIP]
>Sie können auch in diesen kurzen Videos verwenden, können Sie erste Schritte und zuverlässig verwalten System Insights: [Erste Schritte mit System Einblicke in 10 Minuten](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

Obwohl in diesem PowerShell-Beispiele bereitstellt, können Sie die [System Insights – PowerShell-Dokumentation](https://aka.ms/systeminsightspowershell) allen Cmdlets, Parameter und Parameter in System Insights angezeigt. 

## <a name="viewing-capabilities"></a>Anzeigen von Funktionen

Informationen zum Einstieg können Sie Auflisten aller verfügbaren Funktionen mithilfe der **Get-InsightsCapability** Cmdlet: 

```PowerShell
Get-InsightsCapability
``` 
Diese Funktionen sind auch im System-Insights-Erweiterung angezeigt:

![Seite "Übersicht" System Insights Auflisten von verfügbaren Funktionen](media/overview-page-contoso.png)

## <a name="enabling-and-disabling-a-capability"></a>Aktivieren und deaktivieren eine Funktion
Jede Funktion kann aktiviert oder deaktiviert werden. Deaktivieren eine Funktion verhindert, dass diese Funktion aufgerufen wird und für nicht standardmäßige-Funktionen und alle Datensammlung für diese Funktion beendet eine Funktion zu deaktivieren. Standardmäßig sind alle Funktionen aktiviert, und sehen Sie sich den Status einer Funktion mit dem **Get-InsightsCapability** Cmdlet. 

Verwenden Sie zum Aktivieren oder deaktivieren eine Funktion, die **aktivieren-InsightsCapability** und **Disable-InsightsCapability** Cmdlets:

```PowerShell
Enable-InsightsCapability -Name "CPU capacity forecasting"
Disable-InsightsCapability -Name "Networking capacity forecasting"
``` 
Diese Einstellungen auch ausgeschaltet werden, durch die eine Funktion in Windows Admin Center auf ausgewählten der **aktivieren** oder **deaktivieren** Schaltflächen.

### <a name="invoking-a-capability"></a>Eine Funktion aufrufen
Eine Funktion direkt aufrufen, führt die Möglichkeit, eine Vorhersage zu abzurufen, und Administratoren können Aufrufen einer Funktion jederzeit durch Klicken auf die **Invoke** Schaltfläche in Windows Admin Center oder mithilfe der  **Rufen Sie InsightsCapability** Cmdlet:

```PowerShell
Invoke-InsightsCapability -Name "CPU capacity forecasting"
```

>[!TIP]
>Um sicherzustellen, dass eine Funktion aufrufen kritische Vorgänge auf dem Computer nicht widerspricht, erwägen Sie in der Vorhersagen zu planen, während der Geschäftszeiten ausschalten.

## <a name="retrieving-capability-results"></a>Abrufen der Ergebnisse
Nachdem eine Funktion aufgerufen wurde, die neuesten Ergebnisse sind sichtbar **Get-InsightsCapability** oder **Get-InsightsCapabilityResult**. Diese Cmdlets der letzten Ausgabe **Status** und **Statusbeschreibung** der einzelnen Funktionen, die das Ergebnis der einzelnen Vorhersage beschreiben. Die **Status** und **Statusbeschreibung** Felder ausführlicher beschrieben werden die [Grundlegendes zu Funktionen Dokument](understanding-capabilities.md). 

Darüber hinaus können Sie mithilfe der **Get-InsightsCapabilityResult** Cmdlet zum Anzeigen der Vorhersageergebnisse der letzten 30 und zum Abrufen der Daten, die mit der Vorhersage verknüpft ist: 

```PowerShell
# Specify the History parameter to see the last 30 prediction results.
Get-InsightsCapabilityResult -Name "CPU capacity forecasting" -History

# Use the Output field to locate and then show the results of "CPU capacity forecasting."
# Specify the encoding as UTF8, so that Get-Content correctly parses non-English characters.
$Output = Get-Content (Get-InsightsCapabilityResult -Name "CPU capacity forecasting").Output -Encoding UTF8 | ConvertFrom-Json
$Output.ForecastingResults
```
Die System-Insights-Erweiterung automatisch zeigt den Verlauf für die Vorhersage und analysiert die Ergebnisse des JSON-Ergebnisses wird Ihnen nur ein Diagramm intuitiv und sehr detailgetreue jede Planung:

![Funktion zum einmaligen-Seite, die mit einem forecasting-Diagramm und den Verlauf für die Vorhersage](media/cpu-forecast-2.png)

### <a name="using-the-event-log-to-retrieve-capability-results"></a>Verwenden das Ereignisprotokoll zum Abrufen der Ergebnisse
System Insights protokolliert ein Ereignis jedes Mal, eine Funktion eine Vorhersage abgeschlossen ist. Diese Ereignisse werden in der **Microsoft-Windows-System-Insights/Admin** Channel und Insights von System veröffentlicht eine anderes Ereignis-ID für jeden Status:   

| Vorhersage-status | Ereignis-ID |
| --------------- | --------------- |
| OK | 151 |
| Warnung | 148 |
| Kritisch | 150 |
| Fehler | 149 |
| Keine | 132 |

>[!TIP]
>Verwendung [Azure Monitor](https://azure.microsoft.com/services/monitor/) oder [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) diese Ereignisse zu aggregieren und Vorhersageergebnisse, die für eine Gruppe von Computern.


## <a name="setting-a-capability-schedule"></a>Festlegen eines Zeitplans für die Funktion
Zusätzlich zu einer bedarfsgesteuerten vorhersagen können Sie regelmäßige Vorhersagen für jede Funktion konfigurieren, damit, dass die angegebene Funktion automatisch nach einem vordefinierten Zeitplan aufgerufen wird. Verwenden der **Get-InsightsCapabilitySchedule** Cmdlet, um die Funktion Zeitplänen finden Sie unter: 

>[!TIP]
>In PowerShell den Pipelineoperator verwenden, um Informationen für alle Funktionen, die zurückgegeben werden, indem die **Get-InsightsCapability** Cmdlet.

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilitySchedule
```

Regelmäßige Vorhersagen sind standardmäßig aktiviert, obwohl sie jederzeit deaktiviert werden, können die **aktivieren-InsightsCapabilitySchedule** und **Disable-InsightsCapabilitySchedule** Cmdlets:

```PowerShell
Enable-InsightsCapabilitySchedule -Name "Total storage consumption forecasting"
Disable-InsightsCapabilitySchedule -Name "Volume consumption forecasting"
```

Jede Standardfunktion ist geplant, jeden Tag um 3 Uhr ausgeführt. Sie können jedoch benutzerdefinierte Zeitpläne für jede Funktion erstellen und Insights von System unterstützt eine Vielzahl von Zeitplantypen, die mit konfiguriert werden können die **Set-InsightsCapabilitySchedule** Cmdlet: 

```PowerShell
Set-InsightsCapabilitySchedule -Name "CPU capacity forecasting" -Daily -DaysInterval 2 -At 4:00PM
Set-InsightsCapabilitySchedule -Name "Networking capacity forecasting" -Daily -DaysOfWeek Saturday, Sunday -At 2:30AM
Set-InsightsCapabilitySchedule -Name "Total storage consumption forecasting" -Hourly -HoursInterval 2 -DaysOfWeek Monday, Wednesday, Friday
Set-InsightsCapabilitySchedule -Name "Volume consumption forecasting" -Minute -MinutesInterval 30 
```
>[!NOTE]
>Da die Standardfunktionen täglichen Daten zu analysieren, hat es empfohlen, um tageszeitpläne für diese Funktionen zu verwenden. Erfahren Sie mehr über die Standardfunktionen [hier](understanding-capabilities.md).

Sie können auch Windows Admin Center verwenden, anzeigen und Festlegen der Zeitpläne für die einzelnen Funktionen durch Klicken auf **Einstellungen**. Sehen Sie der aktuelle Zeitplan für die **Zeitplan** Registerkarte, und Sie können die GUI-Tools verwenden, um einen neuen Zeitplan erstellen:

![Zeigt aktuelle Zeitplan auf der Seite "Einstellungen"](media/schedule-page-contoso.png)

## <a name="creating-remediation-actions"></a>Erstellen von Aktionen zur Problembehebung
System Insights können Sie die benutzerdefinierte Wiederherstellungsskripts, die abhängig vom Ergebnis einer Funktion zu starten. Für jede Funktion können Sie konfigurieren, benutzerdefinierte PowerShell-Skript zum Status der einzelnen Vorhersagen, da Administratoren korrigierenden Maßnahmen ergreift automatisch, anstatt dass manueller Eingriff erforderlich. 

Beispiel-Wartungsaktionen einschließen, Ausführen der Datenträgerbereinigung, erweitern ein Volume mit Deduplizierung live Migration von virtuellen Computern und das Einrichten von Azure File Sync.

Sehen Sie die Aktionen für jede Funktion mithilfe der **Get-InsightsCapabilityAction** Cmdlet:

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilityAction
```

Sie können neue Aktionen erstellen oder löschen Sie vorhandene Aktionen, die mit der **Set-InsightsCapabilityAction** und **Remove-InsightsCapabilityAction** Cmdlets. Jede Aktion ausgeführt wird, im angegebenen, Anmeldeinformationen über die **ActionCredential** Parameter.

>[!NOTE]
>In der ersten Version des System-Einblicke müssen Sie die Bereinigungsskripts außerhalb von Verzeichnissen nach Benutzer angeben. Dies wird in einer zukünftigen Version behoben.

```PowerShell
$Cred = Get-Credential
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning -Action "C:\Users\Public\WarningScript.ps1" -ActionCredential $Cred
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Critical -Action "C:\Users\Public\CriticalScript.ps1" -ActionCredential $Cred

Remove-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning
```

Sie können auch Windows Admin Center verwenden, Festlegen von Aktionen zur Problembehebung durch Verwendung der **Aktionen** Registerkarte in der **Einstellungen** Seite:

![Seite "Einstellungen", in dem Benutzer Aktionen zur Problembehebung angeben kann](media/actions-page-contoso.png)


## <a name="see-also"></a>Siehe auch
Weitere Informationen zum System Insights können Sie die folgenden Ressourcen:

- [System-Insights-Übersicht](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Hinzufügen und die Entwicklung von Funktionen](adding-and-developing-capabilities.md)
- [System Insights – häufig gestellte Fragen](faq.md)