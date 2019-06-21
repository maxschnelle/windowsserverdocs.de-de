---
Title: Volumeschattenkopie-Dienst
ms.date: 01/30/2019
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 0a4af25723c6d1e796cd3255875c15faf21fb8be
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284383"
---
# <a name="volume-shadow-copy-service"></a>Volumeschattenkopie-Dienst

Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012 und WindowsServer 2008 R2, WindowsServer 2008, Windows 10, Windows 8.1, Windows 8, Windows 7

Sichern und Wiederherstellen von kritischen Geschäftsdaten aufgrund von folgenden Problemen sehr komplex sind möglich:

  - In der Regel müssen die Daten gesichert werden, während die Anwendungen, die die Daten generiert noch ausgeführt werden. Dies bedeutet, dass einige der Datendateien geöffnet sein kann oder möglicherweise in einem inkonsistenten Zustand.  
      
  - Wenn der DataSet groß ist, kann es schwierig, alle auf einmal gesichert sein.  
      

Sicherungs-und Wiederherstellungsvorgänge ordnungsgemäß funktioniert, erfordert enger Koordination zwischen der backup-Anwendungen, die Line-of-Business-Anwendungen, die sich gesichert werden und Speicher-Management-Hardware und Software. Das Volume Shadow Copy Service (VSS), die in Windows Server® 2003 eingeführt wurde, ermöglicht die Kommunikation zwischen diesen Komponenten um besser zusammenarbeiten können. Wenn alle Komponenten VSS unterstützen, können Sie sie verwenden, Ihre Anwendungsdaten sichern, ohne die Anwendungen offline zu schalten.

VSS koordiniert die Aktionen, die Erstellung eine konsistenten Schattenkopie (auch bekannt als eine Momentaufnahme oder eine Point-in-Time-Kopie) der Daten, die gesichert werden, erforderlich sind. Die Schattenkopie als dienen kann – ist, oder in Szenarien wie das folgende verwendet werden können:

  - Sie möchten, um Daten und Systemeinstellungen Statusinformationen zu Anwendungen, einschließlich der Archivierung von Daten auf einem anderen Festplattenlaufwerk, auf Band oder auf einem anderen Wechselmedium zu sichern.  
      
  - Sie können Datamining.  
      
  - Sie werden die Sicherungen von Datenträger zu Datenträger ausführen.  
      
  - Benötigen Sie eine schnelle Wiederherstellung von Daten zu, indem Sie Daten wiederherstellen, auf die ursprüngliche LUN oder auf eine völlig neue LUN, die eine ursprüngliche LUN ersetzt, die nicht.  
      

Windows-Features und Anwendungen, die VSS verwenden umfassen Folgendes:

  - [Windows Server-Sicherung](http://go.microsoft.com/fwlink/?linkid=180891) ()http://go.microsoft.com/fwlink/?LinkId=180891)  
      
  - [Schattenkopien von freigegebenen Ordnern](http://go.microsoft.com/fwlink/?linkid=142874) ()http://go.microsoft.com/fwlink/?LinkId=142874)  
      
  - [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=180892) ()http://go.microsoft.com/fwlink/?LinkId=180892)  
      
  - [Systemwiederherstellung](http://go.microsoft.com/fwlink/?linkid=180893) ()http://go.microsoft.com/fwlink/?LinkId=180893)  
      

## <a name="how-volume-shadow-copy-service-works"></a>Funktionsweise der Volumeschattenkopie-Dienst

Eine vollständige VSS-Lösung erfordert, dass alle von den folgenden grundlegenden Bestandteile:

**VSS-Dienst**   Teil des Windows-Betriebssystems, der die anderen Komponenten gewährleistet ordnungsgemäß miteinander kommunizieren und zusammenarbeiten kann.

**VSS-anforderer**   der Software, die die tatsächliche Erstellung des Volumeschattenkopie-Kopien (oder andere Vorgänge auf höchster Ebene, z. B. Importieren von oder löschen) anfordert. Dies ist normalerweise die sicherungsanwendung. Das Hilfsprogramm Windows Server-Sicherung und der System Center Data Protection Manager-Anwendung sind VSS anfordernde Personen. Nicht von Microsoft® VSS anfordernde Personen sind fast alle Sicherungssoftware, die unter Windows ausgeführt wird.

**VSS-Writer**   die Komponente, die sicherstellt, haben wir ein konsistentes DataSet zu sichern. Dies wird in der Regel als Teil einer Line-of-Business-Anwendung, z. B. SQL Server® oder Exchange-Server bereitgestellt. VSS-Writer für verschiedene Windows-Komponenten, z. B. der Registrierung sind in der Windows-Betriebssystem enthalten. Nicht-Microsoft VSS Writer-Instanzen sind in vielen Anwendungen für Windows, die Gewährleistung der Datenkonsistenz der während der Sicherung einrichten müssen enthalten.

**VSS-Anbieter**   die Komponente, die erstellt und verwaltet die Schattenkopien. Dies kann in der Software oder Hardware auftreten. Das Windows-Betriebssystem enthält einen VSS-Anbieter, der Kopie-bei-Schreibvorgang verwendet. Wenn Sie ein Storage Area Network (SAN) verwenden, ist es wichtig, dass Sie den VSS-Hardwareanbieter für den SAN, installieren, sofern vorhanden. Ein Hardwareanbieter lagert die Aufgabe erstellt und verwaltet eine Schattenkopie von Host-Betriebssystem.

Das folgende Diagramm veranschaulicht, wie der VSS-Dienst koordiniert mit anfordernde Personen, Schreiber und Anbieter, um eine Schattenkopie von einem Volume zu erstellen.

![](media/volume-shadow-copy-service/Ee923636.94dfb91e-8fc9-47c6-abc6-b96077196741(WS.10).jpg)

**Abbildung 1**   Architekturdiagramm der Volumeschattenkopie-Dienst

### <a name="how-a-shadow-copy-is-created"></a>Wie wird eine Schattenkopie erstellt.

In diesem Abschnitt werden die verschiedenen Rollen, der die anfordernde Person, Schreiber und Anbieter in Kontext, durch Auflisten der Schritte, die ausgeführt werden, um eine Schattenkopie erstellt werden müssen. Das folgende Diagramm zeigt, wie der Volumeschattenkopie-Dienst für die gesamte Koordination die anfordernde Person, Schreiber und Anbieter steuert.

![](media/volume-shadow-copy-service/Ee923636.1c481a14-d6bc-4796-a3ff-8c6e2174749b(WS.10).jpg)

**Abbildung 2** Erstellungsvorgang für Schattenkopie

Um eine Schattenkopie zu erstellen, Ausführen die anfordernde Person, Schreiber und Anbieter die folgenden Aktionen:

1.  Die anfordernde Person fragt den Volumeschattenkopie-Dienst die Writer aufgelistet, die Metadaten zu erfassen und Vorbereiten für die Erstellung von Schattenkopien.  
      
2.  Jeden Schreiber erstellt eine XML-Beschreibung der Komponenten und Daten speichert, die gesichert werden müssen und für den Volumeschattenkopie-Dienst bereitgestellt. Der Writer definiert auch eine Restore-Methode, die für alle Komponenten verwendet wird. Der Volumeschattenkopie-Dienst enthält eine Beschreibung für den Writer an der anfordernde Person an, die die Komponenten auswählt, die gesichert werden.  
      
3.  Der Volumeschattenkopie-Dienst benachrichtigt alle Autoren ihre Daten vorbereiten Hinblick auf eine Schattenkopie.  
      
4.  Jede Writer bereitet die Daten nach Bedarf, und öffnen z. B. nachdem alle Transaktionen, parallele Transaktionsprotokolle, und leeren des Caches. Wenn die Daten werden Schattenkopien sind, benachrichtigt der Writer die Volumeschattenkopie-Dienst.  
      
5.  Der Volumeschattenkopie-Dienst weist den Writer vorübergehend sperren Anwendung schreiben e/a-Anforderungen (Lesen, die e/a-Anforderungen sind immer noch möglich) für die Sekunden, die zum Erstellen der Schattenkopie des Datenträgers oder Volumes erforderlich sind. Das Fixieren der Anwendung darf nicht länger als 60 Sekunden dauert. Der Volumeschattenkopie-Dienst die Dateisystem-Puffer leert und klicken Sie dann friert das Dateisystem, der sicherstellt, dass die Metadaten des Dateisystems ordnungsgemäß aufgezeichnet werden und die Daten auf Schattenkopien in einer konsistenten Reihenfolge geschrieben.  
      
6.  Der Volumeschattenkopie-Dienst weist den Anbieter die Schattenkopie zu erstellen. Der Schattenkopie Kopie erstellen Zeitraum dauert nicht mehr als 10 Sekunden, in denen alle Schreibvorgänge, dass e/a-Anforderungen im Dateisystem fixiert bleiben.  
      
7.  Der Volumeschattenkopie-Dienst gibt die Datei-e/a dateisystembezogene Schreibanforderungen frei.  
      
8.  VSS weist den Writer zum Reaktivieren der e/a-Anforderungen von Anwendungen schreiben. Anwendungen können sich an diesem Punkt fortgesetzt, das Schreiben von Daten auf den Datenträger, der Schattenkopie erstellt wird.  
      

> [!NOTE]
> Die Erstellung von Schattenkopien abgebrochen werden kann, wenn der Writer beibehalten werden, in den Fixierungszustand länger als 60 Sekunden oder länger als 10 Sekunden die Schattenkopie commit für die Anbieter erhöht werden. 
<br>

9. Die anfordernde Person kann den Prozess (Wechseln Sie zurück zu Schritt 1) wiederholen oder den Administrator benachrichtigen, um zu einem späteren Zeitpunkt zu wiederholen.  
      
10. Wenn die Schattenkopie wurde erfolgreich erstellt wurde, gibt der Volumeschattenkopie-Dienst die Informationen zum Speicherort für die Schattenkopie an die anfordernde Person zurück. In einigen Fällen kann die Schattenkopie vorübergehend zur Verfügung gestellt als Datenträger für Lese-/ Schreibzugriff, sodass diese VSS und eine oder mehrere Anwendungen können den Inhalt ändern der Schattenkopie, bevor die Schattenkopie abgeschlossen ist. Nachdem die abweichungen zu VSS und den Anwendungen machen, ist die Schattenkopie schreibgeschützt festgelegt. In dieser Phase wird die automatische Wiederherstellung aufgerufen, und es wird verwendet, um alle Transaktionen für das Dateisystem oder eine Anwendung auf dem Schattenkopievolume rückgängig zu machen, die nicht abgeschlossen wurden, bevor die Schattenkopie erstellt wurde.  
      

### <a name="how-the-provider-creates-a-shadow-copy"></a>Wie der Anbieter eine Schattenkopie erstellt

Eine Hardware oder Software Schattenkopieanbieter verwendet eine der folgenden Methoden zum Erstellen einer Schattenkopie:

**Vollständige Kopie**   diese Methode wird eine vollständige Kopie ("full-Copy" oder "Klonen" genannt) des ursprünglichen Volumes zu einem bestimmten Zeitpunkt rechtzeitig. Diese Kopie ist schreibgeschützt.

**Kopie-bei-Schreibvorgang**   kopiert diese Methode nicht das ursprüngliche Volume. Stattdessen wird eine differenzielle Kopie durch Kopieren aller Änderungen (abgeschlossene schreiben e/a-Anforderungen), die auf das Volume nach einem bestimmten Zeitpunkt vorgenommen werden.

**Umleitungs-bei-Schreibvorgang**   kopiert diese Methode nicht das ursprüngliche Volume, und es macht keine Änderungen auf das ursprüngliche Volume nach einem bestimmten Zeitpunkt in der Zeit. Stattdessen wird eine differenzielle Kopie durch das Umleiten von alle Änderungen an einem anderen Volume.

## <a name="complete-copy"></a>Vollständige Kopie

Eine vollständige Kopie wird in der Regel dazu eine "Split-Mirror" wie folgt erstellt:

1.  Das ursprüngliche Volume, und das Schattenkopievolume sind eine Reihe von gespiegelten Volumes.  
      
2.  Der Schattenkopievolume wird aus dem ursprünglichen Volume getrennt. Dies unterbricht die Verbindung für die Spiegelung.  
      

Nachdem die Verbindung für die Spiegelung unterbrochen wird, sind das ursprüngliche Volume, und das Schattenkopievolume unabhängig. Das ursprüngliche Volume weiterhin akzeptieren Sie alle Änderungen (Schreiben e/a-Anforderungen), während die Schattenkopie Volume bleibt eine genaue schreibgeschützte Kopie der ursprünglichen Daten zum Zeitpunkt der Unterbrechung.

### <a name="copy-on-write-method"></a>Copy-on-Write-Methode

In der Kopie-bei-Schreibvorgang-Methode bei einer auf das ursprüngliche Volume Änderung (jedoch vor dem Schreiben e/a-Anforderung abgeschlossen ist), jeden Block zu ändernden gelesen und dann in der Datenträger den Schattenkopie-Speicherbereich (auch als der "Vergleichsbereich" bezeichnet) geschrieben. Die Schattenkopie-Speicherbereich kann auf demselben Datenträger oder ein anderes Volume sein. Dadurch wird eine Kopie der Datenblöcke auf dem ursprünglichen Volume beibehalten, bevor die Änderung wird überschrieben.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Uhrzeit</th>
<th>Quelldaten (Status und Daten)</th>
<th>Schattenkopie (Status und Daten)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>Originaldaten: 1 2 3 4 5</p></td>
<td><p>Keine Kopie::</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>Die Daten im Cache geändert: 3, 3'</p></td>
<td><p>Schattenkopieclient erstellt (nur unterschieden): 3</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>Ursprünglichen Daten, die überschrieben werden: 1 2 3’ 4 5</p></td>
<td><p>Unterschiede und Index auf der Schattenkopie gespeichert: 3</p></td>
</tr>
</tbody>
</table>

**Tabelle 1**   der Kopie-bei-Schreibvorgang-Methode zum Erstellen von Schattenkopien

Die Kopie-bei-Schreibvorgang-Methode ist eine schnelle Methode zum Erstellen einer Schattenkopie, da diese nur Daten kopiert, die geändert wird. Mit den geänderten Daten auf das ursprüngliche Volume, das Volume in den Zustand wiederherstellen, bevor die Änderungen vorgenommen wurden, können die kopierten Blöcke im Bereich "Diff" kombiniert werden. Wenn viele Änderungen vorhanden sind, kann die Kopie-bei-Schreibvorgang-Methode teuer werden.

### <a name="redirect-on-write-method"></a>Umleitungs-bei-Schreibvorgang-Methode

Wenn das ursprüngliche Volume (e/a-Anforderung), Änderungen empfängt, wird in der umleitungs-bei-Schreibvorgang-Methode nicht die Änderung auf das ursprüngliche Volume angewendet. Stattdessen wird die Änderung in ein anderes Volume Schattenkopie-Speicherbereich geschrieben.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Uhrzeit</th>
<th>Quelldaten (Status und Daten)</th>
<th>Schattenkopie (Status und Daten)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>Originaldaten: 1 2 3 4 5</p></td>
<td><p>Keine Kopie::</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>Die Daten im Cache geändert: 3, 3'</p></td>
<td><p>Schattenkopieclient erstellt (nur unterschieden): 3’</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>Ursprünglichen Daten unverändert: 1 2 3 4 5</p></td>
<td><p>Unterschiede und Index auf der Schattenkopie gespeichert: 3’</p></td>
</tr>
</tbody>
</table>

**Tabelle 2**   der umleitungs-bei-Schreibvorgang-Methode zum Erstellen von Schattenkopien

Wie bei der Kopie-bei-Schreibvorgang-Methode ist die umleitungs-bei-Schreibvorgang-Methode eine schnelle Methode zum Erstellen einer Schattenkopie, da diese nur Änderungen an den Daten kopiert. Die kopierte Blöcke im Bereich "Diff" können mit die unveränderten Daten auf das ursprüngliche Volume, erstellen Sie eine vollständige und aktuelle Kopie der Daten kombiniert werden. Wenn viele Lese e/a-Anforderungen, kann die umleitungs-bei-Schreibvorgang-Methode teuer werden.

## <a name="shadow-copy-providers"></a>Volumeschattenkopie-Anbieter

Es gibt zwei Arten von Schattenkopieanbieter: hardwarebasierte und Software-basierten Anbieter. Es gibt auch ein Systemanbieter, der ein Softwareanbieter von ist, der für das Windows-Betriebssystem enthalten ist.

### <a name="hardware-based-providers"></a>Hardware-basierte Anbieter

Hardware-basierte Schattenkopie Kopie Anbieter Act als Schnittstelle zwischen der Volumeschattenkopie-Dienst und der Hardware-Ebene, durch die Arbeit in Verbindung mit einem Hardware-Storage-Adapter oder den Controller. Das Erstellen und verwalten die Schattenkopie vom Speicherarray erfolgt.

Hardwareanbieter immer die Schattenkopie von einer gesamten LUN erstellen, aber der Volumeschattenkopie-Dienst stellt nur die Schattenkopie des Datenträgers oder Volumes, die angefordert wurden.

Eine hardwarebasierte Schattenkopieanbieter nutzt den Volumeschattenkopie-Dienst ermöglicht die datensynchronisierung, verwaltet die Schattenkopie und bietet eine allgemeine Schnittstelle und sicherungsanwendungen Funktionen, die den Punkt definiert, in der Zeit. Der Volumeschattenkopie-Dienst ist jedoch nicht den zugrunde liegende Mechanismus angeben, mit dem der Hardware-basierte Provider erstellt und verwaltet Schattenkopien.

### <a name="software-based-providers"></a>Software-basierte Anbieter

Softwarebasierte Volumeschattenkopie-Anbieter in der Regel abzufangen und zu verarbeiten lesen und Schreiben e/a-Anforderungen in einer Softwareschicht, die zwischen dem Dateisystem und die Volume-Manager-Clientsoftware.

Diese Anbieter werden als Benutzermodus-DLL-Komponente und mindestens eine Kernelmodus-Gerätetreiber in der Regel ein Storage-Filtertreiber implementiert. Im Gegensatz zu Hardware-basierte Anbieter erstellen Sie Software-basierte Anbieter Schattenkopien auf Softwareebene, nicht der Hardware-Ebene.

Eine softwarebasierte Schattenkopieanbieter muss eine "Point-in-Time" Ansicht eines Volumes verwalten, durch den Zugriff auf ein Dataset, das zum Neuerstellen Status des Volumes vor der Erstellung der Schattenkopiezeit verwendet werden kann. Ein Beispiel ist das Verfahren Kopie-bei-Schreibvorgang-System-Anbieter. Der Volumeschattenkopie-Dienst sorgt jedoch keine Einschränkungen verwendeten Technik werden die softwarebasierte-Anbieter verwenden, erstellen und Verwalten von Schattenkopien.

Ein Softwareanbieter gilt für eine größere Zahl von Storage-Plattformen als ein Hardware-basierte Anbieter, und es sollte funktionieren mit grundlegenden Datenträgern oder logischen Volumes ebenso gut. (Logisches Volume ist ein Volume, das durch die Kombination von freien Speicherplatzes von mindestens zwei Datenträger erstellt wird.) Im Gegensatz zu Hardwareschattenkopien nutzen die Softwareanbietern Betriebssystemressourcen, um die Schattenkopie zu gewährleisten.

Weitere Informationen zu Basisdatenträger, finden Sie unter [was grundlegende Datenträger und Volumes sind?](http://go.microsoft.com/fwlink/?linkid=180894) (http://go.microsoft.com/fwlink/?LinkId=180894) auf TechNet.

### <a name="system-provider"></a>System-Anbieter

Eine Schattenkopie-Anbieter, der Anbieter wird im Windows-Betriebssystem bereitgestellt. Zwar ein Standardanbieter in Windows bereitgestellt wird, können andere Anbieter Implementierungen bereitstellen, die für ihre Hardware und Software Storage-Anwendungen optimiert sind.

Um die Ansicht "Point-in-Time" eines Volumes zu gewährleisten, die in einer Schattenkopie enthalten ist, verwendet der System-Anbieter ein Kopie-bei-Schreibvorgang-Verfahren. Kopien von den Blöcken auf Volumes, die seit dem Beginn der Erstellung von Schattenkopien geändert wurden, werden in einer Schattenkopie-Speicherbereich gespeichert.

System-Anbieter kann das Produktionsvolume verfügbar machen, die geschrieben und normalerweise aus gelesen werden kann. Wenn die Schattenkopie benötigt wird, gilt sie logisch Unterschiede Daten unter dem Produktionsvolume, um die vollständige Schattenkopie verfügbar zu machen.

Für den Systemanbieter muss die Schattenkopie-Speicherbereich auf einem NTFS-Volume sein. Das Volume zu spiegelnde muss nicht auf einem NTFS-Volume sein, aber mindestens ein Volume auf dem System bereitgestellt, muss ein NTFS-Volume sein.

Die Komponentendateien, aus denen der Systemanbieter sind swprv.dll und volsnap.sys.

### <a name="in-box-vss-writers"></a>Mitgelieferte VSS-Writer

Das Windows-Betriebssystem umfasst eine Reihe von VSS-Writer, die verantwortlich für das Auflisten der Daten, die von verschiedenen Windows-Features erforderlich sind.

Weitere Informationen zu diesen Writern finden Sie unter den folgenden Microsoft-Websites:

  - [Mitgelieferte VSS-Writer](http://go.microsoft.com/fwlink/?linkid=180895) ()http://go.microsoft.com/fwlink/?LinkId=180895)  
      
  - [Neue integrierte VSS-Writer für WindowsServer 2008 und Windows Vista SP1](http://go.microsoft.com/fwlink/?linkid=180896) ()http://go.microsoft.com/fwlink/?LinkId=180896)  
      
  - [Neue integrierte VSS-Writer für Windows Server 2008 R2 und Windows 7](http://go.microsoft.com/fwlink/?linkid=180897) ()http://go.microsoft.com/fwlink/?LinkId=180897)  
      

## <a name="how-shadow-copies-are-used"></a>Verwendung von Schattenkopien

Zusätzlich zum Sichern von Daten und Systemeinstellungen Statusinformationen zu Anwendungen, können Schattenkopien für unterschiedliche Zwecke, einschließlich der folgenden verwendet werden:

  - Wiederherstellen von LUNs (LUN bei der erneuten Synchronisierung und LUN-Austausch)  
      
  - Die Wiederherstellung einzelner Dateien (Schattenkopien für freigegebene Ordner)  
      
  - Datamining mit übertragbarer Schattenkopien  
      

### <a name="restoring-luns-lun-resynchronization-and-lun-swapping"></a>Wiederherstellen von LUNs (LUN bei der erneuten Synchronisierung und LUN-Austausch)

In Windows Server 2008 R2 und Windows 7 können VSS anfordernde Personen eine Hardware-Anbieter namens LUN neusynchronisierung (oder "Neusynchronisierung" LUN ") Schattenkopiefunktion. Dies ist ein Recovery-Fast-Schema, das ein Anwendungsadministrator, Daten aus einer Schattenkopie, auf die ursprüngliche LUN oder eine neue LUN wiederherzustellen zu können.

Die Schattenkopie kann es sich um ein vollständiger Klon oder eine differenzielle Schattenkopie sein. In beiden Fällen am Ende den Vorgang zur neusynchronisierung müssen die Ziel-LUN den gleichen Inhalt wie die Schattenkopie LUN. Während der Vorgang zur neusynchronisierung führt das Array aus der Schattenkopie eine Kopie auf Blockebene an die Ziel-LUN aus.


> [!NOTE]
> Die Schattenkopie muss es sich um eine Schattenkopie übertragbarer Hardware sein. 
<br>


Die meisten Arrays können Produktion e/a-Vorgänge fortgesetzt werden, kurz nach der Vorgang zur neusynchronisierung beginnt. Während der Vorgang zur neusynchronisierung ausgeführt wird, lesen Sie, dass Anforderungen an die Schattenkopie LUN umgeleitet werden, und Schreibanforderungen an die Ziel-LUN. Dadurch können Arrays zum Wiederherstellen von sehr großen Datasets und normale Vorgänge in mehrere Sekunden fortgesetzt.

LUN bei der erneuten Synchronisierung unterscheidet sich von der LUN-Austausch. Ein LUN-Austausch ist eine schnelle Wiederherstellung-Szenario, die VSS seit Windows Server 2003 SP1 unterstützt hat. In einem LUN-Austausch ist die Schattenkopie importiert, und klicken Sie dann in ein Lese-/ Schreibzugriff Volume konvertiert. Die Konvertierung ist ein unumkehrbarer Vorgang, und des Umfangs und der zugrunde liegenden LUN kann nicht mit den VSS-APIs, gesteuert werden. Die folgende Liste beschreibt, wie die LUN bei der erneuten Synchronisierung mit der LUN-Austausch vergleicht:

  - LUN neusynchronisierung ist die Schattenkopie nicht geändert, damit er mehrere Male verwendet werden kann. In der LUN ausgetauscht wurde, kann die Schattenkopie nur einmal für eine Wiederherstellung verwendet werden. Für die Administratoren am häufigsten Sicherheit preisbewusste ist dies wichtig. Wenn die LUN bei der erneuten Synchronisierung verwendet wird, kann die anfordernde Person den gesamten Wiederherstellungsvorgang wiederholen, wenn ein Fehler erstmals auftritt.  
      
  - Am Ende einen LUN-Austausch wird die Schattenkopie-LUN für Produktions-e/a-Anforderungen verwendet. Aus diesem Grund muss die Schattenkopie LUN verwenden die gleiche Qualität des Speichers als der ursprünglichen Produktions-LUN um sicherzustellen, dass die Leistung nicht beeinträchtigt wird, nachdem der Wiederherstellungsvorgang. Wenn die LUN bei der erneuten Synchronisierung stattdessen verwendet wird, kann der Hardwareanbieter die Schattenkopie im Speicher verwalten, die weniger Kosten als Produktionsqualität Speicher.  
      
  - Wenn das Ziel der LUN kann nicht verwendet werden und muss neu erstellt werden, möglicherweise LUN-Austausch wirtschaftlicher sein, da er nicht, dass ein Ziel-LUN erfordert.  
      


> [!WARNING]
> Alle der aufgeführten Vorgänge sind Vorgänge auf LUN. Wenn Sie versuchen, ein bestimmtes Volume wiederherstellen, indem Sie die LUN bei der erneuten Synchronisierung verwenden, möchten Sie unwissentlich die anderen Volumes wiederherstellen, die die LUN verwenden. 
<br>


### <a name="restoring-individual-files-shadow-copies-for-shared-folders"></a>Die Wiederherstellung einzelner Dateien (Schattenkopien für freigegebene Ordner)

Schattenkopien für freigegebene Ordner verwendet den Volumeschattenkopie-Dienst zu Point-in-Time-Kopien der Dateien, die befinden, auf eine freigegebene Netzwerkressource, z. B. einem Dateiserver. Mit Schattenkopien von freigegebenen Ordnern können Benutzer schnell gelöschten oder geänderte Dateien wiederherstellen, die im Netzwerk gespeichert sind. Da dies ohne Unterstützung durch den Administrator erfolgen kann, können Schattenkopien für freigegebene Ordner die Produktivität zu steigern und Verwaltungskosten reduziert werden.

Weitere Informationen zu Schattenkopien von freigegebenen Ordnern finden Sie unter [Schattenkopien für freigegebene Ordner](http://go.microsoft.com/fwlink/?linkid=180898) (http://go.microsoft.com/fwlink/?LinkId=180898) auf TechNet.

### <a name="data-mining-by-using-transportable-shadow-copies"></a>Datamining mit übertragbarer Schattenkopien

Mit einem Hardware-Anbieter, der für die Verwendung mit dem Volumeschattenkopie-Dienst entwickelt wurde, können Sie übertragbarer Schattenkopien erstellen, die auf Servern innerhalb der gleichen Subsystem (z. B. ein SAN) importiert werden kann. Diese Schattenkopien können zum Seeding für einer produktionsumgebung, oder testen die Installation mit schreibgeschützten Daten für Datamining verwendet werden.

Mit dem Volumeschattenkopie-Dienst und ein Speicherarray mit einem Hardware-Anbieter, der für die Verwendung mit dem Volumeschattenkopie-Dienst entwickelt wurde, ist es möglich, erstellen eine Schattenkopie des Quellvolumes Daten auf einem Server, und klicken Sie dann Importieren der Schattenkopie auf einem anderen server  (oder mit dem gleichen Server sichern). Dieser Vorgang erfolgt in wenigen Minuten, unabhängig von der Größe der Daten. Der Transport-Prozess erfolgt über eine Reihe von Schritten, die einen Schatten Kopie anfordernden (eine Speicher-Management-Anwendung) zu verwenden, der übertragbarer Schattenkopien unterstützt.

## <a name="to-transport-a-shadow-copy"></a>Um eine Schattenkopie zu transportieren.

1.  Erstellen Sie eine Kopie von übertragbarer Schattenkopien für die Quelldaten auf einem Server.

2.  Importieren Sie die Schattenkopie zu einem Server, der mit dem SAN verbunden ist (Sie können auf einen anderen Server oder dem gleichen Server importieren).

3.  Die Daten sind jetzt bereit, die verwendet werden.

![](media/volume-shadow-copy-service/Ee923636.633752e0-92f6-49a7-9348-f451b1dc0ed7(WS.10).jpg)

**Abbildung 3**   Erstellen von Schattenkopien und Transport zwischen zwei Servern


> [!NOTE]
> Übertragbarer Schattenkopien, die unter Windows Server 2003 erstellt wird, kann nicht auf einem Server mit Windows Server 2008 oder Windows Server 2008 R2 importiert werden. Übertragbarer Schattenkopien, die auf Windows Server 2008 oder Windows Server 2008 R2 erstellt wurde, kann nicht auf einen Server importiert werden, auf denen Windows Server 2003 ausgeführt wird. Allerdings kann eine Schattenkopie, die unter Windows Server 2008 erstellt wird auf einem Server importiert werden, auf denen Windows Server 2008 R2 und umgekehrt ausgeführt wird. 
<br>


Schattenkopien sind schreibgeschützt. Wenn Sie eine Schattenkopie einer LUN mit Lese-/Schreibzugriff konvertieren möchten, können Sie eine VDS-basierten Speicher-Management-Anwendung (einschließlich einiger anfordernde Personen) zusätzlich zu den Volumeschattenkopie-Dienst. Durch die Verwendung dieser Anwendung können Sie die Schattenkopie aus der Volume Shadow Copy Service-Verwaltung entfernen und konvertieren Sie ihn in eine LUN mit Lese-/Schreibzugriff.

Volume Shadow Copy Service Transport ist eine fortschrittliche Lösung auf Computern unter Windows Server 2003 Enterprise Edition, Windows Server 2003 Datacenter Edition, Windows Server 2008 oder Windows Server 2008 R2. Dies funktioniert nur bei ein Hardware-Anbieter auf dem Speicherarray. Shadow Copy Transport kann für unterschiedliche Zwecke, einschließlich bandsicherungen, Data mining, und Testen verwendet werden.

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

Diese häufig gestellten Fragen beantwortet Fragen zu Volume Shadow Copy Service (VSS) für Systemadministratoren. Informationen zu VSS-Anwendungsprogrammierschnittstellen, finden Sie unter [Volume Shadow Copy Service](http://go.microsoft.com/fwlink/?linkid=180899) (http://go.microsoft.com/fwlink/?LinkId=180899) in der Windows Developer Center-Bibliothek.

### <a name="when-was-volume-shadow-copy-service-introduced-on-which-windows-operating-system-versions-is-it-available"></a>Wenn eingeführte Volumeschattenkopie-Dienst? Dazu, welche Versionen der Windows-Betriebssystem ist es verfügbaren?

VSS wurde in Windows XP eingeführt. Es ist auf Windows XP, Windows Server 2003, Windows Vista®, Windows Server 2008, Windows 7 und Windows Server 2008 R2 verfügbar.

### <a name="what-is-the-difference-between-a-shadow-copy-and-a-backup"></a>Was ist der Unterschied zwischen einer Schattenkopie und eine Sicherung?

Im Fall von einer Sicherung des Festplattenlaufwerks ist die Schattenkopie erstellt auch die Sicherung. Daten können aus der Schattenkopie für eine Wiederherstellung kopiert werden, oder die Schattenkopie für ein Szenario für die schnelle Wiederherstellung verwendet werden – beispielsweise bei der erneuten Synchronisierung LUN oder LUN-Austausch.

Wenn Daten aus der Schattenkopie auf Band oder anderen Wechselmedien kopiert werden, bildet der Inhalt, der auf den Medien gespeichert ist die Sicherung aus. Die Schattenkopie selbst kann gelöscht werden, nachdem die Daten daraus kopiert werden.

### <a name="what-is-the-largest-size-volume-that-volume-shadow-copy-service-supports"></a>Was ist die größte Größe-Volume, das Volume Shadow Copy Service unterstützt?

Volumeschattenkopie-Dienst unterstützt eine Volumegröße von bis zu 64 TB.

### <a name="i-made-a-backup-on-windows-server2008-can-i-restore-it-on-windows-server2008r2"></a>Mir eine Sicherung unter Windows Server 2008. Kann ich es auf Windows Server 2008 R2 wiederherstellen?

Es hängt von der Sicherungssoftware, die Sie verwendet. Die meisten Sicherungsprogramme unterstützen dieses Szenario, für die Daten jedoch nicht für Sicherungen des Systemstatus.

Schattenkopien, die auf der folgenden Versionen von Windows erstellt werden, können auf dem anderen verwendet werden.

### <a name="i-made-a-backup-on-windows-server2003-can-i-restore-it-on-windows-server2008"></a>Mir eine Sicherung unter Windows Server 2003. Kann ich es unter Windows Server 2008 wiederherstellen?

Es hängt von der Sicherungssoftware, die Sie verwendet. Bei der Erstellung einer Schattenkopie unter Windows Server 2003 kann nicht unter Windows Server 2008 Verwendung. Bei der Erstellung einer Schattenkopie unter Windows Server 2008 können keine Sie es auch unter Windows Server 2003 wiederherstellen.

### <a name="how-can-i-disable-vss"></a>Wie kann ich VSS deaktivieren?

Es ist möglich, die den Volumeschattenkopie-Dienst zu deaktivieren, indem Sie mit der Microsoft Management Console. Allerdings sollten Sie dies nicht tun. Deaktivieren von VSS negativ und wirkt sich auf jegliche Software, die Sie verwenden, die von, z. B. die Systemwiederherstellung und Windows Server-Sicherung abhängig ist.

Weitere Informationen finden Sie unter den folgenden Websites der Microsoft TechNet-Website:

  - [Systemwiederherstellung](http://go.microsoft.com/fwlink/?linkid=157113) ()http://go.microsoft.com/fwlink/?LinkID=157113)  
      
  - [Windows Server-Sicherung](http://go.microsoft.com/fwlink/?linkid=180891) ()http://go.microsoft.com/fwlink/?LinkID=180891)  
      

### <a name="can-i-exclude-files-from-a-shadow-copy-to-save-space"></a>Können Dateien aus einer Schattenkopie um Platz zu sparen werden ausgeschlossen?

VSS wurde entwickelt, um Schattenkopien des gesamten Volumes zu erstellen. Temporäre Dateien, z. B. Auslagerungsdateien, werden automatisch von Schattenkopien, um Platz zu sparen weggelassen.

Um bestimmte Dateien von Schattenkopien auszuschließen, verwenden Sie den folgenden Registrierungsschlüssel: **FilesNotToSnapshot**.


> [!NOTE]
> Die <STRONG>FilesNotToSnapshot</STRONG> Registrierungsschlüssel nur von Anwendungen verwendet werden soll. Benutzer, die versuchen, ihn zu verwenden, treten Einschränkungen wie z. B. Folgendes:
> <br>
> <UL>
> <LI>Es kann nicht aus einer Schattenkopie Dateien gelöscht werden, die auf einem Windows Server erstellt wurde, mithilfe der Funktion für die früheren Versionen.<BR><BR>
> <LI>Es kann keine Dateien von Schattenkopien für freigegebene Ordner löschen.<BR><BR>
> <LI>Können sie Dateien löschen, aus einer Schattenkopie, das erstellt wurde die <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow" data-raw-source="[Diskshadow](https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow)">Diskshadow</a> Dienstprogramm, aber es kann nicht löschen Sie Dateien aus einer Schattenkopie, das erstellt wurde die <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin" data-raw-source="[Vssadmin](https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin)">Vssadmin</a> Hilfsprogramm.<BR><BR>
> <LI>Dateien werden aus einer Schattenkopie Best-Effort-Basis gelöscht. Dies bedeutet, dass sie nicht garantiert werden, gelöscht werden soll.<BR><BR></LI></UL>


Weitere Informationen finden Sie unter [Ausschließen von Dateien aus Schattenkopien](http://go.microsoft.com/fwlink/?linkid=180904) (http://go.microsoft.com/fwlink/?LinkId=180904) auf MSDN.

### <a name="my-non-microsoft-backup-program-failed-with-a-vss-error-what-can-i-do"></a>Mein Sicherungsprogramm nicht von Microsoft bei der VSS-Fehler. Was kann ich tun?

Überprüfen Sie den Produkt-Support-Abschnitt der Website des Unternehmens, die Sicherung erstellt. Es gibt möglicherweise ein Produktupdate, die Sie herunterladen und installieren, um das Problem zu beheben. Wenn dies nicht der Fall ist, wenden Sie sich an das Produkt unterstützt Abteilung.

Systemadministratoren können die VSS-Informationen zur Problembehandlung auf der Website Microsoft TechNet-Bibliothek verwenden, zum Sammeln von Diagnoseinformationen über VSS-bezogene Probleme.

Weitere Informationen finden Sie unter [Volume Shadow Copy Service](http://go.microsoft.com/fwlink/?linkid=180905) (http://go.microsoft.com/fwlink/?LinkId=180905) auf TechNet.

### <a name="what-is-the-diff-area"></a>Was ist der "Vergleichsbereich"?

Die Schattenkopie-Speicherbereich (oder der "Vergleichsbereich") ist der Speicherort die Daten für die Schattenkopie, die von der System-Software-Anbieter erstellt wird.

### <a name="where-is-the-diff-area-located"></a>Wo befindet sich die Vergleichsbereich?

Die Vergleichsbereich kann auf alle lokalen Volume befinden. Allerdings müssen sie auf einem NTFS-Volume befinden, die ausreichend Speicherplatz zum Speichern.

### <a name="how-is-the-diff-area-location-determined"></a>Wie wird der Diff-Bereich-Speicherort ab, der ein?

In dieser Reihenfolge aus, um zu bestimmen, den Speicherort der Diff-Bereich werden die folgenden Kriterien ausgewertet:

  - Wenn ein Volume bereits einen vorhandenen Schattenkopie wurde, wird dieser Speicherort verwendet.  
      
  - Wenn eine vorkonfigurierte manuelle Zuordnung zwischen dem ursprünglichen Volume und des Speicherortes der Volumeschattenkopie, vorhanden ist, und klicken Sie dann diesen Speicherort verwendet wird.  
      
  - Wenn die vorherigen beiden Kriterien keinen Speicherort angeben, wählt der Volumeschattenkopie-Dienst einen Speicherort, der basierend auf verfügbaren freien Speicherplatz. Wenn Sie mehrere Volumes Schattenkopien erstellt werden, erstellt der Volumeschattenkopie-Dienst eine Liste der möglichen momentaufnahmespeicherorte basierend auf der Größe des freien Speicherplatzes, in absteigender Reihenfolge. Die Anzahl der Standorte ist gleich der Anzahl der Volumes, die gespiegelt wird.  
      
  - Wenn das Volume, die gespiegelt wird einer der möglichen Speicherorte ist, wird eine lokale Zuordnung erstellt. Andernfalls wird eine Zuordnung mit dem Volume mit dem meisten verfügbaren Speicherplatz erstellt.  
      

### <a name="can-vss-create-shadow-copies-of-non-ntfs-volumes"></a>Kann VSS Schattenkopien von nicht-NTFS-Volumes erstellen?

Ja. Persistente Schattenkopien können jedoch nur für NTFS-Volumes erfolgen. Darüber hinaus muss mindestens ein Volume auf dem System bereitgestellt, einem NTFS-Volume sein.

### <a name="whats-the-maximum-number-of-shadow-copies-i-can-create-at-one-time"></a>Was ist die maximale Anzahl von Schattenkopien, die ich auf einmal erstellen können?

Die maximale Anzahl von Volumes von Schattenkopien in einer einzelnen Schattenkopiesatz ist 64. Beachten Sie, dass dies nicht der Anzahl von Schattenkopien identisch ist.

### <a name="whats-the-maximum-number-of-software-shadow-copies-created-by-the-system-provider-that-i-can-maintain-for-a-volume"></a>Was ist die maximale Anzahl von Softwareschattenkopien vom Systemanbieter erstellt, die ich für ein Volume verwalten kann?

Die maximal zulässige Anzahl ist Software Schattenkopien für jedes Volume 512. Allerdings können standardmäßig nur 64 Schattenkopien verwaltet werden, die von der Funktion für die Schattenkopien von freigegebenen Ordnern verwendet werden. Um den Grenzwert für die Schattenkopien von freigegebenen Ordnern-Funktion zu ändern, verwenden Sie den folgenden Registrierungsschlüssel: **MaxShadowCopies**.

### <a name="how-can-i-control-the-space-that-is-used-for-shadow-copy-storage-space"></a>Wie kann ich den Speicherplatz steuern, der für die Schattenkopie-Speicherplatz verwendet wird?

Typ der **Vssadmin Größe Shadowstorage** Befehl.

Weitere Informationen finden Sie unter [Vssadmin Größe Shadowstorage](http://go.microsoft.com/fwlink/?linkid=180906) (http://go.microsoft.com/fwlink/?LinkId=180906) auf TechNet.

### <a name="what-happens-when-i-run-out-of-space"></a>Was geschieht, wenn ich keinen Speicherplatz mehr?

Schattenkopien für das Volume werden gelöscht, die älteste Schattenkopie ab.

## <a name="volume-shadow-copy-service-tools"></a>Volume Shadow Copy Service-Tools

Das Windows-Betriebssystem bietet die folgenden Tools zum Arbeiten mit VSS:

  - [DiskShadow](http://go.microsoft.com/fwlink/?linkid=180907) (http://go.microsoft.com/fwlink/?LinkId=180907)  
      
  - [VssAdmin](http://go.microsoft.com/fwlink/?linkid=84008) (http://go.microsoft.com/fwlink/?LinkId=84008)  
      

### <a name="diskshadow"></a>DiskShadow

DiskShadow ist eine VSS-anforderer, die Sie verwenden können, alle Hardware- und Momentaufnahmen zu verwalten, die Sie auf einem System verwenden können. DiskShadow umfasst Befehle wie im folgenden:

  - **list**: Listet VSS-Writer, VSS-Anbieter und Schattenkopien  
      
  - **create**: Erstellt eine neue Schattenkopie  
      
  - **import**: Importiert eine übertragbarer Schattenkopien  
      
  - **verfügbar machen**: Stellt eine permanente Schattenkopie (wie einem Laufwerksbuchstaben, z. B.)  
      
  - **revert**: Setzt ein Volume an einer angegebenen Schattenkopie  
      

Dieses Tool ist für die Verwendung von IT-Experten vorgesehen, aber Entwickler auch es könnte hilfreich beim Testen einer VSS Writer oder VSS-Anbieter.

DiskShadow ist nur unter Windows Server-Betriebssystemen verfügbar. Es ist nicht auf Windows-Clientbetriebssystemen verfügbar.

### <a name="vssadmin"></a>VssAdmin

VssAdmin dient zum Erstellen, löschen und Auflisten von Informationen über Schattenkopien. Sie können auch verwendet werden, zum Ändern der Größe der Schattenkopie-Speicherbereich ("Vergleichsbereich").

VssAdmin enthält Befehle wie im folgenden:

  - **Erstellen von Schattenkopien**: Erstellt eine neue Schattenkopie  
      
  - **Löschen Sie Schatten**: Löscht Schattenkopien  
      
  - **Liste von Anbietern**: Listet alle registrierten VSS-Anbieter  
      
  - **Liste der Writer**: Listet alle abonnierten VSS-Writer  
      
  - **Ändern der Größe Shadowstorage**: Ändert die maximale Größe der Schattenkopie-Speicherbereich  
      

VssAdmin kann nur verwendet werden, um Schattenkopien zu verwalten, die von der System-Software-Anbieter erstellt werden.

VssAdmin ist auf Windows-Client und dem Betriebssystem Windows Server-Versionen verfügbar.

## <a name="volume-shadow-copy-service-registry-keys"></a>Registrierungsschlüssel für den Volume Shadow Copy-Dienst

Die folgenden Registrierungsschlüssel sind für die Verwendung mit VSS verfügbar:

  - **VssAccessControl**  
      
  - **MaxShadowCopies**  
      
  - **MinDiffAreaFileSize**  
      

### <a name="vssaccesscontrol"></a>VssAccessControl

Dieser Schlüssel wird verwendet, um anzugeben, welche Benutzer Zugriff auf Schattenkopien haben.

Weitere Informationen finden Sie auf der MSDN-Website die folgenden Einträge:

  - [Sicherheitsüberlegungen für Autoren](http://go.microsoft.com/fwlink/?linkid=157739) ()http://go.microsoft.com/fwlink/?LinkId=157739)  
      
  - [Überlegungen zur Sicherheit für anfordernde Personen](http://go.microsoft.com/fwlink/?linkid=180908) ()http://go.microsoft.com/fwlink/?LinkId=180908)  
      

### <a name="maxshadowcopies"></a>MaxShadowCopies

Dieser Schlüssel gibt die maximale Anzahl von Clients zugängliche Schattenkopien, die auf jedem Volume des Computers gespeichert werden können. Clients zugängliche Schattenkopien werden von Schattenkopien für freigegebene Ordner verwendet.

Weitere Informationen finden Sie auf der MSDN-Website unter den folgenden Eintrag:

**MaxShadowCopies** unter [Registrierungsschlüssel für die Sicherung und Wiederherstellung](http://go.microsoft.com/fwlink/?linkid=180909) ()http://go.microsoft.com/fwlink/?LinkId=180909)

### <a name="mindiffareafilesize"></a>MinDiffAreaFileSize

Dieser Schlüssel gibt die anfängliche minimale Größe in MB, von der Schattenkopie-Speicherbereich.

Weitere Informationen finden Sie auf der MSDN-Website unter den folgenden Eintrag:

**MinDiffAreaFileSize** unter [Registrierungsschlüssel für die Sicherung und Wiederherstellung](http://go.microsoft.com/fwlink/?linkid=180910) ()http://go.microsoft.com/fwlink/?LinkId=180910)

`##`#' Unterstützten Betriebssystemversionen

Die folgende Tabelle enthält die minimalen unterstützten Betriebssystemversionen für VSS-Funktionen.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>VSS-Funktion</th>
<th>Unterstützte Mindestversion (Client)</th>
<th>Unterstützte Mindestversion (Server)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bei der erneuten Synchronisierung LUN</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2008 R2</p></td>
</tr>
<tr class="even">
<td><p><strong>FilesNotToSnapshot</strong> Registrierungsschlüssel</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td><p>Übertragbarer Schattenkopien</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003 mit SP1</p></td>
</tr>
<tr class="even">
<td><p>Hardwareschattenkopien</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>Frühere Versionen von Windows Server</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="even">
<td><p>Schnelle Wiederherstellung mithilfe der LUN-Austausch</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2003 mit SP1</p></td>
</tr>
<tr class="odd">
<td><p>Mehrere importiert der Hardwareschattenkopien</p>
<div class="alert">
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="media/volume-shadow-copy-service/Dd560667.note(WS.10).gif" />Hinweis</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Dies ist die Möglichkeit, eine Schattenkopie mehrmals zu importieren. Nur eine Importvorgang kann zu einem Zeitpunkt ausgeführt werden.
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
<td><p>Übertragbarer automatisch wiederhergestellte Schattenkopien.</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>Gleichzeitige Sicherung Sitzungen (bis zu 64)</p></td>
<td><p>Windows XP</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>Einzelne wiederherstellungssitzung mit Sicherungen</p></td>
<td><p>Windows Vista</p></td>
<td><p>WindowsServer 2003 mit SP2</p></td>
</tr>
<tr class="even">
<td><p>Bis zu 8 Restore-Sitzungen gleichzeitig mit der Sicherungen</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows Server 2003 R2</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>Siehe auch

[Volumeschattenkopie-Dienst im Windows Developer Center](https://docs.microsoft.com/windows/desktop/vss/volume-shadow-copy-service-overview)