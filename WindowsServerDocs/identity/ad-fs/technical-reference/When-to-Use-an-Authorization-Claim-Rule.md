---
ms.assetid: b734cbcb-342c-4a28-8ab5-b9cd990bb1c2
title: Wann sollte eine Autorisierungsanspruchsregel verwendet
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 144e382692e8f2a6732f8c7c5b8a1dd6049192cb
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="when-to-use-an-authorization-claim-rule"></a>Wann sollte eine Autorisierungsanspruchsregel verwendet
Sie können mit dieser Regel in Active Directory Federation Services \(AD FS\) verwenden, wenn Sie einen eingehenden Anspruchstyp und dann eine Aktion anwenden, die bestimmen, ob ein Benutzer wird gewährt oder verweigert den Zugriff basierend auf dem Wert, den Sie in der Regel angeben müssen. Wenn Sie diese Regel verwenden, weitergeleitet bzw. transformieren Ansprüche, die auf Grundlage der Optionen, die Sie in der Regel Konfigurieren der folgenden Regellogik entsprechen:  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Alle Benutzer zulassen|Wenn der eingehende Anspruchstyp dem *beliebigen Anspruchstyp* und der Wert einem *einen beliebigen Wert*, dann Problem Anspruch ausstellungsanspruch mit Wert *zulassen*|  
|Benutzer mit diesem eingehenden Anspruch Zugriff gewähren|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert*, dann Problem Anspruch ausstellungsanspruch mit Wert *zulassen*|  
|Benutzern mit diesem eingehenden Anspruch Zugriff verweigern|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert*, dann Problem Anspruch ausstellungsanspruch mit Wert *verweigern*|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln und bieten weitere Detail zur Verwendung dieser Regeln.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \ (wenn x dann Y\) und erstellen Sie einen ausgehenden Anspruch auf Grundlage der Bedingung-Parameter. Die folgende Liste enthält wichtige Tipps, die Sie kennen sollten Anspruchsregeln bevor Sie weiter lesen in diesem Thema:  
  
-   In der AD FS-Verwaltungs-Snap-In können Anspruchsregeln nur erstellt werden mithilfe von anspruchsregelvorlagen  
  
-   Anspruch Regeln Prozess eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \ (z.B. Active Directory oder einem anderen Verbundservern Service\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Durch die Rangfolge der Regeln festlegen, können Sie optimieren oder Filtern Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden.  
  
-   Anspruchsregelvorlagen werden immer müssen Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit dem gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [der Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie anspruchsregelsätzen verarbeitet werden, finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="permit-all-users"></a>Alle Benutzer zulassen  
Wenn Sie die Regelvorlage für alle Benutzer zulassen verwenden, können alle Benutzer auf die vertrauende Seite zugreifen. Zusätzliche Autorisierungsregeln können Sie jedoch den Zugriff weiter einschränken. Wenn eine Regel erlaubt einem Benutzer Zugriff auf die vertrauende und eine andere Regel den Zugriff auf die vertrauende Seite verweigert, hat das Verweigern überschreibt die erlauben, weshalb, und der Benutzer der Zugriff verweigert wird.  
  
Benutzer, die Zugriff auf die vertrauende Seite vom Verbunddienst zulässig sind möglicherweise Dienst dennoch durch die vertrauende Seite verweigert werden.  
  
## <a name="permit-access-to-users-with-this-incoming-claim"></a>Benutzer mit diesem eingehenden Anspruch Zugriff gewähren  
Bei der Verwendung zulassen oder verweigern Benutzer basierend auf einer eingehenden Anspruchs Regelvorlage zum Erstellen einer Regel, und legen Sie die Bedingung aus, um zuzulassen, dass können Sie bestimmte Benutzer den Zugriff auf die vertrauende Seite basierend auf dem Typ und Wert eines eingehenden Anspruchs erlauben. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel, die nur Benutzer zulässt, die einer Gruppe mit dem Wert der Domänen-Admins geltend machen. Wenn eine Regel erlaubt einem Benutzer Zugriff auf die vertrauende und eine andere Regel den Zugriff auf die vertrauende Seite verweigert, hat das Verweigern überschreibt die erlauben, weshalb, und der Benutzer der Zugriff verweigert wird.  
  
Benutzer, die die vertrauende Seite vom Verbunddienst zugreifen können Dienst dennoch durch die vertrauende Seite verweigert werden. Wenn Sie allen Benutzern Zugriff auf die vertrauende gewähren möchten, verwenden Sie die Regelvorlage für alle Benutzer zulassen.  
  
## <a name="deny-access-to-users-with-this-incoming-claim"></a>Benutzern mit diesem eingehenden Anspruch Zugriff verweigern  
Bei der Verwendung zulassen oder verweigern Benutzer basierend auf einer eingehenden Anspruchs Regelvorlage zum Erstellen einer Regel, und legen Sie die Bedingung auf verweigern, können Sie Benutzer Zugriff auf die vertrauende Seite basierend auf dem Typ und Wert eines eingehenden Anspruchs verweigern. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel, die verweigert wird, dass alle Benutzer mit einer Gruppe mit einem Wert von Domänenbenutzern geltend machen.  
  
Wenn Sie die Bedingung "Verweigern" verwenden, aber den Zugriff auf die vertrauende Seite für bestimmte Benutzer möchten, müssen Sie später explizite Autorisierungsregeln mit der Bedingung zulassen, um diesen Benutzern den Zugriff auf die vertrauende Seite aktivieren hinzufügen.  
  
Wenn ein Benutzer Zugriff verweigert wird, wenn das anspruchsausstellungsmodul den Regelsatz verarbeitet, weitere Regeln, die Verarbeitung beendet wird, und AD FS die Fehlermeldung "Zugriff verweigert" auf Anforderung des Benutzers zurückgegeben.  
  
## <a name="authorizing-users"></a>Autorisieren von Benutzern  
In AD FS-Autorisierungsregeln werden verwendet, um Zulassungs- oder verweigerungsanspruchs, die bestimmt, ob ein Benutzer oder eine Gruppe von Benutzern \ (abhängig von der Anspruch Typ Used\) kann webbasierten Zugriff auf Ressourcen in einer bestimmten vertrauenden oder nicht. Autorisierungsregeln können nur für Vertrauensstellungen der vertrauenden Seite festgelegt werden.  
  
### <a name="authorization-rule-sets"></a>Autorisierungsregelsätze  
Verschiedene autorisierungsregelsätze vorhanden ist, abhängig vom Typ des zulassen oder verweigern, die Sie konfigurieren müssen. Diese Regel umfassen Folgendes:  
  
-   **Ausstellungsautorisierungsregeln**: Diese Regeln bestimmen, ob ein Benutzer Ansprüche für eine vertrauende Seite empfangen und kann, daher auf die vertrauende Seite zugreifen.  
  
-   **Delegationsautorisierungsregeln**: Diese Regeln bestimmen, ob ein Benutzer als ein anderer Benutzer auf die vertrauende Seite fungieren kann. Wenn ein Benutzer als ein anderer Benutzer fungiert, werden Ansprüche an den anfordernden Benutzer weiterhin im Token platziert.  
  
-   **Autorisierungsregeln für den Identitätswechsel**: Diese Regeln bestimmen, ob ein Benutzer vollständig die Identität eines anderen Benutzers auf die vertrauende Seite annehmen kann. Identität eines anderen Benutzers ist eine sehr leistungsstarke Funktion, da die vertrauende Seite nicht weiß, dass der Benutzer angenommen wird.  
  
Weitere Informationen dazu, wie der autorisierungsregelprozess in die anspruchsausstellungs-Pipeline einfügt finden Sie unter der Rolle des Anspruchsausstellungsmodul.  
  
### <a name="supported-claim-types"></a>Unterstützte Anspruchstypen  
AD-FSdefines Anspruchstypen zwei, die verwendet werden, um festzustellen, ob ein Benutzerzugriff erlaubt oder verweigert wird. Dieser Anspruchstypen Uniform Resource Identifiers \(URIs\) lauten wie folgt:  
  
1.  **Zulassen**: http:///\/schemas.microsoft.com\/authorization\/claims\/permit  
  
2.  **Verweigern**: http:///\/schemas.microsoft.com\/authorization\/claims\/deny  
  
## <a name="how-to-create-this-rule"></a>Vorgehensweise beim Erstellen dieser Regel  
Sie können beide Autorisierungsregeln entweder die anspruchsregelsprache oder Erstellen der **alle Benutzer zulassen** Regelvorlage oder die **zulassen oder verweigern Benutzer auf Basis eines eingehenden Anspruchs** Regelvorlage in AD FS-Verwaltungs-Snap-In. Alle Benutzer zulassen Regelvorlage bietet keine Konfigurationsoptionen. Zulassen oder verweigern Benutzer auf Basis einer eingehenden Anspruch Regelvorlage bietet jedoch die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Geben Sie einen eingehenden Anspruchstyp  
  
-   Geben Sie einen eingehenden Anspruchswert  
  
-   Benutzer mit diesem eingehenden Anspruch Zugriff gewähren  
  
-   Benutzern mit diesem eingehenden Anspruch Zugriff verweigern  
  
Weitere Informationen zum Erstellen dieser Vorlage finden Sie unter [Erstellen einer Regel zum Zulassen aller Benutzer](https://technet.microsoft.com/library/ee913577.aspx) oder [erstellen eine Regel zum Zulassen oder verweigern Benutzer basierend auf eines eingehenden Anspruchs](https://technet.microsoft.com/library/ee913594.aspx) in AD FS-Bereitstellungshandbuch.  
  
## <a name="using-the-claim-rule-language"></a>Mithilfe der anspruchsregelsprache  
Wenn ein Anspruch gesendet werden soll, nur, wenn der Wert des Anspruchs mit einem benutzerdefinierten Muster übereinstimmt, müssen Sie eine benutzerdefinierte Regel verwenden. Weitere Informationen finden Sie unter [verwenden eine benutzerdefinierte Anspruchsregel](When-to-Use-a-Custom-Claim-Rule.md).  
  
### <a name="example-of-how-to-create-an-authorization-rule-based-on-multiple-claims"></a>Beispiel zum Erstellen einer Autorisierungsregel basierend auf mehreren Ansprüchen  
Bei Verwendung der Syntax der anspruchsregelsprache zum Autorisieren von Ansprüchen kann ein Anspruch auch basierend auf dem Vorhandensein mehrerer Ansprüche in den ursprünglichen Ansprüchen des Benutzers ausgestellt werden. Die folgende Regel stellt einen autorisierungsanspruch nur dann, wenn der Benutzer ein Mitglied der Gruppe Editoren und mithilfe der Windows-Authentifizierung authentifiziert hat:  
  
```  
[type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod",   
value == "urn:federation:authentication:windows" ]  
&& [type == "http://schemas.xmlsoap.org/claims/Group ", value == “editors”]   
=> issue(type = "http://schemas.xmlsoap.org/claims/authZ", value = "Granted");  
```  
  
### <a name="example-of-how-to-create-authorization-rules-that-will-delegate-who-can-create-or-remove-federation-server-proxy-trusts"></a>Beispiel für die Autorisierung – Erstellen von Regeln, die delegieren, wer erstellen oder Entfernen von Vertrauensstellungen für den Verbundserverproxy  
Bevor ein Verbunddienst einen Verbundserverproxy zum Umleiten von Clientanforderungen verwenden können, muss zunächst eine Vertrauensstellung zwischen den Verbunddienst und die Verbundserverproxy-Computer hergestellt werden. Standardmäßig wird eine proxyvertrauensstellung eingerichtet Wenn eine der folgenden Anmeldeinformationen erfolgt erfolgreich in AD FS Federation Server Proxy-Konfigurations-Assistenten:  
  
-   Das Dienstkonto, das vom Verbunddienst, das der Proxy schützen wird verwendet  
  
-   Ein Active Directory-Domänenkonto, das Mitglied der lokalen Administratorengruppe auf allen Verbundservern in einer Verbundserverfarm ist  
  
Wenn Sie angeben, welche Benutzer oder der Benutzer eine proxyvertrauensstellung für einen bestimmten Verbunddienst erstellen können möchten, können Sie eine der folgenden Methoden der Delegierung. Diese Methoden sind in der Reihenfolge ihrer Priorität, basierend auf dem AD FS-Produktteam Empfehlungen der sichersten und unproblematischsten Methoden der Delegierung. Es ist erforderlich, verwenden Sie nur eine der folgenden Methoden, je nach den Anforderungen Ihrer Organisation:  
  
1.  Erstellen Sie eine Sicherheitsgruppe für die Domäne in Active Directory \ (z.B. FSProxyTrustCreators\), fügen Sie die Gruppe der lokalen Administratorengruppe auf jedem Verbundserver in der Farm und fügen dann nur die Benutzerkonten, die Sie dieses Recht auf die neue Gruppe delegieren möchten. Dies ist die bevorzugte Methode.  
  
2.  Fügen Sie das Konto des Benutzers Domäne der Gruppe "Administratoren" auf jedem Verbundserver in der Farm hinzu.  
  
3.  Wenn aus irgendeinem Grund Sie beide Methoden verwenden können, können Sie für diesen Zweck auch eine Autorisierungsregel erstellen. Obwohl es nicht empfohlen wird – aufgrund möglicher Komplikationen, die auftreten können, wenn diese Regel nicht richtig geschrieben ist, können Sie eine benutzerdefinierte Autorisierungsregel, um welche Active Directory zu delegieren, Domänenbenutzerkonten können auch erstellen oder sogar entfernen die Vertrauensstellungen zwischen allen Verbundserverproxys, die einem bestimmten Verbunddienst zugeordnet sind.  
  
    Wenn Sie Methode 3 wählen, können die folgende Regelsyntax eines autorisierungsanspruchs, die einen bestimmten Benutzer ermöglichen \ (in diesem Fall Contoso\\frankm\), Vertrauensstellungen für einen oder mehrere Federation Server-Proxys für den Verbunddienst zu erstellen. Sie müssen diese Regel mit dem Windows PowerShell-Befehl anwenden **Set-ADFSProperties-AddProxyAuthorizationRules**.  
  
    ```  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", issuer=~"^AD AUTHORITY$" value == "contoso\frankm" ] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true")  
  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
    Wenn Sie möchten den Benutzer zu entfernen, damit der Benutzer nicht mehr proxyvertrauensstellungen erstellen kann, können Sie später zur Standard-Proxy Vertrauensstellung Autorisierungsregel So entfernen Sie das Recht für den Benutzer zum Erstellen von proxyvertrauensstellungen für den Verbunddienst zurückkehren. Sie müssen auch diese Regel mit dem Windows PowerShell-Befehl anwenden **Set-ADFSProperties-AddProxyAuthorizationRules**.  
  
    ```  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
Weitere Informationen zur Verwendung die anspruchsregelsprache finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).  
  

