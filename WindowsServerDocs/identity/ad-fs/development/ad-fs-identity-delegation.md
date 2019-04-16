---
title: "Szenario mit identitätsdelegierung dar mit AD FS"
description: "Dieses Szenario beschreibt eine Anwendung, die muss die Back-End-Zugriff auf Ressourcen, die die Identität Delegierung Kette zugriffssteuerungsüberprüfungen ausführen müssen."
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b82d5fd749ac874d09bc54123727aaf902c4d778
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>Szenario mit identitätsdelegierung dar mit AD FS


[Beginnend mit .NET Framework 4.5, wurde Windows Identity Foundation (WIF) vollständig in .NET Framework integriert. Die Version des WIF Gegenstand dieses Thema WIF 3.5 ist veraltet und sollte nur verwendet werden, bei der Entwicklung mit .NET Framework 3.5 SP1 oder .NET Framework 4. Weitere Informationen zu WIF in .NET Framework 4.5, auch bekannt als WIF 4.5 finden Sie unter der Windows Identity Foundation-Dokumentation im .NET Framework 4.5-Entwicklerhandbuch.] 

Dieses Szenario beschreibt eine Anwendung, die muss die Back-End-Zugriff auf Ressourcen, die die Identität Delegierung Kette zugriffssteuerungsüberprüfungen ausführen müssen. Eine einfache Identität Delegierung Kette in der Regel Informationen zu den ersten Aufrufer und die Identität des direktaufrufer.

Mit dem Kerberos-Delegierungsmodell auf der Windows-Plattform noch heute haben die Back-End-Ressourcen Zugriff nur auf die Identität des direktaufrufer und nicht auf, die mit dem ursprünglichen Aufrufer. Dieses Modell wird häufig als Modell mit vertrauenswürdigem Subsystem bezeichnet. WIF verwaltet die Identität von den ursprünglichen Aufruf sowie den unmittelbaren Aufrufer in der Kette der Delegierung mithilfe der Schauspieler-Eigenschaft.

Das folgende Diagramm zeigt ein typisches Szenario mit identitätsdelegierung dar in der ein Fabrikam-Mitarbeiter in einer Anwendung Contoso.com verfügbar gemachten Ressourcen zugreift.

![Identität](media/ad-fs-identity-delegation/id1.png)

Die fiktiven Benutzer durch die Teilnahme an diesem Szenario sind:

- Frank: Ein Fabrikam-Mitarbeiter, die auf Contoso-Ressourcen zugreifen möchte.
- Daniel: Contoso Anwendungsentwickler, der die erforderlichen Änderungen in der Anwendung implementiert.
- ADAM: Contoso IT-Administrator.

Die Komponenten, die in diesem Szenario sind:

- web1: Web-Apps mit Links auf Back-End-Ressourcen, die die delegierte Identität mit dem ursprünglichen Aufrufer erfordern. Diese Anwendung wird mit ASP.NET erstellt.
- Ein Webdienst, der die delegierte Identität mit dem ursprünglichen Aufrufer, zusammen mit der direktaufrufer erfordert eine SQL Server greift auf. Dieser Dienst wird mit WCF erstellt.
- sts1: ein STS, der die Rolle des Anspruchsanbieters und gibt Ansprüche, die von der Anwendung (web1) erwartet werden. Vertrauensstellung mit Fabrikam.com sowie mit der Anwendung hergestellt hat.
- sts2: ein STS, der die Rolle der Identitätsanbieter für Fabrikam.com und bietet einen Endpunkt auf die der Fabrikam-Mitarbeiter, die zur Authentifizierung verwendet. Vertrauensstellung mit Contoso.com hergestellt hat, damit Fabrikam-Mitarbeiter Zugriff auf Ressourcen in Contoso.com zulässig sind.

>[!NOTE] 
>Der Begriff "ActAs Token", die häufig in diesem Szenario verwendet wird, bezieht sich auf ein Token, das von einem STS ausgestellt und die Identität des Benutzers enthält. Die Schauspieler-Eigenschaft enthält den STS-Identität.

Wie im obigen Diagramm gezeigt, ist der Fluss in diesem Szenario:


1. Die Contoso-Anwendung ist ein ActAs Token abrufen, die Identität der Fabrikam-Mitarbeiter und die sofortige Identität des Aufrufers in der Schauspieler-Eigenschaft enthält konfiguriert. Daniel hat sich auf die Anwendung implementiert werden.
2. Übergeben Sie das Token ActAs an den Back-End-Dienst ist die Contoso-Anwendung konfiguriert. Daniel hat sich auf die Anwendung implementiert werden.
3. Der Contoso-Webdienst ist konfiguriert, um das Token ActAs durch Aufrufen der sts1 überprüfen. ADAM aktiviert hat sts1 Delegierung Anforderungen verarbeiten.
4. Fabrikam Benutzer Frank greift auf die Contoso-Anwendung und erhält Zugriff auf die Back-End-Ressourcen.

## <a name="set-up-the-identity-provider-ip"></a>Einrichten des Identitätsanbieters (IP)

Es gibt drei Optionen für den Administrator Fabrikam.com Frank verfügbar:


1. Erwerben und Installieren eines STS-Produkts, z.B. Active Directory® Federation Services (AD FS).
2. Abonnieren Sie ein Cloud-STS-Produkt wie Live ID STS.
3. Erstellen eines benutzerdefinierten STS WIF verwenden.

In diesem Szenario Beispiel wird vorausgesetzt, dass Frank wählt die Option 1 und AD FS als IP-STS installiert. Zudem konfiguriert er einen Endpunkt mit dem Namen \windowsauth, um den Benutzer zu authentifizieren. Verweisen in der AD FS-Produktdokumentation und sprechen mit Adam, Contoso-IT-Administrator stellt Frank Vertrauensstellung mit der Domäne Contoso.com.

## <a name="set-up-the-claims-provider"></a>Richten Sie den Anspruchsanbieter

Die Optionen für den Administrator Contoso.com verfügbar Adam, sind identisch mit den zuvor für den Identitätsanbieter beschrieben. In diesem Szenario Beispiel wird vorausgesetzt, dass Adam wählt die Option 1 und der RP-STS AD FS 2.0 installiert.

## <a name="set-up-trust-with-the-ip-and-application"></a>Einrichten der Vertrauensstellung mit der IP- und die Anwendung

Anhand der AD FS-Dokumentation, schafft Adam Vertrauensstellung zwischen Fabrikam.com und der Anwendung.

## <a name="set-up-delegation"></a>Die Delegierung einrichten

AD FS bietet Delegierung Verarbeitung. Anhand der AD FS-Dokumentation, ermöglicht Adam die Verarbeitung von ActAs Token.

## <a name="application-specific-changes"></a>App-spezifischen Änderungen

Unterstützung für die identitätsdelegierung einer vorhandenen Anwendung hinzufügen, müssen die folgenden Änderungen vorgenommen werden. Daniel verwendet WIF, um diese Änderungen vorzunehmen.


- Zwischenspeichern der Bootstrap-Tokens, Empfangen von sts1 web1.
- Verwenden Sie CreateChannelActingAs mit dem ausgestellte Token, um einen Kanal an den Back-End-Webdienst zu erstellen.
- Rufen Sie die Back-End-Dienst-Methode.

## <a name="cache-the-bootstrap-token"></a>Das Bootstrap-Token-Cache

Das Bootstrap-Token ist das erste Token vom STS ausgestellt, und die Anwendung extrahiert Ansprüche aus. In diesem Beispielszenario dieses Token von sts1 für den Benutzer Frank ausgestellt, und die Anwendung zwischengespeichert. Das folgende Codebeispiel veranschaulicht einen Bootstrap abrufen Token in einer Anwendung ASP.NET:

```
// Get the Bootstrap Token
SecurityToken bootstrapToken = null;

IClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as IClaimsPrincipal;
if ( claimsPrincipal != null )
{
    IClaimsIdentity claimsIdentity = (IClaimsIdentity)claimsPrincipal.Identity;
    bootstrapToken = claimsIdentity.BootstrapToken;
}
```
WIF stellt eine Methode [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx), erstellt einen Kanal des angegebenen Typs, der tokenausstellungs-Anforderungen mit dem angegebenen Sicherheitstoken als Element ActAs erweitert. Sie können das Bootstrap-Token an diese Methode übergeben und rufen Sie dann die erforderlichen Service-Methode für die zurückgegebene Kanal. In diesem Beispielszenario Frank Identität hat die [Schauspieler](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.iclaimsidentity.actor.aspx) -Eigenschaft auf web1 die Identität festgelegt.

Der folgende Codeausschnitt zeigt einen Aufruf an den Webdienst mit [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx), und rufen Sie eine der Methoden für den Dienst, ComputeResponse, klicken Sie dann auf die zurückgegebene Kanal:

```
// Get the channel factory to the backend service from the application state
ChannelFactory<IService2Channel> factory = (ChannelFactory<IService2Channel>)Application[Global.CachedChannelFactory];

// Create and setup channel to talk to the backend service
IService2Channel channel;
lock (factory)
{
// Setup the ActAs to point to the caller's token so that we perform a 
// delegated call to the backend service
// on behalf of the original caller.
    channel = factory.CreateChannelActingAs<IService2Channel>(callerToken);
}

string retval = null;

// Call the backend service and handle the possible exceptions
try
{
    retval = channel.ComputeResponse(value);
    channel.Close();
} catch (Exception exception)
{
    StringBuilder sb = new StringBuilder();
    sb.AppendLine("An unexpected exception occurred.");
    sb.AppendLine(exception.StackTrace);
    channel.Abort();
    retval = sb.ToString();
}

```
## <a name="web-service-specific-changes"></a>Web Service-spezifischer Änderungen

Da der Webdienst mit WCF erstellt und für WIF, aktiviert werden, wenn die Bindung mit der richtigen Ausstelleradresse solches Element konfiguriert ist, wird die Überprüfung der ActAs automatisch durch WIF behandelt. 

Der Webdienst gibt an, von der Anwendung benötigten spezifischen Methoden. Es gibt keine speziellen Code-Änderungen auf den Dienst erforderlich. Das folgende Codebeispiel zeigt die Konfiguration des Webdiensts mit solches Element:

```
// Configure the issued token parameters with the correct settings
IssuedSecurityTokenParameters itp = new IssuedSecurityTokenParameters( "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" );
itp.IssuerMetadataAddress = new EndpointAddress( "http://localhost:6000/STS/mex" );
itp.IssuerAddress = new EndpointAddress( "http://localhost:6000/STS" );

// Create the security binding element
SecurityBindingElement sbe = SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement( itp );
sbe.MessageSecurityVersion = MessageSecurityVersion.WSSecurity11WSTrust13WSSecureConversation13WSSecurityPolicy12BasicSecurityProfile10;

// Create the HTTP transport binding element
HttpTransportBindingElement httpBE = new HttpTransportBindingElement();

// Create the custom binding using the prepared binding elements
CustomBinding binding = new CustomBinding( sbe, httpBE );

using ( ServiceHost host = new ServiceHost( typeof( Service2 ), new Uri( "http://localhost:6002/Service2" ) ) )
{
    host.AddServiceEndpoint( typeof( IService2 ), binding, "" );
    host.Credentials.ServiceCertificate.SetCertificate( "CN=localhost", StoreLocation.LocalMachine, StoreName.My );

// Enable metadata generation via HTTP GET
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
    smb.HttpGetEnabled = true;
    host.Description.Behaviors.Add( smb );
    host.AddServiceEndpoint( typeof( IMetadataExchange ), MetadataExchangeBindings.CreateMexHttpBinding(), "mex" );

// Configure the service host to use WIF
    ServiceConfiguration configuration = new ServiceConfiguration();
    configuration.IssuerNameRegistry = new TrustedIssuerNameRegistry();

    FederatedServiceCredentials.ConfigureServiceHost( host, configuration );

    host.Open();

    Console.WriteLine( "Service2 started, press ENTER to stop ..." );
    Console.ReadLine();

    host.Close();
}
```

## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
