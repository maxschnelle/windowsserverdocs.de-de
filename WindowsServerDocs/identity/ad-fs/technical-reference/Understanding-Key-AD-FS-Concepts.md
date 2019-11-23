---
ms.assetid: 204f5fe9-3611-4da0-b057-a386004b4598
title: Grundlegendes zu Schlüssel Active Directory-Verbunddienste (AD FS) Konzepten
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d212c2f820204bae8e1e55dc1ebc44200e266a18
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407311"
---
# <a name="understanding-key-ad-fs-concepts"></a>Grundlegendes zu wichtigen AD FS-Konzepten
Es wird empfohlen, dass Sie sich mit den wichtigen Konzepten für Active Directory-Verbunddienste (AD FS) vertraut machen und sich mit dem Funktions Satz vertraut machen.  
  
> [!TIP]  
> Weitere Links zu AD FS 2.0-Ressourcen finden Sie im Microsoft TechNet-Wiki auf der Seite mit [AD FS 2.0-Inhalten](https://social.technet.microsoft.com/wiki/contents/articles/2735.aspx) . Diese Seite wird von Mitgliedern der AD FS-Community verwaltet und regelmäßig vom AD FS-Produktteam überprüft.  
  
## <a name="ad-fs-terminology-used-in-this-guide"></a>AD FS-Terminologie in dieser Anleitung  
  
|AD FS-Begriff|Definition|  
|--------------|--------------|  
|Kontopartnerorganisation|Eine Verbundpartnerorganisation, die durch eine Anspruchsanbieter-Vertrauensstellung im Verbunddienst dargestellt wird. Die Konto Partnerorganisation enthält die Benutzer, die auf auf Web\-basierende Anwendungen im Ressourcen Partner zugreifen.|  
|Kontoverbundserver|Der Verbundserver in der Kontopartnerorganisation. Der Kontoverbundserver stellt Sicherheitstoken für Benutzer auf Basis der Benutzerauthentifizierung aus. Der Server authentifiziert den Benutzer, extrahiert die relevanten Attribute und Gruppen Mitgliedschafts Informationen aus dem Attribut Speicher, verpackt diese Informationen in Ansprüche und generiert und signiert ein Sicherheits Token \(das die Ansprüche\) enthält, die an den Benutzer zurückgegeben werden sollen – entweder zur Verwendung in der eigenen Organisation oder zum Senden an eine Partnerorganisation.|  
|AD FS-Konfigurationsdatenbank|Eine Datenbank zum Speichern sämtlicher Konfigurationsdaten, die eine einzelne AD FS-Instanz oder einen Verbunddienst darstellen. Diese Konfigurationsdaten können entweder in einer SQL Server Datenbank oder mithilfe der internen Windows-Datenbankfunktion in Windows Server 2016, Windows Server 2012 und 2012 R2 sowie Windows Server 2008 und 2008 R2 gespeichert werden. </br></br>Sie können die AD FS Konfigurations Datenbank für SQL Server mithilfe des\-Befehls "fsconfig. exe" und der internen Windows-Datenbank mit dem Konfigurations-Assistenten für AD FS-Verbund Server erstellen.|  
|Anspruchsanbieter|Die Organisation, die Ansprüche für ihre Benutzer bereitstellt. Siehe Kontopartnerorganisation.|  
|Anspruchsanbieter-Vertrauensstellung|Im\-Snap-in "AD FS-Verwaltung" in werden Anspruchs Anbieter-Vertrauens Stellungen vertrauenswürdige Objekte, die in der Regel in Ressourcen Partnerorganisationen erstellt werden, um die Organisation in der Vertrauensstellung darzustellen, deren Konten auf Ressourcen in der Ressourcen Partnerorganisation zugreifen werden. Ein Anspruchsanbieter-Vertrauensstellungsobjekt besteht aus einer Auswahl von IDs, Namen und Regeln, die diesen Partner für den lokalen Verbunddienst identifizieren.|  
|Vertrauensstellung mit lokalem Anspruchsanbieter|Ein Vertrauensstellungs Objekt, das AD LDS oder Dritte\-LDAP-\-basierten Verzeichnisse in einer AD FS Farm darstellt. Ein lokales Anspruchs Anbieter-Vertrauensstellungs Objekt besteht aus einer Vielzahl von Bezeichnernamen, Namen und Regeln, die dieses LDAP-\-basierte Verzeichnis für den lokalen Verbunddienst identifizieren.|  
|Verbundmetadaten|Das Datenformat für die Kommunikation von Konfigurationsinformationen zwischen einem Anspruchsanbieter und einer vertrauenden Seite, um die geeignete Konfiguration von Anspruchsanbieter-Vertrauensstellungen und von Vertrauensstellungen der vertrauenden Seite zu ermöglichen. Das Datenformat wird in Security Assertion Markup Language \(SAML\) 2,0 definiert und in WS\-Federation erweitert.|  
|Verbundserver|Ein Windows-Server, der mithilfe des AD FS-Verbund Server-Konfigurations-Assistenten für die Verbund Server Rolle konfiguriert wurde. Ein Verbundserver stellt Token aus und dient als Komponente eines Verbunddiensts.|  
|Verbundserverproxy|Ein Windows-Server, der mithilfe des Konfigurations-Assistenten für den AD FS Verbund Server Proxy konfiguriert wurde, um als zwischengeschalteter Proxy Dienst zwischen einem Internet Client und einem Verbunddienst zu fungieren, der sich hinter einer Firewall in einem Unternehmensnetzwerk befindet.|  
|Primärer Verbundserver|Ein Windows-Server, der in der Verbund Server Rolle mithilfe des Konfigurations-Assistenten für den AD FS-Verbund Servers konfiguriert wurde und über eine Lese\/Schreib Kopie der AD FS Konfigurations Datenbank verfügt. </br></br> Der primäre Verbund Server wird erstellt, wenn Sie den Konfigurations-Assistenten für den AD FS-Verbund Server verwenden und die Option zum Erstellen eines neuen Verbunddienst auswählen und diesen Computer zum ersten Verbund Server in der Farm machen. Alle anderen Verbund Server in dieser Farm müssen Änderungen, die auf dem primären Verbund Server vorgenommen wurden, in eine Lese\-einzige Kopie der AD FS Konfigurations Datenbank replizieren, die lokal gespeichert wird. Der Begriff "primärer Verbundserver" trifft nicht zu, wenn die AD FS-Konfigurationsdatenbank in einer SQL-Datenbank gespeichert wird, da alle Verbundserver gleichermaßen aus einer Konfigurationsdatenbank lesen bzw. in diese schreiben können, die auf einem SQL Server gespeichert wird.|  
|Vertrauende Seite|Die Organisation, die Ansprüche erhält und verarbeitet. Siehe Ressourcenpartnerorganisation.|  
|Vertrauensstellung der vertrauenden Seite|Im\-Snap-in "AD FS Verwaltung" sind Vertrauens Stellungen der vertrauenden Seite Vertrauenswürdige Objekte, die in der Regel erstellt werden<br /><br />-Konto Partnerorganisationen, um die Organisation in der Vertrauensstellung darzustellen, deren Konten auf Ressourcen in der Ressourcen Partnerorganisation zugreifen werden.<br />-Ressourcen Partnerorganisationen zur Darstellung der Vertrauensstellung zwischen dem Verbunddienst und einer einzelnen auf Web\-basierenden Anwendung.<br /><br />Ein Vertrauensstellungs Objekt der vertrauenden Seite besteht aus einer Vielzahl von Bezeichnernamen, Namen und Regeln, die diesen Partner oder diese Web\-Anwendung für die lokale Verbunddienst identifizieren.|  
|Ressourcenverbundserver|Der Verbundserver in der Ressourcenpartnerorganisation. Der Ressourcenverbundserver stellt in der Regel Sicherheitstoken für Benutzer auf Basis eines Sicherheitstokens aus, das von einem Kontoverbundserver ausgestellt wurde. Der Server empfängt das Sicherheits Token, überprüft die Signatur und wendet die Anspruchs Regellogik auf die unverpackten Ansprüche an, um die gewünschten ausgehenden Ansprüche zu erzeugen, generiert ein neues Sicherheits Token \(mit den ausgehenden Ansprüchen\) basierend auf Informationen im eingehenden Sicherheits Token) und signiert das neue Token, um an den Benutzer und letztendlich an die Webanwendung zurückzukehren.|  
|Ressourcenpartnerorganisation|Ein Verbundpartner, der durch die Vertrauensstellung einer vertrauenden Seite im Verbunddienst dargestellt wird. Der Ressourcen Partner gibt Ansprüche\-basierten Sicherheits Token aus, die veröffentlichte, auf Web\-basierende Anwendungen enthalten, auf die Benutzer des Konto Partners zugreifen können.|  
  
## <a name="overview-of-ad-fs"></a>Übersicht über AD FS  
AD FS ist eine Identitäts Zugriffs Lösung, die Client Computern \(intern oder extern für Ihr Netzwerk bereitstellt\) mit nahtlosem SSO-Zugriff auf geschützte Internet\-Anwendungen oder Dienste, auch wenn sich die Benutzerkonten und Anwendungen in ganz anderen Netzwerken oder Organisationen befinden.  
  
Wenn sich eine Anwendung oder ein Dienst in einem Netzwerk und ein Benutzerkonto in einem anderen Netzwerk befindet, wird der Benutzer beim versuchten Zugriff auf die Anwendung oder den Dienst normalerweise zur Angabe sekundärer Anmeldeinformationen aufgefordert. Diese sekundären Anmeldeinformationen stellen die Identität des Benutzers in dem Bereich dar, in dem sich die Anwendung oder der Dienst befindet. Sie sind in der Regel für den Webserver erforderlich, der die Anwendung oder den Dienst hostet, daher kann er die entsprechende Autorisierungsentscheidung treffen.  
  
Mit AD FS können Organisationen Anforderungen für sekundäre Anmelde Informationen umgehen, indem Sie Vertrauens Stellungen \(Verbund Vertrauensstellungen\) bereitstellen, die diese Organisationen verwenden können, um die digitale Identität eines Benutzers und die Zugriffsrechte für vertrauenswürdige Partner zu projizieren. In dieser Verbundumgebung verwaltet jede Organisation weiterhin die eigenen Identitäten, aber die einzelnen Organisationen können auch Identitäten anderer Organisationen sicher planen und akzeptieren.  
  
-   [Die Rolle von Attribut speichern](The-Role-of-Attribute-Stores.md)  
  
-   [Rolle der AD FS-Konfigurationsdatenbank](The-Role-of-the-AD-FS-Configuration-Database.md)  
  
-   [Rolle von Ansprüchen](The-Role-of-Claims.md)  
  
-   [Rolle von Anspruchsregeln](The-Role-of-Claim-Rules.md)  
  
-   [Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md)  
  
-   [Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md)  
  
-   [Rolle der Anspruchsregelsprache](The-Role-of-the-Claim-Rule-Language.md)  
  
-   [Bestimmen des Typs der zu verwendenden Anspruchs Regel Vorlage](Determine-the-Type-of-Claim-Rule-Template-to-Use.md)  
  
-   [Verwenden von URIs in AD FS](How-URIs-Are-Used-in-AD-FS.md)  
  

