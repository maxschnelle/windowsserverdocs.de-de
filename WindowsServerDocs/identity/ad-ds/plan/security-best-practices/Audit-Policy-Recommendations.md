---
ms.assetid: 0abe0976-4b49-45d6-a7b3-81d28bdb8210
title: Audit Policy Recommendations
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5a5af1691cdfec41cc4f821943b9b849c8822057
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953952"
---
# <a name="audit-policy-recommendations"></a>Audit Policy Recommendations

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10, Windows 8.1, Windows 7

In diesem Abschnitt werden die Standardeinstellungen für die Überwachungsrichtlinie von Windows, die grundlegenden empfohlenen Überwachungs Richtlinien Einstellungen und die aggressiveren Empfehlungen von Microsoft für Arbeitsstationen und Server Produkte behandelt.  

Die hier gezeigten SCM-baselineempfehlungen, zusammen mit den Einstellungen, die wir empfehlen, um eine Gefährdung zu erkennen, dienen nur als Ausgangsbasis Leit Faden für Administratoren. Jede Organisation muss ihre eigenen Entscheidungen hinsichtlich der erkannten Bedrohungen, ihrer akzeptablen Risiko Toleranzen und der zu aktivierenden Überwachungs Richtlinien Kategorien oder Unterkategorien treffen. Weitere Informationen zu Bedrohungen finden Sie im Handbuch zu [Bedrohungen und Gegenmaßnahmen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh125921(v=ws.10)). Administratoren ohne durchdachte Überwachungsrichtlinie werden empfohlen, mit den hier empfohlenen Einstellungen zu beginnen und dann vor der Implementierung von in Ihrer Produktionsumgebung zu ändern und zu testen.  

Die Empfehlungen gelten für Computer auf Unternehmens Niveau, die von Microsoft als Computer definiert werden, die überdurchschnittliche Sicherheitsanforderungen verfügen und ein hohes Maß an Betriebs Funktionalität benötigen. Entitäten, die höhere Sicherheitsanforderungen benötigen, sollten aggressivere Überwachungs Richtlinien in Erwägung zieht.  

> [!NOTE]  
> Microsoft Windows-Standardwerte und-baselineempfehlungen wurden vom [Microsoft Security Compliance Manager-Tool](/previous-versions/tn-archive/cc677002(v=technet.10))übernommen.  

Die folgenden grundlegenden Überwachungs Richtlinien Einstellungen werden für normale Sicherheits Computer empfohlen, die nicht bekanntermaßen aktiv und erfolgreich von ermittelten Angreifern oder Schadsoftware betroffen sind.  

## <a name="recommended-audit-policies-by-operating-system"></a>Empfohlene Überwachungs Richtlinien nach Betriebs System  
Dieser Abschnitt enthält Tabellen, in denen die Empfehlungen für die Überwachungs Einstellungen aufgeführt sind, die für die folgenden Betriebssysteme gelten:  

-   Windows Server 2016 

-   Windows Server 2012  

-   Windows Server 2012 R2  

-   WindowsServer 2008  

-   Windows 10

-   Windows 8.1  

-   Windows 7  

Diese Tabellen enthalten die Windows-Standardeinstellung, die grundlegenden Empfehlungen und die stärkeren Empfehlungen für diese Betriebssysteme.  

**Legende für Überwachungs Richtlinien Tabellen**  

|||  
|-|-|  
|**Notation**|**Empfehlung**|  
|YES|In allgemeinen Szenarien aktivieren|  
|Nein|**Nicht** in allgemeinen Szenarien aktivieren|  
|IF|Aktivieren Sie bei Bedarf für ein bestimmtes Szenario oder, wenn eine Rolle oder ein Feature, für das die Überwachung gewünscht ist, auf dem Computer installiert ist.|  
|SL|Aktivieren auf Domänen Controllern|  
|Blitz|Keine Empfehlung|  

**Empfehlungen zu Überwachungs Einstellungen für Windows 10, Windows 8 und Windows 7**  

**Überwachungsrichtlinie**  

|Kategorie oder Unterkategorie der Überwachungsrichtlinie|Windows-Standard<p>Erfolgs Fehler|Grundlegende Empfehlung<p>Erfolgs Fehler|Stärkere Empfehlung<p>Erfolgs Fehler|  
|----------------------------------------|------------------------------------------|--------------------------------------------------|--------------------------------------------------|  
|**Kontoanmeldung**||||  
|Überprüfen der Anmeldeinformationen überwachen|Nein, nein|Ja Nein|Ja, ja|  
|Kerberos-Authentifizierungsdienst überwachen|||Ja, ja|  
|Ticketvorgänge des Kerberos-Diensts überwachen|||Ja, ja|  
|Andere Kontoanmeldungsereignisse überwachen|||Ja, ja|  
|**Kontoverwaltung**||||  
|Anwendungsgruppenverwaltung überwachen||||  
|Computerkontoverwaltung überwachen||Ja Nein|Ja, ja|  
|Verteilergruppenverwaltung überwachen||||  
|Andere Kontoverwaltungsereignisse überwachen||Ja Nein|Ja, ja|  
|Sicherheitsgruppenverwaltung überwachen||Ja Nein|Ja, ja|  
|Benutzerkontenverwaltung überwachen|Ja Nein|Ja Nein|Ja, ja|  
|**Detaillierte Überwachung**||||  
|DPAPI-Aktivität überwachen|||Ja, ja|  
|Prozesserstellung überwachen||Ja Nein|Ja, ja|  
|Prozessbeendung überwachen||||  
|RPC-Ereignisse überwachen||||  
|**DS-Zugriff**||||  
|Detaillierte Verzeichnisdienstreplikation überwachen||||  
|Verzeichnisdienstzugriff überwachen||||  
|Verzeichnisdienständerungen überwachen||||  
|Verzeichnisdienstreplikation überwachen||||  
|**Anmelden und Abmelden**||||  
|Kontosperrung überwachen|Ja Nein||Ja Nein|  
|Benutzer-/Geräteansprüche überwachen||||  
|IPsec-Erweiterungsmodus überwachen||||  
|IPsec-Hauptmodus überwachen|||Wenn, wenn|  
|IPsec-Schnellmodus überwachen||||  
|Abmelden überwachen|Ja Nein|Ja Nein|Ja Nein|  
|Anmeldung <sup>1</sup> überwachen|Ja, ja|Ja, ja|Ja, ja|  
|Netzwerkrichtlinienserver überwachen|Ja, ja|||  
|Andere Anmelde-/Abmeldeereignisse überwachen||||  
|Spezielle Anmeldung überwachen|Ja Nein|Ja Nein|Ja, ja|  
|**Objektzugriff**||||  
|Anwendung generiert überwachen||||  
|Zertifizierungsdienste überwachen||||  
|Detaillierte Dateifreigabe überwachen||||  
|Dateifreigabe überwachen||||  
|Dateisystem überwachen||||  
|Filterplattformverbindung überwachen||||  
|Filterplattform: Verworfene Pakete überwachen||||  
|Handleänderung überwachen||||  
|Kernelobjekt überwachen||||  
|Andere Objektzugriffsereignisse überwachen||||  
|Registrierung überwachen||||  
|Wechselmedien überwachen||||  
|SAM überwachen||||  
|Staging zentraler Zugriffsrichtlinien überwachen||||  
|**Richtlinienänderung**||||  
|Überwachungsrichtlinienänderung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|Authentifizierungsrichtlinienänderung überwachen|Ja Nein|Ja Nein|Ja, ja|  
|Autorisierungsrichtlinienänderung überwachen||||  
|Filterplattform-Richtlinienänderung überwachen||||  
|MPSSVC-Richtlinienänderung auf Regelebene überwachen|||Ja  |  
|Andere Richtlinienänderungsereignisse überwachen||||  
|**Berechtigungen**||||  
|Nicht sensible Verwendung von Rechten überwachen||||  
|Andere Rechteverwendungsereignisse überwachen||||  
|Sensible Verwendung von Rechten überwachen||||  
|**System**||||  
|IPsec-Treiber überwachen||Ja, ja|Ja, ja|  
|Andere Systemereignisse überwachen|Ja, ja|||  
|Sicherheitsstatusänderung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|Sicherheitssystemerweiterung überwachen||Ja, ja|Ja, ja|  
|Systemintegrität überwachen|Ja, ja|Ja, ja|Ja, ja|  
|**Globale Objektzugriffsüberwachung**||||  
|IPsec-Treiber überwachen||||  
|Andere Systemereignisse überwachen||||  
|Sicherheitsstatusänderung überwachen||||  
|Sicherheitssystemerweiterung überwachen||||  
|Systemintegrität überwachen||||  

<sup>1</sup> ab Windows 10, Version 1809, ist Audit Logon standardmäßig sowohl für Erfolg als auch für Fehler aktiviert. In früheren Versionen von Windows ist nur Erfolg standardmäßig aktiviert.

**Empfehlungen zu Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 Überwachungs Einstellungen**  

|Kategorie oder Unterkategorie der Überwachungsrichtlinie|Windows-Standard<p>Erfolgs Fehler|Grundlegende Empfehlung<p>Erfolgs Fehler|Stärkere Empfehlung<p>Erfolgs Fehler|  
|----------------------------------------|------------------------------------------|--------------------------------------------------|--------------------------------------------------|  
|**Kontoanmeldung**||||  
|Überprüfen der Anmeldeinformationen überwachen|Nein, nein|Ja, ja|Ja, ja|  
|Kerberos-Authentifizierungsdienst überwachen|||Ja, ja|  
|Ticketvorgänge des Kerberos-Diensts überwachen|||Ja, ja|  
|Andere Kontoanmeldungsereignisse überwachen|||Ja, ja|  
|**Kontoverwaltung**||||  
|Anwendungsgruppenverwaltung überwachen||||  
|Computerkontoverwaltung überwachen||Ja, DC|Ja, ja|  
|Verteilergruppenverwaltung überwachen||||  
|Andere Kontoverwaltungsereignisse überwachen||Ja, ja|Ja, ja|  
|Sicherheitsgruppenverwaltung überwachen||Ja, ja|Ja, ja|  
|Benutzerkontenverwaltung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|**Detaillierte Überwachung**||||  
|DPAPI-Aktivität überwachen|||Ja, ja|  
|Prozesserstellung überwachen||Ja Nein|Ja, ja|  
|Prozessbeendung überwachen||||  
|RPC-Ereignisse überwachen||||  
|**DS-Zugriff**||||  
|Detaillierte Verzeichnisdienstreplikation überwachen||||  
|Verzeichnisdienstzugriff überwachen||DC-DC|DC-DC|  
|Verzeichnisdienständerungen überwachen||DC-DC|DC-DC|  
|Verzeichnisdienstreplikation überwachen||||  
|**Anmelden und Abmelden**||||  
|Kontosperrung überwachen|Ja Nein||Ja Nein|  
|Benutzer-/Geräteansprüche überwachen||||  
|IPsec-Erweiterungsmodus überwachen||||  
|IPsec-Hauptmodus überwachen|||Wenn, wenn|  
|IPsec-Schnellmodus überwachen||||  
|Abmelden überwachen|Ja Nein|Ja Nein|Ja Nein|  
|Anmelden überwachen|Ja, ja|Ja, ja|Ja, ja|  
|Netzwerkrichtlinienserver überwachen|Ja, ja|||  
|Andere Anmelde-/Abmeldeereignisse überwachen|||Ja, ja|  
|Spezielle Anmeldung überwachen|Ja Nein|Ja Nein|Ja, ja|  
|**Objektzugriff**||||  
|Anwendung generiert überwachen||||  
|Zertifizierungsdienste überwachen||||  
|Detaillierte Dateifreigabe überwachen||||  
|Dateifreigabe überwachen||||  
|Dateisystem überwachen||||  
|Filterplattformverbindung überwachen||||  
|Filterplattform: Verworfene Pakete überwachen||||  
|Handleänderung überwachen||||  
|Kernelobjekt überwachen||||  
|Andere Objektzugriffsereignisse überwachen||||  
|Registrierung überwachen||||  
|Wechselmedien überwachen||||  
|SAM überwachen||||  
|Staging zentraler Zugriffsrichtlinien überwachen||||  
|**Richtlinienänderung**||||  
|Überwachungsrichtlinienänderung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|Authentifizierungsrichtlinienänderung überwachen|Ja Nein|Ja Nein|Ja, ja|  
|Autorisierungsrichtlinienänderung überwachen||||  
|Filterplattform-Richtlinienänderung überwachen||||  
|MPSSVC-Richtlinienänderung auf Regelebene überwachen|||Ja  |  
|Andere Richtlinienänderungsereignisse überwachen||||  
|**Berechtigungen**||||  
|Nicht sensible Verwendung von Rechten überwachen||||  
|Andere Rechteverwendungsereignisse überwachen||||  
|Sensible Verwendung von Rechten überwachen||||  
|**System**||||  
|IPsec-Treiber überwachen||Ja, ja|Ja, ja|  
|Andere Systemereignisse überwachen|Ja, ja|||  
|Sicherheitsstatusänderung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|Sicherheitssystemerweiterung überwachen||Ja, ja|Ja, ja|  
|Systemintegrität überwachen|Ja, ja|Ja, ja|Ja, ja|  
|**Globale Objektzugriffsüberwachung**||||  
|IPsec-Treiber überwachen||||  
|Andere Systemereignisse überwachen||||  
|Sicherheitsstatusänderung überwachen||||  
|Sicherheitssystemerweiterung überwachen||||  
|Systemintegrität überwachen||||  

## <a name="set-audit-policy-on-workstations-and-servers"></a>Festlegen der Überwachungsrichtlinie für Arbeitsstationen und Server  
Alle Ereignisprotokoll-Verwaltungspläne sollten Arbeitsstationen und Server überwachen. Ein häufiger Fehler besteht darin, nur Server oder Domänen Controller zu überwachen. Da böswillige Hacker häufig auf Arbeitsstationen auftreten, wird die beste und früheste Informationsquelle nicht durch die Überwachung von Arbeitsstationen ignoriert.  

Administratoren sollten alle Überwachungs Richtlinien vor der Implementierung in Ihrer Produktionsumgebung sorgfältig prüfen und testen.  

## <a name="events-to-monitor"></a>Zu überwachende Ereignisse  
Eine perfekte Ereignis-ID zum Generieren einer Sicherheitswarnung sollte die folgenden Attribute enthalten:  

-   Hohe Wahrscheinlichkeit, dass das Vorkommen nicht autorisierte Aktivitäten anzeigt  

-   Eine geringe Anzahl falsch positiver Ergebnisse generieren  

-   Das Vorkommen sollte zu einer Untersuchung/forensischen Antwort führen.  

Es sollten zwei Arten von Ereignissen überwacht und gewarnt werden:  

1.  Ereignisse, bei denen sogar ein einzelnes Vorkommen nicht autorisierte Aktivitäten anzeigt  

2.  Eine Häufung von Ereignissen, die eine erwartete und akzeptierte Baseline überschreitet  

Ein Beispiel für das erste Ereignis ist:  

Wenn die Anmeldung von Domänen-Admins (das) an Computern, die keine Domänen Controller sind, untersagt ist, sollte ein einzelnes Vorkommen eines da-Mitglieds, das sich an einer Endbenutzer Arbeitsstation anmeldet, eine Warnung generieren und untersuchen. Diese Art von Warnung ist leicht zu generieren, indem Sie das Audit Special Logon Event 4964 (spezielle Gruppen wurden einer neuen Anmeldung zugewiesen) verwenden. Weitere Beispiele für einzelinstanzwarnungen:  

-   Wenn Server a nie eine Verbindung mit Server B herstellen soll, wird eine Warnung angezeigt, wenn eine Verbindung untereinander hergestellt wird.  

-   Warnung, wenn ein normales Endbenutzer Konto unerwartet einer sensiblen Sicherheitsgruppe hinzugefügt wird.  

-   Wenn Mitarbeiter am Hersteller Standort A nie nachts arbeiten, wird eine Warnung angezeigt, wenn sich ein Benutzer bei Mitternacht anmeldet.  

-   Warnung, wenn ein nicht autorisierter Dienst auf einem Domänen Controller installiert ist.  

-   Überprüfen Sie, ob ein regulärer Endbenutzer versucht, sich direkt bei einem SQL Server anzumelden, für den es keinen eindeutigen Grund gibt.  

-   Wenn Sie in der Gruppe "da" keine Mitglieder haben, die sich selbst hinzufügen, überprüfen Sie Sie sofort.  

Ein Beispiel für das zweite Ereignis ist:  

Eine Abbruch Anzahl fehlgeschlagener Anmeldungen könnte auf einen Kenn Wort angriffsangriff hindeuten. Damit ein Unternehmen eine Warnung für eine ungewöhnlich hohe Anzahl fehlgeschlagener Anmeldungen bereitstellen kann, müssen Sie zunächst die normalen Ebenen der fehlgeschlagenen Anmeldungen innerhalb Ihrer Umgebung vor einem böswilligen Sicherheits Ereignis verstehen.  

Eine umfassende Liste der Ereignisse, die Sie beim Überwachen von Gefährdungen berücksichtigen sollten, finden Sie unter [Anhang L: zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md).  

## <a name="active-directory-objects-and-attributes-to-monitor"></a>Active Directory zu überwachende Objekte und Attribute  
Im folgenden finden Sie die Konten, Gruppen und Attribute, die Sie überwachen sollten, um zu erkennen, dass Sie versuchen, die Active Directory Domain Services Installation zu kompromittieren.  

-   Systeme zum Deaktivieren oder Entfernen von Antiviren-und Antischadsoftware (automatischer Neustart des Schutzes, wenn er manuell deaktiviert wird)  

-   Administrator Konten für nicht autorisierte Änderungen  

-   Aktivitäten, die mithilfe privilegierter Konten ausgeführt werden (Konto automatisch entfernen, wenn verdächtige Aktivitäten abgeschlossen sind oder die zugewiesene Zeit abgelaufen ist)  

-   Privilegierte und VIP-Konten in AD DS. Überwachen Sie Änderungen, insbesondere Änderungen an Attributen auf der Registerkarte "Konto" (z. b. cn, Name, sAMAccountName, userPrincipalName oder userAccountControl). Zusätzlich zum Überwachen der Konten beschränken Sie den Benutzer, der die Konten ändern kann, so gering wie möglich auf eine Gruppe von Administratoren.  

Eine Liste der zu überwachenden empfohlenen Ereignisse, deren kritikitäts Bewertungen und eine Zusammenfassung der Ereignismeldungen finden Sie unter [Anhang L: zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md) .  

-   Gruppieren Sie Server nach der Klassifizierung ihrer Arbeits Auslastungen, sodass Sie schnell die Server identifizieren können, die am ehesten überwacht werden sollen und die am meisten stringterweise konfiguriert sind.  

-   Änderungen an den Eigenschaften und der Mitgliedschaft der folgenden AD DS Gruppen: Organisations-Admins (EA), Domänen-Admins (da), Administratoren (BA) und Schema-Admins (SA)  

-   Deaktivieren privilegierter Konten (z. b. integrierte Administrator Konten in Active Directory und auf Mitglieds Systemen) zum Aktivieren der Konten  

-   Verwaltungs Konten zum Protokollieren aller Schreibvorgänge an das Konto  

-   Integrierter Sicherheitskonfigurations-Assistent zum Konfigurieren von Dienst-, Registrierungs-, Überwachungs-und Firewalleinstellungen, um die Angriffsfläche des Servers zu verringern. Verwenden Sie diesen Assistenten, wenn Sie Jump-Server als Teil ihrer Verwaltungs Host Strategie implementieren.  

## <a name="additional-information-for-monitoring-active-directory-domain-services"></a>Weitere Informationen zum Überwachen von Active Directory Domain Services  
Überprüfen Sie die folgenden Links, um weitere Informationen zur Überwachungs AD DS zu finden:  
  
-   Die [globale Objekt Zugriffs Überwachung ist magisch](/archive/blogs/askds/global-object-access-auditing-is-magic) . Sie enthält Informationen zum Konfigurieren und Verwenden der erweiterten Überwachungs Richtlinien Konfiguration, die zu Windows 7 und Windows Server 2008 R2 hinzugefügt wurde.  

-   [Einführung von Überwachungs Änderungen in Windows 2008](/archive/blogs/askds/introducing-auditing-changes-in-windows-2008) : führt die in Windows 2008 vorgenommenen Überwachungs Änderungen ein.  

-   Praktische Überwachungs [Tricks in Vista und 2008](/archive/blogs/askds/cool-auditing-tricks-in-vista-and-2008) : erläutert interessante neue Features der Überwachung in Windows Vista und Windows Server 2008, die für die Problembehandlung oder das Auftreten von Ereignissen in Ihrer Umgebung verwendet werden können.  

-   [Zentrale Anlaufstelle für die Überwachung in Windows Server 2008 und Windows Vista](/archive/blogs/askds/one-stop-shop-for-auditing-in-windows-server-2008-and-windows-vista) : enthält eine Kompilierung von Überwachungs Features und Informationen, die in Windows Server 2008 und Windows Vista enthalten sind.  

-   [Schritt-für-Schritt-Anleitung](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731607(v=ws.10)) für die AD DS Überwachung: Beschreibt das neue Active Directory Domain Services (AD DS)-Überwachungs Feature in Windows Server 2008. Außerdem werden Verfahren zur Implementierung dieses neuen Features bereitstellt.  

## <a name="general-list-of-security-event-id-recommendation-criticalities"></a>Allgemeine Liste der Empfehlungen für die Ereignis-ID der Sicherheits Ereignis-ID  
Alle Empfehlungen für Ereignis-IDs werden folgendermaßen mit einer kritikitäts Bewertung versehen:  

**Hoch:** Ereignis-IDs mit einer Bewertung mit hoher Kritizität sollten immer und sofort benachrichtigt und untersucht werden.  

**Mittel:** Eine Ereignis-ID mit einer mittelgroßen kritiktivitäts Bewertung kann auf schädliche Aktivitäten hindeuten, aber Sie muss von einer anderen unter Normalität begleitet werden (z. b. eine ungewöhnliche Zahl, die in einem bestimmten Zeitraum auftritt, unerwartete vorkommen oder Vorkommen auf einem Computer, der normalerweise nicht erwartet wird, dass das Ereignis protokolliert wird.). Ein Ereignis mit mittlerer Kritizität kann auch als Metrik erfasst und im Laufe der Zeit verglichen werden.  

**Niedrig:** Und die Ereignis-ID mit Ereignissen mit niedriger Kritizität sollten nicht berücksichtigt werden oder Warnungen auslösen, es sei denn, Sie korrelieren mit mittleren oder hohen kritiktätsereignissen.  

Diese Empfehlungen sollen eine grundlegende Anleitung für den Administrator bereitstellen. Alle Empfehlungen sollten vor der Implementierung in einer Produktionsumgebung gründlich geprüft werden.  

Eine Liste der zu überwachenden empfohlenen Ereignisse, deren kritikitäts Bewertungen und eine Zusammenfassung der Ereignismeldungen finden Sie unter [Anhang L: zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md) .  
