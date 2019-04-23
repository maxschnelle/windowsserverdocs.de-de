---
ms.assetid: 0abe0976-4b49-45d6-a7b3-81d28bdb8210
title: Empfehlungen zu Überwachungsrichtlinien
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 343a9a7aedf22e9c021249f00fb628f871a2ce1f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835751"
---
# <a name="audit-policy-recommendations"></a>Empfehlungen zu Überwachungsrichtlinien

>Gilt für: Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012, Windows 10, Windows 8.1, Windows 7

In diesem Abschnitt werden die Windows-Standard-überwachungsrichtlinieneinstellungen, empfohlene sicherheitsüberwachungs-Richtlinieneinstellungen, und die umfangreichere wiederherstellungsanforderungen erforderlich Empfehlungen von Microsoft für Arbeitsstation und Server-Produkte.  

Zusammen mit den Einstellungen, es wird empfohlen, um die Gefährdung, erkennen hier gezeigten SCM grundlegende Empfehlungen sollen nur einer Basislinie ab, an Administratoren sein. Jede Organisation muss einen eigenen Entscheidungen in Bezug auf die Gefahren vorgestellt, die sie sehen, ihre Toleranzen annehmbares Risiko, und Audit Policy Kategorien und Unterkategorien ermöglichen sollte wird. Weitere Informationen zu Bedrohungen, finden Sie in der [Handbuch zu Bedrohungen und Gegenmaßnahmen](https://technet.microsoft.com/library/hh125921(v=ws.10).aspx). Administratoren ohne eine durchdachte Überwachungsrichtlinie werden empfohlen, die mit den hier empfohlenen Einstellungen zu starten und dann zu ändern und zu testen, vor der Implementierung in ihrer produktionsumgebung.  

Die Empfehlungen sind für Enterprise-Class-Computer, bei denen Microsoft als Computer definiert, die durchschnittliche sicherheitsanforderungen haben und ein hohes Maß an Betrieb erforderlich. Überwachungsrichtlinien für Entitäten, die höhere Sicherheit, die Anforderungen aggressiver berücksichtigen sollten benötigen.  

> [!NOTE]  
> Microsoft Windows wird standardmäßig und grundlegende Empfehlungen entnommen wurden die [Microsoft Security Compliance Manager-Tool](https://technet.microsoft.com/library/cc677002.aspx).  

Die folgenden Baseline sicherheitsüberwachungs-Richtlinieneinstellungen werden für Computer mit normaler Sicherheit empfohlen, die nicht bekannt sind, aktiv, erfolgreich angegriffen werden bestimmte Angreifer oder Malware.  

## <a name="recommended-audit-policies-by-operating-system"></a>Empfohlene Überwachungsrichtlinien, die vom Betriebssystem  
Dieser Abschnitt enthält die Tabellen, die die Überwachung einstellungsempfehlungen aufzulisten, die für die folgenden Betriebssysteme gelten:  

-   Windows Server 2016 

-   Windows Server 2012  

-   Windows Server 2012 R2  

-   WindowsServer 2008  

-   Windows 10

-   Windows 8.1  

-   Windows 7  

Diese Tabellen enthalten die Windows-Standardeinstellung, grundlegende Empfehlungen und die stärkeren Empfehlungen für diese Betriebssysteme.  

**Audit Policy Tabellen Legende**  

|||  
|-|-|  
|**Notation**|**Empfehlung**|  
|JA|Im allgemeinen Szenarien aktivieren|  
|NEIN|Führen Sie **nicht** ermöglichen im allgemeinen Szenarien|  
|IF|Aktivieren Sie bei Bedarf für ein bestimmtes Szenario oder eine Rolle oder eines Features, die für die Überwachung erforderlich ist auf dem Computer installiert ist|  
|DC|Aktivieren Sie auf einem Domänencontroller|  
|[Leere]|Keine Empfehlung|  

**Windows 10, Windows 8 und Windows 7 Audit Settings Empfehlungen**  

**Überwachungsrichtlinie**  

|Audit Policy-Kategorie oder Unterkategorie|Windows-Standard<br /><br />Erfolg Fehler|Baseline-Empfehlung<br /><br />Erfolg Fehler|Eine stärkere Empfehlung<br /><br />Erfolg Fehler|  
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
|**Detaillierte nachverfolgung**||||  
|DPAPI-Aktivität überwachen|||Ja, ja|  
|Prozesserstellung überwachen||Ja Nein|Ja, ja|  
|Prozessbeendung überwachen||||  
|RPC-Ereignisse überwachen||||  
|**DS-Zugriff**||||  
|Detaillierte Verzeichnisdienstreplikation überwachen||||  
|Verzeichnisdienstzugriff überwachen||||  
|Verzeichnisdienständerungen überwachen||||  
|Verzeichnisdienstreplikation überwachen||||  
|**An- und Abmeldung**||||  
|Kontosperrung überwachen|Ja Nein||Ja Nein|  
|Benutzer-/Geräteansprüche überwachen||||  
|IPsec-Erweiterungsmodus überwachen||||  
|IPsec-Hauptmodus überwachen|||IF     IF|  
|IPsec-Schnellmodus überwachen||||  
|Abmelden überwachen|Ja Nein|Ja Nein|Ja Nein|  
|Überwachen der Anmeldung <sup>1</sup>|Ja, ja|Ja, ja|Ja, ja|  
|Netzwerkrichtlinienserver überwachen|Ja, ja|||  
|Andere Anmelde-/Abmeldeereignisse überwachen||||  
|Spezielle Anmeldung überwachen|Ja Nein|Ja Nein|Ja, ja|  
|**Zugriff auf Objekte**||||  
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
|**Änderung der Richtlinie**||||  
|Überwachungsrichtlinienänderung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|Authentifizierungsrichtlinienänderung überwachen|Ja Nein|Ja Nein|Ja, ja|  
|Autorisierungsrichtlinienänderung überwachen||||  
|Filterplattform-Richtlinienänderung überwachen||||  
|MPSSVC-Richtlinienänderung auf Regelebene überwachen|||Ja  |  
|Andere Richtlinienänderungsereignisse überwachen||||  
|**Rechteverwendung**||||  
|Nicht sensible Verwendung von Rechten überwachen||||  
|Andere Rechteverwendungsereignisse überwachen||||  
|Sensible Verwendung von Rechten überwachen||||  
|**System**||||  
|IPsec-Treiber überwachen||Ja, ja|Ja, ja|  
|Andere Systemereignisse überwachen|Ja, ja|||  
|Sicherheitsstatusänderung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|Sicherheitssystemerweiterung überwachen||Ja, ja|Ja, ja|  
|Systemintegrität überwachen|Ja, ja|Ja, ja|Ja, ja|  
|**Globale Überprüfung**||||  
|IPsec-Treiber überwachen||||  
|Andere Systemereignisse überwachen||||  
|Sicherheitsstatusänderung überwachen||||  
|Sicherheitssystemerweiterung überwachen||||  
|Systemintegrität überwachen||||  

<sup>1</sup> ab Windows 10, Version 1809, Überwachung der Anmeldung standardmäßig für sowohl Erfolgs-als auch aktiviert ist. In früheren Versionen von Windows ist nur erfolgreich, standardmäßig aktiviert.

**WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2 und Windows Server 2008 Audit Settings Empfehlungen**  

|Audit Policy-Kategorie oder Unterkategorie|Windows-Standard<br /><br />Erfolg Fehler|Baseline-Empfehlung<br /><br />Erfolg Fehler|Eine stärkere Empfehlung<br /><br />Erfolg Fehler|  
|----------------------------------------|------------------------------------------|--------------------------------------------------|--------------------------------------------------|  
|**Kontoanmeldung**||||  
|Überprüfen der Anmeldeinformationen überwachen|Nein, nein|Ja, ja|Ja, ja|  
|Kerberos-Authentifizierungsdienst überwachen|||Ja, ja|  
|Ticketvorgänge des Kerberos-Diensts überwachen|||Ja, ja|  
|Andere Kontoanmeldungsereignisse überwachen|||Ja, ja|  
|**Kontoverwaltung**||||  
|Anwendungsgruppenverwaltung überwachen||||  
|Computerkontoverwaltung überwachen||Ja DC|Ja, ja|  
|Verteilergruppenverwaltung überwachen||||  
|Andere Kontoverwaltungsereignisse überwachen||Ja, ja|Ja, ja|  
|Sicherheitsgruppenverwaltung überwachen||Ja, ja|Ja, ja|  
|Benutzerkontenverwaltung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|**Detaillierte nachverfolgung**||||  
|DPAPI-Aktivität überwachen|||Ja, ja|  
|Prozesserstellung überwachen||Ja Nein|Ja, ja|  
|Prozessbeendung überwachen||||  
|RPC-Ereignisse überwachen||||  
|**DS-Zugriff**||||  
|Detaillierte Verzeichnisdienstreplikation überwachen||||  
|Verzeichnisdienstzugriff überwachen||DC    DC|DC    DC|  
|Verzeichnisdienständerungen überwachen||DC    DC|DC    DC|  
|Verzeichnisdienstreplikation überwachen||||  
|**An- und Abmeldung**||||  
|Kontosperrung überwachen|Ja Nein||Ja Nein|  
|Benutzer-/Geräteansprüche überwachen||||  
|IPsec-Erweiterungsmodus überwachen||||  
|IPsec-Hauptmodus überwachen|||IF     IF|  
|IPsec-Schnellmodus überwachen||||  
|Abmelden überwachen|Ja Nein|Ja Nein|Ja Nein|  
|Anmelden überwachen|Ja, ja|Ja, ja|Ja, ja|  
|Netzwerkrichtlinienserver überwachen|Ja, ja|||  
|Andere Anmelde-/Abmeldeereignisse überwachen|||Ja, ja|  
|Spezielle Anmeldung überwachen|Ja Nein|Ja Nein|Ja, ja|  
|**Zugriff auf Objekte**||||  
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
|**Änderung der Richtlinie**||||  
|Überwachungsrichtlinienänderung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|Authentifizierungsrichtlinienänderung überwachen|Ja Nein|Ja Nein|Ja, ja|  
|Autorisierungsrichtlinienänderung überwachen||||  
|Filterplattform-Richtlinienänderung überwachen||||  
|MPSSVC-Richtlinienänderung auf Regelebene überwachen|||Ja  |  
|Andere Richtlinienänderungsereignisse überwachen||||  
|**Rechteverwendung**||||  
|Nicht sensible Verwendung von Rechten überwachen||||  
|Andere Rechteverwendungsereignisse überwachen||||  
|Sensible Verwendung von Rechten überwachen||||  
|**System**||||  
|IPsec-Treiber überwachen||Ja, ja|Ja, ja|  
|Andere Systemereignisse überwachen|Ja, ja|||  
|Sicherheitsstatusänderung überwachen|Ja Nein|Ja, ja|Ja, ja|  
|Sicherheitssystemerweiterung überwachen||Ja, ja|Ja, ja|  
|Systemintegrität überwachen|Ja, ja|Ja, ja|Ja, ja|  
|**Globale Überprüfung**||||  
|IPsec-Treiber überwachen||||  
|Andere Systemereignisse überwachen||||  
|Sicherheitsstatusänderung überwachen||||  
|Sicherheitssystemerweiterung überwachen||||  
|Systemintegrität überwachen||||  

## <a name="set-audit-policy-on-workstations-and-servers"></a>Festlegen von Überwachungsrichtlinien auf Arbeitsstationen und Servern  
Alle Event Log-Management-Pläne sollten auf Arbeitsstationen und Server überwachen. Ein häufiger Fehler werden nur Server oder Domänencontroller überwacht. Da bösartige Hackerangriffe häufig anfänglich auf Arbeitsstationen auftritt, ist die beste und früheste Informationsquelle nicht überwacht Arbeitsstationen ignoriert werden.  

Administratoren sollten so zuvorkommend überprüfen und Testen alle Überwachungsrichtlinie vor der Implementierung in ihrer produktionsumgebung.  

## <a name="events-to-monitor"></a>Zu überwachende Ereignisse  
Eine perfekte Ereignis-ID, um eine sicherheitswarnung generieren, sollten die folgenden Attribute enthalten:  

-   Hohe Wahrscheinlichkeit, dass dieses Ereignis gibt an, nicht autorisierte Aktivitäten  

-   Eine geringe Anzahl falsch positiver Ergebnisse generieren  

-   Vorkommen sollte zu einer von forensischen führen.  

Zwei Arten von Ereignissen sollten überwacht und benachrichtigt werden:  

1.  Diese Ereignisse, in denen auch ein einmaliges auftreten auf nicht autorisierte Aktivitäten hinweist  

2.  Eine Häufung von Ereignissen, die eine erwartete und akzeptierte Baseline überschreitet  

Ein Beispiel für das erste Ereignis ist:  

Wenn Domänen-Admins (DAs) von Protokollierung auf den Computern nicht, die keine Domänencontroller sind zulässig sind, ein einzelnes Vorkommen eines Daten-Elements, das Anmelden an einer Endbenutzerarbeitsstation eine Warnung generieren soll, und untersucht werden. Dieser Warnungstyp ist einfach zu generieren, indem Sie mithilfe des Ereignisses spezielle Anmeldung überwachen 4964 (besondere Gruppen zugewiesen wurden, eine neue Anmeldung). Andere Beispiele für Einzelinstanz-Warnungen sind:  

-   Wenn Server A zu Server B, Warnung, wenn sie eine Verbindung miteinander herstellen nie verbinden soll.  

-   Warnung senden Sie, wenn eine normale Endbenutzerkonto unerwartet eine vertrauliche Sicherheitsgruppe hinzugefügt wird.  

-   Wenn Mitarbeiter in den Speicherort der Factory ein niemals in der Nacht werden die Warnungen bei eines Benutzers um Mitternacht funktionieren Anmeldung.  

-   Warnung senden Sie, wenn ein nicht autorisierter Dienst auf einem Domänencontroller installiert ist.  

-   Untersuchen Sie, ob eine reguläre Endbenutzer, sich direkt bei einer SQL Server für die sie keine klare Grund versucht dafür haben.  

-   Wenn Sie keine Elemente in der Verwaltungsgruppe Daten haben und ein Benutzer sich selbst es hinzufügt, überprüfen Sie ihn sofort.  

Ein Beispiel für das zweite Ereignis ist:  

Eine abweichende Anzahl von fehlerhaften Anmeldungen kann das Erraten des Kennworts hinweisen. Für ein Unternehmen, eine Warnung für eine ungewöhnlich hohe Anzahl von fehlgeschlagenen Anmeldungen bereitzustellen müssen sie zuerst die normalen Ebenen der Anmeldefehler in ihrer Umgebung vor einer böswilligen Sicherheitsereignis verstehen.  

Eine umfassende Liste der Ereignisse, die Sie enthalten soll, wenn Sie auf Anzeichen einer Kompromittierung überwachen, finden Sie unter [Anhang L: Zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md).  

## <a name="active-directory-objects-and-attributes-to-monitor"></a>Active Directory-Objekten und-Attributen zu überwachen  
Im folgenden sind die Konten, Gruppen und Attribute, die Sie überwachen sollten, damit Sie das Erkennen von versuchen, Ihre Active Directory Domain Services-Installation zu gefährden können.  

-   Systeme, für das Deaktivieren oder Entfernen von Antivirus- und Antischadsoftware-Software (automatisch Neustarten des Schutzes, wenn sie manuell deaktiviert ist)  

-   Administratorkonten für nicht autorisierte Änderungen  

-   Aktivitäten, die ausgeführt werden, mithilfe von privilegierten Konten (automatisch Konto entfernen, wenn Sie die verdächtige Aktivitäten abgeschlossen sind, oder vorgesehene Zeit abgelaufen)  

-   Privilegierten und VIP-Konten in AD DS. Überwachen Sie Änderungen, insbesondere Änderungen von Attributen auf der Registerkarte "Konto" (z. B. Cn, Name, "sAMAccountName", "userPrincipalName" oder "UserAccountControl"). Zusätzlich zur Überwachung der Konten an, zu beschränken, den Konten an, wie klein einen Satz von Administratoren wie möglich geändert werden kann.  

Finden Sie unter [Anhang L: Zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md) für eine Liste der empfohlenen Ereignisse zu überwachen, ihre Wichtigkeit Bewertungen und eine Zusammenfassung der Ereignis-Nachricht.  

-   Gruppe von Servern mit der die Klassifizierung der ihre Workloads, sodass Sie schnell die Server zu identifizieren, die die am ehesten überwachten und die meisten repräsentative Motoröltemperatur konfiguriert werden sollen  

-   Änderungen an den Eigenschaften und die Mitgliedschaft in der folgenden AD DS-Gruppen: Organisations-Admins (EA), Domänen-Admins (DA), die Administratoren (BA) und Schema-Admins (SA)  

-   Zum Aktivieren von Konten deaktiviert privilegierte Konten (z. B. der integrierte Administrator-Konten in Active Directory und auf Systemen, die Mitglied)  

-   Management-Konten alle Schreibvorgänge an das Konto anmelden  

-   Integrierte Sicherheitskonfigurations-Assistenten so konfigurieren Sie den Dienst, Registrierung, überwachungs- und Firewall-Einstellungen für die Angriffsfläche des Servers zu verringern. Verwenden Sie diesen Assistenten, wenn Sie Jump-Server als Teil Ihrer Strategie für die administrative Host implementieren.  

## <a name="additional-information-for-monitoring-active-directory-domain-services"></a>Weitere Informationen zum Überwachen von Active Directory-Domänendienste  
Überprüfen Sie den folgenden Links Weitere Informationen zur Überwachung von AD DS:  
  
-   [Globale Objektzugriffsüberwachung Magic ist](http://blogs.technet.com/b/askds/archive/2011/03/10/global-object-access-auditing-is-magic.aspx) – enthält Informationen zum Konfigurieren und verwenden die erweiterte Überwachungsrichtlinienkonfiguration, die Windows 7 und Windows Server 2008 R2 hinzugefügt wurde.  

-   [Einführung in die Überwachung von Änderungen in Windows 2008](http://blogs.technet.com/b/askds/archive/2007/10/19/introducing-auditing-changes-in-windows-2008.aspx) -Überwachung in Windows 2008 vorgenommenen Änderungen führt.  

-   ["Cool" Überwachung Tricks in Vista und 2008](http://blogs.technet.com/b/askds/archive/2007/11/16/cool-auditing-tricks-in-vista-and-2008.aspx) -interessante neue Features der Überwachung in Windows Vista und Windows Server 2008, die verwendet werden können, für die Behandlung von Problemen oder sehen die Abläufe in Ihrer Umgebung erläutert.  

-   [Zentrale Anlaufstelle für die Überwachung in Windows Server 2008 und Windows Vista](http://blogs.technet.com/b/askds/archive/2008/03/27/one-stop-shop-for-auditing-in-windows-server-2008-and-windows-vista.aspx) -enthält eine Zusammenstellung von Überwachung von Funktionen und Informationen, die in Windows Server 2008 und Windows Vista enthalten sind.  

-   [Anleitung für AD DS-Überwachung](https://technet.microsoft.com/library/a9c25483-89e2-4202-881c-ea8e02b4b2a5.aspx) -beschreibt die neue Überwachungsfunktion mit Active Directory Domain Services (AD DS) in Windows Server 2008. Darüber hinaus werden Verfahren zur Implementierung dieser neuen Funktion.  

## <a name="general-list-of-security-event-id-recommendation-criticalities"></a>Allgemeine-Liste der Security-Ereignis-ID Empfehlung Kritikalitäten  
Alle Ereignis-ID-Empfehlungen werden nach eine Bedeutung, die Bewertung wie folgt ergänzt:  

**Hoch:** Ereignis-IDs mit einer Bewertung von hoher Wichtigkeit sollte immer sofort benachrichtigt und untersucht werden.  

**Mittel:** Ereignis-ID mit der Bewertung mittlerer Wichtigkeit deutet auf böswilligen Aktivitäten, aber es muss durch einige andere abnormalen Systemverhalten begleitet werden (z. B. eine ungewöhnlich hohe Anzahl in einen bestimmten Zeitraum, unerwartete Vorkommen oder Vorkommen auf einem Computer auftritt, Normalerweise würden nicht davon ausgegangen werden, die das Ereignis zu protokollieren.). Ein Mittel-wie-Ereignis kann auch r als Metrik gesammelt und im Laufe der Zeit verglichen.  

**Niedrig:** Und Ereignis-ID mit der eine geringe Wichtigkeit Ereignisse sollte nicht beim Sammeln von Aufmerksamkeit oder dazu führen, dass Warnungen, es sei denn, die mit mittlerem oder hohem Wichtigkeit Ereignisse korreliert.  

Diese Empfehlungen sind für den Administrator zu einer Basislinie vorgesehen. Alle Empfehlungen sollten vor der Implementierung in einer produktionsumgebung gründlich überprüft werden.  

Finden Sie unter [Anhang L: Zu überwachende Ereignisse](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md) eine Liste der empfohlenen Ereignisse zu überwachen, ihre Wichtigkeit Bewertungen und eine Zusammenfassung der Ereignis-Nachricht.  
