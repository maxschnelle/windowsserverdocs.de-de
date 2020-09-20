---
title: Verwalten von Funktionen
description: System Insights macht eine Vielzahl von Einstellungen verfügbar, die für jede Funktion konfiguriert werden können. diese Einstellungen können angepasst werden, um den spezifischen Anforderungen Ihrer Bereitstellung gerecht zu werden. In diesem Thema wird beschrieben, wie die verschiedenen Einstellungen für jede Funktion über das Windows Admin Center oder PowerShell verwaltet werden, und es werden grundlegende PowerShell-Beispiele und Windows Admin Center-Screenshots bereitgestellt, um die Anpassung dieser Einstellungen zu veranschaulichen.
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 6/05/2018
ms.openlocfilehash: 3f4e80136b3c70b7a121663a6defa048d2b0e852
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766223"
---
# <a name="managing-capabilities"></a>Verwalten von Funktionen

>Gilt für: Windows Server 2019

In Windows Server 2019 bietet System Insights eine Reihe von Einstellungen, die für jede Funktion konfiguriert werden können. diese Einstellungen können angepasst werden, um den spezifischen Anforderungen Ihrer Bereitstellung gerecht zu werden. In diesem Thema wird beschrieben, wie die verschiedenen Einstellungen für jede Funktion über das Windows Admin Center oder PowerShell verwaltet werden, und es werden grundlegende PowerShell-Beispiele und Windows Admin Center-Screenshots bereitgestellt, um die Anpassung dieser Einstellungen zu veranschaulichen.

>[!TIP]
>Sie können diese kurzen Videos auch verwenden, um Sie bei den ersten Schritten und der Verwaltung von System Insights zu unterstützen: Einstieg in die ersten Schritte [mit System Insights in 10 Minuten](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

Obwohl dieser Abschnitt PowerShell-Beispiele enthält, können Sie die [Dokumentation zu System Insights PowerShell](/powershell/module/systeminsights/) verwenden, um alle Cmdlets, Parameter und Parametersätze in System Insights anzuzeigen.

## <a name="viewing-capabilities"></a>Anzeigen von Funktionen

Zum Einstieg können Sie alle verfügbaren Funktionen mithilfe des Cmdlets **Get-insightscapability** auflisten:

```PowerShell
Get-InsightsCapability
```
Diese Funktionen sind auch in der System Insights-Erweiterung sichtbar:

![Übersichtsseite von System Insights Auflisten der verfügbaren Funktionen](media/overview-page-contoso.png)

## <a name="enabling-and-disabling-a-capability"></a>Aktivieren und Deaktivieren einer Funktion
Jede Funktion kann aktiviert oder deaktiviert werden. Durch das Deaktivieren einer Funktion wird verhindert, dass diese Funktion aufgerufen wird, und bei nicht standardmäßigen Funktionen wird durch das Deaktivieren einer Funktion die gesamte Datensammlung für diese Funktion beendet. Standardmäßig sind alle Funktionen aktiviert, und Sie können den Status einer Funktion mithilfe des Cmdlets **Get-insightscapability** überprüfen.

Um eine Funktion zu aktivieren oder zu deaktivieren, verwenden Sie die Cmdlets **enable-insightscapability** und **Deaktivieren-insightscapability** :

```PowerShell
Enable-InsightsCapability -Name "CPU capacity forecasting"
Disable-InsightsCapability -Name "Networking capacity forecasting"
```
Diese Einstellungen können auch durch Auswahl einer Funktion im Windows Admin Center ein-/ausgeschaltet werden, indem Sie auf die Schaltflächen **aktivieren** oder **Deaktivieren** klicken.

### <a name="invoking-a-capability"></a>Aufrufen einer Funktion
Wenn Sie eine Funktion aufrufen, wird die Funktion zum Abrufen einer Vorhersage sofort ausgeführt. Administratoren können jederzeit eine Funktion aufrufen, indem Sie im Windows Admin Center auf die Schaltfläche " **aufrufen** " oder das Cmdlet " **Aufruf-insightscapability** " klicken:

```PowerShell
Invoke-InsightsCapability -Name "CPU capacity forecasting"
```

>[!TIP]
>Um sicherzustellen, dass der Aufruf einer Funktion nicht mit kritischen Vorgängen auf dem Computer in Konflikt steht, sollten Sie Vorhersagen außerhalb der Geschäftszeiten planen.

## <a name="retrieving-capability-results"></a>Abrufen von Funktions Ergebnissen
Nachdem eine Funktion aufgerufen wurde, werden die neuesten Ergebnisse mithilfe von " **Get-insightscapability** " oder " **Get-insightscapabilityresult**" angezeigt. Mit diesen Cmdlets werden die neuesten **Status** -und **Status Beschreibungen** der einzelnen Funktionen ausgegeben, die das Ergebnis der einzelnen Vorhersagen beschreiben. Die Felder **Status** und **Statusbeschreibung** werden weiter unten im Dokument mit den Grundlagen von [Funktionen](understanding-capabilities.md)beschrieben.

Darüber hinaus können Sie das Cmdlet **Get-insightscapabilityresult** verwenden, um die letzten 30 Vorhersage Ergebnisse anzuzeigen und die der Vorhersage zugeordneten Daten abzurufen:

```PowerShell
# Specify the History parameter to see the last 30 prediction results.
Get-InsightsCapabilityResult -Name "CPU capacity forecasting" -History

# Use the Output field to locate and then show the results of "CPU capacity forecasting."
# Specify the encoding as UTF8, so that Get-Content correctly parses non-English characters.
$Output = Get-Content (Get-InsightsCapabilityResult -Name "CPU capacity forecasting").Output -Encoding UTF8 | ConvertFrom-Json
$Output.ForecastingResults
```
Die System Insights-Erweiterung zeigt automatisch den Vorhersage Verlauf an und analysiert die Ergebnisse des JSON-Ergebnisses, sodass Sie ein intuitives, qualitativ hoch gefases Diagramm der einzelnen Vorhersagen erhalten:

![Einzelne funktionsseite mit einem Prognose Diagramm und dem Vorhersage Verlauf](media/cpu-forecast-2.png)

### <a name="using-the-event-log-to-retrieve-capability-results"></a>Verwenden des Ereignis Protokolls zum Abrufen von Funktions Ergebnissen
System Insights protokolliert jedes Mal ein Ereignis, wenn eine Funktion eine Vorhersage abschließt. Diese Ereignisse werden im Channel " **Microsoft-Windows-System-Insights/admin** " angezeigt, und System Insights veröffentlicht eine andere Ereignis-ID für jeden Status:

| Vorhersage Status | Ereignis-ID |
| --------------- | --------------- |
| OK, | 151 |
| Warnung | 148 |
| Kritisch | 150 |
| Fehler | 149 |
| Keine | 132 |

>[!TIP]
>Verwenden Sie [Azure Monitor](https://azure.microsoft.com/services/monitor/) oder [System Center Operations Manager](/system-center/scom/welcome?view=sc-om-1807) , um diese Ereignisse zu aggregieren und die Vorhersage Ergebnisse für eine Gruppe von Computern anzuzeigen.


## <a name="setting-a-capability-schedule"></a>Festlegen eines Funktions Zeitplans
Zusätzlich zu on-Demand-Vorhersagen können Sie regelmäßige Vorhersagen für jede Funktion konfigurieren, sodass die angegebene Funktion automatisch nach einem vordefinierten Zeitplan aufgerufen wird. Verwenden Sie das Cmdlet **Get-insightscapabilityschedule** , um Funktions Zeitpläne anzuzeigen:

>[!TIP]
>Verwenden Sie den Pipeline-Operator in PowerShell, um Informationen zu allen Funktionen anzuzeigen, die vom Cmdlet " **Get-insightscapability** " zurückgegeben werden.

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilitySchedule
```

Periodische Vorhersagen sind standardmäßig aktiviert, aber Sie können jederzeit mithilfe der Cmdlets " **enable-insightscapabilityschedule** " und " **Deaktivieren-insightscapabilityschedule** " deaktiviert werden:

```PowerShell
Enable-InsightsCapabilitySchedule -Name "Total storage consumption forecasting"
Disable-InsightsCapabilitySchedule -Name "Volume consumption forecasting"
```

Jede Standardfunktion wird für jeden Tag um 3 Uhr geplant. Sie können jedoch benutzerdefinierte Zeitpläne für jede Funktion erstellen, und System Insights unterstützt eine Vielzahl von Zeit Plan Typen, die mithilfe des Cmdlets **Set-insightscapabilityschedule** konfiguriert werden können:

```PowerShell
Set-InsightsCapabilitySchedule -Name "CPU capacity forecasting" -Daily -DaysInterval 2 -At 4:00PM
Set-InsightsCapabilitySchedule -Name "Networking capacity forecasting" -Daily -DaysOfWeek Saturday, Sunday -At 2:30AM
Set-InsightsCapabilitySchedule -Name "Total storage consumption forecasting" -Hourly -HoursInterval 2 -DaysOfWeek Monday, Wednesday, Friday
Set-InsightsCapabilitySchedule -Name "Volume consumption forecasting" -Minute -MinutesInterval 30
```
>[!NOTE]
>Da die Standardfunktionen tägliche Daten analysieren, empfiehlt es sich, tägliche Zeitpläne für diese Funktionen zu verwenden. Weitere Informationen zu den Standardfunktionen [finden Sie hier](understanding-capabilities.md).

Sie können auch das Windows Admin Center verwenden, um Zeitpläne für jede Funktion anzuzeigen und festzulegen, indem Sie auf **Einstellungen**klicken. Der aktuelle Zeitplan wird auf der Registerkarte **Zeitplan** angezeigt, und Sie können die GUI-Tools verwenden, um einen neuen Zeitplan zu erstellen:

![Seite "Einstellungen" mit aktuellem Zeitplan](media/schedule-page-contoso.png)

## <a name="creating-remediation-actions"></a>Erstellen von Wiederherstellungs Aktionen
Mit System Insights können Sie benutzerdefinierte Wiederherstellungs Skripts basierend auf dem Ergebnis einer Funktion starten. Für jede Funktion können Sie ein benutzerdefiniertes PowerShell-Skript für jeden Vorhersage Status konfigurieren, sodass Administratoren automatisch Korrekturmaßnahmen ergreifen können, anstatt einen manuellen Eingriff zu erfordern.

Beispiele für Wiederherstellungs Aktionen sind das Ausführen der Datenträger Bereinigung, das Erweitern eines Volumes, das Ausführen der Deduplizierung, das Live migrieren von VMS und das Einrichten Azure-Dateisynchronisierung

Sie können die Aktionen für jede Funktion mithilfe des Cmdlets **Get-insightscapabilityaction** anzeigen:

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilityAction
```

Mithilfe der Cmdlets " **Set-insightscapabilityaction** " und " **Remove-insightscapabilityaction** " können Sie neue Aktionen erstellen oder vorhandene Aktionen löschen. Jede Aktion wird mit Anmelde Informationen ausgeführt, die im **Action Credential** -Parameter angegeben sind.

>[!NOTE]
>In der ersten System Insights-Version müssen Sie Wiederherstellungs Skripts außerhalb der Benutzerverzeichnisse angeben. Dies wird in einem bevorstehenden Release behoben.

```PowerShell
$Cred = Get-Credential
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning -Action "C:\Users\Public\WarningScript.ps1" -ActionCredential $Cred
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Critical -Action "C:\Users\Public\CriticalScript.ps1" -ActionCredential $Cred

Remove-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning
```

Mithilfe der Registerkarte **Aktionen** auf der Seite **Einstellungen** können Sie auch Wiederherstellungs Aktionen mithilfe des Windows Admin Centers festlegen:

![Seite "Einstellungen", auf der Benutzer Wartungs Aktionen angeben können](media/actions-page-contoso.png)


## <a name="additional-references"></a>Weitere Verweise
Weitere Informationen zu System Insights finden Sie in den folgenden Ressourcen:

- [Systemdaten: Übersicht](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Hinzufügen und Entwickeln von Funktionen](adding-and-developing-capabilities.md)
- [FAQ zu System Insights](faq.md)