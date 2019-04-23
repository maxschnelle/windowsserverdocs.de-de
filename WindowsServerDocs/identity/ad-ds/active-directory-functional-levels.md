---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: Windows Server 2016-Funktionsebenen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: ea56c718394d145a36145d32e5769661a62efd56
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841001"
---
# <a name="forest-and-domain-functional-levels"></a>Funktionsebenen Gesamtstruktur und Domäne

>Gilt für: Windows Server

Die funktionale Ebenen der bestimmen Sie der verfügbaren Funktionen von Active Directory Domain Services (AD DS) Domäne oder Gesamtstruktur. Sie legen außerdem die Windows-Serverbetriebssysteme, die Sie auf Domänencontrollern in der Domäne oder Gesamtstruktur ausführen können. Die funktionale Ebenen der beeinflussen jedoch nicht, welche Betriebssysteme auf Arbeitsstationen ausführen und Mitgliedsservern, die der Domäne oder Gesamtstruktur angehören.

Wenn Sie AD DS bereitstellen, legen Sie die Domänen- und Gesamtstruktur-Funktionsebenen bis zum höchsten Wert, den Ihrer Umgebung unterstützen kann. Auf diese Weise können Sie beliebig viele AD DS-Features wie möglich verwenden. Wenn Sie eine neue Gesamtstruktur bereitstellen, werden Sie aufgefordert, um die Gesamtstrukturfunktionsebene auf festgelegt, und legen Sie dann auf die Domänenfunktionsebene auf. Sie können die Domänenfunktionsebene auf einen Wert, der höher als die Funktionsebene der Gesamtstruktur festlegen, aber Sie können nicht die Domänenfunktionsebene auf ein Wert, der niedriger ist als die Gesamtstrukturfunktionsebene auf festgelegt.

Mit dem Ende der Lebensdauer von Windows 2003, Windows 2003-Domänencontrollern (DCs) auf WindowsServer 2008, 2008 R2, 2012, aktualisiert werden müssen 2012 R2, 2016 oder 2019. Daher sollten alle Domänencontroller mit Windows Server 2003 aus der Domäne entfernt werden.

Auf dem Windows Server 2008 und höher Domänenfunktionsebenen werden Replikation des verteilten Dienst (Distributed File System, DFS) Ordnerinhalt SYSVOL zwischen Domänencontrollern zu replizieren. Wenn Sie eine neue Domäne auf der Domänenfunktionsebene Windows Server 2008 oder höher erstellen, wird die DFS-Replikation zum Replizieren von SYSVOL automatisch verwendet. Wenn Sie auf einer niedrigeren Funktionsebene die Domäne erstellt haben, müssen Sie von der Verwendung von FRS zur DFS-Replikation für SYSVOL migriert. Für Migrationsschritte, können Sie entweder führen Sie die [Prozeduren auf TechNet](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) oder sehen Sie sich die [optimierte Reihe von Schritten im Storage Team File Cabinet Blog](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx).

## <a name="windows-server-2019"></a>Windows Server 2019

Es gibt keine neue Gesamtstruktur oder die Funktionsebenen in dieser Version hinzugefügt.

Die Mindestanforderungen für das Hinzufügen eines Domänencontrollers von Windows Server 2019 ist eine Windows Server 2008 R2-Funktionsebene.

## <a name="windows-server-2016"></a>Windows Server 2016

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2019
* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Windows Server 2016-Gesamtstruktur funktionale Level-Funktionen

* Die Funktionen, die auf die Windows Server 2012 R2-Gesamtstrukturfunktionsebene verfügbar sind und die folgenden Features sind verfügbar:
   * [Privilegierte zugriffsverwaltung (PAM) mithilfe von Microsoft Identity Manager (MIM)](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Windows Server 2016 funktionale Funktionen der Domänenebene

* Alle Active Directory-Standardfeatures, alle Features der Windows Server 2012 R2-Domänenfunktionsebene sowie die folgenden Funktionen:
   * DCs unterstützen die automatische parallele des NTLM und andere Geheimnisse kennwortbasierte für ein Benutzerkonto so konfiguriert, dass die PKI-Authentifizierung erforderlich ist. Diese Konfiguration ist auch bekannt als "Smart Card für die interaktive Anmeldung"
   * Wenn ein Benutzer beschränkt, die Domäne eingebundenen Geräten ist, können DCs ermöglichen Netzwerk NTLM unterstützen.
   * Kerberos-Clients, die mit der Erweiterung der PKInit Aktualität erfolgreich authentifizieren, erhalten die neue öffentliche Schlüssel Identität SID.

    Weitere Informationen finden Sie unter [Neuigkeiten in Kerberos-Authentifizierung](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication) und [Neues in den Schutz von Anmeldeinformationen](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Windows Server 2012 R2-Gesamtstruktur funktionale Funktionen auf Websiteebene

* Alle Funktionen, die unter Windows Server 2012-Gesamtstruktur funktionale Ebene, jedoch keine zusätzlichen Features.

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Windows Server 2012 R2 Domäne funktionale Funktionen auf Websiteebene

* Alle Active Directory-Standardfeatures, alle Features der Domänenfunktionsebene Windows Server 2012 sowie die folgenden Funktionen:
   * DC-Side von Schutzfunktionen für geschützte Benutzer. Authentifizierung von Benutzern auf einem Windows Server 2012 R2 können Domäne nicht mehr geschützt ist:
      * Authentifizieren mit NTLM-Authentifizierung
      * Verwenden von des- oder RC4-Verschlüsselungssammlungen in Kerberos-vorabauthentifizierung
      * Mit uneingeschränkter oder eingeschränkter Delegierung delegiert werden
      * Erneuern von Benutzertickets (TGTs) nach Ablauf der Lebensdauer der ersten 4 Stunden
   * Authentifizierungsrichtlinien
      * Neue Gesamtstruktur-basierten Active Directory-Richtlinien die Konten in Windows Server 2012 R2-Domänen zu steuern, welche Hosts angewendet werden können ein Konto kann aus anmelden und Anwenden von Bedingungen für die Zugriffssteuerung für die Authentifizierung an Dienste, die mit einem Konto ausgeführt.
   * Authentifizierungsrichtliniensilos
      * Neue Gesamtstruktur-basierten Active Directory-Objekt, die eine Beziehung zwischen Benutzer, verwalteter Dienst und Computer, Konten, zum Klassifizieren von Konten für Authentifizierungsrichtlinien oder für die Authentifizierung Isolation verwendet werden soll, erstellen können.

## <a name="windows-server-2012"></a>Windows Server 2012

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Windows Server 2012-Gesamtstruktur funktionale Level-Funktionen

* Alle Funktionen, die unter Windows Server 2008 R2-Gesamtstruktur funktionale Ebene, jedoch keine zusätzlichen Features.

### <a name="windows-server-2012-domain-functional-level-features"></a>Windows Server 2012-Domäne funktionale Level-Funktionen

* Alle Active Directory-Standardfeatures, alle Features der Windows Server 2008 R2-Domänenfunktionsebene sowie die folgenden Funktionen:
   * Der KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring KDC-verwaltungsvorlagenrichtlinie verfügt über zwei Einstellungen (immer Ansprüche bereitstellen und Fehler bei authentifizierungsanforderungen ohne Armor), für die Domänenfunktionsebene auf Windows Server 2012 erforderlich. Weitere Informationen finden Sie unter [Neuigkeiten in Kerberos-Authentifizierung](https://technet.microsoft.com/library/hh831747.aspx)

## <a name="windows-server-2008r2"></a>Windows Server 2008R2

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server 2008 R2-Gesamtstruktur funktionale Funktionen auf Websiteebene

* Alle Features, die auf der Gesamtstrukturfunktionsebene Windows Server 2003 verfügbar sind, plus die folgenden Features:
   * Active Directory-Papierkorb, der die Möglichkeit bietet, gelöschte Objekte in ihrer Gesamtheit wiederherzustellen, während die Active Directory-Domänendienste ausgeführt werden.

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server 2008 R2 Domäne funktionale Funktionen auf Websiteebene

* Alle Active Directory-Standardfeatures, alle Features der Domänenfunktionsebene Windows Server 2008 sowie die folgenden Funktionen:
   * Authentifizierungsmechanismussicherung, bei der Informationen zum Typ der Anmeldemethode (Smartcard oder Benutzername/Kennwort), die zum Authentifizieren von Domänenbenutzern dient, in das Kerberos-Token der einzelnen Benutzer eingefügt werden. Wenn diese Funktion in einer Netzwerkumgebung aktiviert ist, die eine Infrastruktur zur verbundidentitätsverwaltung, z. B. Active Directory-Verbunddienste (AD FS) bereitgestellt wurde kann die Informationen im Token extrahiert werden, wenn ein Benutzer versucht, für den Zugriff auf Ansprüche unterstützende Anwendung, die zum Bestimmen der Autorisierung basierend auf der Anmeldemethode des Benutzers entwickelt wurde.
   * Automatische Dienstprinzipalnamen-Verwaltung für Dienste, die auf einem bestimmten Computer im Kontext eines verwalteten Dienstkontos ausgeführt wird, wenn der Name oder DNS-Namen des dem-Konto Änderungen an einem Computer gehostet. Weitere Informationen zu verwalteten Dienstkonten finden Sie unter [schrittweisen Anleitung zu Dienstkonten](https://go.microsoft.com/fwlink/?LinkId=180401).

## <a name="windows-server-2008"></a>WindowsServer 2008

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Windows Server 2008-Gesamtstruktur funktionale Level-Funktionen

* Alle Funktionen, die auf der Gesamtstrukturfunktionsebene von Windows Server 2003 verfügbar sind, jedoch keine zusätzlichen Features zur Verfügung stehen. 

### <a name="windows-server-2008-domain-functional-level-features"></a>Windows Server 2008 funktionale Funktionen der Domänenebene

* Alle der standardmäßigen AD DS-features, alle Features der Windows Server 2003-Domänenfunktionsebene und die folgenden Funktionen sind verfügbar:
   * Replikationsunterstützung für Distributed File System (DFS) für Windows Server 2003 das Systemvolume (SYSVOL)
      * Unterstützung der DFS-Replikation bietet eine stabilere und genauer abgestimmte Replikation von SYSVOL-Inhalten.
        [!NOTE]>
        >Ab Windows Server 2012 R2, ist (File Replication Service, FRS) veraltet. Eine neue Domäne, die auf einem Domänencontroller erstellt wird, die mindestens muss Windows Server 2012 R2 auf die Domänenfunktionsebene Windows Server 2008 oder höher festgelegt werden.

   * Domänenbasierte DFS-Namespaces, der unter Windows Server 2008-Modus, einschließlich Unterstützung für zugriffsbasierte Aufzählung und erhöhte Skalierbarkeit. Domänenbasierte Namespaces in Windows Server 2008-Modus muss auch die Gesamtstruktur die Funktionsebene der Windows Server 2003-Gesamtstruktur verwenden. Weitere Informationen finden Sie unter [wählen Sie einen Namespace-Typ](https://go.microsoft.com/fwlink/?LinkId=180400).
   * Advanced Encryption Standard (AES-128 und AES-256) Unterstützung für das Kerberos-Protokoll. Klicken Sie in der Reihenfolge für TGTs ausgestellt werden mithilfe von AES die Domänenfunktionsebene muss WindowsServer 2008 oder höher sein, und das Kennwort muss geändert werden. 
      * Weitere Informationen finden Sie unter [Kerberos-Erweiterungen](https://technet.microsoft.com/library/cc749438(ws.10).aspx).
        [!NOTE]>
        >Authentifizierungsfehler können auf einem Domänencontroller auftreten, nachdem die Domänenfunktionsebene auf Windows Server 2008 oder höher ausgelöst wird, wenn der Domänencontroller wurde bereits die Domänenfunktionsebene Änderung repliziert, aber das Krbtgt-Kennwort wurde noch nicht aktualisiert. In diesem Fall wird ein Neustart des KDC-Diensts auf dem Domänencontroller eine in-Memory-Aktualisierung, der das neue Kennwort des Krbtgt auslösen und zugehörige Authentifizierungs-Fehler zu beheben.

   * [Letzte interaktive Anmeldung](https://go.microsoft.com/fwlink/?LinkId=180387) Informationen die folgenden Informationen angezeigt:
      * Die Gesamtanzahl der fehlgeschlagenen Anmeldeversuche auf einem Server für die Domäne eingebundenen Windows Server 2008 oder einer Windows Vista-Arbeitsstation
      * Die Gesamtanzahl fehlgeschlagener Anmeldeversuche nach einer erfolgreichen Anmeldung auf einem Windows Server 2008-Server oder einer Windows Vista-Arbeitsstation
      * Zeitpunkt des letzten fehlgeschlagenen Anmeldeversuchs auf einem Windows Server 2008 oder einer Windows Vista-Arbeitsstation
      * Zeitpunkt der letzten erfolgreichen Anmeldung versucht, auf einem Windows Server 2008-Server oder einer Windows Vista-Arbeitsstation
   * Fein abgestimmte Kennwortrichtlinien ermöglichen es Ihnen die Angabe von Kennwort- und Kontosperrungsrichtlinien für Benutzer und globale Sicherheitsgruppen in einer Domäne. Weitere Informationen finden Sie unter [schrittweisen Anleitung für die Konfiguration abgestimmter Kennwort- und Account Lockout Richtlinienkonfiguration](https://go.microsoft.com/fwlink/?LinkID=91477).
   * Persönliche virtuelle Desktops
      * Um die neue Funktion von der persönlichen virtuellen Desktop-Registerkarte im Dialogfeld Eigenschaften von Benutzerkonten in Active Directory-Benutzer und-Computer zu verwenden, muss das AD DS-Schema erweitert werden für Windows Server 2008 R2 (Objekt-Schemaversion = 47). Weitere Informationen finden Sie unter [bereitstellen persönlicher virtueller Desktops mithilfe der RemoteApp-und Desktop schrittweisen Anleitung zum](https://go.microsoft.com/fwlink/?LinkId=183552).

## <a name="windows-server-2003"></a>Windows Server 2003

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Windows Server 2003-Gesamtstruktur funktionale Level-Funktionen

* Die AD DS-Standardfeatures und die folgenden Features sind verfügbar:
   * Gesamtstruktur-Vertrauensstellung
   * Domänenumbenennung
   * Verknüpfte Wertreplikation
      - Verknüpfte Wertreplikation ermöglicht es Ihnen, Gruppenmitgliedschaft, die zum Speichern und replizieren Werte für einzelne Mitglieder, anstelle der Replikation der gesamten Mitgliedschaft als eine Einheit zu ändern. Speichern und replizieren die Werte der einzelnen Elemente verwendet weniger Netzwerkbandbreite und weniger Prozessorzyklen während der Replikation und verhindert, dass Sie vom Verlust von Updates beim Hinzufügen oder entfernen mehrere Elemente gleichzeitig auf verschiedenen Domänencontrollern.
   * Die Möglichkeit, einen schreibgeschützten Domänencontroller (RODC) bereitzustellen.
   * Verbesserte (Knowledge Consistency Checker, KCC) Algorithmen und Skalierbarkeit
      - Der Generator für standortübergreifende Topologie (ISTG) verwendet verbesserte Algorithmen, die skalieren, um Gesamtstrukturen mit einer größeren Anzahl von Standorten zu unterstützen, als AD DS auf der Gesamtstrukturfunktionsebene Windows 2000 unterstützt werden. Der verbesserte ISTG-Wahlalgorithmus ist ein weniger aufdringlichen Mechanismus zur Auswahl des ISTG auf der Windows 2000-Funktionsebene der Gesamtstruktur.
   * Die Fähigkeit zum Erstellen von Instanzen der dynamischen Erweiterungsklasse mit dem Namen **DynamicObject** in einer Domänenverzeichnispartition
   * Die Möglichkeit zum Konvertieren einer **InetOrgPerson** Objektinstanz in einen **Benutzer** -Objektinstanz herstellen, und für die Konvertierung in die entgegengesetzte Richtung
   * Die Fähigkeit zum Erstellen von Instanzen der neuen Gruppentypen um rollenbasierte Autorisierung zu unterstützen. 
      - Diese Typen werden anwendungsbasierte Gruppen und LDAP-Abfragegruppen bezeichnet.
   * Deaktivierung und Neudefinition von Attributen und Klassen im Schema Die folgenden Attribute wiederverwendet werden können: "ldapDisplayName", "schemaIDGUID", "OID und MapiID.
   * Domänenbasierte DFS-Namespaces, der unter Windows Server 2008-Modus, einschließlich Unterstützung für zugriffsbasierte Aufzählung und erhöhte Skalierbarkeit. Weitere Informationen finden Sie unter [wählen Sie einen Namespace-Typ](https://go.microsoft.com/fwlink/?LinkId=180400).

### <a name="windows-server-2003-domain-functional-level-features"></a>Windows Server 2003-Domäne funktionale Level-Funktionen

* Alle der AD DS-Standardfeatures, alle Features, die auf der Windows 2000-Funktionsebene der Domäne im einheitlichen Modus verfügbar sind und die folgenden Funktionen sind verfügbar:
   * Das Domain-Verwaltungstool Netdom.exe, wodurch es möglich, dass Sie Domänencontroller umbenennen
   * Zeitstempel für die Anmeldung aktualisiert
      * Das **lastLogonTimestamp**-Attribut wird mit dem Zeitpunkt der letzten Anmeldung des Benutzers oder des Computers aktualisiert. Dieses Attribut wird innerhalb der Domäne repliziert.
   * Die Fähigkeit zum Festlegen der **UserPassword** -Attributs als effektives Kennwort für **InetOrgPerson** und Benutzerobjekte
   * Die Möglichkeit zum Umleiten von Benutzer- und Container
      * Standardmäßig werden zwei bekannte Container bereitgestellt, für Computer und Benutzer, d. h., Cn = Computers,<domain root> "und" Cn = Users,<domain root>. Dieses Feature ermöglicht die Definition für diese Konten ein neuer, bekannter Speicherort.
   * Die Fähigkeit zum Autorisierungs-Manager zum Speichern seiner Autorisierungsrichtlinien in AD DS
   * Eingeschränkte Delegierung
      * Eingeschränkter Delegierung ermöglicht es Anwendungen, die sichere Delegierung von Benutzeranmeldeinformationen mittels Kerberos-Authentifizierung nutzen.
      * Sie können die Delegierung für bestimmte Zieldienste nur einschränken.
   * Selektive Authentifizierung
      * Selektive Authentifizierung ermöglicht es möglich, dass Sie angeben, die Benutzer und Gruppen einer vertrauenswürdigen Gesamtstruktur, die für Ressourcenserver in einer vertrauenden Gesamtstruktur authentifizieren dürfen.

## <a name="windows-2000"></a>Windows 2000

Unterstützte Domänencontroller-Betriebssystems:

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows 2000 native Gesamtstruktur funktionale Level-Funktionen

* Alle von den standardmäßig AD DS-Funktionen sind verfügbar.

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows 2000-Domäne im einheitlichen Modus funktionale Ebene features

* Alle AD DS-Standardfeatures und die folgenden Directory-Funktionen sind verfügbar, einschließlich:
   * Universelle Gruppen sowohl Verteiler- und Sicherheitsgruppen.
   * Gruppenverschachtelung
   * Die gruppenkonvertierung, die Konvertierung zwischen Sicherheits-und Verteilergruppen ermöglicht.
   * SID-Verlaufs Sicherheitsbezeichner (SID)

## <a name="next-steps"></a>Nächste Schritte

* [Heraufstufen der Domänenfunktionsebene](https://technet.microsoft.com/library/cc753104.aspx)  
* [Heraufstufen der Gesamtstrukturfunktionsebene](https://technet.microsoft.com/library/cc730985.aspx)
