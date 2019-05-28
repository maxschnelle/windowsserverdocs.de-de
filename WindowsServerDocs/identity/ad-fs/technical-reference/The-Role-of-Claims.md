---
ms.assetid: 22f53391-8c6a-4873-a1f4-08b4760ea621
title: Rolle von Ansprüchen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 542d7a24e29b52dd3fa0d7ea6a9b2d27fb620d8d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188505"
---
# <a name="the-role-of-claims"></a>Rolle von Ansprüchen
In den Ansprüchen\-basierend Identitätsmodell spielen Ansprüche eine Schlüsselrolle im verbundprozess, sie sind der Schlüsselkomponente, mit dem das Ergebnis aller\-basierende der Authentifizierung und Autorisierung Anforderungen bestimmt werden. Dieses Modell ermöglicht es Organisationen, digitale Identitäten und Bezugsrechte bzw. *Ansprüche* über Sicherheits- und Unternehmensgrenzen hinweg auf standardisierte Weise sicher zu planen.  
  
## <a name="what-are-claims"></a>Was sind Ansprüche?  
In seiner einfachsten Form sind Ansprüche einfach *Anweisungen* \(z. B. Name, Identität, Gruppe\), wurden Benutzer, die verwendet werden, in erster Linie für die Autorisierung des Zugriffs auf Ansprüche\--basierte Anwendungen befindet sich eine beliebige Stelle, auf das Internet. Jede Aussage entspricht einem *Wert*, der im Anspruch gespeichert wird.  
  
### <a name="how-claims-are-sourced"></a>Belegen von Ansprüchen  
Der Verbunddienst in Active Directory-Verbunddienste \(AD FS\) definiert, welche Ansprüche zwischen Verbundpartnern ausgetauscht werden. Dazu muss der Anspruch zunächst mit einem abgerufenen oder berechneten Wert ausgefüllt oder belegt werden. Jeder Anspruchswert stellt einen Wert eines Benutzers, einer Gruppe oder Entität dar und es gibt zwei Möglichkeiten, um diesen zu belegen:  
  
1.  Der Wert, der den Anspruch bildet, wird aus einem Attributspeicher abgerufen, z. B. kann ein Attributwert der Vertriebsabteilung aus den Eigenschaften eines Active Directory-Benutzerkontos abgerufen werden. Weitere Informationen finden Sie unter [Rolle des Attributspeichers](The-Role-of-Attribute-Stores.md).  
  
2.  Der Wert eines eingehenden Anspruchs wird auf Basis der in einer Regel angegebenen Logik in einen anderen Wert transformiert. Wenn z. B. ein eingehender Anspruch mit dem Wert "Domänenadministratoren" in den neuen Wert "Administratoren" transformiert wird, bevor dieser als ausgehender Anspruch gesendet wird. Weitere Informationen finden Sie unter [Rolle von Anspruchsregeln](The-Role-of-Claim-Rules.md).  
  
Ansprüche können Werte wie z. B. eine e einschließen\-e-Mail-Adresse, Benutzerprinzipalname \(UPN\), Gruppenmitgliedschaft und andere Kontoattribute.  
  
### <a name="how-claims-flow"></a>Verlauf von Ansprüchen  
Andere Parteien basieren auf den Werten von Forderungen an den Authorization-Aufgaben für das Web\--basierte Anwendungen, die sie hosten. Diese Parteien werden als bezeichnet *vertrauende Seiten* im AD FS-Verwaltungs-Snap-\-in. Der Verbunddienst ist für die Vermittlung der Vertrauensstellung zwischen vielen verschiedenartigen Parteien zuständig. Es dient zum Verarbeiten und zu steuern den vertrauenswürdigen Austausch von Ansprüchen zwischen einer Organisation, das die Ansprüche, die so genannte anfänglich als Quelle *Ansprüche Anbieter* im AD FS-Verwaltungs-Snap-\-in an einen Identitätsempfänger. Eine vertrauende Seite verwendet diese Ansprüche dann zum Treffen von Autorisierungsentscheidungen.  
  
Der diesen Prozess verwendende Anspruchsverlauf wird als *Anspruchspipeline* bezeichnet. Der Anspruchsverlauf durch die Anspruchspipeline umfasst drei Schritte:  
  
1.  Die vom Anspruchsanbieter empfangenen Ansprüche werden mit Akzeptanztransformationsregeln der Vertrauensstellung des Anspruchsanbieters verarbeitet. Diese Regeln bestimmen, welche Ansprüche vom Anspruchsanbieter akzeptiert werden.  
  
2.  Die Ausgabe der Akzeptanztransformationsregeln wird als Eingabe für die Ausstellungsautorisierungsregeln verwendet. Diese Regeln bestimmen, ob dem Benutzer der Zugriff auf die vertrauende Seite gestattet ist.  
  
3.  Die Ausgabe der Akzeptanztransformationsregeln wird als Eingabe für die Ausstellungstransformationsregeln verwendet. Diese Regeln bestimmen die Ansprüche, die an die vertrauende Seite gesendet werden.  
  
Weitere Informationen finden Sie unter [Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md).  
  
### <a name="how-claims-are-issued"></a>Ausstellen von Ansprüchen  
Beim Erstellen von Anspruchsregeln hängt die Quelle der eingehenden Ansprüche für die Anspruchsregeln davon ab, ob Sie die Regeln für die Vertrauensstellung eines Anspruchsanbieters oder einer vertrauenden Seite erstellen. Wenn Sie Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung erstellen, entsprechen die eingehenden Ansprüche den Ansprüchen, die vom vertrauenswürdigen Anspruchsanbieter an den Verbunddienst gesendet werden. Wenn Sie Regeln für die Vertrauensstellung der vertrauenden Seite erstellen, entsprechen die eingehenden Ansprüche den Ansprüchen, die von den Anspruchsregeln der maßgeblichen Anspruchsanbieter-Vertrauensstellung ausgegeben werden. Weitere Informationen zu ein- und ausgehenden Ansprüchen finden Sie unter [Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md) und [Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md).  
  
## <a name="what-are-claim-types"></a>Was sind Anspruchstypen?  
Ein Anspruchstyp stellt den Kontext für den Anspruchswert bereit. Es wird in der Regel als ein Uniform Resource Identifier \(URI\). AD FS können beliebige Anspruchstypen unterstützt, und mit den Anspruchstypen in der folgenden Tabelle wird standardmäßig konfiguriert ist.  
  
|Name|Beschreibung|URI|  
|--------|---------------|-------|  
|E\-e-Mail-Adresse|Das e\-e-Mail-Adresse des Benutzers|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/emailaddress|  
|Angegebener Name|Angegebener Name des Benutzers|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/Identität\/Ansprüche\/"givenName"|  
|Name|Eindeutiger Name des Benutzers|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/Identität\/Ansprüche\/Name|  
|UPN|Der Benutzerprinzipalname \(UPN\) des Benutzers|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/upn|  
|Allgemeiner Name|Allgemeiner Name des Benutzers|http:\/\/schemas.xmlsoap.org\/Ansprüche\/CommonName|  
|AD FS 1.x E\-e-Mail-Adresse|Das e\-e-Mail-Adresse des Benutzers, bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|http:\/\/schemas.xmlsoap.org\/Ansprüche\/e-Mail-Adresse|  
|Gruppieren|Eine Gruppe, in der der Benutzer Mitglied ist|http:\/\/schemas.xmlsoap.org\/Ansprüche\/Gruppe|  
|AD FS 1.x UPN|UPN des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|http:\/\/schemas.xmlsoap.org\/Ansprüche\/UPN|  
|Role-Eigenschaft|Eine Rolle, über die der Benutzer verfügt|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/role|  
|Nachname|Nachname des Benutzers|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/Identität\/Ansprüche\/Nachname|  
|PPID|Private ID des Benutzers|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/privatepersonalidentifier|  
|Namensbezeichner|SAML-Namensbezeichner des Benutzers|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/nameidentifier|  
|Authentifizierungsmethode|Zur Authentifizierung des Benutzers verwendete Methode|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/authenticationmethod|  
|Nur Gruppen-SID verweigern|Deny\-nur Gruppen-SID des Benutzers|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/denyonlysid|  
|Nur primäre SID verweigern|Deny\-nur primäre SID des Benutzers|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/denyonlyprimarysid|  
|Nur primäre Gruppen-SID verweigern|Deny\-nur primäre Gruppen-SID des Benutzers|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/denyonlyprimarygroupsid|  
|Gruppen-SID|Die Gruppen-SID des Benutzers|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/groupsid|  
|Primäre Gruppen-SID|Primäre Gruppen-SID des Benutzers|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/primarygroupsid|  
|Primäre SID|Primäre SID des Benutzers|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/primarysid|  
|Windows-Kontoname|Das Domänenkonto des Benutzers in Form von \<Domäne\>\\\<Benutzer\>|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/windowsaccountname|  
  
## <a name="what-are-claim-descriptions"></a>Was sind Anspruchsbeschreibungen?  
Anspruchsbeschreibungen stellen dar, eine Liste der Anspruchstypen, dass AD FS unterstützt und in den Verbundmetadaten veröffentlicht werden können. In der vorherigen Tabelle aufgeführten Anspruchstypen werden konfiguriert, als die AD FS-Verwaltungs-Snap anspruchsbeschreibungen\-in.  
  
Die in Verbundmetadaten veröffentlichte Sammlung von Anspruchsbeschreibungen wird in der AD FS-Konfigurationsdatenbank gespeichert. Diese Anspruchsbeschreibungen werden von verschiedenen Komponenten des Verbunddiensts verwendet.  
  
Jede Anspruchsbeschreibung umfasst einen Anspruchstyp-URI, einen Namen, den Veröffentlichungsstatus und eine Beschreibung. Sie können die Sammlung der verwalten, mit der **Anspruchsbeschreibungen** Knoten in der AD FS-Verwaltungs-Snap\-in. Sie können den Veröffentlichungsstatus einer anspruchsbeschreibung, die mit dem Snap-in ändern\-in. Die folgenden Einstellungen sind verfügbar:  
  
-   **Dieser Anspruch in Verbundmetadaten als Anspruchstyp, der diesem Verbunddienst akzeptiert veröffentlichen** \(als "akzeptiert" Veröffentlichen\)– gibt die Anspruchstypen an, die von diesen Verbunddienst von anderen Anspruchsanbietern akzeptiert werden -Dienst.  
  
-   **Dieser Anspruch in Verbundmetadaten als Anspruchstyp, der diesem Verbunddienst gesendet werden können veröffentlichen** \(als "gesendet" Veröffentlichen\)– gibt die Anspruchstypen an, die von diesem Verbunddienst angeboten werden. Dies sind die Anspruchstypen, die vom Verbunddienst für andere veröffentlicht werden, da er bereit ist, diese zu senden. Die tatsächlich vom Anspruchsanbieter gesendeten Anspruchstypen sind häufig eine Teilmenge dieser Liste.  
  
Weitere Informationen zum Festlegen des Veröffentlichungsstatus von Anspruchstypen finden Sie unter [Hinzufügen einer Anspruchsbeschreibung](https://technet.microsoft.com/library/dd807051.aspx) in AD FS-Bereitstellungshandbuch.  
  
### <a name="when-generating-federation-metadata"></a>Beim Generieren von Verbundmetadaten  
Verbundmetadaten umfassen alle Anspruchsbeschreibungen, die für die Veröffentlichung markiert sind.  
  
### <a name="when-claims-rules-are-processed"></a>Beim Verarbeiten von Anspruchsregeln  
Wenn Sie Konfigurationsinformationen zu Anspruchsbeschreibungen beibehalten, ist es einfacher für Sie, Regeln für Ansprüche zu konfigurieren. Weitere Informationen zu den Anspruchsregeln, die in der Anspruchsanbieterorganisation verwendet werden können, finden Sie unter [Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md).  
  

