---
ms.assetid: acc0803b-fa05-4fc3-b94d-2916abf4fdbd
title: Grundlegendes zur Datendeduplizierung
ms.technology: storage-deduplication
ms.prod: windows-server
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: 54ad12c1631df39b6fdbe06c78e1a300ff5d73bd
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955602"
---
# <a name="understanding-data-deduplication"></a>Grundlegendes zur Datendeduplizierung

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

Dieses Dokument beschreibt, wie die [Datendeduplizierung](overview.md) funktioniert.

## <a name="how-does-data-deduplication-work"></a><a name="how-does-dedup-work"></a>Wie funktioniert die Datendeduplizierung?

Die Datendeduplizierung unter Windows Server folgt zwei Prinzipien:

1. **Die Optimierung darf Schreibvorgänge auf den Datenträger nicht beeinträchtigen**  
    Datendeduplizierung optimiert Daten mithilfe eines Nachbearbeitungsmodells. Alle Daten werden in nicht optimierter Form auf den Datenträger geschrieben und später durch Datendeduplizierung optimiert.

2. **Die Optimierung darf die Zugriffssemantik nicht ändern**  
    Benutzer und Anwendungen, die auf Daten auf einem optimierten Volume zugreifen, bemerken nicht, dass die Dateien, auf die sie zugreifen, dedupliziert wurden.

Sobald diese Option für ein Volume aktiviert ist, wird die Datendeduplizierung zu folgenden Zwecken im Hintergrund ausgeführt:

- Identifizieren von sich wiederholenden Mustern über Dateien auf diesem Volume hinweg.
- Nahtloses Verschieben dieser Teile oder Blöcke mit speziellen, als [Analysepunkte](#dedup-term-reparse-point) bezeichneten Zeigern, die auf eine eindeutige Kopie dieses Blocks verweisen.

Dies erfolgt in den folgenden vier Schritten:

1. Überprüfen des Dateisystems auf Dateien, die die Optimierungsrichtlinie erfüllen  
![Durchsuchen des Dateisystems](media/understanding-dedup-how-dedup-works-1.gif)  
2. Aufteilen von Dateien in Blöcke variabler Größe  
![Aufteilen von Dateien in Blöcke](media/understanding-dedup-how-dedup-works-2.gif)
3. Bestimmen eindeutiger Blöcke  
![Bestimmen eindeutiger Blöcke](media/understanding-dedup-how-dedup-works-3.gif)
4. Platzieren von Blöcken im Blockspeicher und optionales Komprimieren  
![Verschieben in Blockspeicher](media/understanding-dedup-how-dedup-works-4.gif)
5. Ersetzen des ursprünglichen Dateidatenstroms von nun optimierten Dateien durch einen Analysepunkt im Blockspeicher  
![Ersetzen des Dateidatenstroms durch Analysepunkt](media/understanding-dedup-how-dedup-works-5.gif)

Wenn optimierte Dateien gelesen werden, sendet das Dateisystem die Dateien mit einem Analysepunkt an den Datendeduplizierungs-Dateisystemfilter (Dedup.sys). Der Filter leitet den Lesevorgang an die entsprechenden Blöcke weiter, die den Stream für diese Datei im Blockspeicher bilden. Änderungen an Bereichen einer deduplizierten Datei werden in nicht optimierter Form auf den Datenträger geschrieben und vom [Optimierungsauftrag](understand.md#job-info) bei dessen nächster Ausführung optimiert.

## <a name="usage-types"></a><a id="usage-type"></a>Verwendungstypen
Bei den folgenden Verwendungstypen kann die Datendeduplizierung für gängige Workloads sinnvoll konfiguriert werden:  

| Nutzungstyp | Ideale Workloads | Unterschiede |
|------------|-----------------|------------------|
| <a id="usage-type-default"></a>Vorgegebene | Allgemeiner Dateiserver:<ul><li>Teamfreigaben</li><li>Arbeitsordner</li><li>Umleitung des Ordners</li><li>Freigaben für die Softwareentwicklung</li></ul> | <ul><li>Hintergrundoptimierung</li><li>Standardoptimierungsrichtlinie:<ul><li>Minimales Dateialter = 3 Tage</li><li>Optimieren verwendeter Dateien = Nein</li><li>Teilweises Optimieren von Dateien = Nein</li></ul></li></ul> |
| <a id="usage-type-hyperv"></a>Hyper-V- | VDI-Server (virtuelle Desktopinfrastruktur) | <ul><li>Hintergrundoptimierung</li><li>Standardoptimierungsrichtlinie:<ul><li>Minimales Dateialter = 3 Tage</li><li>Optimieren verwendeter Dateien = Ja</li><li>Teilweises Optimieren von Dateien = Ja</li></ul></li><li>„Verdeckte“ Optimierungsmethoden für Interoperabilität mit Hyper-V</li></ul> |
| <a id="usage-type-backup"></a>Backup | Virtualisierte Sicherungs Anwendungen, wie z. b. [Microsoft Data Protection Manager (DPM)](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)) | <ul><li>Optimierung mit Prioritäten</li><li>Standardoptimierungsrichtlinie:<ul><li>Minimales Dateialter = 0 Tage</li><li>Optimieren verwendeter Dateien = Ja</li><li>Teilweises Optimieren von Dateien = Nein</li></ul></li><li>„Verdeckte“ Optimierungsmethoden für Interoperabilität mit DPM bzw. DPM-ähnlichen Lösungen</li></ul> |

## <a name="jobs"></a><a id="job-info"></a>Tze
Zur Datendeduplizierung erfolgt eine Nachbearbeitung zum Optimieren und Aufrechterhalten der Effizienz des Speicherplatzes eines Volumes.

| Auftragsname | Auftragsbeschreibung | Standardzeitplan |
|----------|------------------|------------------|
| <a id="job-info-optimization"></a>Optimierung | Der **Optimierungs** Auftrag wird dedupliziert, indem Daten auf einem Volume gemäß den volumerichtlinieneinstellungen segmentieren, (optional) diese Blöcke komprimiert und Blöcke im Blockspeicher gespeichert werden. Der für die Datendeduplizierung befolgte Optimierungsprozess wird unter [Wie funktioniert die Datendeduplizierung?](understand.md#how-does-dedup-work) detailliert beschrieben. | Einmal pro Stunde |
| <a id="job-info-gc"></a>Garbage Collection | Der Auftrag **Garbage Collection** gibt Speicherplatz frei, indem unnötige Blöcke entfernt werden, die von Dateien, die vor Kurzem geändert oder gelöscht wurden, nicht mehr referenziert werden. | Samstags um 2:35 Uhr |
| <a id="job-info-scrubbing"></a>Integrity Scrubbing | Der Auftrag **Integrity Scrubbing** bestimmt Beschädigungen im Blockspeicher aufgrund von Datenträgerfehlern oder fehlerhaften Sektoren. Sofern möglich, können für die Datendeduplizierung automatisch Volumefeatures (wie Spiegelung oder Parität auf einem „Speicherplätze“-Volume) genutzt werden, um die beschädigten Daten wiederherzustellen. Darüber hinaus werden bei der Datendeduplizierung Sicherungskopien häufig verwendeter Blöcke beibehalten, wenn diese in einem als „Hotspot“ bezeichneten Bereich mehr als 100 Mal referenziert werden. | Samstags um 03:35 Uhr |
| <a id="job-info-unoptimization"></a>Unoptimization | Der Auftrag **Unoptimization** ist ein Spezialauftrag, der nur manuell ausgeführt werden sollte. Er dient zum Rückgängigmachen der erfolgten Deduplizierung und deaktiviert die Datendeduplizierung auf dem jeweiligen Volume. | [Nur bei Bedarf](run.md#disabling-dedup) |

## <a name="data-deduplication-terminology"></a><a id="dedup-term"></a>Datendeduplizierungterminologie
| Begriff | Definition |
|------|------------|
| <a id="dedup-term-chunk"></a>Block | Ein Block ist ein Abschnitt der Datei, der vom Algorithmus zum Bestimmen von Blöcken der Datendeduplizierung ausgewählt wird, da er wahrscheinlich in anderen, ähnlichen Dateien vorkommt. |
| <a id="dedup-term-chunk-store"></a>Blockspeicher | Der Blockspeicher umfasst eine organisierte Folge von Containerdateien im Ordner „System Volume Information“, mit deren Hilfe für die Datendeduplizierung Blöcke eindeutig gespeichert werden. |
| <a id="dedup-term-dedup"></a>Deduplizierung | Ein Abkürzung für „Datendeduplizierung“, die in PowerShell, Windows Server-APIs und -Komponenten sowie in der Windows Server-Community häufig verwendet wird. |
| <a id="dedup-term-file-metadata"></a>Dateimetadaten | Jede Datei enthält Metadaten, die interessante Eigenschaften der Datei beschreiben und nicht mit dem Hauptinhalt der Datei verknüpft sind. Beispiele: Erstellungsdatum, Datum des letzten Lesevorgangs, Autor usw. |
| <a id="dedup-term-file-stream"></a>Dateidatenstrom | Der Dateidatenstrom ist der Hauptinhalt der Datei. Dies ist der Teil der Datei, der bei der Datendeduplizierung optimiert wird. |
| <a id="dedup-term-file-system"></a>Dateisystem | Das Dateisystem ist die Software und Datenstruktur auf dem Datenträger, die das Betriebssystem zum Speichern von Dateien auf Speichermedien verwendet. Die Datendeduplizierung wird auf mit NTFS formatierten Volumes unterstützt. |
| <a id="dedup-term-file-system-filter"></a>Dateisystemfilter | Ein Dateisystemfilter ist ein Plug-In, das das Standardverhalten des Dateisystems ändert. Zum Beibehalten der Zugriffssemantik verwendet die Datendeduplizierung einen Dateisystemfilter (Dedup.sys), um Lesevorgänge für den Benutzer bzw. die Anwendung, der/die die Leseanforderung stellt, völlig unbemerkt zu optimierten Inhalten umzuleiten. |
| <a id="dedup-term-optimization"></a>Optimierung | Eine Datei gilt als durch die Datendeduplizierung optimiert (bzw. dedupliziert), wenn sie in Blöcke aufgeteilt wurde und ihre eindeutigen Blöcke im Blockspeicher gespeichert wurden. |
| <a id="dedup-term-in-policy"></a>Optimierungsrichtlinie | Die Optimierungsrichtlinie gibt die Dateien an, die für die Datendeduplizierung berücksichtigt werden sollen. Beispielsweise können Dateien als nicht richtlinienkonform gelten, wenn sie ganz neu oder geöffnet sind, sich in einem bestimmten Pfad auf dem Volume befinden oder einen bestimmten Dateityp haben. |
| <a id="dedup-term-reparse-point"></a>Analysepunkt | Ein Analyse [Punkt](/windows/win32/fileio/reparse-points) ist ein spezielles Tag, das das Dateisystem darüber benachrichtigt, e/a-Vorgänge an einen angegebenen Dateisystem Filter zu übergeben. Nachdem der Dateidatenstrom einer Datei optimiert wurde, ersetzt die Datendeduplizierung den Datenstrom durch einen Analysepunkt. Dieser ermöglicht der Datendeduplizierung das Beibehalten der Zugriffssemantik für diese Datei. |
| <a id="dedup-term-volume"></a>Volume | Ein Volume ist ein Windows-Konstrukt für ein logisches Speicherlaufwerk, das sich über mehrere physische Speichergeräte auf einem oder mehreren Servern erstrecken kann. Die Datendeduplizierung wird auf Volumebasis aktiviert. |
| <a id="dedup-term-workload"></a>Workload | Eine Workload ist eine Anwendung, die unter Windows Server ausgeführt wird. Beispielworkloads sind allgemeiner Dateiserver, Hyper-V und SQL Server. |

> [!Warning]  
> Sofern nicht von autorisierten Microsoft-Supportmitarbeitern dazu aufgefordert, versuchen Sie nicht, den Blockspeicher manuell zu ändern. Andernfalls kann es zu Datenbeschädigungen oder -verlusten kommen.

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen
**Wie unterscheidet sich die Datendeduplizierung von anderen Optimierungsprodukten?**  
Es gibt mehrere wichtige Unterschiede zwischen der Datendeduplizierung und anderen gängigen Speicheroptimierungsprodukten:

* *Wie unterscheidet sich die Datendeduplizierung von Single Instance Store?*  
    Single Instance Store (oder SIS) war eine Vorgängertechnologie der Datendeduplizierung, die erstmals in Windows Storage Server 2008 R2 eingeführt wurde. Zum Optimieren eines Volume bestimmte Single Instance Store vollständig identische Dateien und ersetzte sie durch logische Links zu einer einzelnen Kopie einer Datei, die im allgemeinen SIS-Speicher gespeichert wurden. Im Gegensatz zu Single Instance Store kann das Feature „Datendeduplizierung“ für Einsparung von Speicherplatz in Dateien sorgen, die nicht identisch sind, jedoch viele gemeinsame Muster aufweisen, oder die selbst viele wiederholte Muster enthalten. Single Instance Store wurde für Windows Server 2012 R2 als veraltet gekennzeichnet und in Windows Server 2016 zugunsten der Datendeduplizierung entfernt.

* *Wie unterscheidet sich die Datendeduplizierung von der NTFS-Komprimierung?*  
    Die NTFS-Komprimierung ist ein Feature von NTFS, das Sie optional auf Volumeebene aktivieren können. Bei der NTFS-Komprimierung wird jede Datei mittels Komprimierung während des Schreibvorgangs einzeln optimiert. Im Gegensatz zur NTFS-Komprimierung ermöglicht die Datendeduplizierung das Einsparen von Speicherplatz in allen Dateien auf einem Volume. Dies ist gegenüber der NTFS-Komprimierung vorteilhaft, da die Dateien möglicherweise <u>sowohl</u> eine interne Duplizierung aufweisen (der mit der NTFS-Komprimierung begegnet wird) als auch Ähnlichkeiten mit anderen Dateien auf dem Datenträger haben (denen nicht mit der NTFS-Komprimierung begegnet wird). Darüber hinaus zeichnet sich die Datendeduplizierung durch ein Nachbearbeitungsmodell aus. Dies bedeutet, dass neue oder geänderte Dateien nicht optimiert auf den Datenträger geschrieben und mithilfe der Datendeduplizierung später optimiert werden.

* *Wie unterscheidet sich die Datendeduplizierung von Archivdatei Formaten wie ZIP, rar, 7z, CAB usw.?*  
    Archivdateiformate wie ZIP, RAR, 7z, CAB usw. wenden eine Komprimierung auf einen angegebenen Satz von Dateien an. Wie bei der Datendeduplizierung werden doppelte Muster innerhalb einer oder über mehrere Dateien optimiert. Allerdings müssen Sie die Dateien auswählen, die Sie dem Archiv hinzufügen möchten. Auch die Zugriffssemantik unterscheidet sich. Für den Zugriff auf eine bestimmte Datei innerhalb des Archivs müssen Sie das Archiv öffnen, eine bestimmte Datei auswählen und für die Verwendung dekomprimieren. Die Datendeduplizierung erfolgt von Benutzern und Administratoren unbemerkt und erfordert keine manuellen Eingriffe. Außerdem behält die Datendeduplizierung die Zugriffssemantik bei, sodass optimierte Dateien nach der Optimierung unverändert angezeigt werden.

**Kann ich die Datendeduplizierungseinstellungen für meinen ausgewählten Verwendungstyp ändern?**  
Ja. Obwohl die Datendeduplizierung für **empfohlene Workloads** Standardwerte bietet, möchten Sie möglicherweise dennoch die Datendeduplizierungseinstellungen optimieren, um Ihren Speicher optimal zu nutzen. Darüber hinaus [erfordern andere Workloads eine gewisse Optimierung, um sicherzustellen, dass die Datendeduplizierung die Workload nicht stört](install-enable.md#enable-dedup-sometimes-considerations).

**Kann ich einen Datendeduplizierungsauftrag manuell ausführen?**  
Ja, [alle Datendeduplizierungsaufträge können manuell ausgeführt werden](run.md#running-dedup-jobs-manually). Dies ist möglicherweise wünschenswert, wenn geplante Aufträge aufgrund unzureichender Systemressourcen oder eines Fehlers nicht ausgeführt wurden. Der Auftrag „Unoptimization“ kann nur manuell ausgeführt werden.

**Kann ich die Verlaufsergebnisse von Datendeduplizierungsaufträgen überwachen?**  
Ja, [alle Datendeduplizierungsaufträge erstellen Einträge im Windows-Ereignisprotokoll](run.md#monitoring-dedup).

**Kann ich die Standardzeitpläne für die Datendeduplizierungsaufträge auf meinem System ändern?**  
Ja, [alle Zeitpläne sind konfigurierbar](advanced-settings.md#modifying-job-schedules). Das Ändern der Standardzeitpläne für die Datendeduplizierung ist besonders wünschenswert, um sicherzustellen, dass die Datendeduplizierungsaufträge genügend Zeit bis zu ihrem Abschluss haben und nicht mit der Workload in Konkurrenz um Ressourcen stehen.
