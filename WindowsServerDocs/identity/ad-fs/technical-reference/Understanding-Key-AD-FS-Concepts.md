---
ms.assetid: 204f5fe9-3611-4da0-b057-a386004b4598
title: Grundlegendes zum Schlüssel Active Directory-Verbund Services-Konzepte
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 27282c6b88b0457af3b4cf031fdadced7b40268c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878131"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="understanding-key-ad-fs-concepts"></a>Grundlegendes zu wichtigen AD FS-Konzepten
Es wird empfohlen, dass Sie weitere über die wichtigsten Konzepte für Active Directory Federation Services Informationen, und mit der entsprechenden Featuregruppe vertraut zu machen.  
  
> [!TIP]  
> Weitere Links zu AD FS 2.0-Ressourcen finden Sie im Microsoft TechNet-Wiki auf der Seite mit [AD FS 2.0-Inhalten](https://social.technet.microsoft.com/wiki/contents/articles/2735.aspx) . Diese Seite wird von Mitgliedern der AD FS-Community verwaltet und regelmäßig vom AD FS-Produktteam überprüft.  
  
## <a name="ad-fs-terminology-used-in-this-guide"></a>AD FS-Terminologie in dieser Anleitung  
  
|AD FS-Begriff|Definition|  
|--------------|--------------|  
|Kontopartnerorganisation|Eine Verbundpartnerorganisation, die durch eine Anspruchsanbieter-Vertrauensstellung im Verbunddienst dargestellt wird. Die Kontopartnerorganisation enthält die Benutzer, die Zugriff auf Web werden\--basierte Anwendungen in der Ressourcenpartnerorganisation.|  
|Kontoverbundserver|Der Verbundserver in der Kontopartnerorganisation. Der Kontoverbundserver stellt Sicherheitstoken für Benutzer auf Basis der Benutzerauthentifizierung aus. Der Server authentifiziert den Benutzer, extrahiert die relevanten Attribute und Gruppenmitgliedschaftsinformationen aus dem Attributspeicher, verpackt diese Informationen in Ansprüche und generiert und signiert ein Sicherheitstoken \(enthält die Ansprüche\)zur Rückgabe an den Benutzer – entweder in der eigenen Organisation verwendet werden oder an eine Partnerorganisation gesendet werden.|  
|AD FS-Konfigurationsdatenbank|Eine Datenbank zum Speichern sämtlicher Konfigurationsdaten, die eine einzelne AD FS-Instanz oder einen Verbunddienst darstellen. Diese Konfigurationsdaten können in einer SQL Server-Datenbank gespeichert werden, oder mithilfe der internen Windows-Datenbank-Funktion mit Windows Server 2016, Windows Server 2012 und 2012 R2 und Windows Server 2008 und 2008 R2 enthalten. </br></br>Sie können die AD FS-Konfigurationsdatenbank für SQL Server mithilfe des Befehls Fsconfig.exe erstellen\-Tools "Linie" und für die interne Windows-Datenbank mithilfe der AD FS Konfigurations-Assistenten.|  
|Anspruchsanbieter|Die Organisation, die Ansprüche für ihre Benutzer bereitstellt. Siehe Kontopartnerorganisation.|  
|Anspruchsanbieter-Vertrauensstellung|Im AD FS-Verwaltungs-Snap-\-in die Anspruchsanbieter-Vertrauensstellungen vertrauensstellungsobjekten in der Regel erstellt werden, in ressourcenpartnerorganisationen, um die Organisation in der Vertrauensstellung darzustellen, deren Konten auf zugreifen werden Ressourcen in der Ressource die Organisation. Ein Anspruchsanbieter-Vertrauensstellungsobjekt besteht aus einer Auswahl von IDs, Namen und Regeln, die diesen Partner für den lokalen Verbunddienst identifizieren.|  
|Vertrauensstellung mit lokalem Anspruchsanbieter|Ein Vertrauensstellungsobjekt, das AD LDS oder dritte darstellt\-Partei LDAP\-basierten Verzeichnissen in einer AD FS-Farm. Ein lokales Anspruchsanbieter-Vertrauensstellung Objekt besteht aus einer Vielzahl von IDs, Namen und Regeln, die dieses LDAP identifizieren\-basierten Verzeichnisses für den lokalen Verbunddienst.|  
|Verbundmetadaten|Das Datenformat für die Kommunikation von Konfigurationsinformationen zwischen einem Anspruchsanbieter und einer vertrauenden Seite, um die geeignete Konfiguration von Anspruchsanbieter-Vertrauensstellungen und von Vertrauensstellungen der vertrauenden Seite zu ermöglichen. Das Datenformat ist in der Security Assertion Markup Language definiert \(SAML\) 2.0, und es wird im WS erweitert\-Verbund.|  
|Verbundserver|Ein Windows-Server, der mit der AD FS Konfigurations-Assistenten, die in der Verbundserver-Rolle verwendet konfiguriert wurde. Ein Verbundserver stellt Token aus und dient als Komponente eines Verbunddiensts.|  
|Verbundserverproxy|Ein Windows-Server, der mit der AD FS-Proxy Konfigurations-Assistenten als fungieren konfiguriert wurde ein zwischengeschalteter Proxy-service zwischen Internetclient und Verbunddienst, der in einem Unternehmensnetzwerk hinter einer Firewall befindet.|  
|Primärer Verbundserver|Ein Windows-Server, die Verbundserver-Rolle mithilfe der AD FS Konfigurations-Assistenten konfiguriert wurde, und verfügt über ein Lesevorgang\/Kopie der AD FS-Konfigurationsdatenbank zu schreiben. </br></br> Der primäre Verbundserver wird erstellt, wenn Sie die AD FS Konfigurations-Assistenten verwenden, und wählen Sie die Option zum Erstellen eines neuen Verbunddiensts und dem Computer des ersten Verbundservers in der Farm machen. Alle anderen Verbundserver in dieser Farm müssen am lesen die primären Verbundserver vorgenommenen Änderungen replizieren\-nur die Kopie der AD FS-Konfigurationsdatenbank, die lokal gespeichert ist. Der Begriff "primärer Verbundserver" trifft nicht zu, wenn die AD FS-Konfigurationsdatenbank in einer SQL-Datenbank gespeichert wird, da alle Verbundserver gleichermaßen aus einer Konfigurationsdatenbank lesen bzw. in diese schreiben können, die auf einem SQL Server gespeichert wird.|  
|Vertrauende Seite|Die Organisation, die Ansprüche erhält und verarbeitet. Siehe Ressourcenpartnerorganisation.|  
|Vertrauensstellung der vertrauenden Seite|Im AD FS-Verwaltungs-Snap-\-in Vertrauensstellungen der vertrauenden Seite vertrauensstellungsobjekte in der Regel erstellt werden:<br /><br />-Kontopartnerorganisationen Sie, um die Organisation in der Vertrauensstellung darzustellen, deren Konten auf Ressourcen in der Ressourcenpartnerorganisation zugegriffen werden.<br />-Ressourcenpartnerorganisationen zur Darstellung der Vertrauensstellung zwischen Verbunddienst und eine einzelne Web\--basierten Anwendung.<br /><br />Eine Partei-Vertrauensstellungsobjekt besteht aus einer Vielzahl von IDs, Namen und Regeln, die diesen Partner oder eine Web identifizieren\-Anwendung auf den lokalen Verbunddienst.|  
|Ressourcenverbundserver|Der Verbundserver in der Ressourcenpartnerorganisation. Der Ressourcenverbundserver stellt in der Regel Sicherheitstoken für Benutzer auf Basis eines Sicherheitstokens aus, das von einem Kontoverbundserver ausgestellt wurde. Der Server empfängt das Sicherheitstoken, überprüft die Signatur, die Ansprüche entpackt, um die gewünschten ausgehenden Ansprüche zu erzeugen Logik für die Regel gilt, generiert ein neues Sicherheitstoken \(mit den ausgehenden Ansprüchen\) basierend auf Informationen im eingehenden Sicherheitstoken und zur Rückgabe an den Benutzer das neue Token signiert und schließlich an die Webanwendung.|  
|Ressourcenpartnerorganisation|Ein Verbundpartner, der durch die Vertrauensstellung einer vertrauenden Seite im Verbunddienst dargestellt wird. Der Ressourcenpartner stellt Ansprüche\-basierten Sicherheitstoken, die veröffentlichte Web enthält\--basierte Anwendungen die Benutzer des Kontopartners zugreifen können.|  
  
## <a name="overview-of-ad-fs"></a>Übersicht über AD FS  
AD FS ist eine identitätszugriffslösung, die Client-Computern bietet \(innerhalb oder außerhalb Ihres Netzwerks\) nahtlosen SSO-Zugriff auf geschützte Internet\-mit Internetzugriff, Anwendungen oder Dienste, auch wenn die Benutzerkonten und Anwendungen werden in ganz anderen Netzwerken oder Organisationen befinden.  
  
Wenn sich eine Anwendung oder ein Dienst in einem Netzwerk und ein Benutzerkonto in einem anderen Netzwerk befindet, wird der Benutzer beim versuchten Zugriff auf die Anwendung oder den Dienst normalerweise zur Angabe sekundärer Anmeldeinformationen aufgefordert. Diese sekundären Anmeldeinformationen stellen die Identität des Benutzers in dem Bereich dar, in dem sich die Anwendung oder der Dienst befindet. Sie sind in der Regel für den Webserver erforderlich, der die Anwendung oder den Dienst hostet, daher kann er die entsprechende Autorisierungsentscheidung treffen.  
  
Mit AD FS Organisationen Anforderungen sekundärer Anmeldeinformationen durch die Bereitstellung von Vertrauensstellungen umgehen \(Verbundvertrauensstellungen\) , dass diese Organisationen verwenden können, um die Zugriffsrechte eines Benutzers digitale Identität und Zugriff auf vertrauenswürdige Projekt Partner. In dieser Verbundumgebung verwaltet jede Organisation weiterhin die eigenen Identitäten, aber die einzelnen Organisationen können auch Identitäten anderer Organisationen sicher planen und akzeptieren.  
  
-   [Die Rolle des Attributspeichers](The-Role-of-Attribute-Stores.md)  
  
-   [Die Rolle der AD FS-Konfigurationsdatenbank](The-Role-of-the-AD-FS-Configuration-Database.md)  
  
-   [Die Rolle von Ansprüchen](The-Role-of-Claims.md)  
  
-   [Die Rolle von Anspruchsregeln](The-Role-of-Claim-Rules.md)  
  
-   [Die Rolle der Anspruchs-Engine](The-Role-of-the-Claims-Engine.md)  
  
-   [Die Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md)  
  
-   [Die Rolle der Anspruchsregelsprache](The-Role-of-the-Claim-Rule-Language.md)  
  
-   [Bestimmen Sie den Typ der Anspruchsregelvorlage verwenden](Determine-the-Type-of-Claim-Rule-Template-to-Use.md)  
  
-   [Wie werden URIs in AD FS verwendet](How-URIs-Are-Used-in-AD-FS.md)  
  

