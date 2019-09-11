---
title: AD FS OpenID Connect/OAuth-Konzepte
description: Erfahren Sie mehr über AD FS modernen Authentifizierungs Konzepten.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 08/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6a0a1da3dd5c92dff885478c1669bbda5ae07fe5
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867475"
---
# <a name="ad-fs-openid-connectoauth-concepts"></a>AD FS OpenID Connect/OAuth-Konzepte
Gilt für AD FS 2016 und höher
 
## <a name="modern-authentication-actors"></a>Moderne Authentifizierungs Akteure 

|Actor| Beschreibung|
|-----|-----|
|Endbenutzer|Dies ist der Sicherheits Prinzipal (Benutzer, Anwendungen, Dienste und Gruppen), der auf die Ressource zugreifen muss.|  
|Client|Dies ist Ihre Webanwendung, die durch die Client-ID identifiziert wird. Der Client ist in der Regel die Partei, mit der der Endbenutzer interagiert, und fordert Token vom autorisierungsserver an.
|Autorisierungs Server/Identitäts Anbieter (IDP)| Dies ist der AD FS Server. Er ist verantwortlich für die Überprüfung der Identität von Sicherheits Prinzipale, die im Verzeichnis einer Organisation vorhanden sind. Bei erfolgreicher Authentifizierung dieser Sicherheits Prinzipale werden Sicherheits Token (bearerzugriffstoken, ID-Token, Aktualisierungs Token) ausgegeben.
|Ressourcen Server/Ressourcenanbieter/vertrauende Seite| Hier befindet sich die Ressource oder die Daten. Es vertraut dem Autorisierungs Server, den Client sicher zu authentifizieren und zu autorisieren, und verwendet bearerzugriffstoken, um sicherzustellen, dass Zugriff auf eine Ressource gewährt werden kann

Das folgende Diagramm stellt die grundlegende Beziehung zwischen den Akteuren dar:

![Moderne Authentifizierungs Akteure](media/adfs-modern-auth-concepts/concept1.png)

## <a name="application-types"></a>Anwendungs Typen 
 

|Anwendungstyp|Beschreibung|Rolle|
|-----|-----|-----|
|Native Anwendung|Dies wird manchmal als **öffentlicher Client**bezeichnet und soll eine Client-App sein, die auf einem PC oder einem Gerät ausgeführt wird und mit dem der Benutzer interagiert.|Fordert Token vom autorisierungsserver (AD FS) an, um Benutzer Zugriff auf Ressourcen zu erhalten. Sendet HTTP-Anforderungen an geschützte Ressourcen und verwendet dabei die Token als HTTP-Header.| 
|Server Anwendung (Web-App)|Eine Webanwendung, die auf einem Server ausgeführt wird und im Allgemeinen für Benutzer über einen Browser zugänglich ist. Da es in der Lage ist, seinen eigenen geheimen Client Schlüssel oder Anmelde Informationen beizubehalten, wird es manchmal als **vertraulicher Client**bezeichnet. |Fordert Token vom autorisierungsserver (AD FS) an, um Benutzer Zugriff auf Ressourcen zu erhalten. Vor dem Anfordern von Token muss sich der Client (Web-App) mithilfe seines geheimen Schlüssels authentifizieren. | 
|Web-API|Die Endressource, auf die der Benutzer zugreift. Stellen Sie sich diese als neue Darstellung von "vertrauende Seiten" vor.|Beansprucht bearerzugriffstoken von den Clients| 

## <a name="application-group"></a>Anwendungs Gruppe 
 
Jeder OAuth-Client (Native oder Web-App) oder Ressource (Web-API), der mit AD FS konfiguriert ist, muss einer Anwendungs Gruppe zugeordnet werden. Die Clients in einer Anwendungs Gruppe können für den Zugriff auf die Ressourcen in der gleichen Gruppe konfiguriert werden. Eine Anwendungs Gruppe kann mehrere Clients und Ressourcen enthalten.  

## <a name="security-tokens"></a>Sicherheits Token 
 
Die moderne Authentifizierung verwendet die folgenden Tokentypen: 
- **ID**: Ein vom autorisierungsserver (AD FS) ausgestelltes JWT-Token, das vom Client verwendet wird. Ansprüche im ID-Token enthalten Informationen über den Benutzer, damit dieser vom Client verwendet werden kann.  
- **access_token**: Ein vom autorisierungsserver (AD FS) ausgestelltes JWT-Token, das von der Ressource verwendet werden soll. Der "AUD"-oder "Audience"-Anspruch dieses Tokens muss mit dem Bezeichner der Ressource oder der Web-API identisch sein.  
- **refresh_token**: Dies ist ein Token, das von AD FS für den Client ausgegeben wird, wenn ID und access_token aktualisiert werden müssen. Das Token ist für den Client nicht transparent und kann nur von AD FS genutzt werden.  

## <a name="scopes"></a>Bereiche 
 
Beim Registrieren einer Ressource in AD FS können Bereiche so konfiguriert werden, dass AD FS bestimmte Aktionen ausführen kann. Zusätzlich zum Konfigurieren des Bereichs muss auch der Bereichs Wert in der Anforderung gesendet werden, um AD FS die Aktion auszuführen. Beispielsweise muss der Administrator während der Ressourcen Registrierung den Bereich als OpenID konfigurieren, und die Anwendung (Client) muss Scope = OpenID in der Authentifizierungsanforderung senden, damit AD FS das ID-Token ausgibt. Details zu den in AD FS verfügbaren Bereichen werden unten bereitgestellt. 
 
- Aza: Wenn die [OAuth 2,0-Protokoll Erweiterungen für Broker Clients](https://docs.microsoft.com/openspecs/windows_protocols/ms-oapxbc/2f7d8875-0383-4058-956d-2fb216b44706) verwendet werden und der Scope-Parameter den Bereich "Aza" enthält, gibt der Server ein neues primäres Aktualisierungs Token aus und legt es im refresh_token-Feld der Antwort fest. Außerdem wird das refresh_token_expires_in-Feld bis zur Lebensdauer des neuen primären Aktualisierungs Tokens, wenn eine erzwungen wird. 
- OpenID: ermöglicht es der Anwendung, die Verwendung des OpenID Connect-Autorisierungs Protokolls anzufordern. 
- logon_cert: der logon_cert-Bereich ermöglicht es einer Anwendung, Anmelde Zertifikate anzufordern, die für die interaktive Anmeldung von authentifizierten Benutzern verwendet werden können. Der AD FS Server lässt den access_token-Parameter aus der Antwort aus und stellt stattdessen eine Base64-codierte CMS-Zertifikatskette oder eine SMTP-vollständige PKI-Antwort bereit. Weitere Informationen finden Sie [hier](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-oapx/32ce8878-7d33-4c02-818b-6c9164cc731e).
- user_impersonation: der Bereich "user_impersonation" ist erforderlich, um erfolgreich ein Zugriffs Token aus AD FS anzufordern. Ausführliche Informationen zur Verwendung dieses Bereichs finden Sie unter [Erstellen einer Anwendung mit mehreren Stufen mithilfe von "on-Auftrag-of" (OBO) mithilfe von OAuth mit AD FS 2016](ad-fs-on-behalf-of-authentication-in-windows-server.md). 
- allatclaims – mit dem allatclaims-Bereich kann die Anwendung anfordern, dass Ansprüche im Zugriffs Token ebenfalls im ID-Token hinzugefügt werden.   
- vpn_cert: der vpn_cert-Bereich ermöglicht einer Anwendung das Anfordern von VPN-Zertifikaten, die zum Einrichten von VPN-Verbindungen mithilfe der EAP-TLS-Authentifizierung verwendet werden können. Dies wird nicht mehr unterstützt. 
- e-Mail: ermöglicht es der Anwendung, einen e-Mail-Anspruch für den angemeldeten Benutzer anzufordern.  
- Profil: ermöglicht es der Anwendung, Profil bezogene Ansprüche für den Anmelde Benutzer anzufordern.  

## <a name="claims"></a>Ansprüche 
 
Sicherheits Token (Zugriffs-und ID-Token), die von AD FS ausgegeben werden, enthalten Ansprüche oder Assertionen von Informationen über den authentifizierten Betreff. Anwendungen können Ansprüche für verschiedene Aufgaben verwenden, einschließlich: 
- Token überprüfen 
- Identifizieren des Verzeichnis Mandanten des Antragstellers 
- Anzeigen von Benutzerinformationen 
- Ermitteln der Autorisierung des Antragstellers die Ansprüche, die in einem bestimmten Sicherheits Token vorhanden sind, hängen vom Typ des Tokens, von der Art der zum Authentifizieren des Benutzers verwendeten Anmelde Informationen und von der Anwendungskonfiguration ab.  
 
## <a name="high-level-ad-fs-authentication-flow"></a>Allgemeine AD FS Authentifizierungs Fluss 

![AD FS Authentifizierungs Fluss](media/adfs-modern-auth-concepts/adfsauthflow.png)


 1. AD FS empfängt eine Authentifizierungsanforderung vom Client.  
 
 2. AD FS überprüft die Client-ID in der Authentifizierungsanforderung mit der Client-ID, die bei der Client-und Ressourcen Registrierung in AD FS abgerufen wurde. Wenn Sie den vertraulichen Client verwenden, überprüft AD FS auch den geheimen Client Schlüssel, der in der Authentifizierungsanforderung angegeben ist. AD FS auch den Umleitungs-URI des Clients überprüfen. 
 
 3. AD FS identifiziert die Ressource, auf die der Client über den in der Authentifizierungsanforderung übergebenen Ressourcen Parameter zugreifen möchte. Wenn Sie die msal-Client Bibliothek verwenden, wird der Ressourcen Parameter nicht gesendet. Stattdessen wird die Ressourcen-URL als Teil des Bereichs Parameters gesendet: *Scope = [resource URL]//[Bereichs Werte, z. b. OpenID]* . 

    Wenn die Ressource nicht mit dem Resource-oder Scope-Parameter übergeben wird, verwendet ADFS einen Standard Ressourcen-urn: Microsoft: userinfo, deren Richtlinien (z. b. MFA, Ausstellung oder Autorisierungs Richtlinie) nicht konfiguriert werden können. 
 
 4. Im nächsten AD FS überprüft, ob der Client über die Berechtigungen für den Zugriff auf die Ressource verfügt. AD FS überprüft auch, ob die in der Authentifizierungsanforderung übergebenen Bereiche mit den Bereichen übereinstimmen, die beim Registrieren der Ressource konfiguriert wurden. Wenn der Client nicht über die Berechtigungen verfügt oder die richtigen Bereiche nicht in der Authentifizierungsanforderung gesendet werden, wird der Authentifizierungs Fluss beendet.   
 
 5. Nachdem Berechtigungen und Bereiche überprüft wurden, werden AD FS den Benutzer mithilfe der konfigurierten [Authentifizierungsmethode](../operations/configure-authentication-policies.md)authentifiziert.   

 6. Wenn gemäß der Ressourcen Richtlinie oder der globalen Authentifizierungs Richtlinie eine [zusätzliche Authentifizierungsmethode](../operations/configure-additional-authentication-methods-for-ad-fs.md) erforderlich ist, löst AD FS die zusätzliche Authentifizierung aus. 

 7. AD FS verwendet [Azure MFA](../operations/configure-ad-fs-and-azure-mfa.md) oder die [MFA von Drittanbietern](../operations/additional-authentication-methods-ad-fs.md) , um die Authentifizierung durchzuführen.   
 
 8. Sobald der Benutzer authentifiziert wurde, wendet AD FS die [Anspruchs Regeln](../deployment/configuring-claim-rules.md) (bestimmt die Ansprüche, die als Teil der Sicherheits Token an die Ressource gesendet werden) und [Zugriffs Steuerungs Richtlinien](../operations/ad-fs-client-access-policies.md) an (stellt fest, dass der Benutzer die für den Zugriff auf die Ressource erforderlichen Bedingungen erfüllt).   

 9. Als nächstes generiert AD FS die Zugriffs-und Aktualisierungs Token. 

 10. AD FS generiert auch das ID-Token. 
 
 11. Wenn der Bereich = allatclaims in der Authentifizierungsanforderung enthalten ist, [wird das ID-Token angepasst](custom-id-tokens-in-ad-fs.md) , um Ansprüche im Zugriffs Token basierend auf den definierten Anspruchs Regeln einzuschließen. 
    
 12. Nachdem die erforderlichen Token generiert und angepasst wurden, reagiert AD FS auf den Client, einschließlich der Token. Nur wenn die Authentifizierungsanforderung Scope = OpenID enthält, ist das ID-Token in der Antwort enthalten. Der Client kann immer das ID-Token nach der Authentifizierung über den tokenendpunkt abrufen. 

## <a name="types-of-libraries"></a>Typen von Bibliotheken 
  
Mit AD FS werden zwei Arten von Bibliotheken verwendet: 
- **Client Bibliotheken**: Native Clients und Server-Apps verwenden Client Bibliotheken zum Abrufen von Zugriffs Token zum Aufrufen einer Ressource, z. b. einer Web-API. Die Microsoft Authentication Library (msal) ist die neueste und empfohlene Client Bibliothek bei Verwendung von AD FS 2019. Active Directory-Authentifizierungsbibliothek (Adal) wird für AD FS 2016 empfohlen.  

- **Bibliotheken der Server Middleware**: Web-Apps verwenden Server-middlewarebibliotheken für die Benutzeranmeldung. Web-APIs verwenden Server Middleware-Bibliotheken zum Überprüfen von Token, die von nativen Clients oder anderen Servern gesendet werden. Owin (Open Web Interface für .net) ist die empfohlene Middleware-Bibliothek. 

## <a name="customize-id-token-additional-claims-in-id-token"></a>ID-Token anpassen (zusätzliche Ansprüche im ID-Token)
 
In bestimmten Szenarien ist es möglich, dass die Web-App (Client) zusätzliche Ansprüche in einem ID-Token benötigt, um die Funktionalität zu unterstützen. Dies kann mithilfe einer der folgenden Optionen erreicht werden. 

**Option 1:** Sollte verwendet werden, wenn ein öffentlicher Client verwendet wird und die Web-App nicht über eine Ressource verfügt, auf die zugegriffen werden soll. Die Option erfordert 
1.  response_mode als form_post festlegen 
2.  Bezeichner der vertrauenden Seite (Web-API-Bezeichner) ist identisch mit dem Client

![AD FS Option "Token anpassen" 1](media/adfs-modern-auth-concepts/option1.png)

**Option 2:** Sollte verwendet werden, wenn die Web-App über eine Ressource verfügt, auf die zugegriffen werden soll, und zusätzliche Ansprüche über das ID-Token übergeben werden müssen. Es können sowohl öffentliche als auch vertrauliche Clients verwendet werden. Die Option erfordert 
1.  response_mode als form_post festlegen 
2.  KB4019472 ist auf den AD FS-Servern installiert. 
3.  Bereich allatclaims, der dem Client – RP-paar zugewiesen ist. Sie können den Bereich zuweisen, indem Sie das PowerShell-Cmdlet Grant-adfsapplicationberechtigung (Set-adfsapplicationberechtigung, falls bereits erteilt) verwenden, wie im folgenden Beispiel gezeigt: 

    ``` powershell
    Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
    ```

![AD FS Option "Token anpassen" 2](media/adfs-modern-auth-concepts/option2.png)

Informationen zum Konfigurieren einer Web-App in ADFS zum Abrufen eines angepassten ID-Tokens finden Sie unter [Anpassen von Anspruchs, die in ID ausgegeben werden sollen, wenn OpenID Connect oder OAuth mit AD FS 2016 oder höher verwendet wird](Custom-Id-Tokens-in-AD-FS.md).

## <a name="single-log-out"></a>Einmaliges abmelden

Die einmalige Abmeldung führt dazu, dass alle Client Sitzungen mithilfe der Sitzungs-ID beendet werden. AD FS 2016 und höher unterstützt die einmalige Abmeldung für OpenID Connect/OAuth. Weitere Informationen finden [Sie unter Single Log-out for OpenID Connect with AD FS](ad-fs-logout-openid-connect.md).


## <a name="ad-fs-endpoints"></a>AD FS Endpunkte

|AD FS-Endpunkt|Beschreibung|
|-----|-----|
|/Authorize-Endpunkt|AD FS gibt einen Autorisierungs Code zurück, der zum Abrufen des Zugriffs Tokens verwendet werden kann.|
|/Token|AD FS gibt ein Zugriffs Token zurück, das für den Zugriff auf die Ressource (Web-API) verwendet werden kann.|
|/userinfo|AD FS gibt Ansprüche über den authentifizierten Benutzer zurück.|
|/devicecode|AD FS gibt den Geräte Code und Benutzercode zurück.|
|/logout|AD FS meldet den Benutzer ab.|
|/keys|AD FS öffentlichen Schlüssel zum Signieren von Antworten|
|/.well-known/openid-configuration|AD FS gibt OAuth/OpenID Connect-Metadaten zurück.|
