---
title: Wiederherstellung der Active Directory-Gesamtstruktur - bestimmen, wie die Gesamtstruktur wiederherstellen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: cc2525068225644b0964a2726bd9c0dcf2e0cba0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="determine-how-to-recover-the-forest"></a>Bestimmen der Vorgehensweise beim Wiederherstellen der Gesamtstruktur  

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Wiederherstellen einer Active Directory-Gesamtstruktur umfasst das aus einer Sicherung wiederherstellen, oder installieren Active Directory-Domänendienste (AD DS) auf jedem Domänencontroller (DC) in der Gesamtstruktur. Wiederherstellung der Gesamtstruktur wird jede Domäne in der Gesamtstruktur in den Zustand zum Zeitpunkt der letzten vertrauenswürdigen Sicherung wiederhergestellt. Daher führt der Wiederherstellungsvorgang den Verlust von mindestens die folgenden Active Directory-Daten:  
  
-   Alle Objekte (z.B. Benutzer und Computer), die nach der letzten Sicherung des vertrauenswürdigen hinzugefügt wurden  
  
-   Alle Updates, die an bestehenden Objekten vorgenommen wurden seit die letzten vertrauenswürdige Sicherung  
  
-   Alle Änderungen, die seit der letzten vertrauenswürdigen Sicherung die Konfigurationspartition oder die Schemapartition in AD DS (z.B. Schemaänderungen) vorgenommen wurden  
  
 Für jede Domäne in der Gesamtstruktur muss das Kennwort eines Domänenadministratorkontos bekannt sein. Vorzugsweise, ist dies das Kennwort für das integrierte Administratorkonto an, der nicht deaktiviert werden muss. Sie müssen auch das DSRM-Kennwort zum Ausführen der Wiederherstellung des Systemstatus eines Domänencontrollers kennen. Im Allgemeinen ist es empfehlenswert, das Administratorkonto und das DSRM-Kennwortverlauf an einem sicheren Ort für archivieren, solange die Sicherungen gültig ist, d.h. innerhalb der Tombstone-Lebensdauer Zeitraum oder innerhalb des gelöschten Objekts Lebensdauer Zeitraum, wenn die Active Directory-Papierkorb aktiviert ist. Sie können auch das DSRM-Kennwort mit einem Domänenbenutzerkonto synchronisieren, um leichter zu merken. Weitere Informationen finden Sie im KB-Artikel [961320](https://support.microsoft.com/kb/961320). Synchronisieren das DSRM-Konto muss vor der Wiederherstellung der Gesamtstruktur, als Teil der Vorbereitung erfolgen.  
  
> [!NOTE]
>  Das Administratorkonto ist Mitglied der integrierten Administratorengruppe standardmäßig, wie die Gruppen Domänen-Admins und Organisations-Admins sind. Diese Gruppe über Vollzugriff auf alle Domänencontroller in der Domäne verfügt.  
  
## <a name="determining-which-backups-to-use"></a>Bestimmen die Sicherungen verwenden  
 Mindestens zwei beschreibbaren Domänencontroller für jede Domäne regelmäßig sichern Sie müssen Sie mehrere Sicherungen aus. Beachten Sie, dass Sie nicht die Sicherung eines schreibgeschützten Domänencontrollers (RODC) zum Wiederherstellen von eines beschreibbaren Domänencontrollers verwenden. Es wird empfohlen, dass Sie den Domänencontroller mithilfe von Sicherungen, die ein paar Tage vor dem Auftreten des Fehlers ausgeführt wurden, wiederherstellen. Im Allgemeinen müssen Sie einen Kompromiss zwischen die Aktualität und die Safeness der wiederhergestellten Daten ermitteln. Eine aktuelle Sicherung werden nützlichere Daten wiederhergestellt, aber möglicherweise muss das Risiko, dass darin gefährliche Daten in der wiederhergestellten Gesamtstruktur auswählen.  
  
 Wiederherstellen von Sicherungen des Systemstatus, hängt von der ursprünglichen Betriebssystem und Server der Sicherung. Beispielsweise sollten Sie eine Sicherung des Systemstatus nicht auf einen anderen Server wiederherstellen. In diesem Fall wird möglicherweise folgende Warnung angezeigt:  
  
 "Die angegebene Sicherung wird von einem anderen Server als den aktuellen. Es wird nicht empfohlen, den Systemstatus mit der Sicherung auf einem alternativen Server ausführen, da der Server nicht mehr verwendet werden kann. Sind Sie sicher, dass Sie diese Sicherung zum Wiederherstellen des aktuellen Servers verwenden möchten?"  
  
 Wenn Sie Active Directory auf anderer Hardware wiederherstellen müssen, erstellen Sie Sicherungen für vollständige Server- und planen eine vollständigen Wiederherstellung ausführen.  
  
> [!IMPORTANT]
>  Ab Windows Server2008, ist es nicht unterstützt Sicherung des Systemstatus zu einer neuen Installation von Windows Server auf neue Hardware oder der gleichen Hardware wiederherstellen. Wenn Windows Server auf der gleichen Hardware erneut installiert wird, wie weiter unten in diesem Handbuch empfohlen, können Sie den Domänencontroller in dieser Reihenfolge wiederherstellen:  
>   
>  1.  Führen Sie eine Wiederherstellung vollständiger Server, um das Betriebssystem und alle Dateien und Anwendungen wiederherstellen.  
> 2.  Führen Sie die Wiederherstellung des Systemstatus mit wbadmin.exe um SYSVOL als autorisierend kennzeichnen.  
>   
>  Weitere Informationen finden Sie im Microsoft KB-Artikel [249694](https://support.microsoft.com/kb/249694).  
  
 Wenn die Uhrzeit des Auftretens des Fehlers unbekannt ist, untersuchen Sie weiter, um Sicherungen zu identifizieren, die die letzten sicheren Zustand der Gesamtstruktur enthalten. Dieser Ansatz ist weniger geeignet ist. Aus diesem Grund wird dringend empfohlen, detaillierte Protokolle über den Zustand der AD DS täglich zu halten, ist ein Fehler bei der Gesamtstruktur, die ungefähre Zeitpunkt des Fehlers identifiziert werden kann. Sie sollten auch eine lokale Kopie der Sicherungen beschleunigen.  
  
 Wenn die Active Directory-Papierkorb aktiviert ist, entspricht die Sicherung Lebensdauer der **DeletedObjectLifetime** Wert oder die **TombstoneLifetime** Wert ist. Weitere Informationen finden Sie unter [Active Directory-Papierkorb Step-by-Step Handbuch](https://go.microsoft.com/fwlink/?LinkId=178657) (https://go.microsoft.com/fwlink/?LinkId=178657).  
  
 Alternativ können Sie auch die Active Directory-Datenbank bereitstellen Tool (Dsamain.exe) und ein Lightweight Directory Access Protocol (LDAP)-Tool, z.B. Ldp.exe oder Active Directory-Benutzer und -Computer zum Identifizieren der Sicherung der letzten sicheren Zustand der Gesamtstruktur verfügt. Das Active Directory-Datenbank bereitstellen-Tool, das in Windows Server2008 und neueren Windows Server-Betriebssystemen enthalten ist, macht die Active Directory-Daten, die in Sicherungen oder Momentaufnahmen als LDAP-Server gespeichert sind. Ein LDAP-Tool können Sie dann die Daten durchsuchen. Dieser Ansatz hat den Vorteil, dass Sie einen beliebigen DC in Directory Services-Wiederherstellungsmodus (DSRM), überprüfen Sie den Inhalt der Sicherung von AD DS neu starten nicht erforderlich.  
  
 Weitere Informationen zur Verwendung von Active Directory-Datenbank bereitstellen Tool finden Sie unter der [Tool von Active Directory-Datenbank bereitstellen Step-by-Step Handbuch](https://technet.microsoft.com/library/cc753609\(WS.10\).aspx).  
  
 Sie können auch die **Ntdsutil Snapshot** Befehl zum Erstellen von Snapshots von Active Directory-Datenbank. Durch einen Task zum Erstellen von Snapshots in regelmäßigen Abständen planen, können Sie mit der Zeit zusätzliche Kopien der Active Directory-Datenbank abrufen. Diese Kopien können Sie besser ermitteln, wenn die Gesamtstruktur-Fehler aufgetreten ist, und wählen Sie dann die besten Sicherung wiederherstellen. Verwenden Sie zum Erstellen von Snapshots, die Version der **Ntdsutil**, die im Lieferumfang von Windows Server2008 oder die Remoteserver-Verwaltungstools (RSAT) für Windows Vista oder höher. Der Zieldomänencontroller kann eine beliebige Version von Windows Server ausführen. Weitere Informationen zur Verwendung der **Ntdsutil Snapshot** finden Sie unter [Snapshot](https://technet.microsoft.com/library/cc731620\(WS.10\).aspx).  
  
  
## <a name="determining-which-domain-controllers-to-restore"></a>Ermitteln welche Domänencontroller wiederherstellen  
 Der Wiederherstellungsvorgang für die erleichterte Bedienung ist ein wichtiger Faktor bei der Entscheidung, welcher Domänencontroller wiederherstellen. Es wird empfohlen, einen dedizierten Domänencontroller für jede Domäne verfügen, die der bevorzugten Domänencontroller für die Wiederherstellung ist. Eine dedizierte wieder her, die DC erleichtert das zuverlässig planen und die Wiederherstellung der Gesamtstruktur ausgeführt werden, da Sie dieselbe Quellkonfiguration, die verwendet wurde verwenden, führen Sie Tests wiederhergestellt werden. Sie können Skript für die Wiederherstellung, und nicht mit unterschiedlichen Konfigurationen konkurrieren, z.B., ob der Domänencontroller Betriebsmasterfunktionen oder nicht innehat, oder ob es ein globaler Katalogserver oder DNS-Server ist.  
  
> [!NOTE]
>  Obwohl es nicht empfehlenswert ist eine Betriebsmasterfunktion aus Gründen der Einfachheit wiederherstellen, können einige Organisationen für weitere Vorteile wiederherstellen. Z.B. Wiederherstellen des RID-Masters kann verhindern, Probleme mit der Verwaltung von RIDs während der Wiederherstellungs.  
  
 Wählen Sie einen Domänencontroller, der am besten die folgenden Kriterien erfüllt:  
  
-   Einen Domänencontroller, der nicht schreibgeschützt ist. Dies ist erforderlich.  
  
-   Ein Domänencontroller unter Windows Server2012 als eine virtuelle Maschine auf einem Hypervisor, der VM-GenerationID unterstützt. Dieser Domänencontroller kann als Quelle für das Klonen verwendet werden.  
  
-   Einen Domänencontroller, der zugegriffen werden kann, entweder direkt oder in einem virtuellen Netzwerk, und vorzugsweise in einem Rechenzentrum. Auf diese Weise können Sie ganz einfach es über das Netzwerk während der Wiederherstellung der Gesamtstruktur isolieren.  
  
-   Einen Domänencontroller, der eine gute vollständige Server-Sicherung hat. Eine gute Sicherung ist eine Sicherung, die erfolgreich wiederhergestellt werden kann, ein paar Tage vor Auftreten des Fehlers erstellt wurde, und enthält als sehr viel sinnvolle Daten wie möglich.  
  
-   Einen Domänencontroller, der einen Domain Name System (DNS) Server vor Auftreten des Fehlers wurde. Dadurch sparen die erforderliche Zeit zum Installieren von DNS.  
  
-   Wenn Sie Windows-Bereitstellungsdienste verwenden, wählen Sie einen Domänencontroller, der nicht für die Verwendung von BitLocker-Netzwerkentsperrung konfiguriert ist. In diesem Fall wird BitLocker-Netzwerkentsperrung nicht unterstützt für den ersten Domänencontroller verwendet werden, die Sie während einer Wiederherstellung der Gesamtstruktur aus einer Sicherung wiederherstellen.  
  
     BitLocker-Netzwerkentsperrung als die *nur* Schlüsselschutzvorrichtung *kann nicht* verwendet werden auf Domänencontrollern, in dem Sie Windows-Verwaltungsinstrumentation (Windows Deployment Services, WDS) bereitgestellt haben, da dies in einem Szenario führt erforderlich ist, in denen des ersten Domänencontrollers, Active Directory und Windows-Bereitstellungsdienste ausgeführt werden, um zu entsperren. Vor der Wiederherstellung des ersten Domänencontrollers, Active Directory ist aber noch nicht verfügbar für Windows-Bereitstellungsdienste, damit es nicht entsperren kann.  
  
     Um festzustellen, ob ein Domänencontroller für die BitLocker-Netzwerkentsperrung verwenden konfiguriert ist, überprüfen Sie, dass es sich bei einem netzwerkentsperrungszertifikat in den folgenden Registrierungsschlüssel angegeben ist:  
  
     HKEY_LOCAL_MACHINESoftwarePoliciesMicrosoftSystemCertificatesFVE_NKP  
  
 Verwalten Sie Sicherheitsverfahren beim Behandeln von oder Wiederherstellen von Sicherungsdateien, die Active Directory enthalten. Die Dringlichkeit, die Wiederherstellung der Gesamtstruktur begleitet kann unbeabsichtigt zu Blick auf die bewährten Sicherheitsmethoden führen. Weitere Informationen finden Sie im Abschnitt "Einrichten Domänencontroller Sicherung und Wiederherstellung Strategien" in [Best Practice Guide for Securing Active Directory-Installationen und zuverlässig betreiben: Teil II](https://technet.microsoft.com/library/bb727066.aspx).  
  
## <a name="identify-the-current-forest-structure-and-dc-functions"></a>Identifizieren der aktuellen Gesamtstruktur und DC-Funktionen  
 Ermitteln der aktuellen Gesamtstruktur identifizieren alle Domänen in der Gesamtstruktur. Erstellen Sie eine Liste aller Domänencontroller in jeder Domäne, insbesondere die Domänencontroller, die Sicherungen und virtualisierte Domänencontroller, die als Quelle zum Klonen verwendet werden können. Eine Liste der Domänencontroller für die Stammdomäne der Gesamtstruktur ist die wichtigste, da Sie zunächst diese Domäne wiederhergestellt werden. Nach der Wiederherstellung der Gesamtstruktur-Stammdomäne erhalten Sie eine Liste mit den anderen Domänen, Domänencontroller und die Standorte in der Gesamtstruktur, mithilfe von Active Directory-Snap-Ins.  
  
 Bereiten Sie eine Tabelle mit den Funktionen der einzelnen Domänencontroller in der Domäne vor, wie im folgenden Beispiel gezeigt. Dies hilft Ihnen die Konfiguration vor dem Ausfall der Gesamtstruktur nach der Wiederherstellung wiederherzustellen.  
  
|DC-name|Betriebssystem|FSMO-FUNKTION|GLOBALER KATALOG|RODC|Sicherung|DNS|Server Core|VIRTUELLE MASCHINE|VM-GenID|  
|-------------|----------------------|----------|--------|----------|------------|---------|-----------------|--------|---------------|  
|DC_1|Windows Server 2012|Schemamaster, Domänennamenmaster|Ja|Nein|Ja|Nein|Nein|Ja|Ja|  
|DC_2|Windows Server 2012|Keine|Ja|Nein|Ja|Ja|Nein|Ja|Ja|  
|DC_3|Windows Server 2012|Infrastrukturmaster|Nein|Nein|Nein|Ja|Ja|Ja|Ja|  
|DC_4|Windows Server 2012|PDC-Emulator, RID-Master|Ja|Nein|Nein|Nein|Nein|Ja|Nein|  
|DC_5|Windows Server 2012|Keine|Nein|Nein|Ja|Ja|Nein|Ja|Ja|  
|RODC_1|Windows Server2008 R2|Keine|Ja|Ja|Ja|Ja|Ja|Ja|Nein|  
|RODC_2|Windows Server 2008|Keine|Ja|Ja|Nein|Ja|Ja|Ja|Nein|  
  
 Identifizieren Sie für jede Domäne in der Gesamtstruktur einen beschreibbaren Domänencontroller, der über einen vertrauenswürdigen Sicherung von Active Directory-Datenbank für diese Domäne verfügt. Seien Sie vorsichtig, wenn Sie Domänencontroller die wiederherzustellende Sicherung auswählen. Ungefähr den Tag und die Ursache des Fehlers bekannt sind, ist im Allgemeinen müssen Sie eine Sicherung zu verwenden, die ein paar Tage vor diesem Datum erstellt wurde.  
  
 In diesem Beispiel stehen vier Backup Kandidaten: DC_1, DC_2, DC_4 und DC_5. Dieser Sicherung Kandidaten stellen Sie nur eine her. Der empfohlene Domänencontroller ist DC_5 aus den folgenden Gründen:  
  
-   Es erfüllt die Anforderungen für die Verwendung als Quelle für virtualisierte Domänencontroller klonen, der, die sie Windows Server2012 ausgeführt wird, wie ein virtueller Domänencontroller auf einem Hypervisor, unterstützt VM-GenerationID, ausgeführt wird, Software, die zulässig ist, geklont zu werden (oder, die entfernt werden kann, ist dies nicht möglich sein geklonten). Nach der Wiederherstellung wird der PDC-Emulatorrolle übernommen werden, und der Gruppe "Klonbare Domänencontroller" für die Domäne hinzugefügt werden können.  
  
-   Es wird eine vollständige Installation von Windows Server2012 ausgeführt. Ein Domänencontroller, der eine Server Core-Installation ausgeführt wird, kann umständlicher als Ziel für die Wiederherstellung.  
  
-   Es ist ein DNS-Server. Aus diesem Grund muss DNS nicht neu installiert werden.  
  
> [!NOTE]
>  Da DC_5 kein globaler Katalogserver ist, hat sie auch einen Vorteil darin, dass der globale Katalog nicht nach der Wiederherstellung entfernt werden muss. Aber ob der Domänencontroller auch, dass ein globaler Katalogserver nicht ausschlaggebend ist, daran, dass ab Windows Server2012 ist, sind alle Domänencontroller globale Katalogserver standardmäßig, und entfernen und Hinzufügen des globalen Katalogs nach die Wiederherstellung in jedem Fall als Teil des Wiederherstellungsprozesses Gesamtstruktur empfohlen wird.  
  
## <a name="recover-the-forest-in-isolation"></a>Wiederherstellen der Gesamtstruktur isoliert  
 Das bevorzugte Szenario ist das Herunterfahren alle beschreibbaren Domänencontroller vor der ersten wiederhergestellten Domänencontroller wieder in die Produktionsumgebung aufgenommen wurde. Dadurch wird sichergestellt, dass alle gefährlichen Daten nicht erneut in die wiederhergestellten Gesamtstruktur repliziert werden. Es ist besonders wichtig, alle Betriebsmasterrolle herunterzufahren.  
  
> [!NOTE]
>  Gibt es möglicherweise Fälle, in denen Verschieben des ersten Domänencontrollers, die Sie für jede Domäne mit einem isolierten Netzwerk wiederherstellen und zulassen, dass andere Domänencontroller online, um Ausfallzeiten des Systems zu minimieren bleiben möchten. Wenn Sie aus einem fehlgeschlagenen Schemaupgrade wiederherstellen möchten, können Sie z.B. wahlweise behalten Domänencontroller, die im Produktionsnetzwerk ausgeführt wird, während Sie die Schrittezur Wiederherstellung isoliert ausführen.  
  
 Wenn Sie die virtualisierte Domänencontroller ausgeführt werden, können Sie verschieben sie mit einem virtuellen Netzwerk, das vom Produktionsnetzwerk isoliert ist, führen Sie Wiederherstellung aus. Virtualisierte Domänencontroller in einem separaten Netzwerk verschieben bietet zwei Vorteile:  
  
-   Wiederhergestellten Domänencontroller sind jeden das Problem verhindert, die die Wiederherstellung der Gesamtstruktur verursacht werden, da sie isoliert sind.  
  
-   Klonen von virtualisierten Domänencontroller kann, bevor sie wieder mit dem Produktionsnetzwerk geschaltet werden in der separaten Netzwerk durchgeführt werden, sodass eine kritische Anzahl von Domänencontrollern ausgeführt werden kann und getestet werden.  
  
 Wenn Sie Domänencontroller auf physische Hardware ausgeführt werden, trennen Sie das Netzwerkkabel des primären Domänencontrollers, die Sie in der Gesamtstruktur-Stammdomäne wiederherstellen möchten. Nach Möglichkeit auch trennen Sie Netzwerk von allen anderen Domänencontrollern. Dies verhindert, dass Domänencontroller replizieren, wenn sie versehentlich während der Wiederherstellung der Gesamtstruktur gestartet werden.  
  
 Bei einer großen Gesamtstruktur, die über mehrere Standorte verteilt sind, kann es schwierig sein zu garantieren, dass alle beschreibbaren Domänencontroller heruntergefahren werden. Aus diesem Grund werden die Schrittezur Wiederherstellung – z.B. das Computerkonto und Krbtgt-Konto außerdem auf Metadatenbereinigung zurücksetzen – wurden entwickelt, um sicherzustellen, dass die wiederhergestellten beschreibbaren Domänencontroller nicht gefährliche beschreibbaren Domänencontroller replizieren (für den Fall, dass einige in der Gesamtstruktur noch online sind).  
  
 Nur durch das Offlineschalten von beschreibbaren Domänencontroller können Sie jedoch sicherstellen, dass die Replikation nicht der Fall? Aus diesem Grund sollten nach Möglichkeit, Sie remote Management-Technologie bereitstellen, mit denen Sie Herunterfahren und physisch beschreibbaren Domänencontroller während der Wiederherstellung der Gesamtstruktur zu isolieren.  
  
 RODCs können weiterhin ausgeführt werden, während die beschreibbaren Domänencontroller offline sind. Keine andere Domänencontroller repliziert direkt Änderungen von jedem RODC – insbesondere keine Schema oder Konfiguration Container ändert sich – damit sie während der Wiederherstellung keine Risiko wie beschreibbaren Domänencontroller darstellen. Nachdem alle beschreibbaren Domänencontroller wiederhergestellt und online sind, sollten Sie alle RODCs neu erstellen.  
  
 RODCs weiterhin Zugriff auf lokale Ressourcen zu ermöglichen, die in ihren jeweiligen Standorten zwischengespeichert werden, während der Wiederherstellungsvorgänge parallel passiert werden. Lokale Ressourcen, die nicht auf dem RODC zwischengespeichert werden müssen Authentifizierungsanforderungen an einem beschreibbaren Domänencontroller weitergeleitet. Diese Anforderungen schlägt fehl, da beschreibbaren Domänencontroller offline sind. Einige Vorgänge, z.B. Kennwortänderungen funktioniert auch nicht, bis Sie beschreibbaren Domänencontroller wiederherstellen.  
  
 Wenn Sie eine Hub-and-Spoke-Netzwerkarchitektur verwenden, können Sie zunächst zur Wiederherstellung der beschreibbaren Domänencontroller an den Hubstandorten konzentrieren. Später können Sie die RODCs an Remotestandorten neu erstellen.  
  
## <a name="next-steps"></a>Nächste Schritte
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Konzipierung einen Wiederherstellungsplan benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - identifizieren](AD-Forest-Recovery-Identify-the-Problem.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - führen Sie erste wiederherstellen](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  
-   [AD-Gesamtstruktur-Wiederherstellung – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server2003-Domänencontroller](AD-Forest-Recovery-Windows-Server-2003.md)  
