---
Title: Virtualisieren von Domänencontrollern, die mit Hyper-V
description: Überlegungen bei der Windows Server Active Directory-Domänencontrollern in Hyper-V-Virtualisierung
author: MicrosoftGuyJFlo
ms.author: joflore
ms.date: 04/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.openlocfilehash: 297c2a26f10503cb68ae241576a72e08aa4e55a0
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469568"
---
# <a name="virtualizing-domain-controllers-using-hyper-v"></a>Virtualisieren von Domänencontrollern, die mit Hyper-V

> Gilt für: Windows Server 2016

In diesem Thema wird aktualisiert werden, um die Anleitungen zu Windows Server 2016 anwendbar zu machen. Windows Server 2012 enthält viele Verbesserungen für virtualisierte Domänencontroller (DCs), einschließlich der Sicherheitsmaßnahmen, um USN-Rollback auf virtuelle DCs und die Möglichkeit zum Klonen von virtuellen DCs zu verhindern. Weitere Informationen zu diesen Verbesserungen finden Sie unter [Einführung in die Active Directory Domain Services (AD DS) Virtualization (Level 100)](../../introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100.md).

Hyper-V werden unterschiedliche Serverrollen auf einem einzelnen physischen Computer konsolidiert. In diesem Leitfaden wird beschrieben, wie Domänencontroller als 32-Bit- oder 64-Bit-Gastbetriebssysteme ausgeführt werden.

## <a name="planning-to-virtualize-domain-controllers"></a>Überlegungen zur Planung für virtualisierte Domänencontroller

Themen dieses Abschnitts sind die Hardwareanforderungen für Hyper-V-Server, die Vermeidung einzelner Fehlerquellen (Single Points of Failure, SPOFs), die Auswahl des geeigneten Konfigurationstyps für die Server und virtuellen Computer der Hyper-V-Umgebung sowie Überlegungen zur Sicherheit und Leistung.

## <a name="hyper-v-requirements"></a>Anforderungen für Hyper-V

Zum Installieren und verwenden Sie die Hyper-V-Serverrolle, müssen Sie über Folgendes verfügen:

   - **X X64 Prozessor**
      - Hyper-V ist in x64-basierten Versionen von Windows Server 2008 oder höher verfügbar.  
   - **Eine hardwaregestützte Virtualisierung**
      - Dieses Feature ist verfügbar für Prozessoren mit Virtualisierungsoption, d. h., Intel Virtualization Technology (Intel VT) oder AMD Virtualization (AMD-V).  
   - **Hardware Data Execution Protection (DEP)**
      - Die Hardware-Datenausführungsverhinderung muss verfügbar und aktiviert sein. Das heißt, Sie müssen Intel XD-Bit (Execute Disable Bit) oder AMD NX-Bit (No Execute Bit) aktivieren.  

## <a name="avoid-creating-single-points-of-failure"></a>Vermeiden des Erstellens einzelner Fehlerpunkte

Versuchen Sie, das Erstellen potenzieller einzelner Fehlerpunkte beim Planen der virtuellen Domänencontrollerbereitstellung zu vermeiden. Sie können das Einführen potenzieller einzelner Fehlerpunkte durch das Implementieren von Systemredundanz vermeiden. Beachten Sie z. B. die folgenden Empfehlungen und die potenziell höheren Verwaltungskosten:

1. Führen Sie mindestens zwei virtualisierte Domänencontroller pro Domäne auf anderen Virtualisierungshosts aus. Dadurch wird das Risiko verringert, bei Ausfall eines Virtualisierungshosts alle Domänencontroller zu verlieren.  
2. Diversifizieren Sie die Hardware (mit anderen CPUs, Hauptplatinen, Netzwerkadaptern oder anderer Hardware), auf der die Domänencontroller ausgeführt werden, wie für andere Technologien empfohlen. Hardwarediversifizierung grenzt mögliche Schäden ein, die durch eine Fehlfunktion verursacht werden, die für eine Herstellerkonfiguration, einen Treiber, ein einzelnes Hardwaregerät oder einen Hardwaretyp spezifisch sind.  
3. Domänencontroller sollten möglichst auf Hardware ausgeführt werden, die sich in anderen Regionen der Welt befindet. Dadurch werden die Auswirkungen von Notfällen oder Fehlern reduziert, die sich auf eine Website auswirken, auf der die Domänencontroller gehostet werden.  
4. Unterhalten Sie physische Domänencontroller an allen Domänen. Dadurch wird das Risiko einer Fehlfunktion der Virtualisierungsplattform verringert, die sich auf alle Hostsysteme auswirkt, die diese Plattform verwenden.  

## <a name="security-considerations"></a>Sicherheitsüberlegungen

Der Hostcomputer, auf dem virtuelle Domänencontroller ausgeführt werden, muss so sorgfältig wie ein beschreibbarer Domänencontroller verwaltet werden, selbst wenn es sich bei diesem Computer nur um einen Computer, der einer Domäne angehört, oder um einen Arbeitsgruppencomputer handelt. Dies ist ein wichtiger Sicherheitsaspekt. Ein fehlerhaft verwalteter Host ist anfällig für einen Rechteerweiterungsangriff, der auftritt, wenn sich ein böswilliger Benutzer Zugriff verschafft und Systemberechtigungen nicht autorisiert oder nicht ordnungsgemäß zugewiesen wurden. Ein böswilliger Benutzer kann mit einem solchen Angriff alle von diesem Computer gehosteten virtuellen Computer, Domänen, und Gesamtstrukturen gefährden.

Berücksichtigen Sie unbedingt die folgenden Sicherheitsaspekte, wenn Sie Domänencontroller virtualisieren möchten:

   - Der lokale Administrator eines Computers, von dem virtuelle, beschreibbare Domänencontroller gehostet werden, sollte bezüglich der Anmeldeinformationen als gleichwertig betrachtet werden mit dem Standarddomänenadministrator aller Domänen und Gesamtstrukturen, denen diese Domänencontroller angehören.  
   - Zur Vermeidung von Sicherheits- und Leistungsproblemen wird als Konfiguration empfohlen, auf einem Host eine Server Core-Installation von Windows Server 2008 oder höher mit Hyper-V als einziger Anwendung auszuführen. Je weniger Anwendungen und Dienste auf dem Server installiert sind, desto höher ist die Leistung und desto geringer ist das Risiko von Angriffen auf den Computer oder das Netzwerk über installierte Anwendungen oder Dienste. Diese Art von Konfiguration hat eine so genannte reduzierte Angriffsfläche zur Folge. Für eine Zweigstelle oder andere Standorten, die nicht ausreichend geschützt werden können, wird ein schreibgeschützter Domänencontroller (Read-only Domain Controller, RODC) empfohlen. Falls ein separates Verwaltungsnetzwerk vorhanden ist, sollte der Host nur mit dem Verwaltungsnetzwerk verbunden werden.  
   - Sie können Bitlocker mit Ihren Domänencontrollern, seit Windows Server 2016 können Sie die virtuelle TPM-Funktion auch bieten das Gast-Schlüsselmaterial Entsperren des Systemvolumes.
   - [Überwachten Fabric und abgeschirmte VMs](/it-server/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) bieten zusätzliche Steuerelemente, um Ihren Domänencontrollern zu schützen.

Weitere Informationen zu RODCs finden Sie unter [Read-Only Domain Controller Planungs- und Bereitstellungshandbuch](../../deploy/rodc/read-only-domain-controller-updates.md).

Weitere Informationen zum Schützen von Domänencontrollern finden Sie unter [Leitfaden mit bewährten Methoden zum Absichern von Active Directory-Installationen](../../plan/security-best-practices/best-practices-for-securing-active-directory.md).

## <a name="security-boundaries-for-different-host-and-guest-configurations"></a>Sicherheitsbegrenzungen für unterschiedliche Host- und Gastkonfigurationen

Die Verwendung virtueller Computer ermöglicht viele verschiedene Konfigurationen von Domänencontrollern. Die Art und Weise, wie virtuelle Computer Begrenzungen und Vertrauensstellungen in Ihrer Active Directory-Topologie beeinflussen, muss sorgfältig berücksichtigt werden. Mögliche Konfigurationen für einen Active Directory-Domänencontroller und einen Host (Hyper-V-Server) und dessen Gastcomputer (virtuelle Computer, die auf dem Hyper-V-Server ausgeführt werden) werden in der folgenden Tabelle beschrieben.

|Computer|Konfiguration 1|Konfiguration 2|
|-------|---------------|---------------|
|Host|Arbeitsgruppen- oder Mitgliedscomputer|Arbeitsgruppen- oder Mitgliedscomputer|
|Gast|Domänencontroller|Arbeitsgruppen- oder Mitgliedscomputer|

![](media/virtualized-domain-controller-architecture/Dd363553.f44706fd-317e-4f0b-9578-4243f4db225f(WS.10).gif)

   - Der Administrator auf dem Hostcomputer hat die gleichen Zugriffsrechte wie ein Domänenadministrator auf die beschreibbaren Domänencontrollergäste und muss als solcher behandelt werden. Bei einem RODC-Gast hat der Administrator des Hostcomputers die gleichen Zugriffsrechte wie ein lokaler Administrator auf den Gast-RODC.   
   - Ein Domänencontroller in einem virtuellen Computer hat Administratorrechte auf dem Host, wenn der Host derselben Domäne angehört. Ein böswilliger Benutzer, der sich zunächst Zugriff auf den virtuellen Computer 1 verschafft, kann alle virtuellen Computer gefährden. Dieses Phänomen wird als Angriffsvektor bezeichnet. Wenn Domänencontroller für mehrere Domänen oder Gesamtstrukturen vorhanden sind, sollten diese Domänen zentral verwaltet werden, wobei der Administrator einer Domäne für alle Domänen vertrauenswürdig ist.  
   - Die Angriffsmöglichkeit vom virtuellen Computer 1 aus besteht, selbst wenn der virtuelle Computer 1 als RODC installiert wird. Der Administrator eines RODC verfügt zwar nicht explizit über Domänenadministratorrechte, aber der RODC kann zum Senden von Richtlinien an den Hostcomputer verwendet werden. Diese Richtlinien können Skripts zum Starten beinhalten. Wenn dieser Vorgang erfolgreich ist, ist der Hostcomputer gefährdet und in der Folge auch die anderen virtuellen Computer auf dem Hostcomputer.  

## <a name="security-of-vhd-files"></a>Sicherheit von VHD-Dateien

Eine VHD-Datei eines virtuellen Domänencontrollers entspricht der physischen Festplatte eines physischen Domänencontrollers. Als solche sollte sie genauso sorgfältig wie die Festplatte eines physischen Domänencontrollers geschützt werden. Stellen Sie sicher, dass nur zuverlässige und vertrauenswürdige Administratoren Zugriff auf die VHD-Dateien des Domänencontrollers haben.

## <a name="rodcs"></a>RODCs

RODCs haben den Vorteil, dass sie an Standorten verwendet werden können, wo die physische Sicherheit nicht garantiert werden kann, wie z. B. in Zweigstellen. Sie können Windows BitLocker Drive Encryption verwenden, um VHD-Dateien selbst schützen (nicht die Dateisysteme darin) aus, die auf dem Host durch den Diebstahl des physischen Datenträgers beeinträchtigt wird. 

## <a name="performance"></a>Leistung

Die neue Microkernel-64-Bit-Architektur ermöglicht im Vergleich zu früheren Virtualisierungsplattformen eine erhebliche Leistungsverbesserung. Zur Optimierung der Hostleistung sollte für den Host eine Server Core-Installation von Windows Server 2008 oder höher vorgesehen werden, und außer Hyper-V sollten keine anderen Serverrollen installiert werden.

Die Leistung von virtuellen Computern hängt insbesondere von der Arbeitsauslastung ab. Testen Sie verschiedene Topologien, um eine zufriedenstellende Leistung von Active Directory zu garantieren. Bewerten Sie die aktuelle arbeitsauslastung über einen Zeitraum mit einem Tool wie der Zuverlässigkeits- und Leistungsüberwachung (%% amp;quot;Perfmon.msc%%amp;quot;) oder die [Microsoft Assessment and Planning (MAP) Toolkit](https://go.microsoft.com/fwlink/?linkid=137077). Das MAP-Tool ist außerdem hilfreich, wenn Sie eine Bestandsaufnahme aller Server und Serverrollen machen möchten, die derzeit in Ihrem Netzwerk vorhanden sind.

Um einen allgemeinen Überblick über die Leistung virtualisierter Domänencontroller zu erhalten, die folgenden Leistungstests wurden durchgeführt, der die [Active Directory Performance Testtool (ADTest.exe)](https://go.microsoft.com/fwlink/?linkid=137088).

LDAP-Tests (Lightweight Directory Access-Protokoll) wurden auf einem physischen Domänencontroller mit ADTest.exe und anschließend auf einem virtuellen Computer, der auf einem mit dem physischen Domänencontroller identischen Server gehostet wurde, ausgeführt. Nur ein logischer Prozessor wurde für den physischen Computer verwendet, und nur ein virtueller Prozessor wurde für den virtuellen Computer verwendet, um problemlos eine CPU-Auslastung von 100 % zu erreichen. In der folgenden Tabelle bezeichnen der Buchstabe und die Zahl in Klammern (jeweils nach der Testbeschreibung) die verschiedenen Tests von %amp;quot;ADTest.exe%%amp;quot;. Die Leistung des virtualisierten Domänencontrollers betrug demnach zwischen ca. 88 und 98 % von der des physischen Domänencontrollers.

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
<th>Messwert</th>
<th>Test</th>
<th>Physikalisch</th>
<th>Virtuell</th>
<th>Delta</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Suchanfragen/Sek</p></td>
<td><p>Suche nach allgemeinem Namen im Basisbereich (L1)</p></td>
<td><p>11508</p></td>
<td><p>10276</p></td>
<td><p>-10.71%</p></td>
</tr>
<tr class="even">
<td><p>Suchanfragen/Sek</p></td>
<td><p>Suche nach einem Attributsatz im Basisbereich (L2)</p></td>
<td><p>10123</p></td>
<td><p>9005</p></td>
<td><p>-11.04%</p></td>
</tr>
<tr class="odd">
<td><p>Suchanfragen/Sek</p></td>
<td><p>Suche nach allen Attributen im Basisbereich (L3)</p></td>
<td><p>1284</p></td>
<td><p>1242</p></td>
<td><p>-3.27%</p></td>
</tr>
<tr class="even">
<td><p>Suchanfragen/Sek</p></td>
<td><p>Suche nach allgemeinem Namen im Unterstrukturbereich (L6)</p></td>
<td><p>8613</p></td>
<td><p>7904</p></td>
<td><p>-8.23%</p></td>
</tr>
<tr class="odd">
<td><p>Erfolgreiche Bindungen/s</p></td>
<td><p>Ausführen schneller Bindungen (B1)</p></td>
<td><p>1438</p></td>
<td><p>1374</p></td>
<td><p>-4.45%</p></td>
</tr>
<tr class="even">
<td><p>Erfolgreiche Bindungen/s</p></td>
<td><p>Ausführen einfacher Bindungen (B2)</p></td>
<td><p>611</p></td>
<td><p>550</p></td>
<td><p>-9.98%</p></td>
</tr>
<tr class="odd">
<td><p>Erfolgreiche Bindungen/s</p></td>
<td><p>Ausführen von Bindungen mithilfe von NTLM (B5)</p></td>
<td><p>1068</p></td>
<td><p>1056</p></td>
<td><p>-1.12%</p></td>
</tr>
<tr class="even">
<td><p>Schreibvorgänge/s</p></td>
<td><p>Schreiben mehrerer Attribute (W2)</p></td>
<td><p>6467</p></td>
<td><p>5885</p></td>
<td><p>-9.00%</p></td>
</tr>
</tbody>
</table>

Um eine zufriedenstellende Leistung sicherzustellen, wurden Integrationskomponenten installiert, damit das Gastbetriebssystem "Optimierungen" oder hypervisorkompatible synthetische Treiber verwenden kann. Während des Installationsvorgangs müssen möglicherweise emulierte IDE- oder Netwerkadapter-Treiber verwendet werden. In Produktionsumgebungen sollten Sie diese emulierten Treiber durch synthetische Treiber ersetzen, um die Leistung zu optimieren.

Wenn Sie die Leistung von virtuellen Computern mit der Zuverlässigkeits- und Leistungsüberwachung (Perfmon.msc) überwachen, stimmen die CPU-Informationen innerhalb des virtuellen Computers aufgrund der Art und Weise, wie die virtuelle CPU auf dem physischen Prozessor eingeplant wird, nicht genau. Wenn Sie CPU-Information für einen virtuellen Computer abrufen möchten, der auf einem Hyper-V-Server ausgeführt wird, verwenden Sie den Leistungsindikator Logischer Prozessor für Hyper-V-Hypervisor in der Hostpartition.

Weitere Informationen zur leistungsoptimierung für AD DS und Hyper-V, finden Sie unter [Performance Tuning Richtlinien für Windows Server 2016](../../../../administration/performance-tuning/index.md).

Darüber hinaus sollten Sie keine differenzierende virtuelle Festplatte auf einem virtuellen Computer verwenden, der als Domänencontroller konfiguriert ist, da durch die differenzierende virtuelle Festplatte die Leistung beeinträchtigt werden kann. Weitere Informationen zu Hyper-V-Datenträgertypen, einschließlich differenzierender Datenträger, finden Sie unter [Assistenten für neue virtuelle Festplatte](http://go.microsoft.com/fwlink/?linkid=137279).

Weitere Informationen zu AD DS in virtuellen Hostumgebungen finden Sie unter [Punkte zu berücksichtigen, wenn Sie Active Directory-Domänencontrollern in virtuellen Hostumgebungen hosten](https://go.microsoft.com/fwlink/?linkid=141292) in der Microsoft Knowledge Base.

## <a name="deployment-considerations-for-virtualized-domain-controllers"></a>Überlegungen zur Bereitstellung für virtualisierte Domänencontroller

Mehrere gängige Praktiken im Zusammenhang mit virtuellen Computern sollten bei der Bereitstellung virtualisierter Domänencontroller vermieden werden. Zudem gelten spezielle Empfehlungen für die Zeitsynchronisierung und Speicherung.

## <a name="virtualization-deployment-practices-to-avoid"></a>Bei der Virtualisierungsbereitstellung zu vermeidende Praktiken

Virtualisierungsplattformen wie z. B. Hyper-V bieten eine Reihe von Features, die das Verwalten, Warten, Sichern und Migrieren von Computern vereinfachen. Bei der Bereitstellung virtualisierter Domänencontroller empfiehlt es sich jedoch, die folgenden gängigen Praktiken (und zugehörigen Features) zu vermeiden:

- Um die Dauerhaftigkeit von Active Directory-Schreibvorgängen zu gewährleisten, stellen Sie keine Datenbankdateien für einen virtuellen Domänencontroller (Active Directory-Datenbank (NTDS. DIT), Protokolle und SYSVOL) auf virtuelle IDE-Datenträger. Stattdessen erstellen Sie eine zweite virtuelle Festplatte an einen virtuellen SCSI-Controller angefügt, und stellen Sie sicher, dass die Datenbank, Protokolle und SYSVOL auf dem SCSI-Datenträger des virtuellen Computers während der Installation des Domänencontrollers platziert werden.  
- Implementieren Sie keine differenzierenden virtuellen Festplatten (Virtual Hard Disk, VHD) auf einem virtuellen Computer, den Sie als Domänencontroller konfigurieren. Dadurch kann eine frühere Version zu einfach wiederhergestellt werden, und außerdem wird die Leistung reduziert. Weitere Informationen zu VHD-Typen finden Sie unter [Assistenten für neue virtuelle Festplatte](https://go.microsoft.com/fwlink/?linkid=137279).  
- Stellen Sie keine neuen Active Directory-Domänen und Gesamtstrukturen in einer Kopie eines Windows Server-Betriebssystems, die nicht zuerst vorbereitet wurde das Systemvorbereitungstool (Sysprep) verwenden. Weitere Informationen zum Ausführen von Sysprep finden Sie unter [Sysprep (Systemvorbereitung)-Übersicht](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview)

   > [!WARNING]
   > Die Ausführung von Sysprep auf einem Domänencontroller wird nicht unterstützt.

- Um eine potenzielle Rollbacksituation der Aktualisierungssequenznummern (Update Sequence Number, USN) zu vermeiden, sollten Sie keine Kopien einer VHD-Datei, die einen bereits bereitgestellten Domänencontroller repräsentiert, zum Bereitstellen zusätzlicher Domänencontroller verwenden. Weitere Informationen zu USN-Rollbacks, finden Sie unter [USN und USN-Rollback](#usn-and-usn-rollback).
   - WindowsServer 2012 und höher kann Administratoren Domain Controller-Images zu klonen, wenn ordnungsgemäß vorbereitet werden, wenn sie zusätzliche Domänencontroller bereitstellen möchten.
- Verwenden Sie das Exportfeature von Hyper-V nicht zum Exportieren eines virtuellen Computers, auf dem ein Domänencontroller ausgeführt wird.
  - Mit Windows Server 2012 und höher ein exportieren und Importieren eines virtuellen Domänencontrollers-Gasts erfolgt wie eine nicht autoritative Wiederherstellung wie eine Änderung der Generations-ID erkannt und nicht für das Klonen konfiguriert ist.
  - Stellen Sie sicher, dass Sie nicht das Gastbetriebssystem verwenden, das Sie nicht mehr exportiert.
    - Sie können Hyper-V-Replikation verwenden, um eine zweite inaktiv Kopie eines Domänencontrollers zu halten. Wenn Sie das replizierte Abbild starten, müssen Sie auch, eine ordnungsgemäße Bereinigung aus demselben Grund wie die Verwendung von der Quelle nicht nach dem Exportieren einer DC-Gast-Image ausführen.

## <a name="physical-to-virtual-migration"></a>Physical-to-Virtual-Migration (P2V)

System Center Virtual Machine Manager (VMM) 2008 ermöglicht die einheitliche Verwaltung physischer und virtueller Computer. Außerdem kann ein physischer Computer zu einem virtuellen Computer migriert werden. Diese Vorgang wird als P2V-Konvertierung (Physical-to-Virtual) bezeichnet. Während der P2V-Konvertierung der neuen virtuellen Maschine und der physische Domänencontroller, der migriert wird müssen nicht ausgeführt werden zur gleichen Zeit, um eine USN-rollbacksituation zu vermeiden, wie in beschrieben [USN und USN-Rollback](#usn-and-usn-rollback).

Sie sollten die P2V-Konvertierung im Offlinemodus ausführen, damit die Verzeichnisdaten einheitlich sind, wenn der Domänencontroller wieder eingeschaltet wird. Die Offlinemodusoption wird im Assistenten zum Konvertieren des physischen Servers angeboten und empfohlen. Eine Beschreibung des Unterschieds zwischen dem Online- und Offlinemodus, finden Sie unter [P2V: Konvertieren physischer Computer in virtuelle Maschinen in VMM](https://go.microsoft.com/fwlink/?linkid=155072). Während der P2V-Konvertierung sollte der virtuelle Computer nicht mit dem Netzwerk verbunden sein. Aktivieren Sie den Netzwerkadapter des virtuellen Computers erst nach Abschluss und Überprüfung der P2V-Konvertierung. Zu diesem Zeitpunkt ist der physische Quellcomputer ausgeschaltet. Binden Sie den physischen Quellcomputer erst wieder in das Netzwerk ein, nachdem Sie die Festplatte neu formatiert haben.

> [!NOTE]
> Es sind sicherere Optionen zum Erstellen von neuen virtuelle DCs, die nicht die Risiken der Erstellung von einem USN-Rollback ausführen. Sie können ein neues virtuelles Domänencontrollers durch reguläre heraufstufung Verlagerung von die Install from Media (IfM), und auch mit Domänencontroller zu klonen, einrichten, wenn Sie bereits mindestens einen virtuellen Domänencontroller verfügen.
Auch dadurch zur Vermeidung von Problemen mit der Hardware oder Plattform Probleme im Zusammenhang mit P2V-konvertiert virtuelle Gastcomputer auftreten.

> [!WARNING]
> Um Probleme mit Active Directory-Replikation zu vermeiden, stellen Sie sicher, dass nur eine Instanz (physisch oder virtuell) von einer bestimmten Domäne Controller vorhanden ist in einem bestimmten Netzwerk jederzeit rechtzeitig.
> Sie können die Wahrscheinlichkeit, dass der alte Klon wird ein Problem verringern:
> 
> - Wenn der neue virtuelle Domänencontroller ausgeführt wird, ändern Sie das Kennwort des Computerkontos zweimal mit: Netdom Resetpwd/Server: < Domänencontroller >...
> - Exportieren und Importieren des neuen virtuellen Gasts, um zu erzwingen, dass die Datei eine neue Generation-ID und daher den Aufruf einer Datenbank-ID.
> 

## <a name="using-p2v-migration-to-create-test-environments"></a>Erstellen von Testumgebungen mithilfe der P2V-Migration

Mithilfe der P2V-Migration über VMM können Sie Testumgebungen erstellen. Produktionsdomänencontroller können von physischen Computern zu virtuellen Computern migriert werden, um eine Testumgebung zu erstellen, ohne die Produktionsdomänencontroller permanent herunterzufahren. Die Testumgebung muss sich jedoch in einem anderen Netzwerk als die Produktionsumgebung befinden, falls zwei Instanzen desselben Domänencontrollers vorhanden sein sollen. Gehen Sie beim Erstellen von Testumgebungen mit der P2V-Migration äußerst vorsichtig vor, um USN-Rollbacks zu vermeiden, die sich negativ auf Ihre Test- und Produktionsumgebungen auswirken können. Mithilfe der folgenden Methode können Sie Testumgebungen mit P2V erstellen.

Ein in der Produktion Domänencontroller aus jeder Domäne wird in einen virtuellen Testcomputer mithilfe von P2V nach den Empfehlungen im Abschnitt Physical-to-virtual-Migration migriert. Die physischen Produktionscomputer und die virtuellen Testcomputer müssen sich in unterschiedlichen Netzwerken befinden, wenn sie wieder online geschaltet werden. Um USN-Rollbacks in der Testumgebung zu vermeiden, müssen alle Domänencontroller, die von physischen Computern zu virtuellen Computern migriert werden sollen, offline geschaltet werden. (Beenden Sie dazu den NTDS-Dienst, oder starten Sie den Computer im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM) neu.) Wenn die Domänencontroller offline sind, sollten in der Umgebung keine neuen Updates vorgenommen werden. Die Computer müssen während der P2V-Migration offline bleiben. Keiner der Computer sollte wieder online geschaltet werden, bevor alle Computer vollständig migriert wurden. Weitere Informationen zu USN-Rollbacks, finden Sie unter "USN und USN-Rollback".

Nachfolgende Testdomänencontroller sollten in der Testumgebung als Replikate heraufgestuft werden.

## <a name="time-service"></a>Zeitdienst

Für virtuelle Computer, die als Domänencontroller konfiguriert sind, empfiehlt es sich, dass das Deaktivieren der zeitsynchronisierung zwischen dem Betriebssystem des Hosts und dem Gastbetriebssystem, die als Domänencontroller fungieren. Dadurch wird Ihre gastdomänencontroller, Uhrzeit, aus der Domäne zu synchronisieren.

Zum Deaktivieren der Hyper-V-Zeitanbieter Synchronisierung Herunterfahren Sie des virtuellen Computers, und deaktivieren Sie das Kontrollkästchen Zeit Synchronisierung unter Integration Services.

> [!NOTE]
> Dieser Leitfaden wurde kürzlich aktualisiert wurde, entsprechend der vorherigen Empfehlung der zeitsynchronisierung zwischen dem Host teilweise zu deaktivieren, anstatt die aktuelle Empfehlung, die zeitsynchronisierung für den Gast-Domänencontroller aus der Domänenhierarchie Domänencontroller und dem Gastbetriebssystem.

## <a name="storage"></a>Speicher

Verwenden Sie die folgenden Empfehlungen zum Optimieren der Leistung des virtuellen Computers mit dem Domänencontroller und Dauerhaftigkeit von Schreibvorgängen für Active Directory stellen Sie sicher, für die Speicherung von Betriebssystem, Active Directory und VHD-Dateien:

- **Gastspeicherung**: Store, die Active Directory-Datenbankdatei (Ntds.dit), Protokolldateien und SYSVOL-Dateien auf einem separaten virtuellen Datenträger aus den Dateien des Betriebssystems. Erstellen Sie eine zweite virtuelle Festplatte an einen virtuellen SCSI-Controller angefügt, und speichern Sie die Datenbank, Protokolle und SYSVOL auf virtuellen SCSI-Datenträger des virtuellen Computers. Virtuelle SCSI-Datenträger bieten verbesserte Leistung im Vergleich zu virtuellen IDE, und sie Forced Unit Access (FUA) unterstützen. FUA wird sichergestellt, dass das Betriebssystem schreibt und liest Daten direkt aus den Medien, die allen Zwischenspeicherungsmechanismen zu umgehen.

  > [!NOTE]
  > Wenn Sie Bitlocker für den virtuellen DC Gast verwenden möchten, müssen Sie stellen Sie sicher, dass die zusätzlichen Volumes für "automatisch entsperren" konfiguriert sind.
  > Weitere Informationen zum Konfigurieren der automatischen entsperren finden Sie im [aktivieren-BitLockerAutoUnlock](https://docs.microsoft.com/powershell/module/bitlocker/enable-bitlockerautounlock)

- **Hostspeicherung von VHD-Dateien**. Empfehlungen: Die Empfehlungen für die Hostspeicherung beziehen sich auf die Speicherung von VHD-Dateien. Für eine optimale Leistung sollten Sie VHD-Dateien nicht auf einem Datenträger speichern, der häufig von anderen Diensten oder Anwendungen verwendet wird, wie z. B. auf dem Systemdatenträger, auf dem das Windows-Hostbetriebssystem installiert ist. Speichern Sie jede VHD-Datei auf einer vom Hostbetriebssystem und anderen VHD-Dateien getrennten Partition. Die ideale Konfiguration ist die Speicherung jeder VHD-Datei auf einem separaten physischen Laufwerk.  

  Die physischen Datenträger-Hostsystem muss auch erfüllen **mindestens** der folgenden Kriterien, die die Anforderungen der Datenintegrität virtualisierte arbeitsauslastung:  

   - Das System verwendet die Klasse-Server Datenträger (SCSI, Fibre Channel).  
   - Das System stellt sicher, dass es sich bei die Datenträgern ein Akku gestützte Zwischenspeichern Hostbusadapter (HBA) verbunden sind.  
   - Das System verwendet eine Speichercontroller (z. B. ein RAID-System) als das Speichergerät.  
   - Das System stellt sicher, dass es sich bei Power auf den Datenträger mit einer unterbrechungsfreien Stromversorgung (USV) geschützt ist.  
   - Das System stellt sicher, dass es sich bei dem Datenträger Schreibcache deaktiviert ist.  

- **Feste virtuelle Festplatten und Pass-Through-Datenträger**. Es gibt viele Methoden zum Konfigurieren der Speicherung für virtuelle Computer. Wenn VHD-Dateien verwendet werden, sind virtuelle Festplatten mit fester Größe effizienter als dynamische virtuelle Festplatten, da der Arbeitsspeicher für virtuelle Festplatten mit fester Größe beim Erstellen zugeordnet wird. Pass-Through-Datenträger, die von virtuellen Computern für den Zugriff physische Speichermedien verwenden können, weisen sogar eine noch optimalere Leistung auf. Pass-Through-Datenträger sind im Prinzip physische Datenträger oder logische Gerätenummern (Logical Unit Numbers, LUNs), die an einen virtuellen Computer angeschlossen sind. Das Snapshotfeature wird von Pass-Through-Datenträgern nicht unterstützt. Deshalb sind Pass-Through-Datenträger die bevorzugte Festplattenkonfiguration, da von der Verwendung von Snapshots zusammen mit Domänencontrollern abgeraten wird.  

Um das Risiko einer Beschädigung von Active Directory-Daten zu reduzieren, verwenden Sie virtuelle SCSI-Controller:

   - Verwenden Sie physische SCSI-Laufwerke (anstelle von IDE/ATA-Laufwerken) auf Hyper-V-Servern, von denen virtuelle Domänencontroller gehostet werden. Falls Sie keine SCSI-Laufwerke verwenden können, stellen Sie sicher, dass der Schreibcache auf den ATA/IDE-Laufwerken, von denen virtuelle Domänencontroller gehostet werden, deaktiviert ist. Weitere Informationen finden Sie unter [Ereignis-ID 1539/Datenbankintegrität](https://go.microsoft.com/fwlink/?linkid=162419).
   - Um die Dauerhaftigkeit des Active Directory gewährleisten schreibt, Active Directory-Datenbank, Protokolle und SYSVOL muss auf einen virtuellen SCSI-Datenträger platziert werden. Virtuelle SCSI-Datenträger unterstützen Forced Unit Access (FUA). FUA wird sichergestellt, dass das Betriebssystem schreibt und liest Daten direkt aus den Medien, die allen Zwischenspeicherungsmechanismen zu umgehen.  

## <a name="operational-considerations-for-virtualized-domain-controllers"></a>Überlegungen zur Verwendung für virtualisierte Domänencontroller

Für Domänencontroller, die auf virtuellen Computern ausgeführt werden, gelten im Gegensatz zu Domänencontrollern, die auf physischen Computern ausgeführt werden, Einschränkungen hinsichtlich der Verwendung. Bei Einsatz eines virtualisierten Domänencontrollers sollten bestimmte Praktiken und Features der Virtualisierungssoftware nicht verwendet werden:

   - Sie dürfen den gespeicherten Zustand eines Domänencontrollers in einem virtuellen Computer nicht für einen Zeitraum anhalten, beenden oder speichern, der die Tombstone-Lebensdauer der Gesamtstruktur überschreitet, und dann den Vorgang von dem angehaltenen oder gespeicherten Zustand fortsetzen. Dadurch können Probleme bei der Replikation verursacht werden. Vorgehensweise: bestimmen die Tombstone-Lebensdauer für die Gesamtstruktur finden Sie unter [Bestimmen der Tombstone-Lebensdauer für die Gesamtstruktur](https://go.microsoft.com/fwlink/?linkid=137177).  
   - Kopieren oder klonen Sie keine virtuellen Festplatten (Virtual Hard Disks, VHDs). Auch bei den Sicherungen für den Gast-VM eingerichtet einzelne VHDs noch kopiert werden können und verursachen USN-Rollback.
   - Erstellen oder verwenden Sie keinen Snapshot eines virtuellen Domänencontrollers. Es ist technisch mit Windows Server 2012 unterstützt und höher, es ist kein Ersatz für eine gute Sicherungsstrategie. Es gibt einige Gründe für DC-Momentaufnahmen oder Wiederherstellen von Momentaufnahmen.
   - Verwenden Sie keine differenzierende virtuelle Festplatte auf einem virtuellen Computer, der als Domänencontroller konfiguriert ist. Dadurch kann eine frühere Version zu einfach wiederhergestellt werden, und außerdem wird die Leistung reduziert.  
   - Verwenden Sie das Exportfeature nicht auf einem virtuellen Computer, auf dem ein Domänencontroller ausgeführt wird.  
   - Stellen Sie einen Domänencontroller einer Active Directory-Datenbank nur mit einer unterstützten Sicherung her bzw. führen Sie ein Rollback für die Inhalte einer Active Directory-Datenbank nur mit einer unterstützten Sicherung aus. Weitere Informationen finden Sie unter [Überlegungen sichern und Wiederherstellen für virtualisierte Domänencontroller](#backup-and-restore-practices-to-avoid).  

Durch diese Empfehlungen soll ein Rollback der Aktualisierungssequenznummern (Update Sequence Number, USN) vermieden werden. Weitere Informationen zu USN-Rollbacks finden Sie unter USN und USN-Rollback.

## <a name="backup-and-restore-considerations-for-virtualized-domain-controllers"></a>Überlegungen zum Sichern und Wiederherstellen für virtualisierte Domänencontroller

Das Sichern von Domänencontrollern ist für jede Umgebung eine wichtige Aufgabe. Sicherungen schützen bei Domänencontrollerfehlern oder administrativen Fehlern vor Datenverlust. Wenn ein solches Ereignis auftritt, muss für den Systemstatus des Domänencontrollers ein Rollback für einen Zeitpunkt vor Auftreten des Fehlers ausgeführt werden. Zum Wiederherstellen des fehlerfreien Status eines Domänencontrollers wird mithilfe einer Active Directory-kompatiblen Sicherungsanwendung wie z. B. der Windows Server-Sicherung eine Systemstatussicherung wiederhergestellt, die aus der aktuellen Installation des Domänencontrollers stammt. Weitere Informationen zur Verwendung von Windows Server-Sicherung mit Active Directory Domain Services (AD DS) finden Sie unter den [AD DS-Sicherung und Wiederherstellung schrittweise Anleitung für](https://go.microsoft.com/fwlink/?LinkId=138501).

Mit der Technologie der virtuellen Computer erhalten bestimmte Anforderungen von Active Directory-Wiederherstellungsvorgängen zusätzliche Bedeutung. Wenn Sie z. B. einen Domänencontroller mithilfe einer Kopie der VHD-Datei (Virtual Hard Disk, virtuelle Festplatte) wiederherstellen, umgehen Sie den wichtigen Schritt der Aktualisierung der Datenbankversion eines Domänencontrollers, nachdem er wiederhergestellt wurde. Die Replikation wird mit ungeeigneten Trackingnummern fortgesetzt, was zu einer inkonsistenten Datenbank unter den Domänencontrollerreplikaten führt. In den meisten Fällen wird dieses Problem nicht vom Replikationssystem erkannt, und trotz Inkonsistenzen zwischen Domänencontrollern werden keine Fehler gemeldet.

Ein einziges Verfahren wird zum Sichern und Wiederherstellen eines virtualisierten Domänencontrollers unterstützt:

1. Führen Sie die Windows Server-Sicherung im Gastbetriebssystem aus.  

Mit Windows Server 2012 und höher Hyper-V-Hosts und Gästen können Sie unterstützte Sicherungen von Domänencontrollern mithilfe von Momentaufnahmen, Gast-VM zum Exportieren und importieren und auch Hyper-V-Replikation nutzen. Alle diese sind jedoch keine gute Wahl für eine ordnungsgemäße Sicherungsverlauf mit geringfügige Ausnahme des Exports der Gast-VM zu erstellen.

Mit Windows Server 2016 Hyper-V-Unterstützung für "Produktion Momentaufnahmen" Hyper-V-Server eine VSS-basierte Sicherung des Gastbetriebssystems wird ausgelöst, und wenn der Gast und die Momentaufnahme abgeschlossen ist, der Host Ruft die virtuellen Festplatten und speichert sie in den Sicherungsspeicherort.

Wenngleich dies in Windows Server 2012 und höher funktioniert, besteht hierbei eine Inkompatibilität mit Bitlocker vor:

- AD möchte beim Ausrichten der VSS-versuchen, eine Aufgabe nach der Momentaufnahme, markieren Sie die Datenbank als Feedback aus einer Sicherung oder im Falle eine IFM-Quelle für RODC vorbereiten, entfernen Sie die Anmeldeinformationen aus der Datenbank auszuführen.
- Wenn das Volume Snapshot des für diese Aufgabe von Hyper-V bereitgestellt wird, besteht keine Möglichkeit, die das Volume für unverschlüsselten Zugriff entsperrt wird. Damit die AD-Datenbank-Engine besteht nicht den Zugriff auf die Datenbank und schließlich die Momentaufnahme.

> [!NOTE]
> Die abgeschirmte VM-Projekt, das erwähnt hat bereits einen Hyper-V-Hosts, die als nicht-Ziel für maximalen Datenschutz von der Gast-VM-Sicherung gesteuert.

## <a name="backup-and-restore-practices-to-avoid"></a>Bei der Sicherung und Wiederherstellung zu vermeidende Praktiken

Wie bereits erwähnt, gelten für auf virtuellen Computern ausgeführte Domänencontroller im Gegensatz zu auf physischen Computern ausgeführte Domänencontrollern Einschränkungen. Beim Sichern oder Wiederherstellen eines virtuellen Domänencontrollers sollten bestimmte Praktiken und Features der Virtualisierungssoftware nicht verwendet werden:

   - Kopieren oder klonen Sie keine VHD-Dateien von Domänencontrollern, anstatt regelmäßige Sicherungen auszuführen. Wenn die VHD-Datei kopiert oder geklont wird, führt dies dazu, dass sie veraltet ist. Klicken Sie dann, wenn die virtuelle Festplatte im normalen Modus gestartet wird, wird ein USN-Rollback auftreten. Sie sollten ordnungsgemäße Sicherungsvorgänge ausführen, die von Active Directory-Domänendiensten unterstützt werden. Beispielsweise können Sie das Feature der Windows Server-Sicherung verwenden.  
   - Verwenden Sie das Snapshotfeature nicht als Sicherung zum Wiederherstellen eines virtuellen Computers, der als Domänencontroller konfiguriert wurde. Bei der Replikation werden Probleme auftreten, wenn Sie den virtuellen Computer in einem früheren Zustand mit Windows Server 2008 R2 und älteren wiederherstellen. Weitere Informationen finden Sie unter [USN und USN-Rollback](#usn-and-usn-rollback). Die Verwendung eines Snapshots zum Wiederherstellen eines schreibgeschützten Domänencontrollers (Read-Only Domain Controller, RODC) verursacht zwar keine Replikationsprobleme, dennoch wird von dieser Wiederherstellungsmethode abgeraten.  

## <a name="restoring-a-virtual-domain-controller"></a>Wiederherstellen eines virtuellen Domänencontrollers

Sie müssen den Systemstatus regelmäßig sichern, um einen fehlerhaften Domänencontroller wiederherstellen zu können. Zum Systemstatus gehören Active Directory-Daten und -Protokolldateien, die Registrierung, das Systemvolume (Ordner SYSVOL) sowie verschiedene Elemente des Betriebssystems. Diese Anforderung unterscheidet sich nicht zwischen physischen und virtualisierten Domänencontrollern. Mit den von Active Directory-kompatiblen Sicherungsanwendungen ausgeführten Verfahren für die Systemstatuswiederherstellung soll nach einem Wiederherstellungsvorgang die Konsistenz lokaler und replizierter Active Directory-Datenbanken sichergestellt werden, wozu auch die Benachrichtigung von Replikationspartnern über Zurücksetzungen der Aufrufkennung gehört. Mithilfe von virtuellen Hostumgebungen und Datenträger- oder Betriebssystem-Abbilderstellungsanwendungen können Administratoren jedoch die Überprüfungen umgehen, die normalerweise beim Wiederherstellen des Domänencontroller-Systemstatus ausgeführt werden.

Wenn bei einem virtuellen Computer eines Domänencontrollers ein Fehler auftritt und kein Rollback der Aktualisierungssequenznummern (Update Sequence Number, USN) ausgeführt wird, gibt es zwei Möglichkeiten zum Wiederherstellen des virtuellen Computers:

   - Falls eine gültige Sicherung der Systemstatusdaten vorhanden ist, die vor dem Auftreten des Fehlers erstellt wurde, können Sie den Systemstatus mithilfe der Wiederherstellungsoption des Sicherungsprogramms wiederherstellen, mit dem Sie die Sicherung erstellt haben. Die Sicherung der Systemstatusdaten muss mit einem Active Directory-kompatiblen Sicherungsprogramm innerhalb der Tombstone-Lebensdauer erstellt worden sein, also standardmäßig vor maximal 180 Tagen. Sie sollten Ihre Domänencontroller mindestens immer bei Erreichen der Hälfte der Tombstone-Lebensdauer sichern. Anweisungen zum Ermitteln der Tombstone-Lebensdauer für die Gesamtstruktur finden Sie [Bestimmen der Tombstone-Lebensdauer für die Gesamtstruktur](https://go.microsoft.com/fwlink/?linkid=137177).  
   - Falls eine Arbeitskopie der VHD-Datei, aber keine Systemstatussicherung verfügbar ist, können Sie den vorhandenen virtuellen Computer entfernen. Stellen Sie den vorhandenen virtuellen Computer mithilfe einer vorherigen Kopie der VHD-Datei wieder her. Starten Sie den Computer jedoch unbedingt im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM), und konfigurieren Sie die Registrierung ordnungsgemäß, wie im folgenden Abschnitt beschrieben. Anschließend starten Sie den Domänencontroller im normalen Modus neu.

Bestimmen Sie anhand des Verfahrens in der folgenden Abbildung die optimale Methode zum Wiederherstellen Ihres virtualisierten Domänencontrollers.

![](media/virtualized-domain-controller-architecture/Dd363553.85c97481-7b95-4705-92a7-006e48bc29d0(WS.10).gif)

Für RODCs sind der Wiederherstellungsvorgang und die Entscheidungen einfacher.

![](media/virtualized-domain-controller-architecture/Dd363553.4c5c5eda-df95-4c6b-84e0-d84661434e5d(WS.10).gif)

## <a name="restoring-the-system-state-backup-of-a-virtual-domain-controller"></a>Wiederherstellen der Systemstatussicherung eines virtuellen Domänencontrollers

Falls eine gültige Systemstatussicherung für den virtuellen Computer eines Domänencontrollers vorhanden ist, können Sie die Sicherung problemlos wiederherstellen. Führen Sie dazu das Wiederherstellungsverfahren des Sicherungstools aus, mit dem Sie die VHD-Datei gesichert haben.

> [!IMPORTANT]
> Sie müssen den Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus starten, um ihn ordnungsgemäß wiederherstellen zu können. Der Domänencontroller darf nicht im normalen Modus gestartet werden. Falls Sie beim Starten des Systems die Gelegenheit verpasst haben, in den Verzeichnisdienst-Wiederherstellungsmodus zu wechseln, schalten Sie den virtuellen Computer des Domänencontrollers aus, um ihn dann im normalen Modus zu starten. Sie müssen den Domänencontroller unbedingt im Verzeichnisdienst-Wiederherstellungsmodus starten, da beim Starten eines Domänencontrollers im normalen Modus dessen Aktualisierungssequenznummern erhöht werden, selbst wenn der Domänencontroller vom Netzwerk getrennt wird. Weitere Informationen zu USN-Rollbacks finden Sie unter USN und USN-Rollback. 

## <a name="to-restore-the-system-state-backup-of-a-virtual-domain-controller"></a>So stellen Sie die Systemstatussicherung eines virtuellen Domänencontrollers wieder her

1. Starten Sie den virtuellen Computer des Domänencontrollers, und drücken Sie F5, um den Bildschirm des Windows-Start-Managers zu öffnen. Falls Sie Anmeldeinformationen für die Verbindung eingeben müssen, klicken Sie auf dem virtuellen Computer sofort auf die Taste **Pause**, damit der Startvorgang nicht fortgesetzt wird. Geben Sie anschließend die Anmeldeinformationen für die Verbindung ein, und klicken Sie auf dem virtuellen Computer auf die Schaltfläche **Wiedergabe**. Klicken Sie in das Fenster des virtuellen Computers, und drücken Sie F5.

   Wenn der Bildschirm des Windows-Boot-Managers nicht angezeigt wird und der Domänencontroller im normalen Modus gestartet wird, schalten Sie den virtuellen Computer aus, um zu verhindern, dass der Startvorgang abgeschlossen wird. Wiederholen Sie diesen Schritt so oft wie nötig, bis Sie auf den Bildschirm des Windows-Boot-Managers zugreifen können. Im Menü Windows-Fehlerbehebung ist kein Zugriff auf den Verzeichnisdienst-Wiederherstellungsmodus möglich. Schalten Sie deshalb den virtuellen Computer aus, und wiederholen Sie den Vorgang, wenn das Menü Windows-Fehlerbehebung angezeigt wird.

2. Drücken Sie im Bildschirm des Windows-Boot Managers F8, um auf die erweiterten Startoptionen zuzugreifen.
3. Wählen Sie im Bildschirm **Erweiterte Startoptionen** die Option **Verzeichnisdienstwiederherstellung** aus, und drücken Sie dann die EINGABETASTE. Dadurch wird der Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus gestartet.
4. Verwenden Sie die entsprechende Wiederherstellungsmethode für das Tool, mit dem Sie die Systemstatussicherung erstellt haben. Wenn Sie Windows Server-Sicherung verwendet haben, finden Sie unter [nicht autoritativen Wiederherstellung von AD DS](https://go.microsoft.com/fwlink/?linkid=132637).

## <a name="restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available"></a>Wiederherstellen eines virtuellen Domänencontrollers, wenn keine entsprechende Sicherung der Systemstatusdaten verfügbar ist

Falls keine Sicherung der Systemstatusdaten vorhanden ist, die vor dem Auftreten des Fehlers bei dem virtuellen Computer erstellt wurde, können Sie eine vorherige VHD-Datei zum Wiederherstellen eines auf einem virtuellen Computer ausgeführten Domänencontrollers verwenden. Erstellen Sie, falls möglich, eine Kopie der virtuellen Festplatte. Falls nämlich während der Prozedur ein Problem auftritt oder Sie einen Schritt verpassen, können Sie es mit der kopierten virtuellen Festplatte erneut versuchen.

> [!IMPORTANT]
> - Sie sollten die folgende Prozedur nicht als Ersatz für regelmäßig geplante und terminierte Sicherungen in Betracht ziehen.
> - **Wiederherstellungen, die mit der folgenden Prozedur ausgeführt werden, werden von Microsoft nicht unterstützt und sollte verwendet werden, nur, wenn keine andere Alternative.**
> - Verwenden Sie dieses Verfahren nicht, wenn die Kopie der wiederherzustellenden VHD (Virtual Hard Disk, virtuelle Festplatte) von einem virtuellen Computer im normalen Modus gestartet wurde.

## <a name="to-restore-a-previous-version-of-a-virtual-domain-controller-vhd-without-system-state-data-backup"></a>So stellen Sie eine vorherige Version der VHD eines virtuellen Domänencontrollers ohne Sicherung der Systemstatusdaten wieder her

1. Verwenden Sie die vorherige VHD, und starten Sie den virtuellen Domänencontroller wie im vorherigen Abschnitt beschrieben im Verzeichnisdienst-Wiederherstellungsmodus. Der Domänencontroller darf nicht im normalen Modus gestartet werden. Wenn der Bildschirm des Windows-Boot-Managers nicht angezeigt wird und der Domänencontroller im normalen Modus gestartet wird, schalten Sie den virtuellen Computer aus, um zu verhindern, dass der Startvorgang abgeschlossen wird. Ausführliche Anweisungen zum Aktivieren des Verzeichnisdienst-Wiederherstellungsmodus finden Sie im vorherigen Abschnitt.
2. Öffnen Sie den Registrierungs-Editor. Um Registrierungs-Editor zu öffnen, klicken Sie auf **starten**, klicken Sie auf **ausführen**, Typ **"regedit"** , und klicken Sie dann auf OK. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**. Erweitern Sie im Registrierungs-Editor den folgenden Pfad: **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\NTDS\\Parameters**. Suchen Sie nach dem Wert **DSA Previous Restore Count**. Wenn dieser Wert vorhanden ist, notieren Sie sich die Einstellung. Wenn dieser Wert nicht vorhanden ist, entspricht die Einstellung dem Standardwert, also null. Fügen Sie keinen Wert hinzu, falls kein Wert angezeigt wird.
3. Klicken Sie mit der rechten Maustaste auf den Registrierungsschlüssel **Parameters**, klicken Sie auf **Neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)** .
4. Geben Sie den neuen Namen **Von Sicherung wiederhergestellte Datenbank** ein, und drücken Sie die EINGABETASTE.
5. Doppelklicken Sie auf den soeben erstellten Wert, um das Dialogfeld **DWORD-Wert (32-Bit) bearbeiten** zu öffnen, und geben Sie dann **1** im Feld **Wert** ein. Die **von Sicherung wiederhergestellte Datenbank** Option ist verfügbar auf Domänencontrollern, auf denen Windows 2000 Server mit Service Pack 4 (SP4), Windows Server 2003 mit den Updates, die in enthalten sind [wie erkannt Wiederherstellen von einem USN-Rollback in Windows Server 2003, Windows Server 2008 und Windows Server 2008 R2 und](https://go.microsoft.com/fwlink/?linkid=137182) im Microsoft Knowledge Base, installiert und Windows Server 2008.
6. Starten Sie den Domänencontroller im normalen Modus neu.
7. Wenn der Domänencontroller neu gestartet wird, öffnen Sie die Ereignisanzeige. Klicken Sie zum Öffnen der Ereignisanzeige auf **Start** und auf **Systemsteuerung**, doppelklicken Sie auf **Verwaltung** und dann auf **Ereignisanzeige**.
8. Erweitern Sie **Anwendungs- und Dienstprotokolle**, und klicken Sie dann auf das Protokoll **Verzeichnisdienste**. Stellen Sie sicher, dass im Detailbereich Ereignisse angezeigt werden.
9. Klicken Sie mit der rechten Maustaste auf das Protokoll **Verzeichnisdienste**, und klicken Sie dann auf **Suchen**. Geben Sie im Feld **Suchen nach** die Zeichenfolge **1109** ein, und klicken Sie auf **Weitersuchen**.
10. Es sollte mindestens ein Eintrag mit der Ereignis-ID 1109 angezeigt werden. Fahren Sie mit dem nächsten Schritt fort, falls dieser Eintrag nicht angezeigt wird. Doppelklicken Sie andernfalls auf den Eintrag, und bestätigen Sie, dass das InvocationID-Attribut aktualisiert wurde:

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
12. Überprüfen Sie im Registrierungs-Editor, ob der Wert in **DSA Previous Restore Count** dem vorherigen Wert plus 1 entspricht. Falls dies nicht der richtige Wert ist und Sie in der Ereignisanzeige keinen Eintrag mit der Ereignis-ID 1109 finden, prüfen Sie, ob die Service Packs des Domänencontrollers aktuell sind. Sie können diese Prozedur auf der gleichen VHD nicht erneut durchführen. Sie können sie auf einer Kopie der VHD oder einer anderen VHD erneut ausführen, die nicht im normalen Modus gestartet wurde, indem Sie bei Schritt 1 von vorne anfangen.
13. Schließen Sie den Registrierungs-Editor.

## <a name="usn-and-usn-rollback"></a>USN und USN-Rollback

In diesem Abschnitt werden Replikationsprobleme beschrieben, die auftreten können, wenn die Active Directory-Datenbank mit einer älteren Version eines virtuellen Computers fehlerhaft wiederhergestellt wurde. Weitere Informationen zum Active Directory-Replikationsvorgang finden Sie unter [Active Directory-Replikationskonzepte](../replication/active-directory-replication-concepts.md)

## <a name="usns"></a>USNs

Active Directory-Domänendienste (Active Directory Domain Services, AD DS) verwenden Aktualisierungssequenznummern (Update Sequence Number, USN) zum Nachverfolgen der Replikation von Daten zwischen Domänencontrollern. Bei jeder Änderung von Daten im Verzeichnis wird die USN erhöht, um darauf hinzuweisen, dass eine Änderung vorgenommen wurde.

Für jede auf einem Zieldomänencontroller gespeicherte Verzeichnispartition werden mithilfe von USNs das neueste Quellupdate, das der Datenbank eines Domänencontrollers hinzugefügt wurde, sowie der Status jedes anderen Domänencontrollers, auf dem ein Replikat der Verzeichnispartition gespeichert ist, nachverfolgt. Bei der Replikation von Änderungen zwischen Domänencontrollern werden von den Replikationspartnern diejenigen Änderungen abgerufen, deren USNs größer sind als die USN der letzten vom jeweiligen Partner empfangenen Änderung.

Die USNs sind in zwei Tabellen mit Replikationsmetadaten enthalten. Sie werden von Quell- und Zieldomänencontrollern zum Filtern von Updates verwendet, die der Zieldomänencontroller benötigt.

1. **Aktualitätsvektor**: Eine Tabelle, die der Zieldomänencontroller verwaltet wird, zum Nachverfolgen der Quellupdates, die von allen Quelldomänencontrollern empfangen werden. Wenn ein Zieldomänencontroller Änderungen für eine Verzeichnispartition anfordert, stellt er dem Quelldomänencontroller seinen Aktualitätsvektor bereit. Der Quelldomänencontroller filtert dann mithilfe dieses Werts die dem Zieldomänencontroller zu sendenden Updates. Nach erfolgreichem Abschluss eines Replikationszyklus sendet der Quelldomänencontroller dem Zieldomänencontroller seinen Aktualitätsvektor. So kann der Zieldomänencontroller sicherstellen, dass seine Daten mit den Quellupdates aller übrigen Domänencontroller synchronisiert wurden und auf dem aktuellen Stand sind.  
2. **Obere Grenze**: Ein Wert, den dem Zieldomänencontroller zum Nachverfolgen der letzten Änderungen, die sie von einem bestimmten Quelldomänencontroller für eine bestimmte Partition erhalten hat. Die obere Kontingentgrenze verhindert, dass dem Zieldomänencontroller vom Quelldomänencontroller wiederholt dieselben Änderungen gesendet werden.  

## <a name="directory-database-identity"></a>Verzeichnisdatenbankidentität

Neben USNs verfolgen Domänencontroller die Verzeichnisdatenbank der Quellreplikationspartner. Die Identität der auf dem Server ausgeführten Verzeichnisdatenbank wird separat von der Identität des Serverobjekts selbst verwaltet. Die Verzeichnisdatenbankidentität wird auf den einzelnen Domänencontrollern im **invocationID**-Attribut des NTDS-Einstellungsobjekts gespeichert, das sich im folgenden LDAP-Pfad (Lightweight Directory Access-Protokoll) befindet: cn=NTDS Settings, cn=ServerName, cn=Servers, cn=*SiteName*, cn=Sites, cn=Configuration, dc=*ForestRootDomain*. Die Serverobjektidentität wird im **objectGUID**-Attribut des NTDS-Einstellungsobjekts gespeichert. Die Identität des Softwareobjekts wird nie geändert. Die Identität der Verzeichnisdatenbank hingegen ändert sich, wenn auf dem Server eine Systemstatuswiederherstellung ausgeführt wird oder wenn eine Anwendungsverzeichnispartition auf dem Server hinzugefügt, entfernt und dann erneut hinzugefügt wird. (Ein weiteres Szenario: Wenn von einer Hyper-V-Instanz die eigenen VSS Writer in einer Partition ausgelöst werden, die eine VHD-Datei eines virtuellen Domänencontrollers enthält, löst auch der Gast seine eigenen VSS Writer aus. Da es sich um denselben Mechanismus wie beim oben beschriebenen Sicherungs- und Wiederherstellungsvorgang handelt, wird auch in diesem Fall die invocationID zurückgesetzt.)

Demzufolge werden mit **invocationID** Quellupdates auf einem Domänencontroller einer bestimmten Version der Verzeichnisdatenbank zugeordnet. Anhand der beiden genannten Tabellen, Aktualitätsvektor und obere Kontingentgrenze, können die Domänencontroller - unter Verwendung der **invocationID** und der GUID des Domänencontrollers - feststellen, aus welcher Kopie der Active Directory-Datenbank bestimmte Replikationsinformationen stammen.

**invocationID** ist ein global eindeutiger Bezeichner (Globally Unique Identifier, GUID), der am Anfang der Ausgabe angezeigt wird, nachdem Sie den Befehl **repadmin /showrepl** ausgeführt haben. Es folgt ein Beispiel für die Ausgabe dieses Befehls:

   ```
   Repadmin: running command /showrepl against full DC local host
   Default-First-Site-Name\VDC1
   DSA Options: IS_GC
   DSA object GUID: 966651f3-a544-461f-9f2c-c30c91d17818
   DSA invocationID: b0d9208b-8eb6-4205-863d-d50801b325a9
   ```

Wenn die Active Directory-Domänendienste auf einem Domänencontroller ordnungsgemäß wiederhergestellt werden, wird die **invocationID** zurückgesetzt. Damit geht - entsprechend der Größe der zu replizierenden Partition - ein gesteigerter Replikationsdatenverkehr einher.

Angenommen, VDC1 und DC2 sind zwei Domänencontroller in derselben Domäne. In der folgenden Abbildung ist die Sichtweise von VDC1 durch DC2 dargestellt, wenn der Wert für invocationID bei einer ordnungsgemäßen Wiederherstellung zurückgesetzt wird.

![](media/virtualized-domain-controller-architecture/Dd363553.ca71fc12-b484-47fb-991c-5a0b7f516366(WS.10).gif)

## <a name="usn-rollback"></a>USN-Rollback

Das USN-Rollback erfolgt, wenn die normalen Updates der USNs umgangen werden und ein Domänencontroller eine USN zu verwenden versucht, die niedriger als das letzte Update ist. USN-Rollback erkannt, und die Replikation beendet, bevor abweichungen in der Gesamtstruktur, in den meisten Fällen erstellt wird. 

Ein USN-Rollback kann viele Ursachen haben. Beispielsweise, wenn alte VHD-Dateien verwendet werden oder eine P2V-Konvertierung (Physical-to-Virtual) ausgeführt wird, ohne sicherzustellen, dass der physische Computer nach der Konvertierung dauerhaft offline bleibt. Ergreifen Sie die folgenden Vorsichtsmaßnahmen, um sicherzustellen, dass kein USN-Rollback ausgeführt wird:

   - Wenn nicht WindowsServer 2012 oder höher ausgeführt, nicht erstellen Sie oder verwenden Sie eine Momentaufnahme eines virtuellen Domänencontrollercomputers.
   - Kopieren Sie die VHD-Datei des Domänencontrollers nicht.  
   - Wenn nicht WindowsServer 2012 oder höher ausgeführt, nicht exportieren Sie den virtuellen Computer, auf dem Domänencontroller ausgeführt wird.  
   - Stellen Sie einen Domänencontroller einer Active Directory-Datenbank nur mit einer unterstützten Sicherung her bzw. führen Sie ein Rollback für die Inhalte einer Active Directory-Datenbank nur mit einer unterstützten Sicherungslösung wie z. B. der Windows Server-Sicherung aus.  

In manchen Fällen bleibt ein USN-Rollback unerkannt. In anderen Fällen können andere Replikationsfehler verursacht werden. In diesen Fällen muss der Umfang des Problems analysiert und das Problem zeitnah behoben werden. Weitere Informationen zum Entfernen veralteter Objekte, die als Folge USN-Rollbacks eines, finden Sie unter [veralteter Active Directory-Objekte generiert die Ereignis-ID 1988 in Windows Server 2003](https://go.microsoft.com/fwlink/?linkid=137185) in der Microsoft Knowledge Base.

## <a name="usn-rollback-detection"></a>USN-Rollbackerkennung

In den meisten Fällen werden USN-Rollbacks ohne entsprechende Zurücksetzung des Werts **invocationID**, die durch unzulässige Wiederherstellungsverfahren verursacht werden, erkannt. Windows Server 2008 bietet Schutzmaßnahmen vor einer unzulässigen Replikation nach einem unzulässigen Wiederherstellungsvorgang für den Domänencontroller. Diese Schutzmaßnahmen werden dadurch ausgelöst, dass ein unzulässiger Wiederherstellungsvorgang niedrigere USNs für Änderungen ergibt, die die Replikationspartner bereits empfangen haben.

Wenn in Windows Server 2008 und Windows Server 2003 SP1 ein Zieldomänencontroller Änderungen mithilfe einer bereits zuvor verwendeten USN anfordert, wird die Antwort des Quellreplikationspartners vom Zieldomänencontroller so gedeutet, dass die Replikationsmetadaten veraltet sind. Dies bedeutet, dass für die Active Directory-Datenbank auf dem Quelldomänencontroller ein Rollback auf einen vorherigen Status ausgeführt wurde. Beispielsweise wurde für die VHD-Datei eines virtuellen Computers ein Rollback auf eine vorherige Version ausgeführt. In diesem Fall startet der Zieldomänencontroller die folgenden Quarantänemaßnahmen auf dem Domänencontroller, bei dem eine unzulässige Wiederherstellung festgestellt wurde:

   - Der Netzwerkanmeldedienst wird von AD DS angehalten, wodurch Benutzer- und Computerkonten am Ändern von Kontokennwörtern gehindert werden. Diese Maßnahme verhindert den Verlust solcher Änderungen, falls sie nach einer unzulässigen Wiederherstellung auftreten.  
   - Die ein- und ausgehende Active Directory-Replikation wird von AD DS deaktiviert.  
   - Die Ereignis-ID 2095 wird von AD DS im Verzeichnisdienst-Ereignisprotokoll generiert, um auf diesen Zustand hinzuweisen.  

Die folgende Abbildung veranschaulicht die Abfolge von Ereignissen, wenn ein USN-Rollback auf VDC2, dem auf einem virtuellen Computer ausgeführten Zieldomänencontroller, erkannt wird. In dieser Abbildung wird das USN-Rollback auf VDC2 erkannt, wenn ein Replikationspartner feststellt, dass VDC2 einen Aktualitäts-USN-Wert gesendet hat, der zuvor vom Zieldomänencontroller gesehen wurde. Dies ist ein Hinweis darauf, dass für die Datenbank von VDC2 ein unzulässiges Rollback ausgeführt wurde.

![](media/virtualized-domain-controller-architecture/Dd363553.373b0504-43fc-40d0-9908-13fdeb7b3f14(WS.10).gif)

Führen Sie sofort das folgende Verfahren aus, wenn im Verzeichnisdienst-Ereignisprotokoll die Ereignis-ID 2095 gemeldet wird.

## <a name="to-resolve-event-id2095"></a>So beheben Sie die Ereignis-ID 2095

1. Trennen Sie die Netzwerkverbindung des virtuellen Computers, von dem der Fehler aufgezeichnet wurde.
2. Versuchen Sie festzustellen, ob Änderungen von diesem Domänencontroller stammen und an andere Domänencontroller weitergegeben wurden. Falls das Ereignis auf einen Snapshot oder eine Kopie eines gestarteten virtuellen Computers zurückzuführen ist, versuchen Sie den Zeitpunkt des USN-Rollbacks festzustellen. Anschließend können Sie die Replikationspartner dieses Domänencontrollers überprüfen, um festzustellen, ob seit diesem Zeitpunkt eine Replikation stattgefunden hat.

   Hierfür können Sie das Tool Repadmin verwenden. Weitere Informationen zur Verwendung von Repadmin finden Sie unter [Überwachung und Problembehandlung der Active Directory-Replikation mithilfe von Repadmin](https://go.microsoft.com/fwlink/?linkid=122830). Wenn Sie nicht selbst ermitteln können, wenden Sie sich an [Microsoft-Support](https://support.microsoft.com) um Unterstützung zu erhalten.

3. Erzwingen Sie eine Herabstufung des Domänencontrollers. Dies beinhaltet das Bereinigen der Metadaten des Domänencontrollers und das Übernehmen der Betriebsmasterrollen (auch als Flexible Single Master Operations- oder FSMO-Rollen bezeichnet). Weitere Informationen finden Sie im Abschnitt "Wiederherstellung nach einem USN-Rollback" [das Erkennen und Wiederherstellen nach einem USN-Rollback in Windows Server 2003, Windows Server 2008 und Windows Server 2008 R2](https://go.microsoft.com/fwlink/?linkid=137182) in der Microsoft Knowledge Base.
4. Löschen Sie alle vorherigen VHD-Dateien für den Domänencontroller.

## <a name="undetected-usn-rollback"></a>Unerkanntes USN-Rollback

Ein USN-Rollback wird in den folgenden beiden Fällen möglicherweise nicht erkannt:

1. Die VHD-Datei ist an unterschiedliche virtuelle Computer angefügt, die an verschiedenen Standorten gleichzeitig ausgeführt werden.  
2. Die USN auf dem wiederhergestellten Domänencontroller ist höher als die letzte USN, die vom anderen Domänencontroller empfangen wurde.  

Im ersten Fall werden möglicherweise andere Domänencontroller mit einem der virtuellen Computer repliziert, und Änderungen können auf einem der virtuellen Computer auftreten, ohne dass sie an den anderen virtuellen Computer repliziert werden. Die Abweichungen bei der Gesamtstruktur sind schwierig zu erkennen. Das Resultat sind unvorhersehbare Active Directory-Antworten. Diese Situation kann nach einer P2V-Migration auftreten, wenn sowohl der physische Computer als auch der virtuelle Computer im selben Netzwerk ausgeführt werden. Möglich ist diese Situation auch, wenn mehrere virtuelle Domänencontroller vom selben physischen Domänencontroller erstellt und dann im selben Netzwerk ausgeführt werden.

Im zweiten Fall gilt ein USN-Bereich für zwei unterschiedliche Änderungen. Dieses Problem kann sich über längere Zeit fortsetzen, ohne erkannt zu werden. Wenn ein während dieses Zeitraums erstelltes Objekt geändert wird, wird ein veraltetes Objekt erkannt und als Ereignis-ID 1988 in der Ereignisanzeige gemeldet. Die folgende Abbildung veranschaulicht, wie ein USN-Rollback in einer solchen Situation möglicherweise nicht erkannt wird.

![](media/virtualized-domain-controller-architecture/Dd363553.63565fe0-d970-4b4e-b5f3-9c76bc77e2d4(WS.10).gif)

## <a name="read-only-domain-controllers"></a>Schreibgeschützte Domänencontroller

RODCs sind Domänencontroller, auf denen schreibgeschützte Kopien der Partitionen einer Active Directory-Datenbank gehostet werden. RODCs vermeiden die meisten USN-Rollbackprobleme, da sie keine Änderungen an die anderen Domänencontroller replizieren. Wenn jedoch ein RODC von einem beschreibbaren Domänencontroller repliziert, der von einem USN-Rollback betroffen ist, dann ist auch der RODC betroffen.

Von der Wiederherstellung eines RODC mithilfe eines Snapshots wird abgeraten. Stellen Sie einen RODC mithilfe einer Active Directory-kompatiblen Sicherungsanwendung wieder her. Außerdem muss wie bei beschreibbaren Domänencontrollern darauf geachtet werden, dass ein RODC nicht länger als die Tombstone-Lebensdauer offline ist. Dieser Zustand kann auf dem RODC zu veralteten Objekten führen.

Weitere Informationen zu RODCs finden Sie unter den [Read-Only Domain Controller Planungs- und Bereitstellungshandbuch](../../deploy/rodc/read-only-domain-controller-updates.md).
