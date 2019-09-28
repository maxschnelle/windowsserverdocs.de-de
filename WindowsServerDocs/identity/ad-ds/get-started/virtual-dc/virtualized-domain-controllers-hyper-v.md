---
title: Virtualisieren von Domänen Controllern mithilfe von Hyper-V
description: Überlegungen zur Virtualisierung von Windows Server Active Directory-Domäne-Controllern in Hyper-V
author: MicrosoftGuyJFlo
ms.author: joflore
ms.date: 04/19/2018
ms.topic: article
ms.prod: windows-server
ms.openlocfilehash: 19e8eef008d3818c413808ab1f085a7cc247ec36
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369497"
---
# <a name="virtualizing-domain-controllers-using-hyper-v"></a>Virtualisieren von Domänen Controllern mithilfe von Hyper-V

> Gilt für: Windows Server 2016

Dieses Thema wird aktualisiert, um die Richtlinien für Windows Server 2016 zu übernehmen. Windows Server 2012 führt viele Verbesserungen für virtualisierte Domänen Controller (DCS) ein, einschließlich Sicherheitsvorkehrungen, um das USN-Rollback auf virtuellen DCS und die Möglichkeit zum Klonen virtueller DCS zu verhindern. Weitere Informationen zu diesen Verbesserungen finden [Sie unter Introduction to Active Directory Domain Services (AD DS) Virtualization (Level 100)](../../introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100.md).

Hyper-V konsolidiert verschiedene Server Rollen auf einem einzelnen physischen Computer. In diesem Leitfaden wird beschrieben, wie Domänencontroller als 32-Bit- oder 64-Bit-Gastbetriebssysteme ausgeführt werden.

## <a name="planning-to-virtualize-domain-controllers"></a>Überlegungen zur Planung für virtualisierte Domänencontroller

Themen dieses Abschnitts sind die Hardwareanforderungen für Hyper-V-Server, die Vermeidung einzelner Fehlerquellen (Single Points of Failure, SPOFs), die Auswahl des geeigneten Konfigurationstyps für die Server und virtuellen Computer der Hyper-V-Umgebung sowie Überlegungen zur Sicherheit und Leistung.

## <a name="hyper-v-requirements"></a>Anforderungen für Hyper-V

Zum Installieren und Verwenden der Hyper-V-Rolle benötigen Sie Folgendes:

   - **Ein x64-Prozessor**
      - Hyper-V ist in x64-basierten Versionen von Windows Server 2008 oder höher verfügbar.  
   - **Hardware gestützte Virtualisierung**
      - Dieses Feature ist verfügbar für Prozessoren mit Virtualisierungsoption, d. h., Intel Virtualization Technology (Intel VT) oder AMD Virtualization (AMD-V).  
   - **Hardware-Datenausführungsschutz (DEP)**
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
   - Sie können BitLocker mit ihren Domänen Controllern verwenden, da Sie Windows Server 2016 verwenden können, um dem Gast Schlüsselmaterial auch das Entsperren des System Volumes zu ermöglichen.
   - [Geschützte Fabric-und abgeschirmte VMS](/it-server/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) können zusätzliche Kontrollen zum Schutz ihrer Domänen Controller bereitstellen.

Weitere Informationen zu RODCs finden [Sie im Planungs-und Bereitstellungs Handbuch für schreibgeschützte Domänen Controller](../../deploy/rodc/read-only-domain-controller-updates.md).

Weitere Informationen zum Sichern von Domänen Controllern finden Sie unter [Leitfaden für bewährte Methoden zum Sichern von Active Directory Installationen](../../plan/security-best-practices/best-practices-for-securing-active-directory.md).

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

Eine VHD-Datei eines virtuellen Domänencontrollers entspricht der physischen Festplatte eines physischen Domänencontrollers. Als solche sollte sie genauso sorgfältig wie die Festplatte eines physischen Domänencontrollers geschützt werden. Stellen Sie sicher, dass nur zuverlässige und vertrauenswürdige Administratoren auf die VHD-Dateien des Domänen Controllers zugreifen können.

## <a name="rodcs"></a>RODCs

RODCs haben den Vorteil, dass sie an Standorten verwendet werden können, wo die physische Sicherheit nicht garantiert werden kann, wie z. B. in Zweigstellen. Sie können Windows BitLocker-Laufwerkverschlüsselung verwenden, um VHD-Dateien selbst (nicht die Dateisysteme darin) vor der Beeinträchtigung der physischen Festplatte auf dem Host zu schützen. 

## <a name="performance"></a>Leistung

Die neue Microkernel-64-Bit-Architektur ermöglicht im Vergleich zu früheren Virtualisierungsplattformen eine erhebliche Leistungsverbesserung. Zur Optimierung der Hostleistung sollte für den Host eine Server Core-Installation von Windows Server 2008 oder höher vorgesehen werden, und außer Hyper-V sollten keine anderen Serverrollen installiert werden.

Die Leistung von virtuellen Computern hängt insbesondere von der Arbeitsauslastung ab. Testen Sie verschiedene Topologien, um eine zufriedenstellende Leistung von Active Directory zu garantieren. Bewerten Sie die aktuelle Arbeitsauslastung über einen bestimmten Zeitraum mit einem Tool wie der Zuverlässigkeits-und Leistungsüberwachung (Perfmon. msc) oder dem [Microsoft Assessment and Planning (Map) Toolkit](https://go.microsoft.com/fwlink/?linkid=137077). Das MAP-Tool ist außerdem hilfreich, wenn Sie eine Bestandsaufnahme aller Server und Serverrollen machen möchten, die derzeit in Ihrem Netzwerk vorhanden sind.

Um eine allgemeine Vorstellung von der Leistung virtualisierter Domänen Controller zu erhalten, wurden die folgenden Leistungstests mit dem Tool für die [Active Directory Leistungstests (ADTest. exe)](https://go.microsoft.com/fwlink/?linkid=137088)ausgeführt.

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
<td><p>-10,71%</p></td>
</tr>
<tr class="even">
<td><p>Suchanfragen/Sek</p></td>
<td><p>Suche nach einem Attributsatz im Basisbereich (L2)</p></td>
<td><p>10123</p></td>
<td><p>9005</p></td>
<td><p>-11,04%</p></td>
</tr>
<tr class="odd">
<td><p>Suchanfragen/Sek</p></td>
<td><p>Suche nach allen Attributen im Basisbereich (L3)</p></td>
<td><p>1284</p></td>
<td><p>1242</p></td>
<td><p>-3,27%</p></td>
</tr>
<tr class="even">
<td><p>Suchanfragen/Sek</p></td>
<td><p>Suche nach allgemeinem Namen im Unterstrukturbereich (L6)</p></td>
<td><p>8613</p></td>
<td><p>7904</p></td>
<td><p>-8,23%</p></td>
</tr>
<tr class="odd">
<td><p>Erfolgreiche Bindungen/s</p></td>
<td><p>Ausführen schneller Bindungen (B1)</p></td>
<td><p>1438</p></td>
<td><p>1374</p></td>
<td><p>-4,45%</p></td>
</tr>
<tr class="even">
<td><p>Erfolgreiche Bindungen/s</p></td>
<td><p>Ausführen einfacher Bindungen (B2)</p></td>
<td><p>611</p></td>
<td><p>550</p></td>
<td><p>-9,98%</p></td>
</tr>
<tr class="odd">
<td><p>Erfolgreiche Bindungen/s</p></td>
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

Um eine zufriedenstellende Leistung sicherzustellen, wurden Integrationskomponenten installiert, damit das Gastbetriebssystem "Optimierungen" oder hypervisorkompatible synthetische Treiber verwenden kann. Während des Installationsvorgangs müssen möglicherweise emulierte IDE- oder Netwerkadapter-Treiber verwendet werden. In Produktionsumgebungen sollten Sie diese emulierten Treiber durch synthetische Treiber ersetzen, um die Leistung zu optimieren.

Wenn Sie die Leistung von virtuellen Computern mit der Zuverlässigkeits- und Leistungsüberwachung (Perfmon.msc) überwachen, stimmen die CPU-Informationen innerhalb des virtuellen Computers aufgrund der Art und Weise, wie die virtuelle CPU auf dem physischen Prozessor eingeplant wird, nicht genau. Wenn Sie CPU-Information für einen virtuellen Computer abrufen möchten, der auf einem Hyper-V-Server ausgeführt wird, verwenden Sie den Leistungsindikator Logischer Prozessor für Hyper-V-Hypervisor in der Hostpartition.

Weitere Informationen zur Leistungsoptimierung von AD DS und Hyper-V finden Sie unter [Richtlinien für die Leistungsoptimierung für Windows Server 2016](../../../../administration/performance-tuning/index.md).

Darüber hinaus sollten Sie keine differenzierende virtuelle Festplatte auf einem virtuellen Computer verwenden, der als Domänencontroller konfiguriert ist, da durch die differenzierende virtuelle Festplatte die Leistung beeinträchtigt werden kann. Weitere Informationen zu Hyper-V-Datenträger Typen, einschließlich differenzierender Datenträger, finden Sie unter [Assistent für neue virtuelle Festplatten](http://go.microsoft.com/fwlink/?linkid=137279).

Weitere Informationen zu AD DS in virtuellen Hostingumgebungen finden Sie unter Dinge, die [beim Hosten von Active Directory Domänen Controllern in virtuellen Host Umgebungen](https://go.microsoft.com/fwlink/?linkid=141292) in der Microsoft Knowledge Base zu beachten sind.

## <a name="deployment-considerations-for-virtualized-domain-controllers"></a>Überlegungen zur Bereitstellung für virtualisierte Domänencontroller

Mehrere gängige Praktiken im Zusammenhang mit virtuellen Computern sollten bei der Bereitstellung virtualisierter Domänencontroller vermieden werden. Zudem gelten spezielle Empfehlungen für die Zeitsynchronisierung und Speicherung.

## <a name="virtualization-deployment-practices-to-avoid"></a>Bei der Virtualisierungsbereitstellung zu vermeidende Praktiken

Virtualisierungsplattformen wie z. B. Hyper-V bieten eine Reihe von Features, die das Verwalten, Warten, Sichern und Migrieren von Computern vereinfachen. Bei der Bereitstellung virtualisierter Domänencontroller empfiehlt es sich jedoch, die folgenden gängigen Praktiken (und zugehörigen Features) zu vermeiden:

- Stellen Sie die Datenbankdateien eines virtuellen Domänen Controllers (Active Directory Datenbank (NTDS) nicht bereit, um die Dauerhaftigkeit von Active Directory Schreibvorgängen zu gewährleisten. DIT), Protokolle und SYSVOL) auf virtuellen IDE-Datenträgern. Erstellen Sie stattdessen eine zweite VHD, die an einen virtuellen SCSI-Controller angeschlossen ist, und stellen Sie sicher, dass die Datenbank, Protokolle und SYSVOL während der Installation des Domänen Controllers auf dem SCSI-Datenträger des virtuellen Computers platziert werden.  
- Implementieren Sie keine differenzierenden virtuellen Festplatten (Virtual Hard Disk, VHD) auf einem virtuellen Computer, den Sie als Domänencontroller konfigurieren. Dadurch kann eine frühere Version zu einfach wiederhergestellt werden, und außerdem wird die Leistung reduziert. Weitere Informationen zu VHD-Typen finden Sie unter [Assistent für neue virtuelle Festplatten](https://go.microsoft.com/fwlink/?linkid=137279).  
- Stellen Sie keine neuen Active Directory Domänen und Gesamtstrukturen in einer Kopie eines Windows Server-Betriebssystems bereit, das nicht zum ersten Mal mithilfe des System Vorbereitungs Tools (syspree) vorbereitet wurde. Weitere Informationen zur Ausführung von sy-p finden Sie unter [System Vorbereitung (System Vorbereitung)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview) .

   > [!WARNING]
   > Die Ausführung von Sysprep auf einem Domänencontroller wird nicht unterstützt.

- Um eine potenzielle Rollbacksituation der Aktualisierungssequenznummern (Update Sequence Number, USN) zu vermeiden, sollten Sie keine Kopien einer VHD-Datei, die einen bereits bereitgestellten Domänencontroller repräsentiert, zum Bereitstellen zusätzlicher Domänencontroller verwenden. Weitere Informationen über das Rollback für die Wiederverwendung finden Sie unter " [US-v" und "Rollback](#usn-and-usn-rollback)".
   - Mit Windows Server 2012 und höher können Administratoren Domänen Controller Images Klonen, wenn Sie bei der Bereitstellung zusätzlicher Domänen Controller ordnungsgemäß vorbereitet werden.
- Verwenden Sie das Exportfeature von Hyper-V nicht zum Exportieren eines virtuellen Computers, auf dem ein Domänencontroller ausgeführt wird.
  - Bei Windows Server 2012 und höher wird ein Export und Import eines virtuellen Domänen Controller-Gast Betriebssystems wie eine nicht autoritative Wiederherstellung behandelt, da er eine Änderung der Generations-ID erkennt und nicht für das Klonen konfiguriert ist.
  - Stellen Sie sicher, dass Sie den Gast, den Sie exportiert haben, nicht mehr verwenden.
    - Sie können die Hyper-V-Replikation verwenden, um eine zweite Inaktive Kopie eines Domänen Controllers beizubehalten. Wenn Sie das replizierte Image starten, müssen Sie auch eine ordnungsgemäße Bereinigung durchführen, und zwar aus demselben Grund, aus dem die Quelle nach dem Exportieren eines DC-gastimages nicht verwendet werden kann.

## <a name="physical-to-virtual-migration"></a>Physical-to-Virtual-Migration (P2V)

System Center Virtual Machine Manager (VMM) 2008 ermöglicht die einheitliche Verwaltung physischer und virtueller Computer. Außerdem kann ein physischer Computer zu einem virtuellen Computer migriert werden. Diese Vorgang wird als P2V-Konvertierung (Physical-to-Virtual) bezeichnet. Während des P2V-Konvertierungs Vorgangs dürfen der neue virtuelle Computer und der physische Domänen Controller, der migriert wird, nicht gleichzeitig ausgeführt werden, um eine für das Rollback [in der](#usn-and-usn-rollback)upgradesituation beschriebene Betriebs Steuerungs Situation zu vermeiden.

Sie sollten die P2V-Konvertierung im Offlinemodus ausführen, damit die Verzeichnisdaten einheitlich sind, wenn der Domänencontroller wieder eingeschaltet wird. Die Offlinemodusoption wird im Assistenten zum Konvertieren des physischen Servers angeboten und empfohlen. Eine Beschreibung des Unterschieds zwischen Online Modus und Offline Modus finden [Sie unter P2V: Konvertieren physischer Computer in virtuelle Maschinen in VMM](https://go.microsoft.com/fwlink/?linkid=155072). Während der P2V-Konvertierung sollte der virtuelle Computer nicht mit dem Netzwerk verbunden sein. Aktivieren Sie den Netzwerkadapter des virtuellen Computers erst nach Abschluss und Überprüfung der P2V-Konvertierung. Zu diesem Zeitpunkt ist der physische Quellcomputer ausgeschaltet. Binden Sie den physischen Quellcomputer erst wieder in das Netzwerk ein, nachdem Sie die Festplatte neu formatiert haben.

> [!NOTE]
> Es gibt sicherere Optionen zum Erstellen neuer virtueller DCS, die keine Risiken bei der Erstellung eines Rollbacks für eine höhere Laufzeit haben. Sie können einen neuen virtuellen Domänen Controller durch reguläre herauf Stufung, herauf Stufung von der Installation von einem Medium (IFM) und auch durch Klonen des Domänen Controllers einrichten, wenn Sie bereits über mindestens einen virtuellen Domänen Controller verfügen.
Dies hilft auch dabei, Probleme mit Hardware-oder Platt Form bezogenen Problemen zu vermeiden P2V bei konvertierten virtuellen Gästen treten möglicherweise Probleme auf.

> [!WARNING]
> Um Probleme mit Active Directory Replikation zu vermeiden, stellen Sie sicher, dass zu einem bestimmten Zeitpunkt nur eine Instanz (physisch oder virtuell) eines bestimmten Domänen Controllers in einem bestimmten Netzwerk vorhanden ist.
> Sie können die Wahrscheinlichkeit verringern, dass der alte Klon ein Problem darstellt:
> 
> - Wenn der neue virtuelle Domänen Controller ausgeführt wird, ändern Sie das Computer Konto Kennwort zweimal mit: netdom resetpwd/Server: < Domänen Controller >...
> - Exportieren und importieren Sie den neuen virtuellen Gast, um zu erzwingen, dass er zu einer neuen Generations-ID und somit zu einer Datenbank-Aufruf-ID wird.
> 

## <a name="using-p2v-migration-to-create-test-environments"></a>Erstellen von Testumgebungen mithilfe der P2V-Migration

Mithilfe der P2V-Migration über VMM können Sie Testumgebungen erstellen. Produktionsdomänencontroller können von physischen Computern zu virtuellen Computern migriert werden, um eine Testumgebung zu erstellen, ohne die Produktionsdomänencontroller permanent herunterzufahren. Die Testumgebung muss sich jedoch in einem anderen Netzwerk als die Produktionsumgebung befinden, falls zwei Instanzen desselben Domänencontrollers vorhanden sein sollen. Gehen Sie beim Erstellen von Testumgebungen mit der P2V-Migration äußerst vorsichtig vor, um USN-Rollbacks zu vermeiden, die sich negativ auf Ihre Test- und Produktionsumgebungen auswirken können. Mithilfe der folgenden Methode können Sie Testumgebungen mit P2V erstellen.

Ein Domänen Controller in der Produktion aus jeder Domäne wird gemäß den Richtlinien, die im Abschnitt Physical-to-Virtual Migration (Physical-to-Virtual Migration) angegeben sind, zu einem virtuellen Testcomputer migriert. Die physischen Produktionscomputer und die virtuellen Testcomputer müssen sich in unterschiedlichen Netzwerken befinden, wenn sie wieder online geschaltet werden. Um USN-Rollbacks in der Testumgebung zu vermeiden, müssen alle Domänencontroller, die von physischen Computern zu virtuellen Computern migriert werden sollen, offline geschaltet werden. (Beenden Sie dazu den NTDS-Dienst, oder starten Sie den Computer im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM) neu.) Wenn die Domänencontroller offline sind, sollten in der Umgebung keine neuen Updates vorgenommen werden. Die Computer müssen während der P2V-Migration offline bleiben. Keiner der Computer sollte wieder online geschaltet werden, bevor alle Computer vollständig migriert wurden. Weitere Informationen über das Rollback für die Wiederverwendung finden Sie unter "US-v" und "Rollback".

Nachfolgende Testdomänencontroller sollten in der Testumgebung als Replikate heraufgestuft werden.

## <a name="time-service"></a>Zeitdienst

Bei virtuellen Maschinen, die als Domänen Controller konfiguriert sind, wird empfohlen, die Zeitsynchronisierung zwischen dem Host System und dem Gast Betriebssystem zu deaktivieren, die als Domänen Controller fungieren. Dadurch kann der Gast Domänen Controller die Zeit von der Domänen Hierarchie aus synchronisieren.

Um den Hyper-V-Zeit Synchronisierungs Anbieter zu deaktivieren, fahren Sie den virtuellen Computer herunter, und deaktivieren Sie das Kontrollkästchen Zeitsynchronisierung unter Integration Services.

> [!NOTE]
> Diese Anleitung wurde vor kurzem aktualisiert, um die aktuelle Empfehlung zum Synchronisieren der Zeit für den Gast Domänen Controller nur aus der Domänen Hierarchie und nicht die vorherige Empfehlung zum partiellen Deaktivieren der Zeitsynchronisierung zwischen dem Host zu berücksichtigen. System-und Gast Domänen Controller.

## <a name="storage"></a>Speicher

Verwenden Sie die folgenden Empfehlungen zum Speichern von Betriebssystem-, Active Directory-und VHD-Dateien, um die Leistung des virtuellen Computers mit dem Domänen Controller zu optimieren und die Dauerhaftigkeit Active Directory Schreibvorgängen sicherzustellen:

- **Gastspeicherung**: Speichern Sie die Active Directory-Datenbankdatei (NTDS. dit), Protokolldateien und SYSVOL-Dateien auf einem separaten virtuellen Datenträger aus den Betriebssystemdateien. Erstellen Sie eine zweite VHD, die an einen virtuellen SCSI-Controller angefügt ist, und speichern Sie die Datenbank, Protokolle und SYSVOL auf dem virtuellen SCSI-Datenträger der virtuellen Maschine. Virtuelle SCSI-Datenträger bieten eine bessere Leistung im Vergleich zur virtuellen IDE und unterstützen den erzwungenen Einheiten Zugriff Fua stellt sicher, dass das Betriebssystem Daten direkt aus dem Medium schreibt und liest, wobei alle zwischen Speicherungs Mechanismen umgangen werden.

  > [!NOTE]
  > Wenn Sie BitLocker für den Gast des virtuellen Domänen Controllers verwenden möchten, müssen Sie sicherstellen, dass die zusätzlichen Volumes für die automatische Entsperrung konfiguriert sind.
  > Weitere Informationen zum Konfigurieren der automatischen Entsperrung finden Sie unter [enable-bitlockerautounlock](https://docs.microsoft.com/powershell/module/bitlocker/enable-bitlockerautounlock) .

- **Hostspeicherung von VHD-Dateien**. Empfehlungen: Die Empfehlungen für die Hostspeicherung beziehen sich auf die Speicherung von VHD-Dateien. Für eine optimale Leistung sollten Sie VHD-Dateien nicht auf einem Datenträger speichern, der häufig von anderen Diensten oder Anwendungen verwendet wird, wie z. B. auf dem Systemdatenträger, auf dem das Windows-Hostbetriebssystem installiert ist. Speichern Sie jede VHD-Datei auf einer vom Hostbetriebssystem und anderen VHD-Dateien getrennten Partition. Die ideale Konfiguration ist die Speicherung jeder VHD-Datei auf einem separaten physischen Laufwerk.  

  Das System des physischen Host Datenträgers muss auch **mindestens eines** der folgenden Kriterien erfüllen, um die Anforderungen an die Integrität der virtualisierten Arbeits Auslastungs Daten zu erfüllen:  

   - Das System verwendet Server-Klassen Datenträger (SCSI, Fibre Channel).  
   - Das System stellt sicher, dass die Datenträger mit einem Akku gestützten Caching-Hostbus Adapter (HBA) verbunden sind.  
   - Das System verwendet einen Speichercontroller (z. b. ein RAID-System) als Speichergerät.  
   - Das System stellt sicher, dass die Stromversorgung des Datenträgers durch eine unterbrechungsfreie Stromversorgung (USV) geschützt ist.  
   - Das System stellt sicher, dass das Write-Caching-Feature des Datenträgers deaktiviert ist.  

- **Feste virtuelle Festplatten und Pass-Through-Datenträger**. Es gibt viele Methoden zum Konfigurieren der Speicherung für virtuelle Computer. Wenn VHD-Dateien verwendet werden, sind virtuelle Festplatten mit fester Größe effizienter als dynamische virtuelle Festplatten, da der Arbeitsspeicher für virtuelle Festplatten mit fester Größe beim Erstellen zugeordnet wird. Pass-Through-Datenträger, die von virtuellen Computern für den Zugriff physische Speichermedien verwenden können, weisen sogar eine noch optimalere Leistung auf. Pass-Through-Datenträger sind im Prinzip physische Datenträger oder logische Gerätenummern (Logical Unit Numbers, LUNs), die an einen virtuellen Computer angeschlossen sind. Das Snapshotfeature wird von Pass-Through-Datenträgern nicht unterstützt. Deshalb sind Pass-Through-Datenträger die bevorzugte Festplattenkonfiguration, da von der Verwendung von Snapshots zusammen mit Domänencontrollern abgeraten wird.  

Verwenden Sie virtuelle SCSI-Controller, um die Gefahr der Beschädigung von Active Directory Daten zu verringern:

   - Verwenden Sie physische SCSI-Laufwerke (anstelle von IDE/ATA-Laufwerken) auf Hyper-V-Servern, von denen virtuelle Domänencontroller gehostet werden. Falls Sie keine SCSI-Laufwerke verwenden können, stellen Sie sicher, dass der Schreibcache auf den ATA/IDE-Laufwerken, von denen virtuelle Domänencontroller gehostet werden, deaktiviert ist. Weitere Informationen finden Sie unter [Ereignis-ID 1539 – Datenbankintegrität](https://go.microsoft.com/fwlink/?linkid=162419).
   - Um die Dauerhaftigkeit von Active Directory Schreibvorgängen zu gewährleisten, müssen die Active Directory Datenbank, Protokolle und SYSVOL auf einem virtuellen SCSI-Datenträger abgelegt werden. Virtuelle SCSI-Datenträger unterstützen den erzwungenen Unit Access (Fua). Fua stellt sicher, dass das Betriebssystem Daten direkt aus dem Medium schreibt und liest, wobei alle zwischen Speicherungs Mechanismen umgangen werden.  

## <a name="operational-considerations-for-virtualized-domain-controllers"></a>Überlegungen zur Verwendung für virtualisierte Domänencontroller

Für Domänencontroller, die auf virtuellen Computern ausgeführt werden, gelten im Gegensatz zu Domänencontrollern, die auf physischen Computern ausgeführt werden, Einschränkungen hinsichtlich der Verwendung. Bei Einsatz eines virtualisierten Domänencontrollers sollten bestimmte Praktiken und Features der Virtualisierungssoftware nicht verwendet werden:

   - Sie dürfen den gespeicherten Zustand eines Domänencontrollers in einem virtuellen Computer nicht für einen Zeitraum anhalten, beenden oder speichern, der die Tombstone-Lebensdauer der Gesamtstruktur überschreitet, und dann den Vorgang von dem angehaltenen oder gespeicherten Zustand fortsetzen. Dadurch können Probleme bei der Replikation verursacht werden. Informationen zum Bestimmen der Tombstone-Lebensdauer für die Gesamtstruktur finden Sie unter [bestimmen der Tombstone-Lebensdauer für die](https://go.microsoft.com/fwlink/?linkid=137177)Gesamtstruktur.  
   - Kopieren oder klonen Sie keine virtuellen Festplatten (Virtual Hard Disks, VHDs). Auch wenn die Sicherheitsvorkehrungen für die Gast-VM gelten, können einzelne VHDs weiterhin kopiert werden und bewirken ein Rollback für die USN.
   - Erstellen oder verwenden Sie keinen Snapshot eines virtuellen Domänencontrollers. Es wird von Windows Server 2012 und höher technisch unterstützt. es ist kein Ersatz für eine gute Sicherungsstrategie. Es gibt einige Gründe für das nehmen von DC-Momentaufnahmen oder das Wiederherstellen der Momentaufnahmen
   - Verwenden Sie keine differenzierende virtuelle Festplatte auf einem virtuellen Computer, der als Domänencontroller konfiguriert ist. Dadurch kann eine frühere Version zu einfach wiederhergestellt werden, und außerdem wird die Leistung reduziert.  
   - Verwenden Sie das Exportfeature nicht auf einem virtuellen Computer, auf dem ein Domänencontroller ausgeführt wird.  
   - Stellen Sie einen Domänencontroller einer Active Directory-Datenbank nur mit einer unterstützten Sicherung her bzw. führen Sie ein Rollback für die Inhalte einer Active Directory-Datenbank nur mit einer unterstützten Sicherung aus. Weitere Informationen finden Sie unter [Überlegungen zur Sicherung und Wiederherstellung für virtualisierte Domänen Controller](#backup-and-restore-practices-to-avoid).  

Durch diese Empfehlungen soll ein Rollback der Aktualisierungssequenznummern (Update Sequence Number, USN) vermieden werden. Weitere Informationen über das Rollback für die Wiederverwendung finden Sie unter "US-v" und "Rollback".

## <a name="backup-and-restore-considerations-for-virtualized-domain-controllers"></a>Überlegungen zum Sichern und Wiederherstellen für virtualisierte Domänencontroller

Das Sichern von Domänencontrollern ist für jede Umgebung eine wichtige Aufgabe. Sicherungen schützen bei Domänencontrollerfehlern oder administrativen Fehlern vor Datenverlust. Wenn ein solches Ereignis auftritt, muss für den Systemstatus des Domänencontrollers ein Rollback für einen Zeitpunkt vor Auftreten des Fehlers ausgeführt werden. Zum Wiederherstellen des fehlerfreien Status eines Domänencontrollers wird mithilfe einer Active Directory-kompatiblen Sicherungsanwendung wie z. B. der Windows Server-Sicherung eine Systemstatussicherung wiederhergestellt, die aus der aktuellen Installation des Domänencontrollers stammt. Weitere Informationen zur Verwendung von Windows Server-Sicherung mit Active Directory Domain Services (AD DS) finden Sie in der [schrittweisen Anleitung für die AD DS Sicherung und Wiederherstellung](https://go.microsoft.com/fwlink/?LinkId=138501).

Mit der Technologie der virtuellen Computer erhalten bestimmte Anforderungen von Active Directory-Wiederherstellungsvorgängen zusätzliche Bedeutung. Wenn Sie z. B. einen Domänencontroller mithilfe einer Kopie der VHD-Datei (Virtual Hard Disk, virtuelle Festplatte) wiederherstellen, umgehen Sie den wichtigen Schritt der Aktualisierung der Datenbankversion eines Domänencontrollers, nachdem er wiederhergestellt wurde. Die Replikation wird mit ungeeigneten Trackingnummern fortgesetzt, was zu einer inkonsistenten Datenbank unter den Domänencontrollerreplikaten führt. In den meisten Fällen wird dieses Problem nicht vom Replikationssystem erkannt, und trotz Inkonsistenzen zwischen Domänencontrollern werden keine Fehler gemeldet.

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

Wie bereits erwähnt, gelten für auf virtuellen Computern ausgeführte Domänencontroller im Gegensatz zu auf physischen Computern ausgeführte Domänencontrollern Einschränkungen. Beim Sichern oder Wiederherstellen eines virtuellen Domänencontrollers sollten bestimmte Praktiken und Features der Virtualisierungssoftware nicht verwendet werden:

   - Kopieren oder klonen Sie keine VHD-Dateien von Domänencontrollern, anstatt regelmäßige Sicherungen auszuführen. Wenn die VHD-Datei kopiert oder geklont wird, führt dies dazu, dass sie veraltet ist. Wenn die virtuelle Festplatte im normalen Modus gestartet wird, wird ein Rollback für die virtuelle Festplatte angezeigt. Sie sollten ordnungsgemäße Sicherungsvorgänge ausführen, die von Active Directory-Domänendiensten unterstützt werden. Beispielsweise können Sie das Feature der Windows Server-Sicherung verwenden.  
   - Verwenden Sie das Snapshotfeature nicht als Sicherung zum Wiederherstellen eines virtuellen Computers, der als Domänencontroller konfiguriert wurde. Bei der Replikation treten Probleme auf, wenn Sie den virtuellen Computer mit Windows Server 2008 R2 und älter auf einen früheren Status zurücksetzen. Weitere Informationen finden Sie unter " [US-v" und "Wiederverwendungs-Rollback](#usn-and-usn-rollback)". Die Verwendung eines Snapshots zum Wiederherstellen eines schreibgeschützten Domänencontrollers (Read-Only Domain Controller, RODC) verursacht zwar keine Replikationsprobleme, dennoch wird von dieser Wiederherstellungsmethode abgeraten.  

## <a name="restoring-a-virtual-domain-controller"></a>Wiederherstellen eines virtuellen Domänencontrollers

Sie müssen den Systemstatus regelmäßig sichern, um einen fehlerhaften Domänencontroller wiederherstellen zu können. Zum Systemstatus gehören Active Directory-Daten und -Protokolldateien, die Registrierung, das Systemvolume (Ordner SYSVOL) sowie verschiedene Elemente des Betriebssystems. Diese Anforderung unterscheidet sich nicht zwischen physischen und virtualisierten Domänencontrollern. Mit den von Active Directory-kompatiblen Sicherungsanwendungen ausgeführten Verfahren für die Systemstatuswiederherstellung soll nach einem Wiederherstellungsvorgang die Konsistenz lokaler und replizierter Active Directory-Datenbanken sichergestellt werden, wozu auch die Benachrichtigung von Replikationspartnern über Zurücksetzungen der Aufrufkennung gehört. Mithilfe von virtuellen Hostumgebungen und Datenträger- oder Betriebssystem-Abbilderstellungsanwendungen können Administratoren jedoch die Überprüfungen umgehen, die normalerweise beim Wiederherstellen des Domänencontroller-Systemstatus ausgeführt werden.

Wenn bei einem virtuellen Computer eines Domänencontrollers ein Fehler auftritt und kein Rollback der Aktualisierungssequenznummern (Update Sequence Number, USN) ausgeführt wird, gibt es zwei Möglichkeiten zum Wiederherstellen des virtuellen Computers:

   - Falls eine gültige Sicherung der Systemstatusdaten vorhanden ist, die vor dem Auftreten des Fehlers erstellt wurde, können Sie den Systemstatus mithilfe der Wiederherstellungsoption des Sicherungsprogramms wiederherstellen, mit dem Sie die Sicherung erstellt haben. Die Sicherung der Systemstatusdaten muss mit einem Active Directory-kompatiblen Sicherungsprogramm innerhalb der Tombstone-Lebensdauer erstellt worden sein, also standardmäßig vor maximal 180 Tagen. Sie sollten Ihre Domänencontroller mindestens immer bei Erreichen der Hälfte der Tombstone-Lebensdauer sichern. Anweisungen dazu, wie Sie die jeweilige Tombstone-Lebensdauer für Ihre Gesamtstruktur ermitteln, finden Sie unter [bestimmen der Tombstone-Lebensdauer für die](https://go.microsoft.com/fwlink/?linkid=137177)Gesamtstruktur.  
   - Falls eine Arbeitskopie der VHD-Datei, aber keine Systemstatussicherung verfügbar ist, können Sie den vorhandenen virtuellen Computer entfernen. Stellen Sie den vorhandenen virtuellen Computer mithilfe einer vorherigen Kopie der VHD-Datei wieder her. Starten Sie den Computer jedoch unbedingt im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM), und konfigurieren Sie die Registrierung ordnungsgemäß, wie im folgenden Abschnitt beschrieben. Anschließend starten Sie den Domänencontroller im normalen Modus neu.

Bestimmen Sie anhand des Verfahrens in der folgenden Abbildung die optimale Methode zum Wiederherstellen Ihres virtualisierten Domänencontrollers.

![](media/virtualized-domain-controller-architecture/Dd363553.85c97481-7b95-4705-92a7-006e48bc29d0(WS.10).gif)

Für RODCs sind der Wiederherstellungsvorgang und die Entscheidungen einfacher.

![](media/virtualized-domain-controller-architecture/Dd363553.4c5c5eda-df95-4c6b-84e0-d84661434e5d(WS.10).gif)

## <a name="restoring-the-system-state-backup-of-a-virtual-domain-controller"></a>Wiederherstellen der Systemstatussicherung eines virtuellen Domänencontrollers

Falls eine gültige Systemstatussicherung für den virtuellen Computer eines Domänencontrollers vorhanden ist, können Sie die Sicherung problemlos wiederherstellen. Führen Sie dazu das Wiederherstellungsverfahren des Sicherungstools aus, mit dem Sie die VHD-Datei gesichert haben.

> [!IMPORTANT]
> Sie müssen den Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus starten, um ihn ordnungsgemäß wiederherstellen zu können. Der Domänencontroller darf nicht im normalen Modus gestartet werden. Wenn Sie während des Systemstarts nicht die Möglichkeit haben, DSRM einzugeben, deaktivieren Sie den virtuellen Computer des Domänen Controllers, bevor er vollständig im normalen Modus gestartet werden kann. Sie müssen den Domänencontroller unbedingt im Verzeichnisdienst-Wiederherstellungsmodus starten, da beim Starten eines Domänencontrollers im normalen Modus dessen Aktualisierungssequenznummern erhöht werden, selbst wenn der Domänencontroller vom Netzwerk getrennt wird. Weitere Informationen über das Rollback für die Wiederverwendung finden Sie unter "US-v" und "Rollback". 

## <a name="to-restore-the-system-state-backup-of-a-virtual-domain-controller"></a>So stellen Sie die Systemstatussicherung eines virtuellen Domänencontrollers wieder her

1. Starten Sie den virtuellen Computer des Domänen Controllers, und drücken Sie F5, um auf den Bildschirm Windows-Start-Manager zuzugreifen. Falls Sie Anmeldeinformationen für die Verbindung eingeben müssen, klicken Sie auf dem virtuellen Computer sofort auf die Taste **Pause**, damit der Startvorgang nicht fortgesetzt wird. Geben Sie anschließend die Anmeldeinformationen für die Verbindung ein, und klicken Sie auf dem virtuellen Computer auf die Schaltfläche **Wiedergabe**. Klicken Sie in das Fenster des virtuellen Computers, und drücken Sie F5.

   Wenn der Bildschirm des Windows-Boot-Managers nicht angezeigt wird und der Domänencontroller im normalen Modus gestartet wird, schalten Sie den virtuellen Computer aus, um zu verhindern, dass der Startvorgang abgeschlossen wird. Wiederholen Sie diesen Schritt so oft wie nötig, bis Sie auf den Bildschirm des Windows-Boot-Managers zugreifen können. Im Menü Windows-Fehlerbehebung ist kein Zugriff auf den Verzeichnisdienst-Wiederherstellungsmodus möglich. Schalten Sie deshalb den virtuellen Computer aus, und wiederholen Sie den Vorgang, wenn das Menü Windows-Fehlerbehebung angezeigt wird.

2. Drücken Sie im Bildschirm des Windows-Boot Managers F8, um auf die erweiterten Startoptionen zuzugreifen.
3. Wählen Sie im Bildschirm **Erweiterte Startoptionen** die Option **Verzeichnisdienstwiederherstellung** aus, und drücken Sie dann die EINGABETASTE. Dadurch wird der Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus gestartet.
4. Verwenden Sie die entsprechende Wiederherstellungsmethode für das Tool, mit dem Sie die Systemstatussicherung erstellt haben. Wenn Sie Windows Server-Sicherung verwendet haben, finden Sie weitere Informationen unter [Ausführen einer nicht autorisierenden Wiederherstellung AD DS](https://go.microsoft.com/fwlink/?linkid=132637).

## <a name="restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available"></a>Wiederherstellen eines virtuellen Domänencontrollers, wenn keine entsprechende Sicherung der Systemstatusdaten verfügbar ist

Falls keine Sicherung der Systemstatusdaten vorhanden ist, die vor dem Auftreten des Fehlers bei dem virtuellen Computer erstellt wurde, können Sie eine vorherige VHD-Datei zum Wiederherstellen eines auf einem virtuellen Computer ausgeführten Domänencontrollers verwenden. Erstellen Sie, falls möglich, eine Kopie der virtuellen Festplatte. Falls nämlich während der Prozedur ein Problem auftritt oder Sie einen Schritt verpassen, können Sie es mit der kopierten virtuellen Festplatte erneut versuchen.

> [!IMPORTANT]
> - Sie sollten die folgende Prozedur nicht als Ersatz für regelmäßig geplante und terminierte Sicherungen in Betracht ziehen.
> - **Wiederherstellungen, die mit dem folgenden Verfahren ausgeführt werden, werden von Microsoft nicht unterstützt und sollten nur verwendet werden, wenn es keine andere Alternative gibt.**
> - Verwenden Sie dieses Verfahren nicht, wenn die Kopie der wiederherzustellenden VHD (Virtual Hard Disk, virtuelle Festplatte) von einem virtuellen Computer im normalen Modus gestartet wurde.

## <a name="to-restore-a-previous-version-of-a-virtual-domain-controller-vhd-without-system-state-data-backup"></a>So stellen Sie eine vorherige Version der VHD eines virtuellen Domänencontrollers ohne Sicherung der Systemstatusdaten wieder her

1. Verwenden Sie die vorherige VHD, und starten Sie den virtuellen Domänencontroller wie im vorherigen Abschnitt beschrieben im Verzeichnisdienst-Wiederherstellungsmodus. Der Domänencontroller darf nicht im normalen Modus gestartet werden. Wenn der Bildschirm des Windows-Boot-Managers nicht angezeigt wird und der Domänencontroller im normalen Modus gestartet wird, schalten Sie den virtuellen Computer aus, um zu verhindern, dass der Startvorgang abgeschlossen wird. Ausführliche Anweisungen zum Aktivieren des Verzeichnisdienst-Wiederherstellungsmodus finden Sie im vorherigen Abschnitt.
2. Öffnen Sie den Registrierungs-Editor. Klicken Sie zum Öffnen des Registrierungs-Editors auf **Start**und auf **Ausführen**, geben Sie **Regedit**ein, und klicken Sie dann auf OK. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**. Erweitern Sie im Registrierungs-Editor den folgenden Pfad: **HKEY\_\\local\_MachineSystem\\\\CurrentControlSetServices\\NTDS-Parameter.\\** Suchen Sie nach dem Wert **DSA Previous Restore Count**. Wenn dieser Wert vorhanden ist, notieren Sie sich die Einstellung. Wenn dieser Wert nicht vorhanden ist, entspricht die Einstellung dem Standardwert, also null. Fügen Sie keinen Wert hinzu, falls kein Wert angezeigt wird.
3. Klicken Sie mit der rechten Maustaste auf den Registrierungsschlüssel **Parameters**, klicken Sie auf **Neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)** .
4. Geben Sie den neuen Namen **Von Sicherung wiederhergestellte Datenbank** ein, und drücken Sie die EINGABETASTE.
5. Doppelklicken Sie auf den soeben erstellten Wert, um das Dialogfeld **DWORD-Wert (32-Bit) bearbeiten** zu öffnen, und geben Sie dann **1** im Feld **Wert** ein. Die Option **aus Sicherungs Eintrag wiederhergestellte Datenbank** ist auf Domänen Controllern verfügbar, auf denen Windows 2000 Server mit Service Pack 4 (SP4) ausgeführt wird, Windows Server 2003 mit den Updates, die im Abschnitt [zum erkennen und Wiederherstellen nach einem Wiederherstellungs Steuerungspunkt in enthalten sind. Windows Server 2003, Windows Server 2008 und Windows Server 2008 R2](https://go.microsoft.com/fwlink/?linkid=137182) in der installierten Microsoft Knowledge Base und Windows Server 2008.
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
12. Überprüfen Sie im Registrierungs-Editor, ob der Wert in **DSA Previous Restore Count** dem vorherigen Wert plus 1 entspricht. Wenn dies nicht der richtige Wert ist und Sie keinen Eintrag für die Ereignis-ID 1109 in Ereignisanzeige finden, überprüfen Sie, ob die Service Packs des Domänen Controllers aktuell sind. Sie können diese Prozedur auf der gleichen VHD nicht erneut durchführen. Sie können sie auf einer Kopie der VHD oder einer anderen VHD erneut ausführen, die nicht im normalen Modus gestartet wurde, indem Sie bei Schritt 1 von vorne anfangen.
13. Schließen Sie den Registrierungs-Editor.

## <a name="usn-and-usn-rollback"></a>USN und USN-Rollback

In diesem Abschnitt werden Replikationsprobleme beschrieben, die auftreten können, wenn die Active Directory-Datenbank mit einer älteren Version eines virtuellen Computers fehlerhaft wiederhergestellt wurde. Weitere Informationen zum Active Directory Replikationsprozess finden Sie unter [Active Directory Replikations Konzepten](../replication/active-directory-replication-concepts.md) .

## <a name="usns"></a>USNs

Active Directory-Domänendienste (Active Directory Domain Services, AD DS) verwenden Aktualisierungssequenznummern (Update Sequence Number, USN) zum Nachverfolgen der Replikation von Daten zwischen Domänencontrollern. Bei jeder Änderung von Daten im Verzeichnis wird die USN erhöht, um darauf hinzuweisen, dass eine Änderung vorgenommen wurde.

Für jede auf einem Zieldomänencontroller gespeicherte Verzeichnispartition werden mithilfe von USNs das neueste Quellupdate, das der Datenbank eines Domänencontrollers hinzugefügt wurde, sowie der Status jedes anderen Domänencontrollers, auf dem ein Replikat der Verzeichnispartition gespeichert ist, nachverfolgt. Bei der Replikation von Änderungen zwischen Domänencontrollern werden von den Replikationspartnern diejenigen Änderungen abgerufen, deren USNs größer sind als die USN der letzten vom jeweiligen Partner empfangenen Änderung.

Die USNs sind in zwei Tabellen mit Replikationsmetadaten enthalten. Sie werden von Quell- und Zieldomänencontrollern zum Filtern von Updates verwendet, die der Zieldomänencontroller benötigt.

1. **Aktualitätsvektor**: Eine Tabelle, die vom Zieldomänen Controller für die Nachverfolgung der Ursprungs Updates verwaltet wird, die von allen Quell Domänen Controllern empfangen werden. Wenn ein Zieldomänencontroller Änderungen für eine Verzeichnispartition anfordert, stellt er dem Quelldomänencontroller seinen Aktualitätsvektor bereit. Der Quelldomänencontroller filtert dann mithilfe dieses Werts die dem Zieldomänencontroller zu sendenden Updates. Der Quell Domänen Controller sendet seinen Aktualitäts Vektor beim Abschluss eines erfolgreichen Replikations Prozesses an das Ziel, um sicherzustellen, dass der Zieldomänen Controller weiß, dass er mit allen Domänen Controllern synchronisiert wurde. Ursprungs Updates und Updates befinden sich auf derselben Ebene wie die Quelle.  
2. **Obere Grenze**: Ein Wert, der vom Zieldomänen Controller verwaltet wird, um die neuesten Änderungen zu verfolgen, die er von einem bestimmten Quell Domänen Controller für eine bestimmte Partition erhalten hat. Die obere Kontingentgrenze verhindert, dass dem Zieldomänencontroller vom Quelldomänencontroller wiederholt dieselben Änderungen gesendet werden.  

## <a name="directory-database-identity"></a>Verzeichnisdatenbankidentität

Neben USNs verfolgen Domänencontroller die Verzeichnisdatenbank der Quellreplikationspartner. Die Identität der auf dem Server ausgeführten Verzeichnisdatenbank wird separat von der Identität des Serverobjekts selbst verwaltet. Die Verzeichnisdatenbankidentität wird auf den einzelnen Domänencontrollern im **invocationID**-Attribut des NTDS-Einstellungsobjekts gespeichert, das sich im folgenden LDAP-Pfad (Lightweight Directory Access-Protokoll) befindet: cn=NTDS Settings, cn=ServerName, cn=Servers, cn=*SiteName*, cn=Sites, cn=Configuration, dc=*ForestRootDomain*. Die Serverobjektidentität wird im **objectGUID**-Attribut des NTDS-Einstellungsobjekts gespeichert. Die Identität des Softwareobjekts wird nie geändert. Die Identität der Verzeichnisdatenbank hingegen ändert sich, wenn auf dem Server eine Systemstatuswiederherstellung ausgeführt wird oder wenn eine Anwendungsverzeichnispartition auf dem Server hinzugefügt, entfernt und dann erneut hinzugefügt wird. (anderes Szenario: Wenn eine HyperV-Instanz Ihre VSS-Writer auf einer Partition auslöst, die die virtuelle Festplatte eines virtuellen Domänen Controllers enthält, löst der Gast wiederum seine eigenen VSS-Writer aus (derselbe Mechanismus, der von der Sicherung/Wiederherstellung verwendet wird), was zu einer anderen Methode führt, mit der invocationID Festlegen

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

Das USN-Rollback erfolgt, wenn die normalen Updates der USNs umgangen werden und ein Domänencontroller eine USN zu verwenden versucht, die niedriger als das letzte Update ist. In den meisten Fällen wird ein Rollback für die Wiederverwendung in der Gesamtstruktur erkannt, und die Replikation wird beendet. 

Ein USN-Rollback kann viele Ursachen haben. Beispielsweise, wenn alte VHD-Dateien verwendet werden oder eine P2V-Konvertierung (Physical-to-Virtual) ausgeführt wird, ohne sicherzustellen, dass der physische Computer nach der Konvertierung dauerhaft offline bleibt. Ergreifen Sie die folgenden Vorsichtsmaßnahmen, um sicherzustellen, dass kein USN-Rollback ausgeführt wird:

   - Verwenden Sie keine Momentaufnahme eines virtuellen Domänen Controller Computers, wenn Windows Server 2012 oder höher nicht ausgeführt wird.
   - Kopieren Sie die VHD-Datei des Domänencontrollers nicht.  
   - Wenn Windows Server 2012 oder höher nicht ausgeführt wird, exportieren Sie nicht den virtuellen Computer, auf dem ein Domänen Controller ausgeführt wird.  
   - Stellen Sie einen Domänencontroller einer Active Directory-Datenbank nur mit einer unterstützten Sicherung her bzw. führen Sie ein Rollback für die Inhalte einer Active Directory-Datenbank nur mit einer unterstützten Sicherungslösung wie z. B. der Windows Server-Sicherung aus.  

In manchen Fällen bleibt ein USN-Rollback unerkannt. In anderen Fällen können andere Replikationsfehler verursacht werden. In diesen Fällen muss der Umfang des Problems analysiert und das Problem zeitnah behoben werden. Informationen dazu, wie Sie veraltete Objekte entfernen, die als Ergebnis eines Rollbacks für die Benutzer-ID auftreten können, finden Sie unter [Veraltete Active Directory Objekte generieren der Ereignis-ID 1988 in Windows Server 2003](https://go.microsoft.com/fwlink/?linkid=137185) in der Microsoft Knowledge Base.

## <a name="usn-rollback-detection"></a>USN-Rollbackerkennung

In den meisten Fällen werden USN-Rollbacks ohne entsprechende Zurücksetzung des Werts **invocationID**, die durch unzulässige Wiederherstellungsverfahren verursacht werden, erkannt. Windows Server 2008 bietet Schutzmaßnahmen vor einer unzulässigen Replikation nach einem unzulässigen Wiederherstellungsvorgang für den Domänencontroller. Diese Schutzmaßnahmen werden dadurch ausgelöst, dass ein unzulässiger Wiederherstellungsvorgang niedrigere USNs für Änderungen ergibt, die die Replikationspartner bereits empfangen haben.

Wenn in Windows Server 2008 und Windows Server 2003 SP1 ein Zieldomänencontroller Änderungen mithilfe einer bereits zuvor verwendeten USN anfordert, wird die Antwort des Quellreplikationspartners vom Zieldomänencontroller so gedeutet, dass die Replikationsmetadaten veraltet sind. Dies bedeutet, dass für die Active Directory-Datenbank auf dem Quelldomänencontroller ein Rollback auf einen vorherigen Status ausgeführt wurde. Beispielsweise wurde für die VHD-Datei eines virtuellen Computers ein Rollback auf eine vorherige Version ausgeführt. In diesem Fall startet der Zieldomänencontroller die folgenden Quarantänemaßnahmen auf dem Domänencontroller, bei dem eine unzulässige Wiederherstellung festgestellt wurde:

   - Der Netzwerkanmeldedienst wird von AD DS angehalten, wodurch Benutzer- und Computerkonten am Ändern von Kontokennwörtern gehindert werden. Diese Maßnahme verhindert den Verlust solcher Änderungen, falls sie nach einer unzulässigen Wiederherstellung auftreten.  
   - Die ein- und ausgehende Active Directory-Replikation wird von AD DS deaktiviert.  
   - Die Ereignis-ID 2095 wird von AD DS im Verzeichnisdienst-Ereignisprotokoll generiert, um auf diesen Zustand hinzuweisen.  

Die folgende Abbildung veranschaulicht die Abfolge von Ereignissen, wenn ein USN-Rollback auf VDC2, dem auf einem virtuellen Computer ausgeführten Zieldomänencontroller, erkannt wird. In dieser Abbildung erfolgt die Erkennung des Anwendungs Rollbacks auf VDC2, wenn ein Replikations Partner erkennt, dass VDC2 einen Aktualitäts-UPN-Wert gesendet hat, der zuvor vom Zieldomänen Controller erkannt wurde, was darauf hinweist, dass für dies-Datenbank ein Rollback ausgeführt wurde. nicht ordnungsgemäß.

![](media/virtualized-domain-controller-architecture/Dd363553.373b0504-43fc-40d0-9908-13fdeb7b3f14(WS.10).gif)

Führen Sie sofort das folgende Verfahren aus, wenn im Verzeichnisdienst-Ereignisprotokoll die Ereignis-ID 2095 gemeldet wird.

## <a name="to-resolve-event-id2095"></a>So beheben Sie die Ereignis-ID 2095

1. Trennen Sie die Netzwerkverbindung des virtuellen Computers, von dem der Fehler aufgezeichnet wurde.
2. Versuchen Sie festzustellen, ob Änderungen von diesem Domänencontroller stammen und an andere Domänencontroller weitergegeben wurden. Falls das Ereignis auf einen Snapshot oder eine Kopie eines gestarteten virtuellen Computers zurückzuführen ist, versuchen Sie den Zeitpunkt des USN-Rollbacks festzustellen. Anschließend können Sie die Replikationspartner dieses Domänencontrollers überprüfen, um festzustellen, ob seit diesem Zeitpunkt eine Replikation stattgefunden hat.

   Hierfür können Sie das Tool Repadmin verwenden. Informationen zur Verwendung von Repadmin finden [Sie unter Überwachung und Problembehandlung Active Directory Replikation mit repadmin](https://go.microsoft.com/fwlink/?linkid=122830). Wenn Sie dies nicht selbst ermitteln können, wenden Sie sich an [Microsoft-Support](https://support.microsoft.com) , um Unterstützung zu erhalten.

3. Erzwingen Sie eine Herabstufung des Domänencontrollers. Dies umfasst das Bereinigen der Metadaten des Domänen Controllers und das übernehmen der Betriebs Master Rollen (auch als Flexible Single Master Operations oder FSMO bezeichnet). Weitere Informationen finden Sie im Abschnitt "Wiederherstellen von einem Rollback für die [Windows Server 2003, Windows Server 2008 und Windows Server 2008 R2](https://go.microsoft.com/fwlink/?linkid=137182) " in der Microsoft Knowledge Base in der Microsoft Knowledge Base.
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

Weitere Informationen zu RODCs finden [Sie im Planungs-und Bereitstellungs Handbuch für schreibgeschützte Domänen Controller](../../deploy/rodc/read-only-domain-controller-updates.md).
