---
ms.assetid: a7ef2fba-b05c-4be2-93b2-b9456244c3ad
title: Überwachen von Active Directory auf Anzeichen für einen Kompromiss
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 40d0d06f8d6d25c2c1dbf4662d3296a996d22055
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882941"
---
# <a name="monitoring-active-directory-for-signs-of-compromise"></a>Überwachen von Active Directory auf Anzeichen für einen Kompromiss

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*Gesetz Nummer fünf: Endlose Wachsamkeit ist der Preis für die Sicherheit.* - [10 unveränderlichen Gesetze zur Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Ein solid Ereignisprotokoll Überwachungssystem ist ein wichtiger Aspekt jeder sicheren Active Directory-Designs. Viele Computer von sicherheitsgefährdungen konnte frühzeitig in den Ereignisdaten ermittelt werden, wenn die Opfer die entsprechende Ereignisprotokoll, Überwachung und warnungsgenerierung in Kraft gesetzt. Unabhängige Berichte haben lange dieser Schlussfolgerung unterstützt. Z. B. die [2009 Verizon Data Breach-Bericht](http://www.verizonbusiness.com/resources/security/reports/2009_databreach_rp.pdf) Zustände:  
  
"Die scheinbare Ausfall der überwachungs- und Ereignisanalyse dadurch weiterhin eher ein Rätsel. Es gibt es die Möglichkeit für die Erkennung; Ermittler Beachten Sie, dass 66 Prozent des Opfers ausreichenden nachweisen bis in ihre Protokolle sicherheitsverletzung ermittelt dies der Fall wäre mehr gewissenhaft hatte bei der Analyse von Ressourcen zur Verfügung."  
  
Diese mangelnde Überwachen von aktiven Ereignisprotokollen bleibt eine konsistente Schwachstelle in vielen Unternehmen Security Defense-Pläne. Die [2012-Verizon Data Breach-Bericht](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf) festgestellt, dass, obwohl 85 Prozent der sicherheitsverletzungen einige Wochen bemerkt haben, 84 Prozent des Opfers Beweis der sicherheitsverletzung in ihren Ereignisprotokollen hatte.  
  
## <a name="windows-audit-policy"></a>Windows-Überwachungsrichtlinie

Im folgenden finden Links zu den Microsoft official Enterprise Support-Blog. Diese Blogs enthält Empfehlungen, Anleitungen und Empfehlungen zur Überwachung, hilft Ihnen bei der Verbesserung der Sicherheits der Active Directory-Infrastruktur und sind eine wertvolle Ressource, beim Entwerfen einer Überwachungsrichtlinie.  
  
* [Globale Objektzugriffsüberwachung Magic ist](http://blogs.technet.com/b/askds/archive/2011/03/10/global-object-access-auditing-is-magic.aspx) -beschreibt einen Steuerelement-Mechanismus namens erweiterte Überwachungsrichtlinienkonfiguration, die auf Windows 7 und Windows Server 2008 R2, mit dem Sie festlegen, welche Arten von Daten möchten leicht überwachen und nicht Jonglieren hinzugefügt wurde Skripts und auditpol.exe.  
* [Einführung in die Überwachung von Änderungen in Windows 2008](http://blogs.technet.com/b/askds/archive/2007/10/19/introducing-auditing-changes-in-windows-2008.aspx) -Überwachung in Windows Server 2008 vorgenommenen Änderungen führt.  
* ["Cool" Überwachung Tricks in Vista und 2008](http://blogs.technet.com/b/askds/archive/2007/11/16/cool-auditing-tricks-in-vista-and-2008.aspx) -interessante Überwachungsfeatures von Windows Vista und Windows Server 2008, die verwendet werden können, für die Behandlung von Problemen oder sehen die Abläufe in Ihrer Umgebung erläutert.  
* [Zentrale Anlaufstelle für die Überwachung in Windows Server 2008 und Windows Vista](http://blogs.technet.com/b/askds/archive/2008/03/27/one-stop-shop-for-auditing-in-windows-server-2008-and-windows-vista.aspx) -enthält eine Zusammenstellung von Überwachung von Funktionen und Informationen, die in Windows Server 2008 und Windows Vista enthalten sind.  
  
Die folgenden Links bieten Informationen zu Verbesserungen an Windows-Überwachung in Windows 8 und Windows Server 2012 und Informationen zu AD DS in Windows Server 2008-Überwachung.  
  
* [Neues bei der Sicherheitsüberwachung](https://technet.microsoft.com/library/hh849638.aspx) -bietet einen Überblick über neue Features in Windows 8 und Windows Server 2012 für die sicherheitsüberwachung.  
* [Anleitung für AD DS-Überwachung](https://technet.microsoft.com/library/a9c25483-89e2-4202-881c-ea8e02b4b2a5.aspx) -beschreibt die neue Überwachungsfunktion mit Active Directory Domain Services (AD DS) in Windows Server 2008. Darüber hinaus werden Verfahren zur Implementierung dieser neuen Funktion.  
  
### <a name="windows-audit-categories"></a>Windows-Überwachungskategorien

Vor Windows Vista und Windows Server 2008 musste Windows nur neun Ereignisprotokoll Überwachungskategorien Richtlinie:  
  
* Anmeldeversuche  
* Kontenverwaltung  
* Active Directory-Zugriff  
* Logon-Ereignissen  
* Objektzugriff  
* Richtlinienänderung  
* Verwendung von Berechtigungen  
* Überwachen  
* Systemereignisse  
  
Diese neun herkömmliche Überwachungskategorien umfassen eine Überwachungsrichtlinie. Jede Richtlinienkategorie Überwachung kann aktiviert werden, für Erfolg, Fehler oder Erfolg und Fehler Ereignisse. Im nächsten Abschnitt sind die Beschreibungen enthalten.  
  
#### <a name="audit-policy-category-descriptions"></a>Überwachen Sie die Kategorie der Richtlinienbeschreibung  
Die Überwachung von Richtlinienkategorien können die folgenden Nachrichtentypen in Ereignisprotokoll an.  
  
##### <a name="audit-account-logon-events"></a>Anmeldeversuche überwachen  
Meldet jede Instanz eines Sicherheitsprinzipals (z. B. Benutzer, Computer oder Dienstkonto), die Protokollierung auf oder von einem Computer, die in der einen anderen Computer, zum Überprüfen des Kontos verwendet wird abmelden. Anmeldeversuche werden generiert, wenn ein principal Security-Domänenkonto auf einem Domänencontroller authentifiziert wird. Authentifizierung eines lokalen Benutzers auf einem lokalen Computer generiert ein Logon-Ereignis, das im lokalen Sicherheitsprotokoll angemeldet ist. Kein Konto Abmeldeereignisse werden protokolliert.  
  
Diese Kategorie generiert "Rauschen"durch viele da Konten, die Protokollierung auf ständig von Windows aufgetreten sind und auf dem lokalen Computer und Remotecomputer während des normalen Betriebs der Unternehmen an. Dennoch sollte jeder Sicherheitsplan Erfolg und Fehlern dieser Kategorie Überwachung enthalten.  
  
##### <a name="audit-account-management"></a>Kontenverwaltung  
Diese überwachungseinstellung bestimmt, ob die Verwaltung von Benutzern und Gruppen nachverfolgen. Beispielsweise sollten Benutzer und Gruppen nachverfolgt werden, wenn ein Benutzer oder Computerkonto, eine Sicherheitsgruppe oder eine Verteilergruppe erstellt, geändert oder gelöscht wird; Wenn eine Benutzer- oder Computerkonto umbenannt, deaktiviert oder aktiviert ist; oder wenn ein Benutzer oder Computer Kennwort geändert wird. Für Benutzer oder Gruppen, die hinzugefügt oder aus anderen Gruppen entfernt werden, kann ein Ereignis generiert werden.  
  
##### <a name="audit-directory-service-access"></a>Verzeichnisdienstzugriff überwachen  

Mit dieser richtlinieneinstellung wird bestimmt, ob Sicherheitsprinzipal den Zugriff auf Active Directory-Objekt zu überwachen, die eine eigene angegebenen Systemzugriffssteuerungsliste (SACL). Im Allgemeinen sollten diese Kategorie nur auf Domänencontrollern aktiviert werden. Wenn aktiviert, generiert diese Einstellung einen Großteil "Rauschen"durch.  
  
##### <a name="audit-logon-events"></a>Anmeldeereignisse überwachen  
Logon-Ereignissen werden generiert, wenn ein lokale Sicherheitsprinzipal auf einem lokalen Computer authentifiziert wird. Logon-Ereignissen zeichnet domänenanmeldungen, die auf dem lokalen Computer auftreten. Kontoabmeldeereignisse werden nicht generiert. Wenn aktiviert, generiert Anmeldeereignisse viel "Rauschen", aber sie sollten in jeder Überwachung Sicherheitsplan standardmäßig aktiviert werden.  
  
##### <a name="audit-object-access"></a>Überwachen des Objektzugriffs  
Zugriff auf Objekte kann Ereignisse generieren, wenn nachfolgend definierte Objekte mit aktivierter Überwachung (z. B., Opened, lesen, umbenannt, gelöscht oder geschlossen) zugegriffen werden. Nachdem die Überwachung Hauptkategorie aktiviert ist, muss der Administrator einzeln definieren die Objekte, die Überwachung aktiviert haben wird. Viele Windows-System-Objekte verfügen über die Überwachung aktiviert, sodass aktivieren diese Kategorie in der Regel wird zum Generieren von Ereignissen, bevor der Administrator definiert hat.  
  
Diese Kategorie ist sehr "lauten" und fünf bis zehn Ereignisse für jeden Zugriff auf die Objekte generiert. Es kann Administratoren noch nicht mit der Überwachung von Objekten erhalten Sie nützliche Informationen schwierig sein. Es sollte nur bei Bedarf aktiviert werden.  
  
##### <a name="auditing-policy-change"></a>Überwachung von Richtlinienänderungen  
Mit dieser richtlinieneinstellung wird bestimmt, ob alle Vorkommen von eine Änderung an Richtlinien für die Zuweisung von Benutzerrechten, Windows-Firewall-Richtlinien, Vertrauensrichtlinien oder Änderungen an der Überwachungsrichtlinie zu überwachen. Diese Kategorie sollte auf allen Computern aktiviert werden. Es wird nur sehr wenig Rauschen generiert.  
  
##### <a name="audit-privilege-use"></a>Rechteverwendung überwachen  

Es gibt Dutzende von Benutzerrechten und Berechtigungen in Windows (z. B. Anmeldung als Batchauftrag und als Teil des Betriebssystems handeln). Mit dieser richtlinieneinstellung wird bestimmt, ob jede Instanz eines Sicherheitsprinzipals zu überwachen, indem Sie die Möglichkeit, einen Benutzer, die Rechte oder Berechtigungen. Aktivieren diese Kategorie führt eine Vielzahl von "Rauschen durch", aber es kann hilfreich beim Verfolgen von Konten von Sicherheitsprinzipalen mit erweiterten Berechtigungen sein.  
  
##### <a name="audit-process-tracking"></a>Überwachen der Prozessverfolgung  
Mit dieser richtlinieneinstellung wird bestimmt, ob ausführliche Überwachungsinformationen für Ereignisse wie das Programm Aktivierung, Beenden des Prozesses, handleduplizierung und indirekte Objektzugriff zu überwachen. Es ist hilfreich für die nachverfolgung von böswilligen Benutzern und die Programme, die sie verwenden.  
  
Aktivieren der Überwachung nachverfolgen generiert eine große Anzahl von Ereignissen, in der Regel wird festgelegt **keine Überwachung**. Allerdings kann diese Einstellung bereitstellen, ein großer Vorteil bei der Reaktion auf Vorfälle aus das detaillierte Protokoll die Prozesse, die gestartet und die Zeit, die mit der sie gestartet wurden. Für Domänencontroller und anderer Infrastrukturserver für einzelne Rolle kann dieser Kategorie sicher auf die ganze Zeit aktiviert werden. Einzelne Rolle Servern keine viel Datenverkehr der prozessverfolgung während des normalen Verlaufs von ihren Aufgaben generiert. Sie können daher aktiviert werden, um nicht autorisierte Ereignisse zu erfassen, wenn sie auftreten.  
  
##### <a name="system-events-audit"></a>System-Ereignisse überwachen  

Systemereignisse ist fast eine generische Catch-All-Kategorie, registrieren verschiedener Ereignisse, die dem Computer, die Sicherheit des Systems oder das Sicherheitsprotokoll auswirken. Es enthält Ereignisse für Computer Herunterfahren und neu gestartet wird, Stromausfälle, Systemzeit geändert, Authentifizierung Paket Initialisierungen, Audit Log Clearings, Identitätswechsel Probleme und zahlreiche andere allgemeine Ereignisse. Im Allgemeinen, aktivieren diese Überwachungskategorie viel "Rauschen" generiert, sondern generiert genügend sehr nützliche Ereignisse, dass es schwierig, die jemals empfohlen nicht aktiviert, es ist.  
  
#### <a name="advanced-audit-policies"></a>Erweiterten Überwachungsrichtlinien

Ab Windows Vista und Windows Server 2008, hat Microsoft die Möglichkeit, die Ereignisprotokolle vorgenommen werden können, indem Unterkategorien unter jeder verbessert. Die Unterkategorien ermöglichen eine wesentlich differenziertere als es andernfalls könnte die Hauptkategorien mit Überwachung. Sie können mithilfe von Unterkategorien, aktivieren nur Teile einer bestimmten Hauptkategorie und Generieren von Ereignissen, die für die Sie keine Verwendung haben zu überspringen. Jede Unterkategorie der Überwachungsrichtlinie kann für Ereignisse durch Erfolg, Fehler oder Erfolg und Fehler aktiviert werden.  
  
Um alle verfügbaren Überwachung Unterkategorien aufzulisten, überprüfen Sie den erweiterten Überwachungsrichtlinie-Container in einem Group Policy Object, oder geben Sie Folgendes an einer Eingabeaufforderung auf jedem Computer unter Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008, Windows 8, Windows 7 oder Windows Vista:  
  
`auditpol /list /subcategory:\*`
  
Um eine Liste der aktuell konfigurierten Überwachung Unterkategorien auf einem Computer unter Windows Server 2012, Windows Server 2008 R2 oder Windows 2008 zu erhalten, geben Sie Folgendes ein:  
  
`auditpol /get /category:\*`
  
Der folgende Screenshot zeigt ein Beispiel für auditpol.exe Auflisten der aktuellen Überwachungsrichtlinie.  
  
![Überwachung von Active Directory](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_5.gif)  
  
> [!NOTE]  
> Die Gruppenrichtlinie meldet den Status der Überwachungsrichtlinien für alle, aktiviert, während auditpol.exe der Fall ist nicht immer genau. Finden Sie unter [Abrufen der effektiven Überwachungsrichtlinie in Windows 7 und 2008 R2](http://blogs.technet.com/b/askds/archive/2011/03/11/getting-the-effective-audit-policy-in-windows-7-and-2008-r2.aspx) Weitere Details.  
  
Jede Kategorie verfügt über mehrere Unterkategorien. Im folgenden finden eine Liste der Kategorien, deren Unterkategorien und eine Beschreibung ihrer Funktionen.  
  
### <a name="auditing-subcategories-descriptions"></a>Überwachung von Unterkategorien Beschreibungen  
Überwachungsrichtlinien-Unterkategorien aktivieren Sie die folgenden Ereignisprotokoll Nachrichtentypen:  
  
#### <a name="account-logon"></a>Kontoanmeldung  
  
##### <a name="credential-validation"></a>Überprüfung der Anmeldeinformationen  
Dieser Unterkategorie zeigt die Ergebnisse der Tests zur Überprüfung auf Anmeldeinformationen, die für eine anmeldeanforderung eines Benutzers Konto übermittelt. Diese Ereignisse treten auf dem Computer auf, der für die Anmeldeinformationen autoritativ ist. Bei Domänenkonten ist der Domänencontroller autoritativen, während für lokale Konten, der lokale Computer autorisierend ist.  
  
In domänenumgebungen werden die meisten der Anmeldeversuche im Sicherheitsprotokoll der Domänencontroller protokolliert, die für die Domänenkonten autorisierend sind. Allerdings können diese Ereignisse auf anderen Computern in der Organisation auftreten, wenn die lokale Konten zur Anmeldung verwendet werden.  
  
##### <a name="kerberos-service-ticket-operations"></a>Ticketvorgänge des Kerberos-Diensts  
Dieser Unterkategorie meldet Ereignisse, die vom Kerberos-Ticket Anforderung Prozesse auf dem Domänencontroller, der für das Domänenkonto autorisierend ist.  
  
##### <a name="kerberos-authentication-service"></a>Kerberos-Authentifizierungsdienst  
Dieser Unterkategorie meldet Ereignisse, die vom Kerberos Authentication-Dienst generiert. Diese Ereignisse treten auf dem Computer auf, der für die Anmeldeinformationen autoritativ ist.  
  
##### <a name="other-account-logon-events"></a>Andere Kontoanmeldungsereignisse  
Dieser Unterkategorie meldet die Ereignisse, die als Reaktion auf die Anmeldeinformationen für eine anmeldeanforderung eines Benutzers Konto übermittelt auftreten, die nicht auf die Überprüfung der Anmeldeinformationen oder Kerberos-Tickets beziehen. Diese Ereignisse treten auf dem Computer auf, der für die Anmeldeinformationen autoritativ ist. Bei Domänenkonten ist der Domänencontroller autoritativen, während für lokale Konten, der lokale Computer autorisierend ist.  
  
In domänenumgebungen werden die meisten Anmeldeversuche im Sicherheitsprotokoll der Domänencontroller protokolliert, die für die Domänenkonten autorisierend sind. Allerdings können diese Ereignisse auf anderen Computern in der Organisation auftreten, wenn die lokale Konten zur Anmeldung verwendet werden. Beispiele sind etwa:  
  
* Remote Desktop Services Session Trennvorgänge  
* Neue Remote Desktop Services-Sitzungen  
* Sperren und Entsperren einer Arbeitsstation  
* Aufrufen eines Bildschirmschoners  
* Schließen eines Bildschirmschoners  
* Erkennung von einem Kerberos replay-Angriff, in dem eine Kerberos-Anforderung mit identische Informationen zweimal empfangen wird  
* Gewähren des Zugriffs zu einem drahtlosen Netzwerk für ein Benutzer- oder Computerkonto  
* Gewähren des Zugriffs zu einem kabelgebundenen 802.1x-Netzwerk für ein Benutzer- oder Computerkonto  
  
#### <a name="account-management"></a>Kontenverwaltung  
  
##### <a name="user-account-management"></a>Benutzerkontenverwaltung  
Dieser Unterkategorie meldet jedes Ereignis der Verwaltung von Benutzerkonten, z. B. wenn ein Benutzerkonto erstellt, geändert oder gelöscht wird. ein Benutzerkonto ist umbenannt, deaktiviert oder aktiviert; oder ein Kennwort festgelegt oder geändert wird. Wenn diese richtlinieneinstellung für die Überwachung aktiviert ist, können Administratoren die Ereignisse überwachen, um böswillige versehentlichen und autorisierte Erstellung von Benutzerkonten zu erkennen.  
  
##### <a name="computer-account-management"></a>Computer-Kontoverwaltung  
Dieser Unterkategorie meldet jedes Ereignis von der Computer-kontoverwaltung, z. B. wenn ein Computerkonto erstellt, geändert, gelöscht, umbenannt, aktiviert oder deaktiviert ist, an.  
  
##### <a name="security-group-management"></a>Sicherheitsgruppenverwaltung  
Dieser Unterkategorie meldet jedes Ereignis der Verwaltung von Sicherheitsgruppen, wie z. B. wenn eine Sicherheitsgruppe erstellt, geändert oder gelöscht wird, oder wenn ein Element hinzugefügt oder aus einer Sicherheitsgruppe entfernt. Wenn diese richtlinieneinstellung für die Überwachung aktiviert ist, können Administratoren Ereignisse überwachen, um böswillige versehentlichen und autorisierte Erstellungen von Sicherheitsgruppenkonten sein.  
  
##### <a name="distribution-group-management"></a>Distribution-Gruppenverwaltung  
Dieser Unterkategorie meldet jedes Ereignis-verteilergruppenverwaltung, z. B. wenn eine Verteilergruppe erstellt, geändert oder gelöscht wird, oder wenn ein Element hinzugefügt oder aus einer Verteilergruppe entfernt. Wenn diese richtlinieneinstellung für die Überwachung aktiviert ist, können Administratoren Ereignisse überwachen, um böswillige versehentlichen und autorisierte Erstellung Gruppenkonten erkannt.  
  
##### <a name="application-group-management"></a>Application-Gruppenverwaltung  
Dieser Unterkategorie meldet jedes Ereignis der Gruppe anwendungsverwaltung auf einem Computer, z. B. wenn eine Anwendungsgruppe erstellt, geändert oder gelöscht wird, oder wenn ein Element hinzugefügt oder aus einer Anwendungsgruppe entfernt. Wenn diese richtlinieneinstellung für die Überwachung aktiviert ist, können Administratoren Ereignisse überwachen, um böswillige versehentlichen und autorisierte Erstellung Gruppenkonten für die Anwendung zu erkennen.  
  
##### <a name="other-account-management-events"></a>Andere Konto-Verwaltungsereignisse  
Dieser Unterkategorie meldet andere Konto-Verwaltungsereignisse.  
  
#### <a name="detailed-process-tracking"></a>Ausführliche überwachen  
  
##### <a name="process-creation"></a>Prozesserstellung  
Dieser Unterkategorie meldet die Erstellung eines Prozesses und den Namen des Benutzers oder der Anwendung, die sie erstellt haben.  
  
##### <a name="process-termination"></a>Prozessbeendigung  
Dieser Unterkategorie wird berichtet, wenn ein Prozess beendet wird.  
  
##### <a name="dpapi-activity"></a>DPAPI-Aktivität  
Dieser Unterkategorie meldet verschlüsseln oder Entschlüsseln von in die Data Protection Application programming Interface (DPAPI) aufruft. DPAPI wird verwendet, um geheime Informationen wie z. B. gespeicherte Kennwort und wichtige Informationen zu schützen.  
  
##### <a name="rpc-events"></a>RPC-Ereignisse  
Dieser Unterkategorie Berichte Remoteprozeduraufruf (RPC)-Verbindungsereignisse.  
  
#### <a name="directory-service-access"></a>Active Directory-Zugriff  
  
##### <a name="directory-service-access"></a>Active Directory-Zugriff  
Dieser Unterkategorie wird berichtet, wenn ein AD DS-Objekt zugegriffen wird. Nur Objekte mit konfigurierten SACLs dazu führen, dass Überwachungsereignisse werden generiert, und nur, wenn sie in einer Weise zugegriffen werden, die die SACL Einträge entspricht. Diese Ereignisse sind ähnlich wie die Directory-Dienst den Zugriff auf Ereignisse in früheren Versionen von Windows Server. Dieser Unterkategorie gilt nur für Domänencontroller.  
  
##### <a name="directory-service-changes"></a>Directory-Dienst geändert wird.  
Dieser Unterkategorie meldet Änderungen auf Objekte in AD DS. Die Arten von Änderungen, die gemeldet werden, sind erstellen, ändern, verschieben und Wiederherstellen von Vorgängen, die für ein Objekt ausgeführt werden. Änderung verzeichnisdienstüberwachung, falls zutreffend, gibt an, die alten und neuen Werte der geänderten Eigenschaften der Objekte, die geändert wurden. Nur Objekte mit SACLs dazu führen, dass Überwachungsereignisse werden generiert, und nur, wenn darauf in einer Weise zugegriffen wird, die ihre SACL Einträge entspricht. Einige Objekte und Eigenschaften lösen aufgrund der Einstellungen der Objektklasse im Schema keine Überwachungsereignisse aus. Dieser Unterkategorie gilt nur für Domänencontroller.  
  
##### <a name="directory-service-replication"></a>Replikation des Active Directory  
Dieser Unterkategorie wird berichtet, wenn die Replikation zwischen zwei Domänencontrollern beginnt und endet.  
  
##### <a name="detailed-directory-service-replication"></a>Detaillierte Verzeichnisdienstreplikation  
Dieser Unterkategorie meldet ausführliche Informationen zu den Informationen, die zwischen den Domänencontrollern repliziert werden. Diese Ereignisse können per Volumenlizenz sehr hoch sein.  
  
#### <a name="logonlogoff"></a>Anmeldung/Abmeldung  
  
##### <a name="logon"></a>Anmelden  
Dieser Unterkategorie wird berichtet, wenn ein Benutzer versucht, melden Sie sich an das System. Diese Ereignisse treten auf dem Computer zugegriffen werden. Tritt auf, die Generierung dieser Ereignisse auf dem Computer, der angemeldet ist, für die interaktive Anmeldung. Wenn eine Anmeldung am Netzwerk den Zugriff auf eine Dateifreigabe ausgeführt wird, generieren diese Ereignisse, auf dem Computer, der die verwendete Ressource hostet. Wenn diese Einstellung, um konfiguriert ist **keine Überwachung**, es ist schwierig oder unmöglich sein, um zu bestimmen, welcher Benutzer zugegriffen hat, oder es wurde versucht, den Zugriff auf Unternehmens-Computer.  
  
##### <a name="network-policy-server"></a>Netzwerkrichtlinienserver  
Dieser Unterkategorie gibt vom Benutzer-zugriffsanforderungen RADIUS (IAS) und (Network Access Protection, NAP) generierte Ereignisse. Diese Anforderungen möglich **Grant**, **Verweigern**, **verwerfen**, **Quarantäne**, **Sperre**, und **Nicht entsperren**. Überwachen diese Einstellung führt zu einem Volume mittlerem oder hohem von Datensätzen auf NPS- und IAS-Server.  
  
##### <a name="ipsec-main-mode"></a>IPsec-Hauptmodus  
Dieser Unterkategorie zeigt die Ergebnisse der Internetinformationsdienste (Internet Key Exchange, IKE)-Protokoll und Authenticated Internet Protocol (AuthIP), während der Hauptmodusaushandlungen.  
  
##### <a name="ipsec-extended-mode"></a>IPsec-Erweiterungsmodus  
Dieser Unterkategorie zeigt die Ergebnisse der AuthIP während der erweiterte Modus Aushandlungen.  
  
##### <a name="other-logonlogoff-events"></a>Andere Ereignisse Anmelden/Abmelden  
Dieser Unterkategorie meldet andere Anmeldung und Abmeldung Ereignisse, z. B. Remote Desktop Services Session getrennt und erneut eine Verbindung herstellt, mithilfe von RunAs Prozesse unter einem anderen Konto ausgeführt, Sperren und Entsperren einer Arbeitsstation.  
  
##### <a name="logoff"></a>Abmelden (Logoff)  
Dieser Unterkategorie wird berichtet, wenn das System ein Benutzer abmeldet. Diese Ereignisse treten auf dem Computer zugegriffen werden. Tritt auf, die Generierung dieser Ereignisse auf dem Computer, der angemeldet ist, für die interaktive Anmeldung. Wenn eine Anmeldung am Netzwerk den Zugriff auf eine Dateifreigabe ausgeführt wird, generieren diese Ereignisse, auf dem Computer, der die verwendete Ressource hostet. Wenn diese Einstellung, um konfiguriert ist **keine Überwachung**, es ist schwierig oder unmöglich sein, um zu bestimmen, welcher Benutzer zugegriffen hat, oder es wurde versucht, den Zugriff auf Unternehmens-Computer.  
  
##### <a name="account-lockout"></a>Kontosperrung  
Dieser Unterkategorie meldet, wenn es sich bei dem Konto eines Benutzers aufgrund zu vieler fehlerhafter Anmeldeversuche gesperrt ist.  
  
##### <a name="ipsec-quick-mode"></a>IPsec-Schnellmodus  
Dieser Unterkategorie zeigt die Ergebnisse der IKE-Protokoll und AuthIP während Schnellmodusaushandlungen.  
  
##### <a name="special-logon"></a>Spezielle Anmeldung  
Dieser Unterkategorie wird berichtet, wenn eine spezielle Anmeldung verwendet wird. Eine spezielle Anmeldung ist eine Anmeldung, die entsprechenden Administratorberechtigungen und kann verwendet werden, um einen Prozess auf einer höheren Ebene zu erhöhen.  
  
#### <a name="policy-change"></a>Richtlinienänderung  
  
##### <a name="audit-policy-change"></a>Richtlinienänderung überwachen  
Dieser Unterkategorie meldet Änderungen einschließlich SACL Änderungen Überwachungsrichtlinie.  
  
##### <a name="authentication-policy-change"></a>Authentifizierung-Richtlinienänderung  
Dieser Unterkategorie meldet Änderungen Authentifizierungsrichtlinie.  
  
##### <a name="authorization-policy-change"></a>Authorization-Richtlinienänderung  
Dieser Unterkategorie meldet Änderungen Autorisierungsrichtlinie einschließlich berechtigungsänderungen (Zugriffssteuerungsliste DACL).  
  
##### <a name="mpssvc-rule-level-policy-change"></a>MPSSVC Regelebene Richtlinienänderung  
Dieser Unterkategorie meldet Änderungen die Regeln, die von der Microsoft-Schutzdienst (MPSSVC.exe) verwendet. Dieser Dienst wird von der Windows-Firewall verwendet.  
  
##### <a name="filtering-platform-policy-change"></a>Filterplattform-Richtlinienänderung  
Dieser Unterkategorie meldet das Hinzufügen und Entfernen von Objekten von Windows-Dateischutz, einschließlich Startfilter. Diese Ereignisse können per Volumenlizenz sehr hoch sein.  
  
##### <a name="other-policy-change-events"></a>Andere Richtlinienänderungsereignisse  
Dieser Unterkategorie gibt andere Arten von Änderungen von Sicherheitsrichtlinien wie z. B. Konfiguration, der die Trusted Platform Module (TPM) oder den Kryptografieanbieter.  
  
#### <a name="privilege-use"></a>Verwendung von Berechtigungen  
  
##### <a name="sensitive-privilege-use"></a>Sensible Verwendung von rechten  
Dieser Unterkategorie wird berichtet, wenn ein Benutzerkonto oder Dienst verwendet eine vertrauliche Berechtigung. Die Berechtigungen einer vertraulichen umfasst die folgenden Berechtigungen: als Teil des Betriebssystems handeln "," Sichern von Dateien und Verzeichnissen "," Erstellen eines Tokenobjekts "," Debuggen von Programmen "," ermöglichen, Computer- und Benutzerkonten für Delegierungszwecke vertraut werden, Generieren von sicherheitsüberwachungen, Annehmen der Clientidentität nach Authentifizierung, laden und Entladen von Gerätetreibern, Verwalten von überwachungs- und Sicherheitsprotokollen, Firmwareumgebungsvariablen ändern, Ersetzen von Token auf Prozessebene, Wiederherstellen von Dateien und Verzeichnisse und Übernehmen des Besitzes von Dateien oder andere Objekte. Überwachung dieser Unterkategorie wird eine große Anzahl von Ereignissen erstellt werden.  
  
##### <a name="nonsensitive-privilege-use"></a>Nonsensitive Rechteverwendung  
Dieser Unterkategorie wird berichtet, wenn ein Benutzerkonto oder Dienst verwendet eine nonsensitive Berechtigung. Die Berechtigungen einer nonsensitive umfasst die folgenden Berechtigungen: Anmeldeinformations-Manager als vertrauenswürdigem Aufrufer zugreifen, auf diesen Computer vom Netzwerk aus zugreifen, Hinzufügen von Arbeitsstationen zur Domäne, Anpassen des arbeitsspeicherkontingents für einen Prozess, lokal anmelden zulassen, die über Remote anmelden zulassen Desktop Services, Auslassen von durchsuchenden Prüfungen, Ändern der Systemzeit, Erstellen einer Auslagerungsdatei, Erstellen globaler Objekte, dauerhafte freigegebene Objekten erstellen, erstellen Sie symbolische Verknüpfungen, den Zugriff auf diesen Computer vom Netzwerk verweigert, Anmelden als Batchauftrag verweigern, Anmelden als Dienst verweigern Lokal anmelden verweigern, Anmelden über Remotedesktopdienste verweigern, erzwingen des Herunterfahrens von einem Remotesystem, Arbeitssatz eines Prozesses, Anheben der Zeitplanungspriorität, Sperren von Seiten im Speicher, melden Sie sich als Batchauftrag, melden Sie sich als ein Dienst, verändern einer objektbezeichnung, Volume ausführen Wartungstasks Profils für einen Einzelprozess, profilerstellung für die Systemleistung, entfernen Sie Computer aus der Dockingstation, das System heruntergefahren und Synchronisieren von Verzeichnisdienstdaten. Überwachung dieser Unterkategorie wird eine sehr hohe Anzahl von Ereignissen erstellt werden.  
  
##### <a name="other-privilege-use-events"></a>Andere Rechteverwendungsereignisse  
Diese sicherheitseinstellung für die Richtlinie wird derzeit nicht verwendet.  
  
#### <a name="object-access"></a>Objektzugriff  
  
##### <a name="file-system"></a>Dateisystem  
Dieser Unterkategorie wird berichtet, wenn Dateisystemobjekte zugegriffen werden. Systemobjekte nur über die Systemzugriffssteuerungslisten Datei dazu führen, dass Überwachungsereignisse werden generiert, und nur, wenn in einer Weise, die übereinstimmende die SACL-Einträge darauf zugegriffen werden. Selbst wird mit dieser richtlinieneinstellung wird nicht dazu führen, dass Überwachung von Ereignissen. Sie bestimmt, ob das Ereignis eines Benutzers zu überwachen, die ein Dateisystemobjekt zugreift, die eine angegebene System-Zugriffssteuerungsliste (SACL) effektiv das Aktivieren der Überwachung stattfinden soll.  
  
Wenn die Überwachung von Objektzugriffsversuchen Einstellung konfiguriert ist **Erfolg**, ein Überwachungseintrag wird immer generiert, wenn ein Benutzer erfolgreich ein Objekt mit einer angegebenen SACL zugreift. Wenn diese richtlinieneinstellung konfiguriert ist **Fehler**, ein Überwachungseintrag wird jedes Mal, die ein Benutzer Zugriff auf ein Objekt mit einer angegebenen SACL versuchen nicht generiert.  
  
##### <a name="registry"></a>Registrierung  
Dieser Unterkategorie wird berichtet, wenn die Registrierungsobjekte zugegriffen wird. Nur Registrierungsobjekte über die Systemzugriffssteuerungslisten dazu führen, dass Überwachungsereignisse werden generiert, und nur, wenn in einer Weise, die übereinstimmende die SACL-Einträge darauf zugegriffen werden. Selbst wird mit dieser richtlinieneinstellung wird nicht dazu führen, dass Überwachung von Ereignissen.  
  
##### <a name="kernel-object"></a>Kernel-Objekt  
Dieser Unterkategorie wird berichtet, wenn der Kernel-Objekttypen, z. B. Prozesse und Mutexe zugegriffen werden. Nur über die Systemzugriffssteuerungslisten Kernelobjekte dazu führen, dass Überwachungsereignisse werden generiert, und nur, wenn in einer Weise, die übereinstimmende die SACL-Einträge darauf zugegriffen werden. Kernel-Objekttypen werden in der Regel nur SACLs angegeben, wenn die Überwachung AuditBaseObjects oder AuditBaseDirectories-Optionen aktiviert sind.  
  
##### <a name="sam"></a>SAM  
Dieser Unterkategorie wird berichtet, wenn lokale Sicherheitskontenverwaltung (Security Accounts Manager, SAM)-Authentifizierung-Datenbankobjekte zugegriffen wird.  
  
##### <a name="certification-services"></a>Zertifikatdienste  
Dieser Unterkategorie wird berichtet, wenn Zertifizierungsdienste Vorgänge ausgeführt werden.  
  
##### <a name="application-generated"></a>Anwendung generiert  
Dieser Unterkategorie wird berichtet, wenn Anwendungen versuchen, Überwachungsereignisse zu generieren, indem Sie mithilfe der Windows-Überwachung Anwendungsprogrammierschnittstellen (APIs).  
  
##### <a name="handle-manipulation"></a>Handleänderung  
Dieser Unterkategorie wird berichtet, wenn ein Handle für ein Objekt geöffnet bzw. geschlossen wird. Nur Objekte mit SACLs dazu führen, dass diese Ereignisse werden generiert, und nur dann, wenn der versuchte handlevorgang die SACL Einträge entspricht. Handle Manipulation-Ereignisse werden nur für Objekte des Typs generiert, die die Unterkategorie der entsprechenden Objekt zugreifen (z. B. "," Dateisystem "oder" Registrierung ") aktiviert ist.  
  
##### <a name="file-share"></a>Dateifreigabe  
Dieser Unterkategorie wird berichtet, wenn eine Dateifreigabe zugegriffen wird. Selbst wird mit dieser richtlinieneinstellung wird nicht dazu führen, dass Überwachung von Ereignissen. Sie bestimmt, ob das Ereignis eines Benutzers zu überwachen, die ein File-Freigabe-Objekt zugegriffen wird, die eine angegebene System-Zugriffssteuerungsliste (SACL), hat effektiv das Aktivieren der Überwachung stattfinden soll.  
  
##### <a name="filtering-platform-packet-drop"></a>Filterplattform: Verworfene Pakete  
Dieser Unterkategorie wird berichtet, wenn Sie Pakete von Windows-Filterplattform (WFP) gelöscht werden. Diese Ereignisse können per Volumenlizenz sehr hoch sein.  
  
##### <a name="filtering-platform-connection"></a>Filtern von Platform-Verbindung  
Dieser Unterkategorie wird berichtet, wenn Verbindungen zugelassen oder werden von Windows-Dateischutz blockiert. Diese Ereignisse können per Volumenlizenz hoch sein.  
  
##### <a name="other-object-access-events"></a>Andere Objektzugriffsereignisse  
Dieser Unterkategorie meldet andere Objekt zugreifen auf verwandte Ereignisse wie Task Scheduler-Aufträge und COM+-Objekte.  
  
#### <a name="system"></a>System  
  
##### <a name="security-state-change"></a>Ändern des Sicherheitsstatus  
Dieser Unterkategorie meldet Änderungen in den Sicherheitszustand des Systems, z. B. wenn das Subsystem startet und beendet.  
  
##### <a name="security-system-extension"></a>System-Sicherheitserweiterungen  
Dieser Unterkategorie meldet das Laden der Erweiterungscode, z. B. Authentifizierungspaketen durch das Sicherheitssubsystem.  
  
##### <a name="system-integrity"></a>Integrität des Systems  
Dieser Unterkategorie berichtet über Verletzungen der Integrität des Subsystems, Sicherheit.  
  
IPSec-Treiber  
  
Dieser Unterkategorie berichtet über die Aktivitäten des Treibers Internet Protocol Security (IPsec).  
  
##### <a name="other-system-events"></a>Andere Systemereignisse  
Dieser Unterkategorie berichtet über andere Systemereignisse.  
  
Weitere Informationen zu den Unterkategorie-Beschreibungen, finden Sie in der [Microsoft Security Compliance Manager-Tool](https://technet.microsoft.com/library/cc677002.aspx).  
  
Jede Organisation sollte überprüfen Sie die vorherigen, abgedeckte Kategorien und Unterkategorien, und aktivieren diejenigen, die am besten für ihre Umgebung geeignet. Änderungen an der Richtlinie zu überwachen, sollten immer vor der Bereitstellung in einer produktionsumgebung getestet werden.  
  
## <a name="configuring-windows-audit-policy"></a>Konfigurieren von Windows-Überwachungsrichtlinie

Windows-Überwachungsrichtlinie kann mithilfe von Richtlinien, auditpol.exe, APIs oder ein Registrierungsschlüsselwert Änderungen von Gruppe festgelegt werden. Die empfohlenen Methoden für die Konfiguration der Überwachungsrichtlinie für die meisten Unternehmen sind Gruppenrichtlinien oder auditpol.exe. Festlegen der Überwachungsrichtlinie eines Systems ist erforderlich, Berechtigungen auf Administratorebene oder die entsprechenden delegierte Berechtigungen.  
  
> [!NOTE]  
> Die **Verwalten von überwachungs- und Sicherheitsprotokollen** muss Berechtigungen von Sicherheitsprinzipalen gewährt werden (Administratoren haben sie standardmäßig) um die Änderung der Objektzugriff Überwachungsoptionen von einzelnen Ressourcen, z. B. Dateien, aktiv zu ermöglichen. Verzeichnisobjekte und Registrierungsschlüssel.  
  
### <a name="setting-windows-audit-policy-by-using-group-policy"></a>Einstellung: Windows-Überwachungsrichtlinie mithilfe von Gruppenrichtlinien

Zum Festlegen der Überwachungsrichtlinie mithilfe von Gruppenrichtlinien konfigurieren Sie die entsprechenden Überwachungskategorien befindet sich im **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\überwachungsrichtlinie** (Siehe im folgenden Screenshot ein Beispiel: aus dem Editor für lokale Gruppenrichtlinien (gpedit.msc)). Jede Richtlinienkategorie Überwachung kann aktiviert werden, für die **Erfolg**, **Fehler**, oder **Erfolg** und Fehlerereignisse.  
  
![Überwachung von Active Directory](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_6.gif)  
  
Erweiterte Überwachungsrichtlinie kann festgelegt werden, mithilfe von Active Directory oder lokale Gruppenrichtlinien. Zum Festlegen der erweiterten Überwachungsrichtlinie konfigurieren Sie die entsprechenden Unterkategorien befindet sich im **Computerkonfiguration\Windows-einstellungen\sicherheitseinstellungen\erweiterte Audit Richtlinie** (Siehe der folgende Screenshot enthält ein Beispiel aus der lokalen Editor für Gruppenrichtlinien (gpedit.msc)). Jede Unterkategorie der Überwachungsrichtlinie kann aktiviert werden, für die **Erfolg**, **Fehler**, oder **Erfolg** und **Fehler** Ereignisse.  
  
![Überwachung von Active Directory](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_7.gif)  
  
### <a name="setting-windows-audit-policy-using-auditpolexe"></a>Einstellung Windows-Überwachungsrichtlinie mithilfe von Auditpol.exe

Auditpol.exe (zum Festlegen der Windows-Überwachungsrichtlinie) wurde in Windows Server 2008 und Windows Vista eingeführt. Anfangs nur auditpol.exe verwendet werden, um die erweiterten Überwachungsrichtlinie festlegen, aber der Gruppenrichtlinie in Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008, Windows 8 und Windows 7 verwendet werden können.  
  
Auditpol.exe ist ein Befehlszeilen-Hilfsprogramm. Die Syntax lautet wie folgt aus:  
  
`auditpol /set /<Category|Subcategory>:<audit category> /<success|failure:> /<enable|disable>`
  
Auditpol.exe Syntaxbeispiele:  
  
`auditpol /set /subcategory:"user account management" /success:enable /failure:enable`
  
`auditpol /set /subcategory:"logon" /success:enable /failure:enable`
  
`auditpol /set /subcategory:"IPSEC Main Mode" /failure:enable`
  
> [!NOTE]  
> Auditpol.exe legt die erweiterte Überwachungsrichtlinie lokal fest. Wenn lokale Richtlinie mit Active Directory oder lokale Gruppenrichtlinien in Konflikt steht, werden die gruppenrichtlinieneinstellungen in der Regel auditpol.exe Einstellungen Vorrang. Wenn mehrere Gruppe oder lokale Richtlinienkonflikte vorhanden sind, wird nur eine Richtlinie Vorrang (die ersetzt wird). Richtlinien werden nicht zusammengeführt.  
  
#### <a name="scripting-auditpol"></a>Skript "auditpol"

Microsoft bietet eine [Beispielskript](https://support.microsoft.com/kb/921469) für Administratoren mit der erweiterten Überwachungsrichtlinie festlegen, mithilfe eines Skripts verwenden, anstatt Sie in jedem Befehl auditpol.exe manuell eingeben möchten.  
  
**Beachten Sie** Gruppenrichtlinien immer genau meldet nicht den Status der Überwachungsrichtlinien für alle, aktiviert, während auditpol.exe der Fall ist. Finden Sie unter [Abrufen der effektiven Überwachungsrichtlinie in Windows 7 und Windows 2008 R2](http://blogs.technet.com/b/askds/archive/2011/03/11/getting-the-effective-audit-policy-in-windows-7-and-2008-r2.aspx) Weitere Details.  
  
#### <a name="other-auditpol-commands"></a>Andere Befehle "auditpol"

Auditpol.exe kann verwendet werden, speichern und Wiederherstellen von einer Richtlinie für die lokale Überwachung und andere verwandte Überwachungsbefehle anzuzeigen. Hier sind die anderen **"auditpol"** Befehle.  
  
`auditpol /clear` -Wird verwendet, um das Löschen und die lokale Überwachungsrichtlinien zur Kennwortrücksetzung  
  
`auditpol /backup /file:<filename>` -Wird verwendet, um eine aktuelle Richtlinie für die lokale Überwachung in eine binäre Datei sichern  
  
`auditpol /restore /file:<filename>` -Wird verwendet, um eine zuvor gespeicherte Richtlinie Überwachungsdatei in eine Richtlinie für die lokale Überwachung zu importieren.  
  
`auditpol /<get/set> /option:<CrashOnAuditFail> /<enable/disable>` – Wenn diese richtlinieneinstellung für die Überwachung aktiviert ist, wird das System sofort zu beenden (Beenden: C0000244 {Überwachungsfehlgeschlagen} Nachricht) kann nicht, wenn eine sicherheitsüberwachung aus irgendeinem Grund protokolliert werden. In der Regel ein Ereignis protokolliert wird, wenn das Sicherheitsüberwachungsprotokoll voll ist, und die Retention-Methode angegeben, für das Sicherheitsprotokoll ist nicht **Ereignisse nicht überschreiben** oder **Ereignisse überschreiben, um Tage**. In der Regel ist sie nur in Umgebungen aktiviert, die höhere benötigen, die das Sicherheitsprotokoll protokolliert wird. Wenn aktiviert, müssen Administratoren genau überwachen der Größe des Sicherheitsprotokolls und Rotieren von Protokollen nach Bedarf. Es kann auch mit einer Gruppenrichtlinie festgelegt werden, durch Ändern der Sicherheitsoption **überwachen: Herunterfahren des Systems sofort, wenn Sie nicht von sicherheitsüberwachungen anmelden** (Standardeinstellung = deaktiviert).  
  
`auditpol /<get/set> /option:<AuditBaseObjects> /<enable/disable>` -Diese Einstellung für Überwachungsrichtlinien bestimmt, ob den Zugriff auf globale Systemobjekte zu überwachen. Wenn diese Richtlinie aktiviert ist, bewirkt, dass sie Systemobjekte, wie z. B. Mutexe, Semaphoren, Ereignisse und DOS-Geräte mit einem Standard-Systemzugriffssteuerungsliste (SACL) erstellt werden. Die meisten Administratoren sollten Sie globale Systemobjekte aus, um Sie zu "entsprechende abweichungen auf," Überwachung und werden sie nur dann aktivieren, wenn ein Verdacht auf bösartige Hackerangriffe. Nur benannte Objekte werden eine SACL angegeben. Wenn die Überwachung Objekt Zugriff Audit-Richtlinie (oder Kernelobjekt Überwachungsunterkategorie) auch aktiviert ist, wird den Zugriff auf Systemobjekte überwacht. Wenn Sie diese Einstellung zu konfigurieren, werden Änderungen nicht wirksam, bis zum Neustart von Windows. Diese Richtlinie kann auch mit einer Gruppenrichtlinie festgelegt werden, indem Sie die Sicherheitsoption Zugriff auf globale Systemobjekte ändern (Standard = deaktiviert).  
  
`auditpol /<get/set> /option:<AuditBaseDirectories> /<enable/disable>` -Diese Einstellung für Überwachungsrichtlinien gibt an, dass benannte Kernelobjekte (z. B. Mutexe und Semaphoren) SACLs angegeben werden, wenn sie erstellt werden. AuditBaseDirectories betrifft Containerobjekte AuditBaseObjects Objekte, die andere Objekte enthalten können.  
  
`auditpol /<get/set> /option:<FullPrivilegeAuditing> /<enable/disable>` -Diese Einstellung für Überwachungsrichtlinien gibt an, ob der Client generiert ein Ereignis, wenn eine oder mehrere der folgenden Berechtigungen ein Benutzersicherheitstoken zugewiesen sind: AssignPrimaryTokenPrivilege, AuditPrivilege, BackupPrivilege, CreateTokenPrivilege, DebugPrivilege, EnableDelegationPrivilege, ImpersonatePrivilege, LoadDriverPrivilege, RestorePrivilege, SecurityPrivilege, SystemEnvironmentPrivilege, TakeOwnershipPrivilege und TcbPrivilege. Wenn diese Option nicht aktiviert ist (Standardeinstellung = deaktiviert), die Berechtigungen BackupPrivilege und RestorePrivilege nicht aufgezeichnet werden. Durch Aktivieren dieser Option können Sie das Sicherheitsprotokoll extrem noisy (manchmal Hunderte von Ereignissen pro Sekunde) während eines Sicherungsvorgangs vornehmen. Diese Richtlinie kann auch mit einer Gruppenrichtlinie festgelegt werden, durch Ändern der Sicherheitsoption **überwachen: Überwachen Sie die Verwendung von Sicherungs- und wiederherstellungsrechts**.  
  
> [!NOTE]  
> Einige der hier bereitgestellten Informationen stammt aus dem Microsoft [Option Überwachungstyp](https://msdn.microsoft.com/library/dd973862(prot.20).aspx) und das Microsoft SCM-Tool.  
  
## <a name="enforcing-traditional-auditing-or-advanced-auditing"></a>Erzwingen von herkömmlichen Überwachungs- oder erweiterte Überwachung

In Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows 8, Windows 7 und Windows Vista können Administratoren auswählen, zu der herkömmlichen neun Kategorien oder Unterkategorien zu verwenden. Es ist eine binäre Option, die auf jedem Windows-System vorgenommen werden muss. Die Hauptkategorien können aktiviert werden, oder die Subcategoriesit kann nicht gleichzeitig.  
  
Um zu verhindern, dass die ältere herkömmliche Kategorierichtlinie Überwachungsrichtlinien-Unterkategorien zu überschreiben, müssen Sie aktivieren die **unterkategorieeinstellungen der Überwachung (Windows Vista oder höher) um kategorieeinstellungen der Überwachungsrichtlinie außer Kraft setzen** richtlinieneinstellung befindet sich im **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\sicherheitsoptionen**.  
  
Es wird empfohlen, dass die Unterkategorien aktiviert und konfiguriert werden, anstatt die neun Hauptkategorien unterteilt werden. Dies erfordert, dass eine gruppenrichtlinieneinstellung aktiviert werden (damit Unterkategorien der Überwachungskategorien überschreiben zu können) sowie das Konfigurieren der verschiedenen Unterkategorien, die Überwachungsrichtlinien zu unterstützen.  
  
Überwachung von Unterkategorien kann mithilfe mehrerer Methoden, einschließlich der Gruppenrichtlinie und das Befehlszeilenprogramm, auditpol.exe konfiguriert werden.  
  
## <a name="next-steps"></a>Nächste Schritte
  
* [Erweiterte Sicherheitsüberprüfung in Windows 7 und Windows Server 2008 R2](https://social.technet.microsoft.com/wiki/contents/articles/advanced-security-auditing-in-windows-7-and-windows-server-2008-r2.aspx)  
  
* [Überwachung und Compliance in WindowsServer 2008](https://technet.microsoft.com/magazine/2008.03.auditing.aspx)  
  
* [Wie Sie mithilfe von Gruppenrichtlinien zum Konfigurieren von detaillierten sicherheitsüberwachungseinstellungen für Windows Vista und Windows Server 2008-basierten Computer in einer Windows Server 2008-Domäne, in einer Windows Server 2003-Domäne oder in einer Windows 2000-Domäne](https://support.microsoft.com/kb/921469)  
  
* [Advanced Security Audit-Richtlinie schrittweise Anleitung](https://technet.microsoft.com/library/dd408940(WS.10).aspx)  
