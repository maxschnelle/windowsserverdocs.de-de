---
ms.assetid: 204f5fe9-3611-4da0-b057-a386004b4598
title: Grundlegendes zu wichtigen Active Directory Federation Services-Konzepte
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 27282c6b88b0457af3b4cf031fdadced7b40268c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="understanding-key-ad-fs-concepts"></a>Grundlegendes zu wichtigen AD FS Concepts
Es wird empfohlen, dass Sie zu wichtigen Konzepten für Active Directory Federation Services Informationen und mit der entsprechenden Featuregruppe vertraut machen.  
  
> [!TIP]  
> Finden Sie weitere AD FS-Ressourcenlinks auf die [AD FS-Inhalte](https://social.technet.microsoft.com/wiki/contents/articles/2735.aspx) Seite auf der Microsoft TechNet-Wiki. Diese Seite wird von Mitgliedern der AD FS-Community verwaltet und regelmäßig vom der AD FS-Produktteam überprüft.  
  
## <a name="ad-fs-terminology-used-in-this-guide"></a>AD FS-Terminologie in dieser Anleitung  
  
|AD FS-Begriff|Definition|  
|--------------|--------------|  
|Kontopartnerorganisation|Eine verbundpartnerorganisation, die durch eine Anspruchsanbieter-Vertrauensstellung im Verbunddienst dargestellt wird. Die Kontopartnerorganisation enthält die Benutzer, die webbasierten Anwendungen im Ressourcenpartner zugreifen.|  
|Kontoverbundserver|Der Verbundserver in der Kontopartnerorganisation. Der Kontoverbundserver stellt Sicherheitstoken für Benutzer auf Basis der Benutzerauthentifizierung. Der Server authentifiziert den Benutzer, extrahiert die relevanten Attribute und Gruppenmitgliedschaftsinformationen aus dem Attributspeicher, verpackt diese Informationen in Ansprüche und generiert und signiert ein Sicherheitstoken \ (die enthält die Claims\), an den Benutzer zurück – entweder in der eigenen Organisation verwendet werden oder an eine Partnerorganisation gesendet werden.|  
|AD FS-Konfigurationsdatenbank|Eine Datenbank zum Speichern sämtlicher Konfigurationsdaten, die eine einzelne AD FS-Instanz oder einen Verbunddienst darstellt. Diese Konfigurationsdaten können in einer SQL Server-Datenbank gespeichert werden, oder verwenden das Feature Windows Internal Database mit Windows Server2016, Windows Server2012 und 2012 R2 und Windows Server2008 und 2008 R2 enthalten. </br></br>Sie können die AD FS-Konfigurationsdatenbank für SQL Server mithilfe der Fsconfig.exe-Befehlszeilentools und für die interne Windows-Datenbank mithilfe von AD FS Federation Server-Konfigurations-Assistenten erstellen.|  
|Anspruchsanbieter|Die Organisation, die Ansprüche für ihre Benutzer bereitstellt. Siehe Kontopartnerorganisation.|  
|Anspruchsanbieter-Vertrauensstellung|In AD FS-Verwaltungs-Snap-In sind Anspruchsanbieter-Vertrauensstellungen vertrauensstellungsobjekten in der Regel in ressourcenpartnerorganisationen, um die Organisation in der Vertrauensstellung darzustellen, deren Konten Ressourcen in der Ressourcenpartnerorganisation zugreifen werden, erstellt. Eine Anspruchsanbieter-Vertrauensstellungsobjekt besteht aus einer Vielzahl von IDs, Namen und Regeln, die diesen Partner für den lokalen Verbunddienst identifizieren.|  
|Lokales Anspruchsanbieter-Vertrauensstellung|Ein Vertrauensstellungsobjekt, das AD LDS oder Third\ von Drittanbietern LDAP\-basierte Verzeichnisse in einer AD FS-Farm darstellt. Ein lokales Anspruchsanbieter-Vertrauensstellungsobjekt besteht aus einer Vielzahl von IDs, Namen und Regeln, die diese LDAP\-basierte Verzeichnis für den lokalen Verbunddienst identifizieren.|  
|Verbundmetadaten|Das Datenformat für die Kommunikation zwischen einem Anspruchsanbieter und einer vertrauenden ordnungsgemäßen Konfiguration von Anspruchsanbieter-Vertrauensstellungen und Vertrauensstellungen der vertrauenden Seite zu erleichtern. Das Datenformat ist in Security Assertion Markup Language \(SAML\) 2.0 definiert und wird im WS-Verbund erweitert.|  
|Verbundserver|Ein Windows-Server, der mit AD FS Federation Server-Konfigurations-Assistenten konfigurieren die Verbundserverrolle konfiguriert wurde. Ein Verbundserver stellt Token und dient als Teil eines Verbunddiensts.|  
|Verbundserverproxy|Ein Windows-Server, der mit der AD FS-Konfigurationsassistenten für den Verbundserverproxy als fungieren konfiguriert wurde ein zwischengeschalteter Proxy-Service-zwischen Internetclient und Verbunddienst, der in einem Unternehmensnetzwerk hinter einer Firewall befindet.|  
|Primärer Verbundserver|Ein Windows-Server, der die Verbundserver-Rolle mithilfe von AD FS Federation Server-Konfigurations-Assistenten konfiguriert wurde und verfügt über eine Lese-/Schreibkopie der AD FS-Konfigurationsdatenbank. </br></br> Der primäre Verbundserver wird erstellt, wenn Sie AD FS Federation Server-Konfigurations-Assistenten verwenden, und wählen Sie die Option zum Erstellen eines neuen Verbunddiensts und dem Computer des ersten Verbundservers in der Farm machen. Alle anderen Verbundserver in dieser Farm müssen replizieren Änderungen auf dem primären Verbundserver auf eine schreibgeschützte Kopie der AD FS-Konfigurationsdatenbank, die lokal gespeichert wird. Der Begriff "primärer Verbundserver" trifft nicht auf, wenn die AD FS-Konfigurationsdatenbank in einer SQL-Datenbank gespeichert wird, da alle Verbundserver gleichermaßen lesen und einer Konfigurationsdatenbank gespeichert, die auf einem SQL Server schreiben können.|  
|Vertrauende Seite|Die Organisation, die Ansprüche erhält und verarbeitet. Siehe Ressourcenpartnerorganisation.|  
|Vertrauensstellung einer vertrauenden Seite|In AD FS-Verwaltungs-Snap-In werden der vertrauenden Seite Vertrauensstellungen vertrauensstellungsobjekten in der Regel erstellt:<br /><br />-Kontopartnerorganisationen Sie, um die Organisation in der Vertrauensstellung darzustellen, deren Konten auf Ressourcen in der Ressourcenpartnerorganisation zugreifen werden werden.<br />-Ressourcenpartnerorganisationen um die Vertrauensstellung zwischen Verbunddienst und eine einzelne webbasierte Anwendung darzustellen.<br /><br />Ein relying Party-Vertrauensstellungsobjekt besteht aus einer Vielzahl von IDs, Namen und Regeln, die diesen Partner oder Web\-Anwendung für den lokalen Verbunddienst identifizieren.|  
|Ressourcenverbundserver|Der Verbundserver in der Ressourcenpartnerorganisation. Der Ressourcenverbundserver stellt in der Regel Sicherheitstoken für Benutzer basierend auf einem Sicherheitstoken, die von einem Kontoverbundserver ausgestellt wurde. Der Server empfängt das Sicherheitstoken, überprüft die Signatur, wendet Anspruch Regel die Logik auf den nicht gepackten Ansprüche an die gewünschten ausgehenden Ansprüche zu erzeugen, generiert ein neues Sicherheitstoken \ (mit den ausgehenden Claims\) basierend auf den Informationen im eingehenden Sicherheitstoken, und der Benutzer wieder das neue Token signiert und schließlich auf die Webanwendung.|  
|Ressourcenpartnerorganisation|Ein Verbundpartner, der durch eine Vertrauensstellung der vertrauenden Seite im Verbunddienst dargestellt wird. Der Ressourcenpartner stellt Claims\-basierte Sicherheitstoken, die veröffentlichte webbasierte Anwendungen enthält, die Benutzer des Kontopartners zugreifen können.|  
  
## <a name="overview-of-ad-fs"></a>Übersicht über AD FS  
AD FS ist eine identitätszugriffslösung, die Clientcomputer enthält \ (innerhalb oder außerhalb der vom Netzwerk) mit nahtlosen SSO-Zugriff auf geschützte möglicherweise gerichteten Anwendungen oder Dienste, selbst wenn die Benutzerkonten und Anwendungen in ganz anderen Netzwerken oder Organisationen befinden.  
  
Wenn eine Anwendung oder ein Dienst befindet sich in einem Netzwerk und ein Benutzerkonto in einem anderen Netzwerk, wird in der Regel der Benutzer sekundärer Anmeldeinformationen aufgefordert, wenn er versucht, auf die Anwendung oder den Dienst zuzugreifen. Diese sekundären Anmeldeinformationen stellen die Identität des Benutzers in den Bereich, in dem die Anwendung oder der Dienst befindet. Sie sind in der Regel durch den Webserver erforderlich, die die Anwendung oder den Dienst hostet, damit sie die entsprechende Autorisierungsentscheidung vornehmen kann.  
  
Mit AD FS umgehen Organisationen Anforderungen sekundärer Anmeldeinformationen durch die Bereitstellung Vertrauensstellung Beziehungen \(federation trusts\), die diesen Organisationen verwenden können, um die Zugriffsrechte eines Benutzers digitale Identität und Zugriff auf vertrauenswürdige Partner zu projizieren. In dieser verbundumgebung kann jede Organisation weiterhin die eigenen Identitäten verwalten, jede Organisation jedoch auch sicher projizieren und Identitäten anderer Organisationen akzeptieren.  
  
-   [Die Rolle des Attributspeichers](The-Role-of-Attribute-Stores.md)  
  
-   [Die Rolle des AD FS-Konfigurationsdatenbank](The-Role-of-the-AD-FS-Configuration-Database.md)  
  
-   [Die Rolle von Ansprüchen](The-Role-of-Claims.md)  
  
-   [Die Rolle von Anspruchsregeln](The-Role-of-Claim-Rules.md)  
  
-   [Die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md)  
  
-   [Die Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md)  
  
-   [Die Rolle der Anspruchsregelsprache](The-Role-of-the-Claim-Rule-Language.md)  
  
-   [Bestimmen Sie die Art der Anspruchsregelvorlage verwenden](Determine-the-Type-of-Claim-Rule-Template-to-Use.md)  
  
-   [Wie werden die URIs in AD FS verwendet](How-URIs-Are-Used-in-AD-FS.md)  
  

