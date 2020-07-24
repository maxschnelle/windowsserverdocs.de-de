---
ms.assetid: f15c02d7-1cbd-4eba-a571-0ea34ab93ef4
title: Ausführen der Datendeduplizierung
ms.technology: storage-deduplication
ms.prod: windows-server
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: f75a20a8b69a863209f6e782bd34e48d8c12fe91
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86962162"
---
# <a name="running-data-deduplication"></a>Ausführen der Datendeduplizierung

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

## <a name="running-data-deduplication-jobs-manually"></a><a id="running-dedup-jobs-manually"></a>Manuelles Ausführen der Datendeduplizierungsaufträge

Sie können jeden geplanten Datendeduplizierungsauftrag mit den folgenden PowerShell-Cmdlets manuell ausführen:
* [`Start-DedupJob`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)): Startet einen neuen datendeduplizierungsauftrag.
* [`Stop-DedupJob`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)): Stoppt einen bereits in Bearbeitung befindlichen datendeduplizierungsauftrag (oder entfernt ihn aus der Warteschlange).
* [`Get-DedupJob`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)): Zeigt alle aktiven und in der Warteschlange befindlichen datendeduplizierungsaufträge an.

Alle [Einstellungen, die verfügbar sind, wenn Sie einen Datendeduplizierungsauftrag planen](advanced-settings.md#modifying-job-schedules-available-settings), sind auch verfügbar, wenn Sie einen Auftrag manuell starten, mit Ausnahme der planungsspezifischen Einstellungen. Um z.B. einen [Optimierungsauftrag](understand.md#job-info-optimization) manuell mit hoher Priorität und maximaler Auslastung von CPU und Arbeitsspeicher zu starten, führen Sie den folgenden PowerShell-Befehl mit Administratorrechten aus:

```PowerShell
Start-DedupJob -Type Optimization -Volume <Your-Volume-Here> -Memory 100 -Cores 100 -Priority High
```

## <a name="monitoring-data-deduplication"></a><a id="monitoring-dedup"></a>Überwachen der Datendeduplizierung

### <a name="job-successes"></a><a id="monitoring-dedup-job-successes"></a>Auftragserfolge

Da die Datendeduplizierung ein Nachbearbeitungsmodell verwendet, ist es wichtig, dass [Datendeduplizierungsaufträge](understand.md#job-info) erfolgreich ausgeführt werden. Eine einfache Möglichkeit zum Überprüfen des Status des letzten Auftrags besteht darin, das [`Get-DedupStatus`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)) PowerShell-Cmdlet zu verwenden. Überprüfen Sie regelmäßig die folgenden Felder:

* Achten Sie für den [Optimierungsauftrag](understand.md#job-info-optimization) auf `LastOptimizationResult` (0 = erfolgreich), `LastOptimizationResultMessage` und `LastOptimizationTime` (sollte aktuell sein).
* Achten Sie für den [Speicherbereinigungsauftrag](understand.md#job-info-gc) auf `LastGarbageCollectionResult` (0 = erfolgreich), `LastGarbageCollectionResultMessage` und `LastGarbageCollectionTime` (sollte aktuell sein).
* Achten Sie für den [Integritätsbereinigungsauftrag](understand.md#job-info-scrubbing) auf `LastScrubbingResult` (0 = erfolgreich), `LastScrubbingResultMessage` und `LastScrubbingTime` (sollte aktuell sein).

> [!Note]  
> Weitere Informationen zu Auftragserfolgen und -fehlern finden Sie in der Windows-Ereignisanzeige unter `\Applications and Services Logs\Windows\Deduplication\Operational`.

### <a name="optimization-rates"></a><a id="monitoring-dedup-optimization-rates"></a>Optimierungsraten

Ein Indikator für einen Fehler beim [Optimierungsauftrag](understand.md#job-info-optimization) ist eine Optimierungsrate mit Abwärtstrend, die möglicherweise darauf hindeutet, dass die Optimierungsaufträge nicht mit der Änderungsrate mithalten. Sie können die Optimierungs Rate mithilfe des [`Get-DedupStatus`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)) PowerShell-Cmdlets überprüfen.

> [!Important]
> `Get-DedupStatus`verfügt über zwei Felder, die für die Optimierungs Rate relevant sind: `OptimizedFilesSavingsRate` und `SavingsRate` . Die Verfolgung beider Werte ist wichtig, sie haben jedoch unterschiedliche Bedeutungen.
> - `OptimizedFilesSavingsRate`gilt nur für die Dateien, die für die Optimierung "in-Policy" sind `space used by optimized files after optimization / logical size of optimized files` .
> - `SavingsRate`gilt für das gesamte Volume ( `space used by optimized files after optimization / total logical size of the optimization` ).

## <a name="disabling-data-deduplication"></a><a id="disabling-dedup"></a>Deaktivieren der Datendeduplizierung
Führen Sie zum Deaktivieren der Datendeduplizierung den [Deoptimierungsauftrag](understand.md#job-info-unoptimization) aus. Um die Volumeoptimierung rückgängig zu machen, führen Sie den folgenden Befehl aus:

```PowerShell
Start-DedupJob -Type Unoptimization -Volume <Desired-Volume>
```

> [!Important]  
> Beim Deoptimierungsauftrag tritt ein Fehler auf, wenn das Volume nicht über genügend Speicherplatz zum Speichern der nicht optimierten Daten verfügt.

## <a name="frequently-asked-questions"></a><a id="faq"></a>Häufig gestellte Fragen
**Gibt es ein System Center Operations Manager Management Pack zum Überwachen der Datendeduplizierung?**  
Ja. Die Datendeduplizierung kann über das System Center Management Pack für Dateiserver überwacht werden. Weitere Informationen finden Sie im [Handbuch für das System Center-Verwaltungspaket für File Server 2012 R2](https://download.microsoft.com/download/6/F/7/6F7A33B9-9383-48ED-9252-23C2C8AD1BDA/MPGuide_FileServer2012R2.doc).
