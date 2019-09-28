---
ms.assetid: 22f53391-8c6a-4873-a1f4-08b4760ea621
title: Rolle von Ansprüchen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 851a70bbed606530ca8292f65bc4f776eae77fae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407342"
---
# <a name="the-role-of-claims"></a>Rolle von Ansprüchen
Im Anspruchs @ no__t-0basierten Identitäts Modell spielen Ansprüche eine entscheidende Rolle im Verbund Prozess, Sie sind die wichtigste Komponente, mit der das Ergebnis aller Web @ no__t-1basierten Authentifizierungs-und Autorisierungs Anforderungen bestimmt wird. Dieses Modell ermöglicht es Organisationen, digitale Identitäten und Bezugsrechte bzw. *Ansprüche* über Sicherheits- und Unternehmensgrenzen hinweg auf standardisierte Weise sicher zu planen.  
  
## <a name="what-are-claims"></a>Was sind Ansprüche?  
In seiner einfachsten Form sind Ansprüche einfach *Anweisungen* \(Z. b. Name, Identity, Group @ no__t-2, Informationen zu Benutzern, die hauptsächlich zum autorialisieren des Zugriffs auf Ansprüche @ no__t-3based-Anwendungen an beliebiger Stelle im Internet verwendet werden. Jede Aussage entspricht einem *Wert*, der im Anspruch gespeichert wird.  
  
### <a name="how-claims-are-sourced"></a>Belegen von Ansprüchen  
Der Verbunddienst in Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 definiert, welche Ansprüche zwischen Verbund Partnern ausgetauscht werden. Dazu muss der Anspruch zunächst mit einem abgerufenen oder berechneten Wert ausgefüllt oder belegt werden. Jeder Anspruchswert stellt einen Wert eines Benutzers, einer Gruppe oder Entität dar und es gibt zwei Möglichkeiten, um diesen zu belegen:  
  
1.  Der Wert, der den Anspruch bildet, wird aus einem Attributspeicher abgerufen, z. B. kann ein Attributwert der Vertriebsabteilung aus den Eigenschaften eines Active Directory-Benutzerkontos abgerufen werden. Weitere Informationen finden Sie unter [Rolle des Attributspeichers](The-Role-of-Attribute-Stores.md).  
  
2.  Der Wert eines eingehenden Anspruchs wird auf Basis der in einer Regel angegebenen Logik in einen anderen Wert transformiert. Wenn z. B. ein eingehender Anspruch mit dem Wert "Domänenadministratoren" in den neuen Wert "Administratoren" transformiert wird, bevor dieser als ausgehender Anspruch gesendet wird. Weitere Informationen finden Sie unter [Rolle von Anspruchsregeln](The-Role-of-Claim-Rules.md).  
  
Ansprüche können Werte wie z. b. die e @ no__t-e-Mail-Adresse, den Benutzer Prinzipal Namen \(upn @ no__t-2, die Gruppenmitgliedschaft und andere Konto Attribute enthalten.  
  
### <a name="how-claims-flow"></a>Verlauf von Ansprüchen  
Andere Parteien verlassen sich auf die Werte der Ansprüche, um Autorisierungs Aufgaben für auf Web @ no__t 0basierende Anwendungen auszuführen, die Sie hosten. Diese Parteien werden im AD FS Management-Snap @ no__t-1In als vertrauende *Seiten* bezeichnet. Der Verbunddienst ist für das Broker der Vertrauensstellung zwischen vielen verschiedenartigen Parteien verantwortlich. Es ist so konzipiert, dass der vertrauenswürdige Austausch von Ansprüchen aus einer Organisation verarbeitet und durchlaufen wird, die zunächst die Ansprüche, die auch als *Anspruchs Anbieter* im AD FS Verwaltungs-Snap @ no__t-1In bezeichnet werden, an eine vertrauende Seite weitergibt. Eine vertrauende Seite verwendet diese Ansprüche dann zum Treffen von Autorisierungsentscheidungen.  
  
Der diesen Prozess verwendende Anspruchsverlauf wird als *Anspruchspipeline* bezeichnet. Der Anspruchsverlauf durch die Anspruchspipeline umfasst drei Schritte:  
  
1.  Die vom Anspruchsanbieter empfangenen Ansprüche werden mit Akzeptanztransformationsregeln der Vertrauensstellung des Anspruchsanbieters verarbeitet. Diese Regeln bestimmen, welche Ansprüche vom Anspruchsanbieter akzeptiert werden.  
  
2.  Die Ausgabe der Akzeptanztransformationsregeln wird als Eingabe für die Ausstellungsautorisierungsregeln verwendet. Diese Regeln bestimmen, ob dem Benutzer der Zugriff auf die vertrauende Seite gestattet ist.  
  
3.  Die Ausgabe der Akzeptanztransformationsregeln wird als Eingabe für die Ausstellungstransformationsregeln verwendet. Diese Regeln bestimmen die Ansprüche, die an die vertrauende Seite gesendet werden.  
  
Weitere Informationen finden Sie unter [Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md).  
  
### <a name="how-claims-are-issued"></a>Ausstellen von Ansprüchen  
Beim Erstellen von Anspruchsregeln hängt die Quelle der eingehenden Ansprüche für die Anspruchsregeln davon ab, ob Sie die Regeln für die Vertrauensstellung eines Anspruchsanbieters oder einer vertrauenden Seite erstellen. Wenn Sie Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung erstellen, entsprechen die eingehenden Ansprüche den Ansprüchen, die vom vertrauenswürdigen Anspruchsanbieter an den Verbunddienst gesendet werden. Wenn Sie Regeln für die Vertrauensstellung der vertrauenden Seite erstellen, entsprechen die eingehenden Ansprüche den Ansprüchen, die von den Anspruchsregeln der maßgeblichen Anspruchsanbieter-Vertrauensstellung ausgegeben werden. Weitere Informationen zu ein- und ausgehenden Ansprüchen finden Sie unter [Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md) und [Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md).  
  
## <a name="what-are-claim-types"></a>Was sind Anspruchstypen?  
Ein Anspruchstyp stellt den Kontext für den Anspruchswert bereit. Sie wird normalerweise als Uniform Resource Identifier \(uri @ no__t-1 ausgedrückt. AD FS können jeden Anspruchstyp unterstützen, und er wird standardmäßig mit den Anspruchs Typen in der folgenden Tabelle konfiguriert.  
  
|Name|Beschreibung|URI|  
|--------|---------------|-------|  
|E @ no__t-E-Mail-Adresse|Die e @ no__t-e-Mail-Adresse des Benutzers.|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7emailaddress|  
|Angegebener Name|Angegebener Name des Benutzers|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7givenname|  
|Name|Eindeutiger Name des Benutzers|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7name|  
|UPN|Der Benutzer Prinzipal Name \(upn @ no__t-1 des Benutzers.|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7upn|  
|Allgemeiner Name|Allgemeiner Name des Benutzers|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2claims @ no__t-3commonname|  
|AD FS 1. x E @ no__t-E-Mail-Adresse|Die e @ no__t-e-Mail-Adresse des Benutzers bei der Interaktion mit AD FS 1,1 oder ADFS 1,0|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2claims @ no__t-3emailaddress|  
|Gruppieren|Eine Gruppe, in der der Benutzer Mitglied ist|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2claims @ no__t-3group|  
|AD FS 1.x UPN|UPN des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2claims @ no__t-3upn|  
|Role-Eigenschaft|Eine Rolle, über die der Benutzer verfügt|http: @no__t -0\/schemas.Microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7role|  
|Nachname|Nachname des Benutzers|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7nachname|  
|PPID|Private ID des Benutzers|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7privatepersonalidentifier|  
|Namensbezeichner|SAML-Namensbezeichner des Benutzers|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7nameidentifier|  
|Authentifizierungsmethode|Zur Authentifizierung des Benutzers verwendete Methode|http: @no__t -0\/schemas.Microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7authenticationmethod|  
|Nur Gruppen-SID verweigern|Die Gruppen-SID "Deny @ no__t-0only" des Benutzers|http: @no__t -0\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7denyonlysid|  
|Nur primäre SID verweigern|Die primäre SID "Deny @ no__t-0" des Benutzers|http: @no__t -0\/schemas.Microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7denyonlyprimarysid|  
|Nur primäre Gruppen-SID verweigern|Die primäre Gruppen-SID "Deny @ no__t-0" des Benutzers|http: @no__t -0\/schemas.Microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7denyonlyprimarygroupsid|  
|Gruppen-SID|Die Gruppen-SID des Benutzers|http: @no__t -0\/schemas.Microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7groupsid|  
|Primäre Gruppen-SID|Primäre Gruppen-SID des Benutzers|http: @no__t -0\/schemas.Microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7primarygroupsid|  
|Primäre SID|Primäre SID des Benutzers|http: @no__t -0\/schemas.Microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7primarysid|  
|Windows-Kontoname|Der Domänen Konto Name des Benutzers in Form von \<domäne @ no__t-1 @ no__t-2 @ no__t-3user @ no__t-4|http: @no__t -0\/schemas.Microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7windowsaccountname|  
  
## <a name="what-are-claim-descriptions"></a>Was sind Anspruchsbeschreibungen?  
Anspruchs Beschreibungen stellen eine Liste von Anspruchs Typen dar, die von AD FS unterstützt werden und die in Verbund Metadaten veröffentlicht werden können. Die in der vorherigen Tabelle erwähnten Anspruchs Typen sind als Anspruchs Beschreibungen im AD FS Verwaltungs-Snap @ no__t-0in konfiguriert.  
  
Die in Verbundmetadaten veröffentlichte Sammlung von Anspruchsbeschreibungen wird in der AD FS-Konfigurationsdatenbank gespeichert. Diese Anspruchsbeschreibungen werden von verschiedenen Komponenten des Verbunddiensts verwendet.  
  
Jede Anspruchsbeschreibung umfasst einen Anspruchstyp-URI, einen Namen, den Veröffentlichungsstatus und eine Beschreibung. Sie können die Sammlung der Anspruchs Beschreibungen mithilfe des Knotens **Anspruchs Beschreibungen** im AD FS Verwaltungs-Snap @ no__t-1In verwalten. Sie können den Veröffentlichungsstatus einer Anspruchs Beschreibung mit dem Snap @ no__t-0in ändern. Die folgenden Einstellungen sind verfügbar:  
  
-   **Diesen Anspruch in Verbund Metadaten als Anspruchstyp veröffentlichen, der von diesem Verbunddienst akzeptiert werden kann** \(publish as Accepted @ no__t-2 – gibt die Anspruchs Typen an, die von diesem Verbunddienst von anderen Anspruchs Anbietern akzeptiert werden.  
  
-   **Veröffentlichen Sie diesen Anspruch in Verbund Metadaten als Anspruchstyp, den dieser Verbunddienst** \(publish as sent @ no__t-2 senden kann – gibt die Anspruchs Typen an, die von diesem Verbunddienst angeboten werden. Dies sind die Anspruchstypen, die vom Verbunddienst für andere veröffentlicht werden, da er bereit ist, diese zu senden. Die tatsächlich vom Anspruchsanbieter gesendeten Anspruchstypen sind häufig eine Teilmenge dieser Liste.  
  
Weitere Informationen zum Festlegen des Veröffentlichungs Zustands eines Anspruchs Typs finden [Sie unter Hinzufügen einer Anspruchs Beschreibung](https://technet.microsoft.com/library/dd807051.aspx) im AD FS Bereitstellungs Handbuch.  
  
### <a name="when-generating-federation-metadata"></a>Beim Generieren von Verbundmetadaten  
Verbundmetadaten umfassen alle Anspruchsbeschreibungen, die für die Veröffentlichung markiert sind.  
  
### <a name="when-claims-rules-are-processed"></a>Beim Verarbeiten von Anspruchsregeln  
Wenn Sie Konfigurationsinformationen zu Anspruchsbeschreibungen beibehalten, ist es einfacher für Sie, Regeln für Ansprüche zu konfigurieren. Weitere Informationen zu den Anspruchsregeln, die in der Anspruchsanbieterorganisation verwendet werden können, finden Sie unter [Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md).  
  

