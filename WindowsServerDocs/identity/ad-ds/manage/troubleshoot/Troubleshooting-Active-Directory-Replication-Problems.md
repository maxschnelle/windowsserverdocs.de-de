---
ms.assetid: b11f7a65-ec7b-4c11-8dc4-d7cabb54cd94
title: Problembehandlung bei Active Directory-Replikationsproblemen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: eb93ea7cab297d70aa86b71bd5466004e47bfeaf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshooting-active-directory-replication-problems"></a>Problembehandlung bei Active Directory-Replikationsproblemen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


Active Directory-Replikationsproblemen können viele verschiedene Ursachen haben. Domain Name System (DNS) Probleme, Netzwerkprobleme oder Sicherheitsprobleme können alle z.B. Active Directory-Replikation zu Fehlern führen. 

Im weiteren Verlauf dieses Themas wird erläutert, Tools und allgemeine Methoden zum Active Directory-Replikationsfehler beheben. Eine praktische Übung, das veranschaulicht, wie Sie Active Directory-Replikationsprobleme zu beheben, finden Sie unter [TechNet Virtual Lab: Problembehandlung bei Active Directory-Replikationsfehler](https://go.microsoft.com/?linkid=9844718)

Die folgenden Unterthemen cover Symptome, Ursachen und wie bestimmte Replikationsfehler zu beheben:
   
[Beheben von Replikation Fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)](https://technet.microsoft.com/library/cc949124.aspx)
  
[Replikationssicherheit](https://technet.microsoft.com/library/cc949132.aspx)

[Beheben von DNS-Lookup Probleme bei der Replikation (Ereignis-IDs 1925, 2087, 2088)](https://technet.microsoft.com/library/cc949133.aspx)
  
[Beheben von Verbindungsproblemen bei der Replikation (Ereignis-ID 1925)](https://technet.microsoft.com/library/cc949131.aspx)
  
[Beheben von Topologieproblemen bei Replikation (Ereignis-ID 1311)](https://technet.microsoft.com/library/cc949129.aspx)
  
[Überprüfen Sie die DNS-Funktionalität zur Unterstützung der Verzeichnisreplikation](https://technet.microsoft.com/library/dd728017.aspx)
  
[Replikationsfehler kann 8614 der Active Directory nicht mit diesem Server replizieren, da die Zeit seit der letzten Replikation mit diesem Server die Tombstone-Ablaufzeit überschritten hat](https://technet.microsoft.com/library/replication-error-8614-the-active-directory-cannot-replicate-with-this-server-because-the-time-since-the-last-replication-with-this-server-has-exceeded-the-tombstone-lifetime.aspx)
     
[Replikation Fehler 8524 der DSA-Vorgang kann aufgrund einer DNS-Lookup-Problem fortfahren](https://technet.microsoft.com/library/replication-error-8524-the-dsa-operation-is-unable-to-proceed-because-of-a-dns-lookup-failure.aspx)
   
[Replikationsfehler 8456 oder 8457: der Quelle | Zielserver ist derzeit replikationsanforderungen ablehnen.](https://technet.microsoft.com/library/replication-error-8456-the-source-server-is-currently-rejecting-replication-requests-or-replication-error-8457-the-destination-server-is-currently-rejecting-replication-requests.aspx)
   
[Replikation 8453: der Replikationszugriff wurde verweigert.](https://technet.microsoft.com/library/replication-error-8453-replication-access-was-denied.aspx)
  
[Replikationsfehler 8452: der Namenskontext ist dabei, entfernt oder ist nicht vom angegebenen Server repliziert](https://technet.microsoft.com/library/replication-error-8452-the-naming-context-is-in-the-process-of-being-removed-or-is-not-replicated-from-the-specified-server.aspx)
   
[Replikationsfehler 5 wird der Zugriff verweigert](https://technet.microsoft.com/library/replication-error-5-access-is-denied.aspx)
  

      
      

  
[Replikationsfehler-2146893022 der Zielprinzipalname ist falsch](https://technet.microsoft.com/library/replication-error-2146893022-the-target-principal-name-is-incorrect.aspx)
  

      
      

  
[Replikationsfehler 1753 es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung](https://technet.microsoft.com/library/replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper.aspx)
  

      
      

  
[Replikation Fehler 1722 der RPC-Server ist nicht verfügbar](https://technet.microsoft.com/library/replication-error-1722-the-rpc-server-is-unavailable.aspx)
  

      
      

  
[Replikationsfehler 1396: Anmeldefehler. der Zielkontoname ist falsch](https://technet.microsoft.com/library/replication-error-1396-logon-failure-the-target-account-name-is-incorrect.aspx)
  

      
      

  
[Replikationsfehler 1256 das Remotesystem ist nicht verfügbar](https://technet.microsoft.com/library/replication-error-1256-the-remote-system-is-not-available.aspx)
  

      
      

  
[Replikationsfehler 1127 beim Zugriff auf die Festplatte, einem Datenträgervorgang ist auch nach wiederholten](https://technet.microsoft.com/library/replication-error-1127-while-accessing-the-hard-disk-a-disk-operation-failed-even-after-retries.aspx)
  

      
      

  
[Replikationsfehler 8451 der Replikationsvorgang ist ein Datenbankfehler aufgetreten.](https://technet.microsoft.com/library/replication-error-8451-the-replication-operation-encountered-a-database-error.aspx)
  

      
      

  
[Wurden die Replikation Fehler 8606: es nicht genügend Attribute übergeben, zum Erstellen eines Objekts](https://technet.microsoft.com/library/replication-error-8606-insufficient-attributes-were-given-to-create-an-object.aspx)
  

## <a name="introduction-and-resources-for-troubleshooting-active-directory-replication"></a>Einführung und Ressourcen zur Problembehandlung bei Active Directory-Replikation

Eingehende oder ausgehende Replikationsfehler bewirkt, dass Active Directory-Objekte, die die Replikationstopologie, Replikationszeitplan, Domänencontroller, Benutzer, Computer, Kennwörter, Sicherheitsgruppen, Gruppenmitgliedschaften und Gruppenrichtlinien inkonsistent zwischen Domänencontrollern darstellen. Directory Inkonsistenzen und Replikation Fehler dazu führen, dass betriebliche Fehler oder inkonsistenten Ergebnissen, abhängig von dem Domänencontroller, der für den Vorgang eine Verbindung hergestellt ist und zu verhindern, dass die Anwendung der Gruppenrichtlinie und Zugriffssteuerungsberechtigungen können. Active Directory-Domänendienste (AD DS) hängt davon ab, Netzwerkkonnektivität, Namensauflösung, Authentifizierung und Autorisierung, die Verzeichnisdatenbank, die Replikationstopologie und das Replikationsmodul. Wenn die Hauptursache für ein Replikationsproblem nicht sofort offensichtlich ist, muss die Ursache für viele mögliche Ursachen gibt systematische Verzicht auf mögliche Ursachen. 

Ein UI-basiertes Tool zum Überwachen der Replikation und Fehler zu diagnostizieren, finden Sie unter [Status-Tool von Active Directory-Replikation](https://www.microsoft.com/download/details.aspx?id=30005). Es gibt auch eine [praktische Übung](https://go.microsoft.com/?linkid=9844718), das veranschaulicht, wie Active Directory-Replikationsstatus und andere Tools verwenden, um Fehler zu beheben. 

Für ein Dokument, das beschreibt, wie Sie das Tool Repadmin verwenden können, um die Problembehandlung bei Active Directory ist die Replikation verfügbar. finden Sie unter [Überwachung und Problembehandlung für Active Directory-Replikation mithilfe von Repadmin](https://go.microsoft.com/fwlink/?LinkId=122830).

Informationen zur Funktionsweise der Active Directory-Replikation finden Sie unter folgenden technischen Referenzen:


- [Technische Referenz zu Active Directory-Replikation-Modell](https://go.microsoft.com/fwlink/?LinkId=65958)
- [Technische Referenz zu Active Directory-Replikationstopologie](https://go.microsoft.com/fwlink/?LinkId=93578)

## <a name="event-and-tool-solution-recommendations"></a>Ereignis und Tool-Lösung Empfehlungen

Im Idealfall empfiehlt sich, die Rot (Fehler) und Gelb (Warnung)-Ereignisse im Verzeichnisdienst-Ereignisprotokoll die bestimmte Einschränkung, die auf dem Quell- oder Zielserver Domänencontroller Replikationsfehler verursacht. Wenn die Ereignismeldung enthält Schrittefür eine Lösung vorschlägt, versuchen Sie die Schritte, die im Ereignis beschrieben werden. Das Tool Repadmin und andere Diagnoseprogramme enthalten auch Informationen, die Behebung von Replikationsfehlern hilfreich. 

Ausführliche Informationen zum Verwenden von Repadmin für die Problembehandlung bei der Replikation finden Sie unter [Überwachung und Problembehandlung für Active Directory-Replikation mithilfe von Repadmin](https://go.microsoft.com/fwlink/?LinkId=122830).

## <a name="ruling-out-intentional-disruptions-or-hardware-failures"></a>Beabsichtigt Unterbrechungen oder Hardwarefehler angewandten

Manchmal treten Replikationsfehler aufgrund von Unterbrechungen beabsichtigt. Z.B. bei der Problembehandlung von Active Directory-Replikationsproblemen auszuschließen Sie beabsichtigt Trennvorgänge und Hardwarefehlern oder Upgrades zuerst.

### <a name="intentional-disconnections"></a>Beabsichtigt Trennvorgänge

Wenn von einem Domänencontroller Replikationsfehler, die Replikation mit einem Domänencontroller versucht, die in einem staging Standort erstellt wurde und derzeit offline warten auf die Bereitstellung in der endgültigen Produktionsstandort (einem Remotestandort, z.B. einer Zweigstelle) ist gemeldet werden, können Sie diese Replikationsfehler berücksichtigen. Sollten Sie zur Vermeidung von einem Domänencontroller in der Replikationstopologie für einen längeren Zeitraum die fortlaufende Fehler verursacht werden, bis der Domänencontroller wieder verbunden ist, trennen Sie solche Computer zunächst als Mitgliedsserver hinzufügen und verwenden das Installieren von Medium (IFM)-Methode zum Installieren von Active Directory-Domänendienste (AD DS). Anwendungsverzeichnispartitionen können zum Erstellen eines Installationsmediums, die Sie auf einem Wechselmedium (CD, DVD oder andere Medien) gespeichert und an den Zielstandort ausgeliefert. Klicken Sie dann können Sie das Installationsmedium zum Installieren von AD DS auf den Domänencontrollern am Standort, ohne die Verwendung der Replikation. 

### <a name="hardware-failures-or-upgradestitle"></a>Fehler bei der Hardware oder -Upgrades</title>

Treten Probleme bei der Replikation durch Hardwarefehler (z.B. Fehler von Hauptplatine, Festplatten-Subsystem oder Festplatte), Benachrichtigen des Serverbesitzers so, dass das Hardwareproblem behoben werden kann.

Regelmäßige Hardwareupgrades können auch dazu führen, dass Domänencontroller nicht verfügbar. Stellen Sie sicher, dass der Besitzer der Server eine gute System solche Ausfälle im Voraus zu kommunizieren.

### <a name="firewall-configuration"></a>Konfiguration der Firewall

Active Directory-Replikation von Remoteprozeduraufrufen (RPCs) standardmäßig über einen der verfügbaren Ports über RPC Endpoint Mapper (RPCSS) über Port 135 dynamisch abgewickelt. Stellen Sie sicher, dass die Windows-Firewall mit erweiterter Sicherheit und zu anderen Firewalls ordnungsgemäß konfiguriert sind, um für die Replikation zu ermöglichen. Informationen zum Festlegen des Ports für die Active Directory-Replikation und Port-Einstellungen, finden Sie unter [224196 in der Microsoft Knowledge Base-Artikel](https://go.microsoft.com/fwlink/?LinkId=22578). 

Weitere Informationen zu den Ports, die Active Directory-Replikation verwendet, finden Sie unter [Einstellungen und Tools für Active Directory-Replikation](https://go.microsoft.com/fwlink/?LinkId=123774). 

Informationen zum Verwalten von Active Directory-Replikation über Firewalls finden Sie unter [Active Directory-Replikation über Firewalls](https://go.microsoft.com/fwlink/?LinkId=123775).

## <a name="responding-to-failure-of-an-outdated-server-running-windows-2000-server"></a>Reaktion auf Fehler von einem veralteten Server unter Windows2000 Server

Wenn ein Domänencontroller unter Windows2000 Server, die länger als die Anzahl der Tage in der Tombstone-Lebensdauer fehlgeschlagen ist, ist die Lösung immer gleich: 

1. Verschieben Sie den Server aus dem Unternehmensnetzwerk mit einem privaten Netzwerk.
2. Erzwungenes entfernen Sie Active Directory oder installieren Sie das Betriebssystem neu.
3. Entfernen Sie die Metadaten aus Active Directory, sodass das Serverobjekt kann nicht fortgesetzt werden. 

Sie können ein Skript verwenden, Bereinigen von Metadaten für die meisten Windows-Betriebssysteme. Informationen zum Verwenden dieses Skripts finden Sie unter [Entfernen von Active Directory Domänencontroller-Metadaten](https://go.microsoft.com/fwlink/?LinkID=123599). 

Standardmäßig werden die NTDS-Einstellungsobjekten, die gelöscht werden für einen Zeitraum von 14Tagen automatisch fortgesetzt. Aus diesem Grund, wenn Sie Metadaten nicht entfernen (verwenden Sie Ntdsutil oder das Skript aus, die bereits erwähnte Metadatenbereinigung ausführen), Metadaten des wird wiederhergestellt, in dem Verzeichnis, in dem Replikationsversuche erfolgen kann. In diesem Fall werden Fehler als Ergebnis die Unfähigkeit, mit der fehlenden Domänencontroller repliziert werden dauerhaft protokolliert.

## <a name="root-causes"></a>Hauptursachen

Wenn Sie beabsichtigt Trennvorgänge Hardwarefehlern und veraltete Windows2000-Domänencontrollern auszuschließen, haben die restliche Probleme bei der Replikation fast immer eines der folgenden Ursachen: 


- Netzwerk-Konnektivität: die Verbindung möglicherweise nicht verfügbar oder Einstellungen des Netzwerks nicht ordnungsgemäß konfiguriert sind.
- Namensauflösung: DNS-Fehlkonfigurationen sind eine häufige Ursache für Fehler bei der Replikation.
- Authentifizierung und Autorisierung: Authentifizierung und Autorisierung Probleme verursachen Fehler "Zugriff verweigert", wenn ein Domänencontroller versucht eine Verbindung mit dessen Replikationspartner.
- Directory-Datenbank (Speicher): die Verzeichnisdatenbank möglicherweise nicht um Transaktionen zu schnell genug Replikation Timeouts zu verarbeiten.
- Replikationsmodul: Wenn Zeitpläne für die standortübergreifende Replikation zu kurz, Warteschlangen Replikation möglicherweise zu groß, um in der Zeit zu verarbeiten, die durch den Zeitplan für die ausgehende Replikation erforderlich ist. In diesem Fall kann die Replikation von einigen Änderungen angehaltene Indefinitelypotentially lang genug, um die Tombstone-Lebensdauer überschreiten.
- Replikationstopologie: Domänencontroller benötigen standortübergreifende Links in AD DS, die echten wide Area Network (WAN) oder Verbindungen virtuelles privates Netzwerk (VPN) zugeordnet. Wenn Sie Objekte in AD DS für die Replikationstopologie, die von der tatsächlichen Website-Topologie des Netzwerks nicht unterstützt werden erstellen, tritt ein Fehler Replikation, die die falsch konfigurierte Topologie erforderlich sind.

## <a name="general-approach-to-fixing-problems"></a>Allgemeine Methode für die Behebung von Problemen

Verwenden Sie die folgende allgemeine Methode für die Replikationsprobleme beheben: 


1. Überwachen Sie die Replikationsintegrität täglich, oder verwenden Sie Repadmin.exe Replikationsstatus täglich abgerufen.
2. Versuchen Sie, gemeldete Fehler zeitnah mithilfe von Ereignismeldungen und diesem Handbuch beschriebenen Methoden zu beheben. Wenn Software das Problem möglicherweise verursachen, sollten Sie die deinstallieren Sie die Software, bevor Sie andere Lösungen fortsetzen.
3. Wenn das Problem, das verursacht Replikationsfehler von allen bekannten Methoden aufgelöst werden kann, entfernen Sie AD DS von dem Server, und installieren Sie AD DS. Weitere Informationen zum erneuten Installieren von AD DS finden Sie unter [Außerbetriebsetzen eines Domänencontrollers](https://go.microsoft.com/fwlink/?LinkId=128290).
4. Wenn AD DS ordnungsgemäß entfernt werden kann, während der Server mit dem Netzwerk verbunden ist, verwenden Sie eine der folgenden Methoden zum Beheben des Problems:
 

    - Erzwingen Sie Entfernen von AD DS in Directory Services-Wiederherstellungsmodus (DSRM), Bereinigen von Servermetadaten, und installieren Sie AD DS.
    - Das Betriebssystem neu installieren, und erstellen Sie den Domänencontroller neu.

Weitere Informationen zum Entfernen von AD DS erzwingen, finden Sie unter [Erzwingen des Entfernens eines Domänencontrollers](https://go.microsoft.com/fwlink/?LinkId=128291).

## <a name="using-repadmin-to-retrieve-replication-statustitle"></a>Verwenden von Repadmin zum Abrufen des Replikationsstatus</title>

Replikationsstatus ist eine wichtige Methode für Sie den Status des Verzeichnisdiensts auswerten. Wenn die Replikation fehlerfrei funktioniert, wissen Sie Domänencontroller, die online sind. Außerdem wissen Sie, dass die folgenden Systeme und Dienste arbeiten:


- DNS-Infrastruktur
- Kerberos-Authentifizierungsprotokoll
- Windows-Zeitdienst (W32time)
- Remoteprozeduraufruf (RPC)
- Netzwerkkonnektivität

Mithilfe von Repadmin zum Replikationsstatus täglich überwachen, indem Sie einen Befehl, der analysiert den Replikationsstatus aller Domänencontroller in der Gesamtstruktur ausführen. Das Verfahren generiert eine CSV-Datei, die Sie in Microsoft Excel und Filter für Replikationsfehler öffnen können.

Das folgende Verfahren können den Replikationsstatus aller Domänencontroller in der Gesamtstruktur abrufen. 
      
Anforderungen
      
Mitgliedschaft in **Organisations-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen. 

Tools: 


- Repadmin.exe 
- Excel (Microsoft Office)

### <a name="to-generate-a-repadmin-showrepl-spreadsheet-for-domain-controllers"></a>Zum Generieren einer Repadmin /showrepl Arbeitsblatt für Domänencontroller



1. Öffnen Sie ein Eingabeaufforderungsfenster als Administrator: Klicken Sie auf das Menü "Start" Maustaste auf Eingabeaufforderung, und klicken Sie dann auf als Administrator ausführen. Wenn das Dialogfeld der Benutzerkontensteuerung angezeigt wird, Anmeldeinformationen Sie Organisations-Admins, falls erforderlich, und klicken Sie dann auf Weiter. 
2. Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:`repadmin /showrepl * /csv &gt;showrepl.csv`
3. Öffnen Sie Excel.
4. Klicken Sie auf die Office-Schaltfläche, klicken Sie auf Öffnen, wechseln Sie zu showrepl.csv, und klicken Sie dann auf Öffnen.
5. Ausblenden oder Löschen von Spalte A als auch die Spalte Transporttyp wie folgt:
6. Wählen Sie eine Spalte, die Sie ausblenden oder löschen möchten.
      

    - Um die Spalte auszublenden, mit der rechten Maustaste in der Spalte, und klicken Sie dann auf ausblenden.
    - Um die Spalte zu löschen, mit der rechten Maustaste der markierten Spalte, und klicken Sie dann auf Löschen.
7. Wählen Sie Zeile 1 unterhalb der Zeile mit der Spaltenüberschrift. Klicken Sie auf der Registerkarte "Ansicht" klicken Sie auf fixieren, und klicken Sie dann auf die oberste Zeile fixieren.
8. Wählen Sie die gesamte Kalkulationstabelle. Klicken Sie auf der Registerkarte "Daten" filtern.
9. Klicken Sie in der Spalte zuletzt erfolgreich klicken Sie auf den Pfeil nach unten, und klicken Sie dann auf Aufsteigend sortieren.
10. In der Spalte Quelldomänencontroller klicken auf den Pfeil nach unten, zeigen Sie auf Textfilter, und klicken Sie dann auf Benutzerdefiniert.
11. Führen Sie im Dialogfeld Benutzerdefinierter AutoFilter unter Anzeigen Zeilen, klicken Sie auf nicht enthält. Geben Sie in das Feld neben <userInput>del</userInput> aus der Ansicht der Ergebnisse für Unterdrücken gelöscht Domänencontroller.
12. Wiederholen Sie Schritt11 für den Fehler bei der letzten Spalte, aber verwenden Sie der Wert nicht entspricht, und geben Sie den Wert 0.
13. Fehler bei der Replikation zu beheben.

Für jeden Domänencontroller in der Gesamtstruktur, die Kalkulationstabelle Quellreplikationspartner, zeigt die Zeit, dass die Replikation zuletzt aufgetreten ist, und die Uhrzeit für jedes Namenskontext (Verzeichnispartition) der letzten Replikationsfehler aufgetreten ist. Autofilter in Excel verwenden, sehen Sie die Replikationsintegrität für die Arbeit von Domänencontrollern nur Fehler nur Domänencontroller oder Domänencontroller, auf denen mindestens oder die meisten aktuellen sind, und sehen Sie die Replikationspartner, die erfolgreich repliziert werden.

## <a name="replication-problems-and-resolutions"></a>Probleme bei der Replikation und Auflösungen
    
Probleme bei der Replikation werden angezeigt, in Nachrichten und verschiedene Fehlermeldungen, die auftreten, wenn eine Anwendung oder ein Dienst, einen Vorgang versucht. Im Idealfall werden diese Nachrichten erfasst, von der Überwachung Anwendung oder beim Abrufen des Replikationsstatus.

Die meisten Probleme bei der Replikation werden in der Ereignismeldungen identifiziert, die im Verzeichnisdienst-Ereignisprotokoll protokolliert werden. Probleme bei der Replikation möglicherweise auch in Form von Fehlermeldungen in der Ausgabe des identifiziert werden die <system>Repadmin/showrepl</system> Befehl. 

### <a name="repadmin-showrepl-error-messages-that-indicate-replication-problems"></a>Repadmin /showrepl Fehlermeldungen, die Probleme bei der Replikation anzugeben.

Um Active Directory-Replikationsproblemen zu identifizieren, verwenden Sie die <system>Repadmin/showrepl</system> Befehl, wie im vorherigen Abschnittbeschrieben. Die folgende Tabelle zeigt die Fehlermeldungen, die mit diesem Befehl wird zusammen mit der Hauptursachen für die Fehler und Links zu Themen mit Lösungen für die Fehler generiert.


|Repadmin-Fehler|Ursache|Lösung|
| --- | --- | --- |
|Die Zeit seit der letzten Replikation mit diesem hat Server die Tombstone-Lebensdauer überschritten.|Ein Domänencontroller ist fehlgeschlagen, die eingehende Replikation mit dem genannten Quelldomänencontroller, die lange genug für einen Löschvorgang wurde als veraltet markiert wird, repliziert, und die Garbage Collection aus AD DS.|Ereignis-ID 2042: Es ist zu lang Replikation dieses Computers seit|
|Keine eingehenden Nachbarn.|Wenn keine Elemente im Abschnitt "Inbound Neighbors" der Ausgabe angezeigt, die von Repadmin generiert /showrepl, der Domänencontroller wurde nicht Replikationslinks mit einem anderen Domänencontroller herstellen können.|Beheben von Verbindungsproblemen bei der Replikation (Ereignis-ID 1925)| 
|Der Zugriff verweigert.|Ein Replikationslink zwischen zwei Domänencontrollern vorhanden ist, aber die Replikation kann aufgrund der Authentifizierungsfehler bei der nicht ordnungsgemäß ausgeführt werden.|Replikationssicherheit| 
|Der letzte Versuch um < Datum - Zeit > Fehler bei der die Meldung "Zielkontoname ist falsch."|Dieses Problem kann mit Konnektivität, DNS oder Authentifizierungsprobleme verknüpft werden. Ist dies ein DNS-Fehler, der lokale Domänencontroller konnte nicht aufgelöst werden die globally unique Identifier (GUID)-basierten DNS-Namen des seiner Replikationspartner.|Beheben von DNS-Lookup Probleme (Ereignis-IDs 1925, 2087, 2088) beheben von Replikation Sicherheit Replikationsprobleme Beheben von Verbindungsproblemen bei der Replikation (Ereignis-ID 1925)| 
|Fehler bei LDAP-49.|Die Domänencontrollerkonto möglicherweise nicht mit den Key Distribution Center (KDC) synchronisiert werden.|Replikationssicherheit| 
|LDAP-Verbindung zum lokalen Host kann nicht geöffnet werden.|Das Verwaltungstool konnte keine Verbindung mit AD DS.|Beheben von DNS-Lookup Probleme bei der Replikation (Ereignis-IDs 1925, 2087, 2088)| 
|Active Directory-Replikation wurde unterbrochen.|Der Fortschritt der eingehenden Replikation wurde durch eine höhere Priorität replikationsanforderung, z.B. die Anforderung unterbrochen, die mit dem Befehl Repadmin, /sync manuell erstellt wurde.|Warten Sie, bis die Replikation abgeschlossen ist. Diese informationsmeldung gibt Normalbetrieb an.| 
|Replikation wurde übermittelt und warten.| Der Domänencontroller eine Replikation Anforderung und Antwort wartet. Replikation befindet sich im Status aus dieser Quelle.|Warten Sie, bis die Replikation abgeschlossen ist. Diese informationsmeldung gibt Normalbetrieb an.| 

Die folgende Tabelle enthält allgemeine Ereignisse, die auf Probleme mit Active Directory hinweisen Replikation sowie den Stamm der Probleme sowie Links zu Themen mit Lösungen für die Probleme verursacht. 

|Ereignis-ID und die Quelle|Ursache|Lösung|
| --- | --- | --- | 
|1311 NTDS KCC|Die Replikation Konfigurationsinformationen in AD DS wird die physische Topologie des Netzwerks nicht genau wider.|Beheben von Topologieproblemen bei Replikation (Ereignis-ID 1311)| 
|1388 NTDS-Replikation|Strenge Replikationskonsistenz ist nicht aktiv, und ein veraltetes Objekt an den Domänencontroller repliziert wurde.|Beheben von Replikation Fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)|
|1925 NTDS KCC|Fehler beim Herstellen ein Replikationslinks für eine schreibbare Verzeichnispartition. Dieses Ereignis kann je nach Fehler verschiedene Ursachen haben.| Beheben von Verbindungsproblemen Probleme (Ereignis-ID 1925) beheben von Replikation DNS-Lookup bei der Replikation (Ereignis-IDs 1925, 2087, 2088)| 
|1988 NTDS-Replikation|Der lokale Domänencontroller hat versucht, ein Objekt aus einem Quelldomänencontroller repliziert werden, die nicht auf dem lokalen Domänencontroller vorhanden ist, weil es möglicherweise gelöscht und bereits Garbage collection. Replikation wird nicht für diese Verzeichnispartition mit diesen Partner fortgesetzt, bis das Problem gelöst ist.|Beheben von Replikation Fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)|
|2042 NTDS-Replikation|Replikation ist nicht mit diesem Partner aufgetreten, für die Tombstone-Lebensdauer und Replikation kann nicht fortgesetzt werden.|Beheben von Replikation Fortbestehender Objekte (Ereignis-IDs 1388, 1988 2042)| 
|2087 NTDS-Replikation|AD DS konnte den DNS-Hostnamen des Quell-Domänencontroller eine IP-Adresse und ein Fehler bei der Replikation nicht aufgelöst werden.|Beheben von DNS-Lookup Probleme bei der Replikation (Ereignis-IDs 1925, 2087, 2088)| 
|2088 NTDS-Replikation |AD DS konnte den DNS-Hostnamen des Quell-Domänencontroller eine IP-Adresse, aber die Replikation erfolgreich nicht aufgelöst werden.|Beheben von DNS-Lookup Probleme bei der Replikation (Ereignis-IDs 1925, 2087, 2088)|
|Der Anmeldedienst 5805|Ein Computerkonto konnte nicht authentifizieren, die in der Regel von mehreren Instanzen desselben Computernamens oder der Computername nicht auf alle Domänencontroller repliziert verursacht.|Replikationssicherheit| 

Weitere Informationen zu Konzepten der Replikation finden Sie unter [Active Directory-Replikation Technologien](https://go.microsoft.com/fwlink/?LinkId=41950).
  
