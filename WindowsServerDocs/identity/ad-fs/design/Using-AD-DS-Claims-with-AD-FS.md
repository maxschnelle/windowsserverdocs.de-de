---
ms.assetid: 460792e4-9f1d-4e7b-b6b2-53e057f839df
title: Überlegungen zur AD FS-Bereitstellungstopologie
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 46692653ba10558a9236bd321127591bc7c8a275
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838381"
---
# <a name="using-ad-ds-claims-with-ad-fs"></a>Verwenden von AD DS-Ansprüchen mit AD FS
  
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
Sie können umfangreichere Steuerung des Zugriffs auf verbundanwendungen mithilfe von Active Directory Domain Services aktivieren \(AD DS\)\-ausgestellt von Benutzer- und geräteansprüchen, zusammen mit Active Directory Federation Services \(AD FS \).  
  
## <a name="about-dynamic-access-control"></a>Informationen zur dynamischen Zugriffssteuerung  
In Windows Server® 2012, das Feature für die dynamische Zugriffssteuerung ermöglicht es Organisationen, die Zugriff auf Dateien, die basierend auf Ansprüchen des Benutzers gewähren \(die stammen von Attribute des Benutzerkontos\) und geräteansprüchen \(die stammen von Attribute von Computerkonten\) , werden von Active Directory-Domänendiensten ausgestellt \(AD DS\). AD DS-Ansprüche ausgestellt werden in Windows integrierte Authentifizierung über das Authentifizierungsprotokoll Kerberos integriert.  
  
Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter [Dynamic Access Control Content Roadmap](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP).  
  
### <a name="whats-new-in-ad-fs"></a>Was ist neu in AD FS?  
Als Erweiterung für das Szenario für die dynamische Zugriffssteuerung können jetzt mit AD FS unter Windows Server 2012:  
  
-   Access-Konto Computerattribute neben der Attribute des Benutzerkontos aus in AD DS. In früheren Versionen von AD FS konnte den Verbunddienst nicht Computerattribute alle aus AD DS zugreifen.  
  
-   Nutzen Sie die AD DS-Benutzer oder Gerät Ansprüche ausgestellt, die in einer Kerberos-Authentifizierungsticket befinden. In früheren Versionen von AD FS die Anspruchs-Engine konnte der Benutzer- und Sicherheits-IDs lesen \(SIDs\) von Kerberos aber konnte nicht zum Lesen einer Anspruchsinformationen in ein Kerberos-Ticket enthalten sind.  
  
-   Transformieren Sie AD DS ausgestellt von Benutzer- oder Geräteansprüche in SAML-Token, die Anwendungen der vertrauenden Seite verwenden können, um umfassendere Zugriffssteuerung auszuführen.  
  
## <a name="benefits-of-using-ad-ds-claims-with-ad-fs"></a>Vorteile der Verwendung von AD DS die Ansprüche mit AD FS  
Diese AD DS-Ansprüche ausgestellt können in Kerberos-Authentifizierung-Tickets eingefügt werden und mit AD FS verwendet, um die folgenden Vorteile bieten:  
  
-   Organisationen, benötigen umfassendere Access-Control-Richtlinien, können Ansprüche\-schlüsselbasierten Zugriff auf Anwendungen und Ressourcen unter Verwendung von AD DS Ansprüche ausgestellt, die auf den Attributwerten, die für eine bestimmte Benutzer- oder Computerkonto in AD DS gespeicherte basieren. Dadurch können Administratoren zusätzliche Aufwand in Zusammenhang mit der Erstellung und Verwaltung von senken:  
  
    -   AD DS-Sicherheitsgruppen, die andernfalls verwendet werden sollen, zur Steuerung des Zugriffs auf Anwendungen und Ressourcen, die über die integrierte Windows-Authentifizierung zugegriffen werden kann.  
  
    -   Gesamtstruktur-Vertrauensstellungen, die andernfalls verwendet werden würde, für die Steuerung des Zugriffs auf Business\-zu\-Business \(B2B\) \/ Internet zugängliche Anwendungen und Ressourcen.  
  
-   Organisationen können jetzt verhindern, dass nicht autorisierten Zugriff auf Netzwerkressourcen Clientcomputer anhand der gibt an, ob ein bestimmtes Computerkonto in AD DS gespeicherte Wert des Attributs \(z. B. den Namen des Computers DNS\) entspricht die Zugriffssteuerung Richtlinie der Ressource \(z. B. einem Dateiserver, die durch eine ACL geschützt mit Ansprüchen\) oder Richtlinie der vertrauenden Seite \(z. B. eine Ansprüche\-bewusst Webanwendung\). Dadurch können Administratoren eine präzisere Zugriffssteuerungsrichtlinien für Ressourcen oder Anwendungen, die festlegen:  
  
    -   Zugriff nur über die integrierte Windows-Authentifizierung.  
  
    -   Internet, die über AD FS-Authentifizierungsmechanismen zugegriffen werden kann. AD FS kann verwendet werden, zum Transformieren von AD DS ausgestellt von geräteansprüchen in AD FS-Ansprüche, die in der SAML-Token gekapselt werden können, die von einer Internetressource-zugegriffen werden kann oder die Anwendung der vertrauenden Seite genutzt werden können.  
  
## <a name="differences-between-ad-ds-and-ad-fs-issued-claims"></a>Unterschiede zwischen AD DS und AD FS ausgestellten Ansprüche  
Es gibt zwei ausschlaggebenden Faktoren, die wichtig zu verstehen, zu Ansprüchen, die aus AD DS-Visual-Studio ausgegeben werden. AD FS. Zu diesen Unterschieden zählen:  
  
-   AD DS können nur Ansprüche ausgeben, die in Kerberos-Tickets, SAML-Token nicht gekapselt sind. Weitere Informationen dazu, wie AD DS die Ansprüche ausstellt, finden Sie unter [Dynamic Access Control Content Roadmap](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP).  
  
-   AD FS kann nur Ansprüche ausstellen, die im SAML-Token, Kerberos-Tickets nicht gekapselt sind. Weitere Informationen dazu, wie AD FS Ansprüche ausstellt, finden Sie unter [die Rolle des Anspruchsmoduls](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md).  
  
## <a name="how-ad-ds-issued-claims-work-with-ad-fs"></a>Ausgabe von Ansprüchen durch AD DS - Arbeiten mit AD FS  
AD DS-Ansprüche ausgestellt, kann mit AD FS verwendet werden, sowohl Benutzer- und Geräteansprüche direkt aus des Benutzers authentifizierungskontext, anstatt einen separaten Aufruf von LDAP zu Active Directory den Zugriff auf. Die folgende Abbildung und die entsprechenden Schritte wird erläutert, wie dieser Prozess im Detail zu Ansprüchen funktioniert\--basierte Zugriffssteuerung für das Szenario für die dynamische Zugriffssteuerung.  
  
![Verwendung von Ansprüchen](media/UsingADDSClaimswithADFS.gif)  
  
1.  Ein AD DS-Administrator verwendet die Active Directory Administrative Center-Konsole oder das PowerShell-Cmdlets ermöglicht bestimmten Anspruch Objekten in der AD DS-Schema.  
  
2.  Ein AD FS-Administrator verwendet die AD FS-Verwaltungskonsole zum Erstellen und Konfigurieren der Anspruchsanbieter-Vertrauensstellung und der vertrauenden Seite Vertrauensstellungen mit Pass\-über oder Transformation Anspruchsregeln.  
  
3.  Ein Windows-Client versucht, auf das Netzwerk zugreifen. Im Rahmen der Kerberos-Authentifizierungsprozess wird der Client stellt die Benutzer- und Computerobjekte Ticket\-Gewähren von Tickets \(TGT\) die noch keinen Forderungen, mit dem Domänencontroller. Der Domänencontroller in AD DS aktiviert Anspruchstypen sucht und alle resultierenden Ansprüche im zurückgegebenen Kerberos-Ticket enthält.  
  
4.  Wenn der Benutzer\/Client versucht, eine Ressource zuzugreifen, die durch eine ACL geschützt, die Ansprüche erforderlich ist, sie können auf die Ressource zugreifen, da die Verbund-ID, die von Kerberos verfügbar gemacht wurde diese Ansprüche enthält.  
  
5.  Wenn der gleiche Client versucht, die eine Website oder Web-Anwendung zugreifen, die für die AD FS-Authentifizierung konfiguriert ist, wird der Benutzer auf eine AD FS-Verbundserver umgeleitet, die für die integrierte Windows-Authentifizierung konfiguriert ist. Der Client sendet eine Anforderung an den Domänencontroller mithilfe von Kerberos. Der Domänencontroller gibt ein Kerberos-Ticket enthält die angeforderten Ansprüche, die der Client dann an den Verbundserver darstellen kann.  
  
6.  Basierend auf die Möglichkeit, die die Anspruchsregeln für den Anspruchsanbieter konfiguriert wurden, und der vertrauenden Seite Vertrauensstellungen, dass der Administrator, die Sie zuvor konfiguriert haben, AD FS die Ansprüche aus dem Kerberos-Ticket liest und sie in einem SAML-Token fügt, das für den Client herausgegeben.  
  
7.  Der Client die Richtigkeit der Ansprüche mit SAML-Token empfängt, und klicken Sie dann auf der Website umgeleitet wird.  
  
Weitere Informationen zum Erstellen der Anspruchsregeln für AD DS ausgestellten zur Verwendung von AD FS Ansprüche erforderlich sind, finden Sie unter [erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
