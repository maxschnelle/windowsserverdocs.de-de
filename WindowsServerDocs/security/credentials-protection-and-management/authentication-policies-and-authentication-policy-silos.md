---
title: Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7eb0e640-033d-49b5-ab44-3959395ad567
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 460837c79c0e0d2c48331ddaaffcd118fd16ebc1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870611"
---
# <a name="authentication-policies-and-authentication-policy-silos"></a>Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema für IT-Spezialisten werden Authentifizierungsrichtliniensilos und die Richtlinien beschrieben, mit denen Konten auf diese Silos beschränkt werden können. Zudem wird erklärt, wie der Bereich von Konten mit Authentifizierungsrichtlinien eingeschränkt werden kann.

Authentifizierungsrichtliniensilos und die zugehörigen Richtlinien stellen eine Möglichkeit dar, Anmeldeinformationen mit erhöhten Rechten auf Systeme zu beschränken, die nur für ausgewählte Benutzer, Computer oder Dienste relevant sind. Silos können definiert und in Active Directory Domain Services (AD DS) mit Active Directory-Verwaltungscenter und den Active Directory Windows PowerShell-Cmdlets verwaltet werden.

Authentifizierungsrichtliniensilos sind Container, denen Administratoren Benutzerkonten, Computerkonten und Dienstkonten zuweisen können. Über die Authentifizierungsrichtlinien, die auf diesen Container angewendet werden, können dann Gruppen von Konten verwaltet werden. Daher muss der Administrator nicht mehr im gleichen Umfang wie bisher den Ressourcenzugriff einzelner Konten verfolgen, und es wird verhindert, dass böswillige Benutzer durch den Diebstahl von Anmeldeinformationen Zugriff auf andere Ressourcen erlangen.

In Windows Server 2012 R2 eingeführte Funktionen können Sie Authentifizierung authentifizierungsrichtliniensilos erstellen, die eine Gruppe von Benutzern mit erhöhten Rechten zu hosten. Sie können diesem Container Authentifizierungsrichtlinien zuordnen, um die Verwendung privilegierter Konten in der Domäne zu begrenzen. Wenn Konten zur Sicherheitsgruppe "Geschützte Benutzer" gehören, werden zusätzliche Kontrollmechanismen angewendet, z. B. die exklusive Verwendung des Kerberos-Protokolls.

Damit können Sie die Nutzung hochwertiger Konten auf hochwertige Hosts begrenzen. Beispielsweise könnten Sie ein neues Silo für Administratoren der Gesamtstruktur erstellen, das Unternehmens-, Schema- und Domänenadministratoren enthält. Anschließend könnten Sie das Silo mit einer Authentifizierungsrichtlinie konfigurieren, sodass eine kennwort- und smartcard-basierte Authentifizierung von Systemen, die keine Domänencontroller oder Domänenadministratorkonsolen sind, fehlschlägt.

Informationen zum Konfigurieren von Authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien finden Sie unter [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md).

### <a name="about-authentication-policy-silos"></a>Informationen zu Authentifizierungsrichtliniensilos
Mit einem Authentifizierungsrichtliniensilo wird gesteuert, welche Konten durch das Silo eingeschränkt werden können, und es werden damit die Authentifizierungsrichtlinien definiert, die auf die Mitglieder angewendet werden sollen. Sie können das Silo anhand der Anforderungen Ihrer Organisation erstellen. Silos sind Active Directory-Objekte für Benutzer, Computer und Dienste, die nach dem Schema in der folgenden Tabelle definiert sind.

**Active Directory-Schema für authentifizierungsrichtliniensilos**

|Anzeigename|Beschreibung|
|--------|--------|
|Authentifizierungsrichtliniensilo|Eine Instanz dieser Klasse definiert die Authentifizierungsrichtlinien und das zugehörige Verhalten für die zugewiesenen Benutzer, Computer und Dienste.|
|Authentifizierungsrichtliniensilos|Ein Container dieser Klasse kann Authentifizierungsrichtliniensilo-Objekte enthalten.|
|Authentication Policy Silo Enforced (Authentifizierungsrichtliniensilo erzwungen)|Gibt an, ob das Authentifizierungsrichtliniensilo erzwungen wird.<br /><br />Wenn es nicht erzwungen wird, dann ist für die Richtlinie standardmäßig der Überwachungsmodus aktiviert. Es werden Ereignisse generiert, die potenzielle Erfolge und Fehler anzeigen, aber es werden keine Schutzmaßnahmen auf das System angewendet.|
|Assigned Authentication Policy Silo Backlink (Rückverweis für zugewiesenes Authentifizierungsrichtliniensilo)|Dieses Attribut ist der Rückverweis für msDS-AssignedAuthNPolicySilo.|
|Authentication Policy Silo Members (Authentifizierungsrichtliniensilo-Mitglieder)|Gibt an, welche Prinzipale dem AuthNPolicySilo-Objekt zugewiesen sind.|
|Authentication Policy Silo Members Backlink (Rückverweis für Authentifizierungsrichtliniensilo-Mitglieder)|Dieses Attribut ist der Rückverweis für msDS-AuthNPolicySiloMembers.|

Authentifizierungsrichtliniensilos können mit der Active Directory-Verwaltungskonsole oder Windows PowerShell konfiguriert werden. Weitere Informationen finden Sie unter [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md).

### <a name="about-authentication-policies"></a>Informationen zu Authentifizierungsrichtlinien
Authentifizierungsrichtlinien definieren die Lebensdauereigenschaften des Ticket-Granting Ticket (TGT) für das Kerberos-Protokoll und die Bedingungen für die Authentifizierungszugriffssteuerung für einen Kontotyp. Die Richtlinie basiert auf und steuert den AD DS-Container als das authentifizierungsrichtliniensilo bezeichnet.

Über Authentifizierungsrichtlinien wird Folgendes gesteuert:

-   Die TGT-Lebensdauer des Kontos, das als nicht erneuerbar konfiguriert wurde.

-   Die Kriterien, die Gerätekonten erfüllen müssen, um sich mit einem Kennwort oder einem Zertifikat anmelden zu können.

-   Die Kriterien, die Benutzer und Geräte erfüllen müssen, um sich gegenüber Diensten authentifizieren zu können, die unter dem Konto ausgeführt werden.

Der Active Directory-Kontotyp bestimmt die Rolle des Aufrufers als eine der folgenden:

-   **User**

    Benutzer sollten immer Mitglied der Sicherheitsgruppe "Geschützte Benutzer" sein, die Authentifizierungsversuche über NTLM standardmäßig nicht zulässt.

    Richtlinien können konfiguriert werden, um die TGT-Lebensdauer eines Benutzerkontos auf einen kürzeren Wert festgelegt oder beschränken die Geräte, an denen ein Benutzerkonto anmelden kann. Rich-Ausdrücke können konfiguriert werden, in der Authentifizierungsrichtlinie, die Kriterien zu steuern, die die Benutzer und Geräte erfüllen, um den Dienst zu authentifizieren müssen.

    Weitere Informationen finden Sie unter [Sicherheitsgruppe "Geschützte Benutzer"](protected-users-security-group.md).

-   **Service**

    Eigenständige verwaltete Dienstkonten, gruppenverwalteten Dienstkonten oder ein benutzerdefiniertes Kontoobjekt, das von diesen beiden Dienstkontotypen abgeleitet ist, werden verwendet. Richtlinien können Zugriffsstatus eines Geräts zugriffssteuerungsbedingungen festgelegt, die verwendet werden, um Anmeldeinformationen für das verwaltete Dienstkonto auf bestimmte Geräte mit einer Active Directory-Identität zu beschränken. Dienste sollten nie Mitglied der Sicherheitsgruppe "Geschützte Benutzer" sein, weil sonst alle eingehenden Authentifizierungsversuche fehlschlagen.

-   **Computer**

    Verwendet wird das Computerkontoobjekt oder das benutzerdefinierte Kontoobjekt, das vom Computerkontoobjekt abgeleitet wurde. Durch Richtlinien können die Zugriffssteuerungsbedingungen festgelegt werden, die erfüllt sein müssen, um eine Authentifizierung anhand der Benutzer- oder Geräteeigenschaften gegenüber dem Konto zuzulassen. Computer sollten nie Mitglied der Sicherheitsgruppe "Geschützte Benutzer" sein, weil sonst alle eingehenden Authentifizierungsversuche fehlschlagen. Standardmäßig werden NTML-Authentifizierungsversuche abgelehnt. Für Computerkonten sollte keine TGT-Lebensdauer konfiguriert werden.

> [!NOTE]
> Es ist möglich, eine Authentifizierungsrichtlinie für eine Gruppe von Konten festzulegen, ohne die Richtlinie mit einem Authentifizierungsrichtliniensilo zu verknüpfen. Sie können diese Strategie verwenden, wenn nur ein einzelnes Konto geschützt werden muss.

**Active Directory-Schema für Authentifizierungsrichtlinien**

Die Richtlinien für die Active Directory-Objekte für Benutzer, Computer und Dienste werden nach dem Schema in der folgenden Tabelle definiert.

|Typ|Anzeigename|Beschreibung|
|----|--------|--------|
|Richtlinie|Authentifizierungsrichtlinie|Eine Instanz dieser Klasse definiert Authentifizierungsrichtlinienverhalten für die zugewiesenen Prinzipale.|
|Richtlinie|Authentifizierungsrichtlinien|Ein Container dieser Klasse kann Authentifizierungsrichtlinien-Objekte enthalten.|
|Richtlinie|Authentication Policy Enforced (Authentifizierungsrichtlinien erzwungen)|Gibt an, ob die Authentifizierungsrichtlinie erzwungen wird.<br /><br />Wenn sie nicht erzwungen wird, dann ist für die Richtlinie standardmäßig der Überwachungsmodus aktiviert, und es werden Ereignisse zum Anzeigen potenzieller Erfolge oder Fehler generiert, aber keine Schutzmaßnahmen auf das System angewendet.|
|Richtlinie|Assigned Authentication Policy Backlink (Rückverweis für zugewiesene Authentifizierungsrichtlinie)|Dieses Attribut ist der Rückverweis für msDS-AssignedAuthNPolicy.|
|Richtlinie|Assigned Authentication Policy (Zugewiesene Authentifizierungsrichtlinie)|Gibt an, welches AuthNPolicy-Objekt auf diesen Prinzipal angewendet werden soll.|
|Benutzer|User Authentication Policy (Benutzerauthentifizierungsrichtlinie)|Gibt an, welches AuthNPolicy-Objekt auf die Benutzer, die diesem Siloobjekt zugewiesen wurden, angewendet werden soll.|
|Benutzer|User Authentication Policy Backlink (Rückverweis für Benutzerauthentifizierungsrichtlinie)|Dieses Attribut ist der Rückverweis für msDS-UserAuthNPolicy.|
|Benutzer|ms-DS-User-Allowed-To-Authenticate-To|Mit diesem Attribut wird bestimmt, welcher Gruppe von Prinzipalen erlaubt wird, sich gegenüber einem Dienst, der unter dem Benutzerkonto ausgeführt wird, zu authentifizieren.|
|Benutzer|ms-DS-User-Allowed-To-Authenticate-From|Mit diesem Attribut wird die Gruppe von Geräten festgelegt, für die ein Benutzerkonto Anmeldeberechtigungen besitzt.|
|Benutzer|User TGT Lifetime (Benutzer-TGT-Lebensdauer)|Legt das maximale Alter (in Sekunden) eines Kerberos-TGT fest, das für einen Benutzer ausgestellt wird. Die resultierenden TGTs sind nicht erneuerbar.|
|Computer|Computer Authentication Policy (Computerauthentifizierungsrichtlinie)|Gibt an, welches AuthNPolicy-Objekt auf die Computer, die diesem Siloobjekt zugewiesen wurden, angewendet werden soll.|
|Computer|Computer Authentication Policy Backlink (Rückverweis für Computerauthentifizierungsrichtlinie)|Dieses Attribut ist der Rückverweis für msDS-ComputerAuthNPolicy.|
|Computer|ms-DS-Computer-Allowed-To-Authenticate-To|Mit diesem Attribut wird bestimmt, welcher Gruppe von Prinzipalen erlaubt wird, sich gegenüber einem Dienst, der unter dem Computerkonto ausgeführt wird, zu authentifizieren.|
|Computer|Computer TGT Lifetime (Computer-TGT-Lebensdauer)|Legt das maximale Alter (in Sekunden) eines Kerberos-TGT fest, das für einen Computer ausgestellt wird. Von der Änderung dieser Einstellung wird abgeraten.|
|Service|Service Authentication Policy (Dienstauthentifizierungsrichtlinie)|Gibt an, welches AuthNPolicy-Objekt auf die Dienste, die diesem Siloobjekt zugewiesen wurden, angewendet werden soll.|
|Service|Service Authentication Policy Backlink (Rückverweis für Dienstauthentifizierungsrichtlinie)|Dieses Attribut ist der Rückverweis für msDS-ServiceAuthNPolicy.|
|Service|ms-DS-Service-Allowed-To-Authenticate-To|Mit diesem Attribut wird bestimmt, welcher Gruppe von Prinzipalen erlaubt wird, sich gegenüber einem Dienst, der unter dem Dienstkonto ausgeführt wird, zu authentifizieren.|
|Service|ms-DS-Service-Allowed-To-Authenticate-From|Mit diesem Attribut wird die Gruppe von Geräten festgelegt, für die ein Dienstkonto Anmeldeberechtigungen besitzt.|
|Service|Service TGT Lifetime (Dienst-TGT-Lebensdauer)|Legt das maximale Alter (in Sekunden) eines Kerberos-TGT fest, das für einen Dienst ausgestellt wird.|

Authentifizierungsrichtlinien können mit der Active Directory-Verwaltungskonsole oder Windows PowerShell für jedes Silo konfiguriert werden. Weitere Informationen finden Sie unter [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md).

## <a name="how-it-works"></a>Funktionsweise
In diesem Abschnitt wird die Funktionsweise von Authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien in Verbindung mit der Sicherheitsgruppe "Geschützte Benutzer" und die Implementierung des Kerberos-Protokolls in Windows beschrieben.

-   [Wie die Kerberos-Protokolls mit authentifizierungssilos und-Richtlinien verwendet wird](#BKMK_HowKerbUsed)

-   [Einschränken einer Benutzeranmeldung funktioniert](#BKMK_HowRestrictingSignOn)

-   [Funktionsweise von Einschränken der Dienstticket-Ausstellung](#BKMK_HowRestrictingServiceTicket)

**geschützte Konten**

Die Sicherheitsgruppe der geschützten Benutzer löst nicht konfigurierbaren Schutz auf Geräten und Hostcomputern, die unter Windows Server 2012 R2 und Windows 8.1, und klicken Sie auf Domänencontrollern in Domänen mit einem primären Domänencontroller mit Windows Server 2012 R2. Abhängig von der Domänenfunktionsebene des Kontos sind die Mitglieder der Sicherheitsgruppe "Geschützte Benutzer" aufgrund der Änderungen der Authentifizierungsmethoden, die in Windows unterstützt werden, zusätzlich geschützt.

-   Mitglieder der Sicherheitsgruppe "Geschützte Benutzer" können sich nicht unter Verwendung von NTLM, Digestauthentifizierung oder der Delegierung der Standardanmeldeinformationen mit CredSSP authentifizieren. Auf einem Gerät, die mit Windows 8.1, die keines dieser Security Support Provider (SSP) verwendet wird, schlägt die Authentifizierung zu einer Domäne fehl, wenn das Konto ein Mitglied der Sicherheitsgruppe der geschützten Benutzer ist.

-   Das Kerberos-Protokoll verwendet die schwächeren Verschlüsselungstypen DES oder RC4 nicht im Vorauthentifizierungsprozess. Daher muss die Domäne so konfiguriert werden, dass mindestens der Verschlüsselungstyp AES unterstützt wird.

-   Das Konto des Benutzers kann nicht delegiert werden, mit eingeschränkten und uneingeschränkten Kerberos Delegierung. Das bedeutet, dass frühere Verbindungen mit anderen Systemen fehlschlagen, wenn der Benutzer Mitglied der Sicherheitsgruppe "Geschützte Benutzer" ist.

-   Die Standardeinstellung für die Lebensdauer von Kerberos-TGTs von vier Stunden kann mit Authentifizierungsrichtlinien und -silos konfiguriert werden, auf die über das Active Directory-Verwaltungscenter zugegriffen werden kann. Das heißt, dass sich der Benutzer nach Ablauf von vier Stunden erneut authentifizieren muss.

Weitere Informationen zu dieser Sicherheitsgruppe finden Sie unter [Funktionsweise der Gruppe "Geschützte Benutzer"](protected-users-security-group.md#BKMK_HowItWorks).

**Silos und Authentifizierungsrichtlinien**

Authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien nutzen die vorhandene Windows-Authentifizierungsinfrastruktur. Die Verwendung des NTLM-Protokolls wird abgelehnt, und das Kerberos-Protokoll wird mit neueren Verschlüsselungstypen verwendet. Authentifizierungsrichtlinien ergänzen die Sicherheitsgruppe "Geschützte Benutzer" durch die Möglichkeit, konfigurierbare Einschränkungen auf Konten anzuwenden, sowie durch die Bereitstellung von Einschränkungen für Dienst- und Computerkonten. Authentifizierungsrichtlinien werden während des Austauschs des Authentifizierungsdiensts (Authentication Service, AS) und des Ticket-Granting Service (TGS) des Kerberos-Protokolls erzwungen. Weitere Informationen dazu, wie Windows das Kerberos-Protokoll verwendet und welche Änderungen zur Unterstützung von Authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien vorgenommen wurden, finden Sie unter:

-   [Wie funktioniert das Authentifizierungsprotokoll von Kerberos Version 5](https://technet.microsoft.com/library/cc772815(v=ws.10).aspx)

-   [Änderungen bei der Kerberosauthentifizierung](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) (Windows Server 2008 R2 und Windows 7)

### <a name="BKMK_HowKerbUsed"></a>Verwendung des Kerberos-Protokolls mit authentifizierungsrichtliniensilos und-Richtlinien
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

Wenn eine Authentifizierungsrichtlinie aktiviert, im Überwachungsmodus ist und eine Ticket-granting-dienstanforderung für ein Domänenkonto ein Domänencontroller empfangen wird, prüft der Domänencontroller auf, wenn die Authentifizierung anhand des anforderungstickets Berechtigungen Attribut Zertifikat zugelassen wird (PAC) Daten und protokolliert eine Warnmeldung, wenn ein Fehler auftritt. Das PAC enthält verschiedene Arten von Autorisierungsdaten, darunter die Gruppen, denen der Benutzer als Mitglied angehört, die Rechte des Benutzers und die Richtlinien, die für den Benutzer gelten. Diese Informationen werden verwendet, um das Zugriffstoken des Benutzers zu generieren. Ist dies eine erzwungene Authentifizierungsrichtlinie die Authentifizierung für einen Benutzer, Gerät oder Dienst ermöglicht, anhand des anforderungstickets PAC-Daten der Domain Controller wird überprüft, ob die Authentifizierung zulässig ist. Wenn ein Fehler auftritt, gibt der Domänencontroller eine Fehlermeldung zurück und protokolliert ein Ereignis.

> [!NOTE]
> Das Domänenkonto muss entweder direkt oder indirekt über die Silomitgliedschaft mit einer überwachten Richtlinie verknüpft werden, welche die Authentifizierung eines Benutzers, Geräts oder Diensts zulässt.

Sie können eine Authentifizierungsrichtlinie für alle Mitglieder eines Silos oder getrennte Richtlinien für Benutzer, Computer und verwaltete Dienstkonten verwenden.

Authentifizierungsrichtlinien können mit der Active Directory-Verwaltungskonsole oder Windows PowerShell für jedes Silo konfiguriert werden. Weitere Informationen finden Sie unter [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md).

### <a name="BKMK_HowRestrictingSignOn"></a>Einschränken einer Benutzeranmeldung funktioniert
Weil diese Authentifizierungsrichtlinien auf ein Konto angewendet werden, gelten sie auch für Konten, die von Diensten verwendet werden. Wenn Sie die Verwendung eines Kennworts für einen Dienst auf bestimmte Hosts beschränken möchten, ist diese Einstellung hilfreich. Beispielsweise werden gruppenverwaltete Dienstkonten so konfiguriert, dass die Hosts das Kennwort von den Active Directory-Domänendiensten abrufen können. Allerdings kann dieses Kennwort auf jedem Host zur anfänglichen Authentifizierung verwendet werden. Durch die Anwendung einer Zugriffssteuerungsbedingung kann eine zusätzliche Schutzebene eingeführt werden, indem das Kennwort nur auf die Gruppe von Hosts begrenzt wird, welche das Kennwort abrufen können.

Wenn Dienste, die als System, Netzwerkdienst oder andere lokale Dienstidentität ausgeführt auf Netzwerkdienste verbinden möchten, verwenden sie Computerkonto des Hosts. Computerkonten können nicht beschränkt werden. Selbst wenn der Dienst ein Computerkonto verwendet, das nicht für einen Windows-Host vorgesehen ist, kann dieses nicht eingeschränkt werden.

Einschränken der Benutzeranmeldung auf bestimmte Hosts erfordert den Domänencontroller, um die Identität des Hosts zu überprüfen. Bei Verwendung der Kerberos-Authentifizierung mit Kerberos Amoring (die Bestandteil der dynamischen Zugriffssteuerung ist), dann wird das Schlüsselverteilungscenter mit dem TGT des Hosts bereitgestellt, von dem der Benutzer authentifiziert wird. Der Inhalt dieses geschützten TGT wird zur Durchführung einer Zugriffsprüfung verwendet, mit der bestimmt wird, ob der Host zulässig ist.

Wenn sich der Benutzer bei Windows anmeldet oder seine Domänenanmeldeinformationen in eine Eingabeaufforderung für die Anmeldung bei einer Anwendung eingibt, dann sendet Windows standardmäßig eine ungeschützte Authentifizierungsdienstanforderung (AS-REQ) an den Domänencontroller. Wenn der Benutzer die Anforderung von einem Computer sendet, die nicht unterstützt, z. B. Computer mit Windows 7 oder Windows Vista armoring die Anforderung schlägt fehl.

In der folgenden Liste wird der Prozess beschrieben:

-   Der Domänencontroller in einer Domäne mit Windows Server 2012 R2-Abfragen für das Benutzerkonto und bestimmt, ob er mit einer Authentifizierungsrichtlinie konfiguriert ist, die anfängliche Authentifizierung beschränkt, die geschützten Anforderungen erforderlich sind.

-   Der Domänencontroller kann die Anforderung nicht erfüllen.

-   Da Kerberos armoring erforderlich ist, kann der Benutzer zur Anmeldung mit einem Computer unter Windows 8.1 oder Windows 8, das aktiviert wird, um die Kerberos armoring unterstützt, um die Anmeldung erneut versuchen.

-   Windows erkennt, dass die Domäne Kerberos Armoring unterstützt, und sendet eine geschützte AS-REQ, um die Anmeldungsanforderung zu wiederholen.

-   Der Domänencontroller führt eine zugriffsprüfung mit den konfigurierten zugriffssteuerungsbedingungen und Identitätsinformationen für die Client-Betriebssystem in das TGT fest, das zur Abschirmung der Anforderung verwendet wurde.

-   Wenn die Zugriffsprüfung fehlschlägt, lehnt der Domänencontroller die Anforderung ab.

Selbst wenn das Betriebssystem Kerberos Armoring unterstützt, können Zugriffssteuerungsanforderungen angewendet werden, die erfüllt sein müssen, bevor der Zugriff gewährt wird. Die Benutzer melden sich bei Windows an oder geben ihre Domänenanmeldeinformationen in eine Eingabeaufforderung für die Anmeldung bei einer Anwendung ein. Standardmäßig sendet Windows eine ungeschützte AS-REQ an den Domänencontroller. Wenn der Benutzer die Anforderung von einem Computer, die Kerberos armoring sendet, z. B. Windows 8.1 oder Windows 8 unterstützt werden die Authentifizierungsrichtlinien wie folgt ausgewertet:

1.  Der Domänencontroller in einer Domäne mit Windows Server 2012 R2-Abfragen für das Benutzerkonto und bestimmt, ob er mit einer Authentifizierungsrichtlinie konfiguriert ist, die anfängliche Authentifizierung beschränkt, die geschützten Anforderungen erforderlich sind.

2.  Der Domänencontroller führt eine zugriffsprüfung mit den konfigurierten zugriffssteuerungsbedingungen und den Identitätsinformationen des Systems in der TGT fest, das zur Abschirmung der Anforderung verwendet wird. Die Zugriffsprüfung ist erfolgreich.

    > [!NOTE]
    > Wenn ältere Arbeitsgruppeneinschränkungen konfiguriert wurden, müssen auch diese erfüllt werden.

3.  Der Domänencontroller antwortet mit einer geschützten Antwort (AS-REP), und die Authentifizierung wird fortgesetzt.

### <a name="BKMK_HowRestrictingServiceTicket"></a>Funktionsweise von Einschränken der Dienstticket-Ausstellung
Wenn ein Konto ist nicht zulässig und ein Benutzer, der ein TGT besitzt, mit dem Dienst herzustellen versucht (z. B. durch Öffnen einer Anwendung, die Authentifizierungsanforderung an einen Dienst, der durch den Dienst für Dienstprinzipalnamen (SPN) identifiziert wird, dann geschieht Folgendes:

1.  Bei einem Versuch, von SPN eine Verbindung mit SPN1 herzustellen, sendet Windows eine TGS-REQ an den Domänencontroller, der ein Dienstticket für SPN1 anfordert.

2.  Der Domänencontroller in einer Domäne mit Windows Server 2012 R2 schlägt spn1 nach Active Directory Domain Services-Konto für den Dienst zu finden und feststellt, dass das Konto mit einer Authentifizierungsrichtlinie konfiguriert wurde, die Ausstellung von Diensttickets beschränkt.

3.  Der Domänencontroller führt eine zugriffsprüfung mit den konfigurierten zugriffssteuerungsbedingungen und den Identitätsinformationen des Benutzers im TGT enthalten sind. Die Zugriffsprüfung schlägt fehl.

4.  Der Domänencontroller weist die Anforderung zurück.

Wenn ein Konto zulässig ist, da das Konto erfüllt die Bedingungen für die Zugriffssteuerung, die durch die Authentifizierungsrichtlinie festgelegt werden, und ein Benutzer, der ein TGT besitzt, mit dem Dienst herzustellen versucht (z. B. durch Öffnen einer Anwendung, die Authentifizierung bei einem Dienst erfordert, gekennzeichnet durch der SPN des Diensts), dann geschieht Folgendes:

1.  Bei einem Versuch, eine Verbindung mit SPN1 herzustellen, sendet Windows eine TGS-REQ an den Domänencontroller, der ein Dienstticket für SPN1 anfordert.

2.  Der Domänencontroller in einer Domäne mit Windows Server 2012 R2 schlägt spn1 nach Active Directory Domain Services-Konto für den Dienst zu finden und feststellt, dass das Konto mit einer Authentifizierungsrichtlinie konfiguriert wurde, die Ausstellung von Diensttickets beschränkt.

3.  Der Domänencontroller führt eine zugriffsprüfung mit den konfigurierten zugriffssteuerungsbedingungen und den Identitätsinformationen des Benutzers im TGT enthalten sind. Die Zugriffsprüfung ist erfolgreich.

4.  Der Domänencontroller beantwortet die Anforderung mit einer Ticket erteilenden Dienstantwort (TGS-REP).

## <a name="BKMK_ErrorandEvents"></a>Zugehörige Fehler- und informationsmeldungen
In der folgenden Tabelle werden die Ereignisse, die mit der Sicherheitsgruppe "Geschützte Benutzer" zusammenhängen, und die Authentifizierungsrichtlinien, die für Authentifizierungsrichtliniensilos gelten, beschrieben.

Die Ereignisse werden in den Anwendungs- und Dienstprotokollen unter **Microsoft\Windows\Authentication** verzeichnet.

Informationen zu Problembehandlungsschritten mit diesen Ereignissen finden Sie unter [Problembehandlung von Authentifizierungsrichtlinien](how-to-configure-protected-accounts.md#BKMK_TroubleshootAuthnPolicies) und [Problembehandlungen von Ereignissen im Zusammenhang mit geschützten Benutzern](how-to-configure-protected-accounts.md#BKMK_TrubleshootingEvents).

|Ereignis-ID und Protokoll|Beschreibung|
|----------|--------|
|101<br /><br />**AuthenticationPolicyFailures-DomainController**|Grund: Es tritt ein NTLM-Anmeldefehler auf, weil die Authentifizierungsrichtlinie konfiguriert ist.<br /><br />Auf dem Domänencontroller wird ein Ereignis protokolliert, das anzeigt, dass die NTLM-Authentifizierung fehlgeschlagen ist, weil Zugriffssteuerungseinschränkungen erfüllt werden müssen und diese Einschränkungen nicht auf NTLM anwendbar sind.<br /><br />Zeigt den Kontonamen, Gerätenamen, Richtliniennamen und Silonamen an.|
|105<br /><br />**AuthenticationPolicyFailures-DomainController**|Grund: Es tritt ein Kerberos-Einschränkungsfehler auf, weil die Authentifizierung von einem bestimmten Gerät nicht zugelassen wurde.<br /><br />Auf dem Domänencontroller wird ein Ereignis protokolliert, das anzeigt, dass ein Kerberos-TGT verweigert wurde, weil das Gerät nicht die erzwungenen Zugriffssteuerungseinschränkungen erfüllte.<br /><br />Zeigt Kontonamen, Gerätenamen, Richtliniennamen, Silonamen und TGT-Lebensdauer an.|
|305<br /><br />**AuthenticationPolicyFailures-DomainController**|Grund: Es tritt möglicherweise ein potenzieller Kerberos-Einschränkungsfehler auf, weil die Authentifizierung von einem bestimmten Gerät nicht zugelassen wurde.<br /><br />Im Überwachungsmodus wird auf dem Domänencontroller ein Ereignis protokolliert, das anzeigt, dass ein Kerberos-TGT verweigert wurde, weil das Gerät nicht die erzwungenen Zugriffssteuerungseinschränkungen erfüllt.<br /><br />Zeigt Kontonamen, Gerätenamen, Richtliniennamen, Silonamen und TGT-Lebensdauer an.|
|106<br /><br />**AuthenticationPolicyFailures-DomainController**|Grund: Es tritt ein Kerberos-Einschränkungsfehler auf, weil der Benutzer oder das Gerät sich nicht gegenüber dem Server authentifizieren durfte.<br /><br />Auf dem Domänencontroller wird ein Ereignis protokolliert, das anzeigt, dass ein Kerberos-Dienstticket verweigert wurde, weil der Benutzer, das Gerät oder beide nicht die erzwungenen Zugriffssteuerungseinschränkungen erfüllen.<br /><br />Zeigt den Gerätenamen, Richtliniennamen und Silonamen an.|
|306<br /><br />**AuthenticationPolicyFailures-DomainController**|Grund: Möglicherweise tritt ein Kerberos-Einschränkungsfehler auf, weil der Benutzer oder das Gerät sich nicht gegenüber dem Server authentifizieren durfte.<br /><br />Im Überwachungsmodus wird auf dem Domänencontroller ein Ereignis protokolliert, das anzeigt, dass ein Kerberos-Dienstticket verweigert wurde, weil der Benutzer, das Gerät oder beide nicht die Zugriffssteuerungseinschränkungen erfüllen.<br /><br />Zeigt den Gerätenamen, Richtliniennamen und Silonamen an.|

## <a name="see-also"></a>Siehe auch
[Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md)

[Schutz und Verwaltung von Anmeldeinformationen](credentials-protection-and-management.md)

[Sicherheitsgruppe "geschützte Benutzer"](protected-users-security-group.md)


