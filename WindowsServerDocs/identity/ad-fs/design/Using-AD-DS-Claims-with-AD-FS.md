---
ms.assetid: 460792e4-9f1d-4e7b-b6b2-53e057f839df
title: Verwenden von AD DS-Ansprüchen mit AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2f3aa75a865c61d486d68463aceb6574f6381eb0
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864252"
---
# <a name="using-ad-ds-claims-with-ad-fs"></a>Verwenden von AD DS-Ansprüchen mit AD FS
  
  
Sie können eine umfassendere Zugriffs Steuerung für Verbund Anwendungen ermöglichen, indem Sie Active Directory Domain Services \( AD DS von \) \- Benutzer-und Geräte Ansprüchen mit Active Directory-Verbunddienste (AD FS) \( AD FS \) .  
  
## <a name="about-dynamic-access-control"></a>Informationen zu dynamischen Access Control  
In Windows Server &reg; 2012 ermöglicht die Funktion "dynamische Access Control" Organisationen das Gewähren von Zugriff auf Dateien auf der Grundlage von Benutzer Ansprüchen \( , die von Benutzerkonto Attributen \) und Geräte Ansprüchen bezogen werden, \( die von den Active Directory Domain Services-AD DS ausgestellten Computer Konto Attributen stammen \) \( \) . AD DS ausgestellte Ansprüche werden über das Kerberos-Authentifizierungsprotokoll in die integrierte Windows-Authentifizierung integriert.  
  
Weitere Informationen zu dynamischen Access Control finden Sie unter [Dynamic Access Control Content Roadmap](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP).  
  
### <a name="whats-new-in-ad-fs"></a>Neues in AD FS  
Als Erweiterung des dynamischen Access Control Szenarios können AD FS in Windows Server 2012 nun folgende Aktionen ausführen:  
  
-   Greifen Sie zusätzlich zu den Attributen von Benutzerkonten innerhalb AD DS auf Computer Konto Attribute zu. In früheren Versionen von AD FS konnte der Verbunddienst überhaupt nicht auf die Computer Konto Attribute von AD DS zugreifen.  
  
-   Nutzen AD DS ausgegebene Benutzer-oder Geräteansprüche, die sich in einem Kerberos-Authentifizierungs Ticket befinden. In früheren Versionen von AD FS konnte die Anspruchs-Engine die Benutzer-und Gruppen Sicherheits-IDs der \( SIDs \) aus Kerberos lesen, konnte jedoch keine in einem Kerberos-Ticket enthaltenen Anspruchs Informationen lesen.  
  
-   Transformieren Sie AD DS ausgegebene Benutzer-oder Geräteansprüche in SAML-Token, die vertrauende Anwendungen zum Ausführen einer umfassenderen Zugriffs Steuerung verwenden können.  
  
## <a name="benefits-of-using-ad-ds-claims-with-ad-fs"></a>Vorteile der Verwendung von AD DS Ansprüchen mit AD FS  
Diese AD DS ausgestellten Ansprüche können in Kerberos-Authentifizierungs Tickets eingefügt und mit AD FS verwendet werden, um die folgenden Vorteile zu bieten:  
  
-   Organisationen, die umfangreichere Richtlinien für die Zugriffs Steuerung benötigen, können Anspruchs \- basierten Zugriff auf Anwendungen und Ressourcen ermöglichen, indem Sie AD DS ausgestellte Ansprüche verwenden, die auf den in AD DS gespeicherten Attributwerten für ein bestimmtes Benutzer-oder Computer Konto basieren. Dies kann Administratoren helfen, zusätzlichen mehr Aufwand im Zusammenhang mit der Erstellung und Verwaltung zu reduzieren:  
  
    -   AD DS Sicherheitsgruppen, die andernfalls zum Steuern des Zugriffs auf Anwendungen und Ressourcen verwendet werden, die über die integrierte Windows-Authentifizierung zugänglich sind.  
  
    -   Gesamtstruktur-Vertrauens Stellungen, die andernfalls verwendet werden, um den Zugriff auf \- \- \( B2B \) \/ -Anwendungen und Ressourcen, die im Internet zugänglich sind, zu steuern  
  
-   Unternehmen können jetzt den nicht autorisierten Zugriff auf Netzwerkressourcen von Client Computern aus verhindern, abhängig davon, ob ein bestimmter Computer Konto-Attribut Wert in AD DS \( z. b. der DNS-Name eines Computers \) mit der Zugriffs Steuerungs Richtlinie der Ressource übereinstimmt \( , z. b. ein Dateiserver, der mit Ansprüchen \) oder der Richtlinie der vertrauenden Seite wie \( eine Ansprüche unterstützende \- Webanwendung \) verwendet wurde Dies kann Administratoren helfen, präzisere Zugriffs Steuerungs Richtlinien für Ressourcen oder Anwendungen festzulegen, die Folgendes sind:  
  
    -   Nur über die integrierte Windows-Authentifizierung zugänglich.  
  
    -   Internet Zugriff über AD FS Authentifizierungsmechanismen. Mit AD FS können AD DS ausgegebene Geräteansprüche in AD FS Ansprüche transformiert werden, die in SAML-Token gekapselt werden können, die von einer Ressource mit Internet Zugriff oder der Anwendung der vertrauenden Seite genutzt werden können.  
  
## <a name="differences-between-ad-ds-and-ad-fs-issued-claims"></a>Unterschiede zwischen AD DS und AD FS ausgestellten Ansprüchen  
Zwei unterschiedliche Faktoren sind wichtig, um die Ansprüche zu verstehen, die von AD DS vs. AD FS ausgegeben werden. Zu diesen Unterschieden zählen Folgende:  
  
-   AD DS können nur Ansprüche ausstellen, die in Kerberos-Tickets gekapselt sind, nicht SAML-Token. Weitere Informationen darüber, wie AD DS Ansprüche ausgibt, finden Sie unter [Dynamic Access Control Content Roadmap](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP).  
  
-   AD FS können nur Ansprüche ausstellen, die in SAML-Token gekapselt sind, nicht Kerberos-Tickets. Weitere Informationen dazu, wie AD FS Ansprüche ausgibt, finden Sie [unter The Role of the Claims Engine](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md).  
  
## <a name="how-ad-ds-issued-claims-work-with-ad-fs"></a>Ausgabe von Ansprüchen durch AD DS - Arbeiten mit AD FS  
AD DS ausgestellte Ansprüche können mit AD FS verwendet werden, um direkt aus dem Authentifizierungs Kontext des Benutzers auf Benutzer-und Geräteansprüche zuzugreifen, anstatt einen separaten LDAP-aufrufActive Directory zu erstellen. In der folgenden Abbildung und den entsprechenden Schritten wird erläutert, wie dieser Prozess ausführlicher funktioniert, um \- die Anspruchs basierte Zugriffs Steuerung für das dynamische Access Control Szenario zu aktivieren.  
  
![Verwenden von Ansprüchen](media/UsingADDSClaimswithADFS.gif)  
  
1.  Ein AD DS Administrator verwendet die Active Directory-Verwaltungscenter-Konsole oder PowerShell-Cmdlets, um bestimmte Anspruchstyp Objekte im AD DS Schema zu aktivieren.  
  
2.  Ein AD FS Administrator verwendet die AD FS Management Console, um den Anspruchs Anbieter und Vertrauens Stellungen der vertrauenden Seite entweder mit Pass- \- Through-oder Transform-Anspruchs Regeln zu erstellen und zu konfigurieren.  
  
3.  Ein Windows-Client versucht, auf das Netzwerk zuzugreifen. Im Rahmen des Kerberos-Authentifizierungs Vorgangs stellt der Client seinen Benutzer und das Computer Ticket, der \- \( noch keine \) Ansprüche enthält, für den Domänen Controller vor. Der Domänen Controller sucht dann in AD DS nach aktivierten Anspruchs Typen und schließt alle sich ergebenden Ansprüche in das zurückgegebene Kerberos-Ticket ein.  
  
4.  Wenn der Benutzer \/ Client versucht, auf eine Datei Ressource zuzugreifen, die ACLD ist, um die Ansprüche anzufordern, kann er auf die Ressource zugreifen, da die Verbund-ID, die von Kerberos ausgegeben wurde, über diese Ansprüche verfügt.  
  
5.  Wenn derselbe Client versucht, auf eine Website oder Webanwendung zuzugreifen, die für die AD FS Authentifizierung konfiguriert ist, wird der Benutzer zu einem AD FS Verbund Server umgeleitet, der für die integrierte Windows-Authentifizierung konfiguriert ist. Der Client sendet mithilfe von Kerberos eine Anforderung an den Domänen Controller. Der Domänen Controller gibt ein Kerberos-Ticket aus, das die angeforderten Ansprüche enthält, die der Client dann dem Verbund Server präsentieren kann.  
  
6.  Basierend auf der Art und Weise, in der die Anspruchs Regeln für den Anspruchs Anbieter und die Vertrauens Stellungen der vertrauenden Seite konfiguriert wurden, die der Administrator zuvor konfiguriert hat, liest AD FS die Ansprüche aus dem Kerberos-Ticket und schließt Sie in ein SAML-Token ein, das für den Client ausgegeben wird  
  
7.  Der Client empfängt das SAML-Token mit den richtigen Ansprüchen und wird dann an die Website umgeleitet.  
  
Weitere Informationen zum Erstellen der Anspruchs Regeln, die für AD DS ausgestellte Ansprüche zum Arbeiten mit AD FS erforderlich sind, finden Sie unter [Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md).  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
