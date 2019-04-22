---
title: Szenario mit identitätsdelegierung mit AD FS
description: Dieses Szenario beschreibt eine Anwendung, die Back-End-Zugriff auf Ressourcen, die die identitätsdelegierungskette benötigt auszuführenden zugriffssteuerungsüberprüfungen erfordern.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b82d5fd749ac874d09bc54123727aaf902c4d778
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819851"
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>Szenario mit identitätsdelegierung mit AD FS


[Ab .NET Framework 4.5, wurde Windows Identity Foundation (WIF) vollständig in .NET Framework integriert. Die Version von WIF, die diesem Thema, WIF 3.5 ist veraltet und sollte nur verwendet werden, wenn Sie für die .NET Framework 3.5 SP1 oder .NET Framework 4 entwickeln. Weitere Informationen über WIF in .NET Framework 4.5, auch bekannt als WIF 4.5 finden Sie unter der Windows Identity Foundation-Dokumentation in der .NET Framework 4.5-Entwicklungsleitfaden.] 

Dieses Szenario beschreibt eine Anwendung, die Back-End-Zugriff auf Ressourcen, die die identitätsdelegierungskette benötigt auszuführenden zugriffssteuerungsüberprüfungen erfordern. Eine einfache identitätsdelegierungskette besteht in der Regel die Informationen zu den ursprünglichen Aufrufer und die Identität des unmittelbaren Aufrufers aus.

Mit dem Kerberos-Delegierung-Modell auf der Windows-Plattform noch heute stehen alle Back-End-Ressourcen Zugriff nur für die Identität des unmittelbaren Aufrufers und nicht auf die von den ursprünglichen Aufrufer. Dieses Modell wird häufig als vertrauenswürdiges Subsystem Modell bezeichnet. WIF behält die Identität des ursprünglichen Aufrufers sowie der direkte Aufrufer in der delegierungskette mithilfe der Actor-Eigenschaft.

Das folgende Diagramm veranschaulicht einen typischen identitätsdelegierungsszenario in der ein Fabrikam-Mitarbeiter in einer "contoso.com"-Anwendung verfügbar gemachten Ressourcen zugreift.

![Identität](media/ad-fs-identity-delegation/id1.png)

Die fiktiven Benutzer, die in diesem Szenario beteiligt sind:

- Frank: Ein Mitarbeiter von Fabrikam, Contoso-Ressourcen zugreifen möchte.
- Daniel: Ein Entwickler der Contoso-Anwendung, die die erforderlichen Änderungen in der Anwendung implementiert.
- Adam: Der Contoso-IT-Administrator.

Die Komponenten, die in diesem Szenario sind:

- web1: Eine Webanwendung mit Verknüpfungen zu Back-End-Ressourcen, die die delegierten Identität des ursprünglichen Aufrufers erfordern. Diese Anwendung wird mit ASP.NET erstellt.
- Einen Webdienst, der auf einem SQL Server zugreift, müssen Sie die delegierte Identität des ursprünglichen Aufrufers, zusammen mit der der direkte Aufrufer. Dieser Dienst wird mit WCF erstellt.
- sts1: Ein STS, der die Rolle der Anspruchsanbieter-Vertrauensstellung ist, und gibt die Ansprüche, die von der Anwendung (web1) erwartet werden. Mit "Fabrikam.com" und auch mit der Anwendung hergestellt hat.
- sts2: Ein STS, der in der Rolle des Identitätsanbieters für "Fabrikam.com" und stellt einen Endpunkt auf dem der Fabrikam-Mitarbeiter, die zur Authentifizierung verwendet. Vertrauensstellung mit "contoso.com" hergestellt hat, damit der Fabrikam-Mitarbeiter den Zugriff auf Ressourcen auf "contoso.com" zulässig sind.

>[!NOTE] 
>Der Begriff "ActAs-Token", das häufig in diesem Szenario verwendet wird, bezieht sich auf ein Token, das von einem STS ausgestellt wird, und die Identität des Benutzers enthält. Die Actor-Eigenschaft enthält die STS Dienste-Identität.

Wie in der vorherigen Abbildung gezeigt wird, wird der Flow in diesem Szenario:


1. Um ein ActAs-Token zu erhalten, das die Fabrikam Identität des Mitarbeiters und die sofortige Identität des Aufrufers in der Actor-Eigenschaft enthält ist die Anwendung von Contoso konfiguriert. Daniel hat diese Änderungen an der Anwendung implementiert.
2. Die Anwendung von Contoso ist konfiguriert, um das ActAs-Token an die Back-End-Dienst zu übergeben. Daniel hat diese Änderungen an der Anwendung implementiert.
3. Der Contoso Web-Dienst ist um das ActAs-Token zu überprüfen, durch den Aufruf von sts1 konfiguriert. ADAM hat sts1 zum Verarbeiten von Anforderungen der Delegierung aktiviert.
4. Fabrikam-Benutzer Frank greift auf die Contoso-Anwendung und erhält Zugriff auf die Back-End-Ressourcen.

## <a name="set-up-the-identity-provider-ip"></a>Richten Sie den Identitätsanbieter (IP)

Drei Optionen stehen zur Verfügung, für den Administrator "Fabrikam.com" Frank:


1. Erwerben Sie und installieren Sie einen STS-Produkt wie Active Directory® Federation Services (AD FS).
2. Abonnieren Sie ein Cloud-STS-Produkt wie Live ID-STS aus.
3. Erstellen Sie einen benutzerdefinierten STS mit WIF.

In diesem Beispielszenario wird davon ausgegangen, dass Frank option1 auswählt und die IP-STS AD FS installiert. Er konfiguriert außerdem einen Endpunkt, mit dem Namen \windowsauth, um den Benutzer zu authentifizieren. Verweisen auf die AD FS-Produktdokumentation und die Kommunikation mit Adam, Contoso IT-Administrator richtet Frank Vertrauensstellung mit der Domäne "contoso.com".

## <a name="set-up-the-claims-provider"></a>Einrichten der Anspruchsanbieter-Vertrauensstellung

Die Optionen für den Administrator für "contoso.com" verfügbar, Adam, entsprechen wie zuvor für den Identitätsanbieter beschrieben. In diesem Beispielszenario wird davon ausgegangen, dass Adam wählt die Option 1 aus, und die RP-STS AD FS 2.0 installiert.

## <a name="set-up-trust-with-the-ip-and-application"></a>Einrichten der Vertrauensstellung mit der IP-Adresse und die Anwendung

Verweisen Sie auf der AD FS-Dokumentation, richtet Adam die Vertrauensstellung zwischen "Fabrikam.com" und die Anwendung.

## <a name="set-up-delegation"></a>Einrichten der Delegierung

AD FS bietet Delegierung Verarbeitung. Finden Sie in der Dokumentation zu AD FS, kann Adam für die Verarbeitung von ActAs-Token.

## <a name="application-specific-changes"></a>Anwendungsspezifische Änderungen

Unterstützung für die identitätsdelegierung zu einer vorhandenen Anwendung hinzufügen, müssen die folgenden Änderungen vorgenommen werden. Daniel verwendet WIF, um diese Änderungen vorzunehmen.


- Zwischenspeichern von bootstrap-Token, web1 von sts1 empfangen.
- Verwenden Sie CreateChannelActingAs den ausgestellten Token, um einen Kanal an den Back-End-Webdienst zu erstellen.
- Rufen Sie die Back-End-Dienst-Methode.

## <a name="cache-the-bootstrap-token"></a>Bootstrap-Token-Cache

Bootstrap-Token ist die erste von der STS ausgegebenen Token, und die Anwendung extrahiert die Ansprüche aus. In diesem Beispielszenario dieses Token wird von sts1 für den Benutzer Frank ausgestellt, und die Anwendung zwischengespeichert. Das folgende Codebeispiel zeigt zum Abrufen von Bootstrap-Tokens in einer ASP.NET-Anwendung:

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
WIF stellt eine Methode, [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx), erstellt einen Kanal des angegebenen Typs, die Anforderungen der Ausstellung von token mit dem angegebenen Sicherheitstoken als ein ActAs-Element erweitert. Sie können bootstrap-Token an diese Methode übergeben und dann die erforderlichen Service-Methode aufrufen, auf dem Kanal zurückgegeben. In diesem Beispielszenario Franks Identität verfügt über die [Actor](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.iclaimsidentity.actor.aspx) -Eigenschaft auf web1 die Identität festgelegt.

Der folgende Codeausschnitt zeigt, wie an den Webdienst mit [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx) und rufen Sie eine der Methoden des Diensts ComputeResponse, klicken Sie dann auf dem Kanal zurückgegeben:

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
## <a name="web-service-specific-changes"></a>Web Service-spezifisches Änderungen

Da der Webdienst mit WCF erstellt und für WIF aktiviert werden, nachdem die Bindung mit IssuedSecurityTokenParameters mit der richtigen Issuer-Adresse konfiguriert wurde, wird die Überprüfung der ActAs von WIF automatisch behandelt. 

Der Webdienst stellt die spezifischen Methoden, die von der Anwendung benötigt. Es gibt keine bestimmte codeänderungen, die für den Dienst erforderlich sind. Das folgende Codebeispiel zeigt die Konfiguration des Webdiensts mit IssuedSecurityTokenParameters:

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
