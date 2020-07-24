---
title: Virtualisieren von Domänen Controllern mithilfe von Hyper-V
description: Überlegungen zur Virtualisierung von Windows Server Active Directory-Domäne-Controllern in Hyper-V
author: MicrosoftGuyJFlo
ms.author: joflore
ms.date: 04/19/2018
ms.topic: article
ms.prod: windows-server
ms.openlocfilehash: 2a4d743f05d9a8cd70197b7a70589ce7eac84273
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966242"
---
# <a name="virtualizing-domain-controllers-using-hyper-v"></a>Virtualisieren von Domänen Controllern mithilfe von Hyper-V

> Gilt für: Windows Server 2016

Dieses Thema wird aktualisiert, um die Richtlinien für Windows Server 2016 zu übernehmen. Windows Server 2012 führt viele Verbesserungen für virtualisierte Domänen Controller (DCS) ein, einschließlich Sicherheitsvorkehrungen, um das USN-Rollback auf virtuellen DCS und die Möglichkeit zum Klonen virtueller DCS zu verhindern. Weitere Informationen zu diesen Verbesserungen finden [Sie unter Introduction to Active Directory Domain Services (AD DS) Virtualization (Level 100)](../../introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100.md).

Hyper-V konsolidiert verschiedene Server Rollen auf einem einzelnen physischen Computer. In diesem Leitfaden wird beschrieben, wie Domänencontroller als 32-Bit- oder 64-Bit-Gastbetriebssysteme ausgeführt werden.

## <a name="planning-to-virtualize-domain-controllers"></a>Überlegungen zur Planung für virtualisierte Domänencontroller

Themen dieses Abschnitts sind die Hardwareanforderungen für Hyper-V-Server, die Vermeidung einzelner Fehlerquellen (Single Points of Failure, SPOFs), die Auswahl des geeigneten Konfigurationstyps für die Server und virtuellen Computer der Hyper-V-Umgebung sowie Überlegungen zur Sicherheit und Leistung.

## <a name="hyper-v-requirements"></a>Hyper-V-Anforderungen

Zum Installieren und Verwenden der Hyper-V-Rolle benötigen Sie Folgendes:

   - **Ein x64-Prozessor**
      - Hyper-V ist in x64-basierten Versionen von Windows Server 2008 oder höher verfügbar.  
   - **Hardwareunterstützte Virtualisierung**
      - Dieses Feature ist für Prozessoren mit Virtualisierungsoption (Intel Virtualization Technology (Intel VT) oder AMD Virtualization (AMD-V)) verfügbar.  
   - **Hardware-Datenausführungsschutz (DEP)**
      - Die Hardware-DEP muss verfügbar und aktiviert sein. Das heißt, Sie müssen Intel XD-Bit (Execute Disable Bit) oder AMD NX-Bit (No Execute Bit) aktivieren.  

## <a name="avoid-creating-single-points-of-failure"></a>Vermeidung einzelner Fehlerquellen

Bei der Planung für die Bereitstellung virtualisierter Domänencontroller sollten Sie darauf achten, einzelne Fehlerquellen (d. h. Komponenten, deren Ausfall den Ausfall des gesamten Systems verursachen würde) möglichst zu vermeiden. Zu diesem Zweck empfiehlt es sich, Systemredundanz vorzusehen. Erwägen Sie beispielsweise die folgenden Empfehlungen (unter Berücksichtigung der potenziell höheren Verwaltungskosten):

1. Führen Sie mindestens zwei virtualisierte Domänencontroller pro Domäne auf anderen Virtualisierungshosts aus. Dadurch wird das Risiko verringert, bei Ausfall eines Virtualisierungshosts alle Domänencontroller zu verlieren.  
2. Verwenden Sie zur Ausführung der Domänencontroller unterschiedliche Hardware (z. B. unterschiedliche CPUs, Hauptplatinen oder Netzwerkadapter), wie auch für andere Technologien empfohlen. Dadurch minimieren Sie Auswirkungen von Fehlfunktionen, die auf bestimmte Elemente (z. B. Anbieterkonfigurationen, Treiber, Hardwaremodelle oder Hardwaretypen) beschränkt sind.  
3. Domänencontroller sollten möglichst auf Hardware ausgeführt werden, die sich in unterschiedlichen geografischen Regionen befindet. Dies verringert die Auswirkungen von Notfällen oder Fehlern an einem bestimmten Standort, an dem Domänencontroller gehostet werden.  
4. Versehen Sie all Ihre Domänen mit physischen Domänencontrollern. Dies verringert die Auswirkungen einer Fehlfunktion einer Virtualisierungsplattform (von der auch die von der Plattform abhängigen Hostsysteme betroffen wären).  

## <a name="security-considerations"></a>Sicherheitshinweise

Der Hostcomputer, auf dem die virtuellen Domänencontroller ausgeführt werden, muss ebenso sorgfältig wie ein beschreibbarer Domänencontroller verwaltet werden, selbst wenn es sich nur um ein Domänenmitglied oder einen Arbeitsgruppencomputer handelt. Dies ist ein wichtiger Sicherheitsaspekt. Ein unzureichend verwalteter Host ist anfällig für Rechteerweiterungsangriffe (d. h., ein böswilliger Benutzer verschafft sich Zugriff und erlangt Systemberechtigungen, die nicht autorisiert oder nicht ordnungsgemäß zugewiesen wurden). Durch einen solchen Angriff können alle vom betroffenen Computer gehosteten virtuellen Computer, Domänen und Gesamtstrukturen gefährdet werden.

Berücksichtigen Sie bei der Planung der Virtualisierung von Domänencontrollern unbedingt die folgenden Sicherheitsaspekte:

   - Der lokale Administrator eines Computers, auf dem virtuelle, beschreibbare Domänencontroller gehostet werden, sollte bezüglich der Anmeldeinformationen als gleichwertig betrachtet werden mit dem Standarddomänenadministrator aller Domänen und Gesamtstrukturen, denen die betreffenden Domänencontroller angehören.  
   - Zur Vermeidung von Sicherheits- und Leistungsproblemen wird als Konfiguration empfohlen, auf einem Host eine Server Core-Installation von Windows Server 2008 oder höher mit Hyper-V als einziger Anwendung auszuführen. Je weniger Anwendungen und Dienste auf dem Server installiert sind, desto höher ist die Leistung und desto geringer ist das Risiko von Angriffen auf den Computer oder das Netzwerk über installierte Anwendungen oder Dienste. Diese Art der Konfiguration bietet eine sogenannte reduzierte Angriffsfläche. Für Zweigstellen oder andere Standorte, die nicht ausreichend geschützt werden können, wird ein schreibgeschützter Domänencontroller (Read-Only Domain Controller, RODC) empfohlen. Falls ein separates Verwaltungsnetzwerk vorhanden ist, sollte der Host nur mit dem Verwaltungsnetzwerk verbunden werden.  
   - Sie können BitLocker mit ihren Domänen Controllern verwenden, da Sie Windows Server 2016 verwenden können, um dem Gast Schlüsselmaterial auch das Entsperren des System Volumes zu ermöglichen.
   - [Geschützte Fabric-und abgeschirmte VMS](/it-server/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) können zusätzliche Kontrollen zum Schutz ihrer Domänen Controller bereitstellen.

Weitere Informationen zu RODCs finden [Sie im Planungs-und Bereitstellungs Handbuch für schreibgeschützte Domänen Controller](../../deploy/rodc/read-only-domain-controller-updates.md).

Weitere Informationen zum Sichern von Domänen Controllern finden Sie unter [Leitfaden für bewährte Methoden zum Sichern von Active Directory Installationen](../../plan/security-best-practices/best-practices-for-securing-active-directory.md).

## <a name="security-boundaries-for-different-host-and-guest-configurations"></a>Sicherheitsbegrenzungen für unterschiedliche Host- und Gastkonfigurationen

Die Verwendung virtueller Computer ermöglicht viele verschiedene Konfigurationen von Domänencontrollern. Die Art und Weise, wie virtuelle Computer Begrenzungen und Vertrauensstellungen in Ihrer Active Directory-Topologie beeinflussen, muss sorgfältig berücksichtigt werden. Mögliche Konfigurationen für einen Active Directory-Domänencontroller und -Host (Hyper-V-Server) sowie dessen Gastcomputer (virtuelle Computer, die auf dem Hyper-V-Server ausgeführt werden) werden in der folgenden Tabelle beschrieben:

|Machine|Konfiguration 1|Konfiguration 2|
|-------|---------------|---------------|
|Host|Arbeitsgruppen- oder Mitgliedscomputer|Arbeitsgruppen- oder Mitgliedscomputer|
|Gast|Domänencontroller|Arbeitsgruppen- oder Mitgliedscomputer|

![](media/virtualized-domain-controller-architecture/Dd363553.f44706fd-317e-4f0b-9578-4243f4db225f(WS.10).gif)

   - Der Administrator des Hostcomputers hat hinsichtlich der beschreibbaren Domänencontrollergäste die gleichen Zugriffsrechte wie ein Domänenadministrator und muss als solcher behandelt werden. Bei RODC-Gästen hat der Administrator des Hostcomputers hinsichtlich des Gast-RODCs die gleichen Zugriffsrechte wie ein lokaler Administrator.   
   - Ein Domänencontroller auf einem virtuellen Computer hat Administratorrechte hinsichtlich des Hosts, wenn dieser derselben Domäne angehört. Ein böswilliger Benutzer, der sich zunächst Zugriff auf den virtuellen Computer 1 verschafft, kann alle virtuellen Computer gefährden. Dieses Phänomen wird als Angriffsvektor bezeichnet. Wenn Domänencontroller für mehrere Domänen oder Gesamtstrukturen vorhanden sind, sollten diese Domänen zentral verwaltet werden, wobei der Administrator einer Domäne für alle Domänen als vertrauenswürdig gelten muss.  
   - Die Angriffsmöglichkeit vom virtuellen Computer 1 aus besteht, selbst wenn dieser als RODC installiert wird. Ein RODC-Administrator verfügt zwar nicht explizit über Domänenadministratorrechte, doch der RODC kann zum Senden von Richtlinien an den Hostcomputer verwendet werden. Diese Richtlinien können Startskripts enthalten. Bei erfolgreicher Ausführung des Vorgangs sind der Hostcomputer - und dadurch auch die anderen virtuellen Computer auf dem Hostcomputer - gefährdet.  

## <a name="security-of-vhd-files"></a>Sicherheit von VHD-Dateien

Eine VHD-Datei eines virtuellen Domänencontrollers entspricht der physischen Festplatte eines physischen Domänencontrollers. Daher sollte sie genauso sorgfältig wie die Festplatte eines physischen Domänencontrollers geschützt werden. Stellen Sie sicher, dass nur zuverlässige und vertrauenswürdige Administratoren auf die VHD-Dateien des Domänen Controllers zugreifen können.

## <a name="rodcs"></a>RODCs

Ein Vorteil von RODCs ist, dass sie an Standorten verwendet werden können, an denen die physische Sicherheit nicht garantiert werden kann (z. B. an Zweigstellen). Sie können Windows BitLocker-Laufwerkverschlüsselung verwenden, um VHD-Dateien selbst (nicht die Dateisysteme darin) vor der Beeinträchtigung der physischen Festplatte auf dem Host zu schützen. 

## <a name="performance"></a>Leistung

Mit der neuen Microkernel-64-Bit-Architektur wurde die Leistung von Hyper-V im Vergleich zu früheren Virtualisierungsplattformen erheblich verbessert. Zur Optimierung der Hostleistung sollte für den Host eine Server Core-Installation von Windows Server 2008 oder höher vorgesehen werden, und außer Hyper-V sollten keine anderen Serverrollen installiert werden.

Die Leistung virtueller Computer hängt insbesondere von der Arbeitsauslastung ab. Testen Sie verschiedene Topologien, um eine zufriedenstellende Leistung von Active Directory sicherzustellen. Bewerten Sie die aktuelle Arbeitsauslastung über einen bestimmten Zeitraum mit einem Tool wie der Zuverlässigkeits-und Leistungsüberwachung (Perfmon. msc) oder dem [Microsoft Assessment and Planning (Map) Toolkit](https://go.microsoft.com/fwlink/?linkid=137077). Das MAP-Tool ist außerdem hilfreich, um eine Bestandsaufnahme aller gegenwärtigen Server und Serverrollen im Netzwerk vorzunehmen.

Um eine allgemeine Vorstellung von der Leistung virtualisierter Domänen Controller zu erhalten, wurden die folgenden Leistungstests mit dem [Active Directory Leistungs Testtool (ADTest.exe)](https://go.microsoft.com/fwlink/?linkid=137088)durchgeführt.

LDAP-Tests (Lightweight Directory Access-Protokoll) wurden zunächst auf einem physischen Domänencontroller mit %%amp;quot;ADTest.exe%%amp;quot; und anschließend auf einem virtuellen Computer (gehostet auf einem mit dem physischen Domänencontroller identischen Server) ausgeführt. Um problemlos eine CPU-Auslastung von 100 % zu erreichen, wurde für den physischen Computer nur ein logischer Prozessor und für den virtuellen Computer nur ein virtueller Prozessor verwendet. In der folgenden Tabelle bezeichnen der Buchstabe und die Zahl in Klammern (jeweils nach der Testbeschreibung) die verschiedenen Tests von %amp;quot;ADTest.exe%%amp;quot;. Die Leistung des virtualisierten Domänencontrollers betrug demnach zwischen ca. 88 und 98 % von der des physischen Domänencontrollers.

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Messung</th>
<th>Test</th>
<th>Physisch</th>
<th>Virtuell</th>
<th>Delta</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Suchen/Sek.</p></td>
<td><p>Suche nach einem allgemeinen Namen im Basisbereich (L1)</p></td>
<td><p>11508</p></td>
<td><p>10276</p></td>
<td><p>-10,71%</p></td>
</tr>
<tr class="even">
<td><p>Suchen/Sek.</p></td>
<td><p>Suche nach einem Attributsatz im Basisbereich (L2)</p></td>
<td><p>10123</p></td>
<td><p>9005</p></td>
<td><p>-11,04%</p></td>
</tr>
<tr class="odd">
<td><p>Suchen/Sek.</p></td>
<td><p>Suche nach allen Attributen im Basisbereich (L3)</p></td>
<td><p>1284</p></td>
<td><p>1242</p></td>
<td><p>-3,27%</p></td>
</tr>
<tr class="even">
<td><p>Suchen/Sek.</p></td>
<td><p>Suche nach einem allgemeinen Namen im Unterstrukturbereich (L6)</p></td>
<td><p>8613</p></td>
<td><p>7904</p></td>
<td><p>-8,23%</p></td>
</tr>
<tr class="odd">
<td><p>Erfolgreiche Bindungen/Sek.</p></td>
<td><p>Ausführen schneller Bindungen (B1)</p></td>
<td><p>1438</p></td>
<td><p>1374</p></td>
<td><p>-4,45%</p></td>
</tr>
<tr class="even">
<td><p>Erfolgreiche Bindungen/Sek.</p></td>
<td><p>Ausführen einfacher Bindungen (B2)</p></td>
<td><p>611</p></td>
<td><p>550</p></td>
<td><p>-9,98%</p></td>
</tr>
<tr class="odd">
<td><p>Erfolgreiche Bindungen/Sek.</p></td>
<td><p>Ausführen von Bindungen mithilfe von NTLM (B5)</p></td>
<td><p>1068</p></td>
<td><p>1056</p></td>
<td><p>-1,12%</p></td>
</tr>
<tr class="even">
<td><p>Schreibvorgänge/s</p></td>
<td><p>Schreiben mehrerer Attribute (W2)</p></td>
<td><p>6467</p></td>
<td><p>5885</p></td>
<td><p>-9,00%</p></td>
</tr>
</tbody>
</table>

Zur Sicherstellung einer zufriedenstellenden Leistung wurden Integrationskomponenten installiert, damit das Gastbetriebssystem Optimierungen oder hypervisorkompatible synthetische Treiber verwenden konnte. Zur Installation sind möglicherweise emulierte IDE- (Integrated Drive Electronics) oder Netwerkadaptertreiber erforderlich. In Produktionsumgebungen sollten Sie diese emulierten Treiber durch synthetische Treiber ersetzen, um die Leistung zu optimieren.

Wenn Sie die Leistung virtueller Computer mit der Zuverlässigkeits- und Leistungsüberwachung (%%amp;quot;Perfmon.msc%%amp;quot;) überwachen, sind die CPU-Informationen des virtuellen Computers nicht ganz zutreffend. Dies ist auf das Verfahren zurückzuführen, mit dem die virtuelle CPU auf dem physischen Prozessor zeitlich abgestimmt wird. Zum Abrufen von CPU-Informationen für einen virtuellen Computer, der auf einem Hyper-V-Server ausgeführt wird, verwenden Sie die Leistungsindikatoren %%amp;quot;Logischer Prozessor für Hyper-V-Hypervisor%%amp;quot; in der Hostpartition.

Weitere Informationen zur Leistungsoptimierung von AD DS und Hyper-V finden Sie unter [Richtlinien für die Leistungsoptimierung für Windows Server 2016](../../../../administration/performance-tuning/index.md).

Zudem ist davon abzuraten, eine differenzierende virtuelle Festplatte (Virtual Hard Disk, VHD) auf einem virtuellen Computer zu verwenden, der als Domänencontroller konfiguriert ist, da dadurch die Leistung beeinträchtigt werden kann. Weitere Informationen zu Hyper-V-Datenträger Typen, einschließlich differenzierender Datenträger, finden Sie unter [Assistent für neue virtuelle Festplatten](https://go.microsoft.com/fwlink/?linkid=137279).

Weitere Informationen zu AD DS in virtuellen Hostingumgebungen finden Sie unter Dinge, die [beim Hosten von Active Directory Domänen Controllern in virtuellen Host Umgebungen](https://go.microsoft.com/fwlink/?linkid=141292) in der Microsoft Knowledge Base zu beachten sind.

## <a name="deployment-considerations-for-virtualized-domain-controllers"></a>Überlegungen zur Bereitstellung virtualisierter Domänencontroller

Mehrere gängige Praktiken im Zusammenhang mit virtuellen Computern sollten bei der Bereitstellung virtualisierter Domänencontroller vermieden werden. Zudem gelten spezielle Empfehlungen für die Zeitsynchronisierung und Speicherung.

## <a name="virtualization-deployment-practices-to-avoid"></a>Bei der Virtualisierungsbereitstellung zu vermeidende Praktiken

Virtualisierungsplattformen, wie z. B. Hyper-V, bieten eine Reihe von Features, die das Verwalten, Warten, Sichern und Migrieren von Computern vereinfachen. Bei der Bereitstellung virtualisierter Domänencontroller empfiehlt es sich jedoch, die folgenden gängigen Praktiken (und zugehörigen Features) zu vermeiden:

- Stellen Sie die Datenbankdateien eines virtuellen Domänen Controllers (Active Directory Datenbank (NTDS) nicht bereit, um die Dauerhaftigkeit von Active Directory Schreibvorgängen zu gewährleisten. DIT), Protokolle und SYSVOL) auf virtuellen IDE-Datenträgern. Erstellen Sie stattdessen eine zweite VHD, die an einen virtuellen SCSI-Controller angeschlossen ist, und stellen Sie sicher, dass die Datenbank, Protokolle und SYSVOL während der Installation des Domänen Controllers auf dem SCSI-Datenträger des virtuellen Computers platziert werden.  
- Implementieren Sie keine differenzierenden virtuellen Festplatten auf einem virtuellen Computer, den Sie als Domänencontroller konfigurieren. Dies macht die Wiederherstellung einer früheren Version zu einfach, und die Leistung wird reduziert. Weitere Informationen zu VHD-Typen finden Sie unter [Assistent für neue virtuelle Festplatten](https://go.microsoft.com/fwlink/?linkid=137279).  
- Stellen Sie keine neuen Active Directory Domänen und Gesamtstrukturen in einer Kopie eines Windows Server-Betriebssystems bereit, das nicht zum ersten Mal mithilfe des System Vorbereitungs Tools (syspree) vorbereitet wurde. Weitere Informationen zur Ausführung von sy-p finden Sie unter [System Vorbereitung (System Vorbereitung)](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview) .

   > [!WARNING]
   > Die Ausführung von Sysprep auf einem Domänencontroller wird nicht unterstützt.

- Zur Vermeidung einer Rollbacksituation der Aktualisierungssequenznummern (Update Sequence Numbers, USNs) sollten Kopien einer VHD-Datei, die zu einem bereitgestellten Domänencontroller gehört, nicht zum Bereitstellen weiterer Domänencontroller verwendet werden. Weitere Informationen über das Rollback für die Wiederverwendung finden Sie unter " [US-v" und "Rollback](#usn-and-usn-rollback)".
   - Mit Windows Server 2012 und höher können Administratoren Domänen Controller Images Klonen, wenn Sie bei der Bereitstellung zusätzlicher Domänen Controller ordnungsgemäß vorbereitet werden.
- Verwenden Sie das Exportfeature von Hyper-V nicht zum Exportieren eines virtuellen Computers, auf dem ein Domänencontroller ausgeführt wird.
  - Bei Windows Server 2012 und höher wird ein Export und Import eines virtuellen Domänen Controller-Gast Betriebssystems wie eine nicht autoritative Wiederherstellung behandelt, da er eine Änderung der Generations-ID erkennt und nicht für das Klonen konfiguriert ist.
  - Stellen Sie sicher, dass Sie den Gast, den Sie exportiert haben, nicht mehr verwenden.
    - Sie können die Hyper-V-Replikation verwenden, um eine zweite Inaktive Kopie eines Domänen Controllers beizubehalten. Wenn Sie das replizierte Image starten, müssen Sie auch eine ordnungsgemäße Bereinigung durchführen, und zwar aus demselben Grund, aus dem die Quelle nach dem Exportieren eines DC-gastimages nicht verwendet werden kann.

## <a name="physical-to-virtual-migration"></a>Physical-to-Virtual-Migration (P2V)

System Center Virtual Machine Manager (VMM) 2008 ermöglicht die einheitliche Verwaltung physischer und virtueller Computer. Außerdem kann ein physischer Computer zu einem virtuellen Computer migriert werden. Dieser Vorgang wird als Physical-to-Virtual-Konvertierung (P2V) bezeichnet. Während des P2V-Konvertierungs Vorgangs dürfen der neue virtuelle Computer und der physische Domänen Controller, der migriert wird, nicht gleichzeitig ausgeführt werden, um eine für das Rollback [in der](#usn-and-usn-rollback)upgradesituation beschriebene Betriebs Steuerungs Situation zu vermeiden.

Die P2V-Konvertierung sollte im Offlinemodus ausgeführt werden, damit die Verzeichnisdaten einheitlich sind, wenn der Domänencontroller wieder eingeschaltet wird. Der Offlinemodus ist die empfohlene Option im Assistenten zum Konvertieren des physischen Servers. Eine Beschreibung des Unterschieds zwischen Online Modus und Offline Modus finden Sie unter [P2V: umstellen physischer Computer in Virtual Machines in VMM](https://go.microsoft.com/fwlink/?linkid=155072). Während der P2V-Konvertierung sollte der virtuelle Computer nicht mit dem Netzwerk verbunden sein. Aktivieren Sie den Netzwerkadapter des virtuellen Computers erst nach Abschluss und Überprüfung der P2V-Konvertierung. Zu diesem Zeitpunkt ist der physische Quellcomputer ausgeschaltet. Bevor Sie den physischen Quellcomputer wieder mit dem Netzwerk verbinden, formatieren Sie die Festplatte neu.

> [!NOTE]
> Es gibt sicherere Optionen zum Erstellen neuer virtueller DCS, die keine Risiken bei der Erstellung eines Rollbacks für eine höhere Laufzeit haben. Sie können einen neuen virtuellen Domänen Controller durch reguläre herauf Stufung, herauf Stufung von der Installation von einem Medium (IFM) und auch durch Klonen des Domänen Controllers einrichten, wenn Sie bereits über mindestens einen virtuellen Domänen Controller verfügen.
Dies hilft auch dabei, Probleme mit Hardware-oder Platt Form bezogenen Problemen zu vermeiden P2V bei konvertierten virtuellen Gästen treten möglicherweise Probleme auf.

> [!WARNING]
> Stellen Sie sicher, dass jeweils immer nur eine einzige Instanz (physisch oder virtuell) eines bestimmten Domänencontrollers in einem bestimmten Netzwerk vorhanden ist, um Probleme bei der Active Directory-Replikation zu vermeiden.
> Sie können die Wahrscheinlichkeit verringern, dass der alte Klon ein Problem darstellt:
> 
> - Wenn der neue virtuelle Domänen Controller ausgeführt wird, ändern Sie das Computer Konto Kennwort zweimal mit: netdom resetpwd/Server: <Domänen Controller>...
> - Exportieren und importieren Sie den neuen virtuellen Gast, um zu erzwingen, dass er zu einer neuen Generations-ID und somit zu einer Datenbank-Aufruf-ID wird.
> 

## <a name="using-p2v-migration-to-create-test-environments"></a>Erstellen von Testumgebungen mithilfe der P2V-Migration

Mithilfe der P2V-Migration über VMM können Sie Testumgebungen erstellen. Sie können Produktionsdomänencontroller von physischen zu virtuellen Computern migrieren, um eine Testumgebung zu erstellen, ohne die Produktionsdomänencontroller dauerhaft offline zu schalten. Falls jedoch zwei Instanzen desselben Domänencontrollers benötigt werden, muss sich die Testumgebung in einem anderen Netzwerk als die Produktionsumgebung befinden. Gehen Sie beim Erstellen von Testumgebungen mit der P2V-Migration äußerst vorsichtig vor, um USN-Rollbacks zu vermeiden, die sich negativ auf Ihre Test- und Produktionsumgebungen auswirken können. Mit der folgenden Methode können Sie Testumgebungen mit dem P2V-Verfahren erstellen:

Ein Produktionsdomänencontroller aus jeder Domäne wird zu einem virtuellen Testcomputer migriert, wobei die P2V-Konvertierung nach den Empfehlungen im Abschnitt Physical-to-Virtual-Migration (P2V) verwendet wird. Die physischen Produktionscomputer und die virtuellen Testcomputer müssen sich in unterschiedlichen Netzwerken befinden, wenn sie wieder online geschaltet werden. Um USN-Rollbacks in der Testumgebung zu vermeiden, müssen alle Domänencontroller, die von physischen zu virtuellen Computern migriert werden sollen, offline geschaltet werden. (Hierzu können Sie den NTDS-Dienst beenden oder den Computer im Verzeichnisdienste-Wiederherstellungs Modus (Directory Services Restore Mode, DSRM) neu starten.) Nachdem die Domänen Controller offline sind, sollten keine neuen Updates in die Umgebung eingefügt werden. Die Computer müssen während der P2V-Migration offline bleiben. Keiner der Computer darf wieder online geschaltet werden, bevor alle Computer vollständig migriert sind. Weitere Informationen zu USN-Rollbacks finden Sie unter USN und USN-Rollback.

Spätere Testdomänencontroller sollten in der Testumgebung als Replikate höher gestuft werden.

## <a name="time-service"></a>Zeitdienst

Bei virtuellen Maschinen, die als Domänen Controller konfiguriert sind, wird empfohlen, die Zeitsynchronisierung zwischen dem Host System und dem Gast Betriebssystem zu deaktivieren, die als Domänen Controller fungieren. Dadurch kann der Gast Domänen Controller die Zeit von der Domänen Hierarchie aus synchronisieren.

Um den Hyper-V-Zeit Synchronisierungs Anbieter zu deaktivieren, fahren Sie den virtuellen Computer herunter, und deaktivieren Sie das Kontrollkästchen Zeitsynchronisierung unter Integration Services.

> [!NOTE]
> Diese Anleitung wurde vor kurzem aktualisiert und enthält jetzt die aktuelle Empfehlung, die Zeit für den Gast Domänen Controller nur aus der Domänen Hierarchie zu synchronisieren, anstatt die vorherige Empfehlung zum partiellen Deaktivieren der Zeitsynchronisierung zwischen dem Host System und dem Gast Domänen Controller zu berücksichtigen.

## <a name="storage"></a>Storage

Verwenden Sie die folgenden Empfehlungen zum Speichern von Betriebssystem-, Active Directory-und VHD-Dateien, um die Leistung des virtuellen Computers mit dem Domänen Controller zu optimieren und die Dauerhaftigkeit Active Directory Schreibvorgängen sicherzustellen:

- **Gastspeicherung**: Speichern Sie die Active Directory-Datenbankdatei (%%amp;quot; Ntds.dit%%amp;quot;) sowie die Protokoll- und SYSVOL-Dateien auf einem anderen virtuellen Datenträger als die Betriebssystemdateien. Erstellen Sie eine zweite VHD, die an einen virtuellen SCSI-Controller angefügt ist, und speichern Sie die Datenbank, Protokolle und SYSVOL auf dem virtuellen SCSI-Datenträger der virtuellen Maschine. Virtuelle SCSI-Datenträger bieten eine bessere Leistung im Vergleich zur virtuellen IDE und unterstützen den erzwungenen Einheiten Zugriff Fua stellt sicher, dass das Betriebssystem Daten direkt aus dem Medium schreibt und liest, wobei alle zwischen Speicherungs Mechanismen umgangen werden.

  > [!NOTE]
  > Wenn Sie BitLocker für den Gast des virtuellen Domänen Controllers verwenden möchten, müssen Sie sicherstellen, dass die zusätzlichen Volumes für die automatische Entsperrung konfiguriert sind.
  > Weitere Informationen zum Konfigurieren der automatischen Entsperrung finden Sie unter [enable-bitlockerautounlock](/powershell/module/bitlocker/enable-bitlockerautounlock) .

- **Hostspeicherung von VHD-Dateien**: Die Empfehlungen für die Hostspeicherung beziehen sich auf die Speicherung von VHD-Dateien. Zur Optimierung der Leistung sollten Sie VHD-Dateien nicht auf einem Datenträger speichern, der häufig von anderen Diensten oder Anwendungen verwendet wird, wie z. B. auf dem Systemdatenträger, auf dem das Windows-Hostbetriebssystem installiert ist. Speichern Sie jede der VHD-Dateien auf einer vom Hostbetriebssystem und anderen VHD-Dateien getrennten Partition. Die ideale Konfiguration ist die Speicherung jeder VHD-Datei auf einem separaten physischen Laufwerk.  

  Das System des physischen Host Datenträgers muss auch **mindestens eines** der folgenden Kriterien erfüllen, um die Anforderungen an die Integrität der virtualisierten Arbeits Auslastungs Daten zu erfüllen:  

   - Das System verwendet Server-Klassen Datenträger (SCSI, Fibre Channel).  
   - Das System stellt sicher, dass die Datenträger mit einem Akku gestützten Caching-Hostbus Adapter (HBA) verbunden sind.  
   - Das System verwendet einen Speichercontroller (z. b. ein RAID-System) als Speichergerät.  
   - Das System stellt sicher, dass die Stromversorgung des Datenträgers durch eine unterbrechungsfreie Stromversorgung (USV) geschützt ist.  
   - Das System stellt sicher, dass das Write-Caching-Feature des Datenträgers deaktiviert ist.  

- **Feste virtuelle Festplatten oder Pass-Through-Datenträger**: Es gibt viele Methoden zum Konfigurieren der Speicherung für virtuelle Computer. Wenn VHD-Dateien verwendet werden, sind virtuelle Festplatten mit fester Größe effizienter als dynamische virtuelle Festplatten, da der Arbeitsspeicher für virtuelle Festplatten mit fester Größe beim Erstellen zugeordnet wird. Eine noch höhere Leistung ermöglichen Pass-Through-Datenträger, die von virtuellen Computern für den Zugriff auf physische Speichermedien verwendet werden können. Pass-Through-Datenträger sind im Prinzip physische Datenträger oder logische Gerätenummern (Logical Unit Numbers, LUNs), die einem virtuellen Computer zugeordnet sind. Das Snapshotfeature wird von Pass-Through-Datenträgern nicht unterstützt. Dies macht Pass-Through-Datenträger zur bevorzugten Festplattenkonfiguration, da bei Domänencontrollern von der Verwendung von Snapshots abgeraten wird.  

Verwenden Sie virtuelle SCSI-Controller, um die Gefahr der Beschädigung von Active Directory Daten zu verringern:

   - Verwenden Sie auf Hyper-V-Servern, auf denen virtuelle Domänencontroller gehostet werden, nicht ATA/IDE-Laufwerke, sondern physische SCSI-Laufwerke. Falls Sie keine SCSI-Laufwerke verwenden können, stellen Sie sicher, dass der Schreibcache für die ATA/IDE-Laufwerke, auf denen virtuelle Domänencontroller gehostet werden, deaktiviert ist. Weitere Informationen finden Sie unter [Ereignis-ID 1539 – Datenbankintegrität](https://go.microsoft.com/fwlink/?linkid=162419).
   - Um die Dauerhaftigkeit von Active Directory Schreibvorgängen zu gewährleisten, müssen die Active Directory Datenbank, Protokolle und SYSVOL auf einem virtuellen SCSI-Datenträger abgelegt werden. Virtuelle SCSI-Datenträger unterstützen den erzwungenen Unit Access (Fua). Fua stellt sicher, dass das Betriebssystem Daten direkt aus dem Medium schreibt und liest, wobei alle zwischen Speicherungs Mechanismen umgangen werden.  

## <a name="operational-considerations-for-virtualized-domain-controllers"></a>Überlegungen zur Verwendung virtualisierter Domänencontroller

Die Verwendungsmöglichkeiten von Domänencontrollern, die auf virtuellen Computern ausgeführt werden, sind - im Vergleich zu Domänencontrollern, die auf physischen Computern ausgeführt werden - eingeschränkt. Folgende Features der Virtualisierungssoftware und folgende Praktiken sollten bei virtualisierten Domänencontrollern nicht verwendet werden:

   - Vermeiden Sie es, den gespeicherten Zustand eines virtualisierten Domänencontrollers für einen längeren Zeitraum als die Tombstone-Lebensdauer der Gesamtstruktur anzuhalten, zu beenden oder zu speichern und dann ausgehend vom angehaltenen oder gespeicherten Zustand weiterzuarbeiten. Dadurch können Probleme bei der Replikation verursacht werden. Informationen zum Bestimmen der Tombstone-Lebensdauer für die Gesamtstruktur finden Sie unter [bestimmen der Tombstone-Lebensdauer für die](https://go.microsoft.com/fwlink/?linkid=137177)Gesamtstruktur.  
   - Kopieren oder klonen Sie keine virtuellen Festplatten. Auch wenn die Sicherheitsvorkehrungen für die Gast-VM gelten, können einzelne VHDs weiterhin kopiert werden und bewirken ein Rollback für die USN.
   - Erstellen oder verwenden Sie keine Snapshots eines virtuellen Domänencontrollers. Es wird von Windows Server 2012 und höher technisch unterstützt. es ist kein Ersatz für eine gute Sicherungsstrategie. Es gibt einige Gründe für das nehmen von DC-Momentaufnahmen oder das Wiederherstellen der Momentaufnahmen
   - Verwenden Sie keine differenzierende virtuelle Festplatte auf einem virtuellen Computer, der als Domänencontroller konfiguriert ist. Dies macht die Wiederherstellung einer früheren Version zu einfach, und die Leistung wird reduziert.  
   - Verwenden Sie das Exportfeature nicht auf einem virtuellen Computer, auf dem ein Domänencontroller ausgeführt wird.  
   - Verwenden Sie zum Wiederherstellen eines Domänencontrollers oder Ausführen eines Rollbacks für den Inhalt einer Active Directory-Datenbank ausschließlich unterstützte Sicherungsvorgänge Weitere Informationen finden Sie unter [Überlegungen zur Sicherung und Wiederherstellung für virtualisierte Domänen Controller](#backup-and-restore-practices-to-avoid).  

Durch diese Empfehlungen soll ein Rollback der Aktualisierungssequenznummern vermieden werden. Weitere Informationen über das Rollback für die Wiederverwendung finden Sie unter "US-v" und "Rollback".

## <a name="backup-and-restore-considerations-for-virtualized-domain-controllers"></a>Überlegungen zum Sichern und Wiederherstellen virtualisierter Domänencontroller

Das Sichern von Domänencontrollern ist für jede Umgebung eine wichtige Aufgabe. Sicherungen schützen bei einem Fehler des Domänencontrollers oder Administrators vor Datenverlust. Nach einem solchen Fehler muss der Systemstatus des Domänencontrollers mithilfe eines Rollbacks auf einen Zeitpunkt vor Auftreten des Fehlers zurückgesetzt werden. Das unterstützte Verfahren dazu besteht darin, mithilfe einer Active Directory-kompatiblen Sicherungsanwendung, wie z. B. der Windows Server-Sicherung, eine Systemstatussicherung wiederherzustellen, die aus der aktuellen Installation des Domänencontrollers stammt. Weitere Informationen zur Verwendung von Windows Server-Sicherung mit Active Directory Domain Services (AD DS) finden Sie in der [schrittweisen Anleitung für die AD DS Sicherung und Wiederherstellung](https://go.microsoft.com/fwlink/?LinkId=138501).

Im Zusammenhang mit der Virtualisierungstechnologie erhalten bestimmte Anforderungen für Active Directory-Wiederherstellungsvorgänge zusätzliche Bedeutung. Wenn Sie z. B. einen Domänencontroller mithilfe einer Kopie der VHD-Datei wiederherstellen, umgehen Sie einen wichtigen Schritt: die Aktualisierung der Datenbankversion eines wiederhergestellten Domänencontrollers. Die Replikation wird mit ungeeigneten Trackingnummern fortgesetzt, was zu Datenbankinkonsistenzen zwischen den Domänencontrollerreplikaten führt. In den meisten Fällen wird dieses Problem vom Replikationssystem nicht erkannt, und trotz der Inkonsistenzen werden keine Fehler gemeldet.

Ein einziges Verfahren wird zum Sichern und Wiederherstellen eines virtualisierten Domänencontrollers unterstützt:

1. Führen Sie die Windows Server-Sicherung im Gastbetriebssystem aus.  

Mit Windows Server 2012 und neueren Hyper-V-Hosts und-Gästen können Sie unterstützte Sicherungen von Domänen Controllern mithilfe von Momentaufnahmen, Export und Import von Gast-VMS und Hyper-v-Replikation erstellen. Alle diese eignen sich jedoch nicht gut für die Erstellung eines ordnungsgemäßen Sicherungs Verlaufs, mit Ausnahme des Gast-VM-Exports.

Mit Windows Server 2016 Hyper-V wird die "Produktions Momentaufnahmen" unterstützt, wenn der Hyper-v-Server eine VSS-basierte Sicherung des Gasts auslöst und wenn der Gast mit der Momentaufnahme ausgeführt wird, ruft der Host die VHDs ab und speichert Sie am Speicherort der Sicherung.

Dies funktioniert zwar mit Windows Server 2012 und höher, es gibt jedoch eine Inkompatibilität mit BitLocker:

- Bei einem VSS-Snap-in möchte AD eine Aufgabe nach der Momentaufnahme durchführen, um die Datenbank als aus einer Sicherung zu markieren, oder wenn Sie eine IFM-Quelle für den RODC vorbereiten, entfernen Sie die Anmelde Informationen aus der Datenbank.
- Wenn Hyper-V das snapshotted-Volume für diese Aufgabe bereitstellt, gibt es keine Möglichkeit, das Volume für den unverschlüsselten Zugriff zu entsperren. Die AD-Datenbank-Engine kann daher nicht auf die Datenbank zugreifen und schließlich die Momentaufnahme nicht mehr.

> [!NOTE]
> Das zuvor erwähnte abgeschirmte VM-Projekt verfügt über eine von Hyper-V-Hosts gesteuerte Sicherung als Ziel für den maximalen Datenschutz der Gast-VM.

## <a name="backup-and-restore-practices-to-avoid"></a>Bei der Sicherung und Wiederherstellung zu vermeidende Praktiken

Wie bereits erwähnt, gelten für virtualisierte Domänencontroller im Vergleich zu physischen Domänencontrollern gewisse Einschränkungen. Folgende Features der Virtualisierungssoftware und folgende Praktiken sollten beim Sichern und Wiederherstellen eines virtualisierten Domänencontrollers nicht verwendet werden:

   - Kopieren oder klonen Sie keine VHD-Dateien von Domänencontrollern als Ersatz für regelmäßige Sicherungen. Kopierte oder geklonte VHD-Dateien können veralten. Wenn die virtuelle Festplatte im normalen Modus gestartet wird, wird ein Rollback für die virtuelle Festplatte angezeigt. Führen Sie stattdessen ordnungsgemäße Sicherungsvorgänge aus, die von den Active Directory-Domänendiensten (Active Directory Domain Services, AD DS) unterstützt werden (beispielsweise mit der Windows Server-Sicherung).  
   - Verwenden Sie zur Sicherung und Wiederherstellung virtualisierter Domänencontroller nicht das Snapshotfeature. Bei der Replikation treten Probleme auf, wenn Sie den virtuellen Computer mit Windows Server 2008 R2 und älter auf einen früheren Status zurücksetzen. Weitere Informationen finden Sie unter " [US-v" und "Wiederverwendungs-Rollback](#usn-and-usn-rollback)". Bei RODCs verursacht die Wiederherstellung anhand eines Snapshots zwar keine Replikationsprobleme, doch auch in diesem Fall wird davon abgeraten.  

## <a name="restoring-a-virtual-domain-controller"></a>Wiederherstellen eines virtuellen Domänencontrollers

Damit Sie einen fehlerhaften Domänencontroller wiederherstellen können, müssen Sie den Systemstatus regelmäßig sichern. Zum Systemstatus gehören Active Directory-Daten und -Protokolldateien, die Registrierung, das Systemvolume (SYSVOL-Ordner) sowie verschiedene Elemente des Betriebssystems. Diese Anforderung unterscheidet sich nicht zwischen physischen und virtualisierten Domänencontrollern. Die Verfahren zur Systemstatuswiederherstellung, die von Active Directory-kompatiblen Sicherungsanwendungen ausgeführt werden, sind dafür ausgelegt, nach einer Wiederherstellung die Konsistenz zwischen lokalen und replizierten Active Directory-Datenbanken sicherzustellen. Dazu zählt auch die Benachrichtigung von Replikationspartnern über Zurücksetzungen der Aufrufkennung. Die Überprüfungen, die gewöhnlich beim Wiederherstellen des Domänencontroller-Systemstatus ausgeführt werden, können jedoch vom Administrator umgangen werden - etwa mit virtuellen Hostumgebungen oder Anwendungen zur Erstellung von Datenträger- oder Betriebssystemimages.

Wenn bei einem virtuellen Computer eines Domänencontrollers ein Fehler aufgetreten ist und kein Rollback der Aktualisierungssequenznummern vorliegt, bestehen zwei Möglichkeiten zum Wiederherstellen des virtuellen Computers:

   - Falls eine gültige Sicherung der Systemstatusdaten vorhanden ist, die vor dem Auftreten des Fehlers erstellt wurde, können Sie den Systemstatus mithilfe des Sicherungsprogramms wiederherstellen, mit dem Sie die Sicherung erstellt haben. Die Sicherung der Systemstatusdaten muss mit einem Active Directory-kompatiblen Sicherungsprogramm innerhalb der Tombstone-Lebensdauer erstellt worden sein, also standardmäßig vor maximal 180 Tagen. Es empfiehlt sich, die Domänencontroller spätestens bei Erreichen der Hälfte der Tombstone-Lebensdauer zu sichern. Anweisungen dazu, wie Sie die jeweilige Tombstone-Lebensdauer für Ihre Gesamtstruktur ermitteln, finden Sie unter [bestimmen der Tombstone-Lebensdauer für die](https://go.microsoft.com/fwlink/?linkid=137177)Gesamtstruktur.  
   - Wenn zwar eine Arbeitskopie der VHD-Datei, aber keine Systemstatussicherung verfügbar ist, können Sie den vorhandenen virtuellen Computer entfernen. Stellen Sie den vorhandenen virtuellen Computer mithilfe einer vorherigen Kopie der VHD-Datei wieder her. Starten Sie den Computer jedoch unbedingt im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM), und konfigurieren Sie die Registrierung ordnungsgemäß, wie im folgenden Abschnitt beschrieben. Anschließend starten Sie den Domänencontroller im normalen Modus neu.

Bestimmen Sie anhand des folgenden Schemas die optimale Methode zum Wiederherstellen Ihres virtualisierten Domänencontrollers:

![](media/virtualized-domain-controller-architecture/Dd363553.85c97481-7b95-4705-92a7-006e48bc29d0(WS.10).gif)

Bei RODCs sind der Wiederherstellungsvorgang und die zu treffenden Entscheidungen einfacher:

![](media/virtualized-domain-controller-architecture/Dd363553.4c5c5eda-df95-4c6b-84e0-d84661434e5d(WS.10).gif)

## <a name="restoring-the-system-state-backup-of-a-virtual-domain-controller"></a>Wiederherstellen der Systemstatussicherung eines virtuellen Domänencontrollers

Wenn eine gültige Systemstatussicherung für den virtuellen Computer eines Domänencontrollers vorhanden ist, können Sie die Sicherung problemlos wiederherstellen. Führen Sie dazu das Wiederherstellungsverfahren des Sicherungstools aus, mit dem Sie die VHD-Datei gesichert haben.

> [!IMPORTANT]
> Sie müssen den Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus starten, um ihn ordnungsgemäß wiederherstellen zu können. Der Domänencontroller darf nicht im normalen Modus gestartet werden. Wenn Sie während des Systemstarts nicht die Möglichkeit haben, DSRM einzugeben, deaktivieren Sie den virtuellen Computer des Domänen Controllers, bevor er vollständig im normalen Modus gestartet werden kann. Der Domänencontroller muss unbedingt im Verzeichnisdienst-Wiederherstellungsmodus gestartet werden, da bei einem Start im normalen Modus die Aktualisierungssequenznummern erhöht würden (auch dann, wenn der Domänencontroller vom Netzwerk getrennt ist). Weitere Informationen über das Rollback für die Wiederverwendung finden Sie unter "US-v" und "Rollback". 

## <a name="to-restore-the-system-state-backup-of-a-virtual-domain-controller"></a>So stellen Sie die Systemstatussicherung eines virtuellen Domänencontrollers wieder her

1. Starten Sie den virtuellen Computer des Domänen Controllers, und drücken Sie F5, um auf den Bildschirm Windows-Start-Manager zuzugreifen. Falls Sie Anmeldeinformationen für die Verbindung eingeben müssen, klicken Sie auf dem virtuellen Computer sofort auf die Schaltfläche **Pause**, damit der Startvorgang nicht fortgesetzt wird. Geben Sie anschließend die Anmeldeinformationen für die Verbindung ein, und klicken Sie auf dem virtuellen Computer auf die Schaltfläche **Wiedergabe**. Klicken Sie auf eine Stelle im Fenster des virtuellen Computers, und drücken Sie dann die Taste F5.

   Wenn der Bildschirm des Windows-Start-Managers nicht angezeigt wird, schalten Sie den virtuellen Computer aus, bevor der Domänencontroller im normalen Modus gestartet werden kann. Wiederholen Sie diesen Schritt so oft wie nötig, bis Sie auf den Bildschirm des Windows-Start-Managers zugreifen können. Über das Menü %%amp;quot;Windows-Fehlerbehebung%%amp;quot; kann der Verzeichnisdienst-Wiederherstellungsmodus nicht aufgerufen werden. Wenn das Menü %%amp;quot;Windows-Fehlerbehebung%%amp;quot; angezeigt wird, schalten Sie den Computer aus, und versuchen Sie es erneut.

2. Drücken Sie im Bildschirm des Windows-Start-Managers die Taste F8, um auf die erweiterten Startoptionen zuzugreifen.
3. Markieren Sie im Bildschirm **Erweiterte Startoptionen** die Option **Verzeichnisdienstwiederherstellung**, und drücken Sie dann die EINGABETASTE. Dadurch wird der Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus gestartet.
4. Verwenden Sie das passende Wiederherstellungsverfahren für das Tool, mit dem Sie die Systemstatussicherung erstellt haben. Wenn Sie Windows Server-Sicherung verwendet haben, finden Sie weitere Informationen unter [Ausführen einer nicht autorisierenden Wiederherstellung AD DS](https://go.microsoft.com/fwlink/?linkid=132637).

## <a name="restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available"></a>Wiederherstellen eines virtuellen Domänencontrollers, wenn keine geeignete Sicherung der Systemstatusdaten verfügbar ist

Wenn vor dem Auftreten des Fehlers beim virtuellen Computer keine Systemstatussicherung erstellt wurde, können Sie den auf dem virtuellen Computer ausgeführten Domänencontroller mithilfe einer vorherigen VHD-Datei wiederherstellen. Erstellen Sie möglichst eine Kopie der VHD-Datei. So können Sie das Verfahren wiederholen, falls ein Problem auftritt oder Sie einen Schritt auslassen.

> [!IMPORTANT]
> - Das folgende Verfahren eignet sich nicht als Ersatz für regelmäßig geplante und terminierte Sicherungen.
> - **Mit der folgenden Prozedur ausgeführte Wiederherstellungen werden nicht von Microsoft unterstützt und sollten nur bei Mangel an Alternativen verwendet werden.**
> - Verwenden Sie das Verfahren nicht, wenn die Kopie der virtuellen Festplatte, die Sie zur Wiederherstellung verwenden, von einem beliebigen virtuellen Computer im normalen Modus gestartet wurde.

## <a name="to-restore-a-previous-version-of-a-virtual-domain-controller-vhd-without-system-state-data-backup"></a>So stellen Sie für einen virtuellen Domänencontroller eine vorherige VHD-Version wieder her, wenn keine Sicherung der Systemstatusdaten verfügbar ist

1. Starten Sie den virtuellen Domänencontroller wie im vorherigen Abschnitt beschrieben im Verzeichnisdienst-Wiederherstellungsmodus, wobei Sie die vorherige VHD-Datei verwenden. Der Domänencontroller darf nicht im normalen Modus gestartet werden. Wenn der Bildschirm des Windows-Start-Managers nicht angezeigt wird, schalten Sie den virtuellen Computer aus, bevor der Domänencontroller im normalen Modus gestartet werden kann. Ausführliche Anweisungen zum Aktivieren des Verzeichnisdienst-Wiederherstellungsmodus finden Sie im vorherigen Abschnitt.
2. Öffnen Sie den Registrierungs-Editor. Klicken Sie zum Öffnen des Registrierungs-Editors auf **Start**und auf **Ausführen**, geben Sie **Regedit**ein, und klicken Sie dann auf OK. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**. Erweitern Sie im Registrierungs-Editor den folgenden Pfad: **HKEY \_ local \_ Machine \\ System \\ CurrentControlSet \\ Services \\ NTDS \\ Parameters**. Suchen Sie nach dem Wert **DSA Previous Restore Count**. Wenn dieser Wert vorhanden ist, notieren Sie sich die Einstellung. Wenn dieser Wert nicht vorhanden ist, entspricht die Einstellung dem Standardwert, also Null. Fügen Sie keinen Wert hinzu, falls kein Wert angezeigt wird.
3. Klicken Sie mit der rechten Maustaste auf den Registrierungsschlüssel **Parameters**, klicken Sie auf **Neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)**.
4. Geben Sie den neuen Namen **Von Sicherung wiederhergestellte Datenbank** ein, und drücken Sie die EINGABETASTE.
5. Doppelklicken Sie auf den soeben erstellten Wert, um das Dialogfeld **DWORD-Wert (32-Bit) bearbeiten** zu öffnen, und geben Sie dann **1** im Feld **Wert** ein. Die Option **aus Sicherungs Eintrag wiederhergestellte Datenbank** ist auf Domänen Controllern verfügbar, auf denen Windows 2000 Server mit Service Pack 4 (SP4) ausgeführt wird, Windows Server 2003 mit den Updates, die in [erkennen und Wiederherstellen von einem Wiederherstellungs-Rollback in Windows Server 2003, Windows Server 2008 und Windows Server 2008 R2](https://go.microsoft.com/fwlink/?linkid=137182) in der installierten Microsoft Knowledge Base und Windows Server 2008 enthalten sind.
6. Starten Sie den Domänencontroller im normalen Modus neu.
7. Wenn der Domänencontroller neu gestartet wird, öffnen Sie die Ereignisanzeige. Klicken Sie zum Öffnen der Ereignisanzeige auf **Start** und auf **Systemsteuerung**, doppelklicken Sie auf **Verwaltung** und dann auf **Ereignisanzeige**.
8. Erweitern Sie **Anwendungs- und Dienstprotokolle**, und klicken Sie dann auf das Protokoll **Verzeichnisdienste**. Vergewissern Sie sich, dass im Detailbereich Ereignisse angezeigt werden.
9. Klicken Sie mit der rechten Maustaste auf das Protokoll **Verzeichnisdienste**, und klicken Sie dann auf **Suchen**. Geben Sie im Feld **Suchen nach** die Zeichenfolge **1109** ein, und klicken Sie auf **Weitersuchen**.
10. Es sollte mindestens ein Eintrag mit der Ereignis-ID 1109 angezeigt werden. Falls dieser Eintrag nicht angezeigt wird, führen Sie den nächsten Schritt aus. Doppelklicken Sie andernfalls auf den Eintrag. Die Aktualisierung des invocationID-Werts sollte mit dem folgenden (oder einem ähnlichen) Text bestätigt werden:

    ```
    Active Directory has been restored from backup media, or has been configured to host an application partition. 
    The invocationID attribute for this directory server has been changed. 
    The highest update sequence number at the time the backup was created is <time>

    InvocationID attribute (old value):<Previous InvocationID value>
    InvocationID attribute (new value):<New InvocationID value>
    Update sequence number:<USN>

    The InvocationID is changed when a directory server is restored from backup media or is configured to host a writeable application directory partition.
    ```

11. Schließen Sie die Ereignisanzeige.
12. Überprüfen Sie im Registrierungs-Editor, ob der Wert in **DSA Previous Restore Count** dem vorherigen Wert plus 1 entspricht. Wenn dies nicht der richtige Wert ist und Sie keinen Eintrag für die Ereignis-ID 1109 in Ereignisanzeige finden, überprüfen Sie, ob die Service Packs des Domänen Controllers aktuell sind. Sie können dieses Verfahren mit derselben VHD-Datei nicht wiederholen. Jedoch können Sie es mit einer Kopie der VHD-Datei oder einer anderen virtuellen Festplatte, die nicht im normalen Modus gestartet wurde, erneut versuchen. Beginnen Sie dazu wieder bei Schritt 1.
13. Schließen Sie den Registrierungs-Editor.

## <a name="usn-and-usn-rollback"></a>USN und USN-Rollback

In diesem Abschnitt werden Replikationsprobleme beschrieben, die auftreten können, wenn die Active Directory-Datenbank mit einer älteren Version eines virtuellen Computers fehlerhaft wiederhergestellt wurde. Weitere Informationen zum Active Directory Replikationsprozess finden Sie unter [Active Directory Replikations Konzepten](../replication/active-directory-replication-concepts.md) .

## <a name="usns"></a>Aktualisierungssequenznummern (Update Sequence Numbers, USNs)

USNs dienen den Active Directory-Domänendiensten zur Nachverfolgung der Replikation von Daten zwischen Domänencontrollern. Bei jeder Änderung von Daten im Verzeichnis wird die USN erhöht.

Für jede auf einem Zieldomänencontroller gespeicherte Verzeichnispartition werden mithilfe von USNs das neueste Quellupdate, das der Datenbank eines Domänencontrollers hinzugefügt wurde, sowie der Status jedes anderen Domänencontrollers, auf dem ein Replikat der Verzeichnispartition gespeichert ist, nachverfolgt. Bei der Replikation von Änderungen zwischen Domänencontrollern werden von den Replikationspartnern diejenigen Änderungen abgerufen, deren USNs größer sind als die USN der letzten vom jeweiligen Partner empfangenen Änderung.

Die USNs sind in zwei Tabellen mit Replikationsmetadaten enthalten. Sie werden vom Quell- und Zieldomänencontroller verwendet, um die vom Zieldomänencontroller benötigten Änderungen zu bestimmen.

1. **Aktualitätsvektor**: Eine vom Zieldomänencontroller verwaltete Tabelle zum Nachverfolgen der Quellupdates, die von den verschiedenen Quelldomänencontrollern eingehen. Wenn ein Zieldomänencontroller Änderungen für eine Verzeichnispartition anfordert, stellt er dem Quelldomänencontroller seinen Aktualitätsvektor bereit. Der Quelldomänencontroller filtert dann mithilfe dieses Werts die dem Zieldomänencontroller zu sendenden Updates. Der Quell Domänen Controller sendet seinen Aktualitäts Vektor beim Abschluss eines erfolgreichen Replikations Prozesses an das Ziel, um sicherzustellen, dass der Zieldomänen Controller weiß, dass er mit den Ursprungs Updates aller Domänen Controller synchronisiert wurde und sich die Updates auf derselben Ebene wie die Quelle befinden.  
2. **Obere Kontingentgrenze**: Ein vom Zieldomänencontroller verwalteter Wert zum Nachverfolgen der letzten Änderungen, die von einem bestimmten Quelldomänencontroller für eine bestimmte Partition eingegangen sind. Die obere Kontingentgrenze verhindert, dass dem Zieldomänencontroller vom Quelldomänencontroller wiederholt dieselben Änderungen gesendet werden.  

## <a name="directory-database-identity"></a>Verzeichnisdatenbankidentität

Neben USNs wird von Domänencontrollern auch die Verzeichnisdatenbankidentität der Quellreplikationspartner nachverfolgt. Die Identität der auf dem Server ausgeführten Verzeichnisdatenbank wird separat von der Identität des Serverobjekts selbst verwaltet. Die Verzeichnisdatenbankidentität wird auf den einzelnen Domänencontrollern im **invocationID**-Attribut des NTDS-Einstellungsobjekts gespeichert, das sich im folgenden LDAP-Pfad (Lightweight Directory Access-Protokoll) befindet: cn=NTDS Settings, cn=ServerName, cn=Servers, cn=*SiteName*, cn=Sites, cn=Configuration, dc=*ForestRootDomain*. Die Serverobjektidentität wird im **objectGUID**-Attribut des NTDS-Einstellungsobjekts gespeichert. Die Identität des Serverobjekts bleibt unverändert. Die Identität der Verzeichnisdatenbank hingegen ändert sich, wenn auf dem Server eine Systemstatuswiederherstellung ausgeführt wird oder wenn eine Anwendungsverzeichnispartition auf dem Server hinzugefügt, entfernt und dann erneut hinzugefügt wird. (anderes Szenario: Wenn eine HyperV-Instanz die VSS-Writer auf einer Partition auslöst, die die virtuelle Festplatte eines virtuellen Domänen Controllers enthält, löst der Gast wiederum seine eigenen VSS-Writer aus (derselbe Mechanismus, der von der Sicherung/Wiederherstellung verwendet wird), was zu einer anderen Methode führt, mit der invocationID zurückgesetzt wird.

Das **invocationID**-Attribut dient also letztlich dazu, einen Satz von Quellupdates auf einem Domänencontroller einer bestimmten Version der Verzeichnisdatenbank zuzuordnen. Anhand der beiden genannten Tabellen, Aktualitätsvektor und obere Kontingentgrenze, können die Domänencontroller - unter Verwendung der **invocationID** und der GUID des Domänencontrollers - feststellen, aus welcher Kopie der Active Directory-Datenbank bestimmte Replikationsinformationen stammen.

Die **invocationID** ist eine GUID (Globally Unique Identifier), die in einer der ersten Zeilen des Ausgabetexts angezeigt wird, nachdem Sie den Befehl **repadmin /showrepl** ausgeführt haben. Im Folgenden ein Beispiel für den Ausgabetext dieses Befehls:

   ```
   Repadmin: running command /showrepl against full DC local host
   Default-First-Site-Name\VDC1
   DSA Options: IS_GC
   DSA object GUID: 966651f3-a544-461f-9f2c-c30c91d17818
   DSA invocationID: b0d9208b-8eb6-4205-863d-d50801b325a9
   ```

Wenn die Active Directory-Domänendienste auf einem Domänencontroller ordnungsgemäß wiederhergestellt werden, wird die **invocationID** zurückgesetzt. Damit geht - entsprechend der Größe der zu replizierenden Partition - ein gesteigerter Replikationsdatenverkehr einher.

Angenommen, VDC1 und DC2 sind zwei Domänencontroller in derselben Domäne. Die folgende Abbildung zeigt, wie VDC1 von DC2 wahrgenommen wird, wenn der Wert der invocationID bei einer ordnungsgemäßen Wiederherstellung zurückgesetzt wird.

![](media/virtualized-domain-controller-architecture/Dd363553.ca71fc12-b484-47fb-991c-5a0b7f516366(WS.10).gif)

## <a name="usn-rollback"></a>USN-Rollback

Ein USN-Rollback erfolgt, wenn die regulären Updates der USNs umgangen werden und ein Domänencontroller eine USN zu verwenden versucht, die niedriger als das letzte Update ist. In den meisten Fällen wird ein Rollback für die Wiederverwendung in der Gesamtstruktur erkannt, und die Replikation wird beendet. 

Ein USN-Rollback kann viele Ursachen haben: beispielsweise die Verwendung alter VHD-Dateien oder die Ausführung einer P2V-Konvertierung, ohne sicherzustellen, dass der physische Computer nach der Konvertierung dauerhaft offline bleibt. Mit den folgenden Maßnahmen können Sie die Ausführung von USN-Rollbacks verhindern:

   - Verwenden Sie keine Momentaufnahme eines virtuellen Domänen Controller Computers, wenn Windows Server 2012 oder höher nicht ausgeführt wird.
   - Kopieren Sie die VHD-Datei des Domänencontrollers nicht.  
   - Wenn Windows Server 2012 oder höher nicht ausgeführt wird, exportieren Sie nicht den virtuellen Computer, auf dem ein Domänen Controller ausgeführt wird.  
   - Verwenden Sie zum Wiederherstellen eines Domänencontrollers oder zum Ausführen eines Rollbacks für die Inhalte einer Active Directory-Datenbank ausschließlich eine unterstützte Sicherungslösung, wie z. B. die Windows Server-Sicherung.  

In manchen Fällen bleibt ein USN-Rollback unerkannt. Es kann jedoch auch weitere Replikationsfehler zur Folge haben. Bei solchen Fehlern muss zunächst das Ausmaß des Problems festgestellt werden, um es dann zeitnah zu beheben. Informationen dazu, wie Sie veraltete Objekte entfernen, die als Ergebnis eines Rollbacks für die Benutzer-ID auftreten können, finden Sie unter [Veraltete Active Directory Objekte generieren der Ereignis-ID 1988 in Windows Server 2003](https://go.microsoft.com/fwlink/?linkid=137185) in der Microsoft Knowledge Base.

## <a name="usn-rollback-detection"></a>USN-Rollbackerkennung

USN-Rollbacks ohne Zurücksetzung der **invocationID** (verursacht durch unzulässige Wiederherstellungsverfahren) werden in den meisten Fällen erkannt. Windows Server 2008 bietet Schutzmaßnahmen, um zu verhindern, dass nach einem unzulässigen Wiederherstellungsvorgang für einen Domänencontroller eine Replikation ausgeführt wird. Diese Schutzmaßnahmen werden dadurch ausgelöst, dass ein unzulässiger Wiederherstellungsvorgang niedrigere USNs für Quelländerungen ergibt, die die Replikationspartner bereits empfangen haben.

Wenn unter Windows Server 2008 und Windows Server 2003 SP1 ein Zieldomänencontroller Änderungen über eine bereits verwendete USN anfordert, wird die Antwort des Quellreplikationspartners vom Zieldomänencontroller dahin gehend gedeutet, dass die Replikationsmetadaten veraltet sind. Dies bedeutet, dass für die Active Directory-Datenbank auf dem Quelldomänencontroller ein Rollback auf einen vorherigen Status ausgeführt wurde. Beispielsweise kann für die VHD-Datei eines virtuellen Computers ein Rollback auf eine vorherige Version ausgeführt worden sein. In diesem Fall werden vom Zieldomänencontroller die folgenden Quarantänemaßnahmen auf dem Domänencontroller gestartet, bei dem eine unzulässige Wiederherstellung festgestellt wurde:

   - Der Netzwerkanmeldedienst wird von den Active Directory-Domänendiensten angehalten, wodurch Benutzer- und Computerkonten am Ändern von Kontokennwörtern gehindert werden. Diese Maßnahme verhindert den Verlust solcher Änderungen im Anschluss an eine unzulässige Wiederherstellung.  
   - Die ein- und ausgehende Active Directory-Replikation wird von den Active Directory-Domänendiensten deaktiviert.  
   - Zur Meldung dieses Zustands wird von den Active Directory-Domänendiensten die Ereignis-ID 2095 im Verzeichnisdienst-Ereignisprotokoll generiert.  

Die folgende Abbildung veranschaulicht die Abfolge von Ereignissen, wenn ein USN-Rollback auf VDC2, dem auf einem virtuellen Computer ausgeführten Zieldomänencontroller, erkannt wird. In dieser Abbildung erfolgt die Erkennung des Anwendungs Rollbacks auf VDC2, wenn ein Replikations Partner erkennt, dass VDC2 einen Aktualitäts-UPN-Wert gesendet hat, der zuvor vom Zieldomänen Controller erkannt wurde. Dies deutet darauf hin, dass dies-Datenbank in der Zeit nicht ordnungsgemäß ein Rollback ausgeführt hat.

![](media/virtualized-domain-controller-architecture/Dd363553.373b0504-43fc-40d0-9908-13fdeb7b3f14(WS.10).gif)

Wenn im Verzeichnisdienst-Ereignisprotokoll die Ereignis-ID 2095 gemeldet wird, führen Sie sofort das folgende Verfahren aus:

## <a name="to-resolve-event-id2095"></a>So beheben Sie die Ereignis-ID 2095

1. Trennen Sie die Netzwerkverbindung des virtuellen Computers, von dem der Fehler aufgezeichnet wurde.
2. Versuchen Sie festzustellen, ob Änderungen dieses Domänencontrollers an andere Domänencontroller weitergegeben wurden. Falls das Ereignis auf den Start eines Snapshots oder einer Kopie eines virtuellen Computers zurückzuführen ist, versuchen Sie den Zeitpunkt des USN-Rollbacks festzustellen. Anschließend können Sie die Replikationspartner des Domänencontrollers auf Replikationen nach diesem Zeitpunkt überprüfen.

   Hierfür eignet sich das Tool Repadmin. Informationen zur Verwendung von Repadmin finden [Sie unter Überwachung und Problembehandlung Active Directory Replikation mit repadmin](https://go.microsoft.com/fwlink/?linkid=122830). Wenn Sie dies nicht selbst ermitteln können, wenden Sie sich an [Microsoft-Support](https://support.microsoft.com) , um Unterstützung zu erhalten.

3. Erzwingen Sie eine Herabstufung des Domänencontrollers. Dies umfasst das Bereinigen der Metadaten des Domänen Controllers und das übernehmen der Betriebs Master Rollen (auch als Flexible Single Master Operations oder FSMO bezeichnet). Weitere Informationen finden Sie im Abschnitt "Wiederherstellen von einem Rollback für die [Windows Server 2003, Windows Server 2008 und Windows Server 2008 R2](https://go.microsoft.com/fwlink/?linkid=137182) " in der Microsoft Knowledge Base in der Microsoft Knowledge Base.
4. Löschen Sie alle vorherigen VHD-Dateien für den Domänencontroller.

## <a name="undetected-usn-rollback"></a>Unerkanntes USN-Rollback

Ein USN-Rollback wird in den folgenden beiden Fällen möglicherweise nicht erkannt:

1. Die VHD-Datei ist unterschiedlichen virtuellen Computern zugeordnet, die an verschiedenen Standorten gleichzeitig ausgeführt werden.  
2. Die USN auf dem wiederhergestellten Domänencontroller ist höher als die letzte USN, die vom anderen Domänencontroller empfangen wurde.  

Im ersten Fall können infolge einer Replikation mit anderen Domänencontrollern Änderungen auf einem der virtuellen Computer auftreten, die nicht an den anderen virtuellen Computer repliziert werden. Solche Abweichungen in der Gesamtstruktur sind schwer zu erkennen. Das Resultat sind unvorhersehbare Verzeichnisantworten. Die beschriebene Situation kann nach einer P2V-Migration eintreten, wenn sowohl der physische als auch der virtuelle Computer im selben Netzwerk ausgeführt werden. Möglich ist diese Situation auch, wenn mehrere virtuelle Domänencontroller vom selben physischen Domänencontroller erstellt und dann im selben Netzwerk ausgeführt werden.

Im zweiten Fall gilt ein USN-Bereich für zwei unterschiedliche Änderungen. Dieses Problem kann sich über längere Zeit fortsetzen, ohne erkannt zu werden. Wenn jedoch ein während dieses Zeitraums erstelltes Objekt geändert wird, wird ein veraltetes Objekt erkannt und als Ereignis-ID 1988 in der Ereignisanzeige gemeldet. Die folgende Abbildung veranschaulicht, wie ein USN-Rollback in einer solchen Situation möglicherweise nicht erkannt wird.

![](media/virtualized-domain-controller-architecture/Dd363553.63565fe0-d970-4b4e-b5f3-9c76bc77e2d4(WS.10).gif)

## <a name="read-only-domain-controllers"></a>Schreibgeschützte Domänencontroller

RODCs sind Domänencontroller, auf denen schreibgeschützte Kopien der Partitionen einer Active Directory-Datenbank gehostet werden. Da RODCs keine Änderungen an andere Domänencontroller replizieren, werden die meisten Probleme im Zusammenhang mit USN-Rollbacks vermieden. Kommt es jedoch zur Replikation mit einem beschreibbaren Domänencontroller, der von einem USN-Rollback betroffen ist, dann ist auch der RODC betroffen.

Von der Wiederherstellung eines RODCs mithilfe eines Snapshots wird abgeraten. Verwenden Sie zur Wiederherstellung von RODCs eine Active Directory-kompatible Sicherungsanwendung. Zudem muss wie auch bei beschreibbaren Domänencontrollern darauf geachtet werden, dass RODCs nicht länger als die Tombstone-Lebensdauer offline bleiben. Andernfalls kann es auf den RODCs zu veralteten Objekten kommen.

Weitere Informationen zu RODCs finden [Sie im Planungs-und Bereitstellungs Handbuch für schreibgeschützte Domänen Controller](../../deploy/rodc/read-only-domain-controller-updates.md).
