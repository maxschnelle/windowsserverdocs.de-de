---
ms.assetid: b11f7a65-ec7b-4c11-8dc4-d7cabb54cd94
title: Problembehandlung für Active Directory-Replikationsprobleme
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: aef89bb1d57aff57b90f0eaeed67832f8778ba8c
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93068962"
---
# <a name="troubleshooting-active-directory-replication-problems"></a>Problembehandlung für Active Directory-Replikationsprobleme

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Replikationsprobleme können mehrere verschiedene Quellen haben. Beispielsweise können Domain Name System (DNS)-Probleme, Netzwerkprobleme oder Sicherheitsprobleme dazu führen, dass Active Directory Replikation fehlschlägt.

Im weiteren Verlauf dieses Themas werden Tools und eine allgemeine Methode zur Behebung Active Directory Replikations Fehlers erläutert. In den folgenden Unterthemen werden Symptome, Gründe und die Vorgehensweise zum Beheben bestimmter Replikations Fehler behandelt:

## <a name="introduction-and-resources-for-troubleshooting-active-directory-replication"></a>Einführung und Ressourcen zur Problembehandlung Active Directory Replikation

Ein eingehender oder ausgehender Replikations Fehler bewirkt, dass Active Directory Objekte, die die Replikations Topologie, den Replikations Zeitplan, Domänen Controller, Benutzer, Computer, Kenn Wörter, Sicherheitsgruppen, Gruppenmitgliedschaften und Gruppenrichtlinie darstellen, zwischen Domänen Controllern nicht Verzeichnis Inkonsistenz und Replikations Fehler führen entweder zu Betriebsfehlern oder zu inkonsistenten Ergebnissen, abhängig vom Domänen Controller, der für den Vorgang kontaktiert wird, und können die Anwendung von Gruppenrichtlinie und Zugriffs Steuerungs Berechtigungen verhindern. Active Directory Domain Services (AD DS) hängt von Netzwerk Konnektivität, Namensauflösung, Authentifizierung und Autorisierung, der Verzeichnis Datenbank, der Replikations Topologie und der Replikations-Engine ab. Wenn die Ursache eines Replikations Problems nicht sofort offensichtlich ist, müssen Sie die Ursache für viele mögliche Ursachen ermitteln, um mögliche Ursachen zu beseitigen.

Ein Benutzeroberflächen basiertes Tool zur Überwachung der Replikation und Diagnose von Fehlern finden Sie unter [Active Directory-Replikationsstatusmonitor Tool](https://www.microsoft.com/download/details.aspx?id=30005) .

Ein umfassendes Dokument, in dem beschrieben wird, wie Sie mit dem repadmin-Tool Probleme beheben können, Active Directory Replikation verfügbar ist. Informationen finden [Sie unter Überwachung und Problembehandlung Active Directory Replikation mit repadmin](https://go.microsoft.com/fwlink/?LinkId=122830).

Informationen zur Funktionsweise Active Directory Replikation finden Sie in den folgenden technischen Referenzen:

- [Technische Referenz für Active Directory Replikations Modell](https://go.microsoft.com/fwlink/?LinkId=65958)
- [Technische Referenz zur Active Directory-Replikations Topologie](https://go.microsoft.com/fwlink/?LinkId=93578)

## <a name="event-and-tool-solution-recommendations"></a>Empfehlungen zur Ereignis-und Tool Lösung

Im Idealfall wird durch die roten (Fehler) und gelben Ereignisse (Warnung) im Verzeichnisdienst-Ereignisprotokoll die bestimmte Einschränkung vorgeschlagen, die auf dem Quell-oder Zieldomänen Controller einen Replikations Fehler auslöst. Wenn in der Ereignismeldung Schritte für eine Projekt Mappe vorgeschlagen werden, führen Sie die Schritte aus, die im Ereignis beschrieben werden. Das repadmin-Tool und andere Diagnosetools bieten außerdem Informationen, die Ihnen beim Beheben von Replikations Fehlern helfen können.

Ausführliche Informationen zur Verwendung von Repadmin bei der Behandlung von Replikations Problemen finden [Sie unter Überwachung und Problembehandlung Active Directory Replikation mit repadmin](https://go.microsoft.com/fwlink/?LinkId=122830).

## <a name="ruling-out-intentional-disruptions-or-hardware-failures"></a>Ausschließen von absichtlichen Störungen oder Hardwarefehlern

Manchmal treten Replikations Fehler aufgrund von absichtlichen Störungen auf. Wenn Sie z. b. Active Directory Replikationsprobleme beheben, schließen Sie absichtliche disverbindungen und Hardwarefehler oder-Upgrades zuerst aus.

### <a name="intentional-disconnections"></a>Absichtliche Trennung von Verbindungen

Wenn Replikations Fehler von einem Domänen Controller gemeldet werden, der versucht, eine Replikation mit einem Domänen Controller durchlaufen, der in einem Stagingstandort erstellt wurde und zurzeit offline ist und seine Bereitstellung am endgültigen Produktionsstandort (einem Remote Standort, wie z. b. einer Zweigstelle) wartet, können Sie diese Replikations Fehler berücksichtigen Um zu vermeiden, dass ein Domänen Controller für erweiterte Zeiträume von der Replikations Topologie getrennt wird, sodass fortlaufende Fehler auftreten, bis der Domänen Controller wieder verbunden ist, sollten Sie diese Computer anfänglich als Mitglieds Server hinzufügen und die Methode Install From Media (IFM) zum Installieren von Active Directory Domain Services (AD DS) verwenden. Mit dem Befehlszeilen Tool Ntdsutil können Sie Installationsmedien erstellen, die Sie auf Wechselmedien (CD, DVD oder anderen Medien) speichern und an den Ziel Standort senden können. Anschließend können Sie das-Installationsmedium zum Installieren von AD DS auf den Domänen Controllern am Standort verwenden, ohne die Replikation zu verwenden.

### <a name="hardware-failures-or-upgradestitle"></a>Hardware Fehler oder-Upgrades</title>

Wenn aufgrund eines Hardwarefehlers Replikationsprobleme auftreten (z. b. ein Fehler bei einem Motherboard, einem Datenträger Subsystem oder einer Festplatte), Benachrichtigen Sie den Serverbesitzer, damit das Hardwareproblem behoben werden kann.

Regelmäßige Hardware Upgrades können auch dazu führen, dass Domänen Controller nicht mehr zur Verfügung stehen. Stellen Sie sicher, dass die Serverbesitzer über ein gutes System zur Kommunikation solcher Ausfälle verfügen.

### <a name="firewall-configuration"></a>Firewallkonfiguration

Standardmäßig erfolgen Active Directory Replikations-Remote Prozedur Aufrufe (Remote Procedure Calls, RPCs) über einen verfügbaren Port dynamisch über den RPC-Endpunkt Mapper (RPCSS) an Port 135. Stellen Sie sicher, dass die Windows-Firewall mit erweiterter Sicherheit und anderen Firewalls ordnungsgemäß konfiguriert ist, um die Replikation zuzulassen. Informationen zum Angeben des Ports für Active Directory Replikation und Port Einstellungen finden Sie [im Artikel 224196 in der Microsoft Knowledge Base](https://go.microsoft.com/fwlink/?LinkId=22578).

Informationen zu den Ports, die Active Directory Replikation verwendet, finden Sie unter [Active Directory Replikations Tools und-Einstellungen](https://go.microsoft.com/fwlink/?LinkId=123774).

Informationen zum Verwalten von Active Directory Replikation über Firewalls finden Sie unter [Active Directory Replikation über Firewalls](https://go.microsoft.com/fwlink/?LinkId=123775).

## <a name="responding-to-failure-of-an-outdated-server-running-windows-2000-server"></a>Reagieren auf Ausfälle eines veralteten Servers mit Windows 2000 Server

Wenn ein Domänen Controller unter Windows 2000 Server länger als die Anzahl der Tage in der Tombstone-Lebensdauer fehlgeschlagen ist, ist die Lösung immer identisch:

1. Verschieben Sie den Server aus dem Unternehmensnetzwerk in ein privates Netzwerk.
2. Entfernen Sie entweder das Betriebssystem Active Directory oder installieren Sie es neu.
3. Entfernen Sie die Server Metadaten aus Active Directory, damit das Server Objekt nicht wieder verwendet werden kann.

Sie können ein Skript zum Bereinigen von Server Metadaten auf den meisten Windows-Betriebssystemen verwenden. Weitere Informationen zum Verwenden dieses Skripts finden Sie unter [Remove Active Directory-Domäne Controller Metadata](https://go.microsoft.com/fwlink/?LinkID=123599).

Standardmäßig werden NTDS-Einstellungs Objekte, die gelöscht werden, für einen Zeitraum von 14 Tagen automatisch wieder hergestellt. Wenn Sie also keine Server Metadaten entfernen (verwenden Sie Ntdsutil oder das zuvor erwähnte Skript zum Durchführen der Metadatenbereinigung), werden die Server Metadaten im Verzeichnis wieder hergestellt, das die Replikation anfordert. In diesem Fall werden Fehler permanent protokolliert, weil die Replikation nicht mit dem fehlenden Domänen Controller fehlschlägt.

## <a name="root-causes"></a>Hauptursachen

Wenn Sie absichtliche Trennungen, Hardwarefehler und veraltete Windows 2000-Domänen Controller ausschließen, haben die restlichen Replikationsprobleme fast immer eine der folgenden Ursachen:

- Netzwerk Konnektivität: die Netzwerkverbindung ist möglicherweise nicht verfügbar, oder die Netzwerkeinstellungen sind nicht ordnungsgemäß konfiguriert.
- Namensauflösung: DNS-Fehlkonfigurationen sind eine häufige Ursache für Replikations Fehler.
- Authentifizierung und Autorisierung: Authentifizierungs-und Autorisierungs Probleme führen zu "Zugriff verweigert"-Fehlern, wenn ein Domänen Controller versucht, eine Verbindung zum Replikations Partner herzustellen
- Verzeichnis Datenbank (Speicher): die Verzeichnis Datenbank ist möglicherweise nicht in der Lage, Transaktionen schnell genug zu verarbeiten, um mit den Replikations Timeouts Schritt zu halten.
- Replikations-Engine: Wenn die Zeitpläne für die Replikation Zwischenstand Orten zu kurz sind, sind die Replikations Warteschlangen möglicherweise zu groß für die Verarbeitung in der Zeit, die für den ausgehenden In diesem Fall kann die Replikation einiger Änderungen unbegrenzt angehalten werden, und zwar so lange, bis die Tombstone-Lebensdauer überschritten wird.
- Replikations Topologie: Domänen Controller müssen über standortübergreifende Verknüpfungen in AD DS verfügen, die den Verbindungen mit einem WAN (Real Wide Area Network) oder VPN (virtuelles privates Netzwerk) entsprechen. Wenn Sie Objekte in AD DS für die Replikations Topologie erstellen, die von der eigentlichen Standort Topologie Ihres Netzwerks nicht unterstützt werden, schlägt die Replikation fehl, die die falsch konfigurierte Topologie erfordert.

## <a name="general-approach-to-fixing-problems"></a>Allgemeiner Ansatz zum Beheben von Problemen

Verwenden Sie den folgenden allgemeinen Ansatz, um Replikationsprobleme zu beheben:

1. Überwachen der Replikations Integrität Repadmin.exe täglich
2. Versuchen Sie, alle gemeldeten Fehler rechtzeitig mithilfe der Methoden zu beheben, die in Ereignismeldungen und in diesem Handbuch beschrieben werden. Wenn möglicherweise das Problem durch Software verursacht wird, deinstallieren Sie die Software, bevor Sie mit anderen Lösungen fortfahren.
3. Wenn das Problem, das zu einem Fehler bei der Replikation führt, von keiner bekannten Methode gelöst werden kann, entfernen Sie AD DS vom Server, und installieren Sie AD DS erneut. Weitere Informationen zum erneuten Installieren von AD DS finden Sie unter Außerbetriebsetzen [eines Domänen Controllers](https://go.microsoft.com/fwlink/?LinkId=128290).
4. Wenn AD DS nicht normal entfernt werden kann, während der Server mit dem Netzwerk verbunden ist, verwenden Sie eine der folgenden Methoden, um das Problem zu beheben:

   - Erzwingen Sie AD DS Entfernung im Verzeichnisdienst-Wiederherstellungs Modus (Directory Services Restore Mode, DSRM), bereinigen Sie Server Metadaten, und installieren Sie AD DS neu
   - Installieren Sie das Betriebssystem neu, und erstellen Sie den Domänen Controller neu.

Weitere Informationen zum Erzwingen der Entfernung von AD DS finden Sie unter [Erzwingen des Entfernens eines Domänen Controllers](https://go.microsoft.com/fwlink/?LinkId=128291).

## <a name="using-repadmin-to-retrieve-replication-statustitle"></a>Verwenden von Repadmin zum Abrufen des Replikations Status</title>

Der Replikations Status ist eine wichtige Möglichkeit zum Auswerten des Status des Verzeichnis Dienstanbieter. Wenn die Replikation ohne Fehler funktioniert, kennen Sie die Online Domänen Controller. Außerdem wissen Sie, dass die folgenden Systeme und Dienste funktionieren:


- DNS-Infrastruktur
- Kerberos-Authentifizierungsprotokoll
- Windows-Zeit Dienst (W32Time)
- Remoteprozeduraufruf (RPC)
- Netzwerkverbindungen

Verwenden Sie Repadmin, um den Replikations Status täglich zu überwachen, indem Sie einen Befehl ausführen, mit dem der Replikations Status aller Domänen Controller in der Die Prozedur generiert eine CSV-Datei, die Sie in Microsoft Excel öffnen und nach Replikations Fehlern filtern können.

Mit dem folgenden Verfahren können Sie den Replikations Status aller Domänen Controller in der Gesamtstruktur abrufen.

Anforderungen

Um dieses Verfahren auszuführen, ist mindestens die Mitgliedschaft in **Unternehmensadministratoren** oder eine entsprechende Berechtigung erforderlich.

Tools:

- Repadmin.exe
- Excel (Microsoft Office)

### <a name="to-generate-a-repadmin-showrepl-spreadsheet-for-domain-controllers"></a>So generieren Sie ein repadmin/showrepl-Arbeitsblatt für Domänen Controller

1. Öffnen Sie eine Eingabeaufforderung als Administrator: Klicken Sie im Startmenü mit der rechten Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld Benutzerkontensteuerung angezeigt wird, geben Sie bei Bedarf Anmelde Informationen für Enterprise Admins an, und klicken Sie dann auf Weiter.
2. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE: `repadmin /showrepl * /csv > showrepl.csv`
3. Öffnen Sie Excel.
4. Klicken Sie auf die Schaltfläche Office, klicken Sie auf öffnen, navigieren Sie zu showrepl.csv und klicken Sie dann auf Öffnen.
5. Blenden Sie die Spalte A und die Spalte Transporttyp wie folgt aus, oder löschen Sie Sie:
6. Wählen Sie eine Spalte aus, die Sie ausblenden oder löschen möchten.

   - Um die Spalte auszublenden, klicken Sie mit der rechten Maustaste auf die Spalte, und klicken Sie dann auf ausblenden.
   - Zum Löschen der Spalte klicken Sie mit der rechten Maustaste auf die ausgewählte Spalte, und klicken Sie dann auf Löschen.

7. Wählen Sie Zeile 1 unterhalb der Spaltenüberschrift Zeile aus. Klicken Sie auf der Registerkarte Ansicht auf Bereiche Einfrieren, und klicken Sie dann auf oberste Zeile fixieren.
8. Wählen Sie die gesamte Tabelle aus. Klicken Sie auf der Registerkarte Daten auf Filtern.
9. Klicken Sie in der Spalte Letzte Erfolgs Zeit auf den Pfeil nach unten, und klicken Sie dann auf Aufsteigend sortieren.
10. Klicken Sie in der Spalte Quell-DC auf den Pfeil nach unten, zeigen Sie auf Text Filter, und klicken Sie dann auf benutzerdefinierter Filter.
11. Klicken Sie im Dialogfeld Benutzerdefinierter AutoFilter Unterzeilen anzeigen, auf nicht enthalten. Geben Sie im angrenzenden Textfeld die Zeichenfolge <userInput>del</userInput> ein, um die Ergebnisse von gelöschten Domänen Controllern anzuzeigen.
12. Wiederholen Sie Schritt 11 für die Spalte Letzter Fehler Zeit, aber verwenden Sie den Wert ist nicht gleich, und geben Sie dann den Wert 0 ein.
13. Beheben Sie Replikations Fehler.

Für jeden Domänen Controller in der Gesamtstruktur zeigt das Arbeitsblatt den Quell Replikations Partner, den Zeitpunkt der letzten Replikation und den Zeitpunkt an, zu dem der letzte Replikations Fehler für jeden namens Kontext (Verzeichnis Partition) aufgetreten ist. Mithilfe von AutoFilter in Excel können Sie die Replikations Integrität für Arbeits Domänen Controller, nur fehlerhafte Domänen Controller oder Domänen Controller, die am wenigsten oder aktuellen sind, anzeigen, und Sie können die Replikations Partner anzeigen, die erfolgreich repliziert werden.

## <a name="replication-problems-and-resolutions"></a>Replikationsprobleme und-Lösungen

Replikationsprobleme werden in Ereignismeldungen und in verschiedenen Fehlermeldungen gemeldet, die auftreten, wenn eine Anwendung oder ein Dienst einen Vorgang startet. Diese Nachrichten werden im Idealfall von ihrer Überwachungsanwendung oder beim Abrufen des Replikations Status gesammelt.

Die meisten Replikationsprobleme werden in den Ereignismeldungen identifiziert, die im Verzeichnisdienst-Ereignisprotokoll protokolliert werden. Replikationsprobleme können auch in Form von Fehlermeldungen in der Ausgabe des Befehls <system>repadmin/showrepl</system> identifiziert werden.

### <a name="repadmin-showrepl-error-messages-that-indicate-replication-problems"></a>repadmin/showrepl Fehlermeldungen, die auf Replikationsprobleme hinweisen

Um Active Directory Replikationsprobleme zu identifizieren, verwenden Sie den Befehl <system>repadmin/showrepl</system> , wie im vorherigen Abschnitt beschrieben. In der folgenden Tabelle werden Fehlermeldungen, die von diesem Befehl generiert werden, zusammen mit den Hauptursachen der Fehler und Links zu Themen angezeigt, die Lösungen für die Fehler bereitstellen.

|Repadmin-Fehler|Grundursache|Lösung|
| --- | --- | --- |
|Die Zeit seit der letzten Replikation mit diesem Server hat die Tombstone-Lebensdauer überschritten.|Ein Domänen Controller hat die eingehende Replikation mit dem benannten Quell Domänen Controller so lange nicht bestanden, dass ein Löschvorgang, repliziert und Garbage Collection von AD DS durchgeführt wurde.|Ereignis-ID 2042: Die Replikation dieses Computers ist zu lange her|
|Keine eingehenden Nachbarn.|Wenn im Abschnitt "eingehende Nachbarn" der von Repadmin/showrepl generierten Ausgabe keine Elemente angezeigt werden, konnte der Domänen Controller keine Replikations Verknüpfungen mit einem anderen Domänen Controller herstellen.|Beheben von Verbindungsproblemen bei der Replikation (Ereignis-ID 1925)|
|Zugriff verweigert.“|Zwischen zwei Domänen Controllern ist ein Replikations Link vorhanden, aber die Replikation kann aufgrund eines Authentifizierungsfehlers nicht ordnungsgemäß ausgeführt werden.|Beheben von Problemen mit der Replikationssicherheit|
|Der letzte Versuch zum <Datum/Uhrzeit-> mit dem "Ziel Konto Name ist falsch" fehlgeschlagen.|Dieses Problem kann sich auf Konnektivitätsprobleme, DNS-oder Authentifizierungs Probleme beziehen. Wenn es sich um einen DNS-Fehler handelt, konnte der lokale Domänen Controller den Globally Unique Identifier (GUID)-basierten DNS-Namen seines Replikations Partners nicht auflösen.|Beheben von Problemen mit der DNS-Replikation (Ereignis-IDs 1925, 2087, 2088) beheben von Replikations Sicherheitsproblemen Beheben von Problemen 1925 bei der Replikation|
|LDAP-Fehler 49.|Das Domänen Controller-Computer Konto ist möglicherweise nicht mit dem Schlüsselverteilungscenter (KDC) synchronisiert.|Beheben von Problemen mit der Replikationssicherheit|
|Die LDAP-Verbindung zum lokalen Host kann nicht geöffnet werden.|Vom Verwaltungs Tool konnte keine Verbindung mit AD DS hergestellt werden.|Beheben von DNS-Lookup-Problemen bei der Replikation (Ereignis-IDs 1925, 2087, 2088)|
|Active Directory Replikation wurde vorzeitig entfernt.|Der Fortschritt der eingehenden Replikation wurde durch eine Replikations Anforderung mit höherer Priorität unterbrochen, z. b. eine Anforderung, die manuell mit dem Befehl repadmin/Sync generiert wurde.|Warten Sie, bis die Replikation beendet ist. Diese Informations Meldung gibt den normalen Vorgang an.|
|Die Replikation wurde gesendet und wartet.| Der Domänen Controller hat eine Replikations Anforderung gepostet und wartet auf eine Antwort. Die Replikation wird von dieser Quelle ausgeführt.|Warten Sie, bis die Replikation beendet ist. Diese Informations Meldung gibt den normalen Vorgang an.|

In der folgenden Tabelle werden häufige Ereignisse aufgelistet, die auf Probleme mit Active Directory Replikation hinweisen können, sowie die Hauptursachen der Probleme und Links zu Themen, die Lösungen für die Probleme bereitstellen.

|Ereignis-ID und Quelle|Grundursache|Lösung|
| --- | --- | --- |
|1311 NTDS-KCC|Die Replikations Konfigurationsinformationen in AD DS entsprechen nicht exakt der physischen Topologie des Netzwerks.|Beheben von Topologieproblemen bei der Replikation (Ereignis-ID 1311)|
|1388 NTDS-Replikation|Strikte Replikations Konsistenz ist nicht wirksam, und ein veraltetes Objekt wurde auf dem Domänen Controller repliziert.|Beheben von Problemen bei der Replikation fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)|
|1925 NTDS-KCC|Der Versuch, einen Replikations Link für eine beschreibbare Verzeichnis Partition festzulegen, ist fehlgeschlagen. Dieses Ereignis kann je nach Fehler verschiedene Gründe haben.| Beheben von Konnektivitätsproblemen (Ereignis-ID 1925) beheben von Problemen mit der DNS-Suche (Ereignis-IDs 1925, 2087, 2088)|
|1988 NTDS-Replikation|Der lokale Domänen Controller hat versucht, ein Objekt von einem Quell Domänen Controller zu replizieren, der nicht auf dem lokalen Domänen Controller vorhanden ist, weil er möglicherweise gelöscht und bereits in die Garbage Collection aufgenommen wurde. Die Replikation wird für diese Verzeichnis Partition mit diesem Partner nicht fortgesetzt, bis die Situation behoben ist.|Beheben von Problemen bei der Replikation fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)|
|2042 NTDS-Replikation|Bei diesem Partner ist keine Replikation für eine Tombstone-Lebensdauer aufgetreten, und die Replikation kann nicht fortgesetzt werden|Beheben von Problemen bei der Replikation fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)|
|2087 NTDS-Replikation|Der DNS-Hostname des Quell Domänen Controllers konnte von AD DS nicht in eine IP-Adresse aufgelöst werden, und die Replikation ist fehlgeschlagen.|Beheben von DNS-Lookup-Problemen bei der Replikation (Ereignis-IDs 1925, 2087, 2088)|
|2088 NTDS-Replikation |Der DNS-Hostname des Quell Domänen Controllers konnte AD DS nicht in eine IP-Adresse aufgelöst werden, aber die Replikation war erfolgreich.|Beheben von DNS-Lookup-Problemen bei der Replikation (Ereignis-IDs 1925, 2087, 2088)|
|5805 net-Anmeldung|Ein Computer Konto konnte nicht authentifiziert werden. Dies wird normalerweise durch mehrere Instanzen desselben Computer namens oder durch den Computernamen verursacht, der nicht auf jeden Domänen Controller repliziert wird.|Beheben von Problemen mit der Replikationssicherheit|

Weitere Informationen zu den Replikations Konzepten finden Sie unter [Active Directory Replikations Technologien](https://go.microsoft.com/fwlink/?LinkId=41950).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen, einschließlich der für Fehlercodes spezifischen Support Artikeln, finden Sie im Artikel zur Problembehandlung allgemeiner [Active Directory Replikations Fehler](https://support.microsoft.com/help/3108513) .
