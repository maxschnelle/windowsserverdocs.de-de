---
ms.assetid: b11f7a65-ec7b-4c11-8dc4-d7cabb54cd94
title: Problembehandlung für Active Directory-Replikationsprobleme
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ffc0933f70a2ab518c575a944efdac4c2dcd6a1a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869421"
---
# <a name="troubleshooting-active-directory-replication-problems"></a>Problembehandlung für Active Directory-Replikationsprobleme

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory-Replikationsproblemen können viele verschiedene Ursachen haben. Beispielsweise können Probleme, Netzwerkprobleme oder Sicherheitsprobleme Domain Name System (DNS) alle Active Directory zu Replikationsfehlern führen. 

Im weiteren Verlauf dieses Themas wird erläutert, Tools und eine allgemeine Methode für die Active Directory-Replikationsfehler zu beheben. In den folgenden Unterthemen behandeln Symptome, Ursachen und wie Sie bestimmten Replikations-Fehler beheben:

## <a name="introduction-and-resources-for-troubleshooting-active-directory-replication"></a>Einführung und Ressourcen zur Problembehandlung von Active Directory-Replikation

Eingehende oder ausgehende Replikationsfehler bewirkt, dass Active Directory-Objekte, die die Replikationstopologie, Replikationszeitplan, Domänencontroller, Benutzer, Computer, Kennwörter, Sicherheitsgruppen, Gruppenmitgliedschaften und Gruppenrichtlinien inkonsistent sind darstellen. zwischen Domänencontrollern. Verzeichnisfehler Inkonsistenz und Replikation dazu führen, dass entweder Betriebsfehler oder inkonsistente Ergebnisse, je nach dem Domänencontroller, der für den Vorgang, kontaktiert wird und verhindert, dass die Anwendung der Gruppenrichtlinie und Zugriffssteuerungsberechtigungen können. Active Directory-Domänendienste (AD DS) hängt davon ab, über eine Netzwerkverbindung, namensauflösung, Authentifizierung und Autorisierung, die Directory-Datenbank, die Replikationstopologie und die Replikations-Engine. Wenn die Ursache eines Problems Replikation nicht sofort ersichtlich ist, ist das Ermitteln der Ursache für viele möglichen Ursachen systematische Beseitigung der wahrscheinlichen Ursachen erforderlich.

Eine UI-basiertes Tool zur Replikation überwachen und Diagnostizieren von Fehlern, finden Sie unter [Status-Tool von Active Directory-Replikation](https://www.microsoft.com/download/details.aspx?id=30005)

Für ein umfassendes Dokument, das beschreibt, wie Sie das Repadmin-Tool verwenden können, um die Problembehandlung für Active Directory ist die Replikation verfügbar. finden Sie unter [Überwachung und Problembehandlung der Active Directory-Replikation mithilfe von Repadmin](https://go.microsoft.com/fwlink/?LinkId=122830).

Informationen zur Funktionsweise der Active Directory-Replikation finden Sie unter den folgenden technischen Dokumentationen:

- [Technische Referenz zu Active Directory-Replikation-Modell](https://go.microsoft.com/fwlink/?LinkId=65958)
- [Technische Referenz für den Active Directory-Replikationstopologie](https://go.microsoft.com/fwlink/?LinkId=93578)

## <a name="event-and-tool-solution-recommendations"></a>Empfehlungen für die Lösung von Ereignis und Tools

Im Idealfall empfiehlt es sich bei der Rot (Fehler) und Gelb (Warnung) Ereignisse im Verzeichnisdienst-Ereignisprotokoll um die bestimmte Einschränkung, die auf dem Quell- oder Zielschema Domänencontroller Replikationsfehler verursacht. Wenn Schritte für eine Lösung in der ereignismeldung wird bereits vermuten lässt, versuchen Sie die Schritte, die in das Ereignis beschrieben werden. Das Repadmin-Tool und für andere Diagnosetools bieten auch Informationen, mit denen Sie Replikationsfehler beheben kann. 

Ausführliche Informationen zur Verwendung von Repadmin für die Behandlung von Problemen bei der Replikation finden Sie unter [Überwachung und Problembehandlung der Active Directory-Replikation mithilfe von Repadmin](https://go.microsoft.com/fwlink/?LinkId=122830).

## <a name="ruling-out-intentional-disruptions-or-hardware-failures"></a>Absichtliche Unterbrechungen oder Hardwarefehler ermöglichen

Manchmal treten Replikationsfehler aufgrund absichtliche Unterbrechungen. Z. B. bei der Problembehebung für Active Directory-Replikationsproblemen auszuschließen Sie, beabsichtigt Trennvorgänge und Hardwarefehlern oder Upgrades zunächst.

### <a name="intentional-disconnections"></a>Beabsichtigt Trennvorgänge

Wenn von einem Domänencontroller, die versucht, die Replikation mit einem Domänencontroller, die auf einer staging-Website erstellt wurde, und ist zurzeit offline. Warten auf die Bereitstellung der endgültigen Produktionsstandort (eine remote-standortsystemserver, z. B. einer Zweigstelle, Replikationsfehler gemeldet werden ), tragen, können Sie für diesen Replikationsfehler. Um zu vermeiden, trennen einen Domänencontroller in der Replikationstopologie für längere Zeiträume, die fortlaufende Fehler verursacht, bis der Domänencontroller wiederhergestellt ist, erwägen Sie, solche Computer zunächst als Mitgliedsserver hinzufügen, und verwenden Install from Media ( IFM)-Methode zum Installieren von Active Directory Domain Services (AD DS). Sie können, dass des Befehlszeilenprogramms Ntdsutil-Installationsmedien zu erstellen, die Sie speichern auf Wechselmedien (CD, DVD oder anderen Medien) und an den Zielstandort senden. Anschließend können Sie das Installationsmedium verwenden, zum Installieren von AD DS auf den Domänencontrollern am Standort, ohne die Verwendung der Replikation. 

### <a name="hardware-failures-or-upgradestitle"></a>Hardwarefehler oder -upgrades</title>

Treten Probleme bei der Replikation durch Hardwarefehler (z. B. Fehler eines Hauptplatine, Festplatten-Subsystem oder Festplatte), benachrichtigen Sie den Besitzer des Servers, damit Sie das Hardwareproblem aufgelöst werden kann.

Regelmäßige Hardwareupgrades können ebenfalls Domänencontroller außer Betrieb werden verursachen. Sicherstellen Sie, dass Ihre Server Besitzer gutes System wie Ausfälle im Voraus zu kommunizieren.

### <a name="firewall-configuration"></a>Firewallkonfiguration

Standardmäßig werden die Active Directory-Replikation Remoteprozeduraufrufe (RPCs) dynamisch über einen verfügbaren Port über die RPC Endpoint Mapper (RPCSS) an Port 135. Stellen Sie sicher, dass die Windows-Firewall mit erweiterter Sicherheit und anderer Firewalls richtig konfiguriert sind, um für die Replikation zu ermöglichen. Informationen zur Angabe des Ports für die Active Directory-Replikation und Port-Einstellungen finden Sie unter [224196 in der Microsoft Knowledge Base-Artikel](https://go.microsoft.com/fwlink/?LinkId=22578). 

Weitere Informationen zu den Ports, die Active Directory-Replikation verwendet, finden Sie unter [Active Directory-Replikation-Tools und Einstellungen](https://go.microsoft.com/fwlink/?LinkId=123774).

Informationen zum Verwalten von Active Directory-Replikation über Firewalls finden Sie unter [Active Directory-Replikation über Firewalls hinweg](https://go.microsoft.com/fwlink/?LinkId=123775).

## <a name="responding-to-failure-of-an-outdated-server-running-windows-2000-server"></a>Reagieren auf Fehler von einem veralteten-Server unter Windows 2000 Server

Wenn es sich bei ein Domänencontroller unter Windows 2000 Server länger als die Anzahl der Tage in der Tombstone-Lebensdauer ein Fehler auftritt, ist die Lösung immer gleich: 

1. Verschieben Sie den Server aus dem Unternehmensnetzwerk, mit einem privaten Netzwerk.
2. Das Entfernen von Active Directory oder das Betriebssystem neu installieren.
3. Entfernen Sie die Metadaten aus Active Directory, sodass das Server-Objekt kann nicht wieder aktiviert werden. 

Sie können ein Skript zum Bereinigen von Servermetadaten unter den meisten Windows-Betriebssystemen verwenden. Informationen zum Verwenden dieses Skripts finden Sie unter [Entfernen von Active Directory Domänencontroller-Metadaten](https://go.microsoft.com/fwlink/?LinkID=123599). 

Standardmäßig werden Objekte NTDS-Einstellungen, die gelöscht werden automatisch für einen Zeitraum von 14 Tagen wieder aktiviert. Aus diesem Grund, wenn Sie Server-Metadaten nicht entfernen (verwenden Sie Ntdsutil oder das Skript, das zuvor erwähnte Metadatenbereinigung ausführen), die Servermetadaten wird reaktiviert, in dem Verzeichnis, das Replikation versucht, die auftreten, werden aufgefordert. In diesem Fall werden Fehler als Ergebnis die Unfähigkeit, mit dem fehlenden Domänencontroller repliziert werden dauerhaft protokolliert.

## <a name="root-causes"></a>Hauptursachen

Wenn Sie absichtlich Trennvorgänge, Hardwarefehlern zu gewährleisten und veraltete Windows 2000-Domänencontroller auszuschließen, muss der Rest der Probleme bei der Replikation fast immer eine der folgenden Ursachen:

- Netzwerkkonnektivität: Die Netzwerkverbindung ist möglicherweise nicht verfügbar oder Netzwerkeinstellungen nicht ordnungsgemäß konfiguriert sind.
- Namensauflösung: DNS-Fehlkonfigurationen sind eine häufige Ursache für den Replikationsfehler.
- Authentifizierung und Autorisierung: Authentifizierung und Autorisierung Probleme verursachen Fehler "Zugriff verweigert" aus, wenn ein Domänencontroller für die Verbindung zu seinem Replikationspartner versucht.
- Directory-Datenbank (Speicher): Die Directory-Datenbank möglicherweise nicht schnell genug Verarbeitung von Transaktionen mit Timeouts für Replikation Schritt halten kann.
- Replikations-Engine: Wenn die standortübergreifende Replikationszeitpläne zu kurz sind, möglicherweise Replikationswarteschlangen zu groß, um in der Zeit zu verarbeiten, die durch den Zeitplan für die ausgehende Replikation erforderlich ist. In diesem Fall kann die Replikation von Änderungen auf unbestimmte Zeit potenziell angehaltene, so lange die Tombstone-Lebensdauer überschreiten sein.
- Die Replikationstopologie: Domänencontroller müssen standortübergreifende Links in AD DS verfügen, die für echte Fernnetz (WAN) oder virtuelles privates Netzwerk (VPN) zuordnen. Wenn Sie Objekte in AD DS für die Replikationstopologie, die von der tatsächlichen Website-Topologie Ihres Netzwerks nicht unterstützt werden erstellen, schlägt fehl Replikation, die die falsch konfigurierte Topologie ist erforderlich.

## <a name="general-approach-to-fixing-problems"></a>Allgemeiner Ansatz zum Beheben von Problemen

Verwenden Sie die folgende allgemeine Vorgehensweise für die Behebung von Problemen bei der Replikation: 

1. Überwachen Sie der Replikationsintegrität täglich, oder verwenden Sie Repadmin.exe, um Replikationsstatus täglich abzurufen.
2. Versucht, alle gemeldeten Fehler rechtzeitig aufzulösen, mithilfe der Methoden, die in die ereignismeldungen und die diesem Handbuch beschrieben werden. Wenn die Software kann das Problem verursacht werden, deinstallieren Sie die Software, bevor Sie mit anderen Lösungen fortfahren.
3. Wenn das Problem, das zum Fehlschlagen der Replikation verursacht durch bekannte Methoden aufgelöst werden kann, entfernen Sie AD DS auf dem Server, und installieren Sie AD DS. Weitere Informationen zur Neuinstallation von AD DS finden Sie unter [Außerbetriebsetzen eines Domänencontrollers](https://go.microsoft.com/fwlink/?LinkId=128290).
4. Wenn Sie AD DS normalerweise nicht entfernt werden kann, während der Server mit dem Netzwerk verbunden ist, verwenden Sie eine der folgenden Methoden zum Beheben des Problems:

   - Erzwingen Sie Entfernen von AD DS im Verzeichnis Verzeichnisdienst-Wiederherstellungsmodus (DSRM), Bereinigen von Servermetadaten, zu, und installieren Sie AD DS.
   - Das Betriebssystem neu installieren, und erstellen Sie den Domänencontroller neu.

Weitere Informationen zum Entfernen von AD DS erzwingen, finden Sie unter [Erzwingen des Entfernens eines Domänencontrollers](https://go.microsoft.com/fwlink/?LinkId=128291).

## <a name="using-repadmin-to-retrieve-replication-statustitle"></a>Verwenden von Repadmin zum Replikationsstatus abzurufen.</title>

Replikationsstatus ist eine wichtige Möglichkeit für Sie den Status des Verzeichnisdiensts zu bewerten. Wenn die Replikation fehlerfrei funktioniert, wissen Sie, die Domänencontroller, die online sind. Sie wissen auch, dass es sich bei den folgenden Systemen und Diensten arbeiten:


- DNS-Infrastruktur
- Kerberos-Authentifizierungsprotokoll
- Windows-Zeitdienst (W32time)
- Remoteprozeduraufruf (RPC)
- Netzwerkverbindungen

Verwenden von Repadmin zum Überwachen des Replikationsstatus täglich durch Ausführen eines Befehls, das bewertet, den Replikationsstatus aller Domänencontroller in Ihrer Gesamtstruktur wird. Die Prozedur generiert eine CSV-Datei, die Sie in Microsoft Excel und Filter für Replikationsfehler öffnen können.

Sie können das folgende Verfahren verwenden, den Replikationsstatus aller Domänencontroller in der Gesamtstruktur abrufen. 

Anforderungen

Um dieses Verfahren auszuführen, ist mindestens die Mitgliedschaft in **Unternehmensadministratoren** oder eine entsprechende Berechtigung erforderlich. 

Tools:

- Repadmin.exe
- Excel (Microsoft Office)

### <a name="to-generate-a-repadmin-showrepl-spreadsheet-for-domain-controllers"></a>Um ein Repadmin/showrepl Arbeitsblatt für Domänencontroller zu generieren.

1. Öffnen Sie eine Eingabeaufforderung als Administrator. Klicken Sie im Startmenü mit der rechten Maustaste auf Eingabeaufforderung, und klicken Sie dann auf Als Administrator ausführen. Wenn das Dialogfeld "Benutzerkontensteuerung" angezeigt wird, geben Sie Anmeldeinformationen der Organisations-Admins, falls erforderlich, und klicken Sie dann auf Weiter.
2. Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE: `repadmin /showrepl * /csv > showrepl.csv`
3. Öffnen Sie Excel.
4. Klicken Sie auf die Schaltfläche "Office", klicken Sie auf Öffnen, navigieren Sie zu showrepl.csv, und klicken Sie dann auf Öffnen.
5. Blenden Sie aus oder löschen Sie der Spalte A als auch der Transport-Type-Spalte, wie folgt:
6. Wählen Sie eine Spalte, die Sie ausblenden oder löschen möchten.

   - Um die Spalte auszublenden, mit der rechten Maustaste in der Spalte, und klicken Sie dann auf ausblenden.
   - Löschen Sie die Spalte, mit der rechten Maustaste in der ausgewählten Spalte, und klicken Sie dann auf Löschen.

7. Wählen Sie die Zeile "1" unter der Kopfzeile der Spalten. Auf der Registerkarte Ansicht auf fixieren und klicken Sie dann auf Zeile der obersten fixiert werden soll.
8. Wählen Sie das gesamte Arbeitsblatt ein. Klicken Sie auf "Filter", klicken Sie auf der Registerkarte "Daten".
9. Klicken Sie in der Spalte in der letzten erfolgreichen klicken Sie auf den Pfeil nach unten, und klicken Sie dann auf Aufsteigend sortieren.
10. In der Spalte Quelldomänencontroller klicken auf den Pfeil nach unten, zeigen Sie auf den Textfilter, und klicken Sie dann auf Benutzerdefinierter Filter.
11. Führen Sie im Dialogfeld Benutzerdefinierter AutoFilter unter Anzeigen von Zeilen, klicken Sie auf keinen enthält. Geben Sie in das daneben stehende Textfeld, <userInput>del</userInput> Anzeigen der Ergebnisse für ausgeschlossen gelöscht Domänencontroller.
12. Wiederholen Sie Schritt 11 für den Zeitpunkt des letzten Fehlers-Spalte, aber verwenden Sie der Wert nicht gleich, und geben Sie den Wert 0 ein.
13. Beheben Sie Replikationsfehler.

Für jeden Domänencontroller in der Gesamtstruktur, das Arbeitsblatt Quellreplikationspartner, zeigt die Zeit, dass die Replikation zuletzt auftrat, und die Zeit, die der letzten Replikationsfehler aufgetreten ist, wird für jeden Namenskontext (Verzeichnispartition). Automatisch Filtern in Excel verwenden, sehen Sie die Replikationsintegrität für die Verwendung von Domänencontrollern nur Fehler bei der nur Domänencontroller oder Domänencontroller, die der mindestens oder die meisten aktuellen sind, und sehen Sie die Replikationspartner, die repliziert werden erfolgreich.

## <a name="replication-problems-and-resolutions"></a>Probleme bei der Replikation und Lösungen

Probleme bei der Replikation werden gemeldet, in die ereignismeldungen und verschiedene Fehlermeldungen, die auftreten, wenn eine Anwendung oder ein Dienst ein Vorgang versucht. Im Idealfall werden diese Nachrichten gesammelt, indem Ihre überwachungsanwendung oder beim Abrufen des Replikationsstatus.

Die meisten Probleme bei der Replikation werden in die ereignismeldungen identifiziert, die im Verzeichnisdienst-Ereignisprotokoll protokolliert werden. Probleme bei der Replikation können auch ermittelt werden, in Form von Fehlermeldungen in der Ausgabe der <system>Repadmin/showrepl</system> Befehl.

### <a name="repadmin-showrepl-error-messages-that-indicate-replication-problems"></a>Repadmin/showrepl Fehlermeldungen, die angeben, Probleme bei der Replikation

Verwenden Sie zum Identifizieren von Active Directory-Replikationsproblemen der <system>Repadmin/showrepl</system> Befehl, wie im vorherigen Abschnitt beschrieben. Die folgende Tabelle zeigt Fehlermeldungen, die mit diesem Befehl wird zusammen mit die Ursachen für Fehler und Links zu Themen, die Lösungen für die Fehler generiert, an.

|Repadmin-Fehler|Ursache|Lösung|
| --- | --- | --- |
|Die Zeit seit der letzten Replikation dieses hat Server die Tombstone-Lebensdauer überschritten.|Ein Domänencontroller ist fehlgeschlagen, eingehenden Replikation mit dem genannten Quelldomänencontroller, die lange genug für einen Löschvorgang wurden Tombstone-Zustand, repliziert und Garbage Collection aus AD DS.|Ereignis-ID 2042: Es ist zu viel Zeit vergangen seit der letzten Replikation dieses Computers|
|Keine eingehenden Nachbarn.|Wenn keine Elemente im Abschnitt "Inbound Neighbors" der Ausgabe angezeigt, die von Repadmin/showrepl generiert wird werden, konnte der Domänencontroller nicht zu Replikationslinks mit einem anderen Domänencontroller herzustellen.|Beheben von Verbindungsproblemen bei der Replikation (Ereignis-ID 1925)| 
|Zugriff wird verweigert.|Ein Replikationslink zwischen zwei Domänencontroller vorhanden, aber die Replikation kann aufgrund eines Authentifizierungsfehlers nicht ordnungsgemäß ausgeführt werden.|Beheben von Problemen mit der Replikationssicherheit| 
|Der letzte Versuch um < Datum - Uhrzeit > Fehler bei der Meldung "Zielkontoname ist falsch."|Dieses Problem kann mit Konnektivität, DNS oder Authentifizierungsprobleme verknüpft werden. Ist dies ein DNS-Fehler, der lokale Domänencontroller konnte nicht aufgelöst werden die globally unique Identifier (GUID)-basierten DNS-Namen des dessen Replikationspartner.|Beheben Replikation DNS-Lookup Probleme (Ereignis-IDs 1925, 2087, 2088) beheben von Problemen mit der Replikationssicherheit Beheben von Verbindungsproblemen bei der Replikation (Ereignis-ID 1925)| 
|LDAP Error 49.|Die Domänencontrollerkonto möglicherweise nicht mit dem Schlüsselverteilungscenter (KDC) synchronisiert werden.|Beheben von Problemen mit der Replikationssicherheit| 
|LDAP-Verbindung zum lokalen Host kann nicht geöffnet werden.|Das Verwaltungstool konnte AD DS nicht kontaktiert werden.|Beheben von DNS-Lookupproblemen bei der Replikation (Ereignis-IDs 1925, 2087, 2088)| 
|Active Directory-Replikation wurde vorweggenommen.|Der Fortschritt der eingehenden Replikation wurde durch eine replikationsanforderung höherer Priorität, z. B. eine Anforderung unterbrochen, die manuell mit dem Befehl Repadmin Synchronisierungsvorgangs generiert wurde.|Warten Sie auf die Replikation abgeschlossen. Diese informationsmeldung gibt Normalbetrieb an.| 
|Replikation warten, gesendet.| Der Domänencontroller eine replikationsanforderung gesendet und wartet auf eine Antwort. Replikation wird ausgeführt, die von dieser Quelle.|Warten Sie auf die Replikation abgeschlossen. Diese informationsmeldung gibt Normalbetrieb an.| 

Die folgende Tabelle enthält allgemeine Ereignisse, die Probleme mit Active Directory-Replikation, zusammen mit Stamm bewirkt, dass der Probleme sowie Links zu Themen, die Lösungen für Probleme hinweisen können. 

|Ereignis-ID und Quelle|Grundursache|Lösung|
| --- | --- | --- | 
|1311 NTDS KCC|Die Konfigurationsdaten der Replikation in AD DS ist die physische Topologie des Netzwerks nicht genau wider.|Beheben von Topologieproblemen bei der Replikation (Ereignis-ID 1311)| 
|1388 NTDS-Replikation|Strenge Replikationskonsistenz ist nicht aktiv, und ein veraltetes Objekt mit dem Domänencontroller repliziert wurde.|Beheben von Problemen bei der Replikation fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)|
|1925 NTDS KCC|Fehler beim Herstellen ein Replikationslinks für eine schreibbare Verzeichnispartition. Dieses Ereignis kann verschiedene Ursachen, je nach Fehler auswirken.| Beheben Verbindungsproblemen Probleme (Ereignis-ID 1925) beheben Replication-DNS-Suche bei der Replikation (Ereignis-IDs 1925, 2087, 2088)| 
|1988 NTDS-Replikation|Der lokale Domänencontroller hat versucht, auf ein Objekt aus einem Quelldomänencontroller zu replizieren, die nicht auf dem lokalen Domänencontroller vorhanden ist, da möglicherweise wurde Sie gelöscht und bereits von der Garbage collection. Replikation wird nicht für diese Verzeichnispartition mit diesem Partner fortgesetzt, bis das Problem gelöst ist.|Beheben von Problemen bei der Replikation fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)|
|2042 NTDS-Replikation|Replikation ist nicht mit diesem Partner für die Tombstone-Lebensdauer aufgetreten, und die Replikation kann nicht fortgesetzt werden.|Beheben von Problemen bei der Replikation fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)| 
|2087 NTDS-Replikation|AD DS konnte den DNS-Hostnamen des Quelldomänencontroller in eine IP-Adresse und Fehler bei der Replikation nicht aufgelöst werden.|Beheben von DNS-Lookupproblemen bei der Replikation (Ereignis-IDs 1925, 2087, 2088)| 
|2088 NTDS-Replikation |AD DS konnte den DNS-Hostnamen der Quelldomänencontroller ein IP-Adresse, aber die Replikation erfolgreich nicht aufgelöst werden.|Beheben von DNS-Lookupproblemen bei der Replikation (Ereignis-IDs 1925, 2087, 2088)|
|Anmeldedienst 5805|Ein Computerkonto Fehler für die Authentifizierung der wird normalerweise verursacht durch entweder mehrere Instanzen denselben Computernamen oder den Namen des Computers nicht auf alle Domänencontroller repliziert werden.|Beheben von Problemen mit der Replikationssicherheit| 

Weitere Informationen über Konzepte für die Replikation finden Sie unter [Active Directory-Replikationstechnologien](https://go.microsoft.com/fwlink/?LinkId=41950).
  
## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie einschließlich der Unterstützung Artikeln-Fehlercodes für den Support-Artikel: [Gewusst wie: Problembehandlung bei allgemeinen Fehlern von Active Directory-Replikation](https://support.microsoft.com/help/3108513)
