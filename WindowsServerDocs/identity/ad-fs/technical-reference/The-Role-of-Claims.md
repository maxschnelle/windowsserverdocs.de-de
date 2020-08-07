---
ms.assetid: 22f53391-8c6a-4873-a1f4-08b4760ea621
title: Rolle von Ansprüchen
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: eb41b8168024a231282716e5edd0bc59554d7da6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937823"
---
# <a name="the-role-of-claims"></a>Rolle von Ansprüchen

Im Anspruchs \- basierten Identitäts Modell spielen Ansprüche eine entscheidende Rolle im Verbund Prozess, Sie sind die wichtigste Komponente, mit der das Ergebnis aller \- webbasierten Authentifizierungs-und Autorisierungs Anforderungen bestimmt wird. Dieses Modell ermöglicht es Organisationen, digitale Identitäten und Bezugsrechte bzw. *Ansprüche* über Sicherheits- und Unternehmensgrenzen hinweg auf standardisierte Weise sicher zu planen.

## <a name="what-are-claims"></a>Was sind Ansprüche?

In seiner einfachsten Form sind Ansprüche einfach *Anweisungen* \( , z. b. "Name", "Identität", "Gruppe" \) und "Benutzer", die hauptsächlich zum autorialisieren des Zugriffs auf Anspruchs basierte Anwendungen verwendet werden, \- die sich an einer beliebigen Stelle im Internet Jede Aussage entspricht einem *Wert*, der im Anspruch gespeichert wird.

### <a name="how-claims-are-sourced"></a>Belegen von Ansprüchen

Der Verbunddienst in Active Directory-Verbunddienste (AD FS) \( AD FS \) definiert, welche Ansprüche zwischen Verbund Partnern ausgetauscht werden. Dazu muss der Anspruch zunächst mit einem abgerufenen oder berechneten Wert ausgefüllt oder belegt werden. Jeder Anspruchswert stellt einen Wert eines Benutzers, einer Gruppe oder Entität dar und es gibt zwei Möglichkeiten, um diesen zu belegen:

1.  Der Wert, der den Anspruch bildet, wird aus einem Attributspeicher abgerufen, z. B. kann ein Attributwert der Vertriebsabteilung aus den Eigenschaften eines Active Directory-Benutzerkontos abgerufen werden. Weitere Informationen finden Sie unter [Rolle des Attributspeichers](The-Role-of-Attribute-Stores.md).

2.  Der Wert eines eingehenden Anspruchs wird auf Basis der in einer Regel angegebenen Logik in einen anderen Wert transformiert. Wenn z. B. ein eingehender Anspruch mit dem Wert "Domänenadministratoren" in den neuen Wert "Administratoren" transformiert wird, bevor dieser als ausgehender Anspruch gesendet wird. Weitere Informationen finden Sie unter [Rolle von Anspruchsregeln](The-Role-of-Claim-Rules.md).

Ansprüche können Werte wie e-Mail- \- Adresse, Benutzer Prinzipal Namen \( -UPN \) , Gruppenmitgliedschaft und andere Konto Attribute enthalten.

### <a name="how-claims-flow"></a>Verlauf von Ansprüchen

Andere Parteien basieren auf den Werten der Ansprüche, um Autorisierungs Aufgaben für webbasierte \- Anwendungen auszuführen, die Sie hosten. Diese Parteien werden im Snap-in AD FS Verwaltung als vertrauende *Seiten* bezeichnet \- . Der Verbunddienst ist für das Broker der Vertrauensstellung zwischen vielen verschiedenartigen Parteien verantwortlich. Es ist so konzipiert, dass der vertrauenswürdige Austausch von Ansprüchen aus einer Organisation verarbeitet und durchlaufen wird, die zunächst die Ansprüche, auch als *Anspruchs Anbieter* im Snap-in AD FS Verwaltung bezeichnet \- , an eine vertrauende Seite weitergibt. Eine vertrauende Seite verwendet diese Ansprüche dann zum Treffen von Autorisierungsentscheidungen.

Der diesen Prozess verwendende Anspruchsverlauf wird als *Anspruchspipeline* bezeichnet. Der Anspruchsverlauf durch die Anspruchspipeline umfasst drei Schritte:

1.  Die vom Anspruchsanbieter empfangenen Ansprüche werden mit Akzeptanztransformationsregeln der Vertrauensstellung des Anspruchsanbieters verarbeitet. Diese Regeln bestimmen, welche Ansprüche vom Anspruchsanbieter akzeptiert werden.

2.  Die Ausgabe der Akzeptanztransformationsregeln wird als Eingabe für die Ausstellungsautorisierungsregeln verwendet. Diese Regeln bestimmen, ob dem Benutzer der Zugriff auf die vertrauende Seite gestattet ist.

3.  Die Ausgabe der Akzeptanztransformationsregeln wird als Eingabe für die Ausstellungstransformationsregeln verwendet. Diese Regeln bestimmen die Ansprüche, die an die vertrauende Seite gesendet werden.

Weitere Informationen finden Sie unter [Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md).

### <a name="how-claims-are-issued"></a>Ausstellen von Ansprüchen

Beim Erstellen von Anspruchsregeln hängt die Quelle der eingehenden Ansprüche für die Anspruchsregeln davon ab, ob Sie die Regeln für die Vertrauensstellung eines Anspruchsanbieters oder einer vertrauenden Seite erstellen. Wenn Sie Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung erstellen, entsprechen die eingehenden Ansprüche den Ansprüchen, die vom vertrauenswürdigen Anspruchsanbieter an den Verbunddienst gesendet werden. Wenn Sie Regeln für die Vertrauensstellung der vertrauenden Seite erstellen, entsprechen die eingehenden Ansprüche den Ansprüchen, die von den Anspruchsregeln der maßgeblichen Anspruchsanbieter-Vertrauensstellung ausgegeben werden. Weitere Informationen zu ein- und ausgehenden Ansprüchen finden Sie unter [Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md) und [Rolle der Anspruchs-Engine](The-Role-of-the-Claims-Engine.md).

## <a name="what-are-claim-types"></a>Was sind Anspruchstypen?

Ein Anspruchstyp stellt den Kontext für den Anspruchswert bereit. Sie wird normalerweise als Uniform Resource Identifier- \( URI ausgedrückt \) . AD FS können jeden Anspruchstyp unterstützen, und er wird standardmäßig mit den Anspruchs Typen in der folgenden Tabelle konfiguriert.

|Name|Beschreibung|URI|
|--------|---------------|-------|
|E- \- Mail-Adresse|E- \- Mail-Adresse des Benutzers|http: \/ \/schemas.xmlSOAP.org \/ WS \/ 2005 \/ 05 \/ - \/ identitätforderungs- \/ EmailAddress|
|Vorname|Angegebener Name des Benutzers|http: \/ \/schemas.xmlSOAP.org \/ WS \/ 2005 \/ 05 \/ Identitäts \/ Ansprüche \/ givenName|
|Name|Eindeutiger Name des Benutzers|http: \/ \/schemas.xmlSOAP.org \/ WS \/ 2005 \/ 05 \/ Identitäts \/ Anspruchs \/ Name|
|UPN|Der Benutzer Prinzipal Name- \( UPN \) des Benutzers|http: \/ \/schemas.xmlSOAP.org \/ WS \/ 2005 \/ 05- \/ Identitäts \/ Anspruchs- \/ UPN|
|Allgemeiner Name|Allgemeiner Name des Benutzers|http: \/ \/schemas.xmlSOAP.org \/ Claims \/ CommonName|
|E-Mail-Adresse für AD FS 1. x \-|E- \- Mail-Adresse des Benutzers bei der Interaktion mit AD FS 1,1 oder ADFS 1,0|http: \/ \/schemas.xmlSOAP.org \/ Claims \/ EmailAddress|
|Group|Eine Gruppe, in der der Benutzer Mitglied ist|http: \/ \/schemas.xmlSOAP.org- \/ Anspruchs \/ Gruppe|
|AD FS 1.x UPN|UPN des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|http: \/ \/schemas.xmlSOAP.org \/ Anspruchs- \/ UPN|
|Role|Eine Rolle, über die der Benutzer verfügt|http: \/ \/ Schemas.Microsoft.com \/ WS \/ 2008 \/ 06- \/ Identitäts \/ Anspruchs \/ Rolle|
|Surname|Nachname des Benutzers|http: \/ \/schemas.xmlSOAP.org \/ WS \/ 2005 \/ 05- \/ Identitäts \/ Anspruchs \/ Nachname|
|PPID|Private ID des Benutzers|http: \/ \/schemas.xmlSOAP.org \/ WS \/ 2005 \/ 05- \/ Identitäts \/ Ansprüche \/ PrivatePersonalIdentifier|
|Namensbezeichner|SAML-Namensbezeichner des Benutzers|http: \/ \/schemas.xmlSOAP.org \/ WS \/ 2005 \/ 05 \/ Identity \/ Claims \/ NameIdentifier|
|Authentifizierungsmethode|Zur Authentifizierung des Benutzers verwendete Methode|http: \/ \/ Schemas.Microsoft.com \/ WS \/ 2008 \/ 06- \/ Identitäts \/ Ansprüche \/ AuthenticationMethod|
|Nur Gruppen-SID verweigern|Die Gruppen-SID "nur verweigern" \- des Benutzers|http: \/ \/schemas.xmlSOAP.org \/ WS \/ 2005 \/ 05 \/ Identitäts \/ Ansprüche \/ denyonlysid|
|Nur primäre SID verweigern|Die \- einzige primäre SID des Benutzers verweigern|http: \/ \/ Schemas.Microsoft.com \/ WS \/ 2008 \/ 06 \/ Identitäts \/ Ansprüche \/ denyonlyprimarysid|
|Nur primäre Gruppen-SID verweigern|Die \- SID nur der primären Gruppen-SID des Benutzers verweigern|http: \/ \/ Schemas.Microsoft.com \/ WS \/ 2008 \/ 06 \/ Identitäts \/ Ansprüche \/ denyonlyprimarygroupsid|
|Gruppen-SID|Die Gruppen-SID des Benutzers|http: \/ \/ Schemas.Microsoft.com \/ WS \/ 2008 \/ 06 \/ Identitäts \/ Anspruchs- \/ groupsid|
|Primäre Gruppen-SID|Primäre Gruppen-SID des Benutzers|http: \/ \/ Schemas.Microsoft.com \/ WS \/ 2008 \/ 06 \/ Identitäts \/ Ansprüche \/ primarygroupsid|
|Primäre SID|Primäre SID des Benutzers|http: \/ \/ Schemas.Microsoft.com \/ WS \/ 2008 \/ 06 \/ Identitäts \/ Ansprüche \/ primarysid|
|Windows-Kontoname|Der Domänen Konto Name des Benutzers in der Form\<domain\>\\\<user\>|http: \/ \/ Schemas.Microsoft.com \/ WS \/ 2008 \/ 06 \/ Identitäts \/ Ansprüche \/ windowsaccountname|

## <a name="what-are-claim-descriptions"></a>Was sind Anspruchsbeschreibungen?

Anspruchs Beschreibungen stellen eine Liste von Anspruchs Typen dar, die von AD FS unterstützt werden und die in Verbund Metadaten veröffentlicht werden können. Die in der vorherigen Tabelle erwähnten Anspruchs Typen werden im Snap-in AD FS Verwaltung als Anspruchs Beschreibungen konfiguriert \- .

Die in Verbundmetadaten veröffentlichte Sammlung von Anspruchsbeschreibungen wird in der AD FS-Konfigurationsdatenbank gespeichert. Diese Anspruchsbeschreibungen werden von verschiedenen Komponenten des Verbunddiensts verwendet.

Jede Anspruchsbeschreibung umfasst einen Anspruchstyp-URI, einen Namen, den Veröffentlichungsstatus und eine Beschreibung. Sie können die Sammlung der Anspruchs Beschreibungen mithilfe des Knotens **Anspruchs Beschreibungen** im Snap-in AD FS Verwaltung verwalten \- . Mit dem Snap-in können Sie den Veröffentlichungsstatus einer Anspruchs Beschreibung ändern \- . Die folgenden Einstellungen sind verfügbar:

- **Diesen Anspruch in Verbund Metadaten als Anspruchstyp veröffentlichen, der von diesem Verbunddienst akzeptiert** \( werden kann Als akzeptiert veröffentlichen \) – gibt die Anspruchs Typen an, die von diesem Verbunddienst von anderen Anspruchs Anbietern akzeptiert werden.

- **Diesen Anspruch in Verbund Metadaten als Anspruchstyp veröffentlichen, der von diesem Verbunddienst gesendet** \( werden kann Als gesendet veröffentlichen \) – gibt die Anspruchs Typen an, die von diesem Verbunddienst angeboten werden. Dies sind die Anspruchstypen, die vom Verbunddienst für andere veröffentlicht werden, da er bereit ist, diese zu senden. Die tatsächlich vom Anspruchsanbieter gesendeten Anspruchstypen sind häufig eine Teilmenge dieser Liste.

Weitere Informationen zum Festlegen des Veröffentlichungs Zustands eines Anspruchs Typs finden [Sie unter Hinzufügen einer Anspruchs Beschreibung](../operations/add-a-claim-description.md) im AD FS Bereitstellungs Handbuch.

### <a name="when-generating-federation-metadata"></a>Beim Generieren von Verbundmetadaten

Verbundmetadaten umfassen alle Anspruchsbeschreibungen, die für die Veröffentlichung markiert sind.

### <a name="when-claims-rules-are-processed"></a>Beim Verarbeiten von Anspruchsregeln

Wenn Sie Konfigurationsinformationen zu Anspruchsbeschreibungen beibehalten, ist es einfacher für Sie, Regeln für Ansprüche zu konfigurieren. Weitere Informationen zu den Anspruchsregeln, die in der Anspruchsanbieterorganisation verwendet werden können, finden Sie unter [Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md).
