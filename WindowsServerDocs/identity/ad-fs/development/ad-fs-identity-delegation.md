---
title: Identitäts Delegierungs Szenario mit AD FS
description: In diesem Szenario wird eine Anwendung beschrieben, die auf Back-End-Ressourcen zugreifen muss, die die Identitäts Delegierungs Kette für die Durchführung von Zugriffs Steuerungs Prüfungen benötigen.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 292bec5f73e2746103ffc41cde729ddc59728e0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407878"
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>Identitäts Delegierungs Szenario mit AD FS


[Windows Identity Foundation (WIF) wurde ab dem .NET Framework 4,5 vollständig in das .NET Framework integriert. Die in diesem Thema, WIF 3,5, adressierte WIF-Version ist veraltet und sollte nur bei der Entwicklung für die .NET Framework 3,5 SP1 oder .NET Framework 4 verwendet werden. Weitere Informationen zu WIF im .NET Framework 4,5, auch bekannt als WIF 4,5, finden Sie in der Dokumentation zu Windows Identity Foundation im .NET Framework 4,5-Entwicklungs Handbuch. 

In diesem Szenario wird eine Anwendung beschrieben, die auf Back-End-Ressourcen zugreifen muss, die die Identitäts Delegierungs Kette für die Durchführung von Zugriffs Steuerungs Prüfungen benötigen. Eine einfache Identitäts Delegierungs Kette besteht normalerweise aus den Informationen zum ursprünglichen Aufrufer und der Identität des unmittelbaren Aufrufers.

Mit dem Kerberos-Delegierungs Modell auf der Windows-Plattform haben die Back-End-Ressourcen nur Zugriff auf die Identität des unmittelbaren Aufrufers und nicht auf die des anfänglichen Aufrufers. Dieses Modell wird im Allgemeinen als vertrauenswürdiges subsystemmodell bezeichnet. WIF verwaltet die Identität des ursprünglichen Aufrufers und des unmittelbaren Aufrufers in der Delegierungs Kette mithilfe der Actor-Eigenschaft.

Das folgende Diagramm veranschaulicht ein typisches Identitäts Delegierungs Szenario, bei dem ein Fabrikam-Mitarbeiter auf Ressourcen zugreift, die in einer contoso.com-Anwendung verfügbar gemacht werden

![Identität](media/ad-fs-identity-delegation/id1.png)

Die fiktiven Benutzer, die an diesem Szenario teilnehmen, sind:

- Offen Ein Fabrikam-Mitarbeiter, der auf die Ressourcen von "Configuration Manager" zugreifen möchte.
- Daniel Ein Anwendungsentwickler von Configuration Manager, der die erforderlichen Änderungen in der Anwendung implementiert.
- Adam Der IT-Administrator von "Configuration Manager".

Folgende Komponenten sind an diesem Szenario beteiligt:

- web1 Eine Webanwendung mit Links zu Back-End-Ressourcen, die die Delegierte Identität des anfänglichen Aufrufers benötigen. Diese Anwendung wird mit ASP.NET erstellt.
- Ein Webdienst, der auf eine SQL Server zugreift, die die Delegierte Identität des anfänglichen Aufrufers erfordert, zusammen mit der des unmittelbaren Aufrufers. Dieser Dienst wird mit WCF erstellt.
- sts1: Ein STS, der die Rolle des Anspruchs Anbieters hat, und gibt Ansprüche aus, die von der Anwendung erwartet werden (web1). Sie hat eine Vertrauensstellung mit fabrikam.com und auch mit der Anwendung hergestellt.
- sts2: Ein STS, der sich in der Rolle des Identitäts Anbieters für fabrikam.com befindet und einen Endpunkt bereitstellt, den der Fabrikam-Mitarbeiter zum Authentifizieren verwendet. Sie hat eine Vertrauensstellung mit contoso.com hergestellt, sodass Fabrikam-Mitarbeiter auf Ressourcen auf contoso.com zugreifen können.

>[!NOTE] 
>Der Begriff "ACTAS Token", der in diesem Szenario häufig verwendet wird, bezieht sich auf ein Token, das von einem STS ausgegeben wird und die Identität des Benutzers enthält. Die Actor-Eigenschaft enthält die STS-Identität.

Wie im vorherigen Diagramm gezeigt, ist der Ablauf in diesem Szenario:


1. Die Anwendung "Configuration Manager" ist so konfiguriert, dass Sie ein ACTAS-Token erhält, das sowohl die Identität des Fabrikam-Mitarbeiters als auch die Identität des unmittelbaren Aufrufers in der Actor-Eigenschaft enthält. Daniel hat diese Änderungen für die Anwendung implementiert.
2. Die Anwendung "atoso" ist so konfiguriert, dass Sie das ACTAS-Token an den Back-End-Dienst übergibt. Daniel hat diese Änderungen für die Anwendung implementiert.
3. Der Webdienst von "Webdienst" ist so konfiguriert, dass das ACTAS-Token durch Aufrufen von sts1 überprüft wird. Adam hat sts1 für die Verarbeitung von Delegierungs Anforderungen aktiviert.
4. Der Fabrikam-Benutzer Frank greift auf die Anwendung "Configuration Manager" zu und erhält Zugriff auf die Back-End-Ressourcen.

## <a name="set-up-the-identity-provider-ip"></a>Einrichten des Identitäts Anbieters (IP)

Es stehen drei Optionen für den fabrikam.com-Administrator offen:


1. Erwerben und installieren Sie ein STS-Produkt, z. b. Active Directory® Verbund Dienste (AD FS).
2. Abonnieren Sie ein Cloud STS-Produkt, z. b. LiveID STS.
3. Erstellen Sie einen benutzerdefinierten STS mithilfe von WIF.

In diesem Beispielszenario wird davon ausgegangen, dass Frank Option1 auswählt und AD FS als IP-STS installiert. Er konfiguriert außerdem einen Endpunkt mit dem Namen "\windowsauth", um die Benutzer zu authentifizieren. Durch den Verweis auf die AD FS Produktdokumentation und die Diskussion mit Adam, dem IT-Administrator von "IT", richtet Frank eine Vertrauensstellung mit der contoso.com-Domäne ein.

## <a name="set-up-the-claims-provider"></a>Einrichten des Anspruchs Anbieters

Die Optionen, die für den contoso.com-Administrator (Adam) verfügbar sind, sind die gleichen, die bereits für den Identitäts Anbieter beschrieben wurden. Für dieses Beispielszenario wird angenommen, dass Adam Option 1 auswählt und AD FS 2,0 als RP-STS installiert.

## <a name="set-up-trust-with-the-ip-and-application"></a>Einrichten der Vertrauensstellung mit der IP-Adresse und der Anwendung

Durch den Verweis auf die AD FS Dokumentation stellt Adam eine Vertrauensstellung zwischen fabrikam.com und der Anwendung her.

## <a name="set-up-delegation"></a>Einrichten der Delegierung

AD FS stellt die Delegierungs Verarbeitung bereit. Durch den Verweis auf die AD FS Dokumentation ermöglicht Adam die Verarbeitung von ACTAS-Token.

## <a name="application-specific-changes"></a>Anwendungsspezifische Änderungen

Die folgenden Änderungen müssen vorgenommen werden, um einer vorhandenen Anwendung Unterstützung für die Identitäts Delegierung hinzuzufügen. Daniel verwendet WIF, um diese Änderungen vorzunehmen.


- Zwischenspeichern des Bootstrap-Tokens, das web1 von sts1 empfangen hat.
- Verwenden Sie zum Erstellen eines Kanals zum Back-End-Webdienst "kreatechannelactingas" mit dem ausgestellten Token.
- Ruft die-Methode des Back-End-dienstanders auf.

## <a name="cache-the-bootstrap-token"></a>Das Bootstrap-Token Zwischenspeichern

Das Bootstrap-Token ist das anfängliche Token, das vom STS ausgegeben wird, und die Anwendung extrahiert Ansprüche daraus. In diesem Beispielszenario wird dieses Token von sts1 für den Benutzer veröffentlicht und in der Anwendung zwischengespeichert. Im folgenden Codebeispiel wird gezeigt, wie ein Bootstrap-Token in einer ASP.NET-Anwendung abgerufen wird:

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
WIF stellt eine Methode, " [kreatechannelactingas](https://msdn.microsoft.com/library/ee733863.aspx)", bereit, die einen Kanal des angegebenen Typs erstellt, der tokenausstellungsanforderungen mit dem angegebenen Sicherheits Token als ACTAS-Element erweitert. Sie können das Bootstrap-Token an diese Methode übergeben und dann die erforderliche Dienst Methode auf dem zurückgegebenen Kanal aufzurufen. In diesem Beispielszenario hat die Identität von Frank die [Actor](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.iclaimsidentity.actor.aspx) -Eigenschaft auf web1's Identity festgelegt.

Der folgende Code Ausschnitt zeigt, wie Sie den Webdienst mit " [tinatechannelactingas](https://msdn.microsoft.com/library/ee733863.aspx) " aufrufen und dann eine der Dienst Methoden "computeresponse" auf dem zurückgegebenen Kanal aufrufen:

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
## <a name="web-service-specific-changes"></a>Webdienst spezifische Änderungen

Da der Webdienst mit WCF erstellt und für WIF aktiviert ist, wird nach der Konfiguration der Bindung mit IssuedSecurityTokenParameters und der richtigen Aussteller Adresse die Überprüfung der ACTAS automatisch von WIF durchgeführt. 

Der Webdienst macht die spezifischen Methoden verfügbar, die für die Anwendung erforderlich sind. Es gibt keine spezifischen Codeänderungen, die für den Dienst erforderlich sind. Das folgende Codebeispiel zeigt die Konfiguration des Webdiensts mit IssuedSecurityTokenParameters:

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
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
