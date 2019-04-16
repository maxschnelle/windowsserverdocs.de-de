---
ms.assetid: 0abe0976-4b49-45d6-a7b3-81d28bdb8210
title: "Überwachen der Richtlinie Empfehlungen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d03d38834f89f8cda80b7af147e2bd3e31f4f990
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="audit-policy-recommendations"></a>Überwachen der Richtlinie Empfehlungen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Abschnitt werden die Windows-Standard-überwachungsrichtlinieneinstellungen, geplante empfohlene Einstellungen für Sicherheitsüberwachungsrichtlinien und aggressiven Empfehlungen von Microsoft für Arbeitsstationen und Server-Produkte.  

Die SCM Sicherheitsbaseline-Empfehlungen, die hier gezeigte zusammen mit den Einstellungen, die empfehlen wir die Gefährdung erkannt werden, sollen nur ein Ausgangspunkt Basislinie Administratoren sein. Jede Organisation muss, eine eigene Entscheidungen in Bezug auf die Bedrohungen besteht darin, Toleranzen aufwiegen und Audit Policy Kategorien und Unterkategorien bieten sollten. Weitere Informationen zu den Sicherheitsrisiken finden Sie in der [Handbuch zu Bedrohungen und Gegenmaßnahmen](https://technet.microsoft.com/library/hh125921(v=ws.10).aspx). Administratoren, ohne ein durchdachtes Überwachungsrichtlinie werden empfohlen, die mit den Einstellungen sollten hier starten und dann zu ändern und zu testen, vor der Implementierung in ihre produktionsumgebung.  

Die Empfehlungen sind für Enterprise-Klasse Computer, bei denen Microsoft als Computer definiert, die durchschnittliche sicherheitsanforderungen und ein hohes Maß an den ordnungsgemäßen Betrieb erforderlich. Höhere Sicherheit, die Anforderungen aggressiver berücksichtigen sollten benötigen Entitäten Überwachungsrichtlinien.  

> [!NOTE]  
> Microsoft Windows standardmäßig und Sicherheitsbaseline-Empfehlungen stammen aus den [Microsoft Security Compliance Manager-Tool](https://technet.microsoft.com/library/cc677002.aspx).  

Die folgenden Einstellungen für Sicherheitsüberwachungsrichtlinien Baseline sind für normale Sicherheit Computer empfohlen, die nicht bekannt ist, dass aktive, erfolgreich angegriffen werden durch entschlossene oder Schadsoftware.  

## <a name="recommended-audit-policies-by-operating-system"></a>Empfohlene Überwachungsrichtlinien vom Betriebssystem  
Dieser Abschnitt enthält Tabellen, in denen die Überwachung Einstellung Empfehlungen aufgelistet, die für die folgenden Betriebssysteme gelten:  

-   Windows Server 2012  

-   Windows Server2012 R2  

-   Windows Server 2008  

-   Windows 8  

-   Windows 7  

Diese Tabellen enthalten die Windows-Standardeinstellung, die Sicherheitsbaseline-Empfehlungen und die stärkeren Empfehlungen für diese Betriebssysteme.  

**Audit Policy Tabellen Legende**  

|||  
|-|-|  
|**Notation**|**Empfehlung**|  
|JA|Aktivieren Sie im allgemeinen Szenarien|  
|Nein|Führen Sie **nicht** ermöglichen im allgemeinen Szenarien|  
|IF|Aktivieren Sie bei Bedarf für ein bestimmtes Szenario, oder wenn eine Rolle oder das Feature für die Überwachung gewünscht wird auf dem Computer installiert ist|  
|DC|Aktivieren Sie auf Domänencontrollern|  
|[Leere]|Keine Empfehlung|  

**Windows 8 und Windows 7 Audit Einstellungsempfehlungen**  

**Überwachungsrichtlinie**  

|Audit Policy Kategorie oder Unterkategorie|Windows-Standard<br /><br />Fehler bei der Erfolg|Geplante Empfehlung<br /><br />Fehler bei der Erfolg|Stärkere Empfehlung<br /><br />Fehler bei der Erfolg|  
|----------------------------------------|------------------------------------------|--------------------------------------------------|--------------------------------------------------|  
|**Anmeldung**||||  
|Anmeldeinformationen überwachen|Nein, nein|Nein Ja|Ja, ja|  
|Kerberos-Authentifizierungsdienst überwachen|||Ja, ja|  
|Ticketvorgänge des Kerberos-Diensts überwachen|||Ja, ja|  
|Andere Kontoanmeldungsereignisse überwachen|||Ja, ja|  
|**Kontoverwaltung**||||  
|Anwendungsgruppenverwaltung||||  
|Computerkontoverwaltung||Nein Ja|Ja, ja|  
|Verteilergruppenverwaltung||||  
|Andere Kontoverwaltungsereignisse überwachen||Nein Ja|Ja, ja|  
|Sicherheitsgruppenverwaltung||Nein Ja|Ja, ja|  
|Benutzerkontenverwaltung|Nein Ja|Nein Ja|Ja, ja|  
|**Detaillierte Überwachung**||||  
|DPAPI-Aktivität überwachen|||Ja, ja|  
|Prozesserstellung überwachen||Nein Ja|Ja, ja|  
|Prozessbeendung überwachen||||  
|RPC-Ereignisse überwachen||||  
|**DS-Zugriff**||||  
|Detaillierte Verzeichnisdienstreplikation überwachen||||  
|Überwachen des Zugriffs auf Verzeichnisdienste||||  
|Verzeichnisdienständerungen||||  
|Verzeichnisdienstreplikation überwachen||||  
|**An- und Abmelden**||||  
|Kontosperrung überwachen|Nein Ja||Nein Ja|  
|Benutzer-/Geräteansprüche überwachen||||  
|IPsec-Erweiterungsmodus überwachen||||  
|IPsec-Hauptmodus überwachen|||IF IF|  
|IPsec-Schnellmodus überwachen||||  
|Abmelden überwachen|Nein Ja|Nein Ja|Nein Ja|  
|Überwachung der Anmeldung|Nein Ja|Nein Ja|Ja, ja|  
|Netzwerkrichtlinienserver überwachen|Ja, ja|||  
|Andere Anmelde-/Abmeldeereignisse überwachen||||  
|Spezielle Anmeldung überwachen|Nein Ja|Nein Ja|Ja, ja|  
|**Den Zugriff auf Objekte**||||  
|Überwachen Sie Anwendung generiert||||  
|Zertifizierungsdienste überwachen||||  
|Detaillierte Dateifreigabe überwachen||||  
|Dateifreigabe überwachen||||  
|Dateisystem überwachen||||  
|Filterplattformverbindung überwachen||||  
|Filterplattform: Verworfene überwachen||||  
|Handleänderung überwachen||||  
|Kernelobjekt überwachen||||  
|Andere Objektzugriffsereignisse überwachen||||  
|Registrierung überwachen||||  
|Wechselmedien überwachen||||  
|SAM überwachen||||  
|Staging zentraler Zugriffsrichtlinien überwachen||||  
|**Richtlinienänderung**||||  
|Überwachungsrichtlinienänderung überwachen|Nein Ja|Ja, ja|Ja, ja|  
|Authentifizierungsrichtlinienänderung|Nein Ja|Nein Ja|Ja, ja|  
|Autorisierungsrichtlinienänderung überwachen||||  
|Filterplattform-Richtlinienänderung überwachen||||  
|Regelebene MPSSVC-Richtlinienänderung überwachen|||Ja  |  
|Andere Richtlinienänderungsereignisse überwachen||||  
|**Verwendung von rechten**||||  
|Nicht sensible Verwendung von rechten überwachen||||  
|Andere Rechteverwendungsereignisse überwachen||||  
|Sensible Verwendung von rechten überwachen||||  
|**System**||||  
|IPsec-Treiber überwachen||Ja, ja|Ja, ja|  
|Andere Systemereignisse überwachen|Ja, ja|||  
|Sicherheitsstatusänderung|Nein Ja|Ja, ja|Ja, ja|  
|Sicherheitssystemerweiterung||Ja, ja|Ja, ja|  
|Systemintegrität überwachen|Ja, ja|Ja, ja|Ja, ja|  
|**Globaler Objektzugriff überwachen**||||  
|IPsec-Treiber überwachen||||  
|Andere Systemereignisse überwachen||||  
|Sicherheitsstatusänderung||||  
|Sicherheitssystemerweiterung||||  
|Systemintegrität überwachen||||  

**WindowsServer 2012, Windows Server 2008 R2 und Windows Server 2008 Audit Einstellungsempfehlungen**  

|Audit Policy Kategorie oder Unterkategorie|Windows-Standard<br /><br />Fehler bei der Erfolg|Geplante Empfehlung<br /><br />Fehler bei der Erfolg|Stärkere Empfehlung<br /><br />Fehler bei der Erfolg|  
|----------------------------------------|------------------------------------------|--------------------------------------------------|--------------------------------------------------|  
|**Anmeldung**||||  
|Anmeldeinformationen überwachen|Nein, nein|Ja, ja|Ja, ja|  
|Kerberos-Authentifizierungsdienst überwachen|||Ja, ja|  
|Ticketvorgänge des Kerberos-Diensts überwachen|||Ja, ja|  
|Andere Kontoanmeldungsereignisse überwachen|||Ja, ja|  
|**Kontoverwaltung**||||  
|Anwendungsgruppenverwaltung||||  
|Computerkontoverwaltung||Ja, DC|Ja, ja|  
|Verteilergruppenverwaltung||||  
|Andere Kontoverwaltungsereignisse überwachen||Ja, ja|Ja, ja|  
|Sicherheitsgruppenverwaltung||Ja, ja|Ja, ja|  
|Benutzerkontenverwaltung|Nein Ja|Ja, ja|Ja, ja|  
|**Detaillierte Überwachung**||||  
|DPAPI-Aktivität überwachen|||Ja, ja|  
|Prozesserstellung überwachen||Nein Ja|Ja, ja|  
|Prozessbeendung überwachen||||  
|RPC-Ereignisse überwachen||||  
|**DS-Zugriff**||||  
|Detaillierte Verzeichnisdienstreplikation überwachen||||  
|Überwachen des Zugriffs auf Verzeichnisdienste||DC-DC|DC-DC|  
|Verzeichnisdienständerungen||DC-DC|DC-DC|  
|Verzeichnisdienstreplikation überwachen||||  
|**An- und Abmelden**||||  
|Kontosperrung überwachen|Nein Ja||Nein Ja|  
|Benutzer-/Geräteansprüche überwachen||||  
|IPsec-Erweiterungsmodus überwachen||||  
|IPsec-Hauptmodus überwachen|||IF IF|  
|IPsec-Schnellmodus überwachen||||  
|Abmelden überwachen|Nein Ja|Nein Ja|Nein Ja|  
|Überwachung der Anmeldung|Nein Ja|Ja, ja|Ja, ja|  
|Netzwerkrichtlinienserver überwachen|Ja, ja|||  
|Andere Anmelde-/Abmeldeereignisse überwachen|||Ja, ja|  
|Spezielle Anmeldung überwachen|Nein Ja|Nein Ja|Ja, ja|  
|**Den Zugriff auf Objekte**||||  
|Überwachen Sie Anwendung generiert||||  
|Zertifizierungsdienste überwachen||||  
|Detaillierte Dateifreigabe überwachen||||  
|Dateifreigabe überwachen||||  
|Dateisystem überwachen||||  
|Filterplattformverbindung überwachen||||  
|Filterplattform: Verworfene überwachen||||  
|Handleänderung überwachen||||  
|Kernelobjekt überwachen||||  
|Andere Objektzugriffsereignisse überwachen||||  
|Registrierung überwachen||||  
|Wechselmedien überwachen||||  
|SAM überwachen||||  
|Staging zentraler Zugriffsrichtlinien überwachen||||  
|**Richtlinienänderung**||||  
|Überwachungsrichtlinienänderung überwachen|Nein Ja|Ja, ja|Ja, ja|  
|Authentifizierungsrichtlinienänderung|Nein Ja|Nein Ja|Ja, ja|  
|Autorisierungsrichtlinienänderung überwachen||||  
|Filterplattform-Richtlinienänderung überwachen||||  
|Regelebene MPSSVC-Richtlinienänderung überwachen|||Ja  |  
|Andere Richtlinienänderungsereignisse überwachen||||  
|**Verwendung von rechten**||||  
|Nicht sensible Verwendung von rechten überwachen||||  
|Andere Rechteverwendungsereignisse überwachen||||  
|Sensible Verwendung von rechten überwachen||||  
|**System**||||  
|IPsec-Treiber überwachen||Ja, ja|Ja, ja|  
|Andere Systemereignisse überwachen|Ja, ja|||  
|Sicherheitsstatusänderung|Nein Ja|Ja, ja|Ja, ja|  
|Sicherheitssystemerweiterung||Ja, ja|Ja, ja|  
|Systemintegrität überwachen|Ja, ja|Ja, ja|Ja, ja|  
|**Globaler Objektzugriff überwachen**||||  
|IPsec-Treiber überwachen||||  
|Andere Systemereignisse überwachen||||  
|Sicherheitsstatusänderung||||  
|Sicherheitssystemerweiterung||||  
|Systemintegrität überwachen||||  

## <a name="set-audit-policy-on-workstations-and-servers"></a>Festlegen der Überwachungsrichtlinie auf Arbeitsstationen und Servern  
Alle Ereignisprotokoll-Pläne sollten Arbeitsstationen und Servern überwachen. Ein häufiger Fehler besteht nur Server oder Domänencontroller überwacht. Da böswilliger hacking häufig anfänglich auf Arbeitsstationen auftritt, ist die beste und früheste Informationsquelle keine Überwachung Arbeitsstationen ignoriert werden.  

Administratoren sollten sorgfältig überprüfen und Testen alle Überwachungsrichtlinie vor der Implementierung in ihre produktionsumgebung.  

## <a name="events-to-monitor"></a>Zu überwachende Ereignisse  
Eine perfekte Ereignis-ID eine Warnung generiert, sollte die folgenden Attribute enthalten:  

-   Hohe Wahrscheinlichkeit, dass dieses Vorkommen gibt an, nicht autorisierte Aktivitäten  

-   Eine geringe Anzahl falsch positive Ergebnisse  

-   Auftreten sollte in einer forensischen führen.  

Zwei Arten von Ereignissen sollten überwacht und eine Warnung erhalten:  

1.  Diese Ereignisse, in denen auch ein einmaliges auftreten auf nicht autorisierte Aktivitäten hinweist  

2.  Eine Ansammlung von Ereignissen, die eine erwartete und akzeptierte baseline  

Ein Beispiel für das erste Ereignis ist:  

Wenn Domänen-Admins (DAs) am Anmelden bei Computern, die keine Domänencontroller sind verboten sind, wird ein einzelnes Vorkommen des Mitglied DA Anmelden an einer Endbenutzerarbeitsstation sollte eine Warnung generiert und untersucht werden. Dieser Warnungstyp ist einfach zu generieren, indem Sie das spezielle Anmeldung überwachen Ereignis 4964 (Sondergruppen wurden einer neuen Anmeldung zugewiesen). Weitere Beispiele für einzelne Instanz Warnungen:  

-   Wenn Server A zu Server B, Warnung, wenn sie Verbindung zueinander eine nie herstellen soll.  

-   Warnung ausgegeben Sie, wenn eine normale Endbenutzerkonto unerwartet eine sensible Sicherheitsgruppe hinzugefügt wird.  

-   Bei einem Mitarbeiter im Werk Standort A nie bei Nacht, Warnung beim Anmelden eines Benutzers um Mitternacht.  

-   Warnung ausgegeben Sie, wenn eine nicht autorisierte Service auf einem Domänencontroller installiert ist.  

-   Untersuchen Sie, ob eine normale Endbenutzer direkt melden Sie sich bei einem SQL Server versucht, für die sie keine eindeutigen Grund dafür haben.  

-   Wenn Ihnen keine Mitglieder der Gruppe DA und ein Benutzer sich selbst es hinzufügt, versuchen Sie es sofort.  

Ein Beispiel für das zweite Ereignis ist:  

Eine abweichende Anzahl der fehlgeschlagenen Anmeldeversuche hinweisen erraten des Kennworts. Für ein Unternehmen eine Warnung für eine ungewöhnlich hohe Anzahl der fehlgeschlagenen Anmeldeversuche bereitstellen müssen sie zuerst die normale Ebenen der fehlgeschlagenen Anmeldeversuche innerhalb ihrer Umgebung vor einem schädlichen Sicherheitsereignis verstehen.  

Eine umfassende Liste der Ereignisse, die Sie beim Überwachen auf Anzeichen für sicherheitsgefährdungen enthalten soll, finden Sie unter [Anhang L: zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md).  

## <a name="active-directory-objects-and-attributes-to-monitor"></a>Active Directory-Objekte und Attribute überwachen  
Im folgenden sind die Konten, Gruppen und Attribute, die Sie überwachen müssen, damit Sie erkennen, versucht, die Active Directory Domain Services-Installation beeinträchtigen können.  

-   Systeme, deaktivieren oder Entfernen von Antiviren- und Antischadsoftware (automatisch Neustart Schutz, wenn sie manuell deaktiviert ist)  

-   Administratorkonten für nicht autorisierte Änderungen  

-   Aktivitäten, die mithilfe von privilegierten Konten (automatisch entfernen Konto verdächtige Aktivitäten abgeschlossen sind, oder vorgesehene Zeit abgelaufen) ausgeführt werden  

-   Privilegierten und VIP-Konten in AD DS. Überwachen Sie Änderungen, insbesondere Änderungen von Attributen auf der Registerkarte "Konto" (z. B. Cn, Name, sAMAccountName, UserPrincipalName oder UserAccountControl). Zusätzlich zur Überwachung beschränken die Konten, den Konten an, als klein eine Reihe von Administratoren wie möglich geändert werden kann.  

Finden Sie unter [Anhang L: zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md) für eine Liste der empfohlenen Ereignisse überwachen, deren Bedeutung Bewertungen und eine Zusammenfassung der Meldungen Ereignis.  

-   Gruppe von Servern durch die Klassifizierung von Arbeitslasten, wodurch Sie schnell auf die Server identifizieren, die die am ehesten überwachten und die meisten repräsentative Motoröltemperatur konfiguriert werden soll  

-   Ändert die Eigenschaften und die Mitgliedschaft in der folgenden AD DS-Gruppen: Organisations-Admins (EA) "," Domänen-Admins (DA) "," Administratoren (BA) "und" Schema-Admins (SA)  

-   Zum Aktivieren von Konten deaktiviert privilegierte Konten (z. B. integrierter Administratorkonten in Active Directory und auf Member Systemen)  

-   Konten, alle Schreibvorgänge an das Konto anzumelden  

-   Integrierte Sicherheitskonfigurations-Assistenten so konfigurieren Sie den Dienst, Registrierung, überwachen und Firewall-Einstellungen für den Server-Angriffsfläche zu verringern. Verwenden Sie diesen Assistenten, wenn Sie als Teil der Strategie für die administrative Host sprungbrettservern implementieren.  

## <a name="additional-information-for-monitoring-active-directory-domain-services"></a>Weitere Informationen zur Überwachung von Active Directory-Domänendienste  
Überprüfen Sie die folgenden Links, um weitere Informationen zur Überwachung von AD DS:  
  
-   [Globale Objektzugriffsüberwachung ist Magie](http://blogs.technet.com/b/askds/archive/2011/03/10/global-object-access-auditing-is-magic.aspx) -enthält Informationen zum Konfigurieren und Verwenden von erweiterten Sicherheitsüberwachungsrichtlinien-Konfiguration, die Windows 7 und Windows Server 2008 R2 hinzugefügt wurde.  

-   [Einführung in die Überwachung von Änderungen in Windows 2008](http://blogs.technet.com/b/askds/archive/2007/10/19/introducing-auditing-changes-in-windows-2008.aspx) -Überwachung Änderungen im Windows 2008 eingeführt.  

-   [Eine tolle Tricks in Vista und 2008-Überwachung](http://blogs.technet.com/b/askds/archive/2007/11/16/cool-auditing-tricks-in-vista-and-2008.aspx) -erläutert interessanten neuen Features der Überwachung in Windows Vista und Windows Server 2008, die für die Behandlung von Problemen oder sehen, was passiert in Ihrer Umgebung verwendet werden können.  

-   [Zentrale Anlaufstelle für die Überwachung in Windows Server 2008 und Windows Vista](http://blogs.technet.com/b/askds/archive/2008/03/27/one-stop-shop-for-auditing-in-windows-server-2008-and-windows-vista.aspx) -enthält eine Zusammenstellung der Überwachung von Funktionen und Informationen, die in Windows Server 2008 und Windows Vista enthalten sind.  

-   [Leitfaden für AD DS-Überwachung](https://technet.microsoft.com/library/a9c25483-89e2-4202-881c-ea8e02b4b2a5.aspx) -beschreibt die neuen Active Directory-Domänendienste (AD DS) Überwachungsfeatures in Windows Server 2008. Darüber hinaus wie folgt vor, um dieses neue Feature zu implementieren.  

## <a name="general-list-of-security-event-id-recommendation-criticalities"></a>Allgemeine Übersicht über Sicherheit Ereignis-ID Empfehlung Criticalities  
Alle Empfehlungen von Ereignis-ID werden nach einem Bedeutung Bewertung wie folgt ergänzt:  

**Hoch:** Ereignis-IDs mit einer Bewertung mit hoher Wichtigkeit sollten immer und sofort benachrichtigt und untersucht.  

**Mittel:** Ereignis-ID mit einer Bewertung mittlere Gefährlichkeit konnte auf böswillige Aktivitäten hinweisen, aber es muss zusammen mit einigen anderen abnormalen Systemverhalten (z. B. eine ungewöhnliche Anzahl in einen bestimmten Zeitraum, unerwartete Vorkommen oder Vorkommen auf einem Computer, die normalerweise nicht erwartet, protokolliert das Ereignis auftritt). Ein Mittel Gefährlichkeit Ereignis kann auch r als Metrik gesammelt und im Laufe der Zeit Vergleich.  

**Low:** und Ereignis-ID mit einer niedrigen Gefährlichkeit Ereignisse nicht einiges Aufmerksamkeit oder dazu führen, dass Warnungen, es sei denn, Mittel oder hoch Gefährlichkeit Ereignisse korreliert.  

Diese Empfehlungen dienen zum Bereitstellen einer Basislinie für den Administrator. Alle Empfehlungen sollte sorgfältig vor der Implementierung in einer produktionsumgebung überprüft werden.  

Finden Sie unter [Anhang L: zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md) eine Liste der empfohlenen Ereignisse überwachen, deren Bedeutung Bewertungen und eine Zusammenfassung der Meldungen Ereignis.  
