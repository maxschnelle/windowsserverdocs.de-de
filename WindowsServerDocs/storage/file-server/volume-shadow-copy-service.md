---
title: Volumeschattenkopie-Dienst
ms.date: 01/30/2019
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 7bdcb67c5bcb36d2ebe5ee02d765f3cab63c7bed
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766823"
---
# <a name="volume-shadow-copy-service"></a>Volumeschattenkopie-Dienst

Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2, Windows Server 2008, Windows 10, Windows 8.1, Windows 8, Windows 7

Das Sichern und Wiederherstellen wichtiger Geschäftsdaten kann aufgrund der folgenden Probleme sehr komplex sein:

  - Die Daten müssen in der Regel gesichert werden, während die Anwendungen, die die Daten liefern, noch ausgeführt werden. Dies bedeutet, dass einige der Datendateien geöffnet sein oder sich in einem inkonsistenten Zustand befinden können.

  - Wenn das Dataset groß ist, kann es schwierig sein, alle Daten gleichzeitig zu sichern.

Die ordnungsgemäße Ausführung von Sicherungs- und Wiederherstellungsvorgängen erfordert eine enge Koordination zwischen den Sicherungsanwendungen, den zu sichernden Branchenanwendungen und der Speicherverwaltungshardware und -software. Der Volumeschattenkopie-Dienst (Volume Shadow Copy Service oder VSS), der in Windows Server® 2003 eingeführt wurde, ermöglicht die Konversation zwischen diesen Komponenten, damit diese besser zusammenarbeiten können. Wenn alle Komponenten VSS unterstützen, können Sie sie verwenden, um Ihre Anwendungsdaten zu sichern, ohne die Anwendungen offline zu schalten.

VSS koordiniert die Aktionen, die erforderlich sind, um eine konsistente Schattenkopie (auch als Momentaufnahme, Snapshot oder Zeitpunktkopie bezeichnet) der zu sichernden Daten zu erstellen. Die Schattenkopie kann unverändert verwendet oder in Szenarien wie den folgenden verwendet werden:

  - Sie möchten Anwendungsdaten und Systemstatusinformationen sichern, einschließlich der Archivierung von Daten auf einem anderen Festplattenlaufwerk, Band oder anderen Wechselmedium.

  - Sie führen Data Mining aus.

  - Sie führen Sicherungen von Datenträger zu Datenträger (Disk-to-Disk, D2D) aus.

  - Sie müssen eine schnelle Wiederherstellung nach Datenverlust durchführen, indem Sie Daten auf der ursprünglichen LUN oder einer vollkommen neuen LUN wiederherstellen, die eine ursprüngliche, ausgefallene LUN ersetzt.


Zu den Windows-Features und -Anwendungen, die VSS verwenden, gehören die folgenden:

  - [Windows Server Backup](https://go.microsoft.com/fwlink/?linkid=180891) (https://go.microsoft.com/fwlink/?LinkId=180891)

  - [Schattenkopien von freigegebenen Ordnern](https://go.microsoft.com/fwlink/?linkid=142874) (https://go.microsoft.com/fwlink/?LinkId=142874)

  - [System Center Data Protection Manager 2008](https://go.microsoft.com/fwlink/?linkid=180892) (https://go.microsoft.com/fwlink/?LinkId=180892)

  - [Systemwiederherstellung](https://go.microsoft.com/fwlink/?linkid=180893) (https://go.microsoft.com/fwlink/?LinkId=180893)


## <a name="how-volume-shadow-copy-service-works"></a>Funktionsweise des Volumeschattenkopie-Diensts

Für eine vollständige VSS-Lösung sind alle der folgenden grundlegenden Komponenten erforderlich:

**VSS-Dienst**   Teil des Windows-Betriebssystems, mit dem sichergestellt wird, dass die anderen Komponenten ordnungsgemäß miteinander kommunizieren und zusammenarbeiten können.

**VSS-Anforderer**   Die Software, die die tatsächliche Erstellung von Schattenkopien anfordert (oder anderen übergeordneten Vorgängen wie deren Import oder Löschung). In der Regel handelt es sich hierbei um die Sicherungsanwendung. Das Hilfsprogramm Windows Server Backup und die Anwendung System Center Data Protection Manager sind VSS-Anforderer. Zu VSS-Anforderer, die nicht von Microsoft® stammen, gehören fast alle Sicherungssoftware-Anwendungen, die unter Windows ausgeführt werden.

**VSS Writer**   Die Komponente, die garantiert, dass ein konsistentes Dataset für die Sicherung vorhanden ist. Dies wird in der Regel als Teil einer Branchenanwendung bereitgestellt (z. B. SQL Server® oder Exchange Server). VSS Writer für verschiedene Windows-Komponenten, z. B. die Registrierung, sind im Windows-Betriebssystem enthalten. Nicht von Microsoft stammende VSS Writer sind in vielen Anwendungen für Windows enthalten, die die Datenkonsistenz während der Sicherung gewährleisten müssen.

**VSS-Anbieter**   Die Komponente, die die Schattenkopien erstellt und verwaltet. Dies kann in der Software oder in der Hardware geschehen. Das Windows-Betriebssystem enthält einen VSS-Provider, der Copy-on-Write (Kopie bei Schreibvorgang) verwendet. Wenn Sie ein Storage Area Network (SAN) verwenden, ist es wichtig, dass Sie den VSS-Hardwareanbieter für das SAN installieren, falls ein solcher vorhanden ist. Ein Hardwareanbieter entlastet das Hostbetriebssystem von der Aufgabe, eine Schattenkopie zu erstellen und zu verwalten.

Im folgenden Diagramm wird veranschaulicht, wie der VSS-Dienst Anforderer, Writer und Anbieter koordiniert, um eine Schattenkopie eines Volumes zu erstellen.

![Architekturdiagramm des Volumeschattenkopie-Diensts](media/volume-shadow-copy-service/Ee923636.94dfb91e-8fc9-47c6-abc6-b96077196741(WS.10).jpg)

**Abbildung 1**   Architekturdiagramm des Volumeschattenkopie-Diensts

### <a name="how-a-shadow-copy-is-created"></a>Erstellen einer Schattenkopie

Dieser Abschnitt setzt die verschiedenen Rollen von Anforderer, Writer und Anbieter in einen Kontext, indem die Schritte aufgelistet werden, die zum Erstellen einer Schattenkopie ausgeführt werden müssen. Das folgende Diagramm zeigt, wie der Volumeschattenkopie-Dienst die Gesamtkoordination von Anforderer, Writer und des Anbieter steuert.

![Diagramm der Funktionsweise des Volumeschattenkopie-Diensts](media/volume-shadow-copy-service/Ee923636.1c481a14-d6bc-4796-a3ff-8c6e2174749b(WS.10).jpg)

**Abbildung 2**Erstellungsvorgang für Schattenkopie

Zum Erstellen einer Schattenkopie führen Anforderer, Writer und Anbieter die folgenden Aktionen aus:

1.  Der Anforderer fordert den Volumeschattenkopie-Dienst zur Enumeration der Writer, zum Sammeln der Writer-Metadaten und zur Vorbereitung der Schattenkopieerstellung auf.

2.  Jeder Writer erstellt eine XML-Beschreibung der Komponenten und Datenspeicher, die gesichert werden müssen, und stellt sie dem Volumeschattenkopie-Dienst zur Verfügung. Der Writer definiert außerdem eine Wiederherstellungsmethode, die für alle Komponenten verwendet wird. Der Volumeschattenkopie-Dienst stellt dem Anforderer die Beschreibung des Writers zur Verfügung, der die zu sichernden Komponenten auswählt.

3.  Der Volumeschattenkopie-Dienst benachrichtigt alle Writer, Ihre Daten für die Erstellung einer Schattenkopie vorzubereiten.

4.  Jeder Writer bereitet die Daten entsprechend vor, wie z. B. durch Abschließen aller geöffneten Transaktionen, Ausführen von Transaktionsprotokollen und Leeren von Caches. Wenn die Daten zum Speichern in der Schattenkopie bereit sind, benachrichtigt der Writer den Volumeschattenkopie-Dienst.

5.  Der Volumeschattenkopie-Dienst weist die Writer an, die Schreib-E/A-Anforderungen von Anwendungen vorübergehend einzufrieren (Lese-E/A-Anforderungen sind immer noch möglich), und zwar für die wenigen Sekunden, die zum Erstellen der Schattenkopie des oder der Volumes benötigt werden. Das Einfrieren der Anwendung darf nicht länger als 60 Sekunden dauern. Der Volumeschattenkopie-Dienst leert die Dateisystempuffer und friert dann das Dateisystem ein, wodurch sichergestellt wird, dass die Metadaten des Dateisystems ordnungsgemäß aufgezeichnet werden und die in der Schattenkopie gesicherten Daten in einer konsistenten Reihenfolge geschrieben werden.

6.  Der Volumeschattenkopie-Dienst weist den Anbieter an, die Schattenkopie zu erstellen. Die Erstellung der Schattenkopie dauert höchstens 10 Sekunden, während der alle Schreib-E/A-Anforderungen an das Dateisystem eingefroren bleiben.

7.  Im Volumeschattenkopie-Dienst gibt Schreib-E/A-Anforderungen des Dateisystems frei.

8.  VSS weist die Writer an, Schreib-E/A-Anforderungen von Anwendungen zu entsperren. An diesem Punkt können Anwendungen das Schreiben von Daten auf den in der Schattenkopie gesicherten Datenträger fortsetzen.


> [!NOTE]
> Die Erstellung von Schattenkopien kann abgebrochen werden, wenn sich die Writer länger als 60 Sekunden im eingefrorenen Zustand befinden oder wenn die Anbieter länger als 10 Sekunden zum Ausführen eines Commit für die Schattenkopie benötigen.
<br>

9. Der Anforderer kann den Prozess wiederholen (wechseln Sie zurück zu Schritt 1), oder den Administrator benachrichtigen, dass der Vorgang zu einem späteren Zeitpunkt wiederholt werden soll.

10. Wenn die Schattenkopie erfolgreich erstellt wurde, gibt der Volumeschattenkopie-Dienst die Speicherortinformationen für die Schattenkopie an den Anforderer zurück. In einigen Fällen kann die Schattenkopie vorübergehend als Volume mit Lese-/Schreibzugriff zur Verfügung gestellt werden, damit VSS und eine oder mehrere Anwendungen den Inhalt der Schattenkopie ändern können, bevor die Erstellung der Schattenkopie abgeschlossen ist. Nachdem VSS und die Anwendungen ihre Änderungen vorgenommen haben, wird die Schattenkopie schreibgeschützt. Diese Phase wird als automatische Wiederherstellung bezeichnet und verwendet, um alle Dateisystem- oder Anwendungstransaktionen auf dem Schattenkopievolume rückgängig zu machen, die vor dem Erstellen der Schattenkopie nicht abgeschlossen wurden.


### <a name="how-the-provider-creates-a-shadow-copy"></a>Erstellen der Schattenkopie durch den Anbieter

Ein Hardware- oder Softwareanbieter von Schattenkopien verwendet zum Erstellen einer Schattenkopie eine der folgenden Methoden:

**Vollständige Kopie**   Bei dieser Methode wird eine vollständige Kopie (als „Vollversion“ oder „Klon“ bezeichnet) des ursprünglichen Volumes zu einem bestimmten Zeitpunkt erstellt. Die Kopie ist schreibgeschützt.

**Kopie bei Schreibvorgang**   Bei dieser Methode wird das ursprüngliche Volume nicht kopiert. Stattdessen wird eine differenzielle Kopie erstellt, indem alle Änderungen (abgeschlossene Schreib-E/A-Anforderungen) kopiert werden, die nach einem bestimmten Zeitpunkt auf dem Volume vorgenommen werden.

**Umleitung bei Schreibvorgang**   Bei dieser Methode wird das ursprüngliche Volume nicht kopiert, und es werden keine Änderungen am ursprünglichen Volume nach einem bestimmten Zeitpunkt durchgeführt. Stattdessen wird eine differenzielle Kopie erstellt, indem alle Änderungen an ein anderes Volume umgeleitet werden.

## <a name="complete-copy"></a>Vollständige Kopie

Eine vollständige Kopie wird in der Regel durch Erstellung eines „Teilspiegels“ wie folgt erstellt:

1. Das ursprüngliche Volume und das Schattenkopievolume sind ein gespiegelter Volumesatz.

2. Das Schattenkopievolume ist vom ursprünglichen Volume getrennt. Dadurch wird die Spiegelverbindung getrennt.


Nachdem die Spiegelverbindung getrennt wurde, sind das ursprüngliche Volume und das Schattenkopievolume voneinander unabhängig. Das ursprüngliche Volume akzeptiert weiterhin alle Änderungen (Schreib-E/A-Anforderungen), während das Schattenkopievolume eine genaue schreibgeschützte Kopie der ursprünglichen Daten zum Zeitpunkt der Trennung bleibt.

### <a name="copy-on-write-method"></a>Methode „Kopie bei Schreibvorgang“

Wenn bei der Methode „Kopie bei Schreibvorgang“ eine Änderung am ursprünglichen Volume stattfindet (aber bevor die Schreib-E/A-Anforderung abgeschlossen ist), wird jeder zu ändernde Block gelesen und dann in den Speicherbereich der Schattenkopie des Volumes geschrieben (auch als „Vergleichsbereich“ bezeichnet). Der Schattenkopie-Speicherbereich kann sich auf demselben Volume oder auf einem anderen Volume befinden. Dadurch wird eine Kopie des Datenblocks auf dem ursprünglichen Volume beibehalten, bevor die Änderung diese überschreibt.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Zeit</th>
<th>Quelldaten (Status und Daten)</th>
<th>Schattenkopie (Status und Daten)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>Originaldaten: 1 2 3 4 5</p></td>
<td><p>Keine Kopie: –</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>Geänderte Daten im Cache: 3 bis 3'</p></td>
<td><p>Erstellte Schattenkopie (nur Unterschiede): 3</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>Ursprüngliche Daten werden überschrieben: 1 2 3' 4 5</p></td>
<td><p>Unterschiede und Index werden in der Schattenkopie gespeichert: 3</p></td>
</tr>
</tbody>
</table>

**Tabelle 1**   Die Methode „Kopie bei Schreibvorgang“ zum Erstellen von Schattenkopien

Die Methode „Kopie bei Schreibvorgang“ ist eine schnelle Methode zum Erstellen einer Schattenkopie, da nur geänderte Daten kopiert werden. Die kopierten Blöcke im Vergleichsbereich können mit den geänderten Daten auf dem ursprünglichen Volume kombiniert werden, um das Volume in dem Zustand wiederherzustellen, bevor Änderungen vorgenommen wurden. Wenn viele Änderungen vorhanden sind, kann die Methode „Kopie bei Schreibvorgang“ kostspielig werden.

### <a name="redirect-on-write-method"></a>Methode „Umleitung bei Schreibvorgang“

Bei der Methode „Umleitung bei Schreibvorgang“ werden Änderungen, die das ursprüngliche Volume empfängt (Schreib-E/A-Anforderung), nicht auf das ursprüngliche Volume angewendet. Stattdessen wird die Änderung in den Schattenkopie-Speicherbereich eines anderen Volumes geschrieben.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Zeit</th>
<th>Quelldaten (Status und Daten)</th>
<th>Schattenkopie (Status und Daten)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>Originaldaten: 1 2 3 4 5</p></td>
<td><p>Keine Kopie: –</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>Geänderte Daten im Cache: 3 bis 3'</p></td>
<td><p>Erstellte Schattenkopie (nur Unterschiede): 3'</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>Die ursprünglichen Daten bleiben unverändert: 1 2 3 4 5</p></td>
<td><p>Unterschiede und Index werden in der Schattenkopie gespeichert: 3'</p></td>
</tr>
</tbody>
</table>

**Tabelle 2**   Die Methode „Umleitung bei Schreibvorgang“ zum Erstellen von Schattenkopien

Wie die Methode „Kopie bei Schreibvorgang“ stellt auch die Methode „Umleitung bei Schreibvorgang“ eine schnelle Methode zum Erstellen einer Schattenkopie dar, da nur Änderungen an den Daten kopiert werden. Die kopierten Blöcke im Vergleichsbereich können mit den unveränderten Daten auf dem ursprünglichen Volume zu einer kompletten, aktuellem Kopie der Daten kombiniert werden. Wenn viele Lese-E/A-Anforderungen vorliegen, kann die Methode „Umleitung bei Schreibvorgang“ kostspielig werden.

## <a name="shadow-copy-providers"></a>Schattenkopieanbieter

Es gibt zwei Arten von Schattenkopieanbietern: hardwarebasierte Anbieter und softwarebasierte Anbieter. Es gibt auch einen Systemanbieter, bei dem es sich um einen in das Windows-Betriebssystem integrierten Softwareanbieter handelt.

### <a name="hardware-based-providers"></a>Hardwarebasierte Anbieter

Hardwarebasierte Schattenkopieanbieter fungieren als Schnittstelle zwischen dem Volumeschattenkopie-Dienst und der Hardwareebene, indem sie in Verbindung mit einem Hardwarespeicheradapter oder Controller verwendet werden. Das Erstellen und Verwalten der Schattenkopie wird vom Speicherarray durchgeführt.

Hardwareanbieter übernehmen immer die Schattenkopie einer ganzen LUN, aber der Volumeschattenkopie-Dienst macht nur die Schattenkopie des oder der angeforderten Volumes verfügbar.

Ein hardwarebasierter Schattenkopieanbieter nutzt die Funktionen des Volumeschattenkopie-Diensts, die den Zeitpunkt definieren, die Datensynchronisierung ermöglichen, die Schattenkopie verwalten und eine gemeinsame Schnittstelle mit Sicherungsanwendungen bereitstellen. Der Volumeschattenkopie-Dienst gibt jedoch nicht den zugrunde liegenden Mechanismus an, mit dem der hardwarebasierte Anbieter Schattenkopien erstellt und verwaltet.

### <a name="software-based-providers"></a>Softwarebasierte Anbieter

Softwarebasierte Schattenkopieanbieter fangen typischerweise Lese- und Schreib-E/A-Anforderungen in einer Softwareschicht zwischen dem Dateisystem und der Volume Manager-Software ab und verarbeiten Sie.

Diese Anbieter werden als DLL-Komponente im Benutzermodus und mindestens einem Gerätetreiber im Kernelmodus, in der Regel einem Speicherfiltertreiber implementiert. Im Gegensatz zu hardwarebasierten Anbietern erstellen softwarebasierte Anbieter Schatten Kopien auf Softwareebene, nicht auf der Hardwareebene.

Ein softwarebasierter Schattenkopieanbieter muss eine Zeitpunktansicht eines Volumes verwalten, indem er Zugriff auf ein Dataset hat, das verwendet werden kann, um den Volumestatus vor dem Zeitpunkt der Schattenkopieerstellung neu zu erstellen. Ein Beispiel hierfür ist die „Kopie bei Schreibvorgang“-Technik des Systemanbieters. Allerdings gelten für den Volumeschattenkopie-Dienst keine Einschränkungen hinsichtlich der Technik, mit der die softwarebasierten Anbieter Schattenkopien erstellen und verwalten.

Ein Softwareanbieter gilt für eine größere Anzahl von Speicherplattformen als ein hardwarebasierten Anbieter und sollte auch mit Basisdatenträgern oder logischen Volumes gleich gut funktionieren. (Ein logisches Volume ist ein Volume, das durch Kombinieren des freie Speicherplatzes von zwei oder mehr Datenträgern erstellt wird.) Im Gegensatz zu Hardwareschattenkopien verbrauchen Softwareanbieter Betriebssystemressourcen, um die Schattenkopie zu verwalten.

Weitere Informationen zu Basisdatenträgern finden Sie unter [Was sind Basisdatenträger und Volumes?](https://go.microsoft.com/fwlink/?linkid=180894) (https://go.microsoft.com/fwlink/?LinkId=180894) auf TechNet.

### <a name="system-provider"></a>Systemanbieter

Im Windows-Betriebssystem wird ein Schattenkopieanbieter, der Systemanbieter, bereitgestellt. Obwohl in Windows ein Standardanbieter bereitgestellt wird, steht es anderen Anbietern frei, Implementierungen bereitzustellen, die für ihre Speicherhardware und Softwareanwendungen optimiert sind.

Um die Zeitpunktansicht eines in einer Schattenkopie enthaltenen Volumes zu verwalten, verwendet der Systemanbieter eine „Kopie bei Schreibvorgang“-Methode. Kopien der Blöcke auf dem Volume, die seit dem Beginn der Erstellung der Schattenkopie geändert wurden, werden in einem Schattenkopie-Speicherbereich gespeichert.

Der Systemanbieter kann das Produktionsvolume verfügbar machen, in das normal geschrieben und das gelesen werden kann. Wird die Schattenkopie benötigt, werden die Unterschiede logisch auf die Daten auf dem Produktionsvolume angewendet, um die gesamte Schattenkopie verfügbar zu machen.

Für den Systemanbieter muss sich der Schattenkopie-Speicherbereich auf einem NTFS-Volume befinden. Das Volume, das als Schatten gesichert werden soll, muss kein NTFS-Volume sein, aber mindestens ein auf dem System eingebundenes Volume muss ein NTFS-Volume sein.

Die Komponentendateien, aus denen der Systemanbieter besteht, sind „swprv.dll“ und „volsnap.sys“.

### <a name="in-box-vss-writers"></a>In-Box-VSS-Writer

Das Windows-Betriebssystem enthält eine Reihe von VSS-Writern, die für das Auflisten der Daten verantwortlich sind, die für die verschiedenen Windows-Features erforderlich sind.

Weitere Informationen zu diesen Writern erhältst du auf der folgenden Webseite der Microsoft-Dokumentation:

- [In-Box-VSS-Writer](/windows/win32/vss/in-box-vss-writers) (https://docs.microsoft.com/windows/win32/vss/in-box-vss-writers)


## <a name="how-shadow-copies-are-used"></a>Verwendung von Schattenkopien

Neben der Sicherung von Anwendungsdaten und Systemstatusinformationen können Schattenkopien für eine Reihe von Zwecken verwendet werden, u. a. für die folgenden:

  - Wiederherstellen von LUNs (LUN-Neusynchronisierung und LUN-Austausch)

  - Wiederherstellen einzelner Dateien (Schattenkopien für freigegebene Ordner)

  - Data Mining mithilfe von übertragbaren Schattenkopien


### <a name="restoring-luns-lun-resynchronization-and-lun-swapping"></a>Wiederherstellen von LUNs (LUN-Neusynchronisierung und LUN-Austausch)

In Windows Server 2008 R2 und Windows 7 können VSS-Anforderer ein Hardwareschattenkopie-Anbieter-Feature namens LUN-Neusynchronisierung (oder LUN-Neusynchronisierung) verwenden. Dies ist ein schnelles Wiederherstellungsschema, das einem Anwendungsadministrator ermöglicht, Daten aus einer Schattenkopie in der ursprünglichen LUN oder einer neuen LUN wiederherzustellen.

Bei der Schattenkopie kann es sich um einen vollständigen Klon oder eine differenzielle Schattenkopie handeln. In beiden Fällen hat die Ziel-LUN am Ende der erneuten Synchronisierung denselben Inhalt wie die Schattenkopie-LUN. Während der erneuten Synchronisierung erstellt das Array eine Kopie auf Blockebene aus der Schattenkopie in die Ziel-LUN.


> [!NOTE]
> Die Schattenkopie muss eine übertragbare Hardwareschattenkopie sein.
<br>


Die meisten Arrays erlauben, dass Produktions-E/A-Vorgänge kurz nach Beginn der Neusynchronisierung fortgesetzt werden. Während der Neusynchronisierung werden Leseanforderungen an die Schattenkopie-LUN und Schreibanforderungen an die Ziel-LUN umgeleitet. Dadurch können Arrays sehr große Datasets wiederherstellen und den normalen Betrieb in wenigen Sekunden fortsetzen.

Die LUN-Neusynchronisierung unterscheidet sich vom LUN-Austausch. Ein LUN-Austausch ist ein schnelles Wiederherstellungsszenario, das von VSS seit Windows Server 2003 SP1 unterstützt wird. Bei einem LUN-Austausch wird die Schattenkopie importiert und anschließend in ein Volume mit Lese-/Schreibzugriff konvertiert. Die Konvertierung kann nicht rückgängig gemacht werden, und das Volume sowie die zugrunde liegende LUN können danach nicht mit den VSS-APIs gesteuert werden. Die folgende Liste ist eine Gegenüberstellung von LUN-Neusynchronisierung und LUN-Austausch:

  - Bei der LUN-Neusynchronisierung wird die Schattenkopie nicht geändert, sodass sie mehrmals verwendet werden kann. Beim LUN-Austausch kann die Schattenkopie nur einmal für eine Wiederherstellung verwendet werden. Für die meisten sicherheitsbewussten Administratoren ist dies wichtig. Wird die LUN-Neusynchronisierung verwendet, kann der Anforderer den gesamten Wiederherstellungsvorgang wiederholen, wenn beim ersten Mal etwas schief geht.

  - Am Ende eines LUN-Austauschs wird die Schattenkopie-LUN für Produktions-E/A-Anforderungen verwendet. Aus diesem Grund muss die Schattenkopie-LUN dieselbe Speicherqualität wie die ursprüngliche Produktions-LUN aufweisen, um sicherzustellen, dass die Leistung nach dem Wiederherstellungsvorgang nicht beeinträchtigt wird. Wird stattdessen die LUN-Neusynchronisierung verwendet, kann der Hardwareanbieter die Schattenkopie in Speicher aufbewahren, der kostengünstiger ist als Speicher in Produktionsqualität.

  - Wenn die Ziel-LUN unbrauchbar ist und neu erstellt werden muss, ist der LUN-Austausch möglicherweise wirtschaftlicher, da er keine Ziel-LUN erfordert.


> [!WARNING]
> Alle aufgeführten Vorgänge sind Vorgänge auf LUN-Ebene. Wenn Sie versuchen, ein bestimmtes Volume mithilfe der LUN-Neusynchronisierung wiederherzustellen, werden alle anderen Volumes, die die LUN gemeinsam nutzen, ebenfalls zurückgesetzt.
<br>


### <a name="restoring-individual-files-shadow-copies-for-shared-folders"></a>Wiederherstellen einzelner Dateien (Schattenkopien für freigegebene Ordner)

Schattenkopien für freigegebene Ordner verwenden den Volumeschattenkopie-Dienst, um Zeitpunktkopien von Dateien bereitzustellen, die sich auf einer freigegebenen Netzwerkressource befinden, z. B. auf einem Dateiserver. Mit Schattenkopien für freigegebene Ordner können Benutzer gelöschte oder geänderte Dateien, die im Netzwerk gespeichert sind, schnell wiederherstellen. Da dies ohne Unterstützung eines Administrators möglich ist, können Schattenkopien für freigegebene Ordner die Produktivität steigern und die Verwaltungskosten senken.

Weitere Informationen zu Schattenkopien für freigegebene Ordner finden Sie unter [Schattenkopien für freigegebene Ordner](https://go.microsoft.com/fwlink/?linkid=180898) (https://go.microsoft.com/fwlink/?LinkId=180898) auf TechNet.

### <a name="data-mining-by-using-transportable-shadow-copies"></a>Data Mining mithilfe von übertragbaren Schattenkopien

Mithilfe eines Hardwareanbieters, der für die Verwendung mit dem Volumeschattenkopie-Dienst konzipiert ist, können Sie übertragbare Schattenkopien erstellen, die auf Server innerhalb desselben Subsystems (z. B. ein SAN) importiert werden können. Diese Schattenkopien können für das Seeding einer Produktions- oder Testinstallation mit schreibgeschützten Daten für Data Mining verwendet werden.

Wenn der Volumeschattenkopie-Dienst und ein Speicherarray mit einem Hardwareanbieter für die Verwendung mit dem Volumeschattenkopie-Dienst entworfen wurden, ist es möglich, eine Schattenkopie des Quelldatenvolumens auf einem Server zu erstellen und die Schattenkopie dann auf einen anderen Server (oder zurück auf den gleichen Server) zu importieren. Dieser Prozess wird in wenigen Minuten ausgeführt, unabhängig von der Größe der Daten. Der Übertragungsvorgang umfasst eine Reihe von Schritten, bei denen ein Schattenkopieanforderer (eine Speicherverwaltungsanwendung) verwendet wird, der übertragbare Schattenkopien unterstützt.

## <a name="to-transport-a-shadow-copy"></a>So übertragen Sie eine Schattenkopie

1.  Erstellen Sie eine übertragbare Schattenkopie der Quelldaten auf einem Server.

2.  Importieren Sie die Schattenkopie auf einen Server, der mit dem SAN verbunden ist (Sie können die Schattenkopie auf einen anderen Server oder auf denselben Server importieren).

3.  Die Daten können jetzt verwendet werden.

![Diagramm des Transports einer Schattenkopie zwischen zwei Servern](media/volume-shadow-copy-service/Ee923636.633752e0-92f6-49a7-9348-f451b1dc0ed7(WS.10).jpg)

**Abbildung 3**   Erstellen von Schattenkopien und Übertragung zwischen zwei Servern


> [!NOTE]
> Eine unter Windows Server 2003 erstellte übertragbare Schattenkopie kann nicht auf einen Server importiert werden, auf dem Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird. Eine unter Windows Server 2008 oder Windows Server 2008 R2 erstellte übertragbare Schattenkopie kann nicht auf einen Server importiert werden, auf dem Windows Server 2003 ausgeführt wird. Eine unter Windows Server 2008 erstellte Schattenkopie kann jedoch auf einen Server importiert werden, auf dem Windows Server 2008 R2 ausgeführt wird, und umgekehrt.
<br>


Schattenkopien sind schreibgeschützt. Wenn Sie eine Schattenkopie in eine Lese-/Schreib-LUN konvertieren möchten, können Sie zusätzlich zum Volumeschattenkopie-Dienst eine VDS-basierte Speicherverwaltungsanwendung (einschließlich bestimmter Anforderer) verwenden. Mithilfe dieser Anwendung können Sie die Schattenkopie aus der Volumeschattenkopie-Dienstverwaltung entfernen und in eine Lese-/Schreib-LUN konvertieren.

Die Volumeschattenkopie-Dienstübertragung ist eine erweiterte Lösung auf Computern, auf denen Windows Server 2003 Enterprise Edition, Windows Server 2003 Datacenter Edition, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird. Dies funktioniert nur, wenn auf dem Speicherarray ein Hardwareanbieter vorhanden ist. Die Schattenkopieübertragung kann für verschiedene Zwecke verwendet werden, beispielsweise Bandsicherungen, Data Mining und Tests.

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

Hier werden häufig gestellte Fragen zum Volumeschattenkopie-Dienst (VSS) für Systemadministratoren beantwortet. Weitere Informationen zu Programmierschnittstellen für VSS-Anwendungen finden Sie unter [Volumeschattenkopie-Dienst](https://go.microsoft.com/fwlink/?linkid=180899) (https://go.microsoft.com/fwlink/?LinkId=180899) in der Windows Developer Center-Bibliothek.

### <a name="when-was-volume-shadow-copy-service-introduced-on-which-windows-operating-system-versions-is-it-available"></a>Wann wurde der Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) eingeführt? In welchen Windows-Betriebssystemversionen ist er verfügbar?

VSS wurde in Windows XP eingeführt. Er ist unter Windows XP, Windows Server 2003, Windows Vista®, Windows Server 2008, Windows 7 und Windows Server 2008 R2 verfügbar.

### <a name="what-is-the-difference-between-a-shadow-copy-and-a-backup"></a>Was ist der Unterschied zwischen einer Schattenkopie und einer Sicherung?

Bei einer Sicherung eines Festplattenlaufwerks ist die erstellte Schattenkopie gleichzeitig die Sicherung. Daten können aus der Schattenkopie für eine Wiederherstellung kopiert werden, oder die Schattenkopie kann für ein schnelles Wiederherstellungsszenario verwendet werden, z. B. LUN-Neusynchronisierung oder LUN-Austausch.

Wenn Daten aus der Schattenkopie auf Band oder ein anderes Wechselmedium kopiert werden, stellt der auf dem Medium gespeicherte Inhalt die Sicherung dar. Die Schattenkopie selbst kann gelöscht werden, nachdem die Daten aus ihr kopiert wurden.

### <a name="what-is-the-largest-size-volume-that-volume-shadow-copy-service-supports"></a>Welche Volumegröße unterstützt der Volumeschattenkopie-Dienst maximal?

Der Volumeschattenkopie-Dienst unterstützt eine Volumegröße von bis zu 64 TB.

### <a name="i-made-a-backup-on-windows-server2008-can-i-restore-it-on-windows-server2008r2"></a>Ich habe eine Sicherung unter Windows Server 2008 erstellt. Kann ich sie unter Windows Server 2008 R2 wiederherstellen?

Dies hängt von der verwendeten Sicherungssoftware ab. Die meisten Sicherungsprogramme unterstützen dieses Szenario für Daten, aber nicht für Sicherungen des Systemstatus.

Schattenkopien, die für eine dieser Versionen von Windows erstellt werden, können für die andere verwendet werden.

### <a name="i-made-a-backup-on-windows-server2003-can-i-restore-it-on-windows-server2008"></a>Ich habe eine Sicherung unter Windows Server 2003 erstellt. Kann ich sie unter Windows Server 2008 wiederherstellen?

Dies hängt von der verwendeten Sicherungssoftware ab. Wenn Sie eine Schattenkopie unter Windows Server 2003 erstellt haben, können Sie sie nicht unter Windows Server 2008 verwenden. Gleiches gilt umgekehrt: Wenn Sie eine Schattenkopie unter Windows Server 2008 erstellt haben, können Sie sie nicht unter Windows Server 2003 wiederherstellen.

### <a name="how-can-i-disable-vss"></a>Wie kann ich VSS deaktivieren?

Der Volumeschattenkopie-Dienst kann mithilfe der Microsoft Management Console deaktiviert werden. Dies empfiehlt sich jedoch nicht. Das Deaktivieren von VSS wirkt sich negativ auf sämtliche von Ihnen verwendeten Software aus, z. B. Systemwiederherstellung und Windows Server Backup.

Weitere Informationen finden Sie auf der Microsoft TechNet-Website:

- [Systemwiederherstellung](https://go.microsoft.com/fwlink/?linkid=157113) (https://go.microsoft.com/fwlink/?LinkID=157113)

- [Windows Server Backup](https://go.microsoft.com/fwlink/?linkid=180891) (https://go.microsoft.com/fwlink/?LinkID=180891)


### <a name="can-i-exclude-files-from-a-shadow-copy-to-save-space"></a>Kann ich Dateien aus einer Schattenkopie ausschließen, um Speicherplatz zu sparen?

VSS dient zum Erstellen von Schattenkopien ganzer Volumes. Temporäre Dateien, z. B. Auslagerungsdateien, werden bei Schattenkopien automatisch weggelassen, um Speicherplatz zu sparen.

Zum Ausschließen bestimmter Dateien aus Schattenkopien wird der folgende Registrierungsschlüssel verwendet: **FilesNotToSnapshot**.


> [!NOTE]
> Der Registrierungsschlüssel <STRONG>FilesNotToSnapshot</STRONG> sollte nur von Anwendungen verwendet werden. Benutzer, die versuchen, den Registrierungsschlüssel zu verwenden, erhalten Einschränkungen wie die folgenden:
> <br>
> <UL>
> <LI>Es können keine Dateien aus einer Schattenkopie gelöscht werden, die unter Windows Server mit dem Feature „Vorherige Versionen“ erstellt wurden.<BR><BR>
> <LI>Es können keine Dateien aus Schattenkopien für freigegebene Ordner gelöscht werden.<BR><BR>
> <LI>Dateien aus Schattenkopien, die mit dem Hilfsprogramm <a href="/windows-server/administration/windows-commands/diskshadow" data-raw-source="[Diskshadow](../../administration/windows-commands/diskshadow.md)">Diskshadow</a> erstellt wurden, können gelöscht werden, aber Dateien aus Schattenkopien, die mit dem Hilfsprogramm <a href="/windows-server/administration/windows-commands/vssadmin" data-raw-source="[Vssadmin](../../administration/windows-commands/vssadmin.md)">Vssadmin</a> erstellt wurden, können nicht gelöscht werden.<BR><BR>
> <LI>Dateien werden auf Grundlage der besten Leistung aus einer Schattenkopie gelöscht. Das bedeutet, dass Sie nicht unbedingt gelöscht werden.<BR><BR></LI></UL>


Weitere Informationen finden Sie unter [Ausschließen von Dateien aus Schattenkopien](https://go.microsoft.com/fwlink/?linkid=180904) (https://go.microsoft.com/fwlink/?LinkId=180904) auf MSDN.

### <a name="my-non-microsoft-backup-program-failed-with-a-vss-error-what-can-i-do"></a>Bei meinem nicht von Microsoft stammenden Sicherungsprogramm ist ein VSS-Fehler aufgetreten. Was kann ich tun?

Suchen Sie den Abschnitt zum Produktsupport auf der Website des Unternehmens, von dem das Sicherungsprogramm erstellt wurde. Möglicherweise gibt es ein Produktupdate, das Sie herunterladen und installieren können, um das Problem zu beheben. Falls nicht, wenden Sie sich an die Produktsupportabteilung des Unternehmens.

Systemadministratoren können Informationen zur Problembehandlung bei VSS auf der folgenden Website der Microsoft TechNet-Bibliothek verwenden, um Diagnoseinformationen zu VSS-bezogenen Problemen zu sammeln.

Weitere Informationen finden Sie unter [Volumeschattenkopie-Dienst](https://go.microsoft.com/fwlink/?linkid=180905) (https://go.microsoft.com/fwlink/?LinkId=180905) auf TechNet.

### <a name="what-is-the-diff-area"></a>Was ist der „Vergleichsbereich“?

Der Schattenkopie-Speicherbereich (oder Vergleichsbereich) ist der Speicherort, an dem die Daten für die vom Systemsoftwareanbieter erstellte Schattenkopie gespeichert werden.

### <a name="where-is-the-diff-area-located"></a>Wo befindet sich der Vergleichsbereich?

Der Vergleichsbereich kann sich auf einem beliebigen lokalen Volume befinden. Er muss sich jedoch auf einem NTFS-Volume befinden, das über genügend Speicherplatz für die Schattenkopie verfügt.

### <a name="how-is-the-diff-area-location-determined"></a>Wie wird der Speicherort des Vergleichsbereichs festgelegt?

Die folgenden Kriterien werden in dieser Reihenfolge ausgewertet, um den Speicherort des Vergleichsbereichs zu bestimmen:

  - Wenn ein Volume bereits über eine vorhandene Schattenkopie verfügt, wird dieser Speicherort verwendet.

  - Wenn eine vorkonfigurierte manuelle Zuordnung zwischen dem ursprünglichen Volume und dem Speicherort des Schattenkopievolumes vorhanden ist, wird dieser Speicherort verwendet.

  - Wenn die beiden vorherigen Kriterien keinen Speicherort angeben, wählt der Schattenkopiedienst einen Speicherort basierend auf dem verfügbaren freien Speicherplatz aus. Wenn von mehreren Volumes Schattenkopien erstellt werden, erstellt der Schattenkopiedienst eine Liste möglicher Momentaufnahmen-Speicherorte basierend auf der Größe des freien Speicherplatzes, in absteigender Reihenfolge. Die Anzahl der bereitgestellten Speicherorte entspricht der Anzahl der Volumes, von denen Schattenkopien erstellt werden.

  - Wenn das Volume, von dem eine Schattenkopie erstellt wird, einer der möglichen Speicherorte ist, wird eine lokale Zuordnung erstellt. Andernfalls wird eine Zuordnung mit dem Volume erstellt, das den meisten verfügbaren Speicherplatz aufweist.


### <a name="can-vss-create-shadow-copies-of-non-ntfs-volumes"></a>Kann VSS Schattenkopien von Nicht-NTFS-Volumes erstellen?

Ja. Persistente Schattenkopien können jedoch nur für NTFS-Volumes erstellt werden. Außerdem muss mindestens ein auf dem System eingebundenes Volume ein NTFS-Volume sein.

### <a name="whats-the-maximum-number-of-shadow-copies-i-can-create-at-one-time"></a>Wie viele Schattenkopien kann ich maximal gleichzeitig erstellen?

Maximal können von 64 Volumes Schattenkopien in einem einzigen Schattenkopiesatz erstellt werden. Beachten Sie, dass dies nicht dasselbe wie die Anzahl der Schattenkopien ist.

### <a name="whats-the-maximum-number-of-software-shadow-copies-created-by-the-system-provider-that-i-can-maintain-for-a-volume"></a>Wie viele vom Systemanbieter erstellte Softwareschattenkopien kann ich maximal für ein Volume verwalten?

Der Wert für die maximale Anzahl von Softwareschattenkopien beträgt 512. Standardmäßig können Sie jedoch nur 64 Schattenkopien verwalten, die vom Feature „Schattenkopien von freigegebenen Ordnern“ verwendet werden. Verwenden Sie den folgenden Registrierungsschlüssel, um den Grenzwert für das Feature „Schattenkopien von freigegebenen Ordnern“ zu ändern: **MaxShadowCopies**.

### <a name="how-can-i-control-the-space-that-is-used-for-shadow-copy-storage-space"></a>Wie kann ich den Speicherplatz steuern, der für Schattenkopien verwendet wird?

Geben Sie den Befehl **vssadmin resize shadowstorage** ein.

Weitere Informationen finden Sie unter [Vssadmin resize shadowstorage](https://go.microsoft.com/fwlink/?linkid=180906) (https://go.microsoft.com/fwlink/?LinkId=180906) auf TechNet.

### <a name="what-happens-when-i-run-out-of-space"></a>Was geschieht, wenn kein Speicherplatz mehr verfügbar ist?

Schattenkopien für das Volume werden gelöscht, beginnend mit der ältesten Schattenkopie.

## <a name="volume-shadow-copy-service-tools"></a>Tools des Volumeschattenkopie-Diensts

Das Windows-Betriebssystem stellt die folgenden Tools zum Arbeiten mit VSS bereit:

  - [DiskShadow](https://go.microsoft.com/fwlink/?linkid=180907) (https://go.microsoft.com/fwlink/?LinkId=180907)

  - [VssAdmin](https://go.microsoft.com/fwlink/?linkid=84008) (https://go.microsoft.com/fwlink/?LinkId=84008)


### <a name="diskshadow"></a>DiskShadow

DiskShadow ist ein VSS-Anforderer, mit dem Sie alle auf einem System vorhandenen Hardware- und Softwaremomentaufnahmen verwalten können. DiskShadow umfasst Befehle wie die folgenden:

  - **list**: Listet VSS-Writer, VSS-Anbieter und Schattenkopien auf.

  - **create**: Erstellt eine neue Schattenkopie.

  - **import**: Importiert eine übertragbare Schattenkopie.

  - **expose**: Macht eine persistente Schattenkopie verfügbar (z. B. als in Form eines Laufwerkbuchstaben).

  - **revert**: Setzt ein Volume auf eine angegebene Schattenkopie zurück.


Dieses Tool ist für die Verwendung durch IT-Experten bestimmt, aber auch für Entwickler kann es beim Testen eines VSS-Writers oder VSS-Anbieters nützlich sein.

DiskShadow ist nur auf Windows Server-Betriebssystemen verfügbar. Auf Windows-Clientbetriebssystemen ist es nicht verfügbar.

### <a name="vssadmin"></a>VssAdmin

VssAdmin dient zum Erstellen, Löschen und Auflisten von Informationen zu Schattenkopien. Es kann auch verwendet werden, um die Größe des Schattenkopie-Speicherbereichs („Vergleichsbereich“) zu ändern.

VssAdmin umfasst Befehle wie die folgenden:

  - **create shadow**: Erstellt eine neue Schattenkopie.

  - **delete shadows**: Löscht Schattenkopien.

  - **list providers**: Listet alle registrierten VSS-Anbieter auf.

  - **list writers**: Listet alle abonnierten VSS-Writer auf.

  - **resize shadowstorage**: Ändert die maximale Größe des Schattenkopie-Speicherbereichs.


VssAdmin kann nur zum Verwalten von Schattenkopien verwendet werden, die vom Systemsoftwareanbieter erstellt wurden.

VssAdmin ist auf Windows-Client- und Windows Server-Betriebssystemversionen verfügbar.

## <a name="volume-shadow-copy-service-registry-keys"></a>Registrierungsschlüssel des Volumeschattenkopie-Diensts

Die folgenden Registrierungsschlüssel sind für die Verwendung mit VSS verfügbar:

  - **VssAccessControl**

  - **MaxShadowCopies**

  - **MinDiffAreaFileSize**


### <a name="vssaccesscontrol"></a>VssAccessControl

Dieser Schlüssel wird verwendet, um anzugeben, welche Benutzer Zugriff auf Schattenkopien haben.

Weitere Informationen finden Sie unter den folgenden Einträgen auf der MSDN-Website:

  - [Sicherheitsüberlegungen für Writer](https://go.microsoft.com/fwlink/?linkid=157739) (https://go.microsoft.com/fwlink/?LinkId=157739)

  - [Sicherheitsüberlegungen für Anforderer](https://go.microsoft.com/fwlink/?linkid=180908) (https://go.microsoft.com/fwlink/?LinkId=180908)


### <a name="maxshadowcopies"></a>MaxShadowCopies

Dieser Schlüssel gibt die maximale Anzahl von über den Client zugänglichen Schattenkopien an, die auf jedem Volume des Computers gespeichert werden können. Die über den Client zugänglichen Schattenkopien werden von Schattenkopien für freigegebene Ordner verwendet.

Weitere Informationen finden Sie unter dem folgenden Eintrag auf der MSDN-Website:

**MaxShadowCopies** unter [Registrierungsschlüssel für Sicherung und Wiederherstellung](https://go.microsoft.com/fwlink/?linkid=180909) (https://go.microsoft.com/fwlink/?LinkId=180909)

### <a name="mindiffareafilesize"></a>MinDiffAreaFileSize

Dieser Schlüssel gibt die minimale anfängliche Größe des Schattenkopie-Speicherbereichs in MB an.

Weitere Informationen finden Sie unter dem folgenden Eintrag auf der MSDN-Website:

**MinDiffAreaFileSize** unter [Registrierungsschlüssel für Sicherung und Wiederherstellung](https://go.microsoft.com/fwlink/?linkid=180910) (https://go.microsoft.com/fwlink/?LinkId=180910)

### <a name="supported-operating-system-versions"></a>Unterstützte Betriebssystemversionen

In der folgenden Tabelle sind die Mindestanforderungen für die unterstützten Clientbetriebssystem-Versionen für VSS-Features aufgeführt.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>VSS-Feature</th>
<th>Unterstützte Mindestversion (Client)</th>
<th>Unterstützte Mindestversion (Server)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LUN-Synchronisierung</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2008 R2</p></td>
</tr>
<tr class="even">
<td><p><strong>FilesNotToSnapshot</strong>-Registrierungsschlüssel</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td><p>Übertragbare Schattenkopien</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003 mit SP1</p></td>
</tr>
<tr class="even">
<td><p>Hardwareschattenkopien</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>Vorherige Versionen von Windows Server</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="even">
<td><p>Schnelle Wiederherstellung mit LUN-Austausch</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003 mit SP1</p></td>
</tr>
<tr class="odd">
<td><p>Mehrere Importe von Hardwareschattenkopien</p>
<div class="alert">
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Hinweis</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dies ist die Möglichkeit, eine Schattenkopie mehrmals zu importieren. Es kann jeweils ein Importvorgang gleichzeitig ausgeführt werden.
<p></p></td>
</tr>
</tbody>
</table>
<p></p>
</div></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>Schattenkopien für freigegebene Ordner</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>Übertragbare automatisch wiederhergestellte Schattenkopien</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>Gleichzeitige Sicherungssitzungen (bis zu 64)</p></td>
<td><p>Windows XP</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>Einzelne Wiederherstellungssitzung parallel zu Sicherungen</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003 mit SP2</p></td>
</tr>
<tr class="even">
<td><p>Bis zu 8 Wiederherstellungssitzungen parallel zu Sicherungen</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows Server 2003 R2</p></td>
</tr>
</tbody>
</table>

## <a name="additional-references"></a>Weitere Verweise

[Volumeschattenkopie-Dienst im Windows Developer Center](/windows/desktop/vss/volume-shadow-copy-service-overview)