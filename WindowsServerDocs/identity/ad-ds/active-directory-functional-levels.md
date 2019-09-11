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
ms.openlocfilehash: c1e2108084b03fabbf7c6a18c2ecbcaf3cbd1dd9
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868257"
---
# <a name="forest-and-domain-functional-levels"></a>Gesamtstruktur-und Domänen Funktionsebene

>Gilt für: Windows Server

Funktionsebenen bestimmen die verfügbaren Domänen-oder Gesamtstruktur Funktionen Active Directory Domain Services (AD DS). Außerdem wird festgelegt, welche Windows Server-Betriebssysteme Sie auf Domänen Controllern in der Domäne oder der Gesamtstruktur ausführen können. Funktionsebenen wirken sich jedoch nicht auf die Betriebssysteme aus, die Sie auf Arbeitsstationen und Mitglieds Servern ausführen können, die mit der Domäne oder Gesamtstruktur verknüpft sind.

Wenn Sie AD DS bereitstellen, legen Sie die Domänen-und Gesamtstruktur Funktionsebenen auf den höchsten Wert fest, den die Umgebung unterstützen kann. Auf diese Weise können Sie so viele AD DS Funktionen wie möglich verwenden. Wenn Sie eine neue Gesamtstruktur bereitstellen, werden Sie aufgefordert, die Gesamtstruktur Funktionsebene festzulegen und die Domänen Funktionsebene dann festzulegen. Sie können die Domänen Funktionsebene auf einen Wert festlegen, der höher als die Gesamtstruktur Funktionsebene ist, aber Sie können die Domänen Funktionsebene nicht auf einen niedrigeren Wert als die Gesamtstruktur Funktionsebene festlegen.

Mit dem Ende der Lebensdauer von Windows 2003 müssen Windows 2003-Domänen Controller (DCS) auf Windows Server 2008, 2008R2, 2012, 2012r2, 2016 oder 2019 aktualisiert werden. Daher sollten alle Domänen Controller, auf denen Windows Server 2003 ausgeführt wird, aus der Domäne entfernt werden.

Auf den Domänen Funktionsebenen Windows Server 2008 und höher wird die DFS-Replikation (DFS) zum Replizieren von SYSVOL-Ordner Inhalten zwischen Domänen Controllern verwendet. Wenn Sie eine neue Domäne auf der Windows Server 2008-Domänen Funktionsebene oder höher erstellen, wird DFS-Replikation automatisch zum Replizieren von SYSVOL verwendet. Wenn Sie die Domäne auf einer niedrigeren Funktionsebene erstellt haben, müssen Sie von der Verwendung von FRS zur DFS-Replikation für SYSVOL migrieren. Für Migrations Schritte können Sie entweder die [Verfahren auf TechNet](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) ausführen oder die [optimierten Schritte im CAB-Blog der Speicher Team Datei](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)lesen.

## <a name="windows-server-2019"></a>Windows Server 2019

In dieser Version wurden keine neuen Gesamtstruktur-oder Domänen Funktionsebenen hinzugefügt.

Die Mindestanforderung zum Hinzufügen eines Windows Server 2019-Domänen Controllers ist eine Windows Server 2008-Funktionsebene. Die Domäne muss auch DFS-R als Engine zum Replizieren von SYSVOL verwenden.

## <a name="windows-server-2016"></a>Windows Server 2016

Unterstütztes Betriebs System des Domänen Controllers:

* Windows Server 2019
* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Features der Windows Server 2016-Gesamtstruktur Funktionsebene

* Alle Features, die auf der Gesamtstruktur Funktionsebene Windows Server 2012r2 verfügbar sind, und die folgenden Features sind verfügbar:
   * [Privilegierte Zugriffs Verwaltung (PAM) mithilfe von Microsoft Identity Manager (MIM)](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Features der Windows Server 2016-Domänen Funktionsebene

* Alle Standard Active Directory Features, alle Features der Domänen Funktionsebene Windows Server 2012r2 sowie die folgenden Features:
   * DCS können das automatische Rollback von NTLM und anderen Kenn Wort basierten Geheimnissen für ein Benutzerkonto unterstützen, das für die PKI-Authentifizierung konfiguriert ist. Diese Konfiguration wird auch als "Smartcard für interaktive Anmeldung erforderlich" bezeichnet.
   * DCS können das Zulassen von Netzwerk-NTLM unterstützen, wenn ein Benutzer auf bestimmte in die Domäne eingebundenen Geräte beschränkt ist.
   * Kerberos-Clients, die sich erfolgreich bei der PKINIT-Erweiterung authentifizieren, erhalten die aktuelle SID der öffentlichen Schlüssel Identität.

    Weitere Informationen finden Sie [unter Neues bei der Kerberos-Authentifizierung](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication) und [Neuerungen beim Schutz von](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection) Anmelde Informationen

## <a name="windows-server-2012r2"></a>Windows Server 2012r2

Unterstütztes Betriebs System des Domänen Controllers:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Features der Windows Server 2012r2-Gesamtstruktur Funktionsebene

* Alle Features, die auf der Gesamtstruktur Funktionsebene von Windows Server 2012 verfügbar sind, jedoch keine zusätzlichen Features.

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Features der Windows Server 2012r2-Domänen Funktionsebene

* Alle Standard Active Directory Features, alle Features der Windows Server 2012-Domänen Funktionsebene sowie die folgenden Features:
   * Domänen Controller seitiger Schutz für geschützte Benutzer. Geschützte Benutzer, die sich bei einer Windows Server 2012 R2-Domäne authentifizieren, können nicht mehr:
      * Authentifizieren mit NTLM-Authentifizierung
      * Verwenden von des-oder RC4-Verschlüsselungs Sammlungen in der Kerberos-Vorauthentifizierung
      * Delegiert mit eingeschränkter oder eingeschränkter Delegierung
      * Verlängern von Benutzer Tickets (TGTs) über die anfängliche Dauer von 4 Stunden hinaus
   * Authentifizierungsrichtlinien
      * Neue Gesamtstruktur basierte Active Directory Richtlinien, die auf Konten in Windows Server 2012 R2-Domänen angewendet werden können, um zu steuern, auf welchen Hosts ein Konto sich anmelden kann, und wenden Zugriffs Steuerungs Bedingungen zur Authentifizierung auf Dienste an, die als Konto ausgeführt werden.
   * Authentifizierungsrichtliniensilos
      * Neues Gesamtstruktur basiertes Active Directory Objekt, mit dem eine Beziehung zwischen Benutzer, verwaltetem Dienst und Computer erstellt werden kann, die zum Klassifizieren von Konten für Authentifizierungs Richtlinien oder zur Authentifizierungs Isolation verwendet werden kann.

## <a name="windows-server-2012"></a>Windows Server 2012

Unterstütztes Betriebs System des Domänen Controllers:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Features der Windows Server 2012-Gesamtstruktur Funktionsebene

* Alle Features, die auf der Funktionsebene der Windows Server 2008 R2-Gesamtstruktur verfügbar sind, jedoch keine zusätzlichen Features.

### <a name="windows-server-2012-domain-functional-level-features"></a>Features der Windows Server 2012-Domänen Funktionsebene

* Alle Standard Active Directory Features, alle Features der Windows Server 2008R2-Domänen Funktionsebene sowie die folgenden Features:
   * Die KDC-Unterstützung für Ansprüche, Verbund Authentifizierung und Kerberos armoring KDC administrative Template-Richtlinie verfügt über zwei Einstellungen (immer Ansprüche bereitstellen und nicht hochgerüstete Authentifizierungsanforderungen fehlschlagen), für die die Windows Server 2012-Domänen Funktionsebene erforderlich ist. Weitere Informationen finden Sie unter [Neues bei der Kerberos-Authentifizierung](https://technet.microsoft.com/library/hh831747.aspx) .

## <a name="windows-server-2008r2"></a>Windows Server 2008R2

Unterstütztes Betriebs System des Domänen Controllers:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Features der Windows Server 2008R2-Gesamtstruktur Funktionsebene

* Alle Features, die auf der Gesamtstrukturfunktionsebene Windows Server 2003 verfügbar sind, plus die folgenden Features:
   * Active Directory-Papierkorb, der die Möglichkeit bietet, gelöschte Objekte in ihrer Gesamtheit wiederherzustellen, während die Active Directory-Domänendienste ausgeführt werden.

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Features der Windows Server 2008R2-Domänen Funktionsebene

* Alle Standard Active Directory Features, alle Features der Windows Server 2008-Domänen Funktionsebene sowie die folgenden Features:
   * Authentifizierung von Authentifizierungsmechanismen, mit der Informationen über den Typ der Anmelde Methode (Smartcard-oder Benutzername/Kennwort) verpackt werden, der zum Authentifizieren von Domänen Benutzern im Kerberos-Token jedes Benutzers verwendet wird. Wenn dieses Feature in einer Netzwerkumgebung aktiviert ist, in der eine Verbund-Identitäts Verwaltungsinfrastruktur (z. b. Active Directory-Verbunddienste (AD FS) (AD FS) bereitgestellt wurde, können die Informationen im Token extrahiert werden, wenn ein Benutzer versucht, auf eine der Ansprüche unterstützende Anwendung, die entwickelt wurde, um die Autorisierung basierend auf der Anmelde Methode eines Benutzers zu bestimmen.
   * Automatische SPN-Verwaltung für Dienste, die auf einem bestimmten Computer im Kontext eines verwalteten Dienst Kontos ausgeführt werden, wenn sich der Name oder der DNS-Hostname des Computer Kontos ändert. Weitere Informationen zu verwalteten Dienst Konten finden Sie unter [schrittweise Anleitung für Dienst Konten](https://go.microsoft.com/fwlink/?LinkId=180401).

## <a name="windows-server-2008"></a>Windows Server 2008

Unterstütztes Betriebs System des Domänen Controllers:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Features der Windows Server 2008-Gesamtstruktur Funktionsebene

* Alle Features, die auf der Gesamtstruktur Funktionsebene von Windows Server 2003 verfügbar sind, aber keine zusätzlichen Features sind verfügbar. 

### <a name="windows-server-2008-domain-functional-level-features"></a>Features der Windows Server 2008-Domänen Funktionsebene

* Alle Standard Features von AD DS, alle Features der Domänen Funktionsebene Windows Server 2003 und die folgenden Features sind verfügbar:
  * Verteiltes Dateisystem (DFS)-Replikations Unterstützung für das Windows Server 2003-System Volume (SYSVOL)
    * Die Unterstützung der DFS-Replikation bietet eine robustere und detailliertere Replikation von SYSVOL-Inhalten

      > [!NOTE]
      > Ab Windows Server 2012 R2 ist der Datei Replikations Dienst (File Replication Service, FRS) veraltet. Eine neue Domäne, die auf einem Domänen Controller erstellt wird, auf dem mindestens Windows Server 2012 R2 ausgeführt wird, muss auf die Domänen Funktionsebene Windows Server 2008 oder höher festgelegt werden.

  * Domänen basierte DFS-Namespaces, die im Windows Server 2008-Modus ausgeführt werden, einschließlich der Unterstützung für die Zugriffs basierte Enumeration und eine größere Skalierbarkeit. Domänen basierte Namespaces im Windows Server 2008-Modus erfordern außerdem, dass die Gesamtstruktur die Gesamtstruktur Funktionsebene von Windows Server 2003 verwendet. Weitere Informationen finden Sie unter [Auswählen eines Namespace Typs](https://go.microsoft.com/fwlink/?LinkId=180400).
  * Advanced Encryption Standard (AES 128 und AES 256) Unterstützung für das Kerberos-Protokoll. Damit TGTs mithilfe von AES ausgestellt werden kann, muss die Domänen Funktionsebene Windows Server 2008 oder höher sein, und das Domänen Kennwort muss geändert werden. 
    * Weitere Informationen finden Sie unter [Kerberos-Erweiterungen](https://technet.microsoft.com/library/cc749438(ws.10).aspx).

      > [!NOTE]
      >Authentifizierungsfehler können auf einem Domänen Controller auftreten, wenn die Domänen Funktionsebene auf Windows Server 2008 oder höher erhöht wird, wenn der Domänen Controller die DFL-Änderung bereits repliziert hat, das krbtgt-Kennwort aber noch nicht aktualisiert hat. In diesem Fall löst ein Neustart des KDC-Dienstanbieter auf dem Domänen Controller eine Aktualisierung des neuen krbtgt-Kennworts im Arbeitsspeicher aus und löst zugehörige Authentifizierungsfehler aus.

  * [Letzte interaktive Anmeldung](https://go.microsoft.com/fwlink/?LinkId=180387) Informationen zeigt die folgenden Informationen an:
     * Die Gesamtzahl der fehlgeschlagenen Anmeldeversuche auf einem in die Domäne eingebundenen Windows Server 2008-Server oder auf einer Windows Vista-Arbeitsstation
     * Die Gesamtanzahl der fehlgeschlagenen Anmeldeversuche nach einer erfolgreichen Anmeldung bei einem Windows Server 2008-Server oder einer Windows Vista-Arbeitsstation
     * Zeitpunkt des letzten fehlgeschlagenen Anmelde Versuchs auf einem Windows Server 2008 oder einer Windows Vista-Arbeitsstation
     * Zeitpunkt des letzten erfolgreichen Anmelde Versuchs auf einem Windows Server 2008-Server oder einer Windows Vista-Arbeitsstation
  * Differenzierte Kenn Wort Richtlinien ermöglichen es Ihnen, Kenn Wort-und Konto Sperrungs Richtlinien für Benutzer und globale Sicherheitsgruppen in einer Domäne anzugeben. Weitere Informationen finden Sie unter [Schritt-für-Schritt-Anleitung für differenzierte Kenn Wort-und Konto Sperrungs Richtlinien Konfiguration](https://go.microsoft.com/fwlink/?LinkID=91477).
  * Persönliche virtuelle Desktops
     * Um die zusätzliche Funktionalität zu verwenden, die von der Registerkarte persönlicher virtueller Desktop im Dialogfeld Eigenschaften von Benutzerkonten in Active Directory-Benutzer und-Computer bereitgestellt wird, muss das AD DS Schema für Windows Server 2008 R2 (Schema Objekt Version = 47) erweitert werden. Weitere Informationen finden Sie unter Bereitstellen [persönlicher virtueller Desktops mithilfe RemoteApp-und Desktopverbindung Schritt-für-Schritt-Anleitung](https://go.microsoft.com/fwlink/?LinkId=183552).

## <a name="windows-server-2003"></a>Windows Server 2003

Unterstütztes Betriebs System des Domänen Controllers:

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Features der Windows Server 2003-Gesamtstruktur Funktionsebene

* Alle standardmäßigen AD DS Features und die folgenden Features sind verfügbar:
   * Gesamtstruktur-Vertrauensstellung
   * Domänenumbenennung
   * Verknüpfte Wert Replikation
      - Mit der verknüpften Wert Replikation können Sie die Gruppenmitgliedschaft ändern, um Werte für einzelne Mitglieder zu speichern und zu replizieren, statt die gesamte Mitgliedschaft als einzelne Einheit zu replizieren. Das Speichern und Replizieren der Werte einzelner Mitglieder beansprucht weniger Netzwerkbandbreite und weniger Prozessor Zyklen während der Replikation und verhindert, dass Updates verloren gehen, wenn Sie mehrere Mitglieder gleichzeitig auf unterschiedlichen Domänen Controllern hinzufügen oder entfernen.
   * Die Möglichkeit zum Bereitstellen eines schreibgeschützten Domänen Controllers (RODC)
   * Verbesserte Konsistenzprüfung für die Konsistenzprüfung (KCC) und Skalierbarkeit
      - Der standortübergreifende Topologie Generator (ISTG) verwendet verbesserte Algorithmen, die skalieren, um Gesamtstrukturen mit einer größeren Anzahl von Standorten zu unterstützen, als AD DS auf der Gesamtstruktur Funktionsebene von Windows 2000 unterstützen können. Der verbesserte ISTG-Wahl Algorithmus ist ein weniger eindringlicher Mechanismus zur Auswahl des ISTG auf der Windows 2000-Gesamtstruktur Funktionsebene.
   * Die Möglichkeit zum Erstellen von Instanzen der dynamischen Hilfsklasse mit dem Namen **DynamicObject** in einer Domänen Verzeichnis Partition
   * Die Möglichkeit zum Konvertieren einer **InetOrgPerson** -Objektinstanz in eine Instanz des **Benutzer** Objekts und zum Vervollständigen der Konvertierung in umgekehrter Richtung
   * Die Möglichkeit zum Erstellen von Instanzen von neuen Gruppen Typen, um die rollenbasierte Autorisierung zu unterstützen. 
      - Diese Typen werden als Anwendungs Basisgruppen und LDAP-Abfrage Gruppen bezeichnet.
   * Deaktivierung und Neudefinition von Attributen und Klassen im Schema Die folgenden Attribute können wieder verwendet werden: "ldapDisplayName", "schemaIDGUID", "OID" und "mAPIID".
   * Domänen basierte DFS-Namespaces, die im Windows Server 2008-Modus ausgeführt werden, einschließlich der Unterstützung für die Zugriffs basierte Enumeration und eine größere Skalierbarkeit. Weitere Informationen finden Sie unter [Auswählen eines Namespace Typs](https://go.microsoft.com/fwlink/?LinkId=180400).

### <a name="windows-server-2003-domain-functional-level-features"></a>Features der Windows Server 2003-Domänen Funktionsebene

* Alle Standard AD DS Features, alle Features, die auf der Funktionsebene der systemeigenen Windows 2000-Domäne verfügbar sind, und die folgenden Funktionen sind verfügbar:
   * Das Domänen Verwaltungs Tool Netdom. exe, das Ihnen das Umbenennen von Domänen Controllern ermöglicht.
   * Updates für den Anmeldezeit Stempel
      * Das **lastLogonTimestamp**-Attribut wird mit dem Zeitpunkt der letzten Anmeldung des Benutzers oder des Computers aktualisiert. Dieses Attribut wird innerhalb der Domäne repliziert.
   * Die Möglichkeit, das **userPassword** -Attribut als effektives Kennwort für **InetOrgPerson** und Benutzer Objekte festzulegen.
   * Möglichkeit zum Umleiten von Benutzern und Computer Containern
      * Standardmäßig werden für Computer-und Benutzerkonten von Computern zwei bekannte Container bereitgestellt: "CN = Computers<domain root> " und "CN =<domain root>Users". Diese Funktion ermöglicht die Definition eines neuen, bekannten Speicher Orts für diese Konten.
   * Die Fähigkeit des Autorisierungs-Managers, seine Autorisierungs Richtlinien in AD DS zu speichern.
   * Eingeschränkte Delegierung
      * Die eingeschränkte Delegierung ermöglicht es Anwendungen, die sichere Delegierung von Benutzer Anmelde Informationen mithilfe der Kerberos-basierten Authentifizierung zu nutzen.
      * Sie können die Delegierung auf bestimmte Ziel Dienste beschränken.
   * Selektive Authentifizierung
      * Durch die selektive Authentifizierung können Sie die Benutzer und Gruppen aus einer vertrauenswürdigen Gesamtstruktur angeben, die sich für Ressourcen Server in einer vertrauenden Gesamtstruktur authentifizieren dürfen.

## <a name="windows-2000"></a>Windows 2000

Unterstütztes Betriebs System des Domänen Controllers:

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Funktionsebene der Features der systemeigenen Windows 2000-Gesamtstruktur

* Alle Standard AD DS Features sind verfügbar.

### <a name="windows-2000-native-domain-functional-level-features"></a>Funktionen der systemeigenen Windows 2000-Domänen Funktionsebene

* Alle standardmäßigen AD DS Features und die folgenden Verzeichnisfunktionen sind verfügbar, darunter:
   * Universelle Gruppen für Verteiler-und Sicherheitsgruppen.
   * Gruppen Schachtelung
   * Gruppen Konvertierung, die die Konvertierung zwischen Sicherheits-und Verteiler Gruppen ermöglicht
   * Verlauf der Sicherheits-ID (SID)

## <a name="next-steps"></a>Nächste Schritte

* [Erhöhen der Domänen Funktionsebene](https://technet.microsoft.com/library/cc753104.aspx)  
* [Erhöhen der Gesamtstruktur Funktionsebene](https://technet.microsoft.com/library/cc730985.aspx)
