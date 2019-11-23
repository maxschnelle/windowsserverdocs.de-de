---
title: Volumeschattenkopie-Dienst
ms.date: 01/30/2019
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 19e07504dad49c5e23cc49630015529e2a746aa7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394448"
---
# <a name="volume-shadow-copy-service"></a>Volumeschattenkopie-Dienst

Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2, Windows Server 2008, Windows 10, Windows 8.1, Windows 8, Windows 7

Das Sichern und Wiederherstellen wichtiger Geschäftsdaten kann aufgrund der folgenden Probleme sehr komplex sein:

  - Die Daten müssen in der Regel gesichert werden, während die Anwendungen, die die Daten liefern, noch ausgeführt werden. Dies bedeutet, dass einige der Datendateien offen sein können oder sich in einem inkonsistenten Zustand befinden.  
      
  - Wenn das DataSet groß ist, kann es schwierig sein, alle Daten gleichzeitig zu sichern.  
      

Das ordnungsgemäße Ausführen von Sicherungs-und Wiederherstellungs Vorgängen erfordert eine enge Koordination zwischen den Sicherungs Anwendungen, den Branchen Anwendungen, die gesichert werden, und der Speicher Verwaltungs Hardware und Software. Der Volumeschattenkopie-Dienst (VSS), der in Windows Server® 2003 eingeführt wurde, ermöglicht die Konversation zwischen diesen Komponenten, damit Sie besser zusammenarbeiten können. Wenn alle Komponenten VSS unterstützen, können Sie diese verwenden, um Ihre Anwendungsdaten zu sichern, ohne die Anwendungen offline zu schalten.

VSS koordiniert die Aktionen, die erforderlich sind, um eine konsistente Schatten Kopie (auch als Momentaufnahme oder eine Zeit Punkt Kopie bezeichnet) der zu sichernden Daten zu erstellen. Die Schatten Kopie kann unverändert verwendet werden, oder Sie kann in Szenarien wie den folgenden verwendet werden:

  - Sie möchten Anwendungsdaten und Systemstatus Informationen sichern, einschließlich der Archivierung von Daten auf einem anderen Festplattenlaufwerk, auf einem Band oder auf einem anderen Wechselmedium.  
      
  - Sie sind Data Mining.  
      
  - Sie führen Sicherungen von Datenträgern auf dem Datenträger aus.  
      
  - Sie müssen eine schnelle Wiederherstellung nach Datenverlust durchführen, indem Sie Daten auf der ursprünglichen LUN oder einer vollkommen neuen LUN wiederherstellen, die eine ursprüngliche LUN ersetzt, die fehlgeschlagen ist.  
      

Zu den Windows-Features und-Anwendungen, die VSS verwenden, gehören die folgenden:

  - [Windows Server-Sicherung](http://go.microsoft.com/fwlink/?linkid=180891) (http://go.microsoft.com/fwlink/?LinkId=180891)  
      
  - [Schatten Kopien von freigegebenen Ordnern](http://go.microsoft.com/fwlink/?linkid=142874) (http://go.microsoft.com/fwlink/?LinkId=142874)  
      
  - [System Center-Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=180892) (http://go.microsoft.com/fwlink/?LinkId=180892)  
      
  - [System Wiederherstellung](http://go.microsoft.com/fwlink/?linkid=180893) (http://go.microsoft.com/fwlink/?LinkId=180893)  
      

## <a name="how-volume-shadow-copy-service-works"></a>Funktionsweise von Volumeschattenkopie-Dienst

Für eine vollständige VSS-Lösung sind alle der folgenden grundlegenden Komponenten erforderlich:

Der **VSS-Dienst**   Teil des Windows-Betriebssystems, mit dem sichergestellt wird, dass die anderen Komponenten ordnungsgemäß miteinander kommunizieren können und zusammenarbeiten.

**VSS-Anforderer**   die Software, die die tatsächliche Erstellung von Schatten Kopien (oder andere allgemeine Vorgänge wie das Importieren oder löschen) anfordert. In der Regel handelt es sich hierbei um die Sicherungs Anwendung. Das Windows Server-Sicherung-Hilfsprogramm und die System Center Data Protection Manager-Anwendung sind VSS-Anforderer. Nicht-Microsoft-® VSS-Anforderer enthält fast alle Sicherungssoftware, die unter Windows ausgeführt wird.

**VSS Writer**   der Komponente, die garantiert, dass ein konsistentes Dataset für die Sicherungskopie vorhanden ist. Dies wird in der Regel als Teil einer Branchen Anwendung (z. b. SQL Server® oder Exchange Server) bereitgestellt. VSS-Writer für verschiedene Windows-Komponenten, z. b. die Registrierung, sind im Windows-Betriebssystem enthalten. Nicht von Microsoft stammenden VSS-Writer sind in vielen Anwendungen für Windows enthalten, die die Datenkonsistenz während der Sicherung gewährleisten müssen.

**VSS-Anbieter**   die Komponente, von der die Schatten Kopien erstellt und verwaltet werden. Dies kann in der Software oder der Hardware vorkommen. Das Windows-Betriebssystem enthält einen VSS-Anbieter, der Copy-on-Write-Vorgänge verwendet. Wenn Sie ein Storage Area Network (San) verwenden, ist es wichtig, dass Sie den VSS-Hardware Anbieter für das San installieren, sofern eine vorhanden ist. Ein Hardware Anbieter verlagert das Erstellen und Verwalten einer Schatten Kopie vom Host Betriebssystem.

Im folgenden Diagramm wird veranschaulicht, wie der VSS-Dienst mit Anforderern, Writern und Anbietern koordiniert, um eine Schatten Kopie eines Volumes zu erstellen.

![](media/volume-shadow-copy-service/Ee923636.94dfb91e-8fc9-47c6-abc6-b96077196741(WS.10).jpg)

**Abbildung 1**   Architektur Diagramm Volumeschattenkopie-Dienst

### <a name="how-a-shadow-copy-is-created"></a>Erstellen einer Schatten Kopie

In diesem Abschnitt werden die verschiedenen Rollen der Anforderer, des Writers und des Anbieters in den Kontext versetzt, indem die Schritte aufgelistet werden, die zum Erstellen einer Schatten Kopie ausgeführt werden müssen. Das folgende Diagramm zeigt, wie die-Volumeschattenkopie-Dienst die Gesamtkoordination der Anforderer, des Writers und des Anbieters steuert.

![](media/volume-shadow-copy-service/Ee923636.1c481a14-d6bc-4796-a3ff-8c6e2174749b(WS.10).jpg)

**Abbildung 2** Erstellungs Vorgang für Schatten Kopie

Zum Erstellen einer Schatten Kopie führen die Anforderer, der Writer und der Anbieter die folgenden Aktionen aus:

1.  Der Anforderer bittet den Volumeschattenkopie-Dienst, die Writer aufzulisten, die Writer-Metadaten zu sammeln und die Erstellung von Schatten Kopien vorzubereiten.  
      
2.  Jeder Writer erstellt eine XML-Beschreibung der Komponenten und Datenspeicher, die gesichert werden müssen, und stellt Sie für die Volumeschattenkopie-Dienst bereit. Der Writer definiert außerdem eine Restore-Methode, die für alle-Komponenten verwendet wird. Der Volumeschattenkopie-Dienst stellt der anfordernden Person die Beschreibung des Writers zur Verfügung, mit der die zu sichernden Komponenten ausgewählt werden.  
      
3.  Der Volumeschattenkopie-Dienst benachrichtigt alle Writer, Ihre Daten für die Erstellung einer Schatten Kopie vorzubereiten.  
      
4.  Jeder Writer bereitet die Daten entsprechend vor, wie z. b. das Abschließen aller geöffneten Transaktionen, das parallele Ausführen von Transaktions Protokollen und das Leeren von Caches. Wenn die Daten für die Schatten Kopie bereit sind, benachrichtigt der Writer die Volumeschattenkopie-Dienst.  
      
5.  Der Volumeschattenkopie-Dienst weist die Writer an, die Schreib-e/a-Anforderungen von Anwendungen vorübergehend zu fixieren (Lese-e/a-Anforderungen sind immer noch möglich) für die wenigen Sekunden, die zum Erstellen der Schatten Kopie des Volumes oder der Volumes benötigt werden. Das Einfrieren der Anwendung darf nicht länger als 60 Sekunden dauern. Der Volumeschattenkopie-Dienst leert die Dateisystem Puffer und friert dann das Dateisystem ein, wodurch sichergestellt wird, dass die Metadaten des Dateisystems ordnungsgemäß aufgezeichnet werden und die zu schattenkopierten Daten in einer konsistenten Reihenfolge geschrieben werden.  
      
6.  Der Volumeschattenkopie-Dienst weist den Anbieter an, die Schatten Kopie zu erstellen. Die Erstellung der Schattenkopieerstellung dauert höchstens 10 Sekunden, während der alle Schreib-e/a-Anforderungen an das Dateisystem eingefroren bleiben.  
      
7.  In der Volumeschattenkopie-Dienst werden Schreib-e/a-Anforderungen des Dateisystems veröffentlicht.  
      
8.  VSS weist die Writer an, Anwendungs Schreib-e/a-Anforderungen zu überschreiben. An diesem Punkt können Anwendungen das Schreiben von Daten auf den Datenträger, auf den die Schatten Kopien kopiert werden, fortsetzen.  
      

> [!NOTE]
> Die Erstellung von Schatten Kopien kann abgebrochen werden, wenn die Writer länger als 60 Sekunden im Einfrieren beibehalten werden oder wenn die Anbieter länger als 10 Sekunden zum Ausführen eines Commit für die Schatten Kopie benötigen. 
<br>

9. Der Anforderer kann den Prozess wiederholen (wechseln Sie zurück zu Schritt 1), oder Benachrichtigen Sie den Administrator, dass er zu einem späteren Zeitpunkt wiederholt werden soll.  
      
10. Wenn die Schatten Kopie erfolgreich erstellt wurde, gibt die Volumeschattenkopie-Dienst die Speicherort Informationen für die Schatten Kopie an den Anforderer zurück. In einigen Fällen kann die Schatten Kopie vorübergehend als Volume mit Lese-/Schreibzugriff zur Verfügung gestellt werden, damit VSS und eine oder mehrere Anwendungen den Inhalt der Schatten Kopie ändern können, bevor die Schatten Kopie abgeschlossen ist. Nachdem VSS und die Anwendungen Ihre Änderungen vorgenommen haben, wird die Schatten Kopie als schreibgeschützt festzulegen. Diese Phase wird als automatische Wiederherstellung bezeichnet und wird verwendet, um alle Dateisystem-oder Anwendungs Transaktionen auf dem Schattenkopievolume rückgängig zu machen, die vor dem Erstellen der Schatten Kopie nicht abgeschlossen wurden.  
      

### <a name="how-the-provider-creates-a-shadow-copy"></a>So erstellt der Anbieter eine Schatten Kopie

Ein Hardware-oder Software Schatten Kopie-Anbieter verwendet zum Erstellen einer Schatten Kopie eine der folgenden Methoden:

**Vollständige Kopie**   diese Methode erstellt zu einem bestimmten Zeitpunkt eine vollständige Kopie (als "Vollversion" oder "Klon" bezeichnet) des ursprünglichen Volumes. Diese Kopie ist schreibgeschützt.

**Copy-on-Write-**    diese Methode kopiert das ursprüngliche Volume nicht. Stattdessen wird eine differenzielle Kopie erstellt, indem alle Änderungen (abgeschlossene Schreib-e/a-Anforderungen) kopiert werden, die nach einem bestimmten Zeitpunkt auf dem Volume vorgenommen werden.

**Umleitung-beim Schreiben**   diese Methode das ursprüngliche Volume nicht kopiert und keine Änderungen am ursprünglichen Volume nach einem bestimmten Zeitpunkt vorgenommen werden. Stattdessen wird eine differenzielle Kopie erstellt, indem alle Änderungen an ein anderes Volume umgeleitet werden.

## <a name="complete-copy"></a>Kopie vervollständigen

Eine komplette Kopie wird in der Regel erstellt, indem ein "Split Mirror" wie folgt erstellt wird:

1.  Das ursprüngliche Volume und das Schattenkopievolume sind ein gespiegelter Volumesatz.  
      
2.  Das Schattenkopievolume ist vom ursprünglichen Volume getrennt. Dadurch wird die Spiegel Verbindung unterbrochen.  
      

Nachdem die Spiegelungs Verbindung getrennt wurde, sind das ursprüngliche Volume und das Schattenkopievolume unabhängig. Das ursprüngliche Volume akzeptiert weiterhin alle Änderungen (Schreib-e/a-Anforderungen), während das Schattenkopievolume eine genaue schreibgeschützte Kopie der ursprünglichen Daten zum Zeitpunkt der Unterbrechung bleibt.

### <a name="copy-on-write-method"></a>Copy-on-Write-Methode

Wenn bei der Copy-on-Write-Methode eine Änderung am ursprünglichen Volume stattfindet (aber bevor die Schreib-e/a-Anforderung abgeschlossen ist), wird jeder zu ändernde Block gelesen und dann in den Speicherbereich der Schatten Kopie des Volumes geschrieben (auch als "diff-Bereich" bezeichnet). Der Schattenkopiespeicherbereich kann sich auf demselben Volume oder auf einem anderen Volume befinden. Dadurch wird eine Kopie des Datenblocks auf dem ursprünglichen Volume beibehalten, bevor die Änderung diese überschreibt.


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
<th>Schatten Kopie (Status und Daten)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>Ursprüngliche Daten: 1 2 3 4 5</p></td>
<td><p>Keine Kopie: –</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>Geänderte Daten im Cache: 3 bis 3 "</p></td>
<td><p>Schatten Kopie erstellt (nur Unterschiede): 3</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>Die ursprünglichen Daten wurden überschrieben: 1 2 3 "4 5</p></td>
<td><p>Unterschiede und Index, die auf der Schatten Kopie gespeichert sind: 3</p></td>
</tr>
</tbody>
</table>

**Tabelle 1**   die Copy-on-Write-Methode zum Erstellen von Schatten Kopien

Die Copy-on-Write-Methode ist eine schnelle Methode zum Erstellen einer Schatten Kopie, da nur geänderte Daten kopiert werden. Die kopierten Blöcke im Vergleichs Bereich können mit den geänderten Daten auf dem ursprünglichen Volume kombiniert werden, um das Volume in seinem Zustand wiederherzustellen, bevor Änderungen vorgenommen wurden. Wenn viele Änderungen vorhanden sind, kann die Copy-on-Write-Methode kostspielig werden.

### <a name="redirect-on-write-method"></a>Redirect-on-Write-Methode

Bei der Redirect-on-Write-Methode wird die Änderung nicht auf das ursprüngliche Volume angewendet, wenn das ursprüngliche Volume eine Änderung empfängt (Schreib-e/a-Anforderung). Stattdessen wird die Änderung in den Schattenkopiespeicherbereich eines anderen Volumes geschrieben.


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
<th>Schatten Kopie (Status und Daten)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>Ursprüngliche Daten: 1 2 3 4 5</p></td>
<td><p>Keine Kopie: –</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>Geänderte Daten im Cache: 3 bis 3 "</p></td>
<td><p>Schatten Kopie erstellt (nur Unterschiede): 3 "</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>Unveränderte ursprüngliche Daten: 1 2 3 4 5</p></td>
<td><p>Unterschiede und in Schatten Kopie gespeicherte Indizes: 3 '</p></td>
</tr>
</tbody>
</table>

**Tabelle 2**   der Redirect-on-Write-Methode zum Erstellen von Schatten Kopien

Wie bei der Copy-on-Write-Methode ist die Redirect-on-Write-Methode eine schnelle Methode zum Erstellen einer Schatten Kopie, da nur die Änderungen an den Daten kopiert werden. Die kopierten Blöcke im Vergleichs Bereich können mit den unverändert Daten auf dem ursprünglichen Volume kombiniert werden, um eine komplette, aktuelle Kopie der Daten zu erstellen. Wenn viele Lese-e/a-Anforderungen vorliegen, kann die Redirect-on-Write-Methode kostspielig werden.

## <a name="shadow-copy-providers"></a>Schattenkopieanbieter

Es gibt zwei Arten von schattenkopieanbietern: hardwarebasierte Anbieter und softwarebasierte Anbieter. Es gibt auch einen-Systemanbieter, bei dem es sich um einen in das Windows-Betriebssystem integrierten Softwareanbieter handelt.

### <a name="hardware-based-providers"></a>Hardware basierte Anbieter

Hardware basierte Schattenkopieanbieter fungieren als Schnittstellen zwischen dem Volumeschattenkopie-Dienst und der Hardwareebene, indem Sie in Verbindung mit einem Hardware Speicher Adapter oder-Controller arbeiten. Das Erstellen und Verwalten der Schatten Kopie wird vom Speicher Array durchgeführt.

Hardware Anbieter nehmen immer die Schatten Kopie einer ganzen LUN an, aber der Volumeschattenkopie-Dienst macht nur die Schatten Kopie der angeforderten Volumes oder Volumes verfügbar.

Ein hardwarebasierter Schattenkopieanbieter nutzt die Volumeschattenkopie-Dienst Funktionen, die den Zeitpunkt definieren, die Datensynchronisierung, die Schatten Kopie und eine gemeinsame Schnittstelle mit Sicherungs Anwendungen bereitstellen. Der-Volumeschattenkopie-Dienst gibt jedoch nicht den zugrunde liegenden Mechanismus an, mit dem der hardwarebasierte Anbieter Schatten Kopien erstellt und verwaltet.

### <a name="software-based-providers"></a>Software basierte Anbieter

Software basierte Schattenkopieanbieter fassen Lese-und Schreib Anforderungen in einer Software Schicht zwischen dem Dateisystem und der Volume Manager-Software in der Regel aus und verarbeiten Sie.

Diese Anbieter werden als benutzermodusdll-Komponente und mindestens ein Gerätetreiber im Kernelmodus implementiert, in der Regel ein Speicher Filtertreiber. Im Gegensatz zu hardwarebasierten Anbietern erstellen softwarebasierte Anbieter Schatten Kopien auf Software Ebene, nicht auf der Hardwareebene.

Ein softwarebasierter Schattenkopieanbieter muss eine "Point-in-Time"-Ansicht eines Volumes verwalten, indem er Zugriff auf ein DataSet hat, das zum Neuerstellen des Volumestatus vor dem Erstellungs Zeitpunkt der Schatten Kopie verwendet werden kann. Ein Beispiel hierfür ist die Copy-on-write-Technik des Systemanbieters. Allerdings gelten für die Volumeschattenkopie-Dienst keine Einschränkungen hinsichtlich der Technik, mit der die softwarebasierten Anbieter Schatten Kopien erstellen und verwalten.

Ein Softwareanbieter gilt für eine größere Anzahl von Speicher Plattformen als bei einem hardwarebasierten Anbieter und sollte auch mit Basis Datenträgern oder logischen Volumes gleich gut funktionieren. (Ein logisches Volume ist ein Volume, das erstellt wird, indem der freie Speicherplatz von zwei oder mehr Datenträgern kombiniert wird.) Im Gegensatz zu Hardware Schatten Kopien verbrauchen Softwareanbieter Betriebssystemressourcen, um die Schatten Kopie zu verwalten.

Weitere Informationen zu Basis Datenträgern finden Sie unter [Was sind grundlegende Datenträger und Volumes?](http://go.microsoft.com/fwlink/?linkid=180894) (http://go.microsoft.com/fwlink/?LinkId=180894) auf TechNet.

### <a name="system-provider"></a>System Anbieter

Im Windows-Betriebssystem wird ein Schattenkopieanbieter, der Systemanbieter, bereitgestellt. Obwohl in Windows ein Standardanbieter bereitgestellt wird, können andere Anbieter Implementierungen bereitstellen, die für Ihre Speicherhardware und Softwareanwendungen optimiert sind.

Um die "Point-in-Time"-Ansicht eines Volumes zu verwalten, das in einer Schatten Kopie enthalten ist, verwendet der Systemanbieter eine Copy-on-Write-Methode. Kopien der Blöcke auf dem Volume, die seit dem Beginn der Erstellung der Schatten Kopie geändert wurden, werden in einem Speicherbereich für Schatten Kopien gespeichert.

Der Systemanbieter kann das Produktions Volume verfügbar machen, das in den Normalfall geschrieben und daraus gelesen werden kann. Wenn die Schatten Kopie benötigt wird, wendet sie logisch die Unterschiede auf die Daten auf dem Produktions Volume an, um die gesamte Schatten Kopie verfügbar zu machen.

Der Schattenkopiespeicherbereich des Systemanbieters muss sich auf einem NTFS-Volume befinden. Das Volume, das als Schatten kopiert werden soll, muss kein NTFS-Volume sein, aber mindestens ein auf dem System eingebundenes Volume muss ein NTFS-Volume sein.

Die Komponenten Dateien, aus denen sich der Systemanbieter besteht, sind "tauprv. dll" und "Volsnap. sys".

### <a name="in-box-vss-writers"></a>In-Box-VSS-Writer

Das Windows-Betriebssystem enthält eine Reihe von VSS-Writern, die für das Auflisten der Daten verantwortlich sind, die für die verschiedenen Windows-Features erforderlich sind.

Weitere Informationen zu diesen Writern finden Sie auf den folgenden Microsoft-Websites:

  - [In-Box-VSS-Writer](http://go.microsoft.com/fwlink/?linkid=180895) (http://go.microsoft.com/fwlink/?LinkId=180895)  
      
  - [Neue in-Box-VSS-Writer für Windows Server 2008 und Windows Vista SP1](http://go.microsoft.com/fwlink/?linkid=180896) (http://go.microsoft.com/fwlink/?LinkId=180896)  
      
  - [Neue in-Box-VSS-Writer für Windows Server 2008 R2 und Windows 7](http://go.microsoft.com/fwlink/?linkid=180897) (http://go.microsoft.com/fwlink/?LinkId=180897)  
      

## <a name="how-shadow-copies-are-used"></a>Verwendung von Schatten Kopien

Zusätzlich zum Sichern von Anwendungsdaten und Systemstatus Informationen können Schatten Kopien für eine Reihe von Zwecken verwendet werden, einschließlich der folgenden:

  - Wiederherstellen von LUNs (LUN-Neusynchronisierung und LUN-Austausch)  
      
  - Wiederherstellen einzelner Dateien (Schattenkopien für freigegebene Ordner)  
      
  - Data Mining mithilfe von austauschen-Schatten Kopien  
      

### <a name="restoring-luns-lun-resynchronization-and-lun-swapping"></a>Wiederherstellen von LUNs (LUN-Neusynchronisierung und LUN-Austausch)

In Windows Server 2008 R2 und Windows 7 können VSS-Anforderer eine Hardware Schatten Kopie-Anbieter Funktion namens LUN Resync (oder "LUN Resync") verwenden. Dies ist ein schnelles Wiederherstellungs Schema, das es einem Anwendungs Administrator ermöglicht, Daten aus einer Schatten Kopie in der ursprünglichen LUN oder einer neuen LUN wiederherzustellen.

Bei der Schatten Kopie kann es sich um einen vollständigen Klon oder eine differenzielle Schatten Kopie handeln. In beiden Fällen hat die Ziel-LUN am Ende des Vorgangs zum erneuten Synchronisieren denselben Inhalt wie die LUN der Schattenkopie. Während des erneuten Synchronisierungs Vorgangs führt das Array eine Kopie auf Blockebene aus der Schatten Kopie in die Ziel-LUN aus.


> [!NOTE]
> Die Schatten Kopie muss eine austauschen-Hardware Schatten Kopie sein. 
<br>


Die meisten Arrays ermöglichen das Fortsetzen von Produktions-e/a-Vorgängen kurz nach Beginn des Vorgangs zum erneuten synchronisieren. Während des erneuten Synchronisierungs Vorgangs werden Lese Anforderungen an die LUN der Schatten Kopie umgeleitet, und es werden Anforderungen an die Ziel-LUN geschrieben. Dadurch können Arrays sehr große Datasets wiederherstellen und den normalen Betrieb in wenigen Sekunden fortsetzen.

Die LUN-Neusynchronisierung unterscheidet sich vom LUN-Austausch. Ein LUN-Swap ist ein schnelles Wiederherstellungs Szenario, das von VSS seit Windows Server 2003 SP1 unterstützt wird. Bei einem LUN-Swap wird die Schatten Kopie importiert und anschließend in ein Volume mit Lese-/Schreibzugriff konvertiert. Die Konvertierung ist ein unumkehrbarer Vorgang, und das Volume und die zugrunde liegende LUN können nicht mit den VSS-APIs gesteuert werden. In der folgenden Liste wird beschrieben, wie die LUN-Neusynchronisierung mit LUN-austauschen verglichen wird:

  - Bei der LUN-Neusynchronisierung wird die Schatten Kopie nicht geändert, sodass Sie mehrmals verwendet werden kann. Beim LUN-Austausch kann die Schatten Kopie nur einmal für eine Wiederherstellung verwendet werden. Bei den meisten sicherheitsbewussten Administratoren ist dies wichtig. Wenn die LUN-Neusynchronisierung verwendet wird, kann der Anforderer den gesamten Wiederherstellungs Vorgang wiederholen, wenn beim ersten Mal etwas schief geht.  
      
  - Am Ende eines LUN-Austauschs wird die LUN der Schatten Kopie für Produktions-e/a-Anforderungen verwendet. Aus diesem Grund muss die LUN der Schatten Kopie dieselbe Qualität des Speichers wie die ursprüngliche Produktions-LUN verwenden, um sicherzustellen, dass die Leistung nach dem Wiederherstellungs Vorgang nicht beeinträchtigt wird. Wenn stattdessen die LUN-Neusynchronisierung verwendet wird, kann der Hardware Anbieter die Schatten Kopie im Speicher aufbewahren, die weniger kostengünstiger ist als der Speicher in der Produktionsqualität.  
      
  - Wenn die Ziel-LUN unbrauchbar ist und neu erstellt werden muss, ist der LUN-Austausch möglicherweise wirtschaftlicher, da er keine Ziel-LUN erfordert.  
      


> [!WARNING]
> Alle aufgeführten Vorgänge sind Vorgänge auf LUN-Ebene. Wenn Sie versuchen, ein bestimmtes Volume mithilfe der LUN-Neusynchronisierung wiederherzustellen, können Sie alle anderen Volumes, die die LUN gemeinsam nutzen, nicht zurücksetzen. 
<br>


### <a name="restoring-individual-files-shadow-copies-for-shared-folders"></a>Wiederherstellen einzelner Dateien (Schattenkopien für freigegebene Ordner)

Schattenkopien für freigegebene Ordner verwendet die Volumeschattenkopie-Dienst, um Zeit Punkt Kopien von Dateien bereitzustellen, die sich auf einer freigegebenen Netzwerkressource befinden, z. b. auf einem Dateiserver. Mit Schattenkopien für freigegebene Ordner können Benutzer gelöschte oder geänderte Dateien, die im Netzwerk gespeichert sind, schnell wiederherstellen. Da dies ohne Administrator Unterstützung möglich ist, können Schattenkopien für freigegebene Ordner die Produktivität steigern und die Verwaltungskosten senken.

Weitere Informationen zu Schattenkopien für freigegebene Ordner finden Sie unter [Schattenkopien für freigegebene Ordner](http://go.microsoft.com/fwlink/?linkid=180898) (http://go.microsoft.com/fwlink/?LinkId=180898) auf TechNet.

### <a name="data-mining-by-using-transportable-shadow-copies"></a>Data Mining mithilfe von austauschen-Schatten Kopien

Mithilfe eines Hardware Anbieters, der für die Verwendung mit dem Volumeschattenkopie-Dienst konzipiert ist, können Sie austauschen-Schatten Kopien erstellen, die auf Server innerhalb desselben Subsystems (z. b. ein SAN) importiert werden können. Diese Schatten Kopien können zum Ausgangswert einer Produktions-oder Testinstallation mit schreibgeschützten Daten für Data Mining verwendet werden.

Wenn die Volumeschattenkopie-Dienst und ein Speicher Array mit einem Hardware Anbieter für die Verwendung mit dem Volumeschattenkopie-Dienst entworfen wurden, ist es möglich, eine Schatten Kopie des Quelldaten Volumens auf einem Server zu erstellen und die Schatten Kopie dann auf einen anderen Server zu importieren.  (oder zurück zum gleichen Server). Dieser Prozess wird in wenigen Minuten ausgeführt, unabhängig von der Größe der Daten. Der Transport Vorgang erfolgt durch eine Reihe von Schritten, bei denen ein schattenkopieanforderer (eine Speicher Verwaltungs Anwendung) verwendet wird, der austauschen-Schatten Kopien unterstützt.

## <a name="to-transport-a-shadow-copy"></a>So transportieren Sie eine Schatten Kopie

1.  Erstellen Sie eine austauschen-Schatten Kopie der Quelldaten auf einem Server.

2.  Importieren Sie die Schatten Kopie auf einen Server, der mit dem SAN verbunden ist (Sie können auf einen anderen Server oder auf denselben Server importieren).

3.  Die Daten können jetzt verwendet werden.

![](media/volume-shadow-copy-service/Ee923636.633752e0-92f6-49a7-9348-f451b1dc0ed7(WS.10).jpg)

**Abbildung 3**   Erstellen von Schatten Kopien und transportieren zwischen zwei Servern


> [!NOTE]
> Eine austauschen-Schatten Kopie, die auf Windows Server 2003 erstellt wird, kann nicht auf einen Server importiert werden, auf dem Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird. Eine austauschen-Schatten Kopie, die unter Windows Server 2008 oder Windows Server 2008 R2 erstellt wurde, kann nicht auf einen Server importiert werden, auf dem Windows Server 2003 ausgeführt wird. Eine Schatten Kopie, die auf Windows Server 2008 erstellt wird, kann jedoch auf einen Server importiert werden, auf dem Windows Server 2008 R2 ausgeführt wird, und umgekehrt. 
<br>


Schattenkopien sind schreibgeschützt. Wenn Sie eine Schatten Kopie in eine Lese-/Schreib-LUN konvertieren möchten, können Sie zusätzlich zum Volumeschattenkopie-Dienst eine Dienst basierte Speicher Verwaltungs Anwendung (einschließlich einiger Anforderer) auf virtuellen Datenträgern verwenden. Mithilfe dieser Anwendung können Sie die Schatten Kopie aus Volumeschattenkopie-Dienst Management entfernen und in eine Lese-/Schreib-LUN konvertieren.

Volumeschattenkopie-Dienst Transport ist eine erweiterte Lösung auf Computern, auf denen Windows Server 2003 Enterprise Edition, Windows Server 2003 Datacenter Edition, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird. Dies funktioniert nur, wenn auf dem Speicher Array ein Hardware Anbieter vorhanden ist. Der schattenkopietransport kann für verschiedene Zwecke verwendet werden, einschließlich Band Sicherungen, Data Mining und Tests.

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

Diese FAQ beantwortet Fragen zu Volumeschattenkopie-Dienst (VSS) für Systemadministratoren. Weitere Informationen zu VSS-Anwendungsprogrammierschnittstellen finden Sie unter [Volumeschattenkopie-Dienst](http://go.microsoft.com/fwlink/?linkid=180899) (http://go.microsoft.com/fwlink/?LinkId=180899) in der Bibliothek des Windows Developer Center).

### <a name="when-was-volume-shadow-copy-service-introduced-on-which-windows-operating-system-versions-is-it-available"></a>Wann wurde Volumeschattenkopie-Dienst eingeführt? Auf welchen Windows-Betriebssystemversionen ist die Version verfügbar?

VSS wurde in Windows XP eingeführt. Es ist unter Windows XP, Windows Server 2003, Windows Vista®, Windows Server 2008, Windows 7 und Windows Server 2008 R2 verfügbar.

### <a name="what-is-the-difference-between-a-shadow-copy-and-a-backup"></a>Worin besteht der Unterschied zwischen einer Schatten Kopie und einer Sicherung?

Im Fall einer Sicherung eines Festplatten Laufwerks ist die erstellte Schatten Kopie ebenfalls die Sicherung. Daten können aus der Schatten Kopie für eine Wiederherstellung kopiert werden, oder die Schatten Kopie kann für ein schnelles Wiederherstellungs Szenario verwendet werden – z. b. für die LUN-Neusynchronisierung oder den LUN-Austausch.

Wenn Daten aus der Schatten Kopie auf das Band oder ein anderes Wechselmedium kopiert werden, stellt der auf dem Medium gespeicherte Inhalt die Sicherung dar. Die Schatten Kopie selbst kann gelöscht werden, nachdem die Daten aus ihr kopiert wurden.

### <a name="what-is-the-largest-size-volume-that-volume-shadow-copy-service-supports"></a>Was ist das größte Volume, das Volumeschattenkopie-Dienst unterstützt?

Volumeschattenkopie-Dienst unterstützt eine Volumegröße von bis zu 64 TB.

### <a name="i-made-a-backup-on-windows-server2008-can-i-restore-it-on-windows-server2008r2"></a>Ich habe eine Sicherung auf Windows Server 2008 erstellt. Kann ich Sie unter Windows Server 2008 R2 wiederherstellen?

Dies hängt von der verwendeten Sicherungssoftware ab. Die meisten Sicherungs Programme unterstützen dieses Szenario für Daten, aber nicht für Sicherungen des Systemstatus.

Schatten Kopien, die für eine dieser Versionen von Windows erstellt werden, können für die andere verwendet werden.

### <a name="i-made-a-backup-on-windows-server2003-can-i-restore-it-on-windows-server2008"></a>Ich habe eine Sicherung auf Windows Server 2003 erstellt. Kann ich Sie unter Windows Server 2008 wiederherstellen?

Dies hängt von der verwendeten Sicherungssoftware ab. Wenn Sie eine Schatten Kopie auf Windows Server 2003 erstellen, können Sie Sie nicht unter Windows Server 2008 verwenden. Wenn Sie eine Schatten Kopie auf Windows Server 2008 erstellen, können Sie Sie auch nicht unter Windows Server 2003 wiederherstellen.

### <a name="how-can-i-disable-vss"></a>Wie kann ich VSS deaktivieren?

Die Volumeschattenkopie-Dienst kann mithilfe der Microsoft Management Console deaktiviert werden. Dies sollte jedoch nicht der Fall sein. Das Deaktivieren von VSS wirkt sich negativ auf alle von ihm verwendeten Software aus, z. b. System Wiederherstellung und Windows Server-Sicherung.

Weitere Informationen finden Sie auf den folgenden Microsoft TechNet-Websites:

  - [System Wiederherstellung](http://go.microsoft.com/fwlink/?linkid=157113) (http://go.microsoft.com/fwlink/?LinkID=157113)  
      
  - [Windows Server-Sicherung](http://go.microsoft.com/fwlink/?linkid=180891) (http://go.microsoft.com/fwlink/?LinkID=180891)  
      

### <a name="can-i-exclude-files-from-a-shadow-copy-to-save-space"></a>Kann ich Dateien aus einer Schatten Kopie ausschließen, um Speicherplatz zu sparen?

VSS dient zum Erstellen von Schatten Kopien ganzer Volumes. Temporäre Dateien, z. b. Auslagerungs Dateien, werden automatisch aus Schatten Kopien weggelassen, um Speicherplatz zu sparen.

Um bestimmte Dateien aus Schatten Kopien auszuschließen, verwenden Sie den folgenden Registrierungsschlüssel: " **filesnottosnapshot**".


> [!NOTE]
> Der Registrierungsschlüssel " <STRONG>filesnottosnapshot</STRONG> " soll nur von Anwendungen verwendet werden. Benutzer, die versuchen, Sie zu verwenden, erhalten Einschränkungen wie die folgenden:
> <br>
> <UL>
> <LI>Dateien aus einer Schatten Kopie, die auf einem Windows-Server erstellt wurde, können mit der Funktion "vorherige Versionen" nicht gelöscht werden.<BR><BR>
> <LI>Dateien aus Schatten Kopien für freigegebene Ordner können nicht gelöscht werden.<BR><BR>
> <LI>Es können Dateien aus einer Schatten Kopie gelöscht werden, die mit dem Hilfsprogramm <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow" data-raw-source="[Diskshadow](https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow)">DiskShadow</a> erstellt wurde, aber es können keine Dateien aus einer Schatten Kopie gelöscht werden, die mit dem Hilfsprogramm <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin" data-raw-source="[Vssadmin](https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin)">vssadmin</a> erstellt wurde.<BR><BR>
> <LI>Dateien werden auf der Grundlage der besten Leistung aus einer Schatten Kopie gelöscht. Dies bedeutet, dass Sie nicht unbedingt gelöscht werden.<BR><BR></LI></UL>


Weitere Informationen finden Sie unter [Ausschließen von Dateien aus Schatten Kopien](http://go.microsoft.com/fwlink/?linkid=180904) (http://go.microsoft.com/fwlink/?LinkId=180904) auf MSDN.

### <a name="my-non-microsoft-backup-program-failed-with-a-vss-error-what-can-i-do"></a>VSS-Fehler bei meinem nicht-Microsoft-Sicherungsprogramm. Was kann ich tun?

Überprüfen Sie den Produktsupport Abschnitt der Website des Unternehmens, von dem das Sicherungsprogramm erstellt wurde. Möglicherweise gibt es ein Produkt Update, das Sie herunterladen und installieren können, um das Problem zu beheben. Falls nicht, wenden Sie sich an die Produktsupport Abteilung des Unternehmens.

System Administratoren können die VSS-Informationen zur Problembehandlung auf der folgenden Microsoft TechNet Library-Website verwenden, um Diagnoseinformationen zu VSS-bezogenen Problemen zu sammeln.

Weitere Informationen finden Sie unter [Volumeschattenkopie-Dienst](http://go.microsoft.com/fwlink/?linkid=180905) (http://go.microsoft.com/fwlink/?LinkId=180905) auf TechNet.

### <a name="what-is-the-diff-area"></a>Was ist der "diff-Bereich"?

Der Schattenkopiespeicherbereich (oder der diff-Bereich) ist der Speicherort, an dem die Daten für die vom Systemsoftware Anbieter erstellte Schatten Kopie gespeichert werden.

### <a name="where-is-the-diff-area-located"></a>Wo befindet sich der diff-Bereich?

Der diff-Bereich kann sich auf einem beliebigen lokalen Volume befinden. Es muss sich jedoch auf einem NTFS-Volume befinden, das über genügend Speicherplatz verfügt, um es zu speichern.

### <a name="how-is-the-diff-area-location-determined"></a>Wie wird der diff-Bereichs Speicherort festgelegt?

Die folgenden Kriterien werden in dieser Reihenfolge ausgewertet, um den diff-Bereichs Speicherort zu bestimmen:

  - Wenn ein Volume bereits über eine Schatten Kopie verfügt, wird dieser Speicherort verwendet.  
      
  - Wenn eine vorkonfigurierte manuelle Zuordnung zwischen dem ursprünglichen Volume und dem Speicherort der Schattenkopievolumes vorhanden ist, wird dieser Speicherort verwendet.  
      
  - Wenn die beiden vorherigen Kriterien keinen Speicherort angeben, wählt der Schattenkopiedienst einen Speicherort basierend auf dem verfügbaren freien Speicherplatz aus. Wenn mehrere Volumes kopiert werden, erstellt der Schattenkopiedienst eine Liste möglicher Momentaufnahme Speicherorte basierend auf der Größe des freien Speicherplatzes in absteigender Reihenfolge. Die Anzahl der bereitgestellten Speicherorte entspricht der Anzahl der Volumes, die mit dem Schatten kopiert werden.  
      
  - Wenn das zu überprüfende Volume einer der möglichen Speicherorte ist, wird eine lokale Zuordnung erstellt. Andernfalls wird eine Zuordnung mit dem Volume mit dem meisten verfügbaren Speicherplatz erstellt.  
      

### <a name="can-vss-create-shadow-copies-of-non-ntfs-volumes"></a>Kann VSS Schatten Kopien von nicht-NTFS-Volumes erstellen?

Ja. Persistente Schatten Kopien können jedoch nur für NTFS-Volumes erstellt werden. Außerdem muss mindestens ein Volume, das auf dem System eingebunden ist, ein NTFS-Volume sein.

### <a name="whats-the-maximum-number-of-shadow-copies-i-can-create-at-one-time"></a>Wie hoch ist die maximale Anzahl von Schatten Kopien, die ich gleichzeitig erstellen kann?

Die maximale Anzahl von schattenkopierten Volumes in einem einzelnen Schattenkopiesatz beträgt 64. Beachten Sie, dass dies nicht mit der Anzahl der Schatten Kopien übereinstimmt.

### <a name="whats-the-maximum-number-of-software-shadow-copies-created-by-the-system-provider-that-i-can-maintain-for-a-volume"></a>Wie hoch ist die maximale Anzahl von Software Schatten Kopien, die vom Systemanbieter für ein Volume erstellt werden können?

Der Wert für die maximale Anzahl von Software Schatten Kopien beträgt 512. Standardmäßig können Sie jedoch nur 64 Schatten Kopien verwalten, die von der Funktion "Schatten Kopien der freigegebenen Ordner" verwendet werden. Verwenden Sie den folgenden Registrierungsschlüssel, um das Limit für die Funktion "Schatten Kopien von freigegebenen Ordnern" zu ändern: **maxshadowkopien**.

### <a name="how-can-i-control-the-space-that-is-used-for-shadow-copy-storage-space"></a>Wie kann ich den Speicherplatz steuern, der für den Speicherplatz für Schatten Kopien verwendet wird?

Geben Sie den Befehl **vssadmin Größe ShadowStorage** ein.

Weitere Informationen finden Sie unter [vssadmin Größe ShadowStorage](http://go.microsoft.com/fwlink/?linkid=180906) (http://go.microsoft.com/fwlink/?LinkId=180906) auf TechNet.

### <a name="what-happens-when-i-run-out-of-space"></a>Was geschieht, wenn kein Speicherplatz mehr verfügbar ist?

Schatten Kopien für das Volume werden ab der ältesten Schatten Kopie gelöscht.

## <a name="volume-shadow-copy-service-tools"></a>Volumeschattenkopie-Dienst Tools

Das Windows-Betriebssystem stellt die folgenden Tools zum Arbeiten mit VSS bereit:

  - [DiskShadow](http://go.microsoft.com/fwlink/?linkid=180907) (http://go.microsoft.com/fwlink/?LinkId=180907)  
      
  - [Vssadmin](http://go.microsoft.com/fwlink/?linkid=84008) (http://go.microsoft.com/fwlink/?LinkId=84008)  
      

### <a name="diskshadow"></a>DiskShadow

DiskShadow ist ein VSS-Anforderer, mit dem Sie alle Hardware-und Software Momentaufnahmen verwalten können, die Sie auf einem System haben können. DiskShadow umfasst Befehle wie die folgenden:

  - **List**: Listet VSS-Writer, VSS-Anbieter und Schatten Kopien auf  
      
  - **Erstellen**: erstellt eine neue Schatten Kopie.  
      
  - **Import**: importiert eine austauschen-Schatten Kopie.  
      
  - verfügbar **machen: macht**eine persistente Schatten Kopie (z. b. als Laufwerk Buchstaben) verfügbar.  
      
  - **Revert**: setzt ein Volume auf eine angegebene Schatten Kopie zurück.  
      

Dieses Tool ist für die Verwendung durch IT-Experten vorgesehen, aber Entwickler können es auch beim Testen eines VSS Writer-oder VSS-Anbieters nützlich finden.

DiskShadow ist nur unter Windows Server-Betriebssystemen verfügbar. Es ist auf Windows-Client Betriebssystemen nicht verfügbar.

### <a name="vssadmin"></a>VssAdmin

Vssadmin dient zum Erstellen, löschen und Auflisten von Informationen zu Schatten Kopien. Sie kann auch verwendet werden, um die Größe des Schattenkopiespeicherbereichs ("diff-Bereich") zu ändern.

Vssadmin umfasst Befehle wie die folgenden:

  - **Schatten erstellen**: erstellt eine neue Schatten Kopie.  
      
  - **Schatten Kopien löschen**: löscht Schatten Kopien.  
      
  - **Anbieter auflisten**: Listet alle registrierten VSS-Anbieter auf.  
      
  - **Writer auflisten**: Listet alle abonnierten VSS-Writer auf.  
      
  - **Größe ShadowStorage**: ändert die maximale Größe des Speicherbereichs für Schatten Kopien.  
      

Vssadmin kann nur zum Verwalten von Schatten Kopien verwendet werden, die vom Systemsoftware Anbieter erstellt werden.

Vssadmin ist auf Windows-Client-und Windows Server-Betriebssystemversionen verfügbar.

## <a name="volume-shadow-copy-service-registry-keys"></a>Registrierungsschlüssel Volumeschattenkopie-Dienst

Die folgenden Registrierungsschlüssel sind für die Verwendung mit VSS verfügbar:

  - **VssAccessControl**  
      
  - **Maxshadowkopien**  
      
  - **MinDiffAreaFileSize**  
      

### <a name="vssaccesscontrol"></a>VssAccessControl

Dieser Schlüssel wird verwendet, um anzugeben, welche Benutzer Zugriff auf Schatten Kopien haben.

Weitere Informationen finden Sie auf der MSDN-Website in den folgenden Einträgen:

  - [Sicherheitsüberlegungen für Writer](http://go.microsoft.com/fwlink/?linkid=157739) (http://go.microsoft.com/fwlink/?LinkId=157739)  
      
  - [Sicherheitsüberlegungen für](http://go.microsoft.com/fwlink/?linkid=180908) Anforderer (http://go.microsoft.com/fwlink/?LinkId=180908)  
      

### <a name="maxshadowcopies"></a>Maxshadowkopien

Dieser Schlüssel gibt die maximale Anzahl von Client zugänglichen Schatten Kopien an, die auf jedem Volume des Computers gespeichert werden können. Die vom Client zugänglichen Schatten Kopien werden von Schattenkopien für freigegebene Ordner verwendet.

Weitere Informationen finden Sie auf der MSDN-Website im folgenden Eintrag:

**Maxshadowkopien** unter [Registrierungs Schlüsseln für die Sicherung und Wiederherstellung](http://go.microsoft.com/fwlink/?linkid=180909) (http://go.microsoft.com/fwlink/?LinkId=180909)

### <a name="mindiffareafilesize"></a>MinDiffAreaFileSize

Dieser Schlüssel gibt die minimale anfängliche Größe des Schattenkopiespeicherbereichs in MB an.

Weitere Informationen finden Sie auf der MSDN-Website im folgenden Eintrag:

**MinDiffAreaFileSize** unter [Registrierungs Schlüsseln für die Sicherung und Wiederherstellung](http://go.microsoft.com/fwlink/?linkid=180910) (http://go.microsoft.com/fwlink/?LinkId=180910)

`##`# "unterstützte Betriebs System Versionen

In der folgenden Tabelle sind die unterstützten Betriebssystemversionen für VSS-Funktionen aufgeführt.


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
<td><p>LUN-Neusynchronisierung</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2008 R2</p></td>
</tr>
<tr class="even">
<td><p>Registrierungsschlüssel " <strong>filesnottosnapshot</strong> "</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td><p>Über transportable Schatten Kopien</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003 mit SP1</p></td>
</tr>
<tr class="even">
<td><p>Hardware Schatten Kopien</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>Frühere Versionen von Windows Server</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="even">
<td><p>Schnelle Wiederherstellung mit LUN-Swap</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003 mit SP1</p></td>
</tr>
<tr class="odd">
<td><p>Mehrere Importe von Hardware Schatten Kopien</p>
<div class="alert">
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="media/volume-shadow-copy-service/Dd560667.note(WS.10).gif" />Hinweis:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dies ist die Möglichkeit, eine Schatten Kopie mehrmals zu importieren. Es kann jeweils nur ein Import Vorgang ausgeführt werden.
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
<td><p>Über transportable automatisch wiederhergestellte Schatten Kopien</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>Gleichzeitige Sicherungs Sitzungen (bis zu 64)</p></td>
<td><p>Windows XP</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>Einzelne Wiederherstellungs Sitzung gleichzeitig mit Sicherungen</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003 mit SP2</p></td>
</tr>
<tr class="even">
<td><p>Bis zu 8 Wiederherstellungs Sitzungen gleichzeitig mit Sicherungen</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows Server 2003 R2</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>Weitere Informationen

[Volumeschattenkopie-Dienst im Windows Developer Center](https://docs.microsoft.com/windows/desktop/vss/volume-shadow-copy-service-overview)