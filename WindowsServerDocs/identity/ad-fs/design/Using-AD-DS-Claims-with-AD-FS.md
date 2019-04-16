---
ms.assetid: 460792e4-9f1d-4e7b-b6b2-53e057f839df
title: "Überlegungen zur AD FS-Bereitstellungstopologie"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 46692653ba10558a9236bd321127591bc7c8a275
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="using-ad-ds-claims-with-ad-fs"></a>Mithilfe von AD DS-Ansprüche mit AD FS
  
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012
  
Sie können umfassendere Steuerung des Zugriffs für verbundanwendungen mithilfe von Active Directory-Domänendienste \(AD DS\)\-issued Benutzer- und Geräteansprüche zusammen mit Active Directory Federation Services \(AD FS\) aktivieren.  
  
## <a name="about-dynamic-access-control"></a>Dynamische Zugriffssteuerung  
In Windows Server® 2012, das Feature für die dynamische Zugriffssteuerung ermöglicht es Organisationen, Gewähren von Zugriff auf Dateien auf Basis von benutzeransprüchen \ (die als Quelle verweisen, vom Benutzer Konto Attributes\) und geräteansprüchen \ (das sind zugrunde liegenden Computer Konto Attributes\), die von Active Directory-Domänendienste \(AD DS\) ausgestellt werden. AD DS-Ansprüche ausgestellt werden in Windows-Authentifizierung über Kerberos-Authentifizierungsprotokolls integriert.  
  
Weitere Informationen zur dynamischen Zugriffssteuerung finden Sie unter [Dynamic Access-Steuerelement Inhaltsroadmap](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP).  
  
### <a name="whats-new-in-ad-fs"></a>Was ist neu in AD FS?  
Als Erweiterung für das Szenario für die dynamische Zugriffssteuerung können jetzt mit AD FS unter Windows Server 2012:  
  
-   Zugriffsattribute von Computerkonten neben Attribute von Benutzerkonten aus innerhalb von AD DS. In früheren Versionen von AD FS konnte der Verbunddienst nicht Computerattribute überhaupt aus AD DS zugreifen.  
  
-   Nutzen Sie die AD DS-Benutzer bzw. das Gerät Ansprüche ausgestellt, die in ein Kerberos-Authentifizierungsticket befinden. In früheren Versionen von AD FS, wurde das anspruchsmodul Benutzer lesen und Gruppe Sicherheits-IDs \(SIDs\) von Kerberos aber konnte nicht lesen Ansprüche von Kerberos-Ticket enthaltenen Informationen.  
  
-   Verwandeln Sie AD DS ausgestellt von Benutzer- oder Geräteansprüche in SAML-Token, mit dem Anwendungen der vertrauenden Seite umfassendere Steuerung des Zugriffs ausführen.  
  
## <a name="benefits-of-using-ad-ds-claims-with-ad-fs"></a>Vorteile der Verwendung von AD DS Ansprüchen mit AD FS  
Diese AD DS-Ansprüche ausgestellt kann in Kerberos Authentication Tickets eingefügt und mit AD FS verwendet, um die folgenden Vorteile werden:  
  
-   Unternehmen, die benötigen umfassendere Zugriffsrichtlinien, können Claims\-basierten Zugriff auf Anwendungen und Ressourcen mithilfe von AD DS-Ansprüche ausgestellt, die basieren auf den Attributwerten für einen bestimmten Benutzer oder das Computerkonto in AD DS gespeichert. Dadurch können Administratoren zusätzlichen Aufwand in Zusammenhang mit erstellen und Verwalten von senken:  
  
    -   AD DS-Sicherheitsgruppen, die ansonsten verwendet würden, zum Steuern des Zugriffs auf Anwendungen und Ressourcen, die über die integrierte Windows-Authentifizierung zugegriffen werden kann.  
  
    -   Gesamtstruktur-Vertrauensstellungen, die ansonsten, zum Steuern des Zugriffs auf Business\-zu-Business \(B2B\) verwendet würden \ / Internet zugegriffen werden Anwendungen und Ressourcen.  
  
-   Organisationen können jetzt verhindern, dass nicht autorisierten Zugriff auf Netzwerkressourcen Clientcomputer anhand der gibt an, ob ein bestimmtes Computerkonto in AD DS gespeicherten Wert-Attribut \ (z. B. einem Computer DNS-Tokentypen) entspricht der Zugriffssteuerungsrichtlinie der Ressource \ (z. B. ein Dateiserver, die ACLd mit Claims\ wurde) oder die relying Party-Richtlinie \ (z. B. Claims\-aware Web-Application\). Dadurch können Administratoren eine genauere Zugriffsrichtlinien für Ressourcen oder Anwendungen festlegen:  
  
    -   Nur über die integrierte Windows-Authentifizierung.  
  
    -   Internet-Zugriff per AD FS-Authentifizierungsmechanismen. AD FS kann verwendet werden, zum Transformieren von AD DS ausgestellt Geräteansprüche in AD FS-Ansprüche, die in SAML-Token gekapselt werden können, die von einem Internet-Ressource zugegriffen werden kann oder der vertrauenden Seite Anwendung genutzt werden kann.  
  
## <a name="differences-between-ad-ds-and-ad-fs-issued-claims"></a>Unterschiede zwischen AD DS- und AD FS Ansprüche ausgestellt.  
Es gibt zwei ausschlaggebenden Faktoren, die wichtig zu verstehen, zu Ansprüchen, die aus AD DS vs. AD FS ausgestellt werden. Zu diesen Unterschieden zählen:  
  
-   AD DS kann nur Ansprüche ausgeben, die in Kerberos-Tickets, nicht die SAML-Token gekapselt werden. Weitere Informationen, wie AD DS die Ansprüche ausstellt, finden Sie unter [Dynamic Access-Steuerelement Inhaltsroadmap](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP).  
  
-   AD FS kann nur Ansprüche ausgeben, die im SAML-Token, keine Kerberos-Tickets gekapselt werden. Weitere Informationen, wie AD FS Ansprüche ausstellt, finden Sie unter [The Role of the Claims Engine](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md).  
  
## <a name="how-ad-ds-issued-claims-work-with-ad-fs"></a>Wie AD DS die Ansprüche arbeiten mit AD FS ausgestellt  
AD DS-Ansprüche ausgestellt können sowohl Benutzer- und Geräteansprüche direkt aus des Benutzers Authentifizierung Kontext, anstatt einen separaten LDAP-Aufruf von Active Directory den Zugriff auf mit AD FS verwendet werden. Die folgende Abbildung und die entsprechenden Schritte erläutert Funktionsweise dieser Vorgang ausführlicher Claims\ basierende Zugriffssteuerung für das Szenario für die dynamische Zugriffssteuerung zu aktivieren.  
  
![Verwendung von Ansprüchen](media/UsingADDSClaimswithADFS.gif)  
  
1.  Ein AD DS-Administrator verwendet die Active Directory Administrative Center-Konsole oder das PowerShell-Cmdlets zum ermöglicht bestimmten Anspruch Typobjekte in AD DS-Schema.  
  
2.  Ein AD FS-Administrator verwendet die AD FS-Verwaltungskonsole zum Erstellen und Konfigurieren der Anspruchsanbieter und einer vertrauenden Vertrauensstellungen entweder mit Pass\ über oder Transformation Anspruchsregeln.  
  
3.  Ein Windows-Client versucht, auf das Netzwerk zugreifen. Im Rahmen der Kerberos-Authentifizierungsprozess der Client zeigt den Benutzer und Computer Ticket\-granting ticket \(TGT\) nicht noch Ansprüche an den Domänencontroller enthalten. Der Domänencontroller sucht aktiviert Anspruchstypen in AD DS und resultierende Ansprüche, die in den zurückgegebenen Kerberos-Ticket enthält.  
  
4.  Wenn der durch den Benutzer/Client versucht, auf eine Ressource zuzugreifen, die acld die Ansprüche erforderlich ist, können sie die Ressource zugreifen, da der Verbund-ID, die von Kerberos angefügt wurde diese Ansprüche enthält.  
  
5.  Wenn der gleiche Client versucht, eine Website oder Anwendung zugreifen, die für die AD FS-Authentifizierung konfiguriert ist, wird der Benutzer zu einer AD FS-Verbundserver umgeleitet, die für die integrierte Windows-Authentifizierung konfiguriert ist. Der Client sendet eine Anforderung an den Domänencontroller mit Kerberos. Der Domänencontroller stellt ein Kerberos-Ticket, enthält die angeforderten Ansprüche, die der Client dann an den Verbundserver darstellen kann.  
  
6.  Basierend auf dem Weg, die die Regeln für Ansprüche auf den Anspruchsanbieter konfiguriert wurden, und der vertrauenden Seite Vertrauensstellungen, dass der Administrator konfigurierte, AD FS die Ansprüche von Kerberos-Tickets liest und schließt sie in ein SAML-Token, die für den Client ausgestellt.  
  
7.  Der Client erhält das SAML-Token, die richtigen Ansprüche enthält, und klicken Sie dann auf der Website weitergeleitet wird.  
  
Weitere Informationen zum Erstellen von der Anspruchsregeln erforderlich für ausgestellt AD DS-Ansprüche mit AD FS funktioniert, finden Sie unter [Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
