---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: Windows Server2016-Funktionsebenen
description: 
author: MicrosoftGuyJFlo
ms.author: joflore
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: a39955cf088ce7ce8bef20c70b83d49c6d508497
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="forest-and-domain-functional-levels"></a>Funktionsebenen der Gesamtstruktur und Domäne

>Gilt für: Windows Server

Müssen mit dem Ende des Lebenszyklus von Windows2003 Windows2003-Domänencontrollern (DCs) auf Windows Server2008, 2012 oder 2016 aktualisiert werden. Daher sollten alle Domänencontroller, die Windows Server2003 ausgeführt wird, aus der Domäne entfernt werden. Die Domäne und Gesamtstruktur-Funktionsebene ausgelöst werden soll mindestens Windows Server2008, um zu verhindern, dass einen Domänencontroller, der eine frühere Version von Windows Server ausgeführt wird, von der Umgebung hinzugefügt wird.

Es wird empfohlen, dass Kunden Aktualisieren von der Domänenfunktionsebene (DFL) und die Funktionsebene der Gesamtstruktur (FFL) im Rahmen dieser, da die DFL 2003 und FFL in Windows Server2016 entfernt wurden und sie nicht mehr in zukünftigen unterstützt werden Versionen.

Für Kunden, die zusätzliche Zeit zum Bewerten, verschieben die Domänenfunktionsebene & FFL von 2003 erforderlich, die DFL 2003 und FFL weiterhin mit Windows10 unterstützt werden und die Windows Server2016 alle Domänencontroller in der Domäne und Gesamtstruktur auf Windows Server2008, 2008 R2, 2012 2012R2, oder 2016.

In der Windows Server2008 und höhere Domänenfunktionsebenen wird Replikation des verteilten Dienst (Distributed File System, DFS) zum Replizieren von SYSVOL-Ordnerinhalte zwischen Domänencontrollern verwendet. Wenn Sie eine neue Domäne, auf der Domänenfunktionsebene Windows Server2008 oder höher erstellen, wird die DFS-Replikation zum Replizieren von SYSVOL automatisch verwendet. Wenn Sie auf einer niedrigeren funktionale Ebene die Domäne erstellt haben, müssen Sie über das Verwenden der FRS-zur DFS-Replikation für SYSVOL migriert. Für Migrationsschritte, können Sie entweder führen Sie die [Verfahren auf TechNet](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) oder verweisen Sie auf die [optimiert die Schritteim Storage Team File Cabinet Blog](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx).

Die Windows Server2003-Domäne und Gesamtstruktur-Funktionsebenen werden weiterhin unterstützt, aber Organisationen sollten die Funktionsebene der Windows Server2008 (oder höher, wenn möglich) sorgen für Kompatibilität mit SYSVOL-Replikation und in Zukunft zu unterstützen. Darüber hinaus stehen viele Vorteile und Funktionen auf der höheren höherer Funktionsebenen. Weitere Informationen finden Sie unter den folgenden Ressourcen für Weitere Informationen:

## <a name="windows-server-2016"></a>Windows Server 2016

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Level-Funktionen von Windows Server2016-Gesamtstruktur

* Alle Features, die auf der Funktionsebene von Windows Server 2012R2 Gesamtstruktur verfügbar sind, und die folgenden Features stehen zur Verfügung:
    * [Privileged Access Management (PAM) mithilfe von Microsoft Identity Manager (MIM)] (https://docs.microsoft.com/windows-server/identity/what's-new-active-directory-Domain-services#a-namebkmkpamaprivileged-access-Management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Level-Funktionen von Windows Server2016-Domäne

* Alle Active Directory-Standardfeatures, alle Features von Windows Server 2012R2 als Domänenfunktionsebene sowie die folgenden Features:
    * DCs unterstützen einen öffentlichen Schlüssel nur NTLM geheimen Schlüssel des Benutzers zurücksetzen. 
    * Wenn ein Benutzer auf bestimmte Geräte in einer Domäne ist, können Domänencontroller ermöglicht Netzwerk NTLM unterstützen. 
    * Kerberos-Clients erfolgreich authentifizieren mit der Erweiterung PKInit Aktualität erhalten die neue öffentliche Schlüssel Identität SID.

    Weitere Informationen finden Sie unter [What's New in Kerberos Authentication](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication) und [Neues in den Schutz von Anmeldeinformationen](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2016
* Windows Server2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>2012R2 Gesamtstruktur funktionale Ebene Features von Windows Server

* Alle Features, die in Windows Server2012 verfügbaren Gesamtstruktur funktionale Ebene, jedoch keine zusätzlichen Features.

### <a name="windows-server-2012r2-domain-functional-level-features"></a>2012R2 Domäne funktionale Ebene Features von Windows Server

* Alle Active Directory-Standardfeatures, alle Features der Domänenfunktionsebene Windows Server2012 sowie die folgenden Features:
    * DC-Seite Schutzmaßnahmen für geschützte Benutzer. Geschützte Authentifizieren von Benutzern zu einer Windows Server2012 R2-Domäne nicht mehr zu können:
        * Authentifizieren mit NTLM-Authentifizierung
        * Verwenden von des- oder RC4-Verschlüsselungssammlungen in Kerberos-Vorauthentifizierung
        * Mit uneingeschränkter oder eingeschränkter Delegierung delegiert werden
        * Erneuern von Benutzertickets (TGTs) über die ersten 4 Stunden hinaus
    * Authentifizierungsrichtlinien
        * Neue Gesamtstruktur-Active Directory-Richtlinien die auf Konten in Windows Server2012 R2-Domänen zu steuern, welche Hosts angewendet werden können ein Konto kann aus anmelden und gelten zugriffssteuerungsbedingungen zur Authentifizierung für Dienste, die mit einem Konto ausgeführt.
    * Authentifizierungsrichtliniensilos
        * Neue Gesamtstruktur-basierten Active Directory-Objekt, die eine Beziehung zwischen Benutzer-, verwaltete und, Konten verwendet werden, die Konten für Authentifizierungsrichtlinien oder für die Authentifizierung Isolation klassifizieren erstellen können.

## <a name="windows-server-2012"></a>Windows Server 2012

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2016
* Windows Server2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Level-Funktionen von Windows Server2012-Gesamtstruktur

* Alle Features, die in der Windows Server2008 R2 verfügbaren Gesamtstruktur funktionale Ebene, jedoch keine zusätzlichen Features.

### <a name="windows-server-2012-domain-functional-level-features"></a>Level-Funktionen von Windows Server2012-Domäne

* Alle Active Directory-Standardfeatures, alle Features von Windows Server2008 R2 als Domänenfunktionsebene sowie die folgenden Features:
    * Der KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring KDC-verwaltungsvorlagenrichtlinie verfügt über zwei Einstellungen (immer Ansprüche bereitstellen und Authentifizierungsanfragen), für die Windows Server2012 als Domänenfunktionsebene erforderlich. Weitere Informationen finden Sie unter [What's New in Kerberos Authentication](https://technet.microsoft.com/en-us/library/hh831747.aspx)

## <a name="windows-server-2008r2"></a>Windows Server2008 R2

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2016
* Windows Server2012 R2
* Windows Server 2012
* Windows Server2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server2008 R2-Gesamtstruktur funktionale Ebene Features

* Alle Features, die in der Windows Server2003 verfügbaren Gesamtstruktur-Funktionsebene sowie die folgenden Features:
    * Active Directory-Papierkorb, der bietet die Möglichkeit, Gelöschte Objekte in ihrer Gesamtheit wiederherzustellen, während AD DS ausgeführt wird.

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server2008 R2-Domäne funktionale Ebene Features

* Alle Active Directory-Standardfeatures, alle Features der Domänenfunktionsebene Windows Server2008 sowie die folgenden Features:
    * Authentifizierungsmechanismussicherung, die Informationen über den Typ der Anmeldemethode (Smartcard oder Benutzername/Kennwort) gepackt, die zum Authentifizieren von Domänenbenutzern in Kerberos-Token des Benutzers verwendet wird. Wenn dieses Feature in einer Netzwerkumgebung aktiviert ist, die eine Infrastruktur zur verbundidentitätsverwaltung, z.B. Active Directory-Verbunddienste (AD FS), bereitgestellt hat kann die Informationen im Token extrahiert werden, wenn ein Benutzer versucht, eine Ansprüche unterstützende Anwendung zuzugreifen, die entwickelt wurde, um die Autorisierung auf der Basis der Anmeldemethode eines Benutzers zu bestimmen.
    * Automatische Dienstprinzipalnamen-Verwaltung für Dienste, die auf einem bestimmten Computer im Kontext eines verwalteten Dienstkontos ausgeführt werden, wenn der Name oder die DNS-Namen des Computers Konto ändert sich hosten. Weitere Informationen über verwaltete Dienstkonten finden Sie unter [Dienstkonten Step-by-Step Handbuch](https://go.microsoft.com/fwlink/?LinkId=180401).

## <a name="windows-server-2008"></a>Windows Server 2008

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2016
* Windows Server2012 R2
* Windows Server 2012
* Windows Server2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Level-Funktionen von Windows Server2008-Gesamtstruktur

* Alle Features, die auf der Gesamtstrukturfunktionsebene Windows Server2003 verfügbar sind, jedoch keine zusätzlichen Features stehen zur Verfügung. 

### <a name="windows-server-2008-domain-functional-level-features"></a>Level-Funktionen von Windows Server2008-Domäne

* Alle der Standard-AD DS, alle Features der Windows Server2003-Domänenfunktionsebene, sondern auch die folgenden Features stehen zur Verfügung:
    * Unterstützung der Distributed File System (DFS) für Windows Server2003 System Volume (SYSVOL)
        * DFS-unterstützt Replikation stabilere und genauer abgestimmte Replikation von SYSVOL-Inhalte.
        [!NOTE]>
        >Ab Windows Server2012 R2, ist (File Replication Service, FRS) veraltet. Eine neue Domäne, die auf einem Domänencontroller erstellt wird, die mindestens muss Windows Server2012 R2 auf die Domänenfunktionsebene Windows Server2008 oder höher festgelegt werden.

    * Domänenbasierte DFS-Namespaces, der unter Windows Server2008-Modus, die zugriffsbasierte Aufzählung und eine bessere Skalierbarkeit unterstützt. Domänenbasierte Namespaces in Windows Server2008-Modus ist auch die Gesamtstruktur, verwenden Sie die Windows Server2003-Gesamtstrukturfunktionsebene erforderlich. Weitere Informationen finden Sie unter [wählen Sie einen Namespace](https://go.microsoft.com/fwlink/?LinkId=180400).
    * Advanced Encryption Standard (AES 128 und AES-256) Unterstützung für das Kerberos-Protokoll. Für TGTs mithilfe von AES ausgestellt werden die Domänenfunktionsebene muss Windows Server 2008 oder höher und das Kennwort geändert werden muss. 
        * Weitere Informationen finden Sie unter [Kerberos-Erweiterungen](https://technet.microsoft.com/library/cc749438(ws.10).aspx).
        [!NOTE]>
        >Authentifizierungsfehler können auf einem Domänencontroller auftreten, nachdem die Domänenfunktionsebene auf Windows Server2008 oder höher ausgelöst wird, wenn der Domänencontroller hat bereits die Domänenfunktionsebene Änderung repliziert, aber das Krbtgt-Kennwort noch nicht aktualisiert wurde. In diesem Fall wird ein Neustart des KDC-Dienst auf dem Domänencontroller eine Aktualisierung im Speicher des neuen Krbtgt-Kennworts auslösen und verwandte Authentifizierungsfehler zu beheben.

    * [Letzte interaktive Anmeldung](https://go.microsoft.com/fwlink/?LinkId=180387) Informationen die folgenden Informationen angezeigt:
        * Die Gesamtanzahl der fehlgeschlagenen Anmeldeversuche auf einem Server für die Domäne Windows Server2008 oder Windows Vista-Arbeitsstation
        * Die Gesamtanzahl der fehlgeschlagenen Anmeldeversuche nach einer erfolgreichen Anmeldung auf einem Windows Server2008-Server oder einer Windows Vista-Arbeitsstation
        * Zeitpunkt des letzten fehlgeschlagenen Anmeldeversuchs auf einem Windows Server2008 oder Windows Vista-Arbeitsstation
        * Versuchen Sie die Uhrzeit der letzten erfolgreichen Anmeldung auf einem Windows Server2008-Server oder einer Windows Vista-Arbeitsstation
    * Fein abgestimmte Kennwortrichtlinien können Sie Kennwort- und Kontosperrungsrichtlinien für Benutzer und globale Sicherheitsgruppen in einer Domäne angeben. Weitere Informationen finden Sie unter [schrittweisen Anleitung für differenzierte Konfiguration Kennwort- und Kontosperrungsrichtlinien Richtlinie](https://go.microsoft.com/fwlink/?LinkID=91477).
    * Persönliche virtuelle Desktops
        * Um die zusätzliche Funktionalität von der Registerkarte "persönlicher virtueller Desktop" im Dialogfeld Eigenschaften von Benutzerkonten in Active Directory-Benutzer und -Computer zu verwenden, muss das AD DS-Schema erweitert werden für Windows Server2008 R2 (Objekt-Schemaversion = 47). Weitere Informationen finden Sie unter [bereitstellen persönlicher virtueller Desktops mithilfe der RemoteApp- und Desktopverbindung Step-by-Step Handbuch](https://go.microsoft.com/fwlink/?LinkId=183552).

## <a name="windows-server-2003"></a>Windows Server 2003

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server2012 R2
* Windows Server 2012
* Windows Server2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Level-Funktionen von Windows Server2003-Gesamtstruktur

* Alle AD DS-Standardfeatures und die folgenden Features sind verfügbar:
    * Gesamtstruktur-Vertrauensstellung
    * Umbenennen von Domänen
    * Verknüpfte Wertreplikation
        - Verknüpfte Wertreplikation ermöglicht es für Sie zum Ändern der Gruppenmitgliedschaft zum Speichern und replizieren Werte für einzelne Mitglieder, anstelle der Replikation der gesamten Mitgliedschaft als eine Einheit. Speichern und Replizieren der Werte der einzelnen Elemente verwendet weniger Netzwerkbandbreite und weniger Prozessorzyklen während der Replikation und verhindert, dass Sie Updates verloren gehen, wenn Sie hinzufügen oder entfernen mehrere Elemente gleichzeitig auf verschiedenen Domänencontrollern.
    * Die Möglichkeit, einen schreibgeschützten Domänencontroller (RODC) bereitzustellen.
    * Verbesserte (Knowledge Consistency Checker, KCC) Algorithmen und Skalierbarkeit
        - Der Generator für standortübergreifende Topologie (ISTG) verwendet verbesserte Algorithmen, die skalieren, um Gesamtstrukturen mit einer größeren Anzahl von Standorten zu unterstützen, als AD DS auf der Gesamtstrukturfunktionsebene Windows2000 unterstützt werden. Der verbesserte ISTG-Wahlalgorithmus ist ein weniger Intrusiver Mechanismus zur Auswahl des ISTG auf der Gesamtstrukturfunktionsebene Windows2000.
    * Die Möglichkeit zum Erstellen von Instanzen der dynamischen Erweiterungsklasse mit dem Namen **DynamicObject** in einer Domänenverzeichnispartition
    * Die Möglichkeit zum Konvertieren einer **InetOrgPerson** Objektinstanz in einer **Benutzer** Objektinstanz, und führen Sie die Konvertierung in die entgegengesetzte Richtung
    * Die Fähigkeit zum Erstellen von Instanzen der neuen Gruppentypen rollenbasierte Autorisierung zu unterstützen. 
        - Um anwendungsbasierte Gruppen und LDAP-Abfragegruppen Sie werden bezeichnet.
    * Deaktivierung und Neudefinition von Attributen und Klassen im Schema. Die folgenden Attribute wiederverwendet werden können: LdapDisplayName SchemaIdGuid, OID und MapiID.
    * Domänenbasierte DFS-Namespaces, der unter Windows Server2008-Modus, die zugriffsbasierte Aufzählung und eine bessere Skalierbarkeit unterstützt. Weitere Informationen finden Sie unter [wählen Sie einen Namespace](https://go.microsoft.com/fwlink/?LinkId=180400).

### <a name="windows-server-2003-domain-functional-level-features"></a>Level-Funktionen von Windows Server2003-Domäne

* Alle der AD DS-Standardfeatures, alle Features, die auf der Windows2000-Funktionsebene der Domäne im einheitlichen Modus verfügbar sind und die folgenden Features sind verfügbar:
    * Das Verwaltungstool Domäne Netdom.exe, wodurch es möglich, dass Sie Domänencontroller umbenennen
    * Anmeldung Zeitstempel aktualisiert
        * Die **LastLogonTimestamp** Attribut mit der Uhrzeit der letzten Anmeldung des Benutzers oder des Computers aktualisiert wird. Dieses Attribut wird innerhalb der Domäne repliziert.
    * Möglichkeit zum Festlegen der **UserPassword** -Attributs als effektives Kennwort auf **InetOrgPerson** und für Benutzerobjekte
    * Die Möglichkeit zum Umleiten von Benutzer- und Container
        * Standardmäßig werden zwei bekannte Container bereitgestellt, für Computer- und Benutzerkonten, Gehäuse und zwar, Cn = Computers,<domain root> "und" Cn = Users,<domain root>. Dieses Feature ermöglicht die Definition der für diese Konten ein neuer, bekannter Speicherort.
    * Die Möglichkeit zum Autorisierungs-Manager zum Speichern seiner Autorisierungsrichtlinien in AD DS
    * Die eingeschränkte Delegierung
        * Die eingeschränkte Delegierung ermöglicht es Anwendungen die sichere Delegierung von Anmeldeinformationen des Benutzers über Kerberos-Authentifizierung nutzen.
        * Sie können die Delegierung für bestimmte Zieldienste nur beschränken.
    * Die ausgewählte Authentifizierung
        * Die ausgewählte Authentifizierung ermöglicht es möglich, dass Sie die Benutzer und Gruppen einer vertrauenswürdigen Gesamtstruktur, die für Ressourcenserver in einer vertrauenden Gesamtstruktur authentifizieren dürfen.

## <a name="windows-2000"></a>Windows2000

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows2000 einheitlichen Gesamtstruktur funktionale-Level-Funktionen

* Alle standardmäßigen AD DS-Features stehen zur Verfügung.

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows2000-Domäne im einheitlichen Modus funktionale Ebene Features

* Alle AD DS-Standardfeatures und die folgenden Directory-Features sind verfügbar, einschließlich:
    * Universelle Gruppen für die Verteilung und Sicherheitsgruppen.
    * Verschachteln von Gruppen
    * Konvertierung, die Konvertierung zwischen Sicherheits- und Verteilergruppen ermöglicht
    * Sicherheit der SID-Verlauf

## <a name="next-steps"></a>Nächste Schritte

* [Heraufstufen der Domänenfunktionsebene](https://technet.microsoft.com/library/cc753104.aspx)  
* [Heraufstufen der Gesamtstrukturfunktionsebene](https://technet.microsoft.com/library/cc730985.aspx)
