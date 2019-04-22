---
title: Wiederherstellung der Active Directory-Gesamtstruktur - bestimmen Sie, wie die Gesamtstruktur wiederherstellen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 30d23d977b4d7cd320d78ff340120df7013dee4c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817731"
---
# <a name="determine-how-to-recover-the-forest"></a>Bestimmen Sie, wie die Gesamtstruktur wiederherstellen

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Wiederherstellen der gesamte Active Directory-Gesamtstruktur umfasst das entweder aus einer Sicherung wiederherstellen oder neu installieren von Active Directory Domain Services (AD DS) auf jedem Domänencontroller (DC) in der Gesamtstruktur. Wiederherstellung der Gesamtstruktur wird jede Domäne in der Gesamtstruktur in den Zustand zum Zeitpunkt der letzten vertrauenswürdigen Sicherung wiederhergestellt. Daher wird der Restore-Vorgang den Verlust von mindestens die folgenden Active Directory-Daten ausgegeben:

- Alle Objekte (z. B. Benutzer und Computer), die nach der letzten Sicherung des vertrauenswürdigen hinzugefügt wurden
- Alle Updates, die an bestehenden Objekten vorgenommen wurden, seitdem vertrauenswürdige der letzten Sicherung
- Alle Änderungen, die entweder die Konfigurationspartition oder die Schemapartition in AD DS (z. B. schemaänderungen), die seit der letzten Sicherung des vertrauenswürdigen vorgenommen wurden

Für jede Domäne in der Gesamtstruktur muss das Kennwort eines Domänenadministratorkontos bekannt sein. Idealerweise ist dies das Kennwort für das integrierte Administratorkonto. Außerdem benötigen Sie das DSRM-Kennwort, um eine Wiederherstellung des Systemstatus eines DC auszuführen. Im Allgemeinen ist es empfiehlt sich, das Administratorkonto und das DSRM-Kennwort-Verlauf an einem sicheren Ort archivieren für so lange die Sicherungen gültig sind, d. h. innerhalb der Tombstone-Lebensdauer oder innerhalb der Lebensdauer des gelöschten Objekts Punkt, wenn die Active Directory-Papierkorb "Bin" aktiviert ist. Sie können auch das DSRM-Kennwort mit einem Domänen-Benutzerkonto synchronisieren, damit einfacher zu merken. Weitere Informationen finden Sie im Artikel KB [961320](https://support.microsoft.com/kb/961320). Synchronisieren das DSRM-Konto muss vor der Wiederherstellung der Gesamtstruktur, im Rahmen der Vorbereitung ausgeführt werden.

> [!NOTE]
> Das Administratorkonto ist Mitglied der integrierten Gruppe Administratoren in der Standardeinstellung an, wie die Gruppen Domänen-Admins und Organisations-Admins sind. Diese Gruppe hat Vollzugriff auf alle Domänencontroller in der Domäne.

## <a name="determining-which-backups-to-use"></a>Bestimmen die Sicherungen verwenden

Sichern Sie Sie über mindestens zwei beschreibbaren Domänencontroller für jede Domäne regelmäßig müssen Sie mehrere Sicherungen auswählen. Beachten Sie, dass Sie die Sicherung von einem schreibgeschützten Domänencontroller (RODC) nicht zum Wiederherstellen von eines beschreibbaren Domänencontroller verwenden können. Es wird empfohlen, dass Sie die DCs wiederherstellen, indem Sicherungen, die ein paar Tage vor dem Auftreten des Fehlers ausgeführt wurden. Im Allgemeinen müssen Sie einen Kompromiss zwischen die Aktualität und die Safeness wiederhergestellten Daten bestimmen. Auswählen eine neuere Sicherung wiederhergestellt wird, weitere nützliche Daten, aber möglicherweise muss das Risiko von Wiedereinführung der risikobehafteten Daten in der wiederhergestellten Gesamtstruktur.

Wiederherstellen von Sicherungen des Systemstatus, hängt von dem ursprünglichen Betriebssystem und die Server der Sicherung. Beispielsweise sollten Sie eine Sicherung des Systemstatus nicht auf einen anderen Server wiederherstellen. In diesem Fall wird möglicherweise die folgende Warnung angezeigt:

"Die angegebene Sicherung ist von einem anderen Server als dem aktuellen Objekt. Wir empfehlen nicht, eine systemstatuswiederherstellung mit der Sicherung auf einem alternativen Server durchführen, da der Server nicht mehr verwendet werden kann. Sind Sie sicher, dass Sie diese Sicherung für die Wiederherstellung nach dem aktuellen Server verwenden möchten? "

Wenn Sie Active Directory auf anderer Hardware wiederherstellen müssen, erstellen Sie vollständige Sicherungen und planen eine vollständigen Wiederherstellung ausführen.

> [!IMPORTANT]
> Ab Windows Server 2008 kann nicht zum Wiederherstellen der Sicherung des Systemstatus auf eine neue Installation von Windows Server auf neuer Hardware oder die gleiche Hardware. Wenn Sie Windows Server auf derselben Hardware, neu installiert wird, wie weiter unten in diesem Handbuch empfohlen, können Sie den Domänencontroller in dieser Reihenfolge wiederherstellen:
>
> 1. Ausführen einer vollständigen Wiederherstellung zum Wiederherstellen des Betriebssystems und aller Dateien und Anwendungen.
> 2. Führen Sie die Wiederherstellung des Systemstatus mithilfe von wbadmin.exe zur SYSVOL als autorisierend kennzeichnen.
>
> Weitere Informationen finden Sie im Microsoft KB-Artikel [249694](https://support.microsoft.com/kb/249694).

Wenn die Uhrzeit des Auftretens des Fehlers unbekannt ist, können Sie weiter untersuchen Sie, um Sicherungen zu identifizieren, die den letzten abgesicherten Zustand der Gesamtstruktur enthalten. Dieser Ansatz ist nicht das bevorzugte Tag. Aus diesem Grund wird dringend empfohlen, detaillierte Protokolle zu den Integritätsstatus von AD DS auf täglicher Basis beizubehalten, wenn ein Gesamtstruktur-Fehler vorliegt, den ungefähren Zeitpunkt des Fehlschlags identifiziert werden kann. Bewahren Sie auch eine lokale Kopie der Sicherungen, um eine schnellere Wiederherstellung zu aktivieren.

Wenn Active Directory-Papierkorb aktiviert ist, entspricht die Lebensdauer der Sicherung der **DeletedObjectLifetime** Wert oder die **TombstoneLifetime** Wert, welcher Wert kleiner ist. Weitere Informationen finden Sie unter [Active Directory Recycle Bin Step Guide](https://go.microsoft.com/fwlink/?LinkId=178657) (https://go.microsoft.com/fwlink/?LinkId=178657).

Als Alternative können Sie auch das Active Directory-Datenbank-Bereitstellungstool (Dsamain.exe) und ein Lightweight Directory Access Protocol (LDAP)-Tool, z. B. Ldp.exe oder Active Directory-Benutzer und Computer, auf die Sicherung zu identifizieren, ist des letzten abgesicherten Zustands, der die Gesamtstruktur. Das Active Directory-Datenbank Bereitstellungstool, das in Windows Server 2008 und Windows Server-Betriebssystemen enthalten ist, stellt Active Directory-Daten, die in Sicherungen oder Momentaufnahmen als LDAP-Server gespeichert ist. Ein LDAP-Tool können Sie dann um die Daten zu durchsuchen. Dieser Ansatz hat den Vorteil, dass keine Domänencontroller im Verzeichnis Verzeichnisdienst-Wiederherstellungsmodus (DSRM), überprüfen Sie den Inhalt der Sicherung von AD DS neu zu starten.

Weitere Informationen zur Verwendung von Active Directory-Datenbank bereitstellen Tool finden Sie unter der [zum Active Directory-Datenbank bereitstellen Tool schrittweise](https://technet.microsoft.com/library/cc753609\(WS.10\).aspx).

Sie können auch die **Ntdsutil Momentaufnahme** Befehl zum Erstellen von Momentaufnahmen von Active Directory-Datenbank. Durch Planen einer Aufgabe in regelmäßigen Abständen Momentaufnahmen erstellen, erhalten Sie zusätzliche Kopien der Active Directory-Datenbank im Laufe der Zeit. Diese Kopien können Sie besser erkennen, wenn der Gesamtstruktur-Fehler aufgetreten ist, und wählen Sie dann die optimale Sicherung wiederherstellen. Um Momentaufnahmen zu erstellen, verwenden Sie die Version des **Ntdsutil** , die mit Windows Server 2008 oder das Remote-Verwaltungstools (RSAT) für Windows Vista oder höher bereitgestellt wird. Das Ziel-DC kann eine beliebige Version von Windows Server ausführen. Weitere Informationen zur Verwendung der **Ntdsutil Momentaufnahme** Befehl, finden Sie unter [Momentaufnahme](https://technet.microsoft.com/library/cc731620\(WS.10\).aspx).

## <a name="determining-which-domain-controllers-to-restore"></a>Ermitteln der Domänencontroller wiederherstellen

Der Wiederherstellungsvorgang für die erleichterte Bedienung ist ein wichtiger Faktor bei der Entscheidung, welcher Domänencontroller wiederherstellen. Es wird empfohlen, um einen dedizierten Domänencontroller für jede Domäne zu erhalten, die der bevorzugte DC für eine Wiederherstellung ist. Eine dedizierte, die DC erleichtert es, zuverlässig planen und die Wiederherstellung der Gesamtstruktur ausgeführt werden, da Sie die gleiche Quellkonfiguration verwenden, die zum Ausführen verwendet wurde die Wiederherstellung Tests. Sie können Skript für die Wiederherstellung und nicht mit unterschiedlichen Konfigurationen, konkurrieren, z. B., ob der Domänencontroller Betriebsmasterfunktionen oder nicht innehat, oder, ob es ein globaler Katalogserver oder DNS-Server handelt oder nicht.

> [!NOTE]
> Obwohl es nicht empfehlenswert ist ein Halter der Masterrolle aus Gründen der Einfachheit wiederherstellen, können einige Organisationen für andere Vorteile wiederherstellen. Z. B. Wiederherstellen des RID-Masters kann hilfreich sein, die Probleme mit der Verwaltung von RIDs während der Wiederherstellungs zu vermeiden.  

Wählen Sie einen Domänencontroller, der am besten die folgenden Kriterien erfüllt:

- Einem Domänencontroller, die nicht schreibgeschützt ist. Dies ist obligatorisch.

- Einem Domänencontroller unter Windows Server 2012 als virtuelle Computer auf einem Hypervisor, der VM-Generations-ID unterstützt. Dieser Domänencontroller kann als Quelle zum Klonen verwendet werden.
- Einem Domänencontroller, die zugegriffen werden kann, entweder physisch oder in einem virtuellen Netzwerk und vorzugsweise in einem Rechenzentrum befinden. Auf diese Weise können Sie ganz einfach über das Netzwerk während der Wiederherstellung der Gesamtstruktur isolieren.
- Einem Domänencontroller, die über eine gute vollständige serversicherung verfügt. Einer gute Sicherung handelt es sich um eine Sicherung, die erfolgreich wiederhergestellt werden kann, wie viel nützliche Daten wie möglich enthält und einige Tage vor Auftreten des Fehlers erstellt wurde.
- Einem Domänencontroller, die einen Domain Name System (DNS)-Server vor Auftreten des Fehlers war. Dies spart den Zeitaufwand für den DNS neu installieren.
- Wenn Sie auch Windows-Bereitstellungsdienste verwenden, wählen Sie einen Domänencontroller, der nicht für die Verwendung der BitLocker-Netzwerkentsperrung konfiguriert ist. In diesem Fall wird BitLocker-Netzwerkentsperrung nicht unterstützt, die Sie aus einer Sicherung, während eine Wiederherstellung der Gesamtstruktur Wiederherstellen des ersten Domänencontrollers verwendet werden soll.

   BitLocker-Netzwerkentsperrung als die *nur* Schlüsselschutzvorrichtung *kann nicht* verwendet werden, auf Domänencontrollern, in dem Sie Windows-Verwaltungsinstrumentation (Windows Deployment Services, WDS) bereitgestellt haben, da dies also in einem Szenario ergibt, in denen erfordert des ersten Domänencontrollers Active Directory und WDS zum Entsperren zu arbeiten. Aber vor der Wiederherstellung des ersten Domänencontrollers Active Directory ist noch nicht verfügbar für WDS, damit es entsperren nicht möglich.

   Um festzustellen, ob es sich bei ein Domänencontroller für die BitLocker-Netzwerkentsperrung verwenden konfiguriert ist, überprüfen Sie, dass eine Netzwerkentsperrungs-Zertifikat in den folgenden Registrierungsschlüssel identifiziert wird:

   HKEY_LOCAL_MACHINESoftwarePoliciesMicrosoftSystemCertificatesFVE_NKP

Verwalten Sie Sicherheitsprozeduren, die beim Verarbeiten oder Wiederherstellen von Sicherungsdateien, die Active Directory enthalten. Die Dringlichkeit, die mit der Wiederherstellung der Gesamtstruktur kann versehentlich zu bewährten Sicherheitsmethoden abfrageparallelität führen. Weitere Informationen finden Sie im Abschnitt "Herstellen Domäne-Controller Sicherungs-und Wiederherstellungsstrategien" in [Leitfaden mit bewährten Methoden zum Absichern von Active Directory-Installationen und zuverlässig betreiben: Teil II](https://technet.microsoft.com/library/bb727066.aspx).

## <a name="identify-the-current-forest-structure-and-dc-functions"></a>Identifizieren Sie die Struktur der aktuellen Gesamtstruktur und der DC-Funktionen

Bestimmen der aktuellen Gesamtstruktur-Struktur durch alle Domänen in der Gesamtstruktur identifizieren. Stellen Sie eine Liste aller von den DCs in jeder Domäne, insbesondere die DCs, die Sicherungen und virtualisierter DCs, von denen Quelle zum Klonen werden können. Eine Liste der Domänencontroller für die Gesamtstruktur-Stammdomäne werden am wichtigsten, da Sie diese Domäne werden zuerst wiederhergestellt. Nach der Wiederherstellung der Gesamtstruktur-Stammdomäne erhalten Sie eine Liste mit den anderen Domänen, Domänencontroller und die Standorte in der Gesamtstruktur, mithilfe von Active Directory-Snap-ins.

Bereiten Sie eine Tabelle mit den Funktionen der einzelnen Domänencontroller in der Domäne vor, wie im folgenden Beispiel gezeigt. Dies hilft Ihnen die Konfiguration vor dem Ausfall der Gesamtstruktur nach der Wiederherstellung wiederherstellen.

|Name des Domänencontrollers|Betriebssystem|FSMO|GC|RODC|Sicherung|DNS|Server Core|Virtuelle Maschine|VM-GenID|  
|-------------|----------------------|----------|--------|----------|------------|---------|-----------------|--------|---------------|  
|DC_1|Windows Server 2012|Schemamaster, Domänennamenmaster|Ja|Nein|Ja|Nein|Nein|Ja|Ja|  
|DC_2|Windows Server 2012|Keine|Ja|Nein|Ja|Ja|Nein|Ja|Ja|  
|DC_3|Windows Server 2012|Infrastrukturmaster|Nein|Nein|Nein|Ja|Ja|Ja|Ja|  
|DC_4|Windows Server 2012|PDC emulator, RID Master|Ja|Nein|Nein|Nein|Nein|Ja|Nein|  
|DC_5|Windows Server 2012|Keine|Nein|Nein|Ja|Ja|Nein|Ja|Ja|  
|RODC_1|Windows Server 2008 R2|Keine|Ja|Ja|Ja|Ja|Ja|Ja|Nein|  
|RODC_2|WindowsServer 2008|Keine|Ja|Ja|Nein|Ja|Ja|Ja|Nein|  

Identifizieren Sie für jede Domäne in der Gesamtstruktur einen einzelnen beschreibbaren Domänencontroller, die über eine vertrauenswürdige Sicherung von Active Directory-Datenbank für diese Domäne verfügt. Verwenden Sie vorsichtig vor, wenn Sie einen DC wiederherzustellende Sicherung auswählen. Wenn ungefähr den Tag und die Ursache des Fehlers bekannt sind, werden im Allgemeinen empfiehlt eine Sicherung zu verwenden, die einige Tage vor diesem Datum erstellt wurde.
  
Es gibt vier backup Kandidaten, in diesem Beispiel: DC_1, DC_2, DC_4, and DC_5. Backup Kandidaten stellen Sie nur ein. Der empfohlene DC ist DC_5 aus den folgenden Gründen:  

- Es erfüllt die Anforderungen für die Verwendung als Quelle für virtualisierte Domänencontroller klonen, die, die sie die Windows Server 2012 ausgeführt wird, während ein virtueller Domänencontroller auf einem Hypervisor, die VM-Generations-ID, unterstützt ausgeführt wird, Software, die zugelassen wird, werden geklont (oder, die entfernt werden, wenn er nicht Klonen werden kann (d). Nach der Wiederherstellung wird der PDC-Emulatorrolle übernommen werden, und der Gruppe "Klonbare Domänencontroller" für die Domäne hinzugefügt werden können.  
- Es wird eine vollständige Installation von Windows Server 2012 ausgeführt. Möglich umständlicher als Ziel für die Wiederherstellung ein Domänencontrollers, der Server Core-Installation ausgeführt wird.  
- Es ist ein DNS-Server. Aus diesem Grund muss DNS nicht neu installiert werden.  

> [!NOTE]
> Da DC_5 kein globaler Katalogserver ist, hat es auch einen Vorteil, da der globale Katalog nicht nach der Wiederherstellung entfernt werden muss. Aber, und zwar unabhängig davon, ob der DC auch, dass ein globaler Katalogserver nicht ausschlaggebend ist, da ab Windows Server 2012 ist, werden alle DCs globale Katalogserver standardmäßig, und entfernen und Hinzufügen des globalen Katalogs, nachdem die Wiederherstellung wird als Teil der Gesamtstruktur empfohlen Wiederherstellung auf jeden Fall verarbeitet werden.  

## <a name="recover-the-forest-in-isolation"></a>Wiederherstellung der Gesamtstruktur isoliert

Das bevorzugte Szenario ist, alle beschreibbaren Domänencontroller vor dem ersten wiederhergestellten DC Herunterfahren in der produktionsumgebung wiederhergestellt wird. Dadurch wird sichergestellt, dass alle gefährlichen Daten nicht erneut in die wiederhergestellte Gesamtstruktur repliziert werden. Es ist besonders wichtig, um alle Betriebsmasterrolle zu schließen.  

> [!NOTE]
> Möglicherweise gibt es Fälle, in dem Verschieben des ersten Domänencontrollers, den Sie für jede Domäne mit einem isolierten Netzwerk wiederhergestellt werden, gleichzeitig werden andere Domänencontroller, um die Systemausfallzeiten zu minimieren, online bleiben möchten. Z. B. Wenn Sie über eine fehlgeschlagene schemaupgrades wiederherstellen, können Sie zu Domänencontrollern, die im Produktionsnetzwerk ausgeführt wird, während Sie die Schritte zur Wiederherstellung isoliert ausführen.

Wenn Sie virtualisierte Domänencontroller ausführen, können Sie verschieben sie mit einem virtuellen Netzwerk, das vom Produktionsnetzwerk isoliert ist, führen Sie Wiederherstellung aus. Virtualisierte Domänencontroller in einem separaten Netzwerk verschieben, bietet zwei Vorteile:  

- Wiederhergestellte Domänencontroller werden gefunden, der das Problem verhindert, die die Wiederherstellung der Gesamtstruktur verursacht hat, da sie isoliert sind.  
- Klonen von virtualisierten Domänencontroller kann, bevor sie mit dem Produktionsnetzwerk wieder hochgefahren werden in der separaten Netzwerk durchgeführt werden, sodass eine kritische Anzahl von-Domänencontrollern ausgeführt werden kann und getestet werden.

Wenn Sie Domänencontroller auf physischer Hardware ausführen, trennen Sie das Netzwerkkabel des ersten Domänencontrollers, die Sie in der Gesamtstruktur-Stammdomäne wiederherstellen möchten. Wenn möglich, trennen Sie die Netzwerkkabel von allen anderen Domänencontrollern auch. Dies verhindert DCs repliziert, wenn sie versehentlich während der Wiederherstellung der Gesamtstruktur gestartet wurden.  

Bei einer großen Gesamtstruktur, die mehrere Standorte verteilt wird, kann es schwierig sein zu garantieren, dass alle beschreibbaren Domänencontroller heruntergefahren werden. Aus diesem Grund die Wiederherstellungsschritte ausführen – z. B. das Computerkonto und das Krbtgt-Konto zusätzlich zum Metadatencleanup zurücksetzen – wurden entwickelt, um sicherzustellen, dass die wiederhergestellten beschreibbaren DCs nicht gefährlich beschreibbaren DCs replizieren (für den Fall, dass einige in noch immer online sind die Gesamtstruktur).  
  
Nur von beschreibbaren DCs offline schalten können Sie jedoch sicherstellen, dass die Replikation nicht auftritt. Aus diesem Grund sollten nach Möglichkeit, Sie remote Management-Technologie bereitstellen, mit denen Sie zum Herunterfahren und die beschreibbaren DCs physisch während der Wiederherstellung der Gesamtstruktur zu isolieren.  
  
RODCs können weiterhin ausgeführt, während beschreibbaren DCs offline sind. Kein anderer DC Änderungen direkt aus jeder RODC repliziert – vor allem für die Verwendung ohne Schema oder Container konfigurationsänderungen, sodass sie während der Wiederherstellung keine Risiko wie beschreibbare DCs darstellen. Nach allen beschreibbaren DC wiederhergestellt und online sind, sollten Sie alle in die RODCs neu erstellen.  
  
RODCs werden weiterhin Zugriff auf lokale Ressourcen zu ermöglichen, die an ihren jeweiligen Standorten zwischengespeichert werden, während der Wiederherstellungsvorgänge parallel passiert werden. Lokale Ressourcen, die nicht auf dem RODC zwischengespeichert werden müssen authentifizierungsanforderungen an einen beschreibbaren DC weitergeleitet. Diese Anforderungen schlägt fehl, da beschreibbaren DCs offline sind. Einige Vorgänge wie z. B. kennwortänderungen funktioniert auch nicht, bis Sie die beschreibbaren DCs wiederherstellen.  
  
Wenn Sie eine Hub-and-Spoke-Architektur verwenden, können Sie sich zunächst konzentrieren, bei der Wiederherstellung der beschreibbaren DCs an den Hubstandorten. Später können Sie die RODCs an Remotestandorten neu erstellen.  
  
## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der Gesamtstruktur der Active Directory - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Ausarbeiten eines Wiederherstellungsplans für die benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Gesamtstruktur des Active Directory - Ermittlung des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur-Wiederherstellung: Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - erste Wiederherstellung ausführen](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [AD-Gesamtstruktur-Wiederherstellung: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server 2003-Domänencontrollern](AD-Forest-Recovery-Windows-Server-2003.md)  
