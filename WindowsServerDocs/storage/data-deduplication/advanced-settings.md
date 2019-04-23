---
ms.assetid: 01c8cece-66ce-4a83-a81e-aa6cc98e51fc
title: Erweiterte Einstellungen für die Datendeduplizierung
ms.prod: windows-server-threshold
ms.technology: storage-deduplication
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: 15cfc054810a2cab85aae9a04d6195c3ae6fe0b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861211"
---
# <a name="advanced-data-deduplication-settings"></a>Erweiterte Einstellungen für die Datendeduplizierung

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Dokument wird beschrieben, wie Sie die Einstellungen für die [Datendeduplizierung](overview.md) ändern können. Für [empfohlene Workloads](install-enable.md#enable-dedup-candidate-workloads) sollten die Standardeinstellungen ausreichend sein. Der Hauptgrund für das Ändern dieser Einstellungen ist das Verbessern der Leistung bei der Datendeduplizierung bei anderen Arten von Workloads.

## <a id="modifying-job-schedules"></a>Ändern der Zeitpläne für die Datendeduplizierung
Die [standardmäßigen Auftragszeitpläne für die Datendeduplizierung](understand.md#job-info) sind so ausgelegt, dass sie gut für empfohlene Workloads funktionieren und so unaufdringlich wie möglich sind (ausgenommen der Auftrag *PriorityOptimization*, der für den Verwendungstyp [**Sicherung** aktiviert ist](understand.md#usage-type-backup)). Wenn Workloads einen großen Ressourcenbedarf haben, kann sichergestellt werden, dass Aufträge nur zu Leerlaufzeiten ausgeführt werden oder die Menge der Systemressourcen verringert oder erhöht wird, die der Datendeduplizierungsauftrag nutzen darf.

### <a id="modifying-job-schedules-change-schedule"></a>Ändern eines Zeitplans für die Datendeduplizierung
Datendeduplizierungsaufträge können über den Windows-Aufgabenplanungsdienst geplant und im Pfad „Microsoft\Windows\Deduplication“ angezeigt und bearbeitet werden. Zur Datendeduplizierung gehören mehrere Cmdlets, die die Planung erleichtern.
* [`Get-DedupSchedule`](https://technet.microsoft.com/library/hh848446.aspx) Zeigt die aktuell geplanten Aufträge an.
* [`New-DedupSchedule`](https://technet.microsoft.com/library/hh848445.aspx) erstellt einen neuen geplanten Auftrag an.
* [`Set-DedupSchedule`](https://technet.microsoft.com/library/hh848447.aspx) Ändert einen vorhandenen geplanten Auftrag an.
* [`Remove-DedupSchedule`](https://technet.microsoft.com/library/hh848451.aspx) Entfernt einen geplanten Auftrag an.

Am häufigsten wird der Zeitpunkt der Ausführung von Datendeduplizierungsaufträgen geändert, um sicherzustellen, dass Aufträge außerhalb der Geschäftszeiten ausgeführt werden. Im folgenden Beispiel wird Schritt für Schritt gezeigt, wie Sie den Zeitplan für die Datendeduplizierung in einem *einfachen* Szenario ändern: ein hyperkonvergenter Hyper-V-Host, der an Wochenenden und wochentags ab 19:00 Uhr im Leerlauf ist. Um den Zeitplan zu ändern, führen Sie die folgenden PowerShell-Cmdlets im Kontext eines Administrators aus.

1. Deaktivieren Sie die stündlich geplanten Aufträge des Typs [Optimization](understand.md#job-info-optimization).  
    ```PowerShell
    Set-DedupSchedule -Name BackgroundOptimization -Enabled $false
    Set-DedupSchedule -Name PriorityOptimization -Enabled $false
    ```

2. Entfernen Sie die derzeit geplanten Aufträge [GarbageCollection](understand.md#job-info-gc) und [IntegrityScrubbing](understand.md#job-info-scrubbing).
    ```PowerShell
    Get-DedupSchedule -Type GarbageCollection | ForEach-Object { Remove-DedupSchedule -InputObject $_ }
    Get-DedupSchedule -Type Scrubbing | ForEach-Object { Remove-DedupSchedule -InputObject $_ }
    ```

3. Erstellen Sie einen Optimierungsauftrag, der um 19:00 Uhr mit hoher Priorität ausgeführt wird und alle auf dem System verfügbaren CPUs und den gesamten Arbeitsspeicher nutzt.
    ```PowerShell
    New-DedupSchedule -Name "NightlyOptimization" -Type Optimization -DurationHours 11 -Memory 100 -Cores 100 -Priority High -Days @(1,2,3,4,5) -Start (Get-Date "2016-08-08 19:00:00")
    ```

    >[!NOTE]  
    > Der *date*-Teil von `System.Datetime`, der für `-Start` angegeben ist, ist irrelevant (solange die Angabe in der Vergangenheit liegt), doch der *time*-Teil gibt an, wann der Auftrag gestartet werden soll.
4. Erstellen Sie einen wöchentlichen Garbage Collection-Auftrag, der samstags um 7:00 Uhr mit hoher Priorität ausgeführt wird und alle auf dem System verfügbaren CPUs und den gesamten Arbeitsspeicher nutzt.
    ```PowerShell
    New-DedupSchedule -Name "WeeklyGarbageCollection" -Type GarbageCollection -DurationHours 23 -Memory 100 -Cores 100 -Priority High -Days @(6) -Start (Get-Date "2016-08-13 07:00:00")
    ```

5. Erstellen Sie einen wöchentlichen Integritätsbereinigungsauftrag (Integrity Scrubbing), der samstags um 7:00 Uhr mit hoher Priorität ausgeführt wird und alle auf dem System verfügbaren CPUs und den gesamten Arbeitsspeicher nutzt.
    ```PowerShell
    New-DedupSchedule -Name "WeeklyIntegrityScrubbing" -Type Scrubbing -DurationHours 23 -Memory 100 -Cores 100 -Priority High -Days @(0) -Start (Get-Date "2016-08-14 07:00:00")
    ```

### <a id="modifying-job-schedules-available-settings"></a>Verfügbare Einstellungen für den gesamten Auftrag
Sie können die folgenden Einstellungen für neue oder geplante Datendeduplizierungsaufträge wechseln:

<table>
    <thead>
        <tr>
            <th style="min-width:125px">Name des Parameters</th>
            <th>Definition</th>
            <th>Zulässige Werte</th>
            <th>Gründe für das Festlegen dieses Werts</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Typ</td>
            <td>Der Typ des Auftrags, der geplant werden soll</td>
            <td>
                <ul>
                    <li>Optimization (Optimierung)</li>
                    <li>GarbageCollection</li>
                    <li>Scrubbing</li>
                </ul>
            </td>
            <td>Dieser Wert ist erforderlich, da es sich um den Typ des Auftrags handelt, der geplant werden soll. Dieser Wert kann nicht geändert werden, nachdem die Aufgabe geplant wurde.</td>
        </tr>
        <tr>
            <td>Priority</td>
            <td>Die Systempriorität des geplanten Auftrags</td>
            <td>
                <ul>
                    <li>Hoch</li>
                    <li>Mittel</li>
                    <li>Niedrig</li>
                </ul>
            </td>
            <td>Dieser Wert hilft dem System beim Zuordnen von CPU-Zeit. *High* benötigt mehr CPU-Zeit, *low* weniger.</td>
        </tr>
        <tr>
            <td>Days</td>
            <td>Die Tage, an denen der Auftrag geplant ist</td>
            <td>Eine Gruppe ganzer Zahlen von 0 bis 6, die die Tage der Woche darstellen:<ul>
                <li>0 = Sonntag</li>
                <li>1 = Montag</li>
                <li>2 = Dienstag</li>
                <li>3 = Mittwoch</li>
                <li>4 = Donnerstag</li>
                <li>5 = Freitag</li>
                <li>6 = Samstag</li>
            </ul></td>
            <td>Geplante Aufgaben müssen an mindestens einem Tag ausgeführt werden.</td>
        </tr>
        <tr>
            <td>Cores</td>
            <td>Der Prozentsatz der Kerne auf dem System, den ein Auftrag verwenden soll</td>
            <td>Ganze Zahlen von 0 bis 100 (Prozentsatz)</td>
            <td>Dient zum Steuern, welchen Einfluss ein Auftrag auf die Rechenressourcen des Systems hat</td>
        </tr>
        <tr>
            <td>DurationHours</td>
            <td>Die maximale Anzahl von Stunden, die ein Auftrag ausgeführt werden darf</td>
            <td>Positive ganze Zahlen</td>
            <td>Dient zum Verhindern, dass die Ausführung einer Workload den vorgegebenen Zeitrahmen überschreitet</td>
        </tr>
        <tr>
            <td>Enabled</td>
            <td>Gibt an, ob der Auftrag ausgeführt wird</td>
            <td>True/false</td>
            <td>Dient zum Deaktivieren eines Auftrags, ohne ihn zu entfernen</td>
        </tr>
        <tr>
            <td>Vollständig</td>
            <td>Dient zum Planen eines vollständigen Garbage Collection-Auftrags</td>
            <td>Schalter (True/False)</td>
            <td>Standardmäßig ist jeder vierte Auftrag ein vollständiger Garbage Collection-Auftrag. Mit diesem Schalter können Sie eine häufigere Ausführung vollständiger Garbage Collection-Aufträge planen.</td>
        </tr>
        <tr>
            <td>InputOutputThrottle</td>
            <td>Gibt den Umfang der Eingabe-/Ausgabedrosselung an, die auf den Auftrag angewendet wird</td>
            <td>Ganze Zahlen von 0 bis 100 (Prozentsatz)</td>
            <td>Durch die Drosselung wird sichergestellt, dass Aufträge andere E/A-intensive Prozesse nicht beeinträchtigen.</td>
        </tr>
        <tr>
            <td>Arbeitsspeicher</td>
            <td>Der Prozentsatz des Arbeitsspeichers auf dem System, den ein Auftrag verwenden soll</td>
            <td>Ganze Zahlen von 0 bis 100 (Prozentsatz)</td>
            <td>Dient zum Steuern, welchen Einfluss der Auftrag auf die Arbeitsspeicherressourcen auf dem System hat</td>
        </tr>
        <tr>
            <td>Name</td>
            <td>Der Name des geplanten Auftrags</td>
            <td>Zeichenfolge</td>
            <td>Ein Auftrag muss einen eindeutig identifizierbaren Namen haben.</td>
        </tr>
        <tr>
            <td>ReadOnly</td>
            <td>Gibt an, dass der Bereinigungsauftrag gefundene Beschädigungen verarbeitet und meldet, aber keine Reparaturaktionen durchführt</td>
            <td>Schalter (True/False)</td>
            <td>Sie müssen Dateien manuell wiederherstellen, die sich in fehlerhaften Bereichen des Datenträgers befinden.</td>
        </tr>
        <tr>
            <td>Beginn</td>
            <td>Gibt die Startzeit des Auftrags an</td>
            <td>`System.DateTime`</td>
            <td>Der *date*-Teil von `System.Datetime`, der für *Start* angegeben ist, ist irrelevant (solange die Angabe in der Vergangenheit liegt), doch der *time*-Teil gibt an, wann der Auftrag gestartet werden soll.</td>
        </tr>
        <tr>
            <td>StopWhenSystemBusy</td>
            <td>Gibt an, ob die Datendeduplizierung beendet werden soll, wenn das System ausgelastet ist</td>
            <td>Schalter (True/False)</td>
            <td>Mithilfe dieses Schalters können Sie das Verhalten bei der Datendeduplizierung steuern. Dies ist besonders wichtig, wenn Sie eine Datendeduplizierung während der Geschäftszeiten ausführen möchten.</td>
        </tr>
    </tbody>
</table>

## <a id="modifying-volume-settings"></a>Ändern die Datendeduplizierung volumeweite Einstellungen
### <a id="modifying-volume-settings-how-to-toggle"></a>Umschalten der Volumeeinstellungen
Sie können die volumeweiten Standardeinstellungen für die Datendeduplizierung über den [Verwendungstyp](understand.md#usage-type) festlegen, den Sie auswählen, wenn Sie eine Deduplizierung für ein Volume aktivieren. Die Datendeduplizierung umfasst Cmdlets, die volumeweite Einstellungen erleichtern:

* [`Get-DedupVolume`](https://technet.microsoft.com/library/hh848448.aspx)
* [`Set-DedupVolume`](https://technet.microsoft.com/library/hh848438.aspx)

Die Hauptgründe für das Ändern der Volumeeinstellungen für den ausgewählten Verwendungstyp sind das Verbessern der Leseleistung für bestimmte Dateien (z. B. Multimedia- oder andere Dateitypen, die bereits komprimiert sind) oder das Optimieren der Datendeduplizierung für Ihre spezifische Workload. Im folgenden Beispiel wird veranschaulicht, wie die Volumeeinstellungen für die Datendeduplizierung für eine Workload geändert werden, die sehr einer Workload eines allgemeinen Dateiservers ähnelt, aber große Dateien aufweist, die sich häufig ändern.

1. Anzeigen der aktuellen Volumeeinstellungen für das freigegebene Clustervolume 1.
    ```PowerShell
    Get-DedupVolume -Volume C:\ClusterStorage\Volume1 | Select *
    ```

2. Aktivieren Sie „OptimizePartialFiles“ für das freigegebene Clustervolume 1, sodass die Richtlinie „MinimumFileAge“ für Abschnitte der Datei statt für die gesamte Datei gilt. Dies stellt sicher, dass die Mehrzahl der Dateien optimiert wird, obwohl sich Abschnitte der Datei regelmäßig ändern.
    ```PowerShell
    Set-DedupVolume -Volume C:\ClusterStorage\Volume1 -OptimizePartialFiles
    ```

### <a id="modifying-volume-settings-available-settings"></a>Verfügbare volumeweite Einstellungen
<table>
    <thead>
        <tr>
            <th style="min-width:125px">Einstellungsname</th>
            <th>Definition</th>
            <th>Zulässige Werte</th>
            <th>Gründe für das Ändern dieses Werts</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ChunkRedundancyThreshold</td>
            <td>Gibt an, wie häufig ein Block referenziert wird, bevor ein Block in den Abschnitt „Hotspot“ des Blockspeichers dupliziert wird. Der Nutzen des Abschnitts „Hotspot“ ist, dass diese sehr aktiven (engl. hot) Blöcke, die häufig referenziert werden, mehrere Zugriffspfade haben, um die Zugriffszeit zu verbessern.</td>
            <td>Positive ganze Zahlen</td>
            <td>Der Hauptgrund zum Ändern dieses Werts ist das Erhöhen der Einsparungsrate für Volumes mit hoher Duplizierung. Im Allgemeinen ist der Standardwert (100) die empfohlene Einstellung, die Sie nicht ändern sollten.</td>
        </tr>
        <tr>
            <td>ExcludeFileType</td>
            <td>Dateitypen, die von der Optimierung ausgeschlossen sind</td>
            <td>Gruppe von Dateinamenerweiterungen</td>
            <td>Einige Dateitypen, insbesondere Multimedia- oder andere Dateien, die bereits komprimiert sind, profitieren nicht besonders von einer Optimierung. Mit dieser Einstellung können Sie konfigurieren, welche Dateitypen ausgeschlossen werden.</td>
        </tr>
        <tr>
            <td>ExcludeFolder</td>
            <td>Gibt die Ordnerpfade an, die für die Optimierung nicht berücksichtigt werden sollen</td>
            <td>Gruppe von Ordnerpfaden</td>
            <td>Wenn Sie die Leistung verbessern oder verhindern möchten, dass Inhalte in bestimmten Pfaden optimiert werden, können Sie bestimmte Pfade auf dem Volume von der Optimierung ausschließen.</td>
        </tr>
        <tr>
            <td>InputOutputScale</td>
            <td>Gibt die Ebene der E/A-Parallelisierung (E/A-Warteschlangen) für die Datendeduplizierung an, die während eines Nachbearbeitungsauftrags auf einem Volume verwendet werden soll</td>
            <td>Positive ganze Zahlen von 1 bis 36</td>
            <td>Der Hauptgrund zum Ändern dieses Werts ist das Verringern der Auswirkung auf die Leistung einer hohen E/A-Workload, indem die Anzahl der E/A-Warteschlangen eingeschränkt wird, die für die Datendeduplizierung auf einem Volume verwendet werden darf. Beachten Sie, dass eine vom Standard abweichende Änderung dieser Einstellung dafür sorgen kann, dass Nachbearbeitungsaufträge für die Datendeduplizierung langsam erfolgen.</td>
        </tr>
        <tr>
            <td>MinimumFileAgeDays</td>
            <td>Anzahl der Tage nach Erstellung der Datei, ehe die Datei für die Optimierungsrichtlinie berücksichtigt wird.</td>
            <td>Positive ganze Zahlen (einschließlich null)</td>
            <td>Bei den Verwendungstypen **Standard** und **HyperV** wird dieser Wert auf 3 festgelegt, um die Leistung für sehr aktive oder zuletzt erstellte Dateien zu maximieren. Möglicherweise möchten Sie dies ändern, wenn die Datendeduplizierung aggressiver erfolgen soll oder Sie die zusätzliche Latenz aufgrund der Deduplizierung in Kauf nehmen.</td>
        </tr>
        <tr>
            <td>MinimumFileSize</td>
            <td>Minimale Größe, die eine Datei haben muss, um von der Optimierungsrichtlinie berücksichtigt zu werden</td>
            <td>Positive ganze Zahlen (Bytes) größer als 32 KB</td>
            <td>Der Hauptgrund zum Ändern dieses Werts ist das Ausschließen kleiner Dateien mit eingeschränktem Optimierungsnutzen zum Einsparen von Rechenzeit.</td>
        </tr>
        <tr>
            <td>NoCompress</td>
            <td>Gibt an, ob die Blöcke komprimiert werden sollen, bevor sie im Blockspeicher abgelegt werden</td>
            <td>True/False</td>
            <td>Einige Arten von Dateien, insbesondere Multimediadateien und bereits komprimierte Dateitypen, lassen sich möglicherweise nicht weiter komprimieren. Mit dieser Einstellung können Sie die Komprimierung für alle Dateien auf dem Volume deaktivieren. Dies ist ideal, wenn Sie ein Dataset mit vielen Dateien optimieren, die bereits komprimiert sind.</td>
        </tr>
        <tr>
            <td>NoCompressionFileType</td>
            <td>Dateitypen, deren Blöcke nicht komprimiert werden sollen, bevor sie im Blockspeicher abgelegt werden</td>
            <td>Gruppe von Dateinamenerweiterungen</td>
            <td>Einige Arten von Dateien, insbesondere Multimediadateien und bereits komprimierte Dateitypen, lassen sich möglicherweise nicht weiter komprimieren. Diese Einstellung ermöglicht das Deaktivieren der Komprimierung für diese Dateien, was CPU-Ressourcen schont.</td>
        </tr>
        <tr>
            <td>OptimizeInUseFiles</td>
            <td>Falls aktiviert, werden Dateien mit aktiven Handles von der Optimierungsrichtlinie berücksichtigt.</td>
            <td>True/false</td>
            <td>Aktivieren Sie diese Einstellung, wenn Ihre Workload Dateien für längere Zeit geöffnet hält. Wenn diese Einstellung nicht aktiviert ist, würde eine Datei nie optimiert werden, wenn die Workload einen offenen Handle dafür hat, auch wenn nur gelegentlich Daten am Ende angefügt werden.</td>
        </tr>
        <tr>
            <td>OptimizePartialFiles</td>
            <td>Falls aktiviert, gilt der „MinimumFileAge“-Wert für Segmente einer Datei und nicht für die gesamte Datei.</td>
            <td>True/false</td>
            <td>Aktivieren Sie diese Einstellung, wenn Ihre Workload mit großen, häufig bearbeiteten Dateien arbeitet, bei denen ein Großteil des Dateiinhalts unverändert bleibt. Wenn diese Einstellung nicht aktiviert ist, würden diese Dateien nie optimiert werden, da sie weiter geändert werden, auch wenn der Großteil des Dateiinhalts für eine Optimierung bereit ist.</td>
        </tr>
        <tr>
            <td>Verify</td>
            <td>Wenn, falls aktiviert, der Hash eines Blocks einem Block entspricht, der bereits im Blockspeicher enthalten ist, werden die Blöcke byteweise verglichen, um sicherzustellen, dass sie identisch sind.</td>
            <td>True/false</td>
            <td>Dies ist ein Integritätsfeature, das sicherstellt, dass der Hashalgorithmus, der die Blöcke vergleicht, nicht den Fehler macht, zwei Datenblöcke zu vergleichen, die eigentlich unterschiedlich sind, aber denselben Hash haben. In der Praxis ist es sehr unwahrscheinlich, dass dies jemals passiert. Das Aktivieren der Überprüfungsfunktion bedeutet für den Optimierungsauftrag einen beträchtlichen Mehraufwand.</td>
        </tr>
    </tbody>
</table>

## <a id="modifying-dedup-system-settings"></a>Ändern die Datendeduplizierung systemweite Einstellungen
Für die Datendeduplizierung gibt es zusätzliche systemweite Einstellungen, die über [die Registrierung](https://technet.microsoft.com/library/cc755256(v=ws.11).aspx) konfiguriert werden können. Diese Einstellungen gelten für alle Aufträge und Volumes, die auf dem System ausgeführt werden. Die Bearbeitung der Registrierung muss äußerst umsichtig erfolgen.

Angenommen, Sie möchten die vollständige Garbage Collection deaktivieren. Weitere Informationen dazu, warum dies für Ihr Szenario hilfreich sein kann, finden Sie in den [häufig gestellten Fragen](#faq-why-disable-full-gc). So bearbeiten Sie die Registrierung mit PowerShell

* Wenn die Datendeduplizierung in einem Cluster ausgeführt wird:
    ```PowerShell
    Set-ItemProperty -Path HKLM:\System\CurrentControlSet\Services\ddpsvc\Settings -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    Set-ItemProperty -Path HKLM:\CLUSTER\Dedup -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    ```

* Wenn die Datendeduplizierung nicht in einem Cluster ausgeführt wird:
    ```PowerShell
    Set-ItemProperty -Path HKLM:\System\CurrentControlSet\Services\ddpsvc\Settings -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    ```

### <a id="modifying-dedup-system-settings-available-settings"></a>Verfügbare systemweite Einstellungen
<table>
    <thead>
        <tr>
            <th style="min-width:125px">Einstellungsname</th>
            <th>Definition</th>
            <th>Zulässige Werte</th>
            <th>Gründe für diese Änderung</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>WlmMemoryOverPercentThreshold</td>
            <td>Mithilfe dieser Einstellung können Aufträge mehr Arbeitsspeicher nutzen, als eigentlich für die Datendeduplizierung verfügbar ist. Die Einstellung 300 bedeutet beispielsweise, dass der Auftrag das Dreifache des zugewiesenen Arbeitsspeichers nutzen muss, um abgebrochen zu werden.</td>
            <td>Positive ganze Zahlen (der Wert 300 bedeutet 300 % oder das Dreifache)</td>
            <td>Wenn es eine andere Aufgabe gibt, die angehalten wird, wenn die Datendeduplizierung mehr Arbeitsspeicher verwendet</td>
        </tr>
        <tr>
            <td>DeepGCInterval</td>
            <td>Diese Einstellung konfiguriert das Intervall, in dem herkömmliche Garbage Collection-Aufträge [vollständige Garbage Collection-Aufträge](advanced-settings.md#faq-full-v-regular-gc) werden. Die Einstellung „n“ bedeutet, dass jeder n<sup>te</sup> Auftrag ein vollständiger Garbage Collection-Auftrag ist. Beachten Sie, dass die vollständige automatische Speicherbereinigung (unabhängig vom Registrierungswert) für Volumes mit dem [Verwendungstyp Sicherung](understand.md#usage-type-backup) immer deaktiviert ist. `Start-DedupJob -Type GarbageCollection -Full` kann verwendet werden, wenn vollständige Garbage Collection auf einem Volume Sicherung gewünscht ist.</td>
            <td>Ganze Zahlen (-1 bedeutet deaktiviert)</td>
            <td>Siehe [diese häufig gestellte](advanced-settings.md#faq-why-disable-full-gc) Frage</td>
        </tr>
    </tbody>
</table>

## <a id="faq"></a>Häufig gestellte Fragen
<a id="faq-use-responsibly"></a>**Ich habe eine Einstellung für die Datendeduplizierung, geändert und jetzt Aufträge sind langsam oder nicht abgeschlossen oder Leistung meiner Workload hat nachgelassen. Warum?**  
Diese Einstellungen bieten Ihnen viele Möglichkeiten zum Steuern der Ausführung der Datendeduplizierung. Nutzen Sie sie überlegt, und [überwachen Sie die Leistung](run.md#monitoring-dedup).

<a id="faq-running-dedup-jobs-manually"></a>**Ich möchte einen datendeduplizierungsauftrag sofort ausführen, aber ich möchte keinen neuen Zeitplan zu erstellen geht das?**  
Ja, [alle Aufträge können manuell ausgeführt werden](run.md#running-dedup-jobs-manually).

<a id="faq-full-v-regular-gc"></a>**Was ist der Unterschied zwischen vollständigen und einer herkömmlichen Garbage Collection?**  
Es gibt zwei Arten von [Garbage Collection](understand.md#job-info-gc):

- Für eine *herkömmliche Garbage Collection* wird ein statistischer Algorithmus verwendet, um große nicht referenzierte Datenblöcke zu suchen, die ein bestimmtes Kriterium (niedriger Wert für Arbeitsspeicher und IOPS) erfüllen. Bei der herkömmlichen Garbage Collection wird ein Blockspeicher erst komprimiert, wenn ein Mindestanteil der Blöcke nicht referenziert wird. Dieser Typ der Garbage Collection erfolgt wesentlich schneller und verwendet weniger Ressourcen als eine vollständige Garbage Collection. Der Standardzeitplan sieht eine Ausführung des herkömmlichen Garbage Collection-Auftrags einmal pro Woche vor.
- Bei der *vollständigen Garbage Collection* wird wesentlich gründlicher nach nicht referenzierten Blöcken gesucht und mehr Speicherplatz auf dem Datenträger freigegeben. Bei der vollständigen Garbage Collection werden alle Container komprimiert, auch wenn nur ein einzelner Block im Container nicht referenziert wird. Bei der vollständigen Garbage Collection wird zudem Speicherplatz freigeben, der ggf. in Gebrauch war, als während eines Optimierungsauftrags ein Absturz oder Stromausfall aufgetreten ist. Vollständige Garbage Collection-Aufträge stellen 100 % des verfügbaren Speicherplatzes wieder her, der auf einem deduplizierten Volume wiederhergestellt werden kann. Dazu sind allerdings im Vergleich mit einem herkömmlichen Garbage Collection-Auftrag mehr Zeit und Systemressourcen erforderlich. Beim vollständige Garbage Collection-Auftrag werden zumeist bis zu 5 % mehr der nicht referenzierten Daten gefunden und wieder freigegeben als bei einem herkömmlichen Garbage Collection-Auftrag. Jeder vierte geplante Garbage Collection-Auftrag ist ein vollständiger Garbage Collection-Auftrag.

<a id="faq-why-disable-full-gc"></a>**Warum sollten vollständige Garbage Collection deaktivieren?**  
- Die Garbage Collection kann sich negativ auf die Lebensdauer der Schattenkopien des Volumes und die Größe inkrementeller Sicherungen auswirken. Bei Workloads, die hohe Änderungsraten haben oder E/A-intensiv sind, kann durch vollständige Garbage Collection-Aufträge eine Verschlechterung der Leistung auftreten.           
- Sie können einen vollständigen Garbage Collection-Auftrag manuell in PowerShell ausführen, um Speicherverluste zu beheben, wenn Sie wissen, dass Ihr System abgestürzt ist.
