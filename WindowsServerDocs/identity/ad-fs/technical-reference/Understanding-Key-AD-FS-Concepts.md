---
ms.assetid: 204f5fe9-3611-4da0-b057-a386004b4598
title: Grundlegendes zu Schlüssel Active Directory-Verbunddienste (AD FS) Konzepten
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e7b204043f685343a32abebb868b441cbdfe37b8
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181786"
---
# <a name="understanding-key-ad-fs-concepts"></a>Understanding Key AD FS Concepts
Es wird empfohlen, dass Sie sich mit den wichtigen Konzepten für Active Directory-Verbunddienste (AD FS) vertraut machen und sich mit dem Funktions Satz vertraut machen.

> [!TIP]
> Weitere AD FS Ressourcen Verknüpfungen finden Sie Untergrund Legendes zu [Schlüssel AD FS Konzepten](https://docs.microsoft.com/windows-server/identity/ad-fs/technical-reference/understanding-key-ad-fs-concepts).

## <a name="ad-fs-terminology-used-in-this-guide"></a>AD FS-Terminologie in dieser Anleitung

|AD FS-Begriff|Definition|
|--------------|--------------|
|Kontopartnerorganisation|Eine Verbundpartnerorganisation, die durch eine Anspruchsanbieter-Vertrauensstellung im Verbunddienst dargestellt wird. Die Konto Partnerorganisation enthält die Benutzer, die auf webbasierte \- Anwendungen im Ressourcen Partner zugreifen werden.|
|Kontoverbundserver|Der Verbundserver in der Kontopartnerorganisation. Der Kontoverbundserver stellt Sicherheitstoken für Benutzer auf Basis der Benutzerauthentifizierung aus. Der Server authentifiziert den Benutzer, extrahiert die relevanten Attribute und Gruppen Mitgliedschafts Informationen aus dem Attribut Speicher, verpackt diese Informationen in Ansprüche und generiert und signiert ein Sicherheits Token, \( das die Ansprüche enthält, die \) an den Benutzer zurückgegeben werden sollen – entweder zur Verwendung in der eigenen Organisation oder zum Senden an eine Partnerorganisation.|
|AD FS-Konfigurationsdatenbank|Eine Datenbank zum Speichern sämtlicher Konfigurationsdaten, die eine einzelne AD FS-Instanz oder einen Verbunddienst darstellen. Diese Konfigurationsdaten können entweder in einer SQL Server Datenbank oder mithilfe der internen Windows-Datenbankfunktion in Windows Server 2016, Windows Server 2012 und 2012 R2 sowie Windows Server 2008 und 2008 R2 gespeichert werden. </br></br>Sie können die AD FS Konfigurations Datenbank für SQL Server mithilfe des Befehls \- Zeilen Tools Fsconfig.exe und für die interne Windows-Datenbank mit dem Konfigurations-Assistenten für AD FS-Verbund Server erstellen.|
|Anspruchsanbieter|Die Organisation, die Ansprüche für ihre Benutzer bereitstellt. Siehe Kontopartnerorganisation.|
|Anspruchsanbieter-Vertrauensstellung|Im Snap-in für die AD FS Verwaltung \- sind Anspruchs Anbieter-Vertrauens Stellungen vertrauenswürdige Objekte, die in der Regel in Ressourcen Partnerorganisationen erstellt werden, um die Organisation in der Vertrauensstellung darzustellen, deren Konten auf Ressourcen in der Ressourcen Partnerorganisation zugreifen werden. Ein Anspruchsanbieter-Vertrauensstellungsobjekt besteht aus einer Auswahl von IDs, Namen und Regeln, die diesen Partner für den lokalen Verbunddienst identifizieren.|
|Vertrauensstellung mit lokalem Anspruchsanbieter|Ein Vertrauensstellungs Objekt, das AD LDS oder \- LDAP-basierte Verzeichnisse von Drittanbietern \- in einer AD FS Farm darstellt. Ein lokales Anspruchs Anbieter-Vertrauensstellungs Objekt besteht aus einer Vielzahl von Bezeichnernamen, Namen und Regeln, die dieses LDAP- \- basierte Verzeichnis für den lokalen Verbunddienst identifizieren.|
|Verbundmetadaten|Das Datenformat für die Kommunikation von Konfigurationsinformationen zwischen einem Anspruchsanbieter und einer vertrauenden Seite, um die geeignete Konfiguration von Anspruchsanbieter-Vertrauensstellungen und von Vertrauensstellungen der vertrauenden Seite zu ermöglichen. Das Datenformat ist in Security Assertion Markup Language \( SAML \) 2,0 definiert und wird im WS-Verbund erweitert \- .|
|Verbundserver|Ein Windows-Server, der mithilfe des AD FS-Verbund Server-Konfigurations-Assistenten für die Verbund Server Rolle konfiguriert wurde. Ein Verbundserver stellt Token aus und dient als Komponente eines Verbunddiensts.|
|Verbundserverproxy|Ein Windows-Server, der mithilfe des Konfigurations-Assistenten für den AD FS Verbund Server Proxy konfiguriert wurde, um als zwischengeschalteter Proxy Dienst zwischen einem Internet Client und einem Verbunddienst zu fungieren, der sich hinter einer Firewall in einem Unternehmensnetzwerk befindet.|
|Primärer Verbundserver|Ein Windows-Server, der in der Verbund Server Rolle mithilfe des Konfigurations-Assistenten für den AD FS-Verbund Servers konfiguriert wurde und über eine Lese- \/ /Schreibkopie der AD FS Konfigurations Datenbank verfügt. </br></br> Der primäre Verbund Server wird erstellt, wenn Sie den Konfigurations-Assistenten für den AD FS-Verbund Server verwenden und die Option zum Erstellen eines neuen Verbunddienst auswählen und diesen Computer zum ersten Verbund Server in der Farm machen. Alle anderen Verbund Server in dieser Farm müssen die am primären Verbund Server vorgenommenen Änderungen in eine schreibgeschützte \- Kopie der AD FS Konfigurations Datenbank replizieren, die lokal gespeichert wird. Der Begriff "primärer Verbund Server" trifft nicht zu, wenn die AD FS Konfigurations Datenbank in einer SQL-Datenbank gespeichert wird, da alle Verbund Server gleichermaßen Lese-und Schreibzugriff auf eine Konfigurations Datenbank haben, die auf einem SQL Server gespeichert ist.|
|Vertrauende Seite|Die Organisation, die Ansprüche erhält und verarbeitet. Siehe Ressourcenpartnerorganisation.|
|Vertrauensstellung der vertrauenden Seite|Im Snap-in "AD FS-Verwaltung" \- sind Vertrauens Stellungen der vertrauenden Seite Vertrauens Objekte, die in der Regel in<p>-Konto Partnerorganisationen, um die Organisation in der Vertrauensstellung darzustellen, deren Konten auf Ressourcen in der Ressourcen Partnerorganisation zugreifen werden.<br />-Ressourcen Partnerorganisationen, die die Vertrauensstellung zwischen dem Verbunddienst und einer einzelnen \- webbasierten Anwendung darstellen.<p>Ein Vertrauensstellungs Objekt der vertrauenden Seite besteht aus einer Vielzahl von Bezeichnernamen, Namen und Regeln, die diesen Partner bzw \- . diese Webanwendung für die lokale Verbunddienst identifizieren.|
|Ressourcenverbundserver|Der Verbundserver in der Ressourcenpartnerorganisation. Der Ressourcenverbundserver stellt in der Regel Sicherheitstoken für Benutzer auf Basis eines Sicherheitstokens aus, das von einem Kontoverbundserver ausgestellt wurde. Der Server empfängt das Sicherheits Token, überprüft die Signatur und wendet die Anspruchs Regellogik auf die unverpackten Ansprüche an, um die gewünschten ausgehenden Ansprüche zu erzeugen, generiert ein neues Sicherheits Token \( mit den ausgehenden Ansprüchen auf der \) Grundlage der Informationen im eingehenden Sicherheits Token und signiert das neue Token, um an den Benutzer und letztendlich an die Webanwendung zurückzukehren.|
|Ressourcenpartnerorganisation|Ein Verbundpartner, der durch die Vertrauensstellung einer vertrauenden Seite im Verbunddienst dargestellt wird. Der Ressourcen Partner stellt Anspruchs \- basierte Sicherheits Token aus, die veröffentlichte webbasierte \- Anwendungen enthalten, auf die Benutzer des Konto Partners zugreifen können.|

## <a name="overview-of-ad-fs"></a>Übersicht über AD FS
Bei AD FS handelt es sich um eine Identitäts Zugriffs Lösung, die Client Computern \( mit internem \) SSO-Zugriff auf geschützte Anwendungen oder Dienste mit Internet Zugriff bereitstellt \- , auch wenn sich die Benutzerkonten und Anwendungen in ganz anderen Netzwerken oder Organisationen befinden.

Wenn sich eine Anwendung oder ein Dienst in einem Netzwerk und ein Benutzerkonto in einem anderen Netzwerk befindet, wird der Benutzer beim versuchten Zugriff auf die Anwendung oder den Dienst normalerweise zur Angabe sekundärer Anmeldeinformationen aufgefordert. Diese sekundären Anmeldeinformationen stellen die Identität des Benutzers in dem Bereich dar, in dem sich die Anwendung oder der Dienst befindet. Sie sind in der Regel für den Webserver erforderlich, der die Anwendung oder den Dienst hostet, daher kann er die entsprechende Autorisierungsentscheidung treffen.

Mit AD FS können Organisationen Anforderungen für sekundäre Anmelde Informationen umgehen, indem Sie Vertrauens Stellungen von Verbund Vertrauensstellungen bereitstellen \( \) , die diese Organisationen verwenden können, um die digitale Identität eines Benutzers und die Zugriffsrechte für vertrauenswürdige Partner zu projizieren. In dieser Verbundumgebung verwaltet jede Organisation weiterhin die eigenen Identitäten, aber die einzelnen Organisationen können auch Identitäten anderer Organisationen sicher planen und akzeptieren.

-   [Die Rolle von Attribut speichern](The-Role-of-Attribute-Stores.md)

-   [Rolle der AD FS-Konfigurationsdatenbank](The-Role-of-the-AD-FS-Configuration-Database.md)

-   [Rolle von Ansprüchen](The-Role-of-Claims.md)

-   [Rolle von Anspruchsregeln](The-Role-of-Claim-Rules.md)

-   [Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md)

-   [Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md)

-   [Rolle der Anspruchsregelsprache](The-Role-of-the-Claim-Rule-Language.md)

-   [Bestimmen des Typs der zu verwendenden Anspruchs Regel Vorlage](Determine-the-Type-of-Claim-Rule-Template-to-Use.md)

-   [Verwenden von URIs in AD FS](How-URIs-Are-Used-in-AD-FS.md)


