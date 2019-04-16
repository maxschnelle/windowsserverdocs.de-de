---
ms.assetid: a7ef2fba-b05c-4be2-93b2-b9456244c3ad
title: "Überwachen von Active Directory auf Anzeichen für Sicherheitsgefährdungen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 096f2fa58b9aae53a06bf26c2107eb4cee3aa5d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="monitoring-active-directory-for-signs-of-compromise"></a>Überwachen von Active Directory auf Anzeichen für Sicherheitsgefährdungen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

*Recht Zahl fünf: externe Wachsamkeit ist der Preis für die Sicherheit.* - [10 unveränderlichen Gesetze zur Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Ein solides Ereignisprotokoll Überwachungssystem ist wichtiger Bestandteil der alle sicheren Active Directory-Entwurfs. Viele Computer Sicherheitslücken konnte früh im Ereignis erkannt werden, wenn die Opfer die entsprechende Ereignisprotokoll Überwachung und warnungsgenerierung in Kraft gesetzt. Unabhängige Berichte haben lange daraus unterstützt. Z. B. die [2009 Verizon Verletzung Bericht](http://www.verizonbusiness.com/resources/security/reports/2009_databreach_rp.pdf) Zustände:  
  
"Die scheinbare Ausfall der Überwachung und die Protokolldateien Ereignisanalyse dadurch weiterhin gewissermaßen eines. Die Möglichkeit für die Erkennung ist vorhanden. Prüfer erwähnt, dass 66 % der Opfer ausreichende Nachweise in ihre Protokolle der Verletzung ermitteln sie beim Analysieren von Grafikressourcen mehr sorgfältig waren verfügbar war."  
  
Diese mangelnde Überwachen von aktiven Ereignisprotokollen bleibt eine konsistente Schwachstelle in vielen Unternehmen Security Defense Plänen. Die [2012 Verizon Datenlecks Bericht](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf) gefunden, obwohl 85 Prozent der unterrichten Wochen bemerkt wird aufgenommen haben, 84 Prozent der Opfer Nachweis über die Verletzung in ihre Ereignisprotokolle waren.  
  
## <a name="windows-audit-policy"></a>Windows-Überwachungsrichtlinie  
Im folgenden finden Links zu den Microsoft offizielle Enterprise Support-Blog. Diese Blogs enthält Ratschläge, Richtlinien und Empfehlungen zur Überwachung hilft Ihnen bei der Verbesserung der Sicherheit Ihrer Active Directory-Infrastruktur und sind eine nützliche Ressource beim Entwerfen einer Überwachungsrichtlinie.  
  
-   [Globale Objektzugriffsüberwachung ist Magie](http://blogs.technet.com/b/askds/archive/2011/03/10/global-object-access-auditing-is-magic.aspx) -beschreibt Steuerelement sogenannte erweiterte Überwachungsrichtlinienkonfiguration, die zu Windows 7 und Windows Server 2008 R2 können Sie festlegen, welche Arten von Daten Sie möchten einfach überwachen und nicht verwalten, Skripts und auditpol.exe hinzugefügt wurde.  
  
-   [Einführung in die Überwachung von Änderungen in Windows 2008](http://blogs.technet.com/b/askds/archive/2007/10/19/introducing-auditing-changes-in-windows-2008.aspx) -Überwachung Änderungen im Windows Server 2008 eingeführt.  
  
-   [Eine tolle Tricks in Vista und 2008-Überwachung](http://blogs.technet.com/b/askds/archive/2007/11/16/cool-auditing-tricks-in-vista-and-2008.aspx) -wird erläutert, interessante Überwachungsfunktionen von Windows Vista und Windows Server 2008, die für die Behandlung von Problemen oder sehen, was passiert in Ihrer Umgebung verwendet werden können.  
  
-   [Zentrale Anlaufstelle für die Überwachung in Windows Server 2008 und Windows Vista](http://blogs.technet.com/b/askds/archive/2008/03/27/one-stop-shop-for-auditing-in-windows-server-2008-and-windows-vista.aspx) -enthält eine Zusammenstellung der Überwachung von Funktionen und Informationen, die in Windows Server 2008 und Windows Vista enthalten sind.  
  
Die folgenden Links bieten Informationen zu den Verbesserungen in Windows, die Überwachung in Windows 8 und Windows Server 2012 und Informationen zu AD DS Überwachung in Windows Server 2008.  
  
-   [What's New in Security Auditing](https://technet.microsoft.com/library/hh849638.aspx) -bietet eine Übersicht über neue Features in Windows 8 und Windows Server 2012-sicherheitsüberwachung.  
  
-   [Leitfaden für AD DS-Überwachung](https://technet.microsoft.com/library/a9c25483-89e2-4202-881c-ea8e02b4b2a5.aspx) -beschreibt die neuen Active Directory-Domänendienste (AD DS) Überwachungsfeatures in Windows Server 2008. Darüber hinaus wie folgt vor, um dieses neue Feature zu implementieren.  
  
### <a name="windows-audit-categories"></a>Windows-Überwachungskategorien  
Vor Windows Vista und Windows Server 2008 wurden in Windows nur neun Ereignisprotokoll Überwachungsrichtlinienkategorien:  
  
-   Kontoanmeldungsereignisse  
  
-   Kontoverwaltung  
  
-   Active Directory-Zugriff  
  
-   Anmeldeereignisse  
  
-   Den Zugriff auf Objekte  
  
-   Richtlinienänderung  
  
-   Verwendung von rechten  
  
-   Verfolgung von Prozessen  
  
-   Systemereignisse  
  
Diese neun herkömmliche Überwachungskategorien umfassen eine Überwachungsrichtlinie. Jede Richtlinienkategorie überwachen kann für Erfolg, Fehler oder Erfolg und Fehler aktiviert werden Ereignisse. Eine Beschreibung finden Sie im nächsten Abschnitt.  
  
#### <a name="audit-policy-category-descriptions"></a>Kategorie Richtlinienbeschreibungen überwachen  
Die Überwachungsrichtlinienkategorien aktivieren Sie die folgenden Meldungstypen im Ereignisprotokoll.  
  
##### <a name="audit-account-logon-events"></a>Anmeldeversuche überwachen  
Meldet Sie jede Instanz eines Sicherheitsprinzipals (z. B. Benutzer, Computer oder Dienstkonto), die anmeldet oder-Abmeldung bei einem Computer in der einen anderen Computer, zur Überprüfung des Kontos verwendet wird. Kontoanmeldungsereignisse werden generiert, wenn ein Domänenkonto für Sicherheit Dienstprinzipalnamen auf einem Domänencontroller authentifiziert wird. Authentifizierung eines lokalen Benutzers auf einem lokalen Computer generiert ein Anmeldeereignis, die im lokalen Sicherheitsprotokoll protokolliert wird. Keine Kontoabmeldeereignisse werden protokolliert.  
  
Diese Kategorie generiert zahlreiche "Rauschen" da Windows ständig Konten anmelden bei aufgetreten sind und auf dem lokalen Computer und Remotecomputer während der normalen Unternehmen. Dennoch sollte jedes Sicherheitsplans der Erfolg und Fehler für diese Überwachungskategorie enthalten.  
  
##### <a name="audit-account-management"></a>Kontenverwaltung  
Dieser überwachungseinstellung bestimmt, ob Verwaltung von Benutzern und Gruppen zu verfolgen. Beispielsweise sollten Benutzer und Gruppen nachverfolgt werden, wenn ein Benutzer oder das Computerkonto, einer Sicherheitsgruppe oder einer Verteilergruppe erstellt, geändert oder gelöscht wird; Wenn ein Benutzer- oder Computerkonto umbenannt, deaktiviert oder aktiviert ist; oder wenn ein Benutzer oder Computer Kennwort geändert wird. Für Benutzer oder Gruppen, die hinzugefügt oder aus anderen Gruppen entfernt, kann ein Ereignis generiert werden.  
  
##### <a name="audit-directory-service-access"></a>Überwachen des Zugriffs auf Verzeichnisdienste  

Diese Einstellung bestimmt, ob Security principal Zugriff auf Active Directory-Objekt überwacht, die einen eigenen angegebenen System-Zugriffssteuerungsliste (SACL). Diese Kategorie sollte im Allgemeinen nur auf Domänencontrollern aktiviert werden. Wenn aktiviert, generiert diese Einstellung zahlreiche "Rauschen."  
  
##### <a name="audit-logon-events"></a>Anmeldeereignisse überwachen  
Anmeldeereignisse werden generiert, wenn ein lokale Sicherheitsprinzipal auf einem lokalen Computer authentifiziert wird. Anmeldeereignisse zeichnet domänenanmeldungen, die auf dem lokalen Computer auftreten. Kontoabmeldeereignisse werden nicht generiert. Wenn aktiviert, generiert Anmeldeereignisse zahlreiche "Geräusch", aber sie sollten in jedem Sicherheitsplan Überwachung standardmäßig aktiviert werden.  
  
##### <a name="audit-object-access"></a>Objektzugriffsversuche überwachen  
Den Zugriff auf Objekte kann Ereignisse, die beim Zugriff auf die nachfolgend definierten Objekte aktiviert (z. B., geöffnet, lesen, umbenannte, gelöscht oder geschlossen) generieren. Nach die Überwachung Hauptkategorie aktiviert ist, muss der Administrator einzeln definieren, welche Objekte die Überwachung aktiviert haben. Viele Windows-System-Objekte verfügen über die Überwachung aktiviert, sodass aktivieren diese Kategorie in der Regel wird zum Generieren von Ereignissen, bevor der Administrator eine definiert wurde.  
  
Diese Kategorie ist sehr "laut" und fünf bis zehn Ereignisse für die einzelnen Objekt generiert werden. Es kann Administratoren die Erfahrung mit der Überwachung von Objekten erhalten nützliche Informationen schwierig sein. Es sollte nur aktiviert werden, wenn erforderlich.  
  
##### <a name="auditing-policy-change"></a>Überwachung der Richtlinienänderung  
Diese Einstellung bestimmt, ob alle Vorkommen von eine Änderung von Richtlinien für die Zuweisung von Benutzerrechten, Windows-Firewall-Richtlinien, Richtlinien für Vertrauensstellungen oder Änderungen an der Überwachungsrichtlinie überwachen. Diese Kategorie sollte auf allen Computern aktiviert werden. Es wird nur sehr wenig Störungen generiert.  
  
##### <a name="audit-privilege-use"></a>Rechteverwendung überwachen  

Es sind Dutzende von Benutzerrechten und-Berechtigungen in Windows (z. B. die Anmeldung als Batchauftrag und Einsetzen als Teil des Betriebssystems). Diese Einstellung bestimmt, ob jede Instanz eines Sicherheitsprinzipals zu überwachen, indem Sie eine Berechtigung oder Benutzerrecht ausübt, überwacht. Aktivieren dieses Kategorie werden zahlreiche "Geräusch", aber es kann beim Auffinden Konten von Sicherheitsprinzipalen mit erhöhten Rechten sein.  
  
##### <a name="audit-process-tracking"></a>Prozessverfolgung überwachen  
Diese Einstellung bestimmt, ob detaillierte Nachverfolgungsinformationen für Ereignisse wie z. B. programmaktivierung, prozessbeendigung, handleduplizierung und indirekter Objektzugriff Prozess zu überwachen. Es ist nützlich zum Nachverfolgen von böswilligen Benutzern und die Programme, die sie verwenden.  
  
Aktivieren der Überwachung Process Tracking eine große Anzahl von Ereignissen, also in der Regel wird festgelegt generiert **keine Überwachung**. Diese Einstellung bietet jedoch ein großer Vorteil bei einem Sicherheitsvorfall aus dem detaillierte Protokoll die Prozesse gestartet und die Zeit, die sie gestartet wurden. Für Domänencontroller und andere Infrastrukturserver Single-Rolle kann diese Kategorie sicher immer aktiviert werden. Einzelne Server generieren nicht viel prozessverfolgung Datenverkehr während der normalen ihrer Aufgaben. Sie können daher aktiviert werden, um nicht autorisierte Ereignisse erfassen, wenn sie auftreten.  
  
##### <a name="system-events-audit"></a>System-Ereignisse überwachen  

Systemereignisse ist fast generische allumfassende Kategorie, registrieren verschiedene Ereignisse, die der Computer, die Systemsicherheit oder das Sicherheitsprotokoll auswirkt. Sie enthält die Ereignisse für den Computer Herunterfahren und Neustart, Stromausfälle, Zeit ändert, Authentifizierung Paket wie, Audit Log Clearings, Identitätswechsel Probleme und zahlreiche andere allgemeine Ereignisse. Im Allgemeinen bei Aktivierung dieser Überwachungskategorie zahlreiche "Rauschen" generiert, sondern generiert ausreichend sehr nützlich, Ereignisse, dass es jemals empfehlen aktivieren es nicht schwierig ist.  
  
#### <a name="advanced-audit-policies"></a>Erweiterte Überwachungsrichtlinien  
Ab Windows Vista und Windows Server 2008, verbessert Microsoft die Möglichkeit, die Ereignisprotokolle vorgenommen werden können, indem Unterkategorien unter jeder hauptüberwachungskategorie. Die Unterkategorien ermöglichen eine wesentlich differenziertere als es andernfalls möglich, durch die Hauptkategorien Überwachung. Mithilfe von Unterkategorien können Sie nur Teile einer bestimmten Hauptkategorie aktiviert und überspringen Generieren von Ereignissen, die für die Sie keine Verwendung haben. Jede Unterkategorie der Überwachungsrichtlinie kann für Erfolg, Fehler oder Erfolg und Fehler aktiviert werden Ereignisse.  
  
Zum Auflisten aller verfügbaren Überwachung Unterkategorien, überprüfen Sie den erweiterten Überwachungsrichtlinie Container in einem Gruppenrichtlinienobjekt, oder geben Sie Folgendes an der Befehlszeile auf jedem Computer unter Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008, Windows 8, Windows 7 oder Windows Vista:  
  
**Auditpol/List / SubCategory: \ ***  
  
Um eine Liste der zurzeit konfigurierten Überwachung Unterkategorien auf einem Computer unter Windows Server 2012, Windows Server 2008 R2 oder Windows 2008 zu erhalten, geben Sie Folgendes ein:  
  
**Auditpol / Get/Category: \ ***  
  
Der folgende Screenshot zeigt ein Beispiel für auditpol.exe Auflisten der aktuellen Überwachungsrichtlinie.  
  
![Überwachung von Active Directory](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_5.gif)  
  
> [!NOTE]  
> Gruppenrichtlinien meldet den Status der Überwachungsrichtlinien für alle, aktiviert, während auditpol.exe ist nicht immer genau. Finden Sie unter [beim Abrufen der effektiven Überwachungsrichtlinie in Windows 7 und 2008 R2](http://blogs.technet.com/b/askds/archive/2011/03/11/getting-the-effective-audit-policy-in-windows-7-and-2008-r2.aspx) Weitere Details.  
  
Jede Kategorie verfügt über mehrere Unterkategorien. Es folgt eine Liste der Kategorien, ihre Unterkategorien und eine Beschreibung der Funktionen.  
  
### <a name="auditing-subcategories-descriptions"></a>Überwachung von Unterkategorien Beschreibungen  
Überwachungsrichtlinien-Unterkategorien ermöglichen die folgenden Meldungstypen Ereignisprotokoll:  
  
#### <a name="account-logon"></a>Anmeldung  
  
##### <a name="credential-validation"></a>Überprüfung der Anmeldeinformationen  
Diese Unterkategorie meldet die Ergebnisse von Validierungstests auf Anmeldeinformationen, die für eine anmeldeanforderung eines Benutzers Konto übermittelt. Diese Ereignisse treten auf dem Computer, der für die Anmeldeinformationen autoritativ ist. Für Domänenkonten ist der Domänencontroller autoritativ festzulegen, für lokale Konten der lokale Computer autoritativ.  
  
In domänenumgebungen werden die meisten der Kontoanmeldungsereignisse in das Sicherheitsprotokoll der Domänencontroller protokolliert, die für die Domänenkonten autoritativ sind. Allerdings können diese Ereignisse auf anderen Computern in der Organisation auftreten, wenn lokale Konten zur Anmeldung verwendet werden.  
  
##### <a name="kerberos-service-ticket-operations"></a>Ticketvorgänge des Kerberos-Diensts  
Diese Unterkategorie protokolliert Ereignisse, die von Kerberos-Ticket Prozesse auf dem Domänencontroller, der für das Domänenkonto generiert.  
  
##### <a name="kerberos-authentication-service"></a>Kerberos-Authentifizierungsdienst  
Diese Unterkategorie protokolliert Ereignisse, die durch die Kerberos-Authentifizierungsdienst generiert. Diese Ereignisse treten auf dem Computer, der für die Anmeldeinformationen autoritativ ist.  
  
##### <a name="other-account-logon-events"></a>Andere Kontoanmeldungsereignisse  
Diese Unterkategorie meldet die auftretenden Ereignisse in Reaktion auf Anmeldeinformationen, die für eine anmeldeanforderung eines Benutzers Konto gesendet, die nicht auf die Überprüfung der Anmeldeinformationen oder Kerberos-Tickets beziehen. Diese Ereignisse treten auf dem Computer, der für die Anmeldeinformationen autoritativ ist. Für Domänenkonten ist der Domänencontroller autoritativ festzulegen, für lokale Konten der lokale Computer autoritativ.  
  
In domänenumgebungen werden die meisten Kontoanmeldungsereignisse in das Sicherheitsprotokoll der Domänencontroller protokolliert, die für die Domänenkonten autoritativ sind. Allerdings können diese Ereignisse auf anderen Computern in der Organisation auftreten, wenn lokale Konten zur Anmeldung verwendet werden. Beispiele für können Folgendes umfassen:  
  
-   Remote Desktop Services Session Trennvorgänge  
  
-   Neue Remotedesktopdienste-Sitzungen  
  
-   Sperren und Entsperren einer Arbeitsstation  
  
-   Aufrufen eines Bildschirmschoners  
  
-   Schließen eines Bildschirmschoners  
  
-   Erkennen eines Kerberos-replay-Angriffs, in dem eine Kerberos-Anfrage mit identischen Informationen zweimal empfangen wird  
  
-   Zugriff auf einen drahtlosen Netzwerk für ein Benutzer- oder Computerkonto  
  
-   Zugriff auf einem kabelgebundenen 802. 1 x-Netzwerk für ein Benutzer- oder Computerkonto  
  
#### <a name="account-management"></a>Kontoverwaltung  
  
##### <a name="user-account-management"></a>Die Verwaltung der Benutzerkonten  
Diese Unterkategorie meldet jedes Ereignis der Verwaltung der Benutzerkonten, z. B. wenn ein Benutzerkonto erstellt, geändert oder gelöscht wird. ein Benutzerkonto wird umbenannt, deaktiviert oder aktiviert; oder ein Kennwort festlegen oder ändern. Wenn diese Einstellung für Überwachungsrichtlinien aktiviert ist, können Administratoren Ereignisse überwachen, um Schadsoftware, versehentliche und autorisierte Erstellung von Benutzerkonten zu erkennen.  
  
##### <a name="computer-account-management"></a>Computerkontoverwaltung  
Diese Unterkategorie meldet jedes Ereignis computerkontoverwaltung, z. B. wenn ein Computerkonto erstellt, geändert, gelöscht, umbenannt, deaktiviert oder aktiviert ist, an.  
  
##### <a name="security-group-management"></a>Sicherheitsgruppenverwaltung  
Diese Unterkategorie meldet jedes Ereignis für die Verwaltung von Sicherheitsgruppen, z. B. wenn eine Sicherheitsgruppe erstellt, geändert oder gelöscht wird oder wenn ein Mitglied hinzugefügt oder aus einer Sicherheitsgruppe entfernt wird. Wenn diese Einstellung für Überwachungsrichtlinien aktiviert ist, können Administratoren Ereignisse überwachen, um Schadsoftware, versehentliche und autorisierte Erstellung von Sicherheitskonten-Gruppe zu erkennen.  
  
##### <a name="distribution-group-management"></a>Verwaltung von Verteilungspunkten  
Diese Unterkategorie meldet jedes Ereignis-verteilergruppenverwaltung, z. B. wenn eine Verteilergruppe erstellt, geändert oder gelöscht wird oder wenn ein Mitglied hinzugefügt oder aus einer Verteilergruppe entfernt wird. Wenn diese Einstellung für Überwachungsrichtlinien aktiviert ist, können Administratoren Ereignisse überwachen, um Schadsoftware, versehentliche und autorisierte Erstellung von Gruppenkonten zu erkennen.  
  
##### <a name="application-group-management"></a>Anwendung Gruppenverwaltung  
Diese Unterkategorie meldet jedes Ereignis der Gruppe der anwendungsverwaltung auf einem Computer, z. B. wenn eine Anwendungsgruppe erstellt, geändert oder gelöscht wird oder wenn ein Mitglied hinzugefügt oder aus einer Anwendungsgruppe entfernt wird. Wenn diese Einstellung für Überwachungsrichtlinien aktiviert ist, können Administratoren Ereignisse zum Erkennen von Schadsoftware, versehentliche und autorisierte Erstellung von Gruppenkonten Anwendung überwachen.  
  
##### <a name="other-account-management-events"></a>Andere Kontoverwaltungsereignisse  
Diese Unterkategorie meldet andere Kontoverwaltungsereignisse.  
  
#### <a name="detailed-process-tracking"></a>Überwachung der ausführlichen Prozesses  
  
##### <a name="process-creation"></a>Erstellung von  
Diese Unterkategorie meldet die Erstellung eines Prozesses und den Namen des Benutzers oder der Anwendung, die sie erstellt haben.  
  
##### <a name="process-termination"></a>Prozess beenden  
Diese Unterkategorie berichtet, wenn ein Prozess beendet wird.  
  
##### <a name="dpapi-activity"></a>DPAPI-Aktivität  
Diese Unterkategorie meldet verschlüsseln oder entschlüsseln ruft in der Data Protection Application programming Interface (DPAPI). DPAPI wird verwendet, um geheime Informationen wie gespeicherte Kennwort und wichtige Informationen zu schützen.  
  
##### <a name="rpc-events"></a>RPC-Ereignisse  
Diese Unterkategorie Berichte Remoteprozeduraufruf (RPC) Verbindungsereignisse.  
  
#### <a name="directory-service-access"></a>Active Directory-Zugriff  
  
##### <a name="directory-service-access"></a>Active Directory-Zugriff  
Diese Unterkategorie berichtet, wenn ein AD DS-Objekt zugegriffen wird. Nur Objekte mit konfigurierten SACLs verursachen Überwachungsereignisse generiert, und nur sein, wenn sie in einer Weise zugegriffen wird, der die Einträge SACL übereinstimmt. Diese Ereignisse sind ähnlich den verzeichnisdienstzugriffsereignisse in früheren Versionen von Windows Server. Diese Unterkategorie gilt nur für Domänencontroller.  
  
##### <a name="directory-service-changes"></a>Verzeichnisdienst geändert wird.  
Diese Unterkategorie meldet Änderungen an der Objekte in AD DS. Sind die Arten von Änderungen, die gemeldet werden erstellen, ändern, verschieben und Wiederherstellen von Vorgängen, die für ein Objekt ausgeführt werden. Directory Service ändern Überwachung, falls zutreffend, gibt die alten und neuen Werte der geänderten Eigenschaften der Objekte, die geändert wurden. Nur Objekte mit SACLs verursachen Überwachungsereignisse generiert, und nur sein, wenn sie in einer Weise zugegriffen wird, die ihren SACL-Einträgen entspricht. Einige Objekte und Eigenschaften bewirken keine Überwachungsereignisse aufgrund der Einstellungen der Objektklasse im Schema generiert werden. Diese Unterkategorie gilt nur für Domänencontroller.  
  
##### <a name="directory-service-replication"></a>Replikation des Active Directory  
Diese Unterkategorie wird berichtet, wenn die Replikation zwischen zwei Domänencontrollern beginnt und endet.  
  
##### <a name="detailed-directory-service-replication"></a>Detaillierte Verzeichnisdienstreplikation  
Diese Unterkategorie meldet ausführliche Informationen zu den Informationen, die zwischen Domänencontrollern repliziert. Diese Ereignisse können im Volume sehr hoch sein.  
  
#### <a name="logonlogoff"></a>Anmelden/Abmelden  
  
##### <a name="logon"></a>Anmeldung  
Diese Unterkategorie berichtet, wenn ein Benutzer versucht, das System anmelden. Diese Ereignisse treten auf dem Computer zugegriffen wurde. Für die interaktive Anmeldung tritt auf, die Generation eines dieser Ereignisse auf dem Computer, auf dem die Anmeldung ist. Wenn Sie zur Anmeldung am Netzwerk auf eine Freigabe zugegriffen wird, generiert diese Ereignisse auf dem Computer, auf dem die Ressource zugegriffen gehostet. Wenn diese Einstellung konfiguriert ist **keine Überwachung**, es ist schwierig oder gar nicht, um zu bestimmen, welche Benutzer zugegriffen hat, oder Computer Organisation zugreifen möchten.  
  
##### <a name="network-policy-server"></a>Der Netzwerkrichtlinienserver  
Diese Unterkategorie protokolliert Ereignisse, die von RADIUS (IAS) und (Network Access Protection, NAP) benutzerzugriffsanfragen generiert. Diese Anforderungen kann **gewähren**, **Verweigern**, **verwerfen**, **Quarantäne**, **Sperre**, und **Unlock**. Überwachung dieser Einstellung führt zu einem Volume Mittel oder hoch Datensätze auf NPS und IAS-Server.  
  
##### <a name="ipsec-main-mode"></a>IPsec-Hauptmodus  
Diese Unterkategorie meldet die Ergebnisse des (Internet Key Exchange, IKE)-Protokolls und des Authenticated Internet Protocol (AuthIP) bei Aushandlungen im Hauptmodus.  
  
##### <a name="ipsec-extended-mode"></a>IPsec-Erweiterungsmodus  
Diese Unterkategorie meldet die Ergebnisse der AuthIP bei Aushandlungen im Erweiterungsmodus.  
  
##### <a name="other-logonlogoff-events"></a>Andere Anmelde-/Abmeldeereignisse  
Diese Unterkategorie meldet anderen an- und Abmeldung-bezogene Ereignisse, z. B. Remote Desktop Services Sitzung trennt und erneut eine Verbindung herstellt, Verwendung von RunAs Prozesse unter einem anderen Konto ausgeführt und Sperren und Entsperren einer Arbeitsstation.  
  
##### <a name="logoff"></a>Abmelden  
Diese Unterkategorie berichtet, wenn ein Benutzer abgemeldet hat. Diese Ereignisse treten auf dem Computer zugegriffen wurde. Für die interaktive Anmeldung tritt auf, die Generation eines dieser Ereignisse auf dem Computer, auf dem die Anmeldung ist. Wenn Sie zur Anmeldung am Netzwerk auf eine Freigabe zugegriffen wird, generiert diese Ereignisse auf dem Computer, auf dem die Ressource zugegriffen gehostet. Wenn diese Einstellung konfiguriert ist **keine Überwachung**, es ist schwierig oder gar nicht, um zu bestimmen, welche Benutzer zugegriffen hat, oder Computer Organisation zugreifen möchten.  
  
##### <a name="account-lockout"></a>Konto gesperrt  
Diese Unterkategorie berichtet, wenn es sich bei dem Konto eines Benutzers durch zu viele fehlerhafte Anmeldeversuche gesperrt wird.  
  
##### <a name="ipsec-quick-mode"></a>IPsec-Schnellmodus  
Diese Unterkategorie meldet die Ergebnisse des IKE-Protokoll und AuthIP bei Aushandlungen im Schnellmodus.  
  
##### <a name="special-logon"></a>Spezielle Anmeldung  
Diese Unterkategorie berichtet, wenn eine spezielle Anmeldung verwendet wird. Eine spezielle Anmeldung ist eine Anmeldung, die entsprechenden Administratorrechte und kann verwendet werden, um einen Prozess auf eine höhere Ebene zu erhöhen.  
  
#### <a name="policy-change"></a>Richtlinienänderung  
  
##### <a name="audit-policy-change"></a>Änderung der Überwachungsrichtlinien  
Diese Unterkategorie meldet Änderungen Überwachungsrichtlinie einschließlich SACL-Änderungen.  
  
##### <a name="authentication-policy-change"></a>Authentication Policy ändern  
Diese Unterkategorie meldet Änderungen Authentifizierungsrichtlinie.  
  
##### <a name="authorization-policy-change"></a>Autorisierungsrichtlinienänderung  
Diese Unterkategorie meldet Änderungen Autorisierungsrichtlinie einschließlich Berechtigungen (DACL).  
  
##### <a name="mpssvc-rule-level-policy-change"></a>MPSSVC-Regel-Richtlinienänderung  
Diese Unterkategorie meldet Änderungen der Richtlinienregeln, die von der Microsoft-Schutzdienst (MPSSVC.exe) verwendet. Dieser Dienst wird von Windows-Firewall verwendet.  
  
##### <a name="filtering-platform-policy-change"></a>Filterplattform-Richtlinienänderung  
Diese Unterkategorie meldet das Hinzufügen und Entfernen von Objekten aus der Windows-Dateischutz, einschließlich Startfilter. Diese Ereignisse können im Volume sehr hoch sein.  
  
##### <a name="other-policy-change-events"></a>Andere Richtlinienänderungsereignisse  
Diese Unterkategorie meldet, andere Arten von sicherheitsrichtlinienänderungen wie z. B. die Konfiguration der Trusted Platform Module (TPM) oder Kryptografieanbieter.  
  
#### <a name="privilege-use"></a>Verwendung von rechten  
  
##### <a name="sensitive-privilege-use"></a>Sensible Verwendung von rechten  
Diese Unterkategorie wird berichtet, wenn ein Benutzerkonto oder Dienst verwendet eine sensible Berechtigung aufgerufen. Eine sensible Berechtigung enthält die folgenden Berechtigungen: Einsetzen als Teil des Betriebssystems, Dateien und Verzeichnisse sichern, Erstellen eines Tokenobjekts, Debuggen von Programmen, Computer- und Benutzerkonten für Delegierungszwecke vertraut, Generieren von sicherheitsüberwachungen, Annehmen der Clientidentität nach Authentifizierung, laden und Entfernen von Gerätetreibern, Verwalten von überwachungs- und Sicherheitsprotokoll aktivieren, Firmwareumgebungsvariablen ändern, Ersetzen eines Tokens auf Prozessebene , Dateien und Verzeichnisse wiederherstellen und den Besitz von Dateien und Objekten. Diese Unterkategorie Überwachung, erstellen Sie eine große Anzahl von Ereignissen.  
  
##### <a name="nonsensitive-privilege-use"></a>Nonsensitive Rechteverwendung  
Diese Unterkategorie wird berichtet, wenn ein Benutzerkonto oder Dienst verwendet ein nonsensitive Recht. Ein nonsensitive Recht umfasst die folgenden Berechtigungen: Anmeldeinformations-Manager als vertrauenswürdigem Aufrufer zugreifen, auf diesen Computer vom Netzwerk aus zugreifen, Hinzufügen von Arbeitsstationen zur Domäne, Anpassen von Speicherkontingenten für einen Prozess, lokal anmelden zulassen, Anmelden über Remotedesktopdienste zulassen, Auslassen der durchsuchenden Überprüfung, Ändern der Systemzeit, erstellen Sie eine Auslagerungsdatei, globale Objekte erstellen, Erstellen von dauerhafte freigegebene Objekten, symbolische Verknüpfungen erstellen , diesen Computer vom Netzwerk für den Zugriff verweigert, Anmelden als Batchauftrag verweigern, Anmelden als Dienst verweigern, lokal anmelden verweigern, Anmelden über Remotedesktopdienste verweigern, erzwingen des Herunterfahrens von einem Remotesystem aus, Arbeitssatz eines Prozesses vergrößern, Anheben der Zeitplanungspriorität, Sperren von Seiten im Speicher, Anmelden als Stapelverarbeitungsauftrag, melden Sie sich als ein Dienst, verändern einer objektbezeichnung , Ausführen von Volumewartungsaufgaben, Profils für einen Einzelprozess, Profils der Systemleistung, Entfernen des Computers von der Dockingstation, Herunterfahren des Systems und Synchronisieren von Verzeichnisdienstdaten. Diese Unterkategorie Überwachung, erstellen Sie eine sehr hohe Anzahl von Ereignissen.  
  
##### <a name="other-privilege-use-events"></a>Andere Rechteverwendungsereignisse  
Diese sicherheitsrichtlinieneinstellung wird derzeit nicht verwendet.  
  
#### <a name="object-access"></a>Den Zugriff auf Objekte  
  
##### <a name="file-system"></a>Dateisystem  
Diese Unterkategorie berichtet, wenn Dateisystemobjekte zugegriffen werden. Nur Dateisystemobjekte mit SACLs verursachen Überwachungsereignisse werden generiert, und nur bei Zugriff auf eine Weise ihre Einträge der SACL entsprechen. Selbst bewirkt diese Einstellung nicht die Überwachung von Ereignissen. Es bestimmt, ob das Ereignis eines Benutzers zu überwachen, die ein Dateisystemobjekt zugreift, für einen angegebenen System-Zugriffssteuerungsliste (SACL), ist effektiv Aktivieren der Überwachung stattfinden.  
  
Wenn die Einstellung Objektzugriffsversuche werden **Erfolg**, ein Überwachungsereignis generiert jedes Mal, ein Benutzer erfolgreich auf ein Objekt mit einer angegebenen SACL zugreift. Wenn diese Einstellung konfiguriert ist **Fehler**, Überwachungseintrag generiert, wird jedes Mal, die ein Benutzer auf ein Objekt mit einer angegebenen SACL zugreifen kann.  
  
##### <a name="registry"></a>Registrierung  
Diese Unterkategorie wird berichtet, wenn die Registrierungsobjekte zugegriffen werden. Nur Registrierungsobjekte mit SACLs verursachen Überwachungsereignisse werden generiert, und nur bei Zugriff auf eine Weise ihre Einträge der SACL entsprechen. Selbst bewirkt diese Einstellung nicht die Überwachung von Ereignissen.  
  
##### <a name="kernel-object"></a>Kernelobjekt  
Diese Unterkategorie wird berichtet, wenn der Kernelobjekte, z. B. Prozesse und Mutexe zugegriffen wird. Nur Kernelobjekte mit SACLs verursachen Überwachungsereignisse werden generiert, und nur bei Zugriff auf eine Weise ihre Einträge der SACL entsprechen. In der Regel erhalten Kernelobjekte nur SACLs, wenn die AuditBaseObjects oder AuditBaseDirectories Überwachungsoptionen aktiviert sind.  
  
##### <a name="sam"></a>SAM  
Diese Unterkategorie berichtet, wenn lokale Sicherheitskontenverwaltung (Security Accounts Manager, SAM) Authentifizierung Datenbankobjekte zugegriffen wird.  
  
##### <a name="certification-services"></a>Zertifikatdienste  
Diese Unterkategorie berichtet, wenn die Zertifikatdienste Vorgänge ausgeführt werden.  
  
##### <a name="application-generated"></a>Anwendung generiert  
Diese Unterkategorie berichtet, wenn Anwendungen versuchen, um Überwachungsereignisse zu generieren, über den Windows-Überwachung Anwendungsprogrammierschnittstellen (APIs).  
  
##### <a name="handle-manipulation"></a>Handleänderung  
Diese Unterkategorie berichtet, wenn ein Handle für ein Objekt geöffnet oder geschlossen wird. Nur Objekte mit SACLs dazu führen, dass diese Ereignisse werden generiert, und nur dann, wenn der versuchte handlevorgang der SACL-Einträgen entspricht. Handle-Manipulationsereignisse werden nur für Objekttypen generiert, die entsprechende Unterkategorie der Objekt zugreifen (z. B. Dateisystem oder Registrierung) aktiviert ist.  
  
##### <a name="file-share"></a>Dateifreigabe  
Diese Unterkategorie berichtet, wenn eine Dateifreigabe zugegriffen wird. Selbst bewirkt diese Einstellung nicht die Überwachung von Ereignissen. Es bestimmt, ob das Ereignis eines Benutzers zu überwachen, die eine Datei Teilen-Objekt zugreift, eine angegebene System-Zugriffssteuerungsliste (SACL), ist, effektiv Aktivieren der Überwachung stattfinden.  
  
##### <a name="filtering-platform-packet-drop"></a>Filterplattform: Verworfene  
Diese Unterkategorie berichtet, wenn Pakete durch Windows Filtering Platform (WFP) gelöscht werden. Diese Ereignisse können im Volume sehr hoch sein.  
  
##### <a name="filtering-platform-connection"></a>Filterplattformverbindung  
Diese Unterkategorie berichtet, wenn Verbindungen zulässt oder WFP blockiert werden. Diese Ereignisse können im Volume hoch sein.  
  
##### <a name="other-object-access-events"></a>Andere Objektzugriffsereignisse  
Diese Unterkategorie meldet andere Objekt Zugriff-bezogene Ereignisse wie Task Scheduler-Aufträgen und COM+-Objekte.  
  
#### <a name="system"></a>System  
  
##### <a name="security-state-change"></a>Sicherheitsstatus ändern  
Diese Unterkategorie meldet Änderungen Sicherheitsstatus des Systems, z. B. wenn das Sicherheitssubsystem startet und beendet.  
  
##### <a name="security-system-extension"></a>Sicherheit System-Erweiterung  
Diese Unterkategorie meldet das Laden von Erweiterungscode z. B. Authentifizierungspakete durch das Sicherheitssubsystem.  
  
##### <a name="system-integrity"></a>Integrität des Systems  
Diese Unterkategorie meldet auf Verletzungen der Integrität des Sicherheitssubsystems.  
  
IPSec-Treiber  
  
Diese Unterkategorie meldet sich auf die Aktivitäten des Treibers Internet Protocol Security (IPsec).  
  
##### <a name="other-system-events"></a>Andere Systemereignisse  
Diese Unterkategorie meldet auf andere Systemereignisse.  
  
Weitere Informationen zu den Beschreibungen der Unterkategorie, finden Sie in der [Microsoft Security Compliance Manager-Tool](https://technet.microsoft.com/library/cc677002.aspx).  
  
Jede Organisation überprüfen den vorherigen abgedeckte Kategorien und Unterkategorien, und aktivieren diejenigen, die in ihrer Umgebung am besten geeignet. Änderungen an Überwachungsrichtlinien sollten immer vor der Bereitstellung in einer produktionsumgebung getestet werden.  
  
### <a name="configuring-windows-audit-policy"></a>Konfigurieren von Windows-Sicherheitsüberwachungsrichtlinie  
Windows-Überwachungsrichtlinie kann mithilfe von Gruppenrichtlinien-Richtlinien, auditpol.exe, APIs oder Registrierung bearbeitet festgelegt werden. Die empfohlenen Methoden zum Konfigurieren von Überwachungsrichtlinien für die meisten Unternehmen sind "Gruppenrichtlinie" oder "auditpol.exe. Festlegen der Überwachungsrichtlinie des Systems erfordert Administratorkonto Berechtigungen oder die entsprechenden Berechtigungen.  
  
> [!NOTE]  
> Die **Verwalten von überwachungs- und Sicherheitsprotokollen** Berechtigung Sicherheitsprinzipalen zugewiesen werden muss (Administratoren haben sie in der Standardeinstellung) ermöglicht die Änderung der Objektzugriff-Überwachungsoptionen für einzelne Ressourcen, z. B. Dateien, Active Directory-Objekte und Registrierungsschlüssel.  
  
#### <a name="setting-windows-audit-policy-by-using-group-policy"></a>Einstellung Windows-Überwachungsrichtlinie mithilfe von Gruppenrichtlinien  
Zum Festlegen der Überwachungsrichtlinie mithilfe von Gruppenrichtlinien konfigurieren Sie die entsprechenden Überwachungskategorien finden Sie unter **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\überwachungsrichtlinie** (Siehe das folgende Bildschirmabbild ein Beispiel aus dem Editor für lokale Gruppenrichtlinien (gpedit.msc)). Jede Richtlinienkategorie überwachen kann aktiviert werden, für die **Erfolg**, **Fehler**, oder **Erfolg** und Fehlerereignisse.  
  
![Überwachung von Active Directory](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_6.gif)  
  
Erweiterte Überwachungsrichtlinie können mithilfe von Active Directory oder lokale Gruppenrichtlinien festgelegt werden. Konfigurieren von erweiterten Überwachungsrichtlinie festlegen, die entsprechenden Unterkategorien finden Sie unter **Computerkonfiguration\Windows-einstellungen\sicherheitseinstellungen\erweiterte Audit-Richtlinie** (Siehe das folgende Bildschirmabbild ein Beispiel aus dem Editor für lokale Gruppenrichtlinien (gpedit.msc)). Jede Unterkategorie der Überwachungsrichtlinie kann aktiviert werden, für die **Erfolg**, **Fehler**, oder **Erfolg** und **Fehler** Ereignisse.  
  
![Überwachung von Active Directory](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_7.gif)  
  
#### <a name="setting-windows-audit-policy-using-auditpolexe"></a>Einstellung Windows-Überwachungsrichtlinie mithilfe von Auditpol.exe  
Auditpol.exe (zum Festlegen der Windows-Überwachungsrichtlinie) wurde in Windows Server 2008 und Windows Vista eingeführt. Zunächst nur auditpol.exe kann verwendet werden, um die erweiterten Überwachungsrichtlinie festlegen, aber der Gruppenrichtlinie in Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008, Windows 8 und Windows 7 verwendet werden können.  
  
Auditpol.exe ist ein Befehlszeilenprogramm. Die Syntax lautet wie folgt:  
  
**Auditpol/Set / < Kategorie | Unterkategorie >:<audit category> / < Erfolg | Fehler: > / < aktivieren | deaktivieren >**  
  
Auditpol.exe Syntaxbeispiele:  
  
**Auditpol/set/SubCategory: "Benutzerkontenverwaltung" /success:enable Success**  
  
**Auditpol/set/SubCategory: /success:enable Success "Anmelden"**  
  
**Auditpol/set/SubCategory: "IPSEC Main Mode" Success**  
  
> [!NOTE]  
> Auditpol.exe legt die erweiterte Überwachungsrichtlinie lokal. Wenn die lokaler Richtlinie mit Active Directory oder lokale Gruppenrichtlinie in Konflikt steht, durchgesetzt Group Policy Settings in der Regel über auditpol.exe Einstellungen. Wenn mehrere Gruppe oder lokale Richtlinienkonflikte vorhanden sind, wird nur eine Richtlinie durchgesetzt (das ist, ersetzen Sie). Überwachungsrichtlinien werden nicht zusammengeführt.  
  
#### <a name="scripting-auditpol"></a>Skripting Auditpol  
Microsoft bietet eine [Beispielskript](https://support.microsoft.com/kb/921469) für Administratoren, die erweiterte Überwachungsrichtlinie festlegen, mit einem Skript, anstatt Sie in jedem Befehl auditpol.exe manuell eingeben möchten.  
  
**Hinweis:** Gruppenrichtlinien nicht immer genau meldet den Status der alle aktivierten Überwachungsrichtlinien, Gegensatz auditpol.exe. Finden Sie unter [beim Abrufen der effektiven Überwachungsrichtlinie in Windows 7 und Windows 2008 R2](http://blogs.technet.com/b/askds/archive/2011/03/11/getting-the-effective-audit-policy-in-windows-7-and-2008-r2.aspx) Weitere Details.  
  
#### <a name="other-auditpol-commands"></a>Andere Befehle Auditpol  
Auditpol.exe kann verwendet werden, speichern und Wiederherstellen einer Überwachungsrichtlinie für den lokalen und andere verwandte Befehle anzuzeigen. Hier erhalten Sie die andere **Auditpol** Befehle.  
  
**Auditpol/clear** – wird verwendet, zu löschen und Wiederherstellen der lokalen Überwachungsrichtlinien  
  
**Auditpol/Backup/file:<filename> ** – wird verwendet, um eine aktuelle lokale Überwachungsrichtlinie in eine binäre Datei sichern  
  
**Auditpol/Restore / file:<filename> ** – wird verwendet, um eine zuvor gespeicherte Audit-Richtliniendatei in eine Überwachungsrichtlinie für den lokalen importieren  
  
**Auditpol / < Get/Set >/Option:<CrashOnAuditFail> / < aktiviert bzw. deaktiviert >** -Einstellung für diese Überwachungsrichtlinien aktiviert ist, wird sofort beendet (mit STOP: C0000244 {Überwachung fehlgeschlagen} Nachricht) Wenn eine sicherheitsüberwachung aus irgendeinem Grund nicht protokolliert werden kann. In der Regel ein Ereignis nicht protokolliert werden, wenn das Sicherheitsüberwachungsprotokoll voll ist und die Aufbewahrungsmethode des Sicherheitsprotokolls **Ereignisse nicht überschreiben** oder **Ereignisse auf Tagen basierend überschreiben**. In der Regel ist sie nur in Umgebungen aktiviert, die höhere benötigen, die das Sicherheitsprotokoll protokolliert wird. Ist diese Einstellung aktiviert ist, müssen Administratoren eng Größe des Sicherheitsprotokolls ansehen und Protokolle nach Bedarf zu drehen. Sie können auch mit der Gruppenrichtlinie festgelegt werden, ändern die Sicherheitsoption, indem Sie **überwachen: System sofort, wenn Sie nicht von sicherheitsüberwachungen protokolliert Herunterfahren** (Standardwert = deaktiviert).  
  
**Auditpol / < Get/Set >/Option:<AuditBaseObjects> / < aktiviert bzw. deaktiviert >** -diese Überwachungsrichtlinie bestimmt, ob den Zugriff auf globale Systemobjekte überwacht. Wenn diese Richtlinie aktiviert ist, werden Systemobjekte wie Mutexe, Ereignisse, Semaphoren und DOS-Geräte mit eine standardmäßige System-Zugriffssteuerungsliste (SACL) erstellt werden. Die meisten Administratoren sollten Sie globale Systemobjekte "rauscht" werden und werden sie nur dann aktivieren, wenn böswilliger hacking vermutet wird. Nur benannte Objekte erhalten eine SACL. Wenn die überwachen Objekt Zugriff Audit Policy (oder Kernelobjekt Überwachungsunterkategorie) ebenfalls aktiviert ist, wird der Zugriff auf diese Systemobjekte überwacht. Wenn Sie diese Einstellung konfigurieren, werden Änderungen nicht wirksam, bis zum Neustart von Windows. Diese Richtlinie kann auch die Sicherheitsoption Zugriff auf globale Systemobjekte ändern, indem Sie mit der Gruppenrichtlinie festgelegt werden (Standardwert = deaktiviert).  
  
**Auditpol / < Get/Set >/Option:<AuditBaseDirectories> / < aktiviert bzw. deaktiviert >** -diese Überwachungsrichtlinie gibt an, dass benannten Kernelobjekte (z. B. Mutexe und Semaphore) SACLs gewährt werden, wenn sie erstellt werden. AuditBaseDirectories betrifft Containerobjekte AuditBaseObjects Objekte, die andere Objekte enthalten kann.  
  
**Auditpol / < Get/Set >/Option:<FullPrivilegeAuditing> / < aktiviert bzw. deaktiviert >** -  
  
Diese Überwachungsrichtlinie gibt an, ob der Client generiert ein Ereignis, wenn eine oder mehrere der folgenden Berechtigungen, ein Sicherheitstoken für Benutzer zugewiesen sind: AssignPrimaryTokenPrivilege, AuditPrivilege, BackupPrivilege, CreateTokenPrivilege, DebugPrivilege, EnableDelegationPrivilege, ImpersonatePrivilege, LoadDriverPrivilege, RestorePrivilege, SecurityPrivilege, SystemEnvironmentPrivilege, TakeOwnershipPrivilege und TcbPrivilege. Wenn diese Option nicht aktiviert ist (Standard = deaktiviert), die BackupPrivilege und RestorePrivilege Berechtigungen werden nicht aufgezeichnet. Durch das Aktivieren dieser Option können Sie das Sicherheitsprotokoll extrem lauten (manchmal Hunderte von Ereignissen pro Sekunde) während eines Sicherungsvorgangs vornehmen. Diese Richtlinie kann auch mit der Gruppenrichtlinie festgelegt werden, durch Ändern der Sicherheitsoption **überwachen: die Verwendung des Sicherungs- und wiederherstellungsrechts überprüfen**.  
  
> [!NOTE]  
> Einige hier bereitgestellten Informationen stammt aus dem Microsoft [Audit Optionstyp](https://msdn.microsoft.com/library/dd973862(prot.20).aspx) und das Microsoft SCM-Tool.  
  
### <a name="enforcing-traditional-auditing-or-advanced-auditing"></a>Herkömmliche Überwachung oder erweiterte Überwachung erzwingen  
In Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows 8, Windows 7 und Windows Vista können Administratoren die neun herkömmlichen Kategorien zu aktivieren oder die Unterkategorien verwenden. Es ist eine binärauswahl, die in den einzelnen Windows-Systemen vorgenommen werden muss. Entweder die Hauptkategorien können aktiviert werden, oder die Subcategoriesit kann nicht gleichzeitig.  
  
Um zu verhindern, dass die ältere herkömmliche Kategorierichtlinie überschreiben Überwachungsrichtlinien-Unterkategorien, müssen Sie aktivieren die **Audit unterkategorieeinstellungen (Windows Vista oder höher) Außerkraftsetzen der Einstellungen für Sicherheitsüberwachungsrichtlinien Kategorie** Einstellung befindet sich unter **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\sicherheitsoptionen**.  
  
Es wird empfohlen, dass die Unterkategorien aktiviert und konfiguriert werden, anstatt die neun Hauptkategorien. Dies erfordert, dass eine gruppenrichtlinieneinstellung aktiviert werden (um die Überwachungskategorien überschreiben die Unterkategorien ermöglichen eine) konfigurieren Sie die verschiedenen Unterkategorien, die Überwachungsrichtlinien zu unterstützen.  
  
Überwachung von Unterkategorien kann verschiedene Methoden, einschließlich der Gruppenrichtlinie und das Befehlszeilenprogramm, auditpol.exe konfiguriert werden.  
  
Weitere Informationen zur Überwachung von Windows finden Sie unter den folgenden Artikeln:  
  
-   [Erweiterter Sicherheitsüberwachung in Windows 7 und Windows Server 2008 R2](https://social.technet.microsoft.com/wiki/contents/articles/advanced-security-auditing-in-windows-7-and-windows-server-2008-r2.aspx)  
  
-   [Überwachung und Compliance in WindowsServer 2008](https://technet.microsoft.com/magazine/2008.03.auditing.aspx)  
  
-   [Wie Sie mithilfe von Gruppenrichtlinien zum Konfigurieren von detaillierten Sicherheitsüberwachungsrichtlinien für Windows Vista und Windows Server 2008-basierte Computer in einer Windows Server 2008-Domäne, in einer Windows Server 2003-Domäne oder in einer Windows 2000-Domäne](https://support.microsoft.com/kb/921469)  
  
-   [Erweiterte Sicherheitsüberwachungsrichtlinien Step-by-Step Guide](https://technet.microsoft.com/library/dd408940(WS.10).aspx)  
  


