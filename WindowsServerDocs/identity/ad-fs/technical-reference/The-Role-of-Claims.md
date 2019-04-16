---
ms.assetid: 22f53391-8c6a-4873-a1f4-08b4760ea621
title: "Die Rolle von Ansprüchen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 98765deaba67ffdc0ee18b6d8ef573e531d739cc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="the-role-of-claims"></a>Die Rolle von Ansprüchen
In der Claims\-basierte Identitätsmodell spielen Ansprüche eine Schlüsselrolle im Verbund-Prozess, jedoch die Schlüsselkomponente, nach denen die Ergebnisse aller webbasierten Authentifizierungs- und Anfragen bestimmt sind. Dieses Modell ermöglicht es Organisationen, digitale Identitäten und Bezugsrechte sicher zu projizieren oder *Ansprüche*, über Sicherheits- und Unternehmensgrenzen in eine standardisierte Methode.  
  
## <a name="what-are-claims"></a>Was sind Ansprüche?  
In seiner einfachsten Form sind Ansprüche einfach *Anweisungen* \ (z.B. name, Identität, Group\), versucht zu Benutzern, die hauptsächlich zur Autorisierung des Zugriffs auf Claims\-basierte Anwendungen, die an einer beliebigen Stelle im Internet befinden. Jede Aussage entspricht einem *Wert* im Anspruch gespeichert wird.  
  
### <a name="how-claims-are-sourced"></a>Belegen von Ansprüchen  
Der Verbunddienst in Active Directory Federation Services \(AD FS\) definiert, welche Ansprüche zwischen Verbundpartnern ausgetauscht werden. Jedoch, bevor sie dies tun kann es muss zunächst Auffüllen oder source den Anspruch mit einem abgerufenen oder berechneten Wert. Jeder Anspruchswert stellt einen Wert von einem Benutzer, die Gruppe oder die Entität und auf zwei Arten zugegriffen werden konnte:  
  
1.  Beim Abrufen des Werts, der den Anspruch bildet aus einem Attributspeicher, z.B. wenn ein Attributwert der Vertriebsabteilung aus den Eigenschaften eines Active Directory-Benutzerkontos abgerufen werden. Weitere Informationen finden Sie unter [der Rolle des Attributspeichers](The-Role-of-Attribute-Stores.md).  
  
2.  Wenn der Wert eines eingehenden Anspruchs in einen anderen Wert auf der Grundlage der Logik in einer Regel ausgedrückt umgewandelt wird. Z.B. werden ein eingehender Anspruch mit dem Wert der Domänen-Admins umgewandelt in einen neuen Wert der Administratoren, bevor sie als ausgehender Anspruch gesendet wird. Weitere Informationen finden Sie unter [The Role of Claim Rules](The-Role-of-Claim-Rules.md).  
  
Ansprüche können Werte wie z.B. eine E\-Mail-Adresse, \(UPN\) User Principal Name, Gruppenmitgliedschaften und andere Attribute enthalten.  
  
### <a name="how-claims-flow"></a>Verlauf von Ansprüchen  
Andere Parteien sind abhängig von der Werte der Ansprüche Autorisierung für webbasierte Anwendungen ausführen, die sie hosten. Diese Parteien werden als bezeichnet *vertrauende Seiten* in AD FS-Verwaltungs-Snap-In. Der Verbunddienst ist für die Vermittlung der Vertrauensstellung zwischen vielen verschiedenartigen Parteien zuständig. Es dient zum Verarbeiten und den vertrauenswürdigen Austausch von Ansprüchen zwischen einer Organisation, die anfänglich, die Ansprüche, die Datenquellen so genannte flow *Ansprüche Anbieter* in der AD FS-Snap-In, um eine vertrauende Seite. Eine vertrauende Seite verwendet diese Ansprüche dann zum treffen von Autorisierungsentscheidungen.  
  
Der Fluss der Ansprüche, die mit diesem Vorgang wird als bezeichnet die *anspruchspipeline*. Den anspruchsverlauf in der anspruchspipeline umfasst drei Schritte:  
  
1.  Die Ansprüche, die vom Anspruchsanbieter empfangen werden, werden vom akzeptanztransformationsregeln auf die Anspruchsanbieter-Vertrauensstellung verarbeitet. Diese Regeln bestimmen, welche Ansprüche vom Anspruchsanbieter akzeptiert werden.  
  
2.  Die Ausgabe der akzeptanztransformationsregeln wird als Eingabe für die Ausstellungsautorisierungsregeln verwendet. Diese Regeln bestimmen, ob der Benutzer berechtigt ist, auf die vertrauende Seite zugreifen.  
  
3.  Die Ausgabe der akzeptanztransformationsregeln wird als Eingabe für die ausstellungstransformationsregeln verwendet. Diese Regeln bestimmen die Ansprüche, die auf die vertrauende Seite gesendet werden.  
  
Weitere Informationen finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md)  
  
### <a name="how-claims-are-issued"></a>Ausstellen von Ansprüchen  
Beim Schreiben von Anspruchsregeln hängt die Quelle der eingehenden Ansprüche für die Anspruchsregeln abhängig, ob Sie Regeln auf eine Anspruchsanbieter-Vertrauensstellung oder eine Vertrauensstellung der vertrauenden Seite schreiben. Wenn Sie Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung erstellen, entsprechen die eingehenden Ansprüche vom vertrauenswürdigen Anspruchsanbieter an den Verbunddienst gesendeten Ansprüche. Wenn Sie Regeln für eine Vertrauensstellung der vertrauenden Seite erstellen, entsprechen die eingehenden Ansprüche den Ansprüchen, die von den Anspruchsregeln der der maßgeblichen Anspruchsanbieter-Vertrauensstellung ausgegeben werden. Weitere Informationen zu eingehenden und ausgehenden Ansprüchen finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md) und [The Role of the Claims Engine ](The-Role-of-the-Claims-Engine.md).  
  
## <a name="what-are-claim-types"></a>Was sind Anspruchstypen?  
Ein Anspruchstyp stellt Kontext für den Anspruchswert bereit. Es wird in der Regel als ein Uniform Resource Identifier \(URI\) ausgedrückt. AD FS können beliebige Anspruchstypen unterstützt, und es ist standardmäßig mit den Anspruchstypen in der folgenden Tabelle konfiguriert.  
  
|Name|Beschreibung|URI|  
|--------|---------------|-------|  
|E\ E-Mail-Adresse|Die E\-Mail-Adresse des Benutzers|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/EmailAddress|  
|Vorname|Der Vorname des Benutzers|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/givenName|  
|Name|Der eindeutige Name des Benutzers|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/Name|  
|UPN|Das Benutzerprinzipalnamen Namen \(UPN\) des Benutzers|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/UPN|  
|Allgemeiner Name|Der allgemeine Name des Benutzers|http:///\/schemas.xmlsoap.org\/claims\/CommonName|  
|AD FS 1.x-E\-Mail-Adresse|Die E\-Mail-Adresse des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|http:///\/schemas.xmlsoap.org\/claims\/EmailAddress|  
|Gruppe|Eine Gruppe, der der Benutzer Mitglied ist|http:///\/schemas.xmlsoap.org\/claims\/Group|  
|AD FS 1.x UPN|Der UPN des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|http:///\/schemas.xmlsoap.org\/claims\/UPN|  
|Rolle|Eine Rolle, die der Benutzer verfügt|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/Role|  
|Nachname|Der Nachname des Benutzers|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/Surname|  
|PPID|Private ID des Benutzers|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/privatepersonalidentifier|  
|Namens-ID|SAML-Namensbezeichner des Benutzers|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/NameIdentifier|  
|Authentifizierungsmethode|Die Methode zum Authentifizieren des Benutzers|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/AuthenticationMethod|  
|Verweigern nur Gruppen-SID|Die Deny\ nur Gruppen-SID des Benutzers|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/denyonlysid|  
|Nur primäre SID verweigern|Deny\ nur primäre SID des Benutzers|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/denyonlyprimarysid|  
|Nur primäre Gruppen-SID verweigern|Deny\ nur primäre Gruppen-SID des Benutzers|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/denyonlyprimarygroupsid|  
|Gruppen-SID|Die Gruppen-SID des Benutzers|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/groupsid|  
|Primäre Gruppen-SID|Primäre Gruppen-SID des Benutzers|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/primarygroupsid|  
|Primäre SID|Die primäre SID des Benutzers|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/primarysid|  
|Windows-Kontoname|Domänenkontenname des Benutzers in Form von <domain>\\<user>|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/windowsaccountname|  
  
## <a name="what-are-claim-descriptions"></a>Was sind anspruchsbeschreibungen?  
Anspruchsbeschreibungen stellen eine Liste der Ansprüche, dass AD FS unterstützt und in den Verbundmetadaten veröffentlicht werden kann. In der obigen Tabelle aufgeführten Anspruchstypen werden als anspruchsbeschreibungen in AD FS-Verwaltungs-Snap-In konfiguriert.  
  
Die Sammlung der anspruchsbeschreibungen, die Verbundmetadaten veröffentlicht wird, wird in der AD FS-Konfigurationsdatenbank gespeichert. Diese Ansprüche Beschreibungen von verschiedenen Komponenten des Verbunddiensts verwendet werden.  
  
Jede anspruchsbeschreibung umfasst einen Anspruchstyp-URI, einen Namen, eine Veröffentlichungsstatus und eine Beschreibung. Sie können die Sammlung verwalten, mit der **Anspruchsbeschreibungen** Knoten in AD FS-Verwaltungs-Snap-In. Sie können den Veröffentlichungsstatus einer anspruchsbeschreibung über das Snap-In ändern. Die folgenden Einstellungen sind verfügbar:  
  
-   **Diesen Anspruch in Verbundmetadaten als Anspruchstyp, die diesem Verbunddienst akzeptiert veröffentlichen** \(Publish as Accepted\) – gibt die Anspruchstypen an, die von diesem Verbunddienst von anderen Anspruchsanbietern akzeptiert werden.  
  
-   **Diesen Anspruch in Verbundmetadaten als Anspruchstyp, die diesem Verbunddienst senden können veröffentlichen** \(Publish as Sent\) – gibt die Anspruchstypen an, die von diesem Verbunddienst angeboten werden. Dies sind die Anspruchstypen, die den Verbunddienst für andere veröffentlicht werden, die sich senden kann. Die tatsächlichen, vom Anspruchsanbieter gesendeten Anspruchstypen sind häufig eine Teilmenge dieser Liste.  
  
Weitere Informationen zur Vorgehensweise beim Festlegen des Veröffentlichungsstatus von Anspruchstypen finden Sie unter [Hinzufügen einer Anspruchsbeschreibung](https://technet.microsoft.com/library/dd807051.aspx) in AD FS-Bereitstellungshandbuch.  
  
### <a name="when-generating-federation-metadata"></a>Beim Erstellen von Metadaten Föderation  
Verbundmetadaten umfassen alle anspruchsbeschreibungen, die für die Veröffentlichung markiert sind.  
  
### <a name="when-claims-rules-are-processed"></a>Beim Verarbeiten von Anspruchsregeln  
Wenn Sie Konfigurationsinformationen zu anspruchsbeschreibungen beibehalten, ist es einfacher für Sie Regeln für Ansprüche zu konfigurieren. Weitere Informationen zu den Anspruchsregeln, die in der anspruchsanbieterorganisation verwendet werden können, finden Sie unter [der Rolle der Anspruchsregeln ](The-Role-of-Claim-Rules.md).  
  

