---
ms.assetid: b734cbcb-342c-4a28-8ab5-b9cd990bb1c2
title: Wann sollte eine Autorisierungsanspruchsregel verwendet werden
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d566113a7579805c8ae9b558a145878557de0958
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872331"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="when-to-use-an-authorization-claim-rule"></a>Wann sollte eine Autorisierungsanspruchsregel verwendet werden
Sie können diese Regel in Active Directory-Verbunddienste \(AD FS\) Wenn müssen Sie einen eingehenden Anspruchstyp und klicken Sie dann eine Aktion anwenden, die bestimmen, ob ein Benutzer wird gewährt oder den Zugriff verweigert auf Grundlage des Werts, den Sie Geben Sie in der Regel an. Wenn Sie diese Regel verwenden, leiten Sie Ansprüche weiter bzw. transformieren Ansprüche, die der folgenden Regellogik entsprechen. Dies geschieht auf Basis der Optionen, die Sie in der Regel konfigurieren:  
  
|Regeloption|Regellogik|  
|---------------|--------------|  
|Alle Benutzer zulassen|Wenn der Typ des eingehenden Anspruchs einem *beliebigen Anspruchstyp* und der Wert einem *beliebigen Wert*entspricht, wird der Ausstellungsanspruch mit Wert auf *Zulassen*festgelegt.|  
|Benutzern mit diesem eingehenden Anspruch Zugriff gewähren|Wenn der Typ des eingehenden Anspruchs einem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert*entspricht, wird der Ausstellungsanspruch mit Wert auf *Zulassen*festgelegt.|  
|Benutzern mit diesem eingehenden Anspruch Zugriff verweigern|Wenn der Typ des eingehenden Anspruchs einem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert* entspricht, wird der Ausstellungsanspruch mit Wert auf *Verweigern* festgelegt.|  
  
Die folgenden Abschnitte enthalten eine grundlegende Einführung in Anspruchsregeln und bieten weitere Details zur Verwendung dieser Regeln.  
  
## <a name="about-claim-rules"></a>Informationen zu Anspruchsregeln  
Eine Anspruchsregel stellt eine Instanz der Geschäftslogik, wird die einen eingehenden Anspruch eine Bedingung anwendet \(If x, dann y\) und Grundlage, auf der Bedingungsparameter einen ausgehenden Anspruch erzeugt. Die folgende Liste enthält wichtige Tipps zu Anspruchsregeln, die Sie kennen sollten, bevor Sie fortfahren, dieses Thema zu lesen:  
  
-   Im AD FS-Verwaltungs-Snap-\-in Anspruch Regeln können nur mit anspruchsregelvorlagen erstellt werden  
  
-   Anspruch Regeln verarbeiten eingehende Ansprüche entweder direkt von einem Anspruchsanbieter \(wie Active Directory oder einem anderen Verbunddienst\) oder aus der Ausgabe der akzeptanztransformationsregeln in einer Anspruchsanbieter-Vertrauensstellung.  
  
-   Anspruchsregeln werden vom Anspruchsausstellungsmodul chronologisch nach einem bestimmten Regelsatz verarbeitet. Indem Sie eine Rangfolge der Regeln festlegen, können Sie Ansprüche, die durch vorausgehende Regeln in einem bestimmten Regelsatz generiert werden, weiter optimieren oder filtern.  
  
-   Anspruchsregelvorlagen erfordern immer, dass Sie einen eingehenden Anspruchstyp angeben. Allerdings können Sie mehrere Anspruchswerte mit den gleichen Anspruchstyp mithilfe einer einzigen Regel verarbeiten.  
  
Ausführlichere Informationen zu Anspruchsregeln und anspruchsregelsätzen finden Sie unter [die Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln finden Sie unter [die Rolle des Anspruchsmoduls](The-Role-of-the-Claims-Engine.md). Weitere Informationen wie die Regel von Anspruchssätze verarbeitet werden, finden Sie unter [die Rolle der Anspruchspipeline](The-Role-of-the-Claims-Pipeline.md).  
  
## <a name="permit-all-users"></a>Alle Benutzer zulassen  
Wenn Sie die Regelvorlage "Alle Benutzer zulassen" verwenden, haben alle Benutzer Zugriff auf die vertrauende Seite. Mithilfe zusätzliche Autorisierungsregeln können Sie jedoch den Zugriff weiter einschränken. Wenn eine Regel einem Benutzer den Zugriff auf die vertrauende Seite erlaubt und eine andere Regel den Zugriff des Benutzers auf die vertrauende Seite verweigert, hat das Verweigern Vorrang vor dem Erlauben, weshalb dem Benutzer der Zugriff verweigert wird.  
  
Benutzern, denen der Zugriff auf die vertrauende Seite über den Verbunddienst erlaubt wird, kann der Dienst durch die vertrauende Seite dennoch verweigert werden.  
  
## <a name="permit-access-to-users-with-this-incoming-claim"></a>Benutzern mit diesem eingehenden Anspruch Zugriff gewähren  
Wenn Sie die Regelvorlage "Benutzer auf Basis eines eingehenden Anspruchs zulassen oder verweigern" zum Erstellen einer Regel nutzen und die Bedingung auf "Erlauben" festlegen, können Sie den Zugriff durch den jeweiligen Benutzer auf die vertrauende Seite basierend auf dem Typ und Wert eines eingehenden Anspruchs erlauben. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel nutzen, die nur Benutzer zulässt, die einen Gruppenanspruch mit dem Wert "Domänenadministratoren" haben. Wenn eine Regel einem Benutzer den Zugriff auf die vertrauende Seite erlaubt und eine andere Regel den Zugriff des Benutzers auf die vertrauende Seite verweigert, hat das Verweigern Vorrang vor dem Erlauben, weshalb dem Benutzer der Zugriff verweigert wird.  
  
Benutzern, denen der Zugriff auf die vertrauende Seite über den Verbunddienst erlaubt wird, kann der Dienst durch die vertrauende Seite dennoch verweigert werden. Wenn alle Benutzer Zugriff auf die vertrauende Seite haben sollen, verwenden Sie die Regelvorlage "Alle Benutzer zulassen".  
  
## <a name="deny-access-to-users-with-this-incoming-claim"></a>Benutzern mit diesem eingehenden Anspruch Zugriff verweigern  
Wenn Sie die Regelvorlage "Benutzer auf Basis eines eingehenden Anspruchs zulassen oder verweigern" zum Erstellen einer Regel nutzen und die Bedingung auf Verweigern" festlegen, können Sie den Zugriff durch den Benutzer auf die vertrauende Seite basierend auf dem Typ und Wert eines eingehenden Anspruchs verweigern. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel nutzen, die alle Benutzer verweigert, die einen Gruppenanspruch mit dem Wert "Domänenbenutzer" haben.  
  
Wenn Sie die Bedingung "Verweigern" verwenden, aber bestimmten Benutzern dennoch den Zugriff auf die vertrauende Seite erlauben möchten, müssen Sie später explizite Autorisierungsregeln mit der Bedingung "Erlauben" hinzufügen, um diesen Benutzern den Zugriff auf die vertrauende Seite zu ermöglichen.  
  
Wenn ein Benutzer Zugriff verweigert wird, wenn die anspruchsausstellungs-Engine den Regelsatz verarbeitet, weitere regelverarbeitung beendet wird, und AD FS gibt einen Fehler "Zugriff verweigert" zurück, um die Anforderung des Benutzers.  
  
## <a name="authorizing-users"></a>Autorisieren von Benutzern  
In AD FS dienen Autorisierungsregeln Ausstellung eines Zulassungs-oder verweigerungsanspruchs, der bestimmt, ob ein Benutzer oder eine Gruppe von Benutzern \(je nach den verwendeten Anspruchstyp\) gestattet ist, die Zugriff auf Web\-Ressourcen in einer bestimmten der vertrauenden Seite die Partei oder nicht. Autorisierungsregeln können nur für Vertrauensstellungen der vertrauenden Seite festgelegt werden.  
  
### <a name="authorization-rule-sets"></a>Autorisierungsregelsätze  
Je nach Typ des Vorgangs (Erlauben oder Verweigern), den Sie konfigurieren möchten, gibt es verschiedene Autorisierungsregelsätze. Diese Regel umfassen Folgendes:  
  
-   **Ausstellungsautorisierungsregeln**: Diese Regeln bestimmen, ob ein Benutzer Ansprüche für eine vertrauende Seite empfangen und damit auf die vertrauende Seite zugreifen kann.  
  
-   **Delegierungsautorisierungsregeln**: Diese Regeln bestimmen, ob ein Benutzer für die vertrauende Seite als ein anderer Benutzer fungieren kann. Wenn ein Benutzer als ein anderer Benutzer fungiert, werden Ansprüche an den anfordernden Benutzer weiter im Token platziert.  
  
-   **Autorisierungsregeln für den Identitätswechsel**: Diese Regeln bestimmen, ob ein Benutzer vollständig die Identität eines anderen Benutzers für die vertrauende Seite annehmen kann. Die Identität eines anderen Benutzers anzunehmen ist eine sehr leistungsstarke Funktion, da die vertrauende Seite nicht weiß, dass der Benutzer die Identität eines anderen angenommen hat.  
  
Weitere Informationen dazu, wie sich der Autorisierungsregelprozess in die Anspruchsausstellungs-Pipeline einfügt, finden Sie unter "Die Rolle des Anspruchsausstellungsmoduls".  
  
### <a name="supported-claim-types"></a>Unterstützte Anspruchstypen  
AD FS definiert zwei Anspruchstypen, die verwendet werden, um festzustellen, ob ein Benutzerzugriff erlaubt oder verweigert wird. Dieser Anspruchstyp Uniform Resource Identifiers \(URIs\) lauten wie folgt:  
  
1.  **Permit**: http:\/\/schemas.microsoft.com\/authorization\/claims\/permit  
  
2.  **Verweigern**: http:\/\/schemas.microsoft.com\/Autorisierung\/Ansprüche\/verweigern  
  
## <a name="how-to-create-this-rule"></a>Erstellen dieser Regel  
Sie können beide Autorisierungsregeln entweder die anspruchsregelsprache oder Erstellen der **alle Benutzer zulassen** Regelvorlage oder **zulassen oder verweigern Benutzer auf der Grundlage eines eingehenden Anspruchs** Regelvorlage in der AD FS Verwaltung-Snap-in\-in. Die Regelvorlage "Alle Benutzer zulassen" bietet keine Konfigurationsoptionen. Die Regelvorlage "Benutzer auf Basis eines eingehenden Anspruchs zulassen oder verweigern" bietet dagegen die folgenden Konfigurationsoptionen:  
  
-   Anspruchsregelname angeben  
  
-   Eingehenden Anspruchstyp angeben  
  
-   Wert eines eingehenden Anspruchs eingeben  
  
-   Benutzern mit diesem eingehenden Anspruch Zugriff gewähren  
  
-   Benutzern mit diesem eingehenden Anspruch Zugriff verweigern  
  
Weitere Anweisungen zum Erstellen dieser Vorlage finden Sie [erstellen eine Regel für alle Benutzer zulassen](https://technet.microsoft.com/library/ee913577.aspx) oder [erstellen Sie eine Regel zum Zulassen oder verweigern Benutzer basierend auf einem eingehenden Anspruch](https://technet.microsoft.com/library/ee913594.aspx) in AD FS-Bereitstellungshandbuch.  
  
## <a name="using-the-claim-rule-language"></a>Verwenden der Anspruchsregelsprache  
Falls ein Anspruch nur gesendet werden soll, wenn der Wert des Anspruchs mit einem benutzerdefinierten Muster übereinstimmt, müssen Sie eine benutzerdefinierte Regel verwenden. Weitere Informationen finden Sie unter [When to Use a Custom Claim Rule](When-to-Use-a-Custom-Claim-Rule.md).  
  
### <a name="example-of-how-to-create-an-authorization-rule-based-on-multiple-claims"></a>Beispiel der Erstellung einer Autorisierungsregel basierend auf mehreren Ansprüchen  
Bei Verwenden der Syntax der Anspruchsregelsprache zum Autorisieren von Ansprüchen kann ein Anspruch auch basierend auf dem Vorhandensein mehrerer Ansprüche in den ursprünglichen Ansprüchen des Benutzers ausgestellt werden. Die folgende Regel stellt einen Autorisierungsanspruch nur dann aus, wenn der Benutzer Mitglied der Gruppe "Editoren" ist und sich mithilfe der Windows-Authentifizierung authentifiziert hat:  
  
```  
[type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod",   
value == "urn:federation:authentication:windows" ]  
&& [type == "http://schemas.xmlsoap.org/claims/Group ", value == “editors”]   
=> issue(type = "http://schemas.xmlsoap.org/claims/authZ", value = "Granted");  
```  
  
### <a name="example-of-how-to-create-authorization-rules-that-will-delegate-who-can-create-or-remove-federation-server-proxy-trusts"></a>Beispiel der Erstellung von Autorisierungsregeln, die delegieren, wer Vertrauensstellungen für den Verbundserverproxy erstellen oder entfernen darf  
Ehe ein Verbunddienst einen Verbundserverproxy zum Umleiten von Clientanforderungen nutzen kann, muss zwischen dem Verbunddienst und dem Computer mit dem Verbundserverproxy eine Vertrauensstellung eingerichtet werden. Standardmäßig wird eine Proxyvertrauensstellung eingerichtet, wenn eine Variante der folgenden Anmeldeinformation erfolgreich in den Assistenten für die Konfiguration eines AD FS-Verbundserverproxys eingegeben wird:  
  
-   Für das Dienstkonto, das vom Verbunddienst verwendet wird, das der Proxy schützen soll  
  
-   Für ein Active Directory-Domänenkonto, das Mitglied der lokalen Gruppe "Administratoren" auf allen Verbundservern in einer Verbundserverfarm ist  
  
Wenn Sie angeben möchten, welche Benutzer eine Proxyvertrauensstellung für einen bestimmten Verbunddienst erstellen dürfen, können Sie für die Delegierung eine der folgenden Methoden verwenden. Diese Methoden sind in der Reihenfolge ihrer Priorität angegeben, und zwar basierend auf den Empfehlungen des AD FS-Produktteams zu den sichersten und unproblematischsten Methoden der Delegierung. Je nach den Erfordernissen Ihrer Organisation muss nur eine dieser Methoden verwendet werden:  
  
1.  Erstellen Sie in Active Directory eine Domänensicherheitsgruppe \(z. B. FSProxyTrustCreators\), fügen Sie die Gruppe der lokalen Administratorgruppe auf jedem Verbundserver in der Farm und fügen Sie dann nur die Benutzerkonten erfolgen soll Dieses Recht für die neue Gruppe zu delegieren. Dies ist die bevorzugte Methode.  
  
2.  Fügen Sie das Domänenkonto des Benutzers der Gruppe "Administratoren" auf jedem Verbundserver in der Farm hinzu.  
  
3.  Wenn Sie aus irgendeinem Grund beide Methoden nicht verwenden können, können Sie für diesen Zweck auch eine Autorisierungsregel erstellen. Dies wird aufgrund möglicher Komplikationen, die auftreten können, wenn diese Regel nicht richtig geschrieben wird, nicht empfohlen. Sie können jedoch eine benutzerdefinierte Autorisierungsregel zum Delegieren erstellen, welche Active Directory-Domänenbenutzerkonten die Vertrauensstellungen zwischen allen Verbundserverproxys erstellen oder sogar entfernen können, die einem bestimmten Verbunddienst zugeordnet sind.  
  
    Wenn Sie Methode 3 wählen, können Sie die folgende Regelsyntax verwenden, einen autorisierungsanspruch ausgeben, die einen angegebenen Benutzer ermöglichen \(in diesem Fall Contoso\\Frankm\) zum Erstellen von Vertrauensstellungen für den Verbund für eine oder mehrere Server-Proxys für die Der Verbunddienst. Sie müssen diese Regel, die mit dem Windows PowerShell-Befehl anwenden **festgelegt\-ADFSProperties-AddProxyAuthorizationRules**.  
  
    ```  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", issuer=~"^AD AUTHORITY$" value == "contoso\frankm" ] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true")  
  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
    Wenn Sie später den Benutzer entfernen möchten, damit er keine weiteren Proxyvertrauensstellungen erstellen kann, können Sie die standardmäßige Autorisierungsregel für Proxyvertrauensstellungen umkehren, um das Recht des Benutzers zum Erstellen von Proxyvertrauensstellungen für den Verbunddienst aufzuheben. Sie müssen auch diese Regel, die mit dem Windows PowerShell-Befehl anwenden **festgelegt\-ADFSProperties-AddProxyAuthorizationRules**.  
  
    ```  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
Weitere Informationen zur Verwendung die anspruchsregelsprache finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).  
  

