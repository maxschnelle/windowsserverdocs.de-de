---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: Windows Server 2016-Funktionsebenen
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: 5f7a8f08ff10102fbc04b6f8272320bd3b77785d
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80825493"
---
# <a name="forest-and-domain-functional-levels"></a>Gesamtstruktur- und Domänenfunktionsebenen

>Gilt für: Windows Server

Funktionsebenen bestimmen die verfügbaren AD DS-Domänen- oder Gesamtstrukturfunktionen (Active Directory Domain Services). Außerdem legen sie fest, welche Windows Server-Betriebssysteme auf Domänencontrollern in der Domäne oder der Gesamtstruktur ausgeführt werden können. Funktionsebenen haben jedoch keine Auswirkung darauf, welche Betriebssysteme Sie auf Arbeitsstationen und Mitgliedsservern ausführen können, die mit der Domäne oder der Gesamtstruktur verknüpft sind.

Legen Sie bei der Bereitstellung von AD DS die Domänen- und Gesamtstrukturfunktionsebenen auf den höchsten Wert fest, den die Umgebung unterstützen kann. Auf diese Weise können Sie so viele AD DS-Features wie möglich verwenden. Wenn Sie eine neue Gesamtstruktur bereitstellen, werden Sie aufgefordert, zunächst die Gesamtstrukturfunktionsebene und anschließend die Domänenfunktionsebene festzulegen. Sie können die Domänenfunktionsebene auf einen Wert festlegen, der höher als die Gesamtstrukturfunktionsebene ist. Sie können die Domänenfunktionsebene jedoch nicht auf einen niedrigeren Wert als die Gesamtstrukturfunktionsebene festlegen.

Mit dem Ende der Lebensdauer von Windows 2003 müssen Windows 2003-Domänencontrollern (DCs) auf Windows Server 2008, 2008 R2, 2012, 2012 R2, 2016 oder 2019 aktualisiert werden. Daher sollten alle Domänencontroller, die auf Windows Server 2003 ausgeführt werden, aus der Domäne entfernt werden.

Bei Windows Server 2008-Domänenfunktionsebenen (und höher) wird die DFS-Replikation (Distributed File Service) zum Replizieren von SYSVOL-Ordnerinhalten zwischen Domänencontrollern verwendet. Wenn Sie auf der Windows Server 2008-Domänenfunktionsebene (oder höher) eine neue Domäne erstellen, wird die DFS-Replikation automatisch zum Replizieren von SYSVOL verwendet. Wenn Sie die Domäne auf einer niedrigeren Funktionsebene erstellt haben, müssen Sie für SYSVOL anstatt des Dateireplikationsdiensts die DFS-Replikation verwenden. Für die Migrationsschritte können Sie entweder die [Anweisungen auf TechNet](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) oder die [optimierten Schritte im Storage Team File Cabinet-Blog](https://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx) befolgen.

## <a name="windows-server-2019"></a>Windows Server 2019

In dieser Version wurden keine neuen Gesamtstruktur- oder Domänenfunktionsebenen hinzugefügt.

Die Mindestanforderung zum Hinzufügen eines Windows Server 2019-Domänencontrollers ist eine Windows Server 2008-Funktionsebene. Die Domäne muss auch DFS-R als Engine zum Replizieren von SYSVOL verwenden.

## <a name="windows-server-2016"></a>Windows Server 2016

Unterstützte Betriebssysteme des Domänencontrollers:

* Windows Server 2019
* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Features für die Windows Server 2016-Gesamtstrukturfunktionsebene

* Alle auf der Windows Server 2012 R2-Gesamtstrukturebene verfügbaren Features sowie die folgenden Features sind verfügbar:
   * [PAM (Privileged Access Management) mithilfe von MIM (Microsoft Identity Manager)](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Features für die Windows Server 2016-Domänenfunktionsebene

* Alle Active Directory-Standardfeatures, alle Features der Windows Server 2012 R2-Domänenfunktionsebene und die folgenden Features sind verfügbar:
   * Domänencontroller können das automatische Rollen von NTLM und anderen kennwortbasierten Geheimnissen für ein Benutzerkonto unterstützen, das so konfiguriert ist, dass die PKI-Authentifizierung erforderlich ist. Diese Konfiguration wird auch als „Smart card required for interactive logon“ (Smartcard für interaktive Anmeldung erforderlich) bezeichnet.
   * Domänencontroller können das Zulassen von Netzwerk-NTLM unterstützen, wenn ein Benutzer auf bestimmte, in die Domäne eingebundene Geräte beschränkt ist.
   * Kerberos-Clients, die sich erfolgreich bei der PKInit Freshness-Erweiterung authentifizieren, erhalten die aktuelle SID der öffentlichen Schlüsselidentität.

    Weitere Informationen finden Sie unter [Neuerungen bei der Kerberos-Authentifizierung](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication) und [Neuerungen beim Schutz von Anmeldeinformationen](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection).

## <a name="windows-server-2012r2"></a>Windows Server 2012 R2

Unterstützte Betriebssysteme des Domänencontrollers:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Features für die Windows Server 2012 R2-Gesamtstrukturfunktionsebene

* Alle auf der Windows Server 2012-Gesamtstrukturfunktionsebene verfügbaren Features, jedoch keine zusätzlichen Features sind verfügbar.

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Features für die Windows Server 2012 R2-Domänenfunktionsebene

* Alle Active Directory-Standardfeatures, alle Features der Windows Server 2012-Domänenfunktionsebene und die folgenden Features sind verfügbar:
   * Domänencontrollerseitiger Schutz für geschützte Benutzer: Geschützte Benutzer, die sich bei einer Windows Server 2012 R2-Domäne authentifizieren, können Folgendes nicht mehr tun:
      * Authentifizieren mit der NTLM-Authentifizierung
      * Verwenden von DES- oder RC4-Verschlüsselungssammlungen bei der Kerberos-Vorauthentifizierung
      * Delegierung mit eingeschränkter oder nicht eingeschränkter Delegierung
      * Erneuern von Benutzertickets (TGTs) jenseits der ursprünglichen vierstündigen Lebensdauer
   * Authentifizierungsrichtlinien
      * Es sind neue gesamtstrukturbasierte Active Directory-Richtlinien verfügbar, die auf Konten in Windows Server 2012 R2-Domänen angewendet werden können. Mit diesen kann gesteuert werden, auf welchen Hosts sich ein Konto anmelden kann, und es können Zugriffssteuerungsbedingungen zur Authentifizierung für Dienste angewendet werden, die als Konto ausgeführt werden.
   * Authentifizierungsrichtliniensilos
      * Es ist ein neues gesamtstrukturbasiertes Active Directory-Objekt verfügbar, das eine Beziehung zwischen dem Benutzer, verwalteten Dienst und Computer sowie Konten herstellen kann, die zum Klassifizieren von Konten für Authentifizierungsrichtlinien oder die Authentifizierungsisolation verwendet werden.

## <a name="windows-server-2012"></a>Windows Server 2012

Unterstützte Betriebssysteme des Domänencontrollers:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Features für die Windows Server 2012-Gesamtstrukturfunktionsebene

* Es sind alle auf der Windows Server 2008 R2-Gesamtstrukturfunktionsebene verfügbaren Features, jedoch keine zusätzlichen Features verfügbar.

### <a name="windows-server-2012-domain-functional-level-features"></a>Features für die Windows Server 2012-Domänenfunktionsebene

* Alle Active Directory-Standardfeatures, alle Features der Windows Server 2008 R2-Domänenfunktionsebene und die folgenden Features sind verfügbar:
   * Für die Kerberos-Domänencontrollerrichtlinie bezüglich administrativer Vorlagen für die KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und den Kerberos-Schutz sind zwei Einstellungen verfügbar („Immer Ansprüche liefern“ und „Ungeschützte Authentifizierungsanfragen ablehnen“), für die die Windows Server 2012-Domänenfunktionsebene erforderlich ist. Weitere Informationen finden Sie unter [Neuerungen bei der Kerberos-Authentifizierung](https://technet.microsoft.com/library/hh831747.aspx).

## <a name="windows-server-2008r2"></a>Windows Server 2008 R2

Unterstützte Betriebssysteme des Domänencontrollers:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Features für die Windows Server 2008 R2-Gesamtstrukturfunktionsebene

* Alle Features, die auf der Gesamtstrukturfunktionsebene Windows Server 2003 verfügbar sind, plus die folgenden Features:
   * Active Directory-Papierkorb, der die Möglichkeit bietet, gelöschte Objekte in ihrer Gesamtheit wiederherzustellen, während AD DS ausgeführt wird.

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Features für die Windows Server 2008 R2-Domänenfunktionsebene

* Alle Active Directory-Standardfeatures, alle Features der Windows Server 2008-Domänenfunktionsebene und die folgenden Features sind verfügbar:
   * Die Authentifizierungsmechanismussicherung ist verfügbar, bei der Informationen zum Typ der Anmeldemethode (Smartcard oder Benutzername/Kennwort), die zum Authentifizieren von Domänenbenutzern dient, in das Kerberos-Token der einzelnen Benutzer eingefügt werden. Wenn dieses Feature in einer Netzwerkumgebung aktiviert ist, in der eine Infrastruktur zur Verbundidentitätsverwaltung wie Active Directory-Verbunddienste (Active Directory Federation Services, AD FS) implementiert ist, können die Informationen im Token extrahiert werden, wenn ein Benutzer auf eine Ansprüche unterstützende Anwendung zugreift, die zum Feststellen der Autorisierung auf Basis der Anmeldemethode des Benutzers entwickelt wurde.
   * Die automatische Dienstprinzipalnamenverwaltung ist für Dienste verfügbar, die auf einem bestimmten Computer im Kontext eines verwalteten Dienstkontos ausgeführt werden, wenn der Name oder DNS-Hostname des Computerkontos geändert wird. Weitere Informationen zu verwalteten Dienstkonten finden Sie in der [schrittweisen Anleitung für Dienstkonten](https://go.microsoft.com/fwlink/?LinkId=180401).

## <a name="windows-server-2008"></a>WindowsServer 2008

Unterstützte Betriebssysteme des Domänencontrollers:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Features für die Windows Server 2008-Gesamtstrukturfunktionsebene

* Es sind alle auf der Windows Server 2003-Gesamtstrukturfunktionsebene verfügbaren Features, jedoch keine zusätzlichen Features verfügbar. 

### <a name="windows-server-2008-domain-functional-level-features"></a>Features für die Windows Server 2008-Domänenfunktionsebene

* Alle AD DS-Standardfeatures, alle Features der Windows Server 2003-Domänenfunktionsebene und die folgenden Features sind verfügbar:
  * Unterstützung für die DFS-Replikation (verteiltes Dateisystem) für Windows Server 2003 System Volume (SYSVOL)
    * Die Unterstützung der DFS-Replikation bietet eine stabilere und detailliertere Replikation von SYSVOL-Inhalten.

      > [!NOTE]
      > Ab Windows Server 2012 R2 ist der Dateireplikationsdienst (File Replication Service, FRS) veraltet. Eine neue Domäne, die auf einem Domänencontroller erstellt wird, auf dem mindestens Windows Server 2012 R2 ausgeführt wird, muss auf die Windows Server 2008-Domänenfunktionsebene (oder höher) festgelegt werden.

  * Es sind im Windows Server 2008-Modus ausgeführte domänenbasierte DFS-Namespaces einschließlich der Unterstützung für die zugriffsbasierte Aufzählung und bessere Skalierbarkeit verfügbar. Domänenbasierte Namespaces im Windows Server 2008-Modus erfordern außerdem die Gesamtstruktur, um die Windows Server 2003-Gesamtstrukturfunktionsebene nutzen zu können. Weitere Informationen finden Sie unter [Auswählen eines Namespacetyps](https://go.microsoft.com/fwlink/?LinkId=180400).
  * Advanced Encryption Standard-Unterstützung (AES 128 und AES 256) für das Kerberos-Protokoll: Damit TGTs mithilfe von AES ausgestellt werden können, muss die Domänenfunktionsebene Windows Server 2008 oder höher sein und das Domänenkennwort geändert werden. 
    * Weitere Informationen finden Sie unter [Kerberos-Erweiterungen](https://technet.microsoft.com/library/cc749438(ws.10).aspx).

      > [!NOTE]
      >Auf einem Domänencontroller können nach der Änderung der Domänenfunktionsebene auf Windows Server 2008 oder höher Authentifizierungsfehler auftreten, wenn der Domänencontroller zwar schon die DFL-Änderung, noch nicht aber das „krbtgt“-Kennwort geändert hat. In diesem Fall löst ein Neustart des KDC-Diensts auf dem Domänencontroller eine Aktualisierung des neuen „krbtgt“-Kennworts im Arbeitsspeicher und zugehörige Authentifizierungsfehler aus.

  * Die Informationen zur [letzten interaktiven Anmeldung](https://go.microsoft.com/fwlink/?LinkId=180387) zeigen Folgendes an:
     * Gesamtanzahl fehlgeschlagener Anmeldeversuche auf einem Windows Server 2008-Server in einer Domäne oder einer Windows Vista-Arbeitsstation
     * Gesamtanzahl fehlgeschlagener Anmeldeversuche nach einer erfolgreichen Anmeldung auf einem Windows Server 2008-Server oder einer Windows Vista-Arbeitsstation
     * Zeitpunkt des letzten fehlgeschlagenen Anmeldeversuchs auf einem Windows Server 2008-Server oder einer Windows Vista-Workstation
     * Zeitpunkt des letzten erfolgreichen Anmeldeversuchs auf einem Windows Server 2008-Server oder einer Windows Vista-Workstation
  * Abgestimmte Kennwortrichtlinien ermöglichen das Festlegen von Kennwort- und Kontosperrungsrichtlinien für Benutzer und globale Sicherheitsgruppen in einer Domäne. Weitere Informationen finden Sie in der [schrittweisen Anleitung für die Konfiguration differenzierter Kennwort- und Kontosperrungsrichtlinien](https://go.microsoft.com/fwlink/?LinkID=91477).
  * persönliche virtuelle Desktops
     * Ihr AD DS-Schema muss für Windows Server 2008 R2 (Schemaobjektversion 47) erweitert werden, um die zusätzliche Funktionalität verwenden zu können, die von der Registerkarte „Persönlicher virtueller Computer“ im Dialogfeld „User Account Properties“ (Eigenschaften des Benutzerkontos) in Active Directory-Benutzern und -Computern bereitgestellt wird. Weitere Informationen finden Sie in der [schrittweisen Anleitung zum Bereitstellen persönlicher virtueller Desktops mithilfe von RemoteApp und Remotedesktopverbindungen](https://go.microsoft.com/fwlink/?LinkId=183552).

## <a name="windows-server-2003"></a>Windows Server 2003

Unterstützte Betriebssysteme des Domänencontrollers:

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Features für die Windows Server 2003-Gesamtstrukturfunktionsebene

* Alle AD DS-Standardfeatures und die folgenden Features sind verfügbar:
   * Gesamtstruktur-Vertrauensstellung
   * Domänenumbenennung
   * Verknüpfte Wertreplikation
      - Die verknüpfte Wertreplikation ermöglicht das Ändern der Gruppenmitgliedschaft zum Speichern und Replizieren von Werten für einzelne Mitglieder anstelle der Replikation der gesamten Mitgliedschaft als einzelne Einheit. Das Speichern und Replizieren der Werte einzelner Mitglieder beansprucht weniger Netzwerkbandbreite und weniger Prozessorzyklen während der Replikation und verhindert, dass Updates verloren gehen, wenn Sie gleichzeitig mehrere Mitglieder auf unterschiedlichen Domänencontrollern hinzufügen oder entfernen.
   * Möglichkeit zum Bereitstellen eines schreibgeschützten Domänencontrollers (RODC)
   * Verbesserte Algorithmen und Skalierbarkeit der Konsistenzprüfung (Knowledge Consistency Checker, KCC)
      - Der Generator für standortübergreifende Topologie (Intersite Topology Generator, ISTG) verwendet verbesserte Algorithmen für die Unterstützung von Gesamtstrukturen mit einer größeren Anzahl von Standorten als AD DS auf Windows 2000-Gesamtstrukturfunktionsebene unterstützen kann. Der verbesserte ISTG-Wahlalgorithmus ist ein weniger intrusiver Mechanismus zur Auswahl des ISTG auf der Windows 2000-Gesamtstrukturfunktionsebene.
   * Möglichkeit zum Erstellen von Instanzen der dynamischen Erweiterungsklasse namens **dynamicObject** in einer Domänenverzeichnispartition
   * Möglichkeit zum Konvertieren einer **inetOrgPerson**-Objektinstanz zu einer **User**-Objektinstanz bzw. in umgekehrter Richtung
   * Möglichkeit zum Erstellen von Instanzen von neuen Gruppentypen für die Unterstützung der rollenbasierten Autorisierung 
      - Diese Typen werden als „Anwendungsbasisgruppen“ und „LDAP-Abfragegruppen“ bezeichnet.
   * Deaktivierung und Neudefinition von Attributen und Klassen im Schema Die folgenden Attribute können wieder verwendet werden: ldapDisplayName, schemaIdGuid, OID und mapiID.
   * Es sind im Windows Server 2008-Modus ausgeführte domänenbasierte DFS-Namespaces einschließlich der Unterstützung für die zugriffsbasierte Aufzählung und bessere Skalierbarkeit verfügbar. Weitere Informationen finden Sie unter [Auswählen eines Namespacetyps](https://go.microsoft.com/fwlink/?LinkId=180400).

### <a name="windows-server-2003-domain-functional-level-features"></a>Features für die Windows Server 2003-Domänenfunktionsebene

* Alle AD DS-Standardfeatures, alle auf der nativen Windows 2000-Domänenfunktionsebene verfügbaren Features und die folgenden Features sind verfügbar:
   * Das Domänenverwaltungstool „Netdom.exe“ ermöglicht das Umbenennen von Domänencontrollern.
   * Updates für Anmeldungszeitstempel
      * Das **lastLogonTimestamp**-Attribut wird mit dem Zeitpunkt der letzten Anmeldung des Benutzers oder des Computers aktualisiert. Dieses Attribut wird innerhalb der Domäne repliziert.
   * Möglichkeit zum Festlegen des **userPassword**-Attributs als effektives Kennwort für das **inetOrgPerson**-Objekt und für Benutzerobjekte
   * Möglichkeit zum Umleiten von Benutzer- und Computercontainern
      * Standardmäßig werden für Computer und Benutzerkonten zwei bekannte Container bereitgestellt: „cn=Computers,<domain root>“ und „cn=Users,<domain root>“. Mit diesem Feature kann für diese Konten ein neuer, bekannter Speicherort definiert werden.
   * Möglichkeit für den Autorisierungs-Manager zum Speichern von Autorisierungsrichtlinien in AD DS
   * Eingeschränkte Delegierung
      * Die eingeschränkte Delegierung ermöglicht Anwendungen die Nutzung der sicheren Delegierung von Anmeldeinformationen mithilfe der Kerberos-basierten Authentifizierung.
      * Sie können die Delegierung auf bestimmte Zieldienste beschränken.
   * Ausgewählte Authentifizierung
      * Die ausgewählte Authentifizierung ermöglicht das Angeben von Benutzern und Gruppen aus einer Gesamtstruktur, die sich bei Ressourcenservern in einer vertrauenswürdigen Gesamtstruktur authentifizieren dürfen.

## <a name="windows-2000"></a>Windows 2000

Unterstützte Betriebssysteme des Domänencontrollers:

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Features für die native Windows 2000-Gesamtstrukturfunktionsebene

* Alle AD DS-Standardfeatures sind verfügbar.

### <a name="windows-2000-native-domain-functional-level-features"></a>Features für die native Windows 2000-Domänenfunktionsebene

* Alle AD DS-Standardfeatures sowie die folgenden Verzeichnisfunktionen sind verfügbar:
   * universelle Gruppen für Verteiler- und Sicherheitsgruppen
   * Gruppenverschachtelung
   * Gruppenkonvertierung für den Wechsel zwischen Sicherheits- und Verteilergruppen
   * Sicherheits-ID-Verlauf (Security Identifier, SID)

## <a name="next-steps"></a>Nächste Schritte

* [Heraufstufen der Domänenfunktionsebene](https://technet.microsoft.com/library/cc753104.aspx)  
* [Heraufstufen der Gesamtstrukturfunktionsebene](https://technet.microsoft.com/library/cc730985.aspx)
