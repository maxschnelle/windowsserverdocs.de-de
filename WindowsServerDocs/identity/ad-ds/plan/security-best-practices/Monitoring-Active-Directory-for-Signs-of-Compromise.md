---
ms.assetid: a7ef2fba-b05c-4be2-93b2-b9456244c3ad
title: Überwachen von Active Directory auf Anzeichen für einen Kompromiss
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 8b28d412411336062187a842912b6f4a41957eba
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87994345"
---
# <a name="monitoring-active-directory-for-signs-of-compromise"></a>Überwachen von Active Directory auf Anzeichen für einen Kompromiss

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*Gesetzes Nummer fünf: die ewige Wachsamkeit ist der Preis der Sicherheit.* - [10 unveränderliche Gesetze der Sicherheitsverwaltung](/previous-versions/cc722488(v=technet.10))

Ein Solid-Ereignisprotokoll-Überwachungssystem ist ein wichtiger Bestandteil jedes sicheren Active Directory Entwurfs. Viele Computer Sicherheits Kompromisse könnten frühzeitig erkannt werden, wenn die Opfer die entsprechende Überwachung und Warnungen für das Ereignisprotokoll erlassen haben. Diese Schlussfolgerung wird von unabhängigen Berichten lange unterstützt. Beispielsweise gibt der [2009 Verizon-Daten Verletzungs Bericht](http://www.verizonbusiness.com/resources/security/reports/2009_databreach_rp.pdf) Folgendes an:

"Die offensichtliche Ineffektivität der Ereignisüberwachung und der Protokollanalyse ist weiterhin etwas von einem Rätsel. Die Möglichkeit zur Erkennung ist: die Forscher haben festgestellt, dass 66 Prozent der Opfer in Ihren Protokollen über ausreichende Beweise verfügen, um die Verletzung zu ermitteln, was bei der Analyse solcher Ressourcen noch sorgfältiger war. "

Diese fehlende Überwachung von aktiven Ereignisprotokollen bleibt in den Sicherheits Verteidigungs Plänen vieler Unternehmen eine konsistente Schwachstelle. Der [Bericht "2012 Verizon-Datenverletzung](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf) " hat festgestellt, dass es bei 84 Prozent der Opfer zu einer Sicherheitsverletzung in den Ereignisprotokollen gekommen ist, obwohl 85 Prozent der Verstöße einige Wochen in Anspruch genommen haben.

## <a name="windows-audit-policy"></a>Windows-Überwachungsrichtlinie

Im folgenden finden Sie Links zum Microsoft Official Enterprise Support-Blog. Der Inhalt dieser Blogs bietet Ratschläge, Anleitungen und Empfehlungen zur Überwachung, die Sie bei der Verbesserung der Sicherheit Ihrer Active Directory Infrastruktur unterstützen und eine wertvolle Ressource beim Entwerfen einer Überwachungsrichtlinie sind.

* Die [globale Objekt Zugriffs Überwachung ist magisch](/archive/blogs/askds/global-object-access-auditing-is-magic) : Beschreibt einen Steuerungsmechanismus namens erweiterte Überwachungs Richtlinien Konfiguration, der Windows 7 und Windows Server 2008 R2 hinzugefügt wurde, mit der Sie festlegen können, welche Typen von Daten Sie problemlos überwachen möchten, und die Skripts und auditpol.exe nicht jonglieren.
* [Einführung von Überwachungs Änderungen in Windows 2008](/archive/blogs/askds/introducing-auditing-changes-in-windows-2008) : führt die in Windows Server 2008 vorgenommenen Überwachungs Änderungen ein.
* Praktische Überwachungs [Tricks in Vista und 2008](/archive/blogs/askds/cool-auditing-tricks-in-vista-and-2008) : erläutert interessante Überwachungs Features von Windows Vista und Windows Server 2008, die für die Problembehandlung oder das Auftreten von Ereignissen in Ihrer Umgebung verwendet werden können.
* [Zentrale Anlaufstelle für die Überwachung in Windows Server 2008 und Windows Vista](/archive/blogs/askds/one-stop-shop-for-auditing-in-windows-server-2008-and-windows-vista) : enthält eine Kompilierung von Überwachungs Features und Informationen, die in Windows Server 2008 und Windows Vista enthalten sind.

Die folgenden Links enthalten Informationen zu Verbesserungen der Windows-Überwachung in Windows 8 und Windows Server 2012 sowie Informationen zur AD DS Überwachung in Windows Server 2008.

* [Neues bei der Sicherheits](/previous-versions/orphan-topics/ws.11/hh849638(v=ws.11)) Überwachung: bietet eine Übersicht über die neuen Sicherheits Überprüfungs Features in Windows 8 und Windows Server 2012.
* [Schritt-für-Schritt-Anleitung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731607(v=ws.10)) für die AD DS Überwachung: Beschreibt das neue Active Directory Domain Services (AD DS)-Überwachungs Feature in Windows Server 2008. Außerdem werden Verfahren zur Implementierung dieses neuen Features bereitstellt.

### <a name="windows-audit-categories"></a>Windows-Überwachungs Kategorien

Vor Windows Vista und Windows Server 2008 verfügte Windows nur über neun Kategorien von Ereignisprotokoll-Überwachungs Richtlinien:

* Konto Anmelde Ereignisse
* Kontoverwaltung
* Verzeichnisdienst Zugriff
* Anmelde Ereignisse
* Objektzugriff
* Richtlinienänderung
* Berechtigungen
* Prozess Nachverfolgung
* System Ereignisse

Diese neun herkömmlichen Überwachungs Kategorien bestehen aus einer Überwachungsrichtlinie. Jede Überwachungs Richtlinien Kategorie kann für Erfolgs-, Fehler-oder Erfolgs-und Fehlerereignisse aktiviert werden. Ihre Beschreibungen sind im nächsten Abschnitt enthalten.

#### <a name="audit-policy-category-descriptions"></a>Beschreibungen der Kategorien der Überwachungsrichtlinie
Die Kategorien der Überwachungs Richtlinien ermöglichen die folgenden Ereignisprotokoll-Nachrichten Typen.

##### <a name="audit-account-logon-events"></a>Konto Anmelde Ereignisse überwachen
Meldet jede Instanz eines Sicherheits Prinzipals (z. b. Benutzer, Computer oder Dienst Konto), die sich bei einem Computer anmeldet, bei dem ein anderer Computer verwendet wird, um das Konto zu überprüfen. Konto Anmelde Ereignisse werden generiert, wenn ein Domänen Sicherheits Prinzipal Konto auf einem Domänen Controller authentifiziert wird. Bei der Authentifizierung eines lokalen Benutzers auf einem lokalen Computer wird ein Anmelde Ereignis generiert, das im lokalen Sicherheitsprotokoll protokolliert wird. Es werden keine Konto Abmelde Ereignisse protokolliert.

Diese Kategorie generiert ein hohes Maß an "Rauschen", da Windows sich ständig im normalen Geschäftsbetrieb auf dem lokalen Computer und dem Remote Computer anmeldet. Dennoch sollte jeder Sicherheitsplan den Erfolg und das Fehlschlagen dieser Überwachungs Kategorie einschließen.

##### <a name="audit-account-management"></a>Kontoverwaltung überwachen
Diese Überwachungs Einstellung bestimmt, ob die Verwaltung von Benutzern und Gruppen nachverfolgt wird. Benutzer und Gruppen sollten z. b. nachverfolgt werden, wenn ein Benutzer-oder Computer Konto, eine Sicherheitsgruppe oder eine Verteiler Gruppe erstellt, geändert oder gelöscht wird. Wenn ein Benutzer-oder Computer Konto umbenannt, deaktiviert oder aktiviert wird. oder wenn ein Benutzer-oder Computer Kennwort geändert wird. Ein Ereignis kann für Benutzer oder Gruppen generiert werden, die hinzugefügt oder aus anderen Gruppen entfernt werden.

##### <a name="audit-directory-service-access"></a>Verzeichnisdienstzugriff überwachen

Mit dieser Richtlinien Einstellung wird festgelegt, ob der Sicherheits Prinzipal Zugriff auf ein Active Directory Objekt überwachen soll, das über eine eigene angegebene System Zugriffs Steuerungs Liste (SACL) verfügt. Im Allgemeinen sollte diese Kategorie nur auf Domänen Controllern aktiviert werden. Wenn diese Einstellung aktiviert ist, wird viel "Rauschen" generiert.

##### <a name="audit-logon-events"></a>Anmelde Ereignisse überwachen
Anmelde Ereignisse werden generiert, wenn ein lokaler Sicherheits Prinzipal auf einem lokalen Computer authentifiziert wird. Anmelde Ereignisse erfasst Domänen Anmeldungen, die auf dem lokalen Computer ausgeführt werden. Kontoabmeldeereignisse werden nicht generiert. Wenn diese Option aktiviert ist, werden bei Anmelde Ereignissen viele "Geräusche" generiert, Sie sollten jedoch standardmäßig in jedem Sicherheits Prüfungsplan aktiviert werden.

##### <a name="audit-object-access"></a>Überwachen des Objekt Zugriffs
Der Objektzugriff kann Ereignisse generieren, wenn auf anschließend definierte Objekte zugegriffen wird, für die die Überwachung aktiviert ist (z. b. öffnen, lesen, umbenennen, löschen oder schließen). Nachdem die Haupt Überwachungs Kategorie aktiviert ist, muss der Administrator einzeln definieren, für welche Objekte die Überwachung aktiviert wird. Bei vielen Windows-System Objekten wird die Überwachung aktiviert. Daher beginnt die Aktivierung dieser Kategorie in der Regel damit, Ereignisse zu generieren, bevor der Administrator eine beliebige definiert hat.

Diese Kategorie ist äußerst "noisy" und generiert fünf bis zehn Ereignisse für jeden Objektzugriff. Es kann schwierig sein, die Objektüberwachung für Administratoren neu zu machen, um nützliche Informationen zu erhalten. Sie sollte nur bei Bedarf aktiviert werden.

##### <a name="auditing-policy-change"></a>Überwachen der Richtlinien Änderung
Mit dieser Richtlinien Einstellung wird festgelegt, ob jedes Auftreten einer Änderung an Benutzerrechte Zuweisungs Richtlinien, Windows-Firewall-Richtlinien, Vertrauensstellungs Richtlinien oder Änderungen an der Überwachungsrichtlinie überprüft werden soll. Diese Kategorie sollte auf allen Computern aktiviert werden. Er erzeugt sehr wenig Rauschen.

##### <a name="audit-privilege-use"></a>Verwendung von Überwachungs Berechtigungen

Es gibt Dutzende von Benutzerrechten und-Berechtigungen in Windows (z. b. als Batch Auftrag anmelden und als Teil des Betriebssystems fungieren). Mit dieser Richtlinien Einstellung wird festgelegt, ob jede Instanz eines Sicherheits Prinzipals überprüft werden soll, indem ein Benutzerrecht oder eine Berechtigung für Sie Das Aktivieren dieser Kategorie führt zu einem hohen "Rauschen", aber es kann hilfreich sein, um Sicherheits Prinzipal Konten mithilfe erweiterter Berechtigungen zu überwachen.

##### <a name="audit-process-tracking"></a>Überwachungsprozess Verfolgung
Mit dieser Richtlinien Einstellung wird festgelegt, ob ausführliche Prozess nach Verfolgungs Informationen für Ereignisse wie Programm Aktivierung, Prozess Beendigung, Duplizierung von Objekten und indirekter Objektzugriff überwacht werden sollen. Es ist nützlich, wenn böswillige Benutzer und die von Ihnen verwendeten Programme nachverfolgt werden.

Durch das Aktivieren der Überwachungsprozess Verfolgung wird eine große Anzahl von Ereignissen generiert, sodass Sie in der Regel auf **keine**Überwachung festgelegt ist. Diese Einstellung kann jedoch während einer Reaktion auf Vorfälle aus dem detaillierten Protokoll der gestarteten Prozesse und der Startzeit des Starts einen großen Vorteil bieten. Für Domänen Controller und andere Infrastruktur Server mit nur einer Rolle kann diese Kategorie sicher jederzeit aktiviert werden. Einzelne Rollen Server generieren im normalen Verlauf ihrer Aufgaben keinen großen Prozess nach Verfolgungs Datenverkehr. Daher können Sie aktiviert werden, um nicht autorisierte Ereignisse zu erfassen, wenn Sie auftreten.

##### <a name="system-events-audit"></a>Überwachung von System Ereignissen

System Ereignisse sind fast eine generische Catch-All-Kategorie, bei der verschiedene Ereignisse registriert werden, die Auswirkungen auf den Computer, die Systemsicherheit oder das Sicherheitsprotokoll haben. Es umfasst Ereignisse für das Herunterfahren und Neustarten von Computern, Stromausfälle, Systemzeit Änderungen, Authentifizierungs Paket Initialisierungen, Überprüfungen des Überwachungs Protokolls, Identitätswechsel Probleme und einen Host anderer allgemeiner Ereignisse. Im allgemeinen generiert die Aktivierung dieser Überwachungs Kategorie viel "Rauschen", aber Sie generiert genug sehr nützliche Ereignisse, die nicht jemals empfohlen werden, Sie zu aktivieren.

#### <a name="advanced-audit-policies"></a>Erweiterte Überwachungs Richtlinien

Ab Windows Vista und Windows Server 2008 hat Microsoft die Auswahlmöglichkeiten für die Ereignisprotokoll Kategorie verbessert, indem Unterkategorien unter jeder Haupt Überwachungs Kategorie erstellt werden. Unterkategorien ermöglichen eine weitaus differenziertere Überwachung, als andernfalls die Hauptkategorien. Mithilfe von Unterkategorien können Sie nur Teile einer bestimmten Hauptkategorie aktivieren und das Erstellen von Ereignissen, für die Sie keine Verwendung haben, überspringen. Jede Unterkategorie der Überwachungsrichtlinie kann für Ereignisse durch Erfolg, Fehler oder Erfolg und Fehler aktiviert werden.

Überprüfen Sie zum Auflisten aller verfügbaren Überwachungs Unterkategorien den erweiterten Überwachungs Richtlinien Container in einem Gruppenrichtlinie Objekt, oder geben Sie an einer Eingabeaufforderung auf einem beliebigen Computer unter Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008, Windows 8, Windows 7 oder Windows Vista Folgendes ein:

`auditpol /list /subcategory:*`

Geben Sie Folgendes ein, um eine Liste der derzeit konfigurierten Überwachungs Unterkategorien auf einem Computer zu erhalten, auf dem Windows Server 2012, Windows Server 2008 R2 oder Windows 2008 ausgeführt wird:

`auditpol /get /category:*`

Der folgende Screenshot zeigt ein Beispiel für das auditpol.exe Auflisten der aktuellen Überwachungsrichtlinie.

![Überwachen von AD](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_5.gif)

> [!NOTE]
> Gruppenrichtlinie gibt nicht immer genau den Status aller aktivierten Überwachungs Richtlinien aus, wohingegen auditpol.exe. Weitere Informationen finden Sie [unter erhalten der effektiven Überwachungsrichtlinie in Windows 7 und 2008 R2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731607(v=ws.10)) .

Jede Hauptkategorie verfügt über mehrere Unterkategorien. Im folgenden finden Sie eine Liste der Kategorien, ihrer Unterkategorien und eine Beschreibung ihrer Funktionen.

### <a name="auditing-subcategories-descriptions"></a>Beschreibungen von Unterkategorien überwachen
Unterkategorien der Überwachungsrichtlinie aktivieren die folgenden Ereignisprotokoll-Nachrichten Typen:

#### <a name="account-logon"></a>Kontoanmeldung

##### <a name="credential-validation"></a>Überprüfung der Anmeldeinformationen
Diese Unterkategorie meldet die Ergebnisse von Validierungstests bei Anmelde Informationen, die für eine Benutzerkonto-Anmelde Anforderung gesendet wurden. Diese Ereignisse treten auf dem Computer auf, der für die Anmeldeinformationen autoritativ ist. Bei Domänen Konten ist der Domänen Controller autorisierend, während für lokale Konten der lokale Computer autorisierend ist.

In Domänen Umgebungen werden die meisten Konto Anmelde Ereignisse im Sicherheitsprotokoll der Domänen Controller protokolliert, die für die Domänen Konten autorisierend sind. Diese Ereignisse können jedoch auf anderen Computern in der Organisation auftreten, wenn lokale Konten verwendet werden, um sich anzumelden.

##### <a name="kerberos-service-ticket-operations"></a>Ticketvorgänge des Kerberos-Diensts
Diese Unterkategorie meldet Ereignisse, die von Kerberos-Ticket Anforderungs Prozessen auf dem Domänen Controller generiert werden, der für das Domänen Konto autorisierend ist.

##### <a name="kerberos-authentication-service"></a>Kerberos-Authentifizierungsdienst
Diese Unterkategorie meldet Ereignisse, die vom Kerberos-Authentifizierungsdienst generiert wurden. Diese Ereignisse treten auf dem Computer auf, der für die Anmeldeinformationen autoritativ ist.

##### <a name="other-account-logon-events"></a>Andere Kontoanmeldungsereignisse
Diese Unterkategorie gibt Aufschluss über die Ereignisse, die als Reaktion auf Anmelde Informationen auftreten, die für eine Benutzerkonto-Anmelde Anforderung gesendet werden und sich nicht auf die Überprüfung der Anmelde Informationen oder Kerberos-Tickets beziehen Diese Ereignisse treten auf dem Computer auf, der für die Anmeldeinformationen autoritativ ist. Bei Domänen Konten ist der Domänen Controller autorisierend, während für lokale Konten der lokale Computer autorisierend ist.

In Domänen Umgebungen werden die meisten Konto Anmelde Ereignisse im Sicherheitsprotokoll der Domänen Controller protokolliert, die für die Domänen Konten autorisierend sind. Diese Ereignisse können jedoch auf anderen Computern in der Organisation auftreten, wenn lokale Konten verwendet werden, um sich anzumelden. Beispiele sind etwa:

* Remotedesktopdienste Sitzungs disverbindungen
* Neue Remotedesktopdienste Sitzungen
* Sperren und Entsperren einer Arbeitsstation
* Aufrufen eines Bildschirmschoners
* Schließen eines Bildschirmschoners
* Erkennung eines Kerberos Replay-Angriffs, bei dem eine Kerberos-Anforderung mit identischen Informationen zweimal empfangen wird
* Gewähren des Zugriffs zu einem drahtlosen Netzwerk für ein Benutzer- oder Computerkonto
* Gewähren des Zugriffs zu einem kabelgebundenen 802.1x-Netzwerk für ein Benutzer- oder Computerkonto

#### <a name="account-management"></a>Kontoverwaltung

##### <a name="user-account-management"></a>Benutzerkontenverwaltung
Diese Unterkategorie meldet jedes Ereignis der Benutzerkonten Verwaltung, z. b. Wenn ein Benutzerkonto erstellt, geändert oder gelöscht wird. ein Benutzerkonto wurde umbenannt, deaktiviert oder aktiviert. oder es wird ein Kennwort festgelegt oder geändert. Wenn diese Überwachungs Richtlinien Einstellung aktiviert ist, können Administratoren Ereignisse nachverfolgen, um eine böswillige, versehentliche und autorisierte Erstellung von Benutzerkonten zu erkennen.

##### <a name="computer-account-management"></a>Computer Kontoverwaltung
Diese Unterkategorie meldet jedes Ereignis der Computer Kontoverwaltung, z. b. beim Erstellen, ändern, löschen, umbenennen, deaktivieren oder Aktivieren eines Computer Kontos.

##### <a name="security-group-management"></a>Verwaltung von Sicherheitsgruppen
Diese Unterkategorie meldet jedes Ereignis der Sicherheitsgruppen Verwaltung, z. b. Wenn eine Sicherheitsgruppe erstellt, geändert oder gelöscht wird oder wenn ein Mitglied einer Sicherheitsgruppe hinzugefügt bzw. aus dieser entfernt wird. Wenn diese Überwachungs Richtlinien Einstellung aktiviert ist, können Administratoren Ereignisse nachverfolgen, um eine böswillige, versehentliche und autorisierte Erstellung von Sicherheitsgruppen Konten zu erkennen.

##### <a name="distribution-group-management"></a>Verteiler Gruppenverwaltung
Diese Unterkategorie meldet jedes Ereignis der Verteiler Gruppenverwaltung, z. b. Wenn eine Verteiler Gruppe erstellt, geändert oder gelöscht wird oder wenn ein Mitglied einer Verteiler Gruppe hinzugefügt oder daraus entfernt wird. Wenn diese Überwachungs Richtlinien Einstellung aktiviert ist, können Administratoren Ereignisse nachverfolgen, um eine böswillige, versehentliche und autorisierte Erstellung von Gruppenkonten zu erkennen.

##### <a name="application-group-management"></a>Anwendungs Gruppenverwaltung
Diese Unterkategorie meldet jedes Ereignis der Anwendungs Gruppenverwaltung auf einem Computer, z. b. Wenn eine Anwendungs Gruppe erstellt, geändert oder gelöscht wird oder wenn ein Mitglied einer Anwendungs Gruppe hinzugefügt oder daraus entfernt wird. Wenn diese Überwachungs Richtlinien Einstellung aktiviert ist, können Administratoren Ereignisse nachverfolgen, um eine böswillige, versehentliche und autorisierte Erstellung von Anwendungs Gruppenkonten zu erkennen.

##### <a name="other-account-management-events"></a>Andere Konto Verwaltungs Ereignisse
Diese Unterkategorie meldet andere Konto Verwaltungs Ereignisse.

#### <a name="detailed-process-tracking"></a>Ausführliche Prozess Nachverfolgung

##### <a name="process-creation"></a>Prozesserstellung
Diese Unterkategorie meldet die Erstellung eines Prozesses und den Namen des Benutzers oder Programms, der ihn erstellt hat.

##### <a name="process-termination"></a>Prozess Beendigung
Diese Unterkategorie meldet, wenn ein Prozess beendet wird.

##### <a name="dpapi-activity"></a>DPAPI-Aktivität
In dieser Unterkategorie werden Aufrufe an die DPAPI (Data Protection Application Programming Interface) verschlüsselt oder entschlüsselt. DPAPI wird zum Schutz geheimer Informationen verwendet, wie z. b. gespeicherte Kenn Wörter und Schlüsselinformationen.

##### <a name="rpc-events"></a>RPC-Ereignisse
Diese Unterkategorie meldet Remote Prozedur Aufruf-Verbindungs Ereignisse (RPC).

#### <a name="directory-service-access"></a>Verzeichnisdienst Zugriff

##### <a name="directory-service-access"></a>Verzeichnisdienst Zugriff
Diese Unterkategorie meldet, wenn auf ein AD DS Objekt zugegriffen wird. Nur Objekte mit konfigurierten SACLs bewirken, dass Überwachungs Ereignisse generiert werden, und zwar nur, wenn auf Sie in einer Weise zugegriffen wird, die mit den SACL-Einträgen übereinstimmt. Diese Ereignisse ähneln den Verzeichnisdienst-Zugriffs Ereignissen in früheren Versionen von Windows Server. Diese Unterkategorie gilt nur für Domänen Controller.

##### <a name="directory-service-changes"></a>Verzeichnisdienst Änderungen
Diese Unterkategorie meldet Änderungen an Objekten in AD DS. Die gemeldeten Änderungs Typen sind Create-, Modify-, Move-und Wiederherstellen-Vorgänge, die für ein-Objekt ausgeführt werden. Die Verzeichnisdienst-Änderungs Überwachung gibt ggf. die alten und neuen Werte der geänderten Eigenschaften der Objekte an, die geändert wurden. Nur Objekte mit SACLs bewirken, dass Überwachungs Ereignisse generiert werden, und zwar nur, wenn auf Sie in einer Weise darauf zugegriffen wird, dass Sie mit ihren SACL-Einträgen übereinstimmt. Einige Objekte und Eigenschaften lösen aufgrund der Einstellungen der Objektklasse im Schema keine Überwachungsereignisse aus. Diese Unterkategorie gilt nur für Domänen Controller.

##### <a name="directory-service-replication"></a>Verzeichnisdienstreplikation
Diese Unterkategorie meldet, wenn die Replikation zwischen zwei Domänen Controllern beginnt und endet.

##### <a name="detailed-directory-service-replication"></a>Ausführliche Verzeichnisdienst Replikation
Diese Unterkategorie meldet ausführliche Informationen zu den Informationen, die zwischen Domänen Controllern repliziert werden. Diese Ereignisse können sehr hoch sein.

#### <a name="logonlogoff"></a>Anmeldung/Abmeldung

##### <a name="logon"></a>Anmelden
Diese Unterkategorie meldet, wenn ein Benutzer versucht, sich am System anzumelden. Diese Ereignisse erfolgen auf dem Computer, auf den zugegriffen wird. Bei interaktiven Anmeldungen tritt die Generierung dieser Ereignisse auf dem Computer auf, der bei angemeldet ist. Wenn für den Zugriff auf eine Freigabe eine Netzwerk Anmeldung erfolgt, werden diese Ereignisse auf dem Computer generiert, der die Ressource hostet, auf die zugegriffen wird. Wenn diese Einstellung auf **keine**Überwachung konfiguriert ist, ist es schwierig oder unmöglich, zu ermitteln, auf welchen Benutzer zugegriffen wurde oder ob er auf Organisations Computer zugegriffen hat.

##### <a name="network-policy-server"></a>Netzwerkrichtlinienserver
Diese Unterkategorie meldet Ereignisse, die von RADIUS-(IAS) und NAP-Benutzer Zugriffs Anforderungen (Network Access Protection) generiert wurden. Diese Anforderungen können **Grant**, **Deny**, **verwerfen**, **Quarantäne**, **Lock**und **Unlock**sein. Wenn Sie diese Einstellung überwachen, führt dies zu einer mittleren oder großen Anzahl von Datensätzen auf NPS-und IAS-Servern.

##### <a name="ipsec-main-mode"></a>IPSec-Hauptmodus
Diese Unterkategorie meldet die Ergebnisse des Internetschlüsselaustausch (IKE)-Protokolls und authentifiziertes Internetprotokoll (AuthIP) während der Hauptmodusverhandlung.

##### <a name="ipsec-extended-mode"></a>Erweiterter IPSec-Modus
Diese Unterkategorie meldet die Ergebnisse von AuthIP während der Aushandlungen im erweiterten Modus.

##### <a name="other-logonlogoff-events"></a>Andere Anmelde-/Abmelde Ereignisse
Diese Unterkategorie meldet andere Anmelde-und Abmelde bezogene Ereignisse, z. b. Remotedesktopdienste Sitzung die Verbindung trennt und die Verbindung wiederherstellt, mithilfe von runas Prozesse unter einem anderen Konto ausführen und eine Arbeitsstation sperren und entsperren.

##### <a name="logoff"></a>Abmelden (Logoff)
Diese Unterkategorie meldet, wenn sich ein Benutzer beim System anmeldet. Diese Ereignisse erfolgen auf dem Computer, auf den zugegriffen wird. Bei interaktiven Anmeldungen tritt die Generierung dieser Ereignisse auf dem Computer auf, der bei angemeldet ist. Wenn für den Zugriff auf eine Freigabe eine Netzwerk Anmeldung erfolgt, werden diese Ereignisse auf dem Computer generiert, der die Ressource hostet, auf die zugegriffen wird. Wenn diese Einstellung auf **keine**Überwachung konfiguriert ist, ist es schwierig oder unmöglich, zu ermitteln, auf welchen Benutzer zugegriffen wurde oder ob er auf Organisations Computer zugegriffen hat.

##### <a name="account-lockout"></a>Kontosperrung
In dieser Unterkategorie wird berichtet, wenn das Konto eines Benutzers aufgrund zu vieler fehlgeschlagener Anmeldeversuche gesperrt ist.

##### <a name="ipsec-quick-mode"></a>IPSec-Schnellmodus
Diese Unterkategorie meldet die Ergebnisse von IKE-Protokoll und AuthIP während der Schnellmodus-Verhandlung.

##### <a name="special-logon"></a>Besondere Anmeldung
Diese Unterkategorie meldet, wenn eine spezielle Anmeldung verwendet wird. Eine spezielle Anmeldung ist eine Anmeldung mit entsprechenden Administratorrechten und kann verwendet werden, um einen Prozess auf eine höhere Ebene zu erhöhen.

#### <a name="policy-change"></a>Richtlinienänderung

##### <a name="audit-policy-change"></a>Richtlinienänderungen überwachen
Diese Unterkategorie meldet Änderungen in der Überwachungsrichtlinie einschließlich SACL-Änderungen.

##### <a name="authentication-policy-change"></a>Änderung der Authentifizierungs Richtlinie
Diese Unterkategorie meldet Änderungen in der Authentifizierungs Richtlinie.

##### <a name="authorization-policy-change"></a>Autorisierungs Richtlinien Änderung
Diese Unterkategorie meldet Änderungen an der Autorisierungs Richtlinie einschließlich der Änderungen an Berechtigungen (DACL).

##### <a name="mpssvc-rule-level-policy-change"></a>Richtlinien Änderung auf mpssvc-Regel Ebene
Diese Unterkategorie meldet Änderungen in Richtlinien Regeln, die vom Microsoft Protection Service (MPSSVC.exe) verwendet werden. Dieser Dienst wird von der Windows-Firewall verwendet.

##### <a name="filtering-platform-policy-change"></a>Filtern von Platt Form Richtlinien Änderungen
Diese Unterkategorie meldet das Hinzufügen und Entfernen von Objekten aus WFP, einschließlich Start filtern. Diese Ereignisse können sehr hoch sein.

##### <a name="other-policy-change-events"></a>Andere Richtlinien Änderungs Ereignisse
In dieser Unterkategorie werden andere Arten von Sicherheitsrichtlinien Änderungen gemeldet, z. b. die Konfiguration der Trusted Platform Module (TPM) oder Kryptografieanbieter.

#### <a name="privilege-use"></a>Berechtigungen

##### <a name="sensitive-privilege-use"></a>Verwendung vertraulicher Berechtigungen
In dieser Unterkategorie wird berichtet, wenn ein Benutzerkonto oder ein Dienst vertrauliche Berechtigungen verwendet. Eine vertrauliche Berechtigung umfasst die folgenden Benutzerrechte: agieren als Teil des Betriebssystems, Sichern von Dateien und Verzeichnissen, Erstellen eines Tokenobjekts, Debuggen von Programmen, Aktivieren von Computer-und Benutzerkonten für die Delegierung, Generieren von Sicherheits Überwachungen, annehmen der Identität eines Clients nach der Authentifizierung, laden und Entladen von Gerätetreibern, Verwalten der Überwachung und des Sicherheitsprotokolls , Wiederherstellen von Dateien und Verzeichnissen und übernehmen des Besitzes von Dateien oder anderen Objekten. Durch das Überwachen dieser Unterkategorie wird eine große Anzahl von Ereignissen erzeugt.

##### <a name="nonsensitive-privilege-use"></a>Verwendung nicht sensibler Berechtigungen
Diese Unterkategorie meldet, wenn ein Benutzerkonto oder ein Dienst eine nicht vertrauliche Berechtigung verwendet. Eine nicht vertrauliche Berechtigung umfasst die folgenden Benutzerrechte: Access Credential Manager als vertrauenswürdiger Aufrufer, zugreifen auf diesen Computer über das Netzwerk, Hinzufügen von Arbeitsstationen zur Domäne, Anpassen von Speicher Kontingenten für einen Prozess, zulassen der lokalen Anmeldung, zulassen der Anmeldung über Remotedesktopdienste, umgehen der traversierungs Überprüfung, Ändern der Systemzeit, Erstellen einer Pagefile, Erstellen globaler Objekte , verweigern Sie den Zugriff auf diesen Computer über das Netzwerk, verweigern Sie die Anmeldung als Batch Auftrag, verweigern Sie die Anmeldung als Dienst, verweigern Sie die Protokollierung, verweigern Sie die Anmeldung über Remotedesktopdienste, erzwingen Sie das Herunterfahren von einem Remote System, ändern Sie die Zeit, und ändern Sie eine Objekt Bezeichnung. , Ausführen von volumewartungstasks, Profilerstellung für einen einzelnen Prozess, Profilsystem Leistung, Computer von Docking Station entfernen, das System Herunterfahren und Verzeichnisdienst Daten synchronisieren. Durch das Überwachen dieser Unterkategorie wird eine sehr hohe Anzahl von Ereignissen erzeugt.

##### <a name="other-privilege-use-events"></a>Andere Berechtigungs Verwendungs Ereignisse
Diese Sicherheitsrichtlinien Einstellung wird derzeit nicht verwendet.

#### <a name="object-access"></a>Objektzugriff

##### <a name="file-system"></a>Dateisystem
Diese Unterkategorie meldet, wenn auf Dateisystem Objekte zugegriffen wird. Nur Dateisystem Objekte mit SACLs bewirken, dass Überwachungs Ereignisse generiert werden, und zwar nur, wenn auf Sie in einer Weise auf Sie zugegriffen wird, die ihren SACL-Einträgen entspricht. Diese Richtlinien Einstellung bewirkt, dass keine Ereignisse überwacht werden. Es bestimmt, ob das Ereignis eines Benutzers überwacht werden soll, der auf ein Dateisystem Objekt zugreift, das über eine angegebene System Zugriffs Steuerungs Liste (SACL) verfügt, sodass die Überwachung wirksam wird.

Wenn die Einstellung Objektzugriff überwachen für **Erfolg**konfiguriert ist, wird jedes Mal, wenn ein Benutzer erfolgreich auf ein Objekt mit einer angegebenen SACL zugreift, ein Überwachungs Eintrag generiert. Wenn diese Richtlinien Einstellung auf **Fehler**festgelegt ist, wird jedes Mal ein Überwachungs Eintrag generiert, wenn ein Benutzer versucht, auf ein Objekt mit einer angegebenen SACL zuzugreifen.

##### <a name="registry"></a>Registrierung
Diese Unterkategorie meldet, wenn auf Registrierungs Objekte zugegriffen wird. Nur Registrierungs Objekte mit SACLs bewirken, dass Überwachungs Ereignisse generiert werden, und zwar nur, wenn auf Sie in einer Weise auf Sie zugegriffen wird, die ihren SACL-Einträgen entspricht. Diese Richtlinien Einstellung bewirkt, dass keine Ereignisse überwacht werden.

##### <a name="kernel-object"></a>Kernel Objekt
Diese Unterkategorie meldet, wenn auf Kernel Objekte wie Prozesse und Mutexen zugegriffen wird. Nur Kernel Objekte mit SACLs bewirken, dass Überwachungs Ereignisse generiert werden, und zwar nur dann, wenn auf Sie in einer Weise auf Sie zugegriffen wird, die ihren SACL-Einträgen entspricht. Normalerweise werden Kernel Objekten nur SACLs zugewiesen, wenn die Überwachungs Optionen auditbaseobjects oder auditbasedirectories aktiviert sind.

##### <a name="sam"></a>SAM
In dieser Unterkategorie wird berichtet, wenn auf die Datenbankobjekte der lokalen Sicherheits Konten Verwaltung (Sam) zugegriffen wird.

##### <a name="certification-services"></a>Zertifizierungsdienste
Diese Unterkategorie meldet, wenn Zertifizierungsdienst Vorgänge ausgeführt werden.

##### <a name="application-generated"></a>Anwendung generiert
Diese SubCategory meldet, wenn Anwendungen versuchen, Überwachungs Ereignisse mithilfe der Windows-Überwachungs Programmierschnittstellen (Application Programming Interfaces, APIs) zu generieren.

##### <a name="handle-manipulation"></a>Bearbeitung von Handles
Diese Unterkategorie meldet, wenn ein Handle für ein Objekt geöffnet oder geschlossen wird. Nur Objekte mit SACLs bewirken, dass diese Ereignisse generiert werden, und nur, wenn der versuchte handle-Vorgang mit den SACL-Einträgen übereinstimmt. Bearbeitungs Ereignisse für die Bearbeitung werden nur für Objekttypen generiert, bei denen die entsprechende Objekt Zugriffs-Unterkategorie aktiviert ist (z. b. Dateisystem oder Registrierung).

##### <a name="file-share"></a>Dateifreigabe
Diese Unterkategorie meldet, wenn auf eine Dateifreigabe zugegriffen wird. Diese Richtlinien Einstellung bewirkt, dass keine Ereignisse überwacht werden. Es bestimmt, ob das Ereignis eines Benutzers, der auf ein Dateifreigabe Objekt mit der angegebenen System Zugriffs Steuerungs Liste (SACL) zugreift, überwacht werden soll, sodass die Überwachung wirksam wird.

##### <a name="filtering-platform-packet-drop"></a>Filtern von Platt Form Paketen
Diese Unterkategorie meldet, wenn Pakete von der Windows-Filter Plattform (WFP) gelöscht werden. Diese Ereignisse können sehr hoch sein.

##### <a name="filtering-platform-connection"></a>Platt Form Verbindung wird gefiltert
Diese Unterkategorie meldet, wenn Verbindungen von WFP zugelassen oder blockiert werden. Diese Ereignisse können hoch sein.

##### <a name="other-object-access-events"></a>Andere Objekt Zugriffsereignisse
Diese Unterkategorie meldet andere Ereignisse im Zusammenhang mit dem Objektzugriff, wie z. b. Taskplaner Aufträge und COM+-Objekte.

#### <a name="system"></a>System

##### <a name="security-state-change"></a>Änderung des Sicherheitszustands
Diese Unterkategorie meldet Änderungen im Sicherheitszustand des Systems, z. b. wenn das Sicherheits Subsystem gestartet und beendet wird.

##### <a name="security-system-extension"></a>Sicherheits System Erweiterung
Diese Unterkategorie meldet das Laden von Erweiterungs Code, wie z. b. Authentifizierungs Pakete, durch das Sicherheits Subsystem.

##### <a name="system-integrity"></a>System Integrität
Diese Unterkategorie berichtet über Verstöße gegen die Integrität des Sicherheits Subsystems.

IPSec-Treiber

Diese Unterkategorie meldet die Aktivitäten des IPSec-Treibers (Internet Protocol Security, Internet Protokoll Sicherheit).

##### <a name="other-system-events"></a>Andere System Ereignisse
Diese Unterkategorie meldet andere Systemereignisse.

Weitere Informationen zu den Beschreibungen der Unterkategorien finden Sie im [Microsoft Security Compliance Manager-Tool](/previous-versions/tn-archive/cc677002(v=technet.10)).

Jede Organisation sollte die zuvor behandelten Kategorien und Unterkategorien überprüfen und diejenigen aktivieren, die für Ihre Umgebung am besten geeignet sind. Änderungen an der Überwachungsrichtlinie sollten vor der Bereitstellung in einer Produktionsumgebung immer getestet werden.

## <a name="configuring-windows-audit-policy"></a>Konfigurieren der Windows-Überwachungsrichtlinie

Die Windows-Überwachungsrichtlinie kann mithilfe von Gruppenrichtlinien, auditpol.exe, APIs oder Registrierungs Änderungen festgelegt werden. Die empfohlenen Methoden zum Konfigurieren der Überwachungsrichtlinie für die meisten Unternehmen sind Gruppenrichtlinie oder auditpol.exe. Zum Festlegen der Überwachungsrichtlinie eines Systems sind Konto Berechtigungen auf Administratorebene oder die entsprechenden Delegierten Berechtigungen erforderlich.

> [!NOTE]
> Die Berechtigung zum Verwalten von Überwachungs **-und Sicherheitsprotokollen** muss Sicherheits Prinzipale erteilt werden (Administratoren verfügen standardmäßig über diese Berechtigung), um die Änderung der Optionen für die Objekt Zugriffs Überwachung einzelner Ressourcen wie Dateien, Active Directory Objekten und Registrierungsschlüssel zuzulassen.

### <a name="setting-windows-audit-policy-by-using-group-policy"></a>Festlegen der Windows-Überwachungsrichtlinie mithilfe von Gruppenrichtlinie

Zum Festlegen der Überwachungsrichtlinie mithilfe von Gruppenrichtlinien konfigurieren Sie die entsprechenden Überwachungs Kategorien unter **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale** Richtlinien \ Überwachungsrichtlinie (ein Beispiel aus der Editor für lokale Gruppenrichtlinien (gpeer dit. msc) finden Sie im folgenden Screenshot). Jede Überwachungs Richtlinien Kategorie kann für **Erfolgs**-, **Fehler**-oder **Erfolgs** -und Fehlerereignisse aktiviert werden.

![Überwachen von AD](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_6.gif)

Erweiterte Überwachungs Richtlinien können mithilfe von Active Directory oder lokalen Gruppenrichtlinien festgelegt werden. Zum Festlegen der erweiterten Überwachungsrichtlinie konfigurieren Sie die entsprechenden Unterkategorien, die sich unter **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Erweiterte Überwachungsrichtlinie** befinden (im folgenden Screenshot finden Sie ein Beispiel aus der Editor für lokale Gruppenrichtlinien (gpeer dit. msc)). Jede Unterkategorie der Überwachungsrichtlinie kann für **Erfolgs**-, **Fehler**-oder **Erfolgs** -und **Fehler** Ereignisse aktiviert werden.

![Überwachen von AD](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_7.gif)

### <a name="setting-windows-audit-policy-using-auditpolexe"></a>Festlegen der Windows-Überwachungsrichtlinie mithilfe von Auditpol.exe

Auditpol.exe (für das Festlegen der Windows-Überwachungsrichtlinie) wurde in Windows Server 2008 und Windows Vista eingeführt. Anfänglich konnten nur auditpol.exe verwendet werden, um die erweiterte Überwachungsrichtlinie festzulegen, aber Gruppenrichtlinie kann in Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008, Windows 8 und Windows 7 verwendet werden.

Auditpol.exe ist ein Befehlszeilen-Hilfsprogramm. Die Syntax lautet wie folgt:

`auditpol /set /<Category|Subcategory>:<audit category> /<success|failure:> /<enable|disable>`

Beispiele für die Auditpol.exe Syntax:

`auditpol /set /subcategory:"user account management" /success:enable /failure:enable`

`auditpol /set /subcategory:"logon" /success:enable /failure:enable`

`auditpol /set /subcategory:"IPSEC Main Mode" /failure:enable`

> [!NOTE]
> Auditpol.exe legt die erweiterte Überwachungsrichtlinie lokal fest. Wenn die lokale Richtlinie mit Active Directory oder lokalen Gruppenrichtlinie in Konflikt steht, werden Gruppenrichtlinie Einstellungen in der Regel über auditpol.exe Einstellungen übernommen. Wenn mehrere Gruppen-oder lokale Richtlinien Konflikte bestehen, wird nur eine Richtlinie Vorrang (d. h. ersetzen). Überwachungs Richtlinien werden nicht zusammengeführt.

#### <a name="scripting-auditpol"></a>Skripterstellung für Auditpol

Microsoft stellt ein [Beispielskript](https://support.microsoft.com/kb/921469) für Administratoren bereit, die erweiterte Überwachungs Richtlinien mithilfe eines Skripts festlegen möchten, anstatt jeden auditpol.exe Befehl manuell einzugeben.

**Hinweis** Gruppenrichtlinie gibt nicht immer genau den Status aller aktivierten Überwachungs Richtlinien aus, wohingegen auditpol.exe. Weitere Informationen finden Sie [unter erhalten der effektiven Überwachungsrichtlinie in Windows 7 und Windows 2008 R2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731607(v=ws.10)) .

#### <a name="other-auditpol-commands"></a>Andere Auditpol-Befehle

Auditpol.exe können zum Speichern und Wiederherstellen einer lokalen Überwachungsrichtlinie sowie zum Anzeigen anderer Überwachungs bezogener Befehle verwendet werden. Hier sind die anderen **Auditpol** -Befehle aufgeführt.

`auditpol /clear`-Dient zum Löschen und Zurücksetzen von lokalen Überwachungs Richtlinien

`auditpol /backup /file:<filename>`-Wird verwendet, um eine aktuelle lokale Überwachungsrichtlinie in einer Binärdatei zu sichern.

`auditpol /restore /file:<filename>`-Wird verwendet, um eine zuvor gespeicherte Überwachungs Richtlinien Datei in eine lokale Überwachungsrichtlinie zu importieren.

`auditpol /<get/set> /option:<CrashOnAuditFail> /<enable/disable>`Wenn diese Überwachungs Richtlinien Einstellung aktiviert ist, bewirkt dies, dass das System sofort beendet wird (mit der Meldung "Pause: C0000244 {Audit failed}"), wenn eine Sicherheitsüberprüfung aus irgendeinem Grund nicht protokolliert werden kann. In der Regel kann ein Ereignis nicht protokolliert werden, wenn das Sicherheits Überwachungs Protokoll voll ist, und die für das Sicherheitsprotokoll angegebene Beibehaltungs Methode **nicht Ereignisse überschreiben** oder **Ereignisse nach Tagen überschreiben**. Sie wird in der Regel nur von Umgebungen aktiviert, die höhere Sicherheit bei der Protokollierung des Sicherheitsprotokolls erfordern. Wenn diese Option aktiviert ist, müssen Administratoren die Größe des Sicherheitsprotokolls genau beobachten und Protokolle nach Bedarf rotieren. Er kann auch mit Gruppenrichtlinie festgelegt werden, indem die Sicherheitsoption Überwachung **: Herunterfahren des Systems sofort geändert wird, wenn Sicherheits Überwachungen nicht protokolliert** werden können (Standardeinstellung = deaktiviert).

`auditpol /<get/set> /option:<AuditBaseObjects> /<enable/disable>`-Diese Überwachungs Richtlinien Einstellung bestimmt, ob der Zugriff auf globale Systemobjekte überprüft werden soll. Wenn diese Richtlinie aktiviert ist, bewirkt dies, dass Systemobjekte, z. b. Mutexes, Ereignisse, Semaphore und DOS-Geräte, mit einer Standard-System Zugriffs Steuerungs Liste (SACL) erstellt werden. Die meisten Administratoren sollten globale Systemobjekte so überwachen, dass Sie zu "unschädlich" werden, und Sie werden nur aktiviert, wenn böswillige Hacker vermutet werden. Nur benannte Objekte erhalten eine SACL. Wenn die Überwachungsrichtlinie für Überwachungs Objektzugriff (oder die Unterkategorie "Kernel Objektüberwachung") ebenfalls aktiviert ist, wird der Zugriff auf diese Systemobjekte überprüft. Wenn Sie diese Sicherheitseinstellung konfigurieren, werden die Änderungen erst wirksam, wenn Sie Windows neu starten. Diese Richtlinie kann auch mit Gruppenrichtlinie festgelegt werden, indem Sie die Sicherheitsoption Überwachen des Zugriffs globaler Systemobjekte (Standardeinstellung = deaktiviert) ändern.

`auditpol /<get/set> /option:<AuditBaseDirectories> /<enable/disable>`-Diese Überwachungs Richtlinien Einstellung gibt an, dass benannte Kernel Objekte (z. b. Mutexen und Semaphore) bei der Erstellung mit SACLs versehen werden sollen. Auditbasedirectories wirkt sich auf Containerobjekte aus, während auditbaseobjects sich auf Objekte auswirkt, die keine anderen Objekte enthalten können.

`auditpol /<get/set> /option:<FullPrivilegeAuditing> /<enable/disable>`-Diese Überwachungs Richtlinien Einstellung gibt an, ob der Client ein Ereignis generiert, wenn mindestens eine dieser Berechtigungen einem Benutzer Sicherheits Token zugewiesen ist: Zuordnungen von "zukenprivilege", "auditprivilege", "backupprivilege", "comatetokenprivilege", "Debug Privilege", "enabledelegationprivilege", "Identität", "loaddriverprivilege", "restoreprivilege", "securityprivilege", "systemumgebprivilege", "takebesitzshipprivilege" Wenn diese Option nicht aktiviert ist (Standardeinstellung = deaktiviert), werden die Berechtigungen backupprivilege und restoreprivilege nicht aufgezeichnet. Wenn Sie diese Option aktivieren, kann das Sicherheitsprotokoll während eines Sicherungs Vorgangs äußerst laut (manchmal Hunderte von Ereignissen pro Sekunde) werden. Diese Richtlinie kann auch mit Gruppenrichtlinie festgelegt werden, indem Sie die Sicherheitsoption Überwachung: überwachen **der Verwendung von Sicherungs-und Wiederherstellungs Berechtigungen**ändern.

> [!NOTE]
> Einige der hier bereitgestellten Informationen stammen aus dem Microsoft [Audit-Optionstyp](/openspecs/windows_protocols/ms-gpac/262a2bed-93d4-4c04-abec-cf06e9ec72fd) und dem Microsoft SCM-Tool.

## <a name="enforcing-traditional-auditing-or-advanced-auditing"></a>Erzwingen der herkömmlichen Überwachung oder der erweiterten Überwachung

In Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows 8, Windows 7 und Windows Vista können Administratoren auswählen, dass die neun herkömmlichen Kategorien aktiviert oder die Unterkategorien verwendet werden sollen. Es handelt sich um eine binäre Auswahl, die in jedem Windows-System getroffen werden muss. Entweder können die Hauptkategorien aktiviert werden, oder der subcategoriesit darf nicht gleichzeitig sein.

Um zu verhindern, dass die Legacy-Richtlinien der herkömmlichen Kategorie überschrieben werden, müssen Sie die Einstellung **Einstellungen der Unterkategorie erzwingen (Windows Vista oder höher) aktivieren, um die Einstellungen der Richtlinien Einstellung für die Überwachungs Richtlinien Kategorie außer Kraft zu setzen** . diese Einstellung befindet sich unter **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale**

Es wird empfohlen, die Unterkategorien anstelle der neun Hauptkategorien zu aktivieren und zu konfigurieren. Hierfür ist es erforderlich, dass eine Gruppenrichtlinie Einstellung aktiviert ist (damit Unterkategorien die Überwachungs Kategorien außer Kraft setzen), und die Unterkategorien, die Überwachungs Richtlinien unterstützen, konfiguriert werden.

Überwachungs Unterkategorien können mithilfe verschiedener Methoden konfiguriert werden, einschließlich Gruppenrichtlinie und des Befehlszeilen Programms auditpol.exe.

## <a name="next-steps"></a>Nächste Schritte

* [Überwachung und Konformität in Windows Server 2008](/previous-versions/technet-magazine/cc194392(v=msdn.10))

* [Verwenden von Gruppenrichtlinie zum Konfigurieren detaillierter Sicherheits Überwachungs Einstellungen für Windows Vista-basierte und Windows Server 2008-basierte Computer in einer Windows Server 2008-Domäne, in einer Windows Server 2003-Domäne oder in einer Windows 2000-Domäne](https://support.microsoft.com/kb/921469)

* [Schritt-für-Schritt-Anleitung für die erweiterte Sicherheits Überwachungsrichtlinie](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd408940(v=ws.10))
