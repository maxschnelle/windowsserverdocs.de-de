---
title: Authentifizierungsrichtlinie und Authentifizierungsrichtliniensilos
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-credential-protection
ms.topic: article
ms.assetid: 7eb0e640-033d-49b5-ab44-3959395ad567
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 705cba94299572f02c12896e2dac0ec8c2d070c0
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520179"
---
# <a name="authentication-policies-and-authentication-policy-silos"></a>Authentifizierungsrichtlinie und Authentifizierungsrichtliniensilos

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema für IT-Spezialisten werden Authentifizierungsrichtliniensilos und die Richtlinien beschrieben, mit denen Konten auf diese Silos beschränkt werden können. Zudem wird erklärt, wie der Bereich von Konten mit Authentifizierungsrichtlinien eingeschränkt werden kann.

Authentifizierungsrichtliniensilos und die zugehörigen Richtlinien stellen eine Möglichkeit dar, Anmeldeinformationen mit erhöhten Rechten auf Systeme zu beschränken, die nur für ausgewählte Benutzer, Computer oder Dienste relevant sind. Silos können mit dem Active Directory-Verwaltungscenter und den Active Directory Windows PowerShell-Cmdlets in den Active Directory-Domänendiensten (Active Directory Domain Services, AD DS) definiert und verwaltet werden.

Authentifizierungsrichtliniensilos sind Container, denen Administratoren Benutzerkonten, Computerkonten und Dienstkonten zuweisen können. Über die Authentifizierungsrichtlinien, die auf diesen Container angewendet werden, können dann Gruppen von Konten verwaltet werden. Daher muss der Administrator nicht mehr im gleichen Umfang wie bisher den Ressourcenzugriff einzelner Konten verfolgen, und es wird verhindert, dass böswillige Benutzer durch den Diebstahl von Anmeldeinformationen Zugriff auf andere Ressourcen erlangen.

In Windows Server 2012 R2 eingeführte Funktionen ermöglichen es Ihnen, Authentifizierungs Richtlinien Silos zu erstellen, die eine Gruppe von Benutzern mit hohen Berechtigungen hosten. Sie können diesem Container Authentifizierungsrichtlinien zuordnen, um die Verwendung privilegierter Konten in der Domäne zu begrenzen. Wenn Konten zur Sicherheitsgruppe "Geschützte Benutzer" gehören, werden zusätzliche Kontrollmechanismen angewendet, z. B. die exklusive Verwendung des Kerberos-Protokolls.

Damit können Sie die Nutzung hochwertiger Konten auf hochwertige Hosts begrenzen. Beispielsweise könnten Sie ein neues Silo für Administratoren der Gesamtstruktur erstellen, das Unternehmens-, Schema- und Domänenadministratoren enthält. Anschließend könnten Sie das Silo mit einer Authentifizierungsrichtlinie konfigurieren, sodass eine kennwort- und smartcard-basierte Authentifizierung von Systemen, die keine Domänencontroller oder Domänenadministratorkonsolen sind, fehlschlägt.

Informationen zum Konfigurieren von Authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien finden Sie unter [Konfigurieren geschützter Konten](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts).

### <a name="about-authentication-policy-silos"></a>Informationen zu Authentifizierungsrichtliniensilos
Mit einem Authentifizierungsrichtliniensilo wird gesteuert, welche Konten durch das Silo eingeschränkt werden können, und es werden damit die Authentifizierungsrichtlinien definiert, die auf die Mitglieder angewendet werden sollen. Sie können das Silo anhand der Anforderungen Ihrer Organisation erstellen. Silos sind Active Directory-Objekte für Benutzer, Computer und Dienste, die nach dem Schema in der folgenden Tabelle definiert sind.

**Active Directory-Schema für Authentifizierungsrichtliniensilos**

|Anzeigename|BESCHREIBUNG|
|--------|--------|
|Authentifizierungsrichtliniensilo|Eine Instanz dieser Klasse definiert die Authentifizierungsrichtlinien und das zugehörige Verhalten für die zugewiesenen Benutzer, Computer und Dienste.|
|Authentifizierungsrichtliniensilos|Ein Container dieser Klasse kann Authentifizierungsrichtliniensilo-Objekte enthalten.|
|Authentication Policy Silo Enforced (Authentifizierungsrichtliniensilo erzwungen)|Gibt an, ob das Authentifizierungsrichtliniensilo erzwungen wird.<p>Wenn es nicht erzwungen wird, dann ist für die Richtlinie standardmäßig der Überwachungsmodus aktiviert. Es werden Ereignisse generiert, die potenzielle Erfolge und Fehler anzeigen, aber es werden keine Schutzmaßnahmen auf das System angewendet.|
|Assigned Authentication Policy Silo Backlink (Rückverweis für zugewiesenes Authentifizierungsrichtliniensilo)|Dieses Attribut ist der Rückverweis für msDS-AssignedAuthNPolicySilo.|
|Authentication Policy Silo Members (Authentifizierungsrichtliniensilo-Mitglieder)|Gibt an, welche Prinzipale dem AuthNPolicySilo-Objekt zugewiesen sind.|
|Authentication Policy Silo Members Backlink (Rückverweis für Authentifizierungsrichtliniensilo-Mitglieder)|Dieses Attribut ist der Rückverweis für msDS-AuthNPolicySiloMembers.|

Authentifizierungsrichtliniensilos können mit der Active Directory-Verwaltungskonsole oder Windows PowerShell konfiguriert werden. Weitere Informationen finden Sie unter [Konfigurieren geschützter Konten](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts).

### <a name="about-authentication-policies"></a>Informationen zu Authentifizierungsrichtlinien
Authentifizierungsrichtlinien definieren die Lebensdauereigenschaften des Ticket-Granting Ticket (TGT) für das Kerberos-Protokoll und die Bedingungen für die Authentifizierungszugriffssteuerung für einen Kontotyp. Die Richtlinie basiert auf dem AD DS-Container, der als Authentifizierungsrichtliniensilo bezeichnet wird, und kontrolliert diesen.

Über Authentifizierungsrichtlinien wird Folgendes gesteuert:

-   Die TGT-Lebensdauer des Kontos, das als nicht erneuerbar konfiguriert wurde.

-   Die Kriterien, die Gerätekonten erfüllen müssen, um sich mit einem Kennwort oder einem Zertifikat anmelden zu können.

-   Die Kriterien, die Benutzer und Geräte erfüllen müssen, um sich gegenüber Diensten authentifizieren zu können, die unter dem Konto ausgeführt werden.

Der Active Directory Kontotyp bestimmt die Rolle des Aufrufers als einer der folgenden:

-   **Benutzer**

    Benutzer sollten immer Mitglied der Sicherheitsgruppe "Geschützte Benutzer" sein, die Authentifizierungsversuche über NTLM standardmäßig nicht zulässt.

    Richtlinien können so konfiguriert werden, dass die TGT-Lebensdauer eines Benutzerkontos auf einen kürzeren Wert festgelegt wird oder die Geräte eingeschränkt werden, auf die sich ein Benutzerkonto anmelden kann. Rich-Ausdrücke können in der Authentifizierungs Richtlinie konfiguriert werden, um die Kriterien zu steuern, die die Benutzer und Ihre Geräte erfüllen müssen, um sich beim Dienst zu authentifizieren.

    Weitere Informationen finden Sie unter [Sicherheitsgruppe "Geschützte Benutzer"](protected-users-security-group.md).

-   **Service**

    Eigenständige verwaltete Dienstkonten, gruppenverwalteten Dienstkonten oder ein benutzerdefiniertes Kontoobjekt, das von diesen beiden Dienstkontotypen abgeleitet ist, werden verwendet. Mit Richtlinien können die Zugriffs Steuerungs Bedingungen eines Geräts festgelegt werden, die verwendet werden, um die Anmelde Informationen für verwaltete Dienst Konten auf bestimmte Geräte mit einer Active Directory-Identität einzuschränken. Dienste sollten nie Mitglied der Sicherheitsgruppe "Geschützte Benutzer" sein, weil sonst alle eingehenden Authentifizierungsversuche fehlschlagen.

-   **Computer**

    Verwendet wird das Computerkontoobjekt oder das benutzerdefinierte Kontoobjekt, das vom Computerkontoobjekt abgeleitet wurde. Durch Richtlinien können die Zugriffssteuerungsbedingungen festgelegt werden, die erfüllt sein müssen, um eine Authentifizierung anhand der Benutzer- oder Geräteeigenschaften gegenüber dem Konto zuzulassen. Computer sollten nie Mitglied der Sicherheitsgruppe "Geschützte Benutzer" sein, weil sonst alle eingehenden Authentifizierungsversuche fehlschlagen. Standardmäßig werden NTML-Authentifizierungsversuche abgelehnt. Für Computerkonten sollte keine TGT-Lebensdauer konfiguriert werden.

> [!NOTE]
> Es ist möglich, eine Authentifizierungsrichtlinie für eine Gruppe von Konten festzulegen, ohne die Richtlinie mit einem Authentifizierungsrichtliniensilo zu verknüpfen. Sie können diese Strategie verwenden, wenn nur ein einzelnes Konto geschützt werden muss.

**Active Directory-Schema für Authentifizierungsrichtlinien**

Die Richtlinien für die Active Directory-Objekte für Benutzer, Computer und Dienste werden nach dem Schema in der folgenden Tabelle definiert.

|type|Anzeigename|BESCHREIBUNG|
|----|--------|--------|
|Policy|Authentifizierungsrichtlinie|Eine Instanz dieser Klasse definiert Authentifizierungsrichtlinienverhalten für die zugewiesenen Prinzipale.|
|Policy|Authentifizierungsrichtlinien|Ein Container dieser Klasse kann Authentifizierungsrichtlinien-Objekte enthalten.|
|Policy|Authentication Policy Enforced (Authentifizierungsrichtlinien erzwungen)|Gibt an, ob die Authentifizierungsrichtlinie erzwungen wird.<p>Wenn sie nicht erzwungen wird, dann ist für die Richtlinie standardmäßig der Überwachungsmodus aktiviert, und es werden Ereignisse zum Anzeigen potenzieller Erfolge oder Fehler generiert, aber keine Schutzmaßnahmen auf das System angewendet.|
|Policy|Assigned Authentication Policy Backlink (Rückverweis für zugewiesene Authentifizierungsrichtlinie)|Dieses Attribut ist der Rückverweis für msDS-AssignedAuthNPolicy.|
|Policy|Assigned Authentication Policy (Zugewiesene Authentifizierungsrichtlinie)|Gibt an, welches AuthNPolicy-Objekt auf diesen Prinzipal angewendet werden soll.|
|Benutzer|User Authentication Policy (Benutzerauthentifizierungsrichtlinie)|Gibt an, welches AuthNPolicy-Objekt auf die Benutzer, die diesem Siloobjekt zugewiesen wurden, angewendet werden soll.|
|Benutzer|User Authentication Policy Backlink (Rückverweis für Benutzerauthentifizierungsrichtlinie)|Dieses Attribut ist der Rückverweis für msDS-UserAuthNPolicy.|
|Benutzer|ms-DS-User-Allowed-To-Authenticate-To|Mit diesem Attribut wird bestimmt, welcher Gruppe von Prinzipalen erlaubt wird, sich gegenüber einem Dienst, der unter dem Benutzerkonto ausgeführt wird, zu authentifizieren.|
|Benutzer|ms-DS-User-Allowed-To-Authenticate-From|Mit diesem Attribut wird die Gruppe von Geräten festgelegt, für die ein Benutzerkonto Anmeldeberechtigungen besitzt.|
|Benutzer|User TGT Lifetime (Benutzer-TGT-Lebensdauer)|Legt das maximale Alter (in Sekunden) eines Kerberos-TGT fest, das für einen Benutzer ausgestellt wird. Die resultierenden TGTs sind nicht erneuerbar.|
|Computer|Computer Authentication Policy (Computerauthentifizierungsrichtlinie)|Gibt an, welches AuthNPolicy-Objekt auf die Computer, die diesem Siloobjekt zugewiesen wurden, angewendet werden soll.|
|Computer|Computer Authentication Policy Backlink (Rückverweis für Computerauthentifizierungsrichtlinie)|Dieses Attribut ist der Rückverweis für msDS-ComputerAuthNPolicy.|
|Computer|ms-DS-Computer-Allowed-To-Authenticate-To|Mit diesem Attribut wird bestimmt, welcher Gruppe von Prinzipalen erlaubt wird, sich gegenüber einem Dienst, der unter dem Computerkonto ausgeführt wird, zu authentifizieren.|
|Computer|Computer TGT Lifetime (Computer-TGT-Lebensdauer)|Legt das maximale Alter (in Sekunden) eines Kerberos-TGT fest, das für einen Computer ausgestellt wird. Von der Änderung dieser Einstellung wird abgeraten.|
|Dienst|Service Authentication Policy (Dienstauthentifizierungsrichtlinie)|Gibt an, welches AuthNPolicy-Objekt auf die Dienste, die diesem Siloobjekt zugewiesen wurden, angewendet werden soll.|
|Dienst|Service Authentication Policy Backlink (Rückverweis für Dienstauthentifizierungsrichtlinie)|Dieses Attribut ist der Rückverweis für msDS-ServiceAuthNPolicy.|
|Dienst|ms-DS-Service-Allowed-To-Authenticate-To|Mit diesem Attribut wird bestimmt, welcher Gruppe von Prinzipalen erlaubt wird, sich gegenüber einem Dienst, der unter dem Dienstkonto ausgeführt wird, zu authentifizieren.|
|Dienst|ms-DS-Service-Allowed-To-Authenticate-From|Mit diesem Attribut wird die Gruppe von Geräten festgelegt, für die ein Dienstkonto Anmeldeberechtigungen besitzt.|
|Dienst|Service TGT Lifetime (Dienst-TGT-Lebensdauer)|Legt das maximale Alter (in Sekunden) eines Kerberos-TGT fest, das für einen Dienst ausgestellt wird.|

Authentifizierungsrichtlinien können mit der Active Directory-Verwaltungskonsole oder Windows PowerShell für jedes Silo konfiguriert werden. Weitere Informationen finden Sie unter [Konfigurieren geschützter Konten](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts).

## <a name="how-it-works"></a>Funktionsweise
In diesem Abschnitt wird die Funktionsweise von Authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien in Verbindung mit der Sicherheitsgruppe "Geschützte Benutzer" und die Implementierung des Kerberos-Protokolls in Windows beschrieben.

-   [Verwendung des Kerberos-Protokolls mit Authentifizierungssilos und -richtlinien](#BKMK_HowKerbUsed)

-   [Einschränken einer Benutzeranmeldung](#BKMK_HowRestrictingSignOn)

-   [Einschränken der Ausstellung von Diensttickets](#BKMK_HowRestrictingServiceTicket)

**Geschützte Konten**

Die Sicherheitsgruppe "geschützte Benutzer" löst nicht konfigurierbaren Schutz auf Geräten und Host Computern aus, auf denen Windows Server 2012 R2 und Windows 8.1 ausgeführt wird, sowie auf Domänen Controllern in Domänen mit einem primären Domänen Controller unter Windows Server 2012 R2. Abhängig von der Domänenfunktionsebene des Kontos sind die Mitglieder der Sicherheitsgruppe "Geschützte Benutzer" aufgrund der Änderungen der Authentifizierungsmethoden, die in Windows unterstützt werden, zusätzlich geschützt.

-   Mitglieder der Sicherheitsgruppe "Geschützte Benutzer" können sich nicht unter Verwendung von NTLM, Digestauthentifizierung oder der Delegierung der Standardanmeldeinformationen mit CredSSP authentifizieren. Auf einem Gerät mit Windows 8.1, das einen dieser SSPs (Security Support Providers) verwendet, schlägt die Authentifizierung bei einer Domäne fehl, wenn das Konto Mitglied der Sicherheitsgruppe "geschützte Benutzer" ist.

-   Das Kerberos-Protokoll verwendet die schwächeren Verschlüsselungstypen DES oder RC4 nicht im Vorauthentifizierungsprozess. Daher muss die Domäne so konfiguriert werden, dass mindestens der Verschlüsselungstyp AES unterstützt wird.

-   Das Konto des Benutzers kann nicht mit eingeschränkter oder nicht eingeschränkter Kerberos-Delegierung delegiert werden. Das bedeutet, dass frühere Verbindungen mit anderen Systemen fehlschlagen, wenn der Benutzer Mitglied der Sicherheitsgruppe "Geschützte Benutzer" ist.

-   Die Standardeinstellung für die Lebensdauer von Kerberos-TGTs von vier Stunden kann mit Authentifizierungsrichtlinien und -silos konfiguriert werden, auf die über das Active Directory-Verwaltungscenter zugegriffen werden kann. Das heißt, dass sich der Benutzer nach Ablauf von vier Stunden erneut authentifizieren muss.

Weitere Informationen zu dieser Sicherheitsgruppe finden Sie unter [Funktionsweise der Gruppe "Geschützte Benutzer"](protected-users-security-group.md#BKMK_HowItWorks).

**Silos und Authentifizierungsrichtlinien**

Authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien nutzen die vorhandene Windows-Authentifizierungsinfrastruktur. Die Verwendung des NTLM-Protokolls wird abgelehnt, und das Kerberos-Protokoll wird mit neueren Verschlüsselungstypen verwendet. Authentifizierungsrichtlinien ergänzen die Sicherheitsgruppe "Geschützte Benutzer" durch die Möglichkeit, konfigurierbare Einschränkungen auf Konten anzuwenden, sowie durch die Bereitstellung von Einschränkungen für Dienst- und Computerkonten. Authentifizierungsrichtlinien werden während des Austauschs des Authentifizierungsdiensts (Authentication Service, AS) und des Ticket-Granting Service (TGS) des Kerberos-Protokolls erzwungen. Weitere Informationen dazu, wie Windows das Kerberos-Protokoll verwendet und welche Änderungen zur Unterstützung von Authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien vorgenommen wurden, finden Sie unter:

-   [Funktionsweise des Kerberos Version 5-Authentifizierungs Protokolls](https://technet.microsoft.com/library/cc772815(v=ws.10).aspx)

-   [Änderungen bei der Kerberos-Authentifizierung](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) (Windows Server 2008 R2 und Windows 7)

### <a name="how-the-kerberos-protocol-is-used-with-authentication-policy-silos-and-policies"></a><a name="BKMK_HowKerbUsed"></a>Verwendung des Kerberos-Protokolls mit Authentifizierungsrichtliniensilos und -richtlinien
Wenn ein Domänenkonto mit einem Authentifizierungsrichtliniensilo verknüpft wird und der Benutzer sich anmeldet, fügt der Sicherheitskonto-Manager den Anspruchstyp "Authentifizierungsrichtliniensilo" hinzu, der das Silo als Wert enthält. Dieser Anspruch im Konto bietet Zugriff auf das betreffende Silo.

Wenn eine Authentifizierungsrichtlinie erzwungen wird und die Authentifizierungsdienstanforderung für ein Domänenkonto beim Domänencontroller eingeht, dann gibt der Domänencontroller ein nicht erneuerbares TGT mit der konfigurierten Lebensdauer zurück (sofern das Domänen-TGT keine kürzere Lebensdauer hat).

> [!NOTE]
> Das Domänenkonto muss eine konfigurierte TGT-Lebensdauer besitzen und entweder direkt oder indirekt über die Silomitgliedschaft mit der Richtlinie verknüpft werden.

Wenn der Überwachungsmodus für eine Authentifizierungsrichtlinie aktiviert ist und beim Domänencontroller die Authentifizierungsdienstanforderung für ein Domänenkonto eingeht, dann prüft der Domänencontroller, ob die Authentifizierung des Geräts zulässig ist, damit beim Auftreten eines Fehlers eine Warnung protokolliert werden kann. Da der Prozess durch eine überwachte Authentifizierungsrichtlinie nicht geändert wird, schlagen Authentifizierungsanforderungen nicht fehl, wenn sie die Anforderungen der Richtlinie nicht erfüllen.

> [!NOTE]
> Das Domänenkonto muss entweder direkt oder indirekt über die Silomitgliedschaft mit der Richtlinie verknüpft werden.

Wenn eine Authentifizierungsrichtlinie erzwungen wird und der Authentifizierungsdienst Kerberos Armoring verwendet, dann wird die Authentifizierungsdienstanforderung für ein Domänenkonto auf dem Domänencontroller empfangen, und der Domänencontroller prüft, ob die Authentifizierung für das Gerät zulässig ist. Wenn ein Fehler auftritt, gibt der Domänencontroller eine Fehlermeldung zurück und protokolliert ein Ereignis.

> [!NOTE]
> Das Domänenkonto muss entweder direkt oder indirekt über die Silomitgliedschaft mit der Richtlinie verknüpft werden.

Wenn sich eine Authentifizierungs Richtlinie im Überwachungsmodus befindet und ein Ticket Erstellungs Service Request vom Domänen Controller für ein Domänen Konto empfangen wird, prüft der Domänen Controller, ob die Authentifizierung gemäß den PAC-Daten (Ticket Privilege Attribute Certificate) der Anforderung zulässig ist, und protokolliert eine Warnmeldung, wenn ein Fehler auftritt. Das PAC enthält verschiedene Arten von Autorisierungsdaten, darunter die Gruppen, denen der Benutzer als Mitglied angehört, die Rechte des Benutzers und die Richtlinien, die für den Benutzer gelten. Diese Informationen werden verwendet, um das Zugriffs Token des Benutzers zu generieren. Handelt es sich um eine erzwungene Authentifizierungs Richtlinie, die die Authentifizierung für einen Benutzer, ein Gerät oder einen Dienst ermöglicht, prüft der Domänen Controller, ob die Authentifizierung auf der Grundlage der PAC-Daten der Anforderung zulässig ist. Wenn ein Fehler auftritt, gibt der Domänencontroller eine Fehlermeldung zurück und protokolliert ein Ereignis.

> [!NOTE]
> Das Domänenkonto muss entweder direkt oder indirekt über die Silomitgliedschaft mit einer überwachten Richtlinie verknüpft werden, welche die Authentifizierung eines Benutzers, Geräts oder Diensts zulässt.

Sie können eine Authentifizierungsrichtlinie für alle Mitglieder eines Silos oder getrennte Richtlinien für Benutzer, Computer und verwaltete Dienstkonten verwenden.

Authentifizierungsrichtlinien können mit der Active Directory-Verwaltungskonsole oder Windows PowerShell für jedes Silo konfiguriert werden. Weitere Informationen finden Sie unter [Konfigurieren geschützter Konten](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts).

### <a name="how-restricting-a-user-sign-in-works"></a><a name="BKMK_HowRestrictingSignOn"></a>Einschränken einer Benutzeranmeldung
Weil diese Authentifizierungsrichtlinien auf ein Konto angewendet werden, gelten sie auch für Konten, die von Diensten verwendet werden. Wenn Sie die Verwendung eines Kennworts für einen Dienst auf bestimmte Hosts beschränken möchten, ist diese Einstellung hilfreich. Beispielsweise werden gruppenverwaltete Dienstkonten so konfiguriert, dass die Hosts das Kennwort von den Active Directory-Domänendiensten abrufen können. Allerdings kann dieses Kennwort auf jedem Host zur anfänglichen Authentifizierung verwendet werden. Durch die Anwendung einer Zugriffssteuerungsbedingung kann eine zusätzliche Schutzebene eingeführt werden, indem das Kennwort nur auf die Gruppe von Hosts begrenzt wird, welche das Kennwort abrufen können.

Wenn von Diensten, die als System, Netzwerkdienst oder andere Identität des lokalen Diensts ausgeführt werden, eine Verbindung mit Netzwerkdiensten hergestellt wird, wird das Computer Konto des Hosts verwendet. Computerkonten können nicht beschränkt werden. Selbst wenn der Dienst ein Computerkonto verwendet, das nicht für einen Windows-Host vorgesehen ist, kann dieses nicht eingeschränkt werden.

Wenn Sie die Benutzeranmeldung auf bestimmte Hosts einschränken, muss der Domänen Controller die Identität des Hosts überprüfen. Bei Verwendung der Kerberos-Authentifizierung mit Kerberos Amoring (die Bestandteil der dynamischen Zugriffssteuerung ist), dann wird das Schlüsselverteilungscenter mit dem TGT des Hosts bereitgestellt, von dem der Benutzer authentifiziert wird. Der Inhalt dieses geschützten TGT wird zur Durchführung einer Zugriffsprüfung verwendet, mit der bestimmt wird, ob der Host zulässig ist.

Wenn sich der Benutzer bei Windows anmeldet oder seine Domänenanmeldeinformationen in eine Eingabeaufforderung für die Anmeldung bei einer Anwendung eingibt, dann sendet Windows standardmäßig eine ungeschützte Authentifizierungsdienstanforderung (AS-REQ) an den Domänencontroller. Wenn der Benutzer die Anforderung von einem Computer, der Kerberos Armoring nicht unterstützt, aus sendet (z. B. Computer mit Windows 7 oder Windows Vista), schlägt die Anforderung fehl.

In der folgenden Liste wird der Prozess beschrieben:

-   Der Domänen Controller in einer Domäne, auf der Windows Server 2012 R2 ausgeführt wird, fragt das Benutzerkonto ab und bestimmt, ob es mit einer Authentifizierungs Richtlinie konfiguriert ist, die die anfängliche Authentifizierung einschränkt, die hochgerüstete Anforderungen erfordert.

-   Der Domänencontroller kann die Anforderung nicht erfüllen.

-   Da armoring erforderlich ist, kann der Benutzer versuchen, sich mit einem Computer anzumelden, auf dem Windows 8.1 oder Windows 8 ausgeführt wird, der Kerberos armoring unterstützen kann, um den Anmeldevorgang zu wiederholen.

-   Windows erkennt, dass die Domäne Kerberos Armoring unterstützt, und sendet eine geschützte AS-REQ, um die Anmeldungsanforderung zu wiederholen.

-   Der Domänen Controller führt eine Zugriffs Überprüfung mit den konfigurierten Zugriffs Steuerungs Bedingungen und den Identitätsinformationen des Client Betriebssystems im TGT aus, die zur Rüstung der Anforderung verwendet wurden.

-   Wenn die Zugriffsprüfung fehlschlägt, lehnt der Domänencontroller die Anforderung ab.

Selbst wenn das Betriebssystem Kerberos Armoring unterstützt, können Zugriffssteuerungsanforderungen angewendet werden, die erfüllt sein müssen, bevor der Zugriff gewährt wird. Die Benutzer melden sich bei Windows an oder geben ihre Domänenanmeldeinformationen in eine Eingabeaufforderung für die Anmeldung bei einer Anwendung ein. Standardmäßig sendet Windows eine ungeschützte AS-REQ an den Domänencontroller. Wenn der Benutzer die Anforderung von einem Computer sendet, der armoring unterstützt (z. b. Windows 8.1 oder Windows 8), werden Authentifizierungs Richtlinien wie folgt ausgewertet:

1.  Der Domänen Controller in einer Domäne, auf der Windows Server 2012 R2 ausgeführt wird, fragt das Benutzerkonto ab und bestimmt, ob es mit einer Authentifizierungs Richtlinie konfiguriert ist, die die anfängliche Authentifizierung einschränkt, die hochgerüstete Anforderungen erfordert.

2.  Der Domänen Controller führt eine Zugriffs Überprüfung mithilfe der konfigurierten Zugriffs Steuerungs Bedingungen und der Identitätsinformationen des Systems im TGT aus, die zur Rüstung der Anforderung verwendet werden. Die Zugriffsprüfung ist erfolgreich.

    > [!NOTE]
    > Wenn ältere Arbeitsgruppeneinschränkungen konfiguriert wurden, müssen auch diese erfüllt werden.

3.  Der Domänencontroller antwortet mit einer geschützten Antwort (AS-REP), und die Authentifizierung wird fortgesetzt.

### <a name="how-restricting-service-ticket-issuance-works"></a><a name="BKMK_HowRestrictingServiceTicket"></a>Einschränken der Ausstellung von Diensttickets
Wenn ein Konto nicht zulässig ist und ein Benutzer, der ein TGT verwendet, eine Verbindung mit dem Dienst herstellt (z. b. durch Öffnen einer Anwendung, die eine Authentifizierung bei einem Dienst erfordert, der durch den Dienst Prinzipal Namen (SPN) des Dienstanbieter identifiziert wird, erfolgt die folgende Sequenz:

1.  Bei einem Versuch, von SPN eine Verbindung mit SPN1 herzustellen, sendet Windows eine TGS-REQ an den Domänencontroller, der ein Dienstticket für SPN1 anfordert.

2.  Der Domänen Controller in einer Domäne, auf der Windows Server 2012 R2 ausgeführt wird, sucht nach dem Active Directory Domain Services Konto für den Dienst und stellt fest, dass das Konto mit einer Authentifizierungs Richtlinie konfiguriert ist, die die Ausstellung von Dienst Tickets einschränkt.

3.  Der Domänen Controller führt eine Zugriffs Überprüfung mit den konfigurierten Zugriffs Steuerungs Bedingungen und den Identitätsinformationen des Benutzers im TGT aus. Die Zugriffsprüfung schlägt fehl.

4.  Der Domänencontroller weist die Anforderung zurück.

Wenn ein Konto zulässig ist, weil das Konto die von der Authentifizierungs Richtlinie festgelegten Zugriffs Steuerungs Bedingungen erfüllt und ein Benutzer, der ein TGT hat, versucht, eine Verbindung mit dem Dienst herzustellen (z. b. durch Öffnen einer Anwendung, die eine Authentifizierung bei einem Dienst erfordert, der durch den Dienst Prinzipal Namen identifiziert wird), erfolgt die folgende Sequenz:

1.  Bei einem Versuch, eine Verbindung mit SPN1 herzustellen, sendet Windows eine TGS-REQ an den Domänencontroller, der ein Dienstticket für SPN1 anfordert.

2.  Der Domänen Controller in einer Domäne, auf der Windows Server 2012 R2 ausgeführt wird, sucht nach dem Active Directory Domain Services Konto für den Dienst und stellt fest, dass das Konto mit einer Authentifizierungs Richtlinie konfiguriert ist, die die Ausstellung von Dienst Tickets einschränkt.

3.  Der Domänen Controller führt eine Zugriffs Überprüfung mit den konfigurierten Zugriffs Steuerungs Bedingungen und den Identitätsinformationen des Benutzers im TGT aus. Die Zugriffsprüfung ist erfolgreich.

4.  Der Domänencontroller beantwortet die Anforderung mit einer Ticket erteilenden Dienstantwort (TGS-REP).

## <a name="associated-error-and-informational-event-messages"></a><a name="BKMK_ErrorandEvents"></a>Zugehörige Fehler- und Informationsmeldungen
In der folgenden Tabelle werden die Ereignisse, die mit der Sicherheitsgruppe "Geschützte Benutzer" zusammenhängen, und die Authentifizierungsrichtlinien, die für Authentifizierungsrichtliniensilos gelten, beschrieben.

Die Ereignisse werden in den Anwendungs- und Dienstprotokollen unter **Microsoft\Windows\Authentication** verzeichnet.

Informationen zu Problembehandlungsschritten mit diesen Ereignissen finden Sie unter [Problembehandlung von Authentifizierungsrichtlinien](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts#troubleshoot-authentication-policies) und [Problembehandlungen von Ereignissen im Zusammenhang mit geschützten Benutzern](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts#troubleshoot-events-related-to-protected-users).

|Ereignis-ID und Protokoll|BESCHREIBUNG|
|----------|--------|
|101<p>**AuthenticationPolicyFailures-DomainController**|Grund: ein NTLM-Anmeldefehler tritt auf, weil die Authentifizierungs Richtlinie konfiguriert ist.<p>Auf dem Domänencontroller wird ein Ereignis protokolliert, das anzeigt, dass die NTLM-Authentifizierung fehlgeschlagen ist, weil Zugriffssteuerungseinschränkungen erfüllt werden müssen und diese Einschränkungen nicht auf NTLM anwendbar sind.<p>Zeigt den Kontonamen, Gerätenamen, Richtliniennamen und Silonamen an.|
|105<p>**AuthenticationPolicyFailures-DomainController**|Ursache: ein Kerberos-Einschränkungs Fehler tritt auf, weil die Authentifizierung von einem bestimmten Gerät nicht zugelassen wurde.<p>Auf dem Domänencontroller wird ein Ereignis protokolliert, das anzeigt, dass ein Kerberos-TGT verweigert wurde, weil das Gerät nicht die erzwungenen Zugriffssteuerungseinschränkungen erfüllte.<p>Zeigt Kontonamen, Gerätenamen, Richtliniennamen, Silonamen und TGT-Lebensdauer an.|
|305<p>**AuthenticationPolicyFailures-DomainController**|Ursache: Möglicherweise tritt ein potenzieller Kerberos-Einschränkungs Fehler auf, weil die Authentifizierung von einem bestimmten Gerät nicht zugelassen wurde.<p>Im Überwachungsmodus wird auf dem Domänencontroller ein Ereignis protokolliert, das anzeigt, dass ein Kerberos-TGT verweigert wurde, weil das Gerät nicht die erzwungenen Zugriffssteuerungseinschränkungen erfüllt.<p>Zeigt Kontonamen, Gerätenamen, Richtliniennamen, Silonamen und TGT-Lebensdauer an.|
|106<p>**AuthenticationPolicyFailures-DomainController**|Ursache: ein Kerberos-Einschränkungs Fehler tritt auf, weil der Benutzer oder das Gerät nicht für die Authentifizierung beim Server berechtigt war.<p>Auf dem Domänencontroller wird ein Ereignis protokolliert, das anzeigt, dass ein Kerberos-Dienstticket verweigert wurde, weil der Benutzer, das Gerät oder beide nicht die erzwungenen Zugriffssteuerungseinschränkungen erfüllen.<p>Zeigt den Gerätenamen, Richtliniennamen und Silonamen an.|
|306<p>**AuthenticationPolicyFailures-DomainController**|Ursache: Möglicherweise tritt ein Kerberos-Einschränkungs Fehler auf, weil der Benutzer oder das Gerät nicht auf dem Server authentifiziert werden darf.<p>Im Überwachungsmodus wird auf dem Domänencontroller ein Ereignis protokolliert, das anzeigt, dass ein Kerberos-Dienstticket verweigert wurde, weil der Benutzer, das Gerät oder beide nicht die Zugriffssteuerungseinschränkungen erfüllen.<p>Zeigt den Gerätenamen, Richtliniennamen und Silonamen an.|

## <a name="additional-references"></a>Zusätzliche Referenzen
[Konfigurieren geschützter Konten](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts)

[Schutz und Verwaltung von Anmeldeinformationen](credentials-protection-and-management.md)

[Sicherheitsgruppe „Geschützte Benutzer“](protected-users-security-group.md)


