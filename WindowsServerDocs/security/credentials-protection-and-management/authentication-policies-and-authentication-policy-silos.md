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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="authentication-policies-and-authentication-policy-silos"></a>Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten beschreibt die authentifizierungsrichtliniensilos und die Richtlinien, die Konten auf diese Silos beschränkt werden können. Es wird erläutert, wie Authentifizierungsrichtlinien verwendet werden können, um den Bereich von Konten zu beschränken.

Authentifizierungsrichtliniensilos und die zugehörigen Richtlinien bieten eine Möglichkeit, Anmeldeinformationen mit umfassenden rechten Systeme enthalten, die nur für ausgewählte Benutzer, Computer oder Dienste relevant sind. Silos können definiert und in Active Directory-Domänendienste (AD DS) mithilfe der Active Directory-Verwaltungscenter und Active Directory Windows PowerShell-Cmdlets verwaltet werden.

Authentifizierungsrichtliniensilos sind Container, die Administratoren Benutzerkonten, Computerkonten und Dienstkonten zuweisen können. Gruppen von Konten können dann über die Authentifizierungsrichtlinien verwaltet werden, die auf diesen Container angewendet wurden. Dies reduziert die Notwendigkeit der Administrator den Zugriff auf Ressourcen für einzelne Konten verfolgen und verhindert, dass böswillige Benutzer Zugriff auf andere Ressourcen durch den Diebstahl von Anmeldeinformationen.

In Windows Server 2012 R2 eingeführte Funktionen ermöglichen die Authentifizierung authentifizierungsrichtliniensilos erstellen, die eine Gruppe von Benutzern mit umfassenden Rechten zu hosten. Sie können dann Authentifizierungsrichtlinien für diesen Container Limit zuweisen, privilegierte Konten in der Domäne verwendet werden können. Konten in der Sicherheitsgruppe der geschützten Benutzer sind, werden zusätzliche Steuerelemente, z. B. die exklusive Verwendung des Kerberos-Protokolls angewendet.

Mit diesen Funktionen können Sie die Verwendung von hochwertiger Konten auf hochwertige Hosts begrenzen. Sie könnten z. B. einem Silo für Administratoren der neuen Gesamtstruktur erstellen, Enterprise, Schema und Domänenadministratoren enthält. Sie können dann das Silo mit einer Authentifizierungsrichtlinie konfigurieren, sodass Kennwort- und Smartcard-basierte Authentifizierung von Systemen, die keine Domänencontroller oder domänenadministratorkonsolen sind, fehlschlägt.

Informationen zum Konfigurieren von authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien finden Sie unter [How to Configure Protected Accounts](how-to-configure-protected-accounts.md).

### <a name="about-authentication-policy-silos"></a>Informationen zu authentifizierungsrichtliniensilos
Authentifizierungsrichtliniensilos steuert, welche Konten durch das Silo eingeschränkt werden können und definiert die Authentifizierungsrichtlinien, die Mitglieder angewendet. Sie können das Silo anhand der Anforderungen Ihrer Organisation erstellen. Silos sind Active Directory-Objekte für Benutzer, Computer und Dienste, die nach dem Schema in der folgenden Tabelle definiert.

**Active Directory-Schema für authentifizierungsrichtliniensilos**

|Anzeigename|Beschreibung|
|--------|--------|
|Authentifizierungsrichtliniensilo|Eine Instanz dieser Klasse definiert die Authentifizierungsrichtlinien und das zugehörige Verhalten für die zugewiesenen Benutzer, Computer und Dienste.|
|Authentifizierungsrichtliniensilos|Ein Container dieser Klasse kann authentifizierungsrichtliniensilo-Objekte enthalten.|
|Authentifizierungsrichtliniensilo erzwungen|Gibt an, ob das authentifizierungsrichtliniensilo erzwungen wird.<br /><br />Wenn Sie nicht erzwungen wird, ist die Richtlinie standardmäßig im Überwachungsmodus. Ereignisse, die potenzielle Erfolge und Fehler generiert, aber Schutzmaßnahmen nicht auf das System angewendet.|
|Assigned Authentication Policy Silo Rückverweis|Dieses Attribut ist der Rückverweis für MsDS-AssignedAuthNPolicySilo.|
|Authentication Policy Silo Mitglieder|Gibt an, welche Prinzipale dem authnpolicysilo-Objekt zugewiesen sind.|
|Authentication Policy Silo Mitglieder Rückverweis|Dieses Attribut ist der Rückverweis für MsDS-AuthNPolicySiloMembers.|

Authentifizierungsrichtliniensilos können mithilfe der Active Directory-Verwaltungskonsole oder Windows PowerShell konfiguriert werden. Weitere Informationen finden Sie unter [How to Configure Protected Accounts](how-to-configure-protected-accounts.md).

### <a name="about-authentication-policies"></a>Informationen zu Authentifizierungsrichtlinien
Authentifizierungsrichtlinien definieren die Kerberos-Ticket-granting Ticket (TGT) Lebensdauer Protokolleigenschaften und die Bedingungen für die authentifizierungszugriffssteuerung für einen Kontotyp. Die Richtlinie basiert auf und steuert den AD DS-Container als das authentifizierungsrichtliniensilo bezeichnet.

Authentifizierungsrichtlinien wird Folgendes gesteuert:

-   Die TGT-Lebensdauer für das Konto, die auf nicht erneuerbar.

-   Die Kriterien, die gerätekonten erfüllen, um sich mit einem Kennwort oder ein Zertifikat anmelden müssen.

-   Die Kriterien, die Benutzer und Geräte erfüllen, um Dienste im Rahmen des Kontos zu authentifizieren müssen.

Der Active Directory-Kontotyp legt die Rolle des Aufrufers als eine der folgenden:

-   **Benutzer**

    Benutzer sollten immer Mitglied der Sicherheitsgruppe der geschützten Benutzer sein, die standardmäßig Authentifizierungsversuche über NTLM abgelehnt.

    Richtlinien können so konfiguriert werden, um die TGT-Lebensdauer eines Benutzerkontos auf einen kürzeren Wert festgelegt oder beschränken die Geräte, für die ein Benutzerkonto anmelden kann. Umfangreiche Ausdrücke können konfiguriert werden, in der Authentifizierungsrichtlinie, die Kriterien zu steuern, die der Benutzer und Geräte erfüllen, um den Dienst zu authentifizieren müssen.

    Weitere Informationen finden Sie unter [Protected Users Security Group](protected-users-security-group.md).

-   **Dienst**

    Eigenständige verwaltete Dienstkonten, gruppenverwalteten Dienstkonten oder ein benutzerdefiniertes Kontoobjekt, das aus diesen beiden Dienstkontotypen abgeleitet ist, werden verwendet. Richtlinien können ein Gerät zugriffssteuerungsbedingungen festgelegt werden verwendet, um die Anmeldeinformationen für verwaltete Dienstkonten auf bestimmte Geräte mit einer Active Directory-Identität zu beschränken. Dienste sollten nie Mitglied der Sicherheitsgruppe "geschützte Benutzer" sein, weil sonst alle eingehenden Authentifizierungsversuche fehlschlagen.

-   **Computer**

    Das Computerkontoobjekt oder das benutzerdefinierte Kontoobjekt, das das Computerkontoobjekt abgeleitet ist, wird verwendet. Richtlinien können die zugriffssteuerungsbedingungen festgelegt, die erforderlich sind, die dem Konto basierend auf Eigenschaften und Benutzer-Authentifizierung ermöglicht. Computer sollten nie Mitglied der Sicherheitsgruppe "geschützte Benutzer" sein, weil sonst alle eingehenden Authentifizierungsversuche fehlschlagen. Standardmäßig werden versucht, NTLM-Authentifizierung abgelehnt. Eine TGT-Lebensdauer sollte nicht für Computerkonten konfiguriert werden.

> [!NOTE]
> Es ist möglich, eine Authentifizierungsrichtlinie auf eine Gruppe von Konten festzulegen, ohne die Richtlinie zu einem authentifizierungsrichtliniensilo zu verknüpfen. Sie können diese Strategie verwenden, wenn Sie ein einzelnes Konto geschützt haben.

**Active Directory-Schema für Authentifizierungsrichtlinien**

Die Richtlinien für die Active Directory-Objekte für Benutzer, Computer und Dienste werden durch das Schema in der folgenden Tabelle definiert.

|Typ|Anzeigename|Beschreibung|
|----|--------|--------|
|Richtlinie|Authentifizierungsrichtlinie|Eine Instanz dieser Klasse definiert authentifizierungsrichtlinienverhalten für die zugewiesenen Prinzipale.|
|Richtlinie|Authentifizierungsrichtlinien|Ein Container dieser Klasse kann Authentifizierungsrichtlinien-Objekte enthalten.|
|Richtlinie|Authentifizierungsrichtlinie erzwungen|Gibt an, ob die Authentifizierungsrichtlinie erzwungen wird.<br /><br />Wenn nicht erzwungen wird, wird die Richtlinie standardmäßig im Überwachungsmodus und Ereignisse, die potenzielle Erfolge und Fehler generiert, aber Schutzmaßnahmen nicht auf das System angewendet.|
|Richtlinie|Assigned Authentication Policy Rückverweis|Dieses Attribut ist der Rückverweis für MsDS-AssignedAuthNPolicy.|
|Richtlinie|Assigned Authentication Policy|Gibt an, welches authnpolicy-Objekt ist auf diesen Prinzipal angewendet.|
|Benutzer|Authentifizierungsrichtlinie für Benutzer|Gibt an, welches authnpolicy-Objekt ist für Benutzer, die diesem siloobjekt zugewiesen wurden angewendet.|
|Benutzer|User Authentication Policy Rückverweis|Dieses Attribut ist der Rückverweis für MsDS-UserAuthNPolicy.|
|Benutzer|ms-DS-User-Allowed-To-Authenticate-To|Dieses Attribut wird verwendet, um die Gruppe von Prinzipalen erlaubt wird mit einem Dienst unter dem Benutzerkonto ausgeführt wird, authentifizieren.|
|Benutzer|ms-DS-User-Allowed-To-Authenticate-From|Dieses Attribut wird verwendet, um die Geräte zu bestimmen, die ein Benutzerkonto Anmeldeberechtigungen verfügt.|
|Benutzer|Benutzer-TGT-Lebensdauer|Gibt das maximale Alter ein Kerberos-TGT, das für einen Benutzer (in Sekunden ausgedrückt) ausgestellt wurde. Die resultierenden TGTs sind nicht erneuerbar.|
|Computer|Computer Authentication Policy|Gibt an, welches authnpolicy-Objekt ist auf Computern, die diesem siloobjekt zugewiesen wurden, angewendet.|
|Computer|Computer Authentication Policy Rückverweis|Dieses Attribut ist der Rückverweis für MsDS-ComputerAuthNPolicy.|
|Computer|ms-DS-Computer-Allowed-To-Authenticate-To|Dieses Attribut wird verwendet, um die Gruppe von Prinzipalen zu bestimmen, die für einen Dienst unter dem Computerkonto ausgeführt wird, authentifiziert.|
|Computer|Computer TGT-Lebensdauer|Gibt das maximale Alter ein Kerberos-TGT, das auf einem Computer (in Sekunden ausgedrückt) ausgestellt wurde. Es wird nicht empfohlen, diese Einstellung zu ändern.|
|Dienst|Service Authentication Policy|Gibt an, welches authnpolicy-Objekt sein soll übernommen, die diesem siloobjekt zugewiesen wurden.|
|Dienst|Service Authentication Policy Rückverweis|Dieses Attribut ist der Rückverweis für MsDS-ServiceAuthNPolicy.|
|Dienst|ms-DS-Service-Allowed-To-Authenticate-To|Dieses Attribut wird verwendet, um die Gruppe von Prinzipalen zu bestimmen, die für einen Dienst unter dem Dienstkonto ausgeführt wird, authentifiziert.|
|Dienst|ms-DS-Service-Allowed-To-Authenticate-From|Dieses Attribut wird verwendet, um die Geräte zu bestimmen, ein Dienstkonto Anmeldeberechtigungen verfügt.|
|Dienst|Service TGT-Lebensdauer|Legt das maximale Alter ein Kerberos-TGT, das an einen Dienst (in Sekunden ausgedrückt) ausgestellt wurde.|

Authentifizierungsrichtlinien können für jedes Silo konfiguriert werden, mithilfe der Active Directory-Verwaltungskonsole oder Windows PowerShell. Weitere Informationen finden Sie unter [How to Configure Protected Accounts](how-to-configure-protected-accounts.md).

## <a name="how-it-works"></a>So funktioniert es
Dieser Abschnitt beschreibt die Funktionsweise von authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien in Verbindung mit der Sicherheitsgruppe "geschützte Benutzer" und die Implementierung des Kerberos-Protokolls in Windows.

-   [Verwendung des Kerberos-Protokolls mit authentifizierungssilos und-Richtlinien](#BKMK_HowKerbUsed)

-   [Einschränken einer Benutzeranmeldung funktioniert](#BKMK_HowRestrictingSignOn)

-   [Funktionsweise von Einschränken der Dienstticket-Ausstellung](#BKMK_HowRestrictingServiceTicket)

**Geschützte Konten**

Die Sicherheitsgruppe "geschützte Benutzer" löst nicht konfigurierbaren Schutz auf Geräten und Hostcomputern, die unter Windows Server 2012 R2 und Windows 8.1, und klicken Sie auf den Domänencontrollern in Domänen mit einem primären Domänencontroller unter Windows Server 2012 R2. Abhängig von der Domänenfunktionsebene des Kontos sind Mitglieder der Sicherheitsgruppe "geschützte Benutzer" Weiter aufgrund von Änderungen der Authentifizierungsmethoden geschützt, die in Windows unterstützt werden.

-   Das Mitglied der Sicherheitsgruppe der geschützten Benutzer kann mithilfe von NTLM, Digestauthentifizierung oder Delegierung der Standardanmeldeinformationen mit CredSSP authentifizieren. Auf einem Gerät unter Windows 8.1, die keines dieser Security Support Provider (SSP) verwendet, schlägt die Authentifizierung mit einer Domäne fehl, wenn das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer ist.

-   Das Kerberos-Protokoll wird nicht die schwächeren des- oder RC4-Verschlüsselungstypen bei der Vorauthentifizierung verwendet. Dies bedeutet, dass die Domäne mindestens den Verschlüsselungstyp AES unterstützt konfiguriert werden muss.

-   Das Konto des Benutzers kann nicht delegiert werden, mit der eingeschränkten und uneingeschränkten Kerberos Delegierung. Dies bedeutet, dass frühere Verbindungen mit anderen Systemen fehlschlagen, wenn der Benutzer Mitglied der Sicherheitsgruppe der geschützten Benutzer ist.

-   Die Standardeinstellung für die Lebensdauer von Kerberos-TGTs von vier Stunden lässt sich mithilfe von Authentifizierungsrichtlinien und Silos konfiguriert werden, die über das Active Directory-Verwaltungscenter zugegriffen werden kann. Dies bedeutet, dass bei der vier Stunden vergangen ist, die der Benutzer erneut authentifizieren muss.

Weitere Informationen zu dieser Sicherheitsgruppe finden Sie unter [wie der geschützten Benutzer funktioniert Gruppe](protected-users-security-group.md#BKMK_HowItWorks).

**Silos und Authentifizierungsrichtlinien**

Authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien nutzen die vorhandene Infrastruktur des Windows-Authentifizierung. Die Verwendung des NTLM-Protokolls wird abgelehnt, und das Kerberos-Protokoll mit neueren Verschlüsselungstypen verwendet wird. Authentifizierungsrichtlinien ergänzen die Sicherheitsgruppe "geschützte Benutzer" durch die Möglichkeit, konfigurierbare Einschränkungen auf Konten, zusätzlich zur Bereitstellung von Einschränkungen für Konten für Dienste und Computer anwenden. Authentifizierungsrichtlinien werden während des Kerberos-Protokoll-Authentifizierungsdienst (AS) oder ein Ticket-granting Service (TGS) Exchange erzwungen. Weitere Informationen wie Windows das Kerberos-Protokoll verwendet, und welche Änderungen zur Unterstützung von authentifizierungsrichtliniensilos und Authentifizierungsrichtlinien vorgenommen wurden finden Sie unter:

-   [Wie funktioniert das Authentifizierungsprotokoll Kerberos Version 5](https://technet.microsoft.com/library/cc772815(v=ws.10).aspx)

-   [Änderungen bei der Kerberosauthentifizierung](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) (Windows Server 2008 R2 und Windows 7)

### <a name="BKMK_HowKerbUsed"></a>Verwendung des Kerberos-Protokolls mit authentifizierungsrichtliniensilos und-Richtlinien
Wenn ein Domänenkonto mit einem authentifizierungsrichtliniensilo verknüpft ist, und der Benutzer anmeldet, fügt der Sicherheitskonto-Manager den Anspruchstyp authentifizierungsrichtliniensilo, der das Silo als Wert enthält. Dieser Anspruch im Konto bietet Zugriff auf das betreffende Silo.

Wenn eine Authentifizierungsrichtlinie erzwungen wird, und die authentifizierungsdienstanforderung für ein Domänenkonto auf dem Domänencontroller empfangen wird, gibt der Domänencontroller ein nicht erneuerbares TGT mit der konfigurierten Gültigkeitsdauer (es sei denn, die Domäne TGT keine kürzere Lebensdauer hat).

> [!NOTE]
> Das Domänenkonto muss eine konfigurierte TGT-Lebensdauer und muss entweder direkt mit der Richtlinie verknüpft oder indirekt über die silomitgliedschaft verknüpft.

Wenn eine Authentifizierungsrichtlinie aktiviert, im Überwachungsmodus ist, und die authentifizierungsdienstanforderung für ein Domänenkonto auf dem Domänencontroller empfangen wird, prüft der Domänencontroller, wenn die Authentifizierung für das Gerät zulässig ist, damit eine Warnung protokolliert werden können, wenn ein Fehler vorliegt. Den Prozess wird von eine überwachte Authentifizierungsrichtlinie nicht geändert werden, damit authentifizierungsanforderungen nicht fehl, wenn sie die Anforderungen der Richtlinie nicht erfüllen.

> [!NOTE]
> Das Domänenkonto muss entweder direkt mit der Richtlinie verknüpft oder indirekt über die silomitgliedschaft verknüpft werden.

Wenn eine Authentifizierungsrichtlinie erzwungen wird und der Authentifizierungsdienst hochgerüstet ist, wird die authentifizierungsdienstanforderung für ein Domänenkonto auf dem Domänencontroller empfangen wird, der Domänencontroller prüft, ob die Authentifizierung für das Gerät zulässig ist. Schlägt fehl, wird der Domänencontroller eine Fehlermeldung zurück und protokolliert ein Ereignis.

> [!NOTE]
> Das Domänenkonto muss entweder direkt mit der Richtlinie verknüpft oder indirekt über die silomitgliedschaft verknüpft werden.

Wenn eine Authentifizierungsrichtlinie aktiviert, im Überwachungsmodus ist, und vom Domänencontroller für ein Domänenkonto eine Ticket-granting Service-Anforderung empfangen wird, prüft der Domänencontroller, wenn die Authentifizierung zulässig ist, basierend auf den anforderungstickets Privilege Attribute Certificate (PAC) Daten, und sie eine Warnung protokolliert, wenn ein Fehler auftritt. Das PAC enthält verschiedene Arten von Autorisierungsdaten, einschließlich Gruppen, denen der Benutzer Mitglied der Rechte, die der Benutzer verfügt, und welche Richtlinien für den Benutzer gelten. Diese Informationen werden verwendet, um Zugriffstoken des Benutzers zu generieren. Ist dies die erzwungene Authentifizierungsrichtlinie die Authentifizierung auf einen Benutzer, Gerät oder Dienst ermöglicht, anhand des anforderungstickets PAC-Daten der Domäne Domänencontroller wird überprüft, ob die Authentifizierung zulässig ist. Schlägt fehl, wird der Domänencontroller eine Fehlermeldung zurück und protokolliert ein Ereignis.

> [!NOTE]
> Das Domänenkonto muss entweder direkt verknüpft oder werden über die silomitgliedschaft mit eine überwachte Authentifizierungsrichtlinie die Authentifizierung eines Benutzers, Geräts oder Diensts zulässt verknüpft,

Sie können eine Authentifizierungsrichtlinie für alle Mitglieder eines Silos oder separate Richtlinien für Benutzer, Computer und verwaltete Dienstkonten verwenden.

Authentifizierungsrichtlinien können für jedes Silo konfiguriert werden, mithilfe der Active Directory-Verwaltungskonsole oder Windows PowerShell. Weitere Informationen finden Sie unter [How to Configure Protected Accounts](how-to-configure-protected-accounts.md).

### <a name="BKMK_HowRestrictingSignOn"></a>Einschränken einer Benutzeranmeldung funktioniert
Da diese Authentifizierungsrichtlinien auf ein Konto angewendet werden, gilt es auch für Konten, die von Diensten verwendet werden. Wenn Sie die Verwendung eines Kennworts für einen Dienst auf bestimmte Hosts beschränken möchten, ist diese Einstellung hilfreich. Beispielsweise verwaltete Gruppe Konten konfiguriert sind, wo die Hosts zum Abrufen des Kennworts aus Active Directory Domain Services zulässig sind. Das Kennwort kann jedoch von jedem Host zur anfänglichen Authentifizierung verwendet werden. Durch das Anwenden einer, kann eine zusätzliche Schutzebene beschränken das Kennwort nur auf die Gruppe von Hosts, die das Kennwort abrufen können erzielt werden.

Wenn Dienste, System, Netzwerkdienst oder andere lokale Dienstidentität ausgeführt, mit Netzwerkdiensten verbinden, verwenden sie das Computerkonto des Hosts. Computerkonten können nicht beschränkt werden. Daher auch, wenn der Dienst ein Computerkonto, die nicht für einen Windows-Host ist verwendet, kann nicht dieses nicht eingeschränkt werden.

Einschränken der Benutzeranmeldung auf bestimmte Hosts erfordert den Domänencontroller die Identität des Hosts zu überprüfen. Bei Verwendung von Kerberos-Authentifizierung mit Kerberos amoring (die Bestandteil der dynamischen Zugriffssteuerung ist), wird das Schlüsselverteilungscenter mit dem TGT des Hosts bereitgestellt von dem der Benutzer authentifiziert wird. Der Inhalt dieses geschützten TGT wird verwendet, um die Durchführung einer zugriffsprüfung, um festzustellen, ob der Host zulässig ist.

Wenn ein Benutzer bei Windows anmeldet oder Anmeldeinformationen für die Domäne in eine Eingabeaufforderung für eine Anwendung in der Standardeinstellung wechselt, sendet Windows eine ungeschützte AS-REQ an den Domänencontroller. Wenn der Benutzer die Anforderung von einem Computer sendet, die nicht unterstützt schlägt armoring, z. B. Computer mit Windows 7 oder Windows Vista, die Anforderung fehl.

In der folgende Liste wird den Prozess beschrieben:

-   Der Domänencontroller in einer Domäne unter Windows Server 2012 R2 für das Benutzerkonto abfragt und bestimmt, ob es mit einer Authentifizierungsrichtlinie konfiguriert ist, die die anfängliche Authentifizierung zu beschränken, die geschützten Anforderungen.

-   Der Domänencontroller wird die Anforderung fehl.

-   Da Kerberos armoring erforderlich ist, kann der Benutzer versuchen, melden Sie sich mit einem Computer unter Windows 8.1 oder Windows 8, die zur Unterstützung der Kerberos-Schutz um den Anmeldevorgang erneut aktiviert wird.

-   Windows erkennt, dass die Domäne Kerberos armoring unterstützt, und eine geschützte AS-REQ sendet, um die Anmeldung Vorgang zu wiederholen.

-   Der Domänencontroller führt eine zugriffsprüfung mit den konfigurierten zugriffssteuerungsbedingungen und den Identitätsinformationen des Client-Betriebssystems im TGT, das zur Abschirmung die Anforderung verwendet wurde.

-   Wenn die zugriffsprüfung fehlschlägt, lehnt der Domänencontroller die Anforderung ab.

Auch wenn Betriebssysteme Kerberos armoring unterstützt, werden Anforderungen an die Zugriffssteuerung angewendet werden können und müssen erfüllt sein, bevor der Zugriff gewährt wird. Benutzer melden Sie sich bei Windows oder geben ihre Domänenanmeldeinformationen in eine Eingabeaufforderung für eine Anwendung. Standardmäßig sendet Windows eine ungeschützte AS-REQ an den Domänencontroller. Wenn der Benutzer die Anforderung von einem Computer, die Kerberos armoring sendet, z. B. Windows 8.1 oder Windows 8 unterstützt werden die Authentifizierungsrichtlinien wie folgt ausgewertet:

1.  Der Domänencontroller in einer Domäne unter Windows Server 2012 R2 für das Benutzerkonto abfragt und bestimmt, ob es mit einer Authentifizierungsrichtlinie konfiguriert ist, die die anfängliche Authentifizierung zu beschränken, die geschützten Anforderungen.

2.  Der Domänencontroller führt eine zugriffsprüfung mit den konfigurierten zugriffssteuerungsbedingungen und den Identitätsinformationen des Systems im TGT, das zur Abschirmung die Anforderung verwendet wird. Die zugriffsprüfung ist erfolgreich.

    > [!NOTE]
    > Wenn ältere arbeitsgruppeneinschränkungen konfiguriert sind, müssen auch diese erfüllt werden.

3.  Der Domänencontroller antwortet mit einer geschützten Antwort (AS-REP), und die Authentifizierung wird fortgesetzt.

### <a name="BKMK_HowRestrictingServiceTicket"></a>Funktionsweise von Einschränken der Dienstticket-Ausstellung
Wenn ein Konto ist nicht zulässig, und ein Benutzer, der ein TGT besitzt, mit dem Dienst herzustellen versucht (z. B. durch Öffnen einer Anwendung, die Authentifizierung bei einem Dienst erfordert, die durch den Dienst für Dienstprinzipalnamen (SPN) identifiziert wird, geschieht Folgendes:

1.  Bei einem Versuch von SPN Verbindung mit SPN1 herzustellen sendet Windows eine TGS-REQ an den Domänencontroller, der ein Dienstticket für SPN1 anfordert.

2.  Der Domänencontroller in einer Domäne unter Windows Server 2012 R2 spn1 nach dem Active Directory Domain Services-Konto für den Dienst zu finden und feststellt, dass das Konto mit einer Authentifizierungsrichtlinie konfiguriert ist, die Ausstellung von Diensttickets beschränkt.

3.  Der Domänencontroller führt eine zugriffsprüfung mit den konfigurierten zugriffssteuerungsbedingungen und den Identitätsinformationen des Benutzers im TGT Die zugriffsprüfung schlägt fehl.

4.  Der Domänencontroller weist die Anforderung zurück.

Wenn ein Konto zulässig ist, weil das Konto erfüllt die Bedingungen für die Zugriffssteuerung, die durch die Authentifizierungsrichtlinie festgelegt werden, und ein Benutzer, der ein TGT besitzt, mit dem Dienst herzustellen versucht (z. B. durch Öffnen einer Anwendung, die eine Authentifizierung erforderlich ist, ein Dienst, der vom SPN des Diensts identifiziert wird), geschieht Folgendes:

1.  Bei einem Versuch zur Verbindung mit SPN1 sendet Windows eine TGS-REQ an den Domänencontroller, der ein Dienstticket für SPN1 anfordert.

2.  Der Domänencontroller in einer Domäne unter Windows Server 2012 R2 spn1 nach dem Active Directory Domain Services-Konto für den Dienst zu finden und feststellt, dass das Konto mit einer Authentifizierungsrichtlinie konfiguriert ist, die Ausstellung von Diensttickets beschränkt.

3.  Der Domänencontroller führt eine zugriffsprüfung mit den konfigurierten zugriffssteuerungsbedingungen und den Identitätsinformationen des Benutzers im TGT Die zugriffsprüfung ist erfolgreich.

4.  Der Domänencontroller antwortet auf die Anforderung mit einer Ticket-granting-Dienstantwort (TGS-REP).

## <a name="BKMK_ErrorandEvents"></a>Zugehörige Fehler- und informationsmeldungen
Die folgende Tabelle beschreibt die Ereignisse, die Sicherheitsgruppe "geschützte Benutzer" zugeordnet sind und die Authentifizierungsrichtlinien, die für authentifizierungsrichtliniensilos angewendet werden.

Die Ereignisse werden aufgezeichnet, in den Anwendungs- und Dienstprotokolle am **Microsoft\Windows\Authentication**.

Schritte zur Problembehandlung, die diese Ereignisse verwenden, finden Sie unter [Problembehandlung von Authentifizierungsrichtlinien](how-to-configure-protected-accounts.md#BKMK_TroubleshootAuthnPolicies) und [Problembehandlung für Ereignisse im Zusammenhang mit geschützten Benutzern](how-to-configure-protected-accounts.md#BKMK_TrubleshootingEvents).

|Ereignis-ID und Protokoll|Beschreibung|
|----------|--------|
|101<br /><br />**"AuthenticationPolicyFailures-DomainController"**|Grund: Ein NTLM-Anmeldefehler tritt auf, weil die Authentifizierungsrichtlinie konfiguriert ist.<br /><br />Auf dem Domänencontroller, um anzugeben, dass die NTLM-Authentifizierung fehlgeschlagen, weil zugriffssteuerungseinschränkungen erforderlich sind, und diese Einschränkungen nicht auf NTLM anwendbar ist ein Ereignis protokolliert.<br /><br />Zeigt das Konto, Gerät, Richtlinie und Silo Namen.|
|105<br /><br />**"AuthenticationPolicyFailures-DomainController"**|Grund: Ein Kerberos-Einschränkungsfehler tritt auf, weil die Authentifizierung von einem bestimmten Gerät nicht zugelassen wurde.<br /><br />Auf dem Domänencontroller, um anzugeben, dass ein Kerberos-TGT verweigert wurde, weil das Gerät nicht die erzwungenen zugriffssteuerungseinschränkungen erfüllt, wird ein Ereignis protokolliert.<br /><br />Zeigt das Konto, Gerät, Gruppenrichtlinie, silonamen und TGT-Lebensdauer.|
|305<br /><br />**"AuthenticationPolicyFailures-DomainController"**|Grund: Ein potenzieller Kerberos-Einschränkungsfehler kann auftreten, da die Authentifizierung von einem bestimmten Gerät nicht zugelassen wurde.<br /><br />Im Überwachungsmodus befinden wird ein Informationsereignis protokolliert, auf dem Domänencontroller, um festzustellen, ob ein Kerberos-TGT verweigert wird, da das Gerät nicht die zugriffssteuerungseinschränkungen erfüllt.<br /><br />Zeigt das Konto, Gerät, Gruppenrichtlinie, silonamen und TGT-Lebensdauer.|
|106<br /><br />**"AuthenticationPolicyFailures-DomainController"**|Grund: Ein Kerberos-Einschränkungsfehler tritt auf, weil der Benutzer bzw. das Gerät nicht mit dem Server authentifizieren durfte.<br /><br />Es wird ein Ereignis protokolliert, auf dem Domänencontroller, um anzugeben, dass ein Kerberos-Dienstticket verweigert wurde, weil der Benutzer, Gerät oder beide nicht die erzwungenen zugriffssteuerungseinschränkungen erfüllen.<br /><br />Zeigt das Gerät, Richtlinie und Silo Namen.|
|306<br /><br />**"AuthenticationPolicyFailures-DomainController"**|Grund: Ein Kerberos-Einschränkungsfehler kann auftreten, da der Benutzer bzw. das Gerät nicht mit dem Server authentifizieren durfte.<br /><br />Im Überwachungsmodus befinden wird ein Informationsereignis protokolliert, auf dem Domänencontroller, um anzugeben, dass ein Kerberos-Dienstticket verweigert wird, da der Benutzer, Gerät oder beide nicht die zugriffssteuerungseinschränkungen erfüllen.<br /><br />Zeigt das Gerät, Richtlinie und Silo Namen.|

## <a name="see-also"></a>Siehe auch
[Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md)

[Schutz von Anmeldeinformationen und Verwaltung](credentials-protection-and-management.md)

[Sicherheitsgruppe "geschützte Benutzer"](protected-users-security-group.md)


