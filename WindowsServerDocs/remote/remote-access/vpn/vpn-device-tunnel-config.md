---
title: Konfigurieren des VPN-Geräte Tunnels in Windows 10
description: Erfahren Sie, wie Sie in Windows 10 einen VPN-Geräte Tunnel erstellen.
ms.prod: windows-server
ms.date: 11/05/2018
ms.technology: networking-ras
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.openlocfilehash: 3cb02bf2ca6aa254a0f1895367abdb90c5c34e6a
ms.sourcegitcommit: c1a5e46f64f25e1a0e658721130d87661b1d59a3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/20/2020
ms.locfileid: "86543384"
---
# <a name="configure-vpn-device-tunnels-in-windows-10"></a>Konfigurieren von VPN-Geräte Tunneln in Windows 10

>Gilt für: Windows 10, Version 1709

Always on-VPN bietet Ihnen die Möglichkeit, ein dediziertes VPN-Profil für das Gerät oder den Computer zu erstellen. Always On-VPN-Verbindungen umfassen zwei Typen von Tunneln: 

- Der _Geräte Tunnel_ stellt eine Verbindung mit angegebenen VPN-Servern her, bevor sich Benutzer am Gerät anmelden. Ein Gerätetunnel wird für Verbindungsszenarios vor der Anmeldung und zur Geräteverwaltung verwendet.

- Der _Benutzer Tunnel_ stellt nur dann eine Verbindung her, nachdem sich ein Benutzer am Gerät angemeldet hat. Mit dem Benutzertunnel können Benutzer über VPN-Server auf Organisationsressourcen zugreifen.

Anders als bei einem _Benutzer Tunnel_, der nur eine Verbindung herstellt, nachdem sich ein Benutzer am Gerät oder Computer anmeldet, ermöglicht der _Geräte Tunnel_ dem VPN das Herstellen von Verbindungen, bevor sich der Benutzer anmeldet. Sowohl _Geräte Tunnel_ als auch _Benutzer Tunnel_ arbeiten unabhängig von Ihren VPN-Profilen, können gleichzeitig verbunden werden und können gegebenenfalls verschiedene Authentifizierungsmethoden und andere VPN-Konfigurationseinstellungen verwenden. Der Benutzer Tunnel unterstützt SSTP und IKEv2, und der Geräte Tunnel unterstützt IKEv2 nur ohne Unterstützung für das SSTP-Fallback.

Der Benutzer Tunnel wird auf in die Domäne eingebundenen, nicht in die Domäne eingebundenen (Arbeitsgruppen) oder Azure AD Geräte unterstützt, die für Unternehmens-und BYOD-Szenarien geeignet sind. Es ist in allen Windows-Editionen verfügbar, und die Plattformfunktionen stehen Drittanbietern mithilfe von UWP-VPN-Plug-in-Unterstützung zur Verfügung.

Der Geräte Tunnel kann nur auf in die Domäne eingebundenen Geräten konfiguriert werden, auf denen Windows 10 Enterprise oder Education Version 1709 oder höher ausgeführt wird. Die Kontrolle des Geräte Tunnels durch Drittanbieter wird nicht unterstützt. Der Geräte Tunnel bietet keine Unterstützung für die Verwendung der Richtlinien Tabelle für die Namensauflösung. Der Geräte Tunnel unterstützt keine Tunnel Erzwingungen. Sie müssen ihn als Split Tunnel konfigurieren.


## <a name="device-tunnel-requirements-and-features"></a>Anforderungen und Features für den Geräte Tunnel
Sie müssen die Computer Zertifikat Authentifizierung für VPN-Verbindungen aktivieren und eine Stamm Zertifizierungsstelle für die Authentifizierung eingehender VPN-Verbindungen definieren. 

```PowerShell
$VPNRootCertAuthority = "Common Name of trusted root certification authority"
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like "*$VPNRootCertAuthority*" })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![Geräte Tunnel Features und-Anforderungen](../../media/device-tunnel-feature-and-requirements.png)

## <a name="vpn-device-tunnel-configuration"></a>Konfiguration des VPN-Geräte Tunnels

Die Beispiel-XML-Datei unten bietet eine gute Anleitung für Szenarien, in denen nur vom Client initiierte Pull-Vorgänge über den Geräte Tunnel erforderlich sind.  Datenverkehrs Filter werden genutzt, um den Geräte Tunnel nur auf den Verwaltungs Datenverkehr zu beschränken.  Diese Konfiguration eignet sich gut für Windows Update, typische Gruppenrichtlinie (GP) und Microsoft Endpoint Configuration Manager Update Szenarios sowie VPN-Konnektivität für die erste Anmeldung ohne zwischengespeicherte Anmelde Informationen oder Szenarios zur Kenn Wort Zurücksetzung. 

Für Server initiierte pushfälle, wie Windows-Remoteverwaltung (WinRM), Remote-gpupdate und Remote Configuration Manager Update Szenarios – Sie müssen eingehenden Datenverkehr für den Geräte Tunnel zulassen, sodass keine Datenverkehrs Filter verwendet werden können.  Wenn Sie im Geräte Tunnel Profildaten Verkehrs Filter aktivieren, wird der eingehende Datenverkehr vom Geräte Tunnel verweigert.  Diese Einschränkung wird in zukünftigen Versionen entfernt.


### <a name="sample-vpn-profilexml"></a>Beispiel-VPN-profileXML

Im folgenden finden Sie ein Beispiel für die VPN-Profilerstellung.

``` xml
<VPNProfile>  
  <NativeProfile>  
<Servers>vpn.contoso.com</Servers>  
<NativeProtocolType>IKEv2</NativeProtocolType>  
<Authentication>  
  <MachineMethod>Certificate</MachineMethod>  
</Authentication>  
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>  
 <!-- disable the addition of a class based route for the assigned IP address on the VPN interface -->
<DisableClassBasedDefaultRoute>true</DisableClassBasedDefaultRoute>  
  </NativeProfile> 
  <!-- use host routes(/32) to prevent routing conflicts -->  
  <Route>  
<Address>10.10.0.2</Address>  
<PrefixSize>32</PrefixSize>  
  </Route>  
  <Route>  
<Address>10.10.0.3</Address>  
<PrefixSize>32</PrefixSize>  
  </Route>  
<!-- traffic filters for the routes specified above so that only this traffic can go over the device tunnel --> 
  <TrafficFilter>  
<RemoteAddressRanges>10.10.0.2, 10.10.0.3</RemoteAddressRanges>  
  </TrafficFilter>
<!-- need to specify always on = true --> 
  <AlwaysOn>true</AlwaysOn> 
<!-- new node to specify that this is a device tunnel -->  
 <DeviceTunnel>true</DeviceTunnel>
<!--new node to register client IP address in DNS to enable manage out -->
<RegisterDNS>true</RegisterDNS>
</VPNProfile>
```

Abhängig von den Anforderungen der einzelnen Bereitstellungs Szenarios ist ein weiteres VPN-Feature, das mit dem Geräte Tunnel konfiguriert werden kann, die [Erkennung vertrauenswürdiger Netzwerke](https://social.technet.microsoft.com/wiki/contents/articles/38546.new-features-for-vpn-in-windows-10-and-windows-server-2016.aspx#Trusted_Network_Detection).

```
 <!-- inside/outside detection -->
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

## <a name="deployment-and-testing"></a>Bereitstellung und Testen

Sie können Geräte Tunnel mithilfe eines Windows PowerShell-Skripts und mithilfe der Windows-Verwaltungsinstrumentation (WMI)-Bridge konfigurieren. Der Always on VPN-Geräte Tunnel muss im Kontext des **lokalen System** Kontos konfiguriert werden. Um dies zu erreichen, muss [PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec)verwendet werden, eines der in der [Sysinternals](https://docs.microsoft.com/sysinternals/) -Dienstprogramme enthaltenen [phocker](https://docs.microsoft.com/sysinternals/downloads/pstools) .

Richtlinien für die Bereitstellung eines pro-Gerät-oder `(.\Device)` pro-Benutzer `(.\User)` Profils finden [Sie unter Verwenden von PowerShell-Skripts mit dem WMI-Bridge Anbieter](https://docs.microsoft.com/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider).

Führen Sie den folgenden Windows PowerShell-Befehl aus, um zu überprüfen, ob ein Geräte Profil erfolgreich bereitgestellt wurde:

  ```powershell
  Get-VpnConnection -AllUserConnection
  ```

In der Ausgabe wird eine Liste der Geräte \- weiten VPN-Profile angezeigt, die auf dem Gerät bereitgestellt werden.

### <a name="example-windows-powershell-script"></a>Windows PowerShell-Beispielskript

Sie können das folgende Windows PowerShell-Skript verwenden, um ein eigenes Skript für die Profilerstellung zu erstellen.

```PowerShell
Param(
[string]$xmlFilePath,
[string]$ProfileName
)

$a = Test-Path $xmlFilePath
echo $a

$ProfileXML = Get-Content $xmlFilePath

echo $XML

$ProfileNameEscaped = $ProfileName -replace ' ', '%20'

$Version = 201606090004

$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'

$nodeCSPURI = './Vendor/MSFT/VPNv2'
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"

$session = New-CimSession

try
{
$newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", 'String', 'Property')
$newInstance.CimInstanceProperties.Add($property)

$session.CreateInstance($namespaceName, $newInstance)
$Message = "Created $ProfileName profile."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}
$Message = "Complete."
Write-Host "$Message"
```

## <a name="additional-resources"></a>Weitere Ressourcen

Im folgenden finden Sie weitere Ressourcen zur Unterstützung Ihrer VPN-Bereitstellung.

### <a name="vpn-client-configuration-resources"></a>VPN-Client Konfigurations Ressourcen

Im folgenden finden Sie VPN-Client Konfigurations Ressourcen.

- [Erstellen von VPN-Profilen in Configuration Manager](https://docs.microsoft.com/configmgr/protect/deploy-use/create-vpn-profiles)
- [Konfigurieren von Windows 10-Client Always on-VPN-Verbindungen](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN-Profiloptionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options)

### <a name="remote-access-server-gateway-resources"></a>Remote Zugriffs-Server Gateway-Ressourcen

Im folgenden finden Sie RAS-gatewayressourcen (Remote Access Server).

- [Konfigurieren von RRAS mit einem Computer Authentifizierungszertifikat](https://technet.microsoft.com/library/dd458982.aspx)
- [Problembehandlung IKEv2 VPN-Verbindungen](https://technet.microsoft.com/library/dd941612.aspx)
- [Konfigurieren des IKEv2-basierten Remote Zugriffs](https://technet.microsoft.com/library/ff687731.aspx)

>[!IMPORTANT]
>Wenn Sie den Geräte Tunnel mit einem Microsoft RAS-Gateway verwenden, müssen Sie den RRAS-Server für die Unterstützung der IKEv2-Computer Zertifikat Authentifizierung konfigurieren, indem Sie die Authentifizierungsmethode " **Computer Zertifikat Authentifizierung für IKEv2 zulassen** " aktivieren, wie [hier](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee922682%28v=ws.10%29)beschrieben. Wenn diese Einstellung aktiviert ist, wird dringend empfohlen, dass das PowerShell-Cmdlet **Set-vpnauthprotocol** zusammen mit dem optionalen Parameter **rootcertifikatenametoaccept** verwendet wird, um sicherzustellen, dass RRAS-IKEv2-Verbindungen nur für VPN-Client Zertifikate zulässig sind, die mit einer explizit definierten internen/privaten Stamm Zertifizierungsstelle verkettet sind. Alternativ dazu sollte der Speicher für **Vertrauenswürdige Stamm Zertifizierungs** stellen auf dem RRAS-Server geändert werden, um sicherzustellen, dass er keine öffentlichen Zertifizierungsstellen enthält, wie [hier](https://blogs.technet.microsoft.com/rrasblog/2009/06/10/what-type-of-certificate-to-install-on-the-vpn-server/)erläutert. Ähnliche Methoden müssen möglicherweise auch für andere VPN-Gateways in Erwägung gezogen werden.
