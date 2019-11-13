---
title: 'AD-Gesamtstruktur Wiederherstellung: Bestimmen der Wiederherstellung der Gesamtstruktur'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: d604efded5b6a2ff3911a92f52817498f43c9933
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369168"
---
# <a name="determine-how-to-recover-the-forest"></a>Festlegen der Wiederherstellung der Gesamtstruktur

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Zum Wiederherstellen einer gesamten Active Directory Gesamtstruktur wird entweder die Wiederherstellung aus einer Sicherung oder die erneute Installation Active Directory Domain Services (AD DS) auf jedem Domänen Controller (DC) in der Gesamtstruktur bereitgestellt. Durch das Wiederherstellen der Gesamtstruktur wird jede Domäne in der Gesamtstruktur zum Zeitpunkt der letzten vertrauenswürdigen Sicherung wieder hergestellt. Folglich führt der Wiederherstellungs Vorgang zu einem Verlust von mindestens den folgenden Active Directory Daten:

- Alle Objekte (z. b. Benutzer und Computer), die nach der letzten vertrauenswürdigen Sicherung hinzugefügt wurden
- Alle Updates, die seit der letzten vertrauenswürdigen Sicherung an vorhandenen Objekten vorgenommen wurden
- Alle Änderungen, die seit der letzten vertrauenswürdigen Sicherung an der Konfigurations Partition oder der Schema Partition in AD DS vorgenommen wurden (z. b. Schema Änderungen).

Für jede Domäne in der Gesamtstruktur muss das Kennwort eines Domänen Administrator Kontos bekannt sein. Vorzugsweise ist dies das Kennwort des integrierten Administrator Kontos. Außerdem müssen Sie das DSRM-Kennwort kennen, um eine Systemstatus Wiederherstellung eines Domänen Controllers auszuführen. Im Allgemeinen empfiehlt es sich, das Administrator Konto und den DSRM-Kenn Wort Verlauf an einem sicheren Ort zu archivieren, solange die Sicherungen gültig sind, d. h. innerhalb der Tombstone-Lebensdauer oder innerhalb der Lebensdauer des gelöschten Objekts, wenn Active Directory wieder verwendet wird. Bin ist aktiviert. Sie können das DSRM-Kennwort auch mit einem Domänen Benutzerkonto synchronisieren, um es einfacher zu merken. Weitere Informationen finden Sie im KB-Artikel [961320](https://support.microsoft.com/kb/961320). Die Synchronisierung des DSRM-Kontos muss im Vorfeld der Gesamtstruktur Wiederherstellung im Rahmen der Vorbereitung erfolgen.

> [!NOTE]
> Das Administrator Konto ist standardmäßig Mitglied der integrierten Gruppe "Administratoren", ebenso wie die Gruppen "Domänen-Admins" und "Organisations-Admins". Diese Gruppe verfügt über vollständige Kontrolle über alle DCS in der Domäne.

## <a name="determining-which-backups-to-use"></a>Bestimmen der zu verwendenden Sicherungen

Sichern Sie mindestens zwei beschreibbare DCS für jede Domäne regelmäßig, damit Sie über mehrere Sicherungen verfügen, aus denen Sie auswählen können. Beachten Sie, dass Sie die Sicherung eines schreibgeschützten Domänen Controllers (RODC) nicht verwenden können, um einen beschreibbaren DC wiederherzustellen. Es wird empfohlen, die DCS mithilfe von Sicherungen wiederherzustellen, die vor dem Auftreten des Fehlers einige Tage in Anspruch genommen wurden. Im Allgemeinen müssen Sie einen Kompromiss zwischen der Wiederherstellung und der safness der wiederhergestellten Daten bestimmen. Durch die Auswahl einer neueren Sicherung werden nützlichere Daten wieder hergestellt, das Risiko einer erneuten Einführung gefährlicher Daten in die wiederhergestellte Gesamtstruktur kann jedoch erhöht werden.

Das Wiederherstellen von Systemstatus Sicherungen ist abhängig vom ursprünglichen Betriebssystem und dem Server der Sicherung. Sie sollten z. b. keine Systemstatus Sicherung auf einem anderen Server wiederherstellen. In diesem Fall wird möglicherweise die folgende Warnung angezeigt:

"Die angegebene Sicherung ist von einem anderen Server als der aktuelle. Es wird nicht empfohlen, eine Systemstatus Wiederherstellung mit der Sicherung auf einem alternativen Server durchzuführen, da der Server möglicherweise unbrauchbar wird. Möchten Sie diese Sicherung für die Wiederherstellung des aktuellen Servers verwenden? "

Wenn Sie Active Directory auf anderer Hardware wiederherstellen müssen, erstellen Sie vollständige Server Sicherungen, und planen Sie die Durchführung einer vollständigen Server Wiederherstellung.

> [!IMPORTANT]
> Ab Windows Server 2008 wird die Wiederherstellung der Systemstatus Sicherung in einer neuen Installation von Windows Server auf neuer Hardware oder auf derselben Hardware nicht unterstützt. Wenn Windows Server auf derselben Hardware neu installiert wird, wie es später in diesem Handbuch empfohlen wird, können Sie den Domänen Controller in dieser Reihenfolge wiederherstellen:
>
> 1. Führen Sie eine vollständige Server Wiederherstellung aus, um das Betriebssystem und alle Dateien und Anwendungen wiederherzustellen.
> 2. Führen Sie eine Systemstatus Wiederherstellung mithilfe von "Wbadmin. exe" aus, um SYSVOL als autorisierend zu markieren.
>
> Weitere Informationen finden Sie im Microsoft KB-Artikel [249694](https://support.microsoft.com/kb/249694).

Wenn der Zeitpunkt des Auftretens des Fehlers unbekannt ist, untersuchen Sie weitere Informationen, um Sicherungen zu identifizieren, die den letzten sicheren Zustand der Gesamtstruktur enthalten. Diese Vorgehensweise ist weniger wünschenswert. Daher wird dringend empfohlen, dass Sie detaillierte Protokolle über den Integritäts Status von AD DS täglich aufbewahren, damit bei einem Gesamtstruktur weiten Ausfall die ungefähre Zeit des Fehlers identifiziert werden kann. Sie sollten auch eine lokale Kopie der Sicherungen aufbewahren, um eine schnellere Wiederherstellung zu ermöglichen.

Wenn Active Directory Papierkorb aktiviert ist, ist die Sicherungs Lebensdauer gleich dem **deletedObjectLifetime** -Wert oder dem **tombstoneLifetime** -Wert, je nachdem, welcher Wert kleiner ist. Weitere Informationen finden Sie unter [schrittweise Anleitung zum Active Directory Papierkorb](https://go.microsoft.com/fwlink/?LinkId=178657) (https://go.microsoft.com/fwlink/?LinkId=178657).

Als Alternative können Sie auch das Active Directory Database-Bereitstellungs Tool (Dsamain. exe) und ein Lightweight Directory Access Protocol (LDAP)-Tool (z. b. "Ldp. exe" oder Active Directory Benutzer und Computer) verwenden, um zu ermitteln, welche Sicherung den letzten sicheren Zustand des Ökosysteme. Das Active Directory-Daten Bank Bereitstellungs Tool, das in Windows Server 2008 und späteren Windows Server-Betriebssystemen enthalten ist, macht Active Directory Daten verfügbar, die in Sicherungen oder Momentaufnahmen als LDAP-Server gespeichert sind. Anschließend können Sie ein LDAP-Tool verwenden, um die Daten zu durchsuchen. Dieser Ansatz hat den Vorteil, dass Sie keinen Domänen Controller im Verzeichnisdienst-Wiederherstellungs Modus (Directory Services Restore Mode, DSRM) neu starten müssen, um den Inhalt der Sicherung AD DS zu untersuchen.

Weitere Informationen zur Verwendung des Active Directory-Daten Bank Bereitstellungs Tools finden Sie in der [schrittweisen Anleitung für die Active Directory-Daten Bank](https://technet.microsoft.com/library/cc753609\(WS.10\).aspx)Bereitstellung.

Sie können auch den Befehl **Ntdsutil snapshot** verwenden, um Momentaufnahmen der Active Directory Datenbank zu erstellen. Wenn Sie eine Aufgabe planen, in regelmäßigen Abständen Momentaufnahmen zu erstellen, können Sie im Laufe der Zeit zusätzliche Kopien der Active Directory Datenbank abrufen. Mit diesen Kopien können Sie besser erkennen, wann der Gesamtstruktur weite Fehler aufgetreten ist, und dann die beste Sicherung für die Wiederherstellung auswählen. Um Momentaufnahmen zu erstellen, verwenden Sie die Version von **Ntdsutil** , die im Lieferumfang von Windows Server 2008 oder dem Remoteserver-Verwaltungstools (RSAT) für Windows Vista oder höher enthalten ist. Der Ziel-DC kann eine beliebige Version von Windows Server ausführen. Weitere Informationen zum Verwenden des Befehls " **Ntdsutil snapshot** " finden Sie unter [Momentaufnahme](https://technet.microsoft.com/library/cc731620\(WS.10\).aspx).

## <a name="determining-which-domain-controllers-to-restore"></a>Ermitteln der wiederherzustellenden Domänen Controller

Der einfache Wiederherstellungs Vorgang ist ein wichtiger Faktor bei der Entscheidung, welcher Domänen Controller wieder hergestellt werden soll. Es wird empfohlen, einen dedizierten Domänen Controller für jede Domäne zu haben, die der bevorzugte Domänen Controller für eine Wiederherstellung ist. Mit einem dedizierten Wiederherstellungs-DC wird die Wiederherstellung der Gesamtstruktur einfacher geplant und ausgeführt, da Sie die gleiche Quell Konfiguration verwenden, die zum Ausführen von Wiederherstellungs Tests verwendet wurde. Sie können ein Skript für die Wiederherstellung erstellen und sich nicht mit verschiedenen Konfigurationen auseinandersetzen, z. b. ob der Domänen Controller Betriebs Master Rollen enthält oder nicht, oder ob es sich um einen GC-oder DNS-Server handelt.

> [!NOTE]
> Obwohl es nicht empfohlen wird, einen Besitzer der Betriebs Master Rolle im Interesse der Einfachheit wiederherzustellen, können einige Organisationen eine Wiederherstellung für andere Vorteile auswählen. Beispielsweise kann das Wiederherstellen des RID-Masters helfen, Probleme beim Verwalten von RIDs während der Wiederherstellung zu vermeiden.  

Wählen Sie einen DC aus, der am besten die folgenden Kriterien erfüllt:

- Ein Domänen Controller, der beschreibbar ist. Dies ist obligatorisch.

- Ein Domänen Controller, auf dem Windows Server 2012 als virtueller Computer auf einem Hypervisor ausgeführt wird, der die VM-generationid unterstützt. Dieser Domänen Controller kann als Quelle für das Klonen verwendet werden.
- Ein Domänen Controller, auf den zugegriffen werden kann, entweder physisch oder in einem virtuellen Netzwerk und vorzugsweise in einem Rechenzentrum. Auf diese Weise können Sie Sie während der Wiederherstellung der Gesamtstruktur problemlos vom Netzwerk isolieren.
- Ein DC, der über eine gute vollständige Server Sicherung verfügt. Eine gute Sicherung ist eine Sicherung, die erfolgreich wieder hergestellt werden kann, einige Tage vor dem Auftreten des Fehlers gedauert hat und so viele nützliche Daten wie möglich enthält.
- Ein Domänen Controller, der vor dem Auftreten eines DNS-Servers (Domain Name System) war. Dies spart die erforderliche Zeit für die Neuinstallation von DNS.
- Wenn Sie auch die Windows-Bereitstellungs Dienste verwenden, wählen Sie einen Domänen Controller, der nicht für die Verwendung der BitLocker-Netzwerk Entsperrung In diesem Fall wird die BitLocker-Netzwerk Entsperrung nicht für den ersten DC unterstützt, den Sie während einer Wiederherstellung der Gesamtstruktur aus einer Sicherung wiederherstellen.

   Die BitLocker-Netzwerk Entsperrung als *einzige* Schlüssel Schutzvorrichtung *kann nicht* auf DCS verwendet werden, auf denen Sie die Windows-Bereitstellungs Dienste (Windows Deployment Services, WDS) bereitgestellt haben, da dies zu einem Szenario führt, bei dem der erste DC erfordert, dass Active Directory und WDS funktionieren, um Bevor Sie jedoch den ersten Domänen Controller wiederherstellen, ist Active Directory für WDS noch nicht verfügbar, daher kann er nicht entsperrt werden.

   Um festzustellen, ob ein Domänen Controller für die Verwendung der BitLocker-Netzwerk Entsperrung konfiguriert ist, überprüfen Sie, ob ein Netzwerk entsperrungs Zertifikat im folgenden Registrierungsschlüssel identifiziert

   HKEY_LOCAL_MACHINESoftwarePoliciesMicrosoftSystemCertificatesFVE_NKP

Behalten Sie Sicherheitsverfahren bei der Behandlung oder Wiederherstellung von Sicherungsdateien bei, die Active Directory enthalten. Die Dringlichkeit, die die Wiederherstellung in der Gesamtstruktur begleitet, kann unbeabsichtigt zu bewährten Sicherheitsmethoden führen. Weitere Informationen finden Sie im Abschnitt "Einrichten von Sicherungs-und Wiederherstellungs Strategien für Domänen Controller" im [Leitfaden mit bewährten Methoden zum Sichern von Active Directory Installationen und alltäglichen Vorgängen: Teil II](https://technet.microsoft.com/library/bb727066.aspx).

## <a name="identify-the-current-forest-structure-and-dc-functions"></a>Identifizieren der aktuellen Gesamtstruktur Struktur und der DC-Funktionen

Bestimmen Sie die aktuelle Gesamtstruktur Struktur, indem Sie alle Domänen in der Gesamtstruktur identifizieren. Erstellen Sie eine Liste aller DCS in jeder Domäne, insbesondere die DCS mit Sicherungen und virtualisierte DCS, die als Quelle für das Klonen fungieren können. Eine Liste der DCS für die Stamm Domäne der Gesamtstruktur ist die wichtigste, da Sie diese Domäne zuerst wiederherstellen. Nachdem Sie die Stamm Domäne der Gesamtstruktur wieder hergestellt haben, können Sie eine Liste der anderen Domänen, DCS und Standorte in der Gesamtstruktur mithilfe Active Directory Snap-Ins abrufen.

Bereiten Sie eine Tabelle vor, die die Funktionen der einzelnen Domänen Controller in der Domäne anzeigt, wie im folgenden Beispiel gezeigt. Auf diese Weise können Sie nach der Wiederherstellung auf die Konfiguration der Gesamtstruktur vor dem Ausfall zurückgreifen.

|DC-Name|Betriebssystem|FSMO|GC|RODC|Sicherung|DNS|Server Core|Virtuelle Maschine|VM-GenID|  
|-------------|----------------------|----------|--------|----------|------------|---------|-----------------|--------|---------------|  
|DC_1|Windows Server 2012|Schema Master, Domänen Namen Master|Ja|nein|Ja|nein|nein|Ja|Ja|  
|DC_2|Windows Server 2012|Keine|Ja|nein|Ja|Ja|nein|Ja|Ja|  
|DC_3|Windows Server 2012|Infrastrukturmaster|nein|nein|nein|Ja|Ja|Ja|Ja|  
|DC_4|Windows Server 2012|PDC-Emulator, RID-Master|Ja|nein|nein|nein|nein|Ja|nein|  
|DC_5|Windows Server 2012|Keine|nein|nein|Ja|Ja|nein|Ja|Ja|  
|RODC_1|Windows Server 2008 R2|Keine|Ja|Ja|Ja|Ja|Ja|Ja|nein|  
|RODC_2|WindowsServer 2008|Keine|Ja|Ja|nein|Ja|Ja|Ja|nein|  

Identifizieren Sie für jede Domäne in der Gesamtstruktur einen einzelnen beschreibbaren DC, der über eine vertrauenswürdige Sicherung der Active Directory-Datenbank für diese Domäne verfügt. Gehen Sie vorsichtig vor, wenn Sie eine Sicherung zum Wiederherstellen eines Domänen Controllers auswählen. Wenn der Tag und die Ursache des Fehlers ungefähr bekannt sind, empfiehlt es sich, eine Sicherung zu verwenden, die ein paar Tage vor diesem Datum erstellt wurde.
  
In diesem Beispiel gibt es vier Sicherungs Kandidaten: DC_1, DC_2, DC_4 und DC_5. Diese Sicherungs Kandidaten stellen nur eine wieder her. Der empfohlene Domänen Controller wird aus den folgenden Gründen DC_5:  

- Sie erfüllt die Anforderungen für die Verwendung als Quelle für das Klonen virtualisierter Domänen Controller, d. h., Sie führt Windows Server 2012 als virtuellen Domänen Controller auf einem Hypervisor aus, der "VM-generationid" unterstützt, führt Software aus, die geklont werden darf (oder die entfernt werden kann, wenn Sie nicht geklont werden kann). d). Nach der Wiederherstellung wird die PDC-Emulatorrolle für diesen Server übernommen und kann der Gruppe klonbare Domänen Controller für die Domäne hinzugefügt werden.  
- Sie führt eine vollständige Installation von Windows Server 2012 aus. Ein Domänen Controller, auf dem eine Server Core-Installation ausgeführt wird, kann als Ziel für die Wiederherstellung weniger praktisch sein  
- Dabei handelt es sich um einen DNS-Server. Daher muss DNS nicht neu installiert werden.  

> [!NOTE]
> Da DC_5 kein globaler Katalogserver ist, hat er auch den Vorteil, dass der globale Katalog nach der Wiederherstellung nicht entfernt werden muss. Ob der DC auch ein globaler Katalogserver ist, ist jedoch kein entscheidender Faktor, da ab Windows Server 2012 alle DCS standardmäßig als globale Katalogserver fungieren und der globale Katalog nach der Wiederherstellung als Teil der Gesamtstruktur empfohlen wird. Wiederherstellungsprozess in jedem Fall.  

## <a name="recover-the-forest-in-isolation"></a>Wiederherstellen der Gesamtstruktur isoliert

Das bevorzugte Szenario besteht darin, Alle beschreibbaren DCS herunterzufahren, bevor der erste wiederhergestellte Domänen Controller wieder in die Produktion gebracht wird. Dadurch wird sichergestellt, dass alle gefährlichen Daten nicht wieder in die wiederhergestellte Gesamtstruktur repliziert werden. Es ist besonders wichtig, alle Inhaber der Betriebs Master Rolle zu beenden.  

> [!NOTE]
> Es gibt möglicherweise Fälle, in denen Sie den ersten Domänen Controller, den Sie für jede Domäne wiederherstellen möchten, in ein isoliertes Netzwerk verschieben, während andere DCS online bleiben, um die Ausfallzeiten des Systems zu minimieren. Wenn Sie z. b. nach einem fehlerhaften Schema Upgrade wiederherstellen, können Sie festlegen, dass die Domänen Controller im Produktionsnetzwerk ausgeführt werden, während Sie die Wiederherstellungsschritte isoliert ausführen.

Wenn Sie virtualisierte DCS ausführen, können Sie Sie in ein virtuelles Netzwerk verschieben, das vom Produktionsnetzwerk isoliert ist, in dem Sie die Wiederherstellung durchführen möchten. Das Verschieben virtualisierter DCS in ein separates Netzwerk bietet zwei Vorteile:  

- Wiederhergestellte DCS werden daran gehindert, das Problem wiederherzustellen, das die Wiederherstellung der Gesamtstruktur verursacht hat, da Sie isoliert sind.  
- Das Klonen virtualisierter Domänen Controller kann im separaten Netzwerk ausgeführt werden, sodass eine kritische Anzahl von DCS ausgeführt und getestet werden kann, bevor Sie in das Produktionsnetzwerk zurückgebracht werden.

Wenn Sie DCS auf physischer Hardware ausführen, trennen Sie das Netzwerkkabel des ersten DC, den Sie wiederherstellen möchten, in der Stamm Domäne der Gesamtstruktur. Trennen Sie nach Möglichkeit auch die Netzwerkkabel aller anderen DCS. Dadurch wird verhindert, dass DCS replizieren, wenn Sie versehentlich während des Wiederherstellungsprozesses der Gesamtstruktur gestartet werden.  

In einer großen Gesamtstruktur, die über mehrere Standorte verteilt ist, kann es schwierig sein, sicherzustellen, dass alle beschreibbaren DCS heruntergefahren werden. Aus diesem Grund sind die Wiederherstellungsschritte – z. b. das Zurücksetzen des Computer Kontos und des krbtgt-Kontos, zusätzlich zur Metadatenbereinigung – so konzipiert, dass sichergestellt ist, dass die wiederhergestellten beschreibbaren DCS nicht mit gefährlichen Schreib baren DCS repliziert werden (Falls einige noch online sind). Gesamtstruktur).  
  
Allerdings können Sie nur, wenn Sie schreibgeschützte DCS offline nehmen, sicherstellen, dass die Replikation nicht erfolgt. Daher sollten Sie nach Möglichkeit eine Remote Verwaltungs Technologie bereitstellen, mit der Sie die beschreibbaren DCS während der Wiederherstellung der Gesamtstruktur Herunterfahren und physisch isolieren können.  
  
RODCs können weiterhin ausgeführt werden, während beschreibbare DCS offline sind. Kein anderer Domänen Controller repliziert Alle Änderungen direkt von einem RODC – insbesondere ohne Schema-oder Konfigurations Container Änderungen – sodass Sie während der Wiederherstellung nicht dasselbe Risiko wie beschreibbare DCS darstellen. Nachdem alle beschreibbaren DCS wieder hergestellt und online geschaltet wurden, sollten Sie alle RODCs neu erstellen.  
  
RODCs erlauben weiterhin den Zugriff auf lokale Ressourcen, die auf den jeweiligen Standorten zwischengespeichert werden, während die Wiederherstellungs Vorgänge parallel ausgeführt werden. Für lokale Ressourcen, die nicht auf dem RODC zwischengespeichert werden, werden Authentifizierungsanforderungen an einen beschreibbaren Domänen Controller weitergeleitet. Diese Anforderungen schlagen fehl, da beschreibbare DCS offline sind. Einige Vorgänge, z. b. Kenn Wort Änderungen, funktionieren auch erst, nachdem Sie beschreibbare DCS wieder hergestellt haben.  
  
Wenn Sie eine Hub-und Sprachnetzwerk Architektur verwenden, können Sie sich zunächst auf die Wiederherstellung der beschreibbaren DCS in den Hub-Standorten konzentrieren. Später können Sie die RODCs an Remote Standorten neu erstellen.  
  
## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [AD-Gesamtstruktur Wiederherstellung: Entwerfen eines benutzerdefinierten Wiederherstellungs Plans](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD-Gesamtstruktur Wiederherstellung: Identifizieren des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur Wiederherstellung: Bestimmen der Wiederherstellung](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD-Gesamtstruktur Wiederherstellung: Ausführen der ersten Wiederherstellung](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)  
- [AD-Gesamtstruktur Wiederherstellung: häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur mit mehreren](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Active Directory-Gesamtstruktur Wiederherstellung mit Windows Server 2003-Domänen Controllern](AD-Forest-Recovery-Windows-Server-2003.md)  
